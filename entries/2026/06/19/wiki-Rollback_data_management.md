---
source: sources/wiki-Rollback_data_management.md
source_url: https://en.wikipedia.org/wiki/Rollback_(data_management)
---

## Rollback Operations in Databases

A rollback is a database operation that restores the database to a previous consistent state by undoing changes made by one or more transactions. Rollbacks are fundamental to database integrity and crash recovery — if a server crashes mid-transaction, rolling back all active transactions returns the database to a consistent state. Rollbacks are typically implemented via a transaction log or multiversion concurrency control (MVCC).

## Key Concepts

- **Rollback** — reverses all data changes made since the last `BEGIN`/`START TRANSACTION`, restoring prior state
- **Transaction log** — the primary mechanism for implementing rollbacks; records changes so they can be undone
- **MVCC** — an alternative rollback implementation that maintains multiple versions of data concurrently
- **Cascading rollback** — when one transaction's failure forces dependent transactions to also roll back; undesirable in practice
- **Cascadeless rollback** — practical recovery techniques guarantee this property, preventing cascade propagation
- **Connection-scoped** — in most SQL dialects, a rollback affects only the connection that issued it, not other concurrent connections; essential for correct concurrency
- **Savepoints** — a `ROLLBACK` releases any existing savepoints in use
- **Applicability beyond databases** — any stateful distributed system (message queues, workflow engines) can use rollback to maintain consistency

## Commands and Syntax

```sql
-- Begin a transaction
START TRANSACTION;
-- or
BEGIN;

-- Undo all changes since the transaction started
ROLLBACK;
```

- `ROLLBACK` discards all changes since the last `START TRANSACTION` or `BEGIN`
- Also releases any active savepoints
- Scope is per-connection, not global

## Relationships

- **Transaction log** — the data structure that makes rollback possible by recording before-images of changes
- **MVCC** — alternative implementation path; instead of undoing via log, old versions are retained
- **Commit** — the inverse of rollback; makes changes permanent
- **Savepoint** — allows partial rollback to a named point within a transaction rather than undoing everything
- **ACID properties** — rollback is the mechanism that enforces Atomicity (all-or-nothing) and supports Consistency
- **Concurrency control** — connection-scoped rollback is critical for isolation between concurrent transactions
- **Schema migration** — rollback concepts extend to reversing DDL changes in migration frameworks
- **Distributed systems** — rollback generalizes beyond RDBMS to any stateful system needing consistency (message queues, workflow systems)

## Exam-Relevant Points

- Rollback restores the database to the state before the current transaction's changes — it does not undo committed transactions
- Two implementation mechanisms: **transaction log** (most common) and **MVCC**
- Cascading rollback is when one transaction's abort forces dependent transactions to abort — production systems are designed to prevent this (cascadeless schedules)
- `ROLLBACK` is **connection-specific** — it does not affect other connections to the same database
- `ROLLBACK` releases existing savepoints
- Rollback is the key mechanism for crash recovery: roll back all transactions that were active at crash time
- The concept applies beyond databases to any stateful distributed system requiring consistency guarantees
