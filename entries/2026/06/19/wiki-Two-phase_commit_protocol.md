---
source: sources/wiki-Two-phase_commit_protocol.md
source_url: https://en.wikipedia.org/wiki/Two-phase_commit_protocol
---

## Two-Phase Commit Protocol (2PC)

The two-phase commit protocol is a distributed algorithm and atomic commitment protocol that coordinates all participants in a distributed transaction to reach a unanimous decision on whether to commit or abort. It is the most widely used protocol for ensuring atomicity across multiple nodes, though it is a blocking protocol and cannot recover from all failure scenarios.

## Key Concepts

- **Atomic commitment protocol (ACP)**: 2PC is a specialized consensus protocol that guarantees all participants in a distributed transaction either all commit or all abort — no partial outcomes.
- **Coordinator and participants**: One node acts as the coordinator (master); all others are participants (cohorts/workers). The coordinator drives the protocol.
- **Phase 1 — Voting (commit-request)**: The coordinator asks all participants to prepare. Each participant executes the transaction locally, writes undo and redo log entries, then votes Yes (ready to commit) or No (must abort).
- **Phase 2 — Commit/Rollback (completion)**: If all participants voted Yes, the coordinator sends commit. If any voted No (or a timeout expires), the coordinator sends rollback. Participants act accordingly and acknowledge.
- **Blocking nature**: The protocol's greatest weakness. If the coordinator fails permanently after participants have voted Yes, those participants are stuck — they cannot unilaterally commit or abort and must wait indefinitely.
- **Unrecoverable double failure**: If both the coordinator and a participant fail during the commit phase, the system cannot determine whether the failed participant had already committed. A new coordinator must block until all members respond.
- **Write-ahead logging**: All protocol state transitions are forced to stable storage so that recovery procedures can determine the correct outcome after a crash.
- **2PC ≠ 2PL**: Two-phase commit (atomicity across nodes) is entirely distinct from two-phase locking (concurrency control within a database).

## Commands and Syntax

**Message flow between coordinator and participant:**

```
Coordinator                                          Participant
                             QUERY TO COMMIT
                 -------------------------------->
                             VOTE YES/NO             prepare*/abort*
                 <-------------------------------
commit*/abort*               COMMIT/ROLLBACK
                 -------------------------------->
                             ACKNOWLEDGEMENT          commit*/abort*
                 <--------------------------------  
end
```

Records marked with `*` are force-written to stable storage before the message is sent.

**Protocol assumptions required:**
1. Stable storage with write-ahead log at each node
2. No node crashes permanently (eventually recovers)
3. Write-ahead log data survives crashes without corruption
4. Any two nodes can communicate (possibly via rerouting)

## Relationships

- **Three-phase commit (3PC)**: A non-blocking extension of 2PC that adds a pre-commit phase to avoid the blocking problem when the coordinator fails.
- **Paxos / Raft**: General consensus algorithms that solve similar agreement problems but with stronger fault tolerance guarantees; often used as the underlying mechanism for coordinator election or as alternatives to 2PC.
- **Two Generals' Problem**: The theoretical impossibility result showing that no protocol can guarantee agreement over an unreliable channel — 2PC sidesteps this by assuming reliable stable storage and eventual recovery, not guaranteed message delivery.
- **Two-phase locking (2PL)**: A concurrency control mechanism (not a commit protocol) — frequently confused with 2PC but operates at a different level.
- **Transaction managers (TMs)**: The common implementation architecture uses dedicated TM components (e.g., X/Open XA) at each node that handle 2PC messaging on behalf of participants, making the protocol fully distributed.
- **Atomic commitment protocols**: 2PC is one instance; the same TM architecture supports other ACPs that share the voting-and-propagation pattern.

## Exam-Relevant Points

- 2PC guarantees atomicity but **is a blocking protocol** — this is its primary disadvantage and the most commonly tested fact.
- A coordinator-only failure is recoverable (if no commit message was sent, assume abort). A **simultaneous coordinator + participant failure during the commit phase is not safely recoverable** — this is the critical failure mode.
- The commit decision rule: commit **only if all participants vote Yes**; abort if **any** participant votes No or times out.
- **Presumed abort** optimization: if no commit evidence is found in the log during recovery, assume abort — saves logging of abort decisions.
- **Presumed commit** optimization: the inverse assumption, saving commit-path logging.
- **Tree 2PC** (nested/recursive): propagates messages along the transaction's invocation tree rather than star topology — reduces message count in hierarchical systems.
- **Dynamic 2PC (D2PC)**: no predetermined coordinator; agreement messages race from leaves inward, and the coordinator is determined at the collision point — achieves time-optimal commit for any tree topology.
- Force-writing log records to stable storage **before** sending protocol messages is essential for correctness — without this, crash recovery cannot determine the node's vote or decision.
- The protocol requires **all participants to respond** — a single unresponsive participant blocks the entire transaction, which is why timeout mechanisms trigger abort.
