---
source: sources/wiki-Redis.md
source_url: https://en.wikipedia.org/wiki/Redis
---

## Redis: In-Memory Key–Value Database

Redis (Remote Dictionary Server) is an in-memory key–value database written in C, used primarily as a distributed cache and message broker with optional durability. Created by Salvatore Sanfilippo in 2009, Redis holds all data in memory for low-latency reads and writes. It differs fundamentally from relational databases by operating on abstract data types via commands rather than SQL queries, and by using the `fork()` system call to persist data without blocking client operations.

## Key Concepts

- **In-memory data store**: All data resides in RAM; disk persistence is optional and asynchronous
- **Data model**: Maps keys to typed values — not a relational model. No secondary indexes or aggregations in the traditional RDBMS sense
- **Supported data types**: Strings, JSON documents, Hashes (field–value pairs), Lists, Sets, Vector Sets, Streams (added in v5.0)
- **Redis Query Engine**: Enables use as a document database, vector database, secondary index, or search engine over hash and JSON documents
- **Pub/Sub**: Lightweight publish/subscribe messaging; subscribers receive messages in real time from channels
- **Transactions**: Group of commands executed as a single isolated operation — no other client request is served mid-transaction
- **Lua scripting**: Users can upload and execute Lua scripts server-side
- **Single-threaded execution**: A single Redis instance cannot parallelize tasks; it is single-threaded (or double-threaded during AOF rewrite)
- **License history**: BSD-3 (original) → RSAL + SSPL (v7.4, 2024) → tri-licensed RSAL + SSPL + AGPL (v8.0, May 2025)

## Commands and Syntax

No specific CLI commands were detailed in this source, but key operational concepts include:

- **RDB snapshotting**: Asynchronous binary dump of the full dataset to disk at configured intervals
- **AOF (Append-Only File)**: Journaling mode that logs every write operation; rewritten in the background to prevent unbounded growth. Generally considered the safer persistence method
- **Default flush interval**: Redis writes to disk at least every 2 seconds; a complete system failure loses only a few seconds of data
- **Clustering**: Available since v3.0 (April 2015). All single-key commands work; multi-key operations restricted to keys on the same node. Scales up to 1,000 nodes
- **Replication**: Master–replica with single-rooted tree topology. Replicas can accept writes (permitting intentional inconsistency). Pub/Sub is fully replicated up the tree

## Relationships

- **Memcached**: Similar in-memory caching system; Redis adds persistence, richer data types, and pub/sub
- **Valkey**: Linux Foundation fork of Redis, created from the last BSD-licensed version after the 2024 license change
- **Managed cloud services**: AWS ElastiCache for Redis, Google Cloud Memorystore, Azure Cache for Redis, Alibaba ApsaraDB for Redis
- **Message brokers**: Redis Pub/Sub and Streams compete with dedicated brokers (Kafka, RabbitMQ) for lightweight use cases
- **Document/vector databases**: Redis Query Engine positions Redis as an alternative to purpose-built document stores and vector databases
- **CRDTs**: Redis supports conflict-free replicated data types for multi-master scenarios

## Exam-Relevant Points

- Redis stands for **Remote Dictionary Server**
- Written in **C**, runs on Unix-like systems
- **Single-threaded** execution model — cannot parallelize within one instance
- Two persistence mechanisms: **RDB snapshots** (point-in-time binary dumps) and **AOF** (append-only journaling). AOF is considered safer
- Default persistence writes at least every **2 seconds**; only seconds of data lost on crash
- Clustering since **v3.0** (2015), scales to **1,000 nodes**
- Multi-key operations in a cluster are **restricted to keys on the same node**
- Replication is **master–replica** with a single-rooted tree; replicas can optionally accept writes
- Redis Streams (v5.0, 2018) store multiple fields and string values with automatic time-based sequencing at a single key
- The `fork()` system call is used to create a child process for persistence while the parent continues serving clients
- As of v8.0, all data types ship in a single package under unified licensing
