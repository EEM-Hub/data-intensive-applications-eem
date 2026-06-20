---
source: sources/wiki-RocksDB.md
source_url: https://en.wikipedia.org/wiki/RocksDB
---

It looks like the write permission is being denied. Could you grant write permission for the entries directory so I can save the RocksDB entry? In the meantime, here's the structured summary I prepared:

## RocksDB: High-Performance Embedded Key-Value Storage Engine

RocksDB is a high-performance embedded key-value database developed at Facebook (now Meta), released May 2012 as a fork of Google's LevelDB. Created by Dhruba Borthakur to optimize for server workloads — multi-core CPUs and SSDs. Based on LSM trees, written in C++, it's one of the most widely adopted embedded storage engines in the industry.

## Key Concepts

- **Fork of LevelDB** — optimized for server-class hardware (multi-core, SSDs), retaining the sorted key-value byte-array model
- **LSM-tree based** — write-optimized design with significant enhancements over LevelDB
- **Embedded library, not a server** — no server process, CLI, SQL, or network protocol
- **Features beyond LevelDB** — transactions, backups/snapshots, column families, Bloom filters, TTL, universal compaction, merge operators, geospatial indexing
- **Column families** — logical data partitioning; can implement secondary indexes
- **Merge operators** — deferred read-modify-write combined during compaction, reducing write amplification
- **Universal compaction** — alternative to leveled compaction trading space for lower write amplification
- **Licensing** — dual Apache 2.0 / GPLv2 (changed from BSD+Patents in 2017 due to ASF blacklisting)

## Relationships

- **LevelDB** → direct fork, adding multi-core/SSD optimization and many features
- **MyRocks** → RocksDB as MySQL/MariaDB storage engine (stable MariaDB 10.2.16+)
- **Cassandra** → Facebook/Instagram's RocksDB-backed engine (10x tail latency reduction)
- **Flink** → state backend checkpointing; **Kafka Streams** → local state stores
- **TiDB, YugabyteDB, ArangoDB, MongoDB (MongoRocks)** → all use RocksDB underneath
- **Ceph BlueStore** → metadata management; **Manhattan (Twitter)** → primary engine since 2018

## Exam-Relevant Points

- Fork of LevelDB optimized for **multi-core CPUs and SSDs**
- Both use **LSM trees**; RocksDB adds **universal compaction**
- **Embedded library** — no SQL, no built-in secondary indexes
- Key additions: **transactions, column families, Bloom filters, TTL, merge operators**
- Ubiquitous as a **storage engine under other databases** (MySQL, Cassandra, TiDB, YugabyteDB)
- Critical **state store for stream processing** (Flink, Kafka Streams)
