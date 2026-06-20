---
source: sources/wiki-PostgreSQL.md
source_url: https://en.wikipedia.org/wiki/PostgreSQL
---

## PostgreSQL: Architecture, Storage, and Extensibility

PostgreSQL is a free, open-source object-relational database management system (RDBMS) originating from the UC Berkeley POSTGRES project (1986). It emphasizes extensibility and SQL compliance, providing full ACID transaction support, MVCC-based concurrency control, and a rich type system. PostgreSQL runs on all major operating systems and scales from single-machine workloads to data warehouses and high-concurrency web services.

## Key Concepts

- **MVCC (Multiversion Concurrency Control)**: Each transaction gets a "snapshot" of the database, largely eliminating read locks. PostgreSQL is immune to dirty reads — requesting Read Uncommitted actually provides Read Committed.
- **Transaction isolation levels**: Read Uncommitted (maps to Read Committed), Read Committed, Repeatable Read, and Serializable (via Serializable Snapshot Isolation / SSI).
- **MVCC performance caveat**: The implementation is prone to performance issues under heavy write loads that update existing rows, requiring tuning (e.g., autovacuum configuration).
- **WAL (Write-Ahead Logging)**: Foundation for both replication and point-in-time recovery. Binary replication ships WAL changes to replicas asynchronously.
- **Synchronous replication**: Master waits until at least one replica writes to its transaction log. Durability guarantees can be configured per-database, per-user, per-session, or per-transaction.
- **Multi-master replication**: Not in core PostgreSQL. Available via Postgres-XC, BDR (Bidirectional Replication), and Bucardo.
- **Schemas**: Namespaces within a single database (not the same as "database schema" in the abstract sense). Cannot be nested. Controlled by `search_path` setting (default: `$user, public`).
- **Inheritance**: Tables can inherit from parent tables. Child data appears in parent queries unless `SELECT * FROM ONLY parent_table` is used. Check constraints and NOT NULL inherit; unique, primary key, and foreign key constraints do not.
- **Foreign Data Wrappers (FDWs)**: Allow PostgreSQL to query external data sources (other RDBMS, file systems, web services) as if they were regular tables, including cross-source joins.
- **Procedural languages**: Safe (sandboxed, any user) vs. unsafe (superuser only). Built-in: plain SQL, PL/pgSQL, C. Extensions: Perl, Tcl, Python 3.
- **Asynchronous notifications**: NOTIFY/LISTEN/UNLISTEN system for pub/sub messaging between sessions, fully transactional.

## Commands and Syntax

- **Schema search path**: `SET search_path TO myschema, public;` — controls unqualified object resolution order. Default: `$user, public`.
- **Inheritance query**: `SELECT * FROM ONLY parent_table;` — excludes child table rows.
- **Range type syntax**: `[4,9)` — inclusive lower bound, exclusive upper bound.
- **Async notifications**: `NOTIFY channel, 'payload';` / `LISTEN channel;` / `UNLISTEN channel;`
- **Inline procedural code**: `DO $$ BEGIN ... END $$;` — execute procedural code without defining a function.
- **In-place upgrades**: `pg_upgrade` — supports upgrades from 8.3.x onward with reduced downtime.

## Index Types

| Index Type | Use Case |
|---|---|
| B-tree | Default, general-purpose ordered data |
| Hash | Equality comparisons |
| GiST | Generalized search trees (spatial, full-text) |
| GIN | Generalized inverted index (arrays, JSONB, full-text) |
| SP-GiST | Space-partitioned data (phone numbers, IP addresses) |
| BRIN | Block Range Index (large, naturally ordered tables) |

- **Expression indexes**: Index on function/expression results, not just column values.
- **Partial indexes**: `CREATE INDEX ... WHERE condition` — index only a subset of rows.
- **Index-only scans**: Fetch data directly from the index without accessing the heap.
- **KNN-GiST**: Nearest-neighbor search for spatial/similarity queries.

## Data Types

Native types include: boolean, arbitrary-precision numerics, text/varchar/char, binary, date/time with timezone support, money, enum, bit strings, composite, arrays (up to 1 GB), geometric primitives, IPv4/IPv6/CIDR/MAC, XML with XPath, UUID, JSON and binary JSONB, HStore (key-value), and range types. Users can define custom types with full indexing support via GiST/GIN/SP-GiST. Domains add constraints to existing types.

## Relationships

- **Ingres → POSTGRES → Postgres95 → PostgreSQL**: Lineage from Michael Stonebraker's UC Berkeley work; SQL support added in 1994–1996.
- **WAL underpins both replication and recovery**: Point-in-time recovery and streaming replication both depend on write-ahead logs.
- **PostGIS**: Premier extension demonstrating PostgreSQL's extensibility model — adds GIS data types using the custom type/index infrastructure.
- **Ecosystem model**: Core team builds only the database engine; third parties provide GUIs (pgAdmin), HA tools (repmgr), replication solutions (Slony-I, Londiste, Bucardo), and language drivers.
- **libpq**: Official C client library implementing the PostgreSQL wire protocol (currently v3.0).

## Exam-Relevant Points

- PostgreSQL's Read Uncommitted isolation level actually behaves as **Read Committed** — dirty reads are impossible.
- Serializable isolation uses **Serializable Snapshot Isolation (SSI)**, not traditional two-phase locking.
- Synchronous replication durability can be configured at **four granularities**: database, user, session, and transaction.
- **Multi-master replication is NOT in core** — requires external tools (Postgres-XC, BDR, Bucardo).
- Table **inheritance does NOT propagate** unique, primary key, or foreign key constraints — only check constraints and NOT NULL.
- Schemas are **namespaces**, not nested hierarchies — they cannot contain other schemas.
- `search_path` default is `$user, public` — non-existent schemas in the path are silently skipped.
- PostgreSQL supports **six index types** (B-tree, hash, GiST, GIN, SP-GiST, BRIN) plus user-defined index methods.
- JSONB is a **binary JSON format specific to PostgreSQL** — it is not the same as BSON (MongoDB's format).
- Triggers fire in **alphabetical order** and can be per-column and conditional (WHERE clause on trigger).
- NOTIFY/LISTEN is **fully transactional** — notifications are not sent until the issuing transaction commits.
- The PostgreSQL license is **permissive** (not copyleft) — BSD/MIT-style, GPL-compatible.
