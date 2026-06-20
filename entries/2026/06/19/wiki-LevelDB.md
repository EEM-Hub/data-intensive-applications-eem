---
source: sources/wiki-LevelDB.md
source_url: https://en.wikipedia.org/wiki/LevelDB
---

## LevelDB: Google's Embedded Key-Value Store

LevelDB is an open-source, on-disk key-value store written in C++ by Google fellows Jeffrey Dean and Sanjay Ghemawat. It is an embedded database library (not a standalone server) inspired by the Bigtable tablet stack, designed for fast writes and sequential reads. It is used as the storage engine behind Chrome's IndexedDB, blockchain clients, and other applications requiring a lightweight persistent store.

## Key Concepts

- **Embedded library, not a server** — applications link against LevelDB directly; there is no separate process, CLI, or network protocol.
- **Sorted key-value model** — keys and values are arbitrary byte arrays; data is stored sorted by key, enabling efficient range scans.
- **Not relational** — no SQL support, no relational data model, no secondary indexes. Classified as a NoSQL / dbm-style store.
- **LSM-tree lineage** — based on the same design principles as Google Bigtable's tablet stack (log-structured merge trees), but written from scratch with no shared code.
- **Snappy compression** — uses Google's Snappy compression library for on-disk data compression.
- **Batch writes** — supports atomic batch write operations.
- **Bidirectional iteration** — supports both forward and backward iteration over sorted keys.
- **Small footprint** — ~350 kB binary size; New BSD License.
- **Written in 2011** — developed specifically to be open-sourceable (unlike the internal Bigtable tablet code which had deep Google-internal dependencies).

## Commands and Syntax

LevelDB is a C++ library with no CLI. Applications interact via the C++ API:

- **Open a database**: `leveldb::DB::Open(options, "/path/to/db", &db)`
- **Put**: `db->Put(write_options, key, value)`
- **Get**: `db->Get(read_options, key, &value)`
- **Delete**: `db->Delete(write_options, key)`
- **Batch write**: create a `leveldb::WriteBatch`, add operations, then `db->Write(write_options, &batch)`
- **Iterate**: create an `Iterator` via `db->NewIterator(read_options)`, then use `SeekToFirst()`, `Next()`, `Prev()`, `key()`, `value()`

MariaDB 10.0+ includes a storage engine that allows SQL queries against LevelDB tables.

## Relationships

- **Bigtable** — LevelDB's design is derived from Bigtable's tablet stack (LSM-tree based). LevelDB is the open-source, dependency-free reimplementation.
- **RocksDB** — Facebook's fork of LevelDB with significant performance and feature enhancements (compaction improvements, column families, etc.). RocksDB is the more common choice in production systems today.
- **LSM-trees** — LevelDB is one of the canonical implementations of log-structured merge-tree storage, relevant to understanding write-optimized storage engines (Chapter 3 of DDIA).
- **IndexedDB / Chrome** — LevelDB serves as the backend for Chrome's IndexedDB, its original motivating use case.
- **Blockchain systems** — Bitcoin Core and go-ethereum use LevelDB for metadata storage.
- **LMDB (Lightning Memory-Mapped Database)** — benchmarks show LMDB is ~10x faster for reads and some write patterns; LMDB uses a B+ tree rather than an LSM-tree.
- **SQLite / Kyoto Cabinet / Berkeley DB** — compared in Google's published benchmarks; LevelDB excels at writes and sequential reads but is slower for large-value random reads.

## Exam-Relevant Points

- LevelDB is an **embedded library**, not a client-server database — this is a key architectural distinction from systems like MySQL or PostgreSQL.
- It stores data **sorted by key**, which is fundamental to its efficient sequential read and range query performance.
- It is based on an **LSM-tree** design (same as Bigtable), making it **write-optimized** at the cost of read amplification — a core tradeoff discussed in DDIA Chapter 3.
- **No secondary indexes** — applications must manage their own indexing if needed.
- **Known reliability concerns** — LevelDB has a documented history of data corruption bugs, especially on non-checksummed file systems after crash or power failure. This is relevant to durability guarantees and the distinction between fsync guarantees across file systems.
- **Snappy compression** is the default — a fast, non-optimal-ratio compressor designed for speed over compression ratio.
- LevelDB vs. LMDB is a classic **LSM-tree vs. B-tree** comparison: LevelDB wins on writes, LMDB wins on reads — directly illustrating DDIA's storage engine tradeoff analysis.
- **Batch writes are atomic** — important for understanding write-ahead logging and atomicity in embedded stores.
