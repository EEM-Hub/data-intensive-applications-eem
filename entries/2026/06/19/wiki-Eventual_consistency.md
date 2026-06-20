---
source: sources/wiki-Eventual_consistency.md
source_url: https://en.wikipedia.org/wiki/Eventual_consistency
---

## Eventual Consistency in Distributed Systems

Eventual consistency is a consistency model used in distributed computing to achieve high availability. It guarantees that if no new updates are made to a data item, all replicas will eventually converge to the same value. Also called optimistic replication, it originated in early mobile computing projects and is now widely deployed in distributed systems. It is a weak guarantee — stronger models like linearizability are trivially eventually consistent.

## Key Concepts

- **Eventual consistency**: All reads of a data item will eventually return the last updated value, provided no new updates are made. A system that reaches this state is said to have **converged** (achieved **replica convergence**).
- **BASE semantics** — the counterpart to ACID for eventually-consistent systems:
  - **Basically Available**: The database is concurrently accessible to all users at all times; no user must wait for another's transaction to complete.
  - **Soft-state**: Data can have transient/temporary states that change over time even without external input. Different queries may see different values until convergence.
  - **Eventually Consistent**: The record achieves consistency once all concurrent updates complete; all queries then return the same value.
- **Liveness vs. Safety**: Eventual consistency provides only a **liveness** guarantee (reads will *eventually* return the same value) but no **safety** guarantee — any intermediate value may be returned before convergence.
- **Strong Eventual Consistency (SEC)**: Adds a safety guarantee — any two nodes that have received the same (unordered) set of updates will be in the same state. Commonly achieved using **conflict-free replicated data types (CRDTs)**.
- **Anti-entropy**: The process of exchanging versions or updates between servers to synchronize replicas.
- **Reconciliation**: Choosing the appropriate final state when concurrent updates have occurred.

## Conflict Resolution Strategies

- **Last writer wins (LWW)**: The most widespread approach; the update with the latest timestamp takes precedence.
- **First writer wins**: Used when LWW is unacceptable (e.g., preventing overwrites of initial values).
- **User-specified conflict handler**: Application-defined logic invoked to resolve conflicts.
- **Concurrency detection tools**: Lamport timestamps and vector clocks are used to detect concurrent updates.

**Reconciliation timing** — when correction of inconsistencies occurs:
- **Read repair**: Inconsistency corrected during a read operation (slows reads).
- **Write repair**: Correction during a write operation (slows writes).
- **Asynchronous repair**: Correction happens in the background, outside read/write paths.

## Relationships

- **Consistency model spectrum**: Eventual consistency is the weakest useful model; linearizability and sequential consistency are strictly stronger. All stronger models are trivially eventually consistent.
- **CAP theorem**: Eventual consistency is the typical consistency tradeoff made to achieve availability and partition tolerance (AP systems).
- **ACID vs. BASE**: Traditional relational databases use ACID; distributed NoSQL systems (Cassandra, DynamoDB, Riak) typically provide BASE/eventual consistency.
- **CRDTs**: The primary mechanism for achieving strong eventual consistency without coordination.
- **Optimistic replication**: Eventual consistency is also known as optimistic replication — replicas accept updates independently and reconcile later.

## Exam-Relevant Points

- Eventual consistency guarantees convergence only in the absence of new updates — it is a **liveness** guarantee, not a safety guarantee.
- BASE stands for **Basically Available, Soft-state, Eventually consistent** — know each term's definition.
- **Strong eventual consistency (SEC)** adds a safety guarantee: same updates → same state, regardless of order. CRDTs are the standard approach to SEC.
- The three reconciliation timing strategies (read repair, write repair, asynchronous repair) and their performance tradeoffs are commonly tested.
- Conflict resolution approaches: last writer wins, first writer wins, application-defined handlers. Lamport timestamps and vector clocks detect concurrency.
- Anti-entropy is the term for the process of exchanging data between replicas to achieve convergence.
- Eventual consistency increases system availability but adds **cognitive complexity** for developers — bugs may only surface during network failures or high concurrency.
- Werner Vogels' 2009 paper "Eventually Consistent" (Communications of the ACM) is the canonical reference.
