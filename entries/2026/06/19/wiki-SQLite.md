---
source: sources/wiki-SQLite.md
source_url: https://en.wikipedia.org/wiki/SQLite
---

## SQLite: Serverless Embedded Relational Database Engine

SQLite is a free, open-source, embedded relational database engine written in C. Unlike client-server RDBMS systems, SQLite is a library linked directly into an application — there is no separate server process. It is the most widely deployed database engine in the world, embedded in every major operating system, web browser, and countless applications. The entire database is stored as a single cross-platform file, and the project is released into the public domain.

## Key Concepts

- **Serverless / embedded architecture**: No daemon process, no configuration, no DBA required. The SQLite library is linked (statically or dynamically) into the host application, which calls functions directly — eliminating IPC overhead.
- **Zero-configuration**: No startup scripts, service management, or GRANT-based access control. Access control relies entirely on filesystem permissions on the database file.
- **Single-file storage**: An entire database (schema, tables, indices, data) lives in one cross-platform file. Also supports in-memory databases via the `:memory:` connection string.
- **Dynamic (manifest) typing**: Types are assigned to values, not columns. A string can be inserted into an integer column. This follows Postel's rule (be liberal in what you accept). STRICT tables (added 2021) opt into static type enforcement.
- **ACID-compliant transactions**: Full transaction support with ACID guarantees despite being lightweight.
- **Write-Ahead Logging (WAL)**: Introduced in v3.7, WAL mode enables concurrent reads and writes (default journaling mode only allows sequential writes).
- **Hidden rowid**: Tables normally include an implicit rowid index. INTEGER PRIMARY KEY columns become aliases for rowid (auto-incrementing behavior). WITHOUT ROWID tables trade this for explicit primary keys with potential space/speed benefits.
- **Foreign keys disabled by default**: Must be enabled per-connection via `PRAGMA foreign_keys = ON`.
- **No stored procedures**: By design — the host application provides procedural logic around the embedded database.
- **Maximum database size**: 281 terabytes.
- **PostgreSQL as reference platform**: SQLite uses "What would PostgreSQL do?" to interpret the SQL standard.
- **Public domain license**: Not open-contribution — contributors must sign an affidavit dedicating work to public domain.
- **Testing rigor**: Over 2 million tests, 92 million lines of test code for 156K lines of source. 100% branch coverage since v3.6.17. Four test harnesses: TCL tests, TH3 (proprietary), SQL Logic Tests, and dbsqlfuzz (fuzzer).

## Commands and Syntax

```sql
-- In-memory database connection
sqlite3 :memory:

-- Enable foreign key enforcement (must be done per connection)
PRAGMA foreign_keys = ON;

-- STRICT table (enforces column types, added 2021)
CREATE TABLE t1(x INTEGER, y TEXT) STRICT;

-- Type checking constraint (pre-STRICT workaround)
CREATE TABLE t2(x CHECK(typeof(x)='integer'));

-- WITHOUT ROWID table (requires explicit primary key)
CREATE TABLE t3(k TEXT PRIMARY KEY, v BLOB) WITHOUT ROWID;

-- Full-text search via FTS5 extension
CREATE VIRTUAL TABLE docs USING fts5(title, body);
SELECT * FROM docs WHERE docs MATCH 'search term';

-- JSON support (json1 extension, enabled by default since 2021)
SELECT json_extract(data, '$.key') FROM t;
```

**CLI tool**: `sqlite3` — standalone shell for creating databases, defining tables, running queries, and managing database files.

**Common file extensions**: `.sqlite`, `.sqlite3`, `.db`, `.db3`, `.s3db`, `.sl3`

**Magic number**: `53 51 4c 69 74 65 20 66 6f 72 6d 61 74 20 33 00` (null-terminated ASCII "SQLite format 3")

## Relationships

- **PostgreSQL**: SQLite's reference platform for SQL standard interpretation; follows PostgreSQL syntax conventions.
- **Web browsers**: Chrome, Firefox, Safari, Opera all use SQLite internally (bookmarks, cookies, history, config). Browser-side SQLite now available via official WebAssembly build.
- **Operating systems**: Bundled in Android, iOS, macOS (Core Data backend), Windows 10+, NetBSD, OpenBSD, Fedora/RHEL (RPM package management), NixOS (Nix package manager).
- **Web frameworks**: Default database for Django and Ruby on Rails; supported by Laravel, Symfony, Drupal, Trac.
- **Fossil VCS**: SQLite's own source code is managed with Fossil, which itself uses SQLite as its storage backend (circular dependency).
- **Library of Congress**: SQLite is one of four approved formats for long-term dataset preservation.
- **Language bindings**: Available for most programming languages; part of Python's standard library (`sqlite3` module).

## Exam-Relevant Points

- SQLite is an **embedded library**, not a client-server system — no separate process, no network protocol.
- **Dynamic typing by default**: types belong to values, not columns. STRICT tables (2021) opt into column-type enforcement.
- **WAL mode** (v3.7+) is required for concurrent reads and writes; default journal mode only allows sequential writes.
- **Foreign keys are OFF by default** — must be explicitly enabled with PRAGMA.
- **No stored procedures** — deliberate design decision favoring simplicity.
- **INTEGER PRIMARY KEY** is aliased to rowid, giving auto-increment-like behavior and 64-bit signed integer storage.
- **WITHOUT ROWID** tables require an explicit primary key and can improve lookup speed / reduce disk usage.
- SQLite is **not suitable for write-intensive deployments** due to file-level locking.
- **Single-file database** up to **281 TB** maximum size.
- **100% branch test coverage** since v3.6.17; 92M lines of test code vs. 156K lines of source.
- **Public domain** license (not GPL, MIT, etc.) — one of very few major projects with this licensing.
- **FTS5** extension provides full-text search; **json1** extension (default since 2021) provides JSON support; **JSONB** binary format added 2024.
- Access control is via **filesystem permissions**, not SQL GRANT statements.
- Version history: v1.0 (2000, gdbm backend) → v2.0 (2001, custom B-tree + transactions) → v3.0 (2004, i18n + manifest typing).
