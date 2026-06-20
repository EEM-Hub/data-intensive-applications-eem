---
source: sources/wiki-Isolation_database_systems.md
source_url: https://en.wikipedia.org/wiki/Isolation_(database_systems)
---

## Transaction Isolation Levels in Database Systems

Isolation is one of the four ACID properties governing database transactions. It defines how concurrent transactions interact — specifically, how the intermediate state of one transaction becomes visible to others. The core tradeoff is between concurrency (allowing more simultaneous access) and correctness (preventing anomalous reads). Lower isolation levels permit higher throughput but expose applications to phenomena like dirty reads, non-repeatable reads, and phantom reads; higher levels eliminate these anomalies at the cost of increased locking, reduced concurrency, and greater deadlock risk.

## Key Concepts

- **Isolation** determines transaction integrity visibility to other users and systems; it is the ACID property most often relaxed in practice.
- **Concurrency control** is the underlying DBMS mechanism that enforces isolation. Two primary strategies exist:
  - **Lock-based concurrency control** (e.g., two-phase locking): transactions acquire read/write locks on data objects; conflicting transactions block until locks are released. Provides serializability and recoverability.
  - **Multiversion concurrency control (MVCC)**: transactions operate on snapshots; no locks acquired, but write collisions cause one transaction to roll back. See also: snapshot isolation.
- **Three read phenomena** defined by ANSI SQL-92:
  - **Dirty read**: reading uncommitted data from another transaction that may later roll back.
  - **Non-repeatable read**: re-reading a row yields different data because another transaction committed an update between the two reads.
  - **Phantom read**: re-executing a range query yields a different set of rows because another transaction inserted or deleted rows matching the predicate.
- **Write skew**: two transactions read the same columns, then each writes to them based on stale reads, producing a mixed result. Possible under Repeatable Read in some systems.
- **Range locks**: locks on a range of index entries (not just individual rows); required at Serializable level to prevent phantom reads under lock-based implementations.
- A DBMS may run a transaction at a **stronger** isolation level than requested — the standard permits this.
- **Anomaly serializable != truly serializable**: being free of dirty reads, non-repeatable reads, and phantom reads is necessary but not sufficient for serializability.
- The ANSI SQL isolation definitions have been **criticized** as ambiguous, lock-centric, and not accurately capturing the behavior of real MVCC-based systems (Berenson et al., "A Critique of ANSI SQL Isolation Levels").

## Commands and Syntax

```sql
-- Setting isolation level (standard SQL)
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;
SET TRANSACTION ISOLATION LEVEL READ UNCOMMITTED;

-- Explicit locking (e.g., PostgreSQL/Oracle)
SELECT * FROM users WHERE id = 1 FOR UPDATE;  -- acquire exclusive write lock
```

**JDBC (Java):**
```java
connection.setTransactionIsolation(Connection.TRANSACTION_SERIALIZABLE);
int level = connection.getTransactionIsolation();
```

**Spring Framework:**
```java
@Transactional(isolation = Isolation.REPEATABLE_READ)
```

## Relationships

- **ACID properties**: Isolation is one of four (Atomicity, Consistency, Isolation, Durability) — often the first to be relaxed.
- **Two-phase locking (2PL)**: the most common mechanism for enforcing serializability in lock-based systems.
- **Snapshot isolation / MVCC**: alternative to locking; transactions see consistent snapshots but may encounter write conflicts at commit time.
- **Deadlocks**: higher isolation levels increase deadlock risk because more locks are held longer.
- **Serializability**: the correctness criterion that the highest isolation level guarantees — equivalent to some serial execution order.
- **Recoverability**: unlike serializability, recoverability cannot be compromised without risking database integrity violations.
- **Transaction managers / TPMs**: middleware that can enforce isolation across distributed tiers (relevant to multi-tier architectures).
- **Optimistic concurrency control**: a non-lock-based alternative related to MVCC approaches.

## Exam-Relevant Points

- **Isolation levels matrix** — memorize which phenomena each level prevents:

| Isolation Level | Dirty Read | Non-repeatable Read | Phantom Read |
|---|---|---|---|
| **Serializable** | No | No | No |
| **Repeatable Read** | No | No | Yes |
| **Read Committed** | No | Yes | Yes |
| **Read Uncommitted** | Yes | Yes | Yes |

- **Serializable** requires range-locks (lock-based) or write-collision detection (MVCC) — it is the only level that prevents all three phenomena.
- **Repeatable Read** holds read and write locks until end of transaction but does **not** manage range-locks, hence phantom reads can still occur.
- **Read Committed** releases read locks immediately after the SELECT completes; write locks are held until commit.
- **Read Uncommitted** is the lowest level — permits dirty reads of uncommitted data.
- **Default isolation levels vary by DBMS** — e.g., PostgreSQL defaults to Read Committed, MySQL/InnoDB defaults to Repeatable Read, Oracle defaults to Read Committed, SQL Server defaults to Read Committed.
- Being free of all three ANSI phenomena is **necessary but not sufficient** for true serializability.
- **Write skew** is a phenomenon not covered by the three ANSI phenomena; it can occur under Repeatable Read and is only prevented at Serializable level.
- **Two-phase locking** provides both serializability and recoverability — the most common concurrency control method in commercial DBMSs.
- The ANSI SQL isolation definitions are **criticized for being lock-biased** and ambiguous — real MVCC implementations may provide different guarantees than the ANSI names suggest.
