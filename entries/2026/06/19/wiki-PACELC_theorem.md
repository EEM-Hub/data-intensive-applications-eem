---
source: sources/wiki-PACELC_theorem.md
source_url: https://en.wikipedia.org/wiki/PACELC_theorem
---

## PACELC Design Principle

PACELC extends the CAP theorem to address trade-offs in distributed systems even when no network partition exists. While CAP states that during a partition (P) you must choose between availability (A) and consistency (C), PACELC adds that **else (E)** — during normal operation — you must choose between **latency (L)** and **consistency (C)**. This makes PACELC a more comprehensive framework for reasoning about distributed database behavior at all times, not just during failure scenarios.

## Key Concepts

- **PACELC acronym**: Partition → Availability vs. Consistency; Else → Latency vs. Consistency
- **CAP is a subset**: CAP only addresses the partition case (PA or PC); PACELC adds the normal-operation trade-off (EL or EC)
- **Four configuration quadrants**:
  - **PA/EL** — favor availability and low latency always (e.g., Dynamo, Cassandra, Riak)
  - **PA/EC** — favor availability during partitions, consistency otherwise (rare; mostly in-memory data grids)
  - **PC/EL** — favor consistency during partitions, low latency otherwise (e.g., PNUTS); tricky — PC means "don't reduce consistency beyond baseline," not "fully consistent"
  - **PC/EC** — favor consistency always, paying availability and latency costs (e.g., VoltDB, PostgreSQL, HBase, Bigtable, MySQL Cluster)
- **Atomic consistency cost**: if a store is atomically consistent, the sum of read and write delay is at least one message delay; in practice, a full network round trip on both reads and writes
- **PA/EL and PC/EC are natural cognitive models**: PA/EL = high availability + low latency with relaxed consistency; PC/EC = strict ACID-style consistency
- **PA/EC and PC/EL are conditional guarantees**: developers must write code to handle cases where the guarantee doesn't hold
- **CAP is most relevant for intermittently connected environments** (IoT, mobile); PACELC is more appropriate for cloud/distributed systems where partitions are rare but latency/consistency trade-offs are constant
- Formally proved in 2018 by Wojciech Golab (SIGACT News)

## Commands and Syntax

No specific commands — PACELC is a theoretical design principle. However, many databases expose tunable consistency:
- **Dynamo, Cassandra, Riak**: user-adjustable settings to control the L/C trade-off
- **Cosmos DB**: five selectable consistency levels (strong, bounded staleness, session, consistent prefix, eventual)
- **DynamoDB**: default eventually consistent reads; optional strongly consistent reads per request
- **Couchbase**: configurable consistency and availability options both during and without partitions

## Relationships

- **Extends CAP theorem**: PACELC is a strict superset — CAP is the "PAC" portion
- **Connects to consistency models**: the C in ELC refers to the same consistency spectrum (eventual, causal, strong/linearizable)
- **Relates to replication strategy**: the ELC trade-off arises specifically from how systems replicate data across nodes
- **ACID vs. BASE**: PC/EC systems align with ACID guarantees; PA/EL systems align with BASE (Basically Available, Soft state, Eventually consistent)
- **Consensus protocols**: Paxos and Raft are mechanisms that PC systems use to maintain consistency at the cost of latency
- **Lambda architecture**: one architectural response to these trade-offs
- **Fallacies of distributed computing**: PACELC formalizes one of the realities those fallacies warn about (the network is not infinitely fast or reliable)

## Exam-Relevant Points

- PACELC was formulated by **Daniel Abadi** (Yale, 2010 blog post, 2012 paper)
- CAP's main oversight according to Abadi: **ignoring the consistency/latency trade-off that exists at all times**, not just during partitions
- Know the PACELC classification of major databases:
  - **PA/EL**: Dynamo (internal), Cassandra, Riak, Cosmos DB (default)
  - **PC/EC**: VoltDB, Megastore, MySQL Cluster, PostgreSQL, Bigtable, HBase
  - **PA/EC**: MongoDB (baseline consistent reads/writes, available during partitions), Hazelcast IMDG
  - **PC/EL**: PNUTS
- **DynamoDB ≠ Dynamo**: DynamoDB uses a strong leader model with serialized writes; the original internal Dynamo was PA/EL
- **Cosmos DB is formally CP** — it never violates its specified consistency level, but offers five tunable levels for the L/C trade-off
- PC/EL does **not** mean fully consistent — it means the system doesn't reduce consistency below baseline during partitions (it reduces availability instead)
- PA/EC systems are rare outside in-memory data grids because in localized systems the latency/consistency trade-off is less significant
