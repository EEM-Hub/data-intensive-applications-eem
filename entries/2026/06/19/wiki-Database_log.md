---
source: sources/wiki-Database_log.md
source_url: https://en.wikipedia.org/wiki/Database_log
---

## Transaction Logs in Database Systems

Transaction logs (also called transaction journals, database logs, binary logs, or audit trails) are the mechanism by which database management systems record a history of all actions executed against the database. Their primary purpose is to guarantee ACID properties — specifically atomicity and durability — in the face of crashes or hardware failures. Physically, a transaction log is a file stored in stable storage that lists changes to the database.

## Key Concepts

- **Transaction log** — a chronological record of all changes made to a database, used for crash recovery
- **Recovery on startup** — if the database is in an inconsistent state after a crash, the DBMS reviews logs to: (1) roll back uncommitted transactions, and (2) re-apply committed transactions whose changes weren't yet materialized
- **Log Sequence Number (LSN)** — unique, monotonically increasing identifier for each log record; enables constant-time recovery (used by algorithms like ARIES)
- **Prev LSN** — each log record links to the previous record, forming a linked list structure
- **Before and After Images** — update log records may store the byte values of a page before and after modification (some systems store one or both)
- **Compensation Log Record (CLR)** — records the rollback of a specific update; contains `undoNextLSN` pointing to the next record to undo
- **Checkpoint Record** — snapshots that speed up recovery by eliminating the need to read far back in the log; contains `redoLSN` (where redo starts) and `undoLSN` (oldest in-progress transaction)
- **Distinction from human-readable logs** — transaction logs are not the same as the diagnostic/query logs a DBMS exposes to operators

## Commands and Syntax

No specific commands are given in this source. The content is structural/conceptual. However, the anatomy of a log record is defined as:

```
Log Record:
  LSN              — unique monotonically increasing ID
  Prev LSN         — pointer to previous log record (linked list)
  Transaction ID   — which transaction produced this record
  Type             — update, CLR, commit, abort, checkpoint, completion
  [type-specific fields]
```

**Update records** add: `PageID`, `Length`, `Offset`, `Before Image`, `After Image`

**CLR records** add: `undoNextLSN`

**Checkpoint records** add: `redoLSN`, `undoLSN`

## Relationships

- **ACID properties** — transaction logs are the implementation mechanism for atomicity (undo uncommitted work) and durability (redo committed work)
- **Write-Ahead Logging (WAL)** — the protocol requiring log records to be written to stable storage before the corresponding data pages; transaction logs are what WAL writes
- **ARIES algorithm** — a specific recovery algorithm that relies on LSN ordering and the log record types described here (update, CLR, checkpoint)
- **Journaling file systems** — apply the same concept at the filesystem level rather than the database level
- **Checkpoints** — interact with dirty page flushing policies (e.g., PostgreSQL flushes all dirty pages at checkpoint time)
- **Rollback / Commit** — the abort and commit record types in the log drive the DBMS's transaction outcome decisions during recovery

## Exam-Relevant Points

- Transaction logs guarantee **atomicity** and **durability** — know which two ACID properties they enforce and how (undo for atomicity, redo for durability)
- **LSNs are monotonically increasing** — this property is essential for recovery algorithms like ARIES
- Log records form a **linked list** via Prev LSN pointers
- A **CLR** corresponds to exactly one Update Log Record and contains `undoNextLSN` — know this 1:1 relationship
- **Checkpoint records** contain two critical LSNs: `redoLSN` (first dirty, unflushed update) and `undoLSN` (oldest active transaction) — these define the recovery window
- **Before and After Images** in update records — some systems store both, some store only one; this affects whether the system can support undo, redo, or both
- **Six log record types**: Update, Compensation (CLR), Commit, Abort, Checkpoint, Completion — know what each signals
- The **Completion Record** indicates all work is done (fully committed or fully aborted) — it is distinct from the Commit Record, which only records the decision to commit
