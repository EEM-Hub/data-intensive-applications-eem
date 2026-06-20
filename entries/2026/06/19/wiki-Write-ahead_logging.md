---
source: sources/wiki-Write-ahead_logging.md
source_url: https://en.wikipedia.org/wiki/Write-ahead_logging
---

## Write-Ahead Logging (WAL)

Write-ahead logging is a family of techniques used in database systems to provide **atomicity** and **durability** — two of the four ACID properties. The core principle is simple: before any change is written to the database itself, it must first be recorded in an append-only log on stable storage. This guarantees that after a crash, the system can reconstruct or roll back incomplete operations by replaying the log.

## Key Concepts

- **WAL is append-only and disk-resident** — it serves as an auxiliary structure specifically for crash and transaction recovery.
- **Log-before-write rule**: every operation modifying database state must be logged to stable storage *before* the actual database pages are modified. This is the fundamental invariant.
- **The log stores both redo and undo information** — redo records allow replaying committed operations; undo records allow rolling back incomplete ones.
- **Page cache buffering**: WAL allows the page cache to buffer updates to disk-resident pages without sacrificing durability. Dirty pages don't need to be flushed immediately.
- **In-place updates**: WAL enables modifying data where it lives, which avoids the overhead of updating indexes and block lists (contrast with shadow paging, which copies-on-write).
- **Checkpointing**: periodically, all changes described in the WAL are flushed to the database and the log is cleared. This bounds recovery time and reclaims log space.
- **Shadow paging** is the alternative to WAL for atomic updates — it is not in-place and requires more index/block-list maintenance.

## Commands and Syntax

No specific commands are defined in this source. In practice, WAL configuration is system-specific:

- **PostgreSQL**: WAL is documented under `wal-intro` in the PostgreSQL docs; configuration parameters include `wal_level`, `fsync`, `synchronous_commit`, `checkpoint_timeout`.
- **SQLite**: Uses WAL mode via `PRAGMA journal_mode=WAL;`
- General pattern: the database engine handles WAL transparently; operators configure checkpoint frequency and log retention.

## Relationships

- **ACID properties** — WAL specifically provides the A (atomicity) and D (durability) guarantees.
- **ARIES** (Algorithms for Recovery and Isolation Exploiting Semantics) — the most widely referenced WAL-based recovery algorithm; uses LSNs, fuzzy checkpointing, and a three-phase recovery process (analysis, redo, undo).
- **Shadow paging** — the main alternative to WAL; trades in-place update efficiency for simpler crash recovery semantics.
- **Journaling file systems** — file systems (ext4, NTFS, XFS) use WAL variants for metadata consistency, applying the same log-before-write principle at the filesystem layer.
- **Checkpointing** — the mechanism that bounds WAL growth and recovery time by synchronizing logged changes to the database.
- **Page cache / buffer pool** — WAL decouples the buffer pool's flush policy from durability requirements; dirty pages can remain cached because the log guarantees recoverability.

## Exam-Relevant Points

- WAL provides **atomicity and durability**, not isolation or consistency — know which ACID properties it covers.
- The strict ordering rule: **log records must reach stable storage before the corresponding data pages are modified on disk**. This is the write-ahead guarantee.
- WAL enables **in-place updates**; shadow paging does **not** — and in-place updates reduce index and block list modifications.
- After a crash, recovery compares the log against the database state to decide whether to **redo** (complete), **undo** (roll back), or leave operations as-is.
- **Checkpoints** flush WAL contents to the database and truncate the log — they are essential for bounding recovery time.
- ARIES is the canonical WAL-family algorithm — expect questions linking WAL to ARIES.
- File system journaling is a WAL variant applied to **metadata** — this is a common cross-domain question linking databases to OS concepts.
