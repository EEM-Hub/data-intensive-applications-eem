---
source: sources/wiki-Three-phase_commit_protocol.md
source_url: https://en.wikipedia.org/wiki/Three-phase_commit_protocol
---

## Three-Phase Commit Protocol (3PC)

The three-phase commit protocol is a distributed algorithm for achieving consensus on whether to commit or abort a transaction across all nodes in a distributed system. It extends the two-phase commit protocol (2PC) by adding an intermediate "Prepared to commit" phase that eliminates the possibility of indefinite blocking when both the coordinator and a cohort member fail during the commit phase.

## Key Concepts

- **Core problem solved**: 2PC can block indefinitely if both the coordinator and a cohort member fail during the Commit phase, because the recovery coordinator cannot determine whether the failed cohort had already committed.
- **Prepared to commit state**: The key innovation — an intermediate phase between voting and committing that ensures no node can commit before all nodes are aware of the decision.
- **Three phases**: (1) CanCommit (voting), (2) PreCommit (prepared to commit), (3) DoCommit (actual commit).
- **Recovery guarantee**: If the coordinator fails before sending PreCommit messages, all cohorts agree the operation was aborted. If some nodes are in the commit phase, the recovery coordinator knows the decision was to commit.
- **Non-blocking property**: Unlike 2PC, surviving nodes can always reach a safe decision without waiting for failed nodes to recover.
- **Bounded delay assumption**: 3PC assumes bounded network delay and bounded node response times — it cannot guarantee atomicity in systems with unbounded delays or process pauses.

## Commands and Syntax

No specific commands — this is a protocol specification. The message flow is:

1. **Phase 1 (CanCommit)**: Coordinator sends `canCommit?` → Cohorts respond `Yes/No`
2. **Phase 2 (PreCommit)**: Coordinator sends `preCommit` → Cohorts ACK with `Prepared to commit`
3. **Phase 3 (DoCommit)**: Coordinator sends `doCommit` → Cohorts commit and ACK

Recovery coordinator logic:
- Query participants → if any node is in commit phase → shepherd to commit
- If any participant has not received PreCommit → safely abort

## Relationships

- **Extends two-phase commit (2PC)**: Adds a phase to solve 2PC's blocking problem during coordinator + cohort failure.
- **Related to Paxos**: Both are consensus algorithms, but Paxos is designed for fault tolerance in asynchronous networks, while 3PC assumes bounded delays.
- **E3PC (Keidar and Dolev)**: A refinement of Skeen's original 3PC that allows a quorum to always make progress even during network partitioning.
- **Practical relevance**: Rarely used in modern systems because the bounded-delay assumption doesn't hold in real networks — Paxos/Raft variants are preferred.

## Exam-Relevant Points

- 3PC adds a **PreCommit phase** between the vote and commit phases of 2PC — this is the single design change that enables non-blocking recovery.
- The specific 2PC failure scenario that 3PC solves: coordinator and a cohort fail simultaneously during commit, where the failed cohort may have been the only node that received and executed the commit.
- 3PC requires **at least 3 round trips (RTTs)**, making it higher latency than 2PC.
- 3PC **cannot guarantee atomicity** in systems with unbounded network delay and process pauses — this is a critical limitation that makes it impractical for most real-world distributed systems.
- The coordinator will not send `doCommit` until **all** cohort members have acknowledged `PreCommit` — this invariant is what prevents ambiguous states.
- Skeen's original 3PC can have a quorum that is connected but unable to make progress during network partitions (not a deadlock, but a liveness issue). E3PC solves this.
