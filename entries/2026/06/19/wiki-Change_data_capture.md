---
source: sources/wiki-Change_data_capture.md
source_url: https://en.wikipedia.org/wiki/Change_data_capture
---

## Change Data Capture (CDC) — Design Patterns for Tracking Data Changes

Change Data Capture (CDC) is a set of software design patterns used to identify, capture, and deliver changes ("deltas") made to data sources. Rather than reprocessing entire datasets, CDC enables incremental, delta-driven data integration. CDC is fundamental to data warehouse environments where preserving the state of data across time is a core function, but applies to any database or data repository system.

## Key Concepts

- **Delta-driven dataset**: The output of CDC — a dataset containing only the changes, not the full state.
- **Source and target**: CDC always involves a source system where changes originate and a target system that acts on those changes. These may be the same physical system.
- **CDC is a data integration approach**: It sits alongside full-load and snapshot-based methods as a way to keep systems synchronized.
- **Multiple CDC solutions can coexist** in a single system, operating at different layers from application logic down to physical storage.
- **CDC vs. SCD**: Slowly Changing Dimensions (SCD) is an alternative/complementary approach. CDC overwrites the target (like SCD Type 1) and delivers only deltas. SCD Type 2 maintains full history in the target. Choose based on whether history is needed at the target.

## Commands and Syntax

No specific commands — CDC is a set of design patterns, not a product. The implementation techniques are:

### Row-Level Techniques (Application/Schema Layer)

| Technique | Mechanism | Column Example |
|-----------|-----------|----------------|
| **Timestamps** | Column stores last modification time; rows newer than last capture are "changed" | `LAST_UPDATE`, `LAST_MODIFIED` |
| **Version numbers** | Table-level version counter stored in a reference table; rows tagged with latest version are captured | `VERSION_NUMBER` |
| **Status indicators** | Boolean or code column flags rows as changed or ready for capture | `IS_CHANGED`, `STATUS` |
| **Combined (time/version/status)** | All three together enable precise queries like "version 2.1, changed in June, status = production-ready" | All of the above |

### System-Level Techniques

- **Database triggers**: Fire on DML events, log changes to a queue/history table (e.g., schema: `Id, TableName, RowId, Timestamp, Operation`). Can implement publish/subscribe for multiple targets. The queue table is "played back" to replicate changes.
- **Transaction log reading**: Parse the database's write-ahead log directly. Provides lowest latency and minimal database impact but is vendor-specific with no cross-DBMS standard. Supported programmatically by Oracle, DB2, SQL/MP, SQL/MX, SQL Server.

### Push vs. Pull Delivery

- **Push**: Source creates a snapshot of changes and delivers downstream.
- **Pull**: Target requests changed data from the source, then delivers onward.

## Relationships

- **Data integration / ETL**: CDC is an incremental alternative to full-load ETL, enabling real-time or near-real-time BI pipelines.
- **Data warehousing**: CDC is core to warehouse loading — capturing state changes over time is a primary warehouse function.
- **Slowly Changing Dimensions (SCD)**: Complementary pattern. SCD Type 2 preserves history at the target; CDC delivers only current deltas (analogous to SCD Type 1).
- **Referential integrity**: Must be maintained when applying CDC deltas to target systems.
- **Optimistic locking**: Timestamp and version columns used for CDC overlap with those used for optimistic concurrency control, but the two uses are distinct — row-level version counters for locking are impractical for CDC because you'd need to know every row's starting version.
- **Observer/publish-subscribe pattern**: Trigger-based CDC can fan out changes to multiple targets via pub/sub.

## Exam-Relevant Points

- **Six CDC techniques**: Timestamps, version numbers, status indicators, combined (time/version/status), triggers, and transaction log reading. Know trade-offs of each.
- **Transaction log advantages**: Minimal DB impact, no application changes needed, low latency, preserves transactional integrity (replays commits in order), no schema changes required.
- **Transaction log challenges**: Vendor-specific formats with no standard, must handle log archiving coordination, uncommitted/rolled-back changes, metadata changes, and format differences across DBMS versions.
- **Combined time/version/status is the recommended row-level approach** — the three are complementary, not redundant. Together they enable precise capture filtering by version, time range, and readiness.
- **Confounding factor**: Source systems that update metadata (e.g., "last viewed by") without changing actual data create noise in CDC.
- **CDC produces a delta-driven dataset** (only changes); SCD Type 2 produces a historized dataset (all versions). The choice depends on whether history is needed at the target.
- **Row-level version numbers for optimistic locking are NOT usable for CDC** — CDC would need to know every row's starting version, which is impractical.
