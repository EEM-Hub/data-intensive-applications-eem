---
source: sources/wiki-Transaction_log.md
source_url: https://en.wikipedia.org/wiki/Transaction_log
---

## Transaction Logs in Database Systems

Transaction logs (also called transaction journals, database logs, binary logs, or audit trails) are the fundamental mechanism database management systems use to guarantee ACID properties across crashes and hardware failures. They are physical files stored in stable storage that record a history of all changes made to a database, enabling recovery through rollback of uncommitted transactions and re-application of committed but not-yet-materialized changes.

## Key Concepts

- **Transaction log**: A chronological history of actions executed by a DBMS, stored as a file in stable storage format
- **Purpose**: Guarantees ACID properties — specifically **atomicity** and **durability** — over crashes or hardware failures
- **Recovery process**: On restart after inconsistent shutdown, the DBMS reviews logs, rolls back uncommitted transactions, and re-applies committed-but-unmaterialized transactions
- **Journal**: In database context, the record of data altered by a given process; in storage context, a chronological record of data processing operations used to reconstruct system state
- **Log Sequence Number (LSN)**: Unique, monotonically increasing identifier for each log record — enables constant-time recovery
- **Linked list structure**: Log records link to their predecessor via Prev LSN, forming a navigable chain
- **Not to be confused** with human-readable log files that a DBMS also produces

## Commands and Syntax

No specific commands are described, but the **log record structure** is defined:

```
Log Record = {
  LSN,              -- unique, monotonically increasing ID
  Prev LSN,         -- pointer to previous log record (linked list)
  Transaction ID,   -- which transaction generated this record
  Type,             -- update, CLR, commit, abort, checkpoint, completion
  Change Info        -- type-specific payload
}
```

**Log record types and their extra fields:**

| Type | Extra Fields | Purpose |
|------|-------------|---------|
| **Update** | PageID, Length, Offset, Before/After Images | Records a database change |
| **Compensation (CLR)** | undoNextLSN | Records rollback of a specific update; maps 1:1 to an Update record |
| **Commit** | — | Marks transaction commit decision |
| **Abort** | — | Marks transaction abort/rollback decision |
| **Checkpoint** | redoLSN, undoLSN | Speeds recovery by bounding how far back the log must be read |
| **Completion** | — | Marks that all work (commit or abort) is fully done |

**Checkpoint fields explained:**
- `redoLSN`: First log record for a dirty page not yet flushed — redo starts here
- `undoLSN`: Oldest log record of the oldest in-progress transaction — oldest record needed to undo active transactions

## Relationships

- **ARIES** (Algorithms for Recovery and Isolation Exploiting Semantics): Recovery algorithm that leverages monotonically increasing LSNs
- **Write-Ahead Logging (WAL)**: Protocol requiring log records be written before data pages — the operational discipline that makes transaction logs effective
- **Journaling file systems**: Apply the same principle at the filesystem level
- **Log-structured file systems**: Take the log concept further, making the log the primary storage structure
- **Redo log**: Specific log type focused on re-applying committed changes
- **Checkpointing**: Optimization that bounds recovery time; PostgreSQL flushes all dirty pages during checkpoint creation
- **Concurrency control**: Transaction logs interact with concurrency mechanisms to maintain isolation
- **ACID properties**: Transaction logs are the implementation mechanism for atomicity (undo uncommitted) and durability (redo committed)

## Exam-Relevant Points

- Transaction logs guarantee **atomicity** and **durability** specifically — know which ACID properties they serve
- Recovery involves **two distinct operations**: rolling back uncommitted transactions AND re-applying committed-but-unmaterialized transactions
- LSNs are **monotonically increasing** — this property is essential for recovery algorithms like ARIES
- Log records form a **linked list** via Prev LSN pointers
- **Compensation Log Records** have a 1:1 correspondence with Update Log Records and contain `undoNextLSN`
- **Before and After Images**: Update records may contain one or both byte-level images of the changed page
- **Checkpoint records** contain two critical LSNs: `redoLSN` (where redo begins) and `undoLSN` (oldest record needed for undo)
- The checkpoint `redoLSN` points to the first update that **wasn't flushed** at checkpoint time
- **Completion records** are distinct from commit/abort records — they indicate all work is fully finished
- Transaction logs are stored in **stable storage** — this physical guarantee is what makes the durability promise possible
