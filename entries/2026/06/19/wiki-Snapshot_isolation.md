---
source: sources/wiki-Snapshot_isolation.md
source_url: https://en.wikipedia.org/wiki/Snapshot_isolation
---

## Snapshot Isolation in Databases

Snapshot isolation (SI) is a transaction isolation guarantee where all reads within a transaction see a consistent snapshot of the database as it existed at transaction start, and the transaction commits only if its writes don't conflict with concurrent writes made since that snapshot. It is widely adopted because it offers better performance than full serializability while avoiding most concurrency anomalies. SI is implemented within multiversion concurrency control (MVCC), which maintains multiple versions of each data item.

## Key Concepts

- **Snapshot guarantee**: A transaction operates on a private snapshot taken at its start time, reading the last committed values as of that moment.
- **Write-write conflict detection**: A transaction aborts if any value it updated was also changed by another committed transaction since the snapshot was taken.
- **Write skew anomaly**: The characteristic anomaly SI permits — two transactions concurrently read overlapping data, make disjoint updates, and both commit, violating a constraint that serializability would enforce. SI detects write-write conflicts but not write-read conflicts across transactions.
- **MVCC relationship**: SI is naturally implemented within MVCC systems, which maintain generational versions of each data item. MVCC allows readers to proceed without blocking writers.
- **Not truly serializable**: Despite avoiding all anomalies defined in the ANSI SQL-92 standard (dirty reads, non-repeatable reads, phantom reads), SI is strictly weaker than serializability. This was used by Berenson et al. (1995) to critique the SQL standard's anomaly-based definition of isolation levels.
- **Terminology confusion**: Oracle and PostgreSQL (pre-9.1) label snapshot isolation as "serializable" mode, which is misleading since true serializability prevents write skew.

## Commands and Syntax

No specific CLI commands, but important configuration/usage patterns:

- **Oracle**: `SET TRANSACTION ISOLATION LEVEL SERIALIZABLE` — actually provides snapshot isolation, not true serializability.
- **PostgreSQL 9.1+**: `SET TRANSACTION ISOLATION LEVEL SERIALIZABLE` — provides Serializable Snapshot Isolation (SSI), which is true serializability built on top of SI.
- **MySQL (InnoDB)**: Uses consistent nonlocking reads (a form of SI) for `REPEATABLE READ` isolation level.
- **Materializing conflicts** (workaround): Create an explicit conflict table that both transactions update, forcing a write-write conflict where the constraint violation would otherwise go undetected.
- **Promotion** (workaround): Use `SELECT FOR UPDATE` (Oracle) or set a value to itself (`SET V1 = V1`) to promote a read to a write, creating an artificial write-write conflict.

## Relationships

- **Multiversion Concurrency Control (MVCC)**: SI is the natural isolation level for MVCC systems; MVCC provides the versioning infrastructure SI depends on.
- **Serializability**: SI is strictly weaker — it prevents dirty reads, non-repeatable reads, and phantoms but permits write skew. Serializable Snapshot Isolation (SSI) closes this gap.
- **ANSI SQL-92 Isolation Levels**: SI exposed the inadequacy of the SQL standard's anomaly-based definitions — it satisfies all listed anomaly prohibitions yet is not serializable.
- **Database normalization**: The "materialize the conflict" workaround introduces redundant data, violating normal forms — a tension between correctness and schema design.
- **Lock-based concurrency control**: The alternative to MVCC; the SQL-92 standard was written assuming lock-based systems, making it a poor fit for MVCC/SI systems.

## Exam-Relevant Points

- **Write skew is the defining anomaly of SI**: Two transactions read overlapping data, write to disjoint items, and both commit — violating a cross-item constraint. The bank balance example (Phil withdrawing $200 from each of two accounts, both succeeding under SI but not under serializability) is the canonical illustration.
- **SI avoids all SQL-92 anomalies but is not serializable** — this is the key insight from Berenson et al. (1995) and a likely exam question framing.
- **Two workarounds for write skew**: (1) materialize the conflict via an auxiliary table, (2) promote reads to writes via `SELECT FOR UPDATE` or self-assignment. Know the tradeoffs — materialization violates normalization; promotion may not always be possible.
- **Serializable Snapshot Isolation (SSI)**: Introduced by Cahill et al. (2008), adopted in PostgreSQL 9.1. Detects "dangerous" triplets of concurrent transactions and aborts to prevent write skew. Eliminates the need for manual workarounds at the cost of increased abort rates.
- **Oracle calls SI "serializable"** — this is a well-known terminology pitfall. Users must understand the distinction.
- **InterBase was the first known SI implementation** (1985), predating the formal definition. The concept arose from work on MVCC databases.
- **MVCC + locks**: Some systems (e.g., MarkLogic) combine MVCC with locks to achieve true serializability while retaining MVCC performance benefits.
