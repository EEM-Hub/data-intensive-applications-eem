---
source: sources/wiki-Split-brain_computing.md
source_url: https://en.wikipedia.org/wiki/Split-brain_(computing)
---

## Split-Brain in Distributed Systems

Split-brain is a failure condition in distributed computing where a cluster's nodes lose communication with each other and begin operating independently, each believing it is the sole active node. This leads to divergent data sets, potential data corruption, and availability inconsistencies. The term derives from the medical split-brain syndrome and is closely related to the concept of a network partition.

## Key Concepts

- **Split-brain** occurs when cluster nodes cannot communicate (e.g., all heartbeat links fail) but continue running independently, each serving clients with its own divergent data set.
- It is fundamentally a consequence of a **network partition** — nodes are alive but cannot synchronize.
- **Split-brain DNS** (split-horizon DNS) is a *deliberate* design where internal and external DNS services maintain separate namespaces — not an error state, but carries risk of FQDN ambiguity if domains overlap.
- **High-availability clusters** use **heartbeat networks** to monitor node health; split-brain occurs when these heartbeat links all fail simultaneously.
- Split-brain can cause **data corruption** or inconsistencies requiring manual operator intervention and cleanup.
- **Two-node clusters** are especially vulnerable — without a quorum witness, there is at least a 50% chance the cluster fails entirely when heartbeat is lost, because neither node can determine which should be active.

## Approaches for Dealing with Split-Brain

- **Optimistic approach**: Let partitioned nodes continue operating normally. Prioritizes **availability over consistency**. Requires automatic or manual reconciliation after the partition heals. Example: Hazelcast (automatic key-value store reconciliation).
- **Pessimistic approach**: Restrict access to sub-partitions to preserve **consistency over availability**. Typically uses a **quorum-consensus** mechanism — the sub-partition with a majority of votes stays active; minority partitions auto-fence (shut themselves down). Examples: MongoDB replica sets, Galera replication (MariaDB/MySQL).
- **Modern HA clusters**: Combine heartbeat network connections with a **quorum witness** (a third-party tiebreaker, possibly cloud-hosted) to avoid the two-node ambiguity problem.

## Commands and Syntax

No specific commands; this is a conceptual/architectural topic. Relevant operational considerations:
- Configure heartbeat networks with redundancy (multiple independent links) to reduce split-brain risk.
- Deploy quorum witness devices for two-node clusters.
- Implement fencing (STONITH — "Shoot The Other Node In The Head") to ensure only one partition remains active.

## Relationships

- **Network partitions (CAP theorem)**: Split-brain is the practical manifestation of a partition event. The CAP theorem states that during a partition, a system must choose between consistency and availability — directly mapping to the pessimistic vs. optimistic approaches.
- **Consensus protocols**: Quorum-based approaches (Raft, Paxos) are the primary mechanism for preventing split-brain in leader-based systems.
- **Replication**: Split-brain is a core failure mode for replicated databases — it determines whether a replica set can accept writes during a partition.
- **Fencing**: The mechanism by which minority partitions are forcibly isolated to prevent divergent writes.
- **High-availability clustering**: Split-brain is the central failure mode that HA cluster designs must address.
- **Conflict resolution / CRDTs**: Optimistic approaches that allow divergent writes need merge strategies (last-writer-wins, vector clocks, CRDTs) for reconciliation.

## Exam-Relevant Points

- Split-brain = nodes operate independently after losing communication, leading to divergent data sets.
- **Optimistic** = higher availability, risk of inconsistency, requires reconciliation.
- **Pessimistic** = higher consistency, uses quorum voting, minority partitions fence themselves.
- Two-node clusters without a quorum witness have at least **50% probability of total failure** when heartbeat is lost.
- MongoDB uses pessimistic (quorum-based) approach; Hazelcast uses optimistic (auto-reconciliation) approach.
- Split-brain DNS is a **deliberate design choice**, not an error — separate internal/external DNS namespaces.
- The Davidson et al. (1985) survey is the canonical classification of partition-handling approaches into optimistic and pessimistic categories.
- Quorum requires a **majority** of votes — this is why odd-numbered node counts or witness devices are preferred in cluster design.
