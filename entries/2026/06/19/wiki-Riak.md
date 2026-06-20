---
source: sources/wiki-Riak.md
source_url: https://en.wikipedia.org/wiki/Riak
---

## Riak: Dynamo-Inspired Distributed Key-Value Store

Riak is a distributed NoSQL key-value data store written in Erlang that implements the principles from Amazon's Dynamo paper. It provides high availability, fault tolerance, and scalability through masterless peer-to-peer architecture with automatic data replication and distribution. Originally developed by Basho Technologies, Riak became fully open source after bet365 acquired the IP in 2017 following Basho's receivership. The latest release is 3.2.0 (January 2023).

## Key Concepts

- **Dynamo-based architecture**: Implements Amazon's Dynamo paper principles, heavily influenced by the CAP theorem — favors availability and partition tolerance (AP system by default)
- **Masterless replication**: Peer-to-peer architecture with no single point of failure; default replication factor (`n_val`) of 3
- **Hinted handoff**: During node outages (network partition or hardware failure), writes go to a neighboring node beyond the initial three replicas, ensuring continued availability
- **Consistent hashing**: Data distributed across nodes using hashing, providing predictable latency even during multiple node failures
- **Tunable consistency**: Per-bucket choice between eventual consistency and strong consistency
- **Pluggable storage backends**: Default is Bitcask; also supports LevelDB and Leveled (pure Erlang backend introduced in 2.9.0)
- **CRDTs (Conflict-free Replicated Data Types)**: Supports counters (v1.4), sets, maps, registers, and flags (v2.0), plus grow-only sets (v2.2.6)
- **TictacAAE (Tictac Active Anti-Entropy)**: Next-generation anti-entropy mechanism for detecting and repairing data inconsistencies across replicas
- **Product family**: Riak Core (distributed systems framework), Riak KV (key-value store), Riak CS (S3-compatible cloud storage built on KV), Riak TS (time series extension — discontinued)
- **Stanchion**: Serialization service used by Riak CS to manage globally unique entities (users, bucket names)
- **Multi-Datacenter Replication (MDC)**: Supports uni-directional and bi-directional replication with fullsync and realtime modes; topologies include chains, hub-and-spoke, and mesh via Cascades

## Commands and Syntax

- **API access**: RESTful HTTP API and Protocol Buffers for PUT, GET, POST, DELETE operations
- **Query mechanisms**: Secondary indexes, full-text search (via Apache Solr integration / Yokozuna), MapReduce (JavaScript via SpiderMonkey, or Erlang)
- **Riak TS SQL subset**: `CREATE TABLE` for schema definition; `SELECT` with `WHERE` (no `HAVING`, no `ORDER BY` in released versions)
- **Storage modes**: Keys/values can be stored in memory, disk, or both
- **Write-once buckets** (v2.1): Optimization for entries written exactly once, never updated
- **Configuration**: Erlang VM memory and scheduler settings configurable via `riak.conf` (v3.0.10+)
- **Console commands**: `reip_manual` for IP reassignment (v3.0.12+)
- **Official client drivers**: Ruby, Java, Erlang, Python (plus community drivers for other languages)

## Relationships

- **Amazon Dynamo**: Riak is a direct implementation of the Dynamo paper's principles (consistent hashing, vector clocks, sloppy quorum, hinted handoff, anti-entropy)
- **CAP theorem**: Riak is an AP system by default (availability + partition tolerance), with optional strong consistency making it CP per-bucket
- **Bitcask / LevelDB / Leveled**: Pluggable storage engine layer — Bitcask is a log-structured hash table (fast writes, keys must fit in memory), LevelDB is an LSM-tree (supports larger key spaces), Leveled is a pure-Erlang alternative
- **Apache Solr**: Powers Riak's full-text search capability (Yokozuna integration, separated from default build in 3.0+)
- **Amazon S3**: Riak CS provides an S3-compatible API for object storage (was briefly rebranded "Riak S2" to emphasize compatibility)
- **Comparable systems**: Cassandra (also Dynamo-inspired), Redis, Memcached, Oracle NoSQL, Apache Accumulo
- **Erlang/OTP**: Written in Erlang; version compatibility is a major concern (3.0+ requires OTP 20+; 3.2.0 supports OTP 22/24/25)

## Exam-Relevant Points

- Riak implements **Amazon's Dynamo** paper — know the specific mechanisms: consistent hashing, replication with configurable n_val (default 3), hinted handoff, and anti-entropy repair
- **Masterless architecture** means any node can serve reads and writes; no leader election, no single point of failure — contrast with leader-based systems like MongoDB or ZooKeeper-dependent systems
- **Tunable consistency per bucket**: can choose eventual (default, AP) or strong consistency (CP) — this is a key differentiator vs. systems that are fixed on the CAP spectrum
- Default storage backend is **Bitcask** (log-structured, append-only, all keys must fit in RAM); **LevelDB** for when key space exceeds memory
- **Multi-datacenter replication** has two modes: **fullsync** (bulk synchronization, metadata-only transfer for efficiency) and **realtime** (streaming updates); designed to work together
- **CRDTs** added in v2.0 (sets, maps, registers, flags) resolve the sibling/conflict problem for specific data structures without application-level conflict resolution
- Riak CS uses **Stanchion** for global uniqueness guarantees (serialized operations) — understand that this is a deliberate consistency chokepoint in an otherwise AP system
- **Riak TS** was a strategic failure that contributed to Basho's demise — illustrates the risk of product line diversification in infrastructure companies
- **Write-once buckets** (v2.1) are an important optimization pattern: when data is immutable (logs, events, sensor readings), skipping conflict resolution yields significant performance gains
- Know that Riak moved from freemium to fully open source (Apache 2.0) — all enterprise features (MDC replication, etc.) are now in the community edition
