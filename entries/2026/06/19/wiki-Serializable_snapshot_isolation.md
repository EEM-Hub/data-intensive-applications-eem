---
source: sources/wiki-Serializable_snapshot_isolation.md
source_url: https://en.wikipedia.org/wiki/Serializable_snapshot_isolation
---

## Snapshot Isolation in Databases

Snapshot isolation (SI) is a transaction isolation guarantee where all reads within a transaction see a consistent snapshot of the database as it existed at transaction start, and the transaction commits only if its writes don't conflict with concurrent writes made since that snapshot. It is widely adopted because it offers better performance than full serializability while avoiding most concurrency anomalies. SI is implemented within multiversion concurrency control (MVCC), which maintains multiple versions of each data item to allow concurrent reads and writes without blocking.

## Key Concepts

- **Snapshot**: Each transaction operates on a private, point-in-time view of the database taken at transaction start — it reads the last committed values as of that moment.
- **Write-write conflict detection**: A transaction aborts if any value it updated was also changed by another committed transaction since the snapshot was taken — this is the sole conflict detection mechanism.
- **Write skew anomaly**: Two transactions concurrently read overlapping data, make disjoint updates, and both commit — neither sees the other's write. This violates constraints that span multiple rows but is permitted under SI because no single row has a write-write conflict.
- **SI vs. serializability**: SI avoids all anomalies defined in ANSI SQL-92 (dirty reads, non-repeatable reads, phantoms) yet is **not** serializable — write skew is the distinguishing anomaly.
- **MVCC as implementation substrate**: MVCC maintains generational versions of objects; SI is a natural isolation level within MVCC systems because consistent snapshots are already available.
- **Serializable Snapshot Isolation (SSI)**: An extension (Cahill et al., 2008) that detects "dangerous" triplets of concurrent transactions to prevent write skew, achieving true serializability on top of MVCC. Adopted in PostgreSQL 9.1+.

## Commands and Syntax

No specific CLI commands, but important SQL-level patterns:

- **Materializing conflicts** — create a summary table that both transactions must update, converting a hidden cross-row constraint into a direct write-write conflict:
  ```sql
  -- Add a total_balance row that both T1 and T2 must update
  UPDATE totals SET balance = balance - 200 WHERE person = 'Phil';
  ```
- **Promoting reads to writes** — force a write-write conflict by "updating" a value to itself:
  ```sql
  -- T2 promotes its read of V1 to a write
  SELECT V1 FROM accounts WHERE person = 'Phil' FOR UPDATE;
  -- Or: UPDATE accounts SET V1 = V1 WHERE person = 'Phil';
  ```
- **Oracle/PostgreSQL terminology**: Oracle calls SI "serializable" mode. PostgreSQL called it "serializable" before 9.1; from 9.1 onward, the `SERIALIZABLE` level uses SSI (true serializability).

## Relationships

- **Multiversion Concurrency Control (MVCC)**: SI is implemented on top of MVCC; understanding MVCC's version chains and garbage collection is prerequisite.
- **Serializability**: SI is strictly weaker — it permits write skew. SSI bridges the gap.
- **ANSI SQL Isolation Levels**: SI exposed flaws in the SQL-92 standard's anomaly-based definitions; Berenson et al. (1995) used SI as the central critique.
- **Transaction processing**: SI is one strategy within the broader design space of concurrency control (pessimistic locking, optimistic concurrency, MVCC).
- **Database normalization**: The materialization workaround for write skew introduces redundant data, violating normal forms — a design trade-off.
- **Write-write conflicts vs. read-write conflicts**: SI only detects write-write conflicts; serializability must also account for read-write dependencies (rw-antidependencies), which SSI tracks.

## Exam-Relevant Points

- **SI permits write skew but prevents dirty reads, non-repeatable reads, and phantoms** — know exactly which anomalies it does and does not prevent.
- **The bank account example**: Two concurrent withdrawals each pass the constraint check against the snapshot but together violate the invariant V1 + V2 >= 0. This is the canonical write skew illustration.
- **Two workarounds for write skew**: (1) materialize the conflict via a summary table, (2) promote a read to a write (SELECT FOR UPDATE or dummy UPDATE). Know the trade-offs — materialization violates normal forms; promotion may not always be possible.
- **Oracle labels SI as "serializable"** — a known terminological pitfall; it is not true serializability.
- **PostgreSQL 9.1 introduced SSI** (Serializable Snapshot Isolation), which detects dangerous structures among concurrent transactions to achieve true serializability within MVCC. SSI increases abort rates but eliminates the need for manual workarounds.
- **Key paper**: Berenson et al. (1995), "A Critique of ANSI SQL Isolation Levels" — foundational for understanding why SQL-92's anomaly definitions are insufficient.
- **First-write-wins rule**: Under SI, if two transactions write the same item, the first to commit wins and the second aborts — this is how write-write conflicts are resolved.
- **SSI trade-off**: More aborts (false positives on "dangerous" triplets) in exchange for guaranteed serializability without application-level workarounds.
