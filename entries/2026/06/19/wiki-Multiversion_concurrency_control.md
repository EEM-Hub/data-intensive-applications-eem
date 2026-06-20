---
source: sources/wiki-Multiversion_concurrency_control.md
source_url: https://en.wikipedia.org/wiki/Multiversion_concurrency_control
---

## Multiversion Concurrency Control (MVCC)

MVCC is a non-locking concurrency control method used by database management systems to provide concurrent access to data. Instead of making readers wait for writers (as with traditional locking), MVCC maintains multiple versions of each data item so that each transaction sees a consistent snapshot of the database at a particular point in time. This allows reads to proceed without blocking writes, and vice versa.

## Key Concepts

- **Core problem solved**: Without concurrency control, readers can see half-written or inconsistent data (e.g., money "disappearing" mid-transfer between accounts)
- **Snapshot isolation**: The most common isolation level implemented with MVCC — each transaction observes the database state as of when the transaction started
- **No overwriting**: When updating data, MVCC creates a *new version* rather than overwriting the original; multiple versions coexist
- **Reads never block**: Read transactions use a timestamp or transaction ID to determine which version to read; no locks required for reads
- **Write conflict rule**: A write to object P is aborted if the transaction's timestamp is earlier than P's current read timestamp (because a later transaction already depends on the old value)
- **Version cleanup (garbage collection)**: Obsolete versions that will never be read must eventually be removed — this is a core operational challenge
- **Two cleanup strategies**:
  - **Sweep/rewrite**: Periodically traverse entire tables and rewrite with only the latest version (e.g., PostgreSQL's `VACUUM FREEZE`)
  - **Undo log**: Data part keeps the last committed version; undo log enables recreation of older versions. Risk: undo log exhaustion under write-heavy workloads causes transaction aborts

## Commands and Syntax

**MVCC record structure** (conceptual, shown in Rust):
```rust
struct Record {
    insert_transaction_id: u32,  // Transaction that created this version
    delete_transaction_id: u32,  // Transaction that deleted this version
    data_length: u16,
    data: Vec<u8>,
}
```

**PostgreSQL garbage collection**:
```sql
VACUUM FREEZE;  -- Rewrites table with only current versions
```

**Timestamp ordering rules**:
- Each object P has a Read Timestamp (RTS) and Write Timestamp (WTS)
- Transaction Ti reads the most recent version where WTS precedes Ti's timestamp
- Transaction Ti writing to P is aborted if TS(Ti) < RTS(P) — a later transaction already read the old value

## Relationships

- **Snapshot isolation**: MVCC is the primary mechanism for implementing true snapshot isolation efficiently
- **Locking / pessimistic concurrency control**: MVCC is an alternative to read-write locks; some databases (e.g., Oracle) still use locks alongside MVCC
- **Timestamp-based concurrency control**: MVCC builds on timestamp ordering concepts
- **ACID isolation property**: MVCC is a concrete mechanism for achieving the Isolation guarantee
- **PostgreSQL VACUUM**: Direct operational consequence of MVCC's version accumulation — dead tuples must be cleaned up
- **Document-oriented databases**: MVCC allows optimization by writing entire documents to contiguous disk sections on update
- **Read-copy-update (RCU)**: Related pattern in OS kernels using similar multi-version principles
- **Vector clocks**: Related timestamp mechanism used in distributed systems

## Exam-Relevant Points

- MVCC **never blocks reads** — this is its primary advantage over lock-based concurrency control
- The tradeoff is **storage cost** of maintaining multiple versions and the need for garbage collection
- A transaction is **aborted and restarted** if it tries to write an object that has already been read by a later transaction (TS(Ti) < RTS(P))
- **Snapshot isolation** is the most common isolation level implemented via MVCC
- PostgreSQL uses **VACUUM** to reclaim space from obsolete versions; undo-log-based systems risk **undo log exhaustion** under heavy writes
- MVCC was first described academically by **David P. Reed (1978 dissertation)** and formalized by **Bernstein and Goodman (1981)**
- First commercial MVCC product: **VAX Rdb/ELN (1984)** by Jim Starkey at DEC; he later created **InterBase**
- MVCC is used not only in databases but also in programming languages for **transactional memory**
