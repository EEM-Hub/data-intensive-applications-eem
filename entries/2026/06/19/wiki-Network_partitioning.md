---
source: sources/wiki-Network_partitioning.md
source_url: https://en.wikipedia.org/wiki/Network_partitioning
---

## Network Partitions in Distributed Systems

A network partition is the division of a computer network into isolated subnets, either intentionally (for optimization) or due to failure of network devices such as switches. When a partition occurs, nodes within each subnet can still communicate with each other, but cannot reach nodes in the other subnet. Distributed software must be designed to be **partition-tolerant** — continuing to function correctly even when partitions occur.

## Key Concepts

- **Network partition**: A split in a network where two or more groups of nodes become unable to communicate with each other, while intra-group communication remains intact.
- **Partition tolerance**: The ability of a system to continue operating correctly despite network partitions causing communication failures between subsystems.
- **Intentional vs. failure-induced partitions**: Partitions can be deliberate (to optimize subnets independently) or accidental (due to device failure).
- **Example scenario**: If nodes A and B are in one subnet and nodes C and D in another, a switch failure between them creates a partition — A and B still work and talk to each other, as do C and D, but cross-subnet communication is lost.

## Commands and Syntax

No specific commands or configuration syntax are described in this source. Network partitions are a network-level phenomenon addressed through system design rather than CLI operations.

## Relationships

- **CAP Theorem**: Partition tolerance is the "P" in CAP. The theorem states that a distributed system can provide at most two of three guarantees: **Consistency**, **Availability**, and **Partition Tolerance**. Since network partitions are unavoidable in practice, real systems must choose between consistency and availability during a partition.
- **Consistency (database systems)**: One of the trade-offs against partition tolerance — ensuring all nodes see the same data at the same time.
- **Availability**: The other trade-off — ensuring every request receives a response (success or failure).
- **Subnets / Subnetworks**: The building blocks that become isolated segments during a partition.
- **Network switches**: Hardware devices whose failure can cause partitions.

## Exam-Relevant Points

- A network partition does **not** mean nodes stop working — it means they lose the ability to communicate **across** the partition boundary.
- Partition tolerance is not optional in real distributed systems — partitions **will** happen; the design question is how the system responds (sacrifice consistency or availability).
- The CAP theorem frames partition tolerance as one of three properties, but in practice it is treated as a given, making the real choice between **CP** (consistent but may become unavailable) and **AP** (available but may return stale data).
- Stonebraker (2010) is a key reference linking network partitions to eventual consistency and CAP trade-offs in database systems.
