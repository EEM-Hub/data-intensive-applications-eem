---
source: sources/wiki-Materialized_view.md
source_url: https://en.wikipedia.org/wiki/Materialized_view
---

## Materialized Views in Databases

A materialized view is a database object that stores the precomputed results of a query as a concrete table, unlike a regular view which is virtual and re-executes its query on each access. This is a form of caching/precomputation used primarily for performance optimization, trading extra storage and potential data staleness for faster read access.

## Key Concepts

- **Materialized view vs. regular view**: A regular (virtual) view re-executes its defining query on every access. A materialized view stores the result as a physical table that can be queried directly.
- **Materialization**: The process of computing and storing the query results. Analogous to memoization in functional programming.
- **Trade-off**: Faster reads at the cost of extra storage and potentially stale data — the materialized result may not reflect the latest base table changes.
- **Indexing advantage**: Indexes can be built on any column of a materialized view. Regular views can typically only exploit indexes from their underlying base tables.
- **Refresh strategies**: Views can be refreshed manually, on a schedule, incrementally (fast refresh), or kept always in sync (SQL Server's approach).
- **Historical terminology**: Oracle previously called materialized views "snapshots" (now deprecated). IBM Db2 calls them "materialized query tables."
- **Primary use case**: Data warehousing, where frequent queries against large base tables are expensive.

## Commands and Syntax

**Oracle** — scheduled auto-refresh:
```sql
CREATE MATERIALIZED VIEW MV_MY_VIEW
REFRESH FAST START WITH SYSDATE
  NEXT SYSDATE + 1
    AS SELECT * FROM <table_name>;
```

**PostgreSQL** — manual refresh (v9.3+):
```sql
CREATE MATERIALIZED VIEW MV_MY_VIEW
  [WITH (storage_parameter [= value] [, ...])]
  [TABLESPACE tablespace_name]
    AS SELECT * FROM <table_name>;

-- Refresh manually:
REFRESH MATERIALIZED VIEW MV_MY_VIEW;

-- Concurrent refresh (v9.4+), allows reads during refresh:
REFRESH MATERIALIZED VIEW CONCURRENTLY MV_MY_VIEW;
```

**SQL Server** — "Indexed Views" (always synchronized):
```sql
CREATE VIEW MV_MY_VIEW
WITH SCHEMABINDING
AS
SELECT COL1, SUM(COL2) AS TOTAL
FROM <table_name>
GROUP BY COL1;
GO
CREATE UNIQUE CLUSTERED INDEX XV
  ON MV_MY_VIEW (COL1);
```

## Relationships

- **Regular views**: Materialized views are the physical counterpart to virtual views; understanding the distinction is fundamental.
- **Caching and precomputation**: Materialized views are a database-level caching strategy, conceptually parallel to application-level caching and memoization.
- **Data warehousing**: Primary domain where materialized views deliver value — precomputing aggregations and joins over large fact/dimension tables.
- **Stream processing**: Modern frameworks (Kafka Streams, Flink, Spark Structured Streaming, Materialize, RisingWave) extend the materialized view concept to continuously updating streaming data.
- **Indexes**: Materialized views can be independently indexed, connecting them to query optimization and index design topics.
- **Change data capture / incremental refresh**: Techniques like Oracle's fast refresh and DynamoDB Streams-based materialization rely on tracking changes to base tables.

## Exam-Relevant Points

- A materialized view stores query results as a **physical table**; a regular view is **virtual** and re-executes.
- The core trade-off is **read performance** vs. **storage cost + data freshness**.
- **SQL Server's indexed views** are unique: they are always synchronized with base tables (no manual refresh needed), but require deterministic mappings and `SCHEMABINDING`.
- **PostgreSQL** materialized views require **manual refresh** (`REFRESH MATERIALIZED VIEW`); `CONCURRENTLY` allows non-blocking refresh but requires a unique index.
- **Oracle** supports `REFRESH FAST` (incremental) and scheduled refresh (`NEXT SYSDATE + 1`).
- Materialized views can have **indexes on any column**, unlike regular views which are limited to base table indexes.
- **MySQL does not natively support** materialized views — workarounds use triggers, stored procedures, or tools like Flexviews.
- In stream processing, materialized views represent **continuously maintained query results** over unbounded data streams — a key concept in modern real-time data architectures.
