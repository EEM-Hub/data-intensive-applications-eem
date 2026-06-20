---
source: sources/wiki-CAP_theorem.md
source_url: https://en.wikipedia.org/wiki/CAP_theorem
---

## CAP Theorem (Brewer's Theorem)

The CAP theorem states that any distributed data store can provide at most two of three guarantees: **Consistency**, **Availability**, and **Partition tolerance**. Since network partitions are inevitable in distributed systems, the practical choice during a partition is between consistency and availability. Proposed by Eric Brewer in 1998–2000 and formally proven by Gilbert and Lynch in 2002.

## Key Concepts

- **Consistency (C)**: Every read receives the most recent write or an error. All clients see the same data at the same time, regardless of which node they connect to. Data must be replicated to all nodes before a write is deemed successful.
- **Availability (A)**: Every request to a non-failing node must result in a response, without guaranteeing it contains the most recent data. This is distinct from "high availability" in software architecture.
- **Partition tolerance (P)**: The system continues to operate despite arbitrary message loss or delay between nodes.
- CAP consistency is **not the same** as ACID consistency — they use the term differently.
- CAP availability is **not the same** as high availability — a system can be CAP-available but not highly available to end users.
- During normal operation (no partition), a system can satisfy all three guarantees simultaneously.
- The "pick two out of three" framing is misleading — the real choice is between C and A **only when a partition occurs**.

## Commands and Syntax

No commands or configuration syntax — CAP is a theoretical result. However, it manifests in database configuration choices:
- **CP systems** (choose consistency, sacrifice availability during partitions): Traditional RDBMS, MongoDB, Redis
- **AP systems** (choose availability, sacrifice consistency during partitions): CouchDB, Cassandra, ScyllaDB
- **CA classification**: Not meaningful for distributed systems — no NoSQL database is classified as CA because partitions cannot be avoided in practice
- Most modern distributed databases offer **configuration options** to tune the consistency/availability trade-off per operation

## Relationships

- **ACID vs BASE**: ACID-oriented systems (RDBMS) favor consistency; BASE-oriented systems (NoSQL) favor availability
- **PACELC theorem**: Extends CAP — even without partitions, there is a latency vs. consistency trade-off. "If Partition, choose A or C; Else, choose L or C"
- **Consensus protocols** (Paxos, Raft): Mechanisms CP systems use to maintain consistency across nodes
- **Replication**: The mechanism through which consistency is achieved — writes must propagate to all replicas
- **Sharding**: Geographic sharding can maintain availability for locally-owned data during partitions
- **Eventual consistency**: The model AP systems use — data converges over time but may be stale during reads
- **Fallacies of distributed computing**: CAP is a formal expression of one of these fallacies (the network is reliable)

## Exam-Relevant Points

- CAP was conjectured by **Eric Brewer (2000)**, formally proven by **Gilbert and Lynch (2002)**
- Network partitions are **unavoidable** — so the practical trade-off is always between C and A
- **CP examples**: MongoDB, Redis, traditional RDBMS
- **AP examples**: CouchDB, Cassandra, ScyllaDB
- **No distributed database is CA** — partition tolerance cannot be optional in a real network
- CAP consistency ≠ ACID consistency (different definitions)
- CAP availability ≠ high availability (different definitions)
- The "two out of three" framing is **oversimplified** — Brewer clarified this in 2012; you only sacrifice C or A during actual partitions
- **PACELC** is the more comprehensive theorem: adds the latency/consistency trade-off that exists even without partitions
- During **normal operation** (no partition), all three guarantees can be satisfied simultaneously
