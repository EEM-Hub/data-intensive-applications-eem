---
source: sources/wiki-Quorum_distributed_computing.md
source_url: https://en.wikipedia.org/wiki/Quorum_(distributed_computing)
---

## Quorum-Based Voting in Distributed Systems

Quorums define the minimum number of votes a distributed transaction must collect before it can commit or abort. This mechanism enforces consistency across distributed databases by ensuring conflicting operations (concurrent reads/writes, simultaneous commit and abort) cannot both succeed. Two primary applications exist: commit protocols that guarantee transaction atomicity during network partitions, and replica control protocols that maintain serializability across replicated data items.

## Key Concepts

- A **quorum** is the minimum vote threshold required to authorize an operation in a distributed system.
- Every site in the system is assigned a vote weight (Vi); votes need not be equal.
- **Commit quorum (Vc)**: minimum votes needed before a transaction can commit.
- **Abort quorum (Va)**: minimum votes needed before a transaction can abort.
- **Read quorum (Vr)**: minimum votes needed to read a replicated data item.
- **Write quorum (Vw)**: minimum votes needed to write a replicated data item.
- The constraint **Va + Vc > V** prevents a transaction from being simultaneously committed and aborted — the two quorums must overlap.
- For replica control (Gifford, 1979):
  - **Vr + Vw > V** ensures read and write quorums overlap, so a read always sees the latest version.
  - **Vw > V/2** ensures two concurrent writes cannot both succeed, preventing write-write conflicts.
- Quorum-based techniques handle **network partitioning** — only the partition that can assemble a quorum may proceed, preventing split-brain inconsistency.
- The approach guarantees **one-copy serializability** for replicated databases.

## Commands and Syntax

No CLI commands. The core formulas for implementing quorum rules:

```
# Commit protocol quorums
Va + Vc > V        (commit and abort quorums must overlap)
0 < Vc, Va ≤ V

# Replica control quorums (Gifford's weighted voting)
Vr + Vw > V        (read quorum overlaps write quorum)
Vw > V/2           (write quorum is a strict majority of votes)
```

Example: 5 replicas each with 1 vote (V=5). Setting Vr=2, Vw=4 satisfies both rules (2+4>5, 4>2.5). Reads are cheap (2 sites), writes are expensive (4 sites).

## Relationships

- **Distributed transactions**: quorums are a mechanism to implement atomicity across sites when network partitions make unanimous agreement impossible.
- **Replication**: quorum voting is a replica control method — an alternative to primary-copy or read-one/write-all protocols.
- **Network partitioning / CAP theorem**: quorums address the partition-tolerance requirement; only the majority partition can make progress, sacrificing availability in the minority partition.
- **Serializability**: the quorum rules for replica control enforce one-copy serializability, the correctness criterion for replicated databases.
- **Consensus protocols**: quorum intersection is the foundational principle behind Paxos, Raft, and other consensus algorithms.

## Exam-Relevant Points

- Know both quorum rule sets and what each constraint prevents:
  - Va + Vc > V → prevents simultaneous commit and abort.
  - Vr + Vw > V → read quorum always includes at least one node with the latest write.
  - Vw > V/2 → prevents concurrent conflicting writes.
- Gifford's weighted voting (1979) is the seminal work for quorum-based replica control.
- Quorum sizes are a tunable tradeoff: increasing Vr decreases Vw and vice versa, letting you optimize for read-heavy or write-heavy workloads.
- A commit quorum requires **at least one site prepared to commit** plus waiting sites totaling ≥ Vc; an abort quorum can consist entirely of waiting sites.
- Quorum-based voting works during network partitions because only the partition with enough votes can reach quorum — the minority partition blocks rather than diverging.
