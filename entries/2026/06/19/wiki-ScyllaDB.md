---
source: sources/wiki-ScyllaDB.md
source_url: https://en.wikipedia.org/wiki/ScyllaDB
---

## ScyllaDB: Cassandra-Compatible High-Performance NoSQL Wide-Column Store

ScyllaDB is a source-available distributed NoSQL wide-column data store designed as a drop-in replacement for Apache Cassandra, offering significantly higher throughput and lower latency. Written in C++20 and built on the Seastar asynchronous programming library, it replaces Cassandra's Java runtime and traditional Linux concurrency primitives (threads, shared memory, mapped files) with a shared-nothing, per-core sharded architecture.

## Key Concepts

- **Wide-column store**: NoSQL data model where data is stored in columns grouped into column families, same model as Cassandra and DynamoDB.
- **Cassandra compatibility**: Supports CQL (Cassandra Query Language) and SSTable file formats — protocol-level and storage-level compatibility with Cassandra.
- **DynamoDB API support**: Also implements the Amazon DynamoDB API, enabling migration from DynamoDB workloads.
- **Shared-nothing per-core sharding**: Each CPU core handles a disjoint subset of data with no shared memory between cores; inter-core communication is explicit message passing. This eliminates lock contention and cache-line bouncing.
- **Seastar framework**: Asynchronous, event-driven programming library purpose-built for modern hardware; replaces threads and blocking I/O with futures/promises and cooperative scheduling per core.
- **NUMA/SMP optimization**: The per-core shard design maps naturally to NUMA topologies, avoiding cross-socket memory access penalties.
- **Performance claims**: Up to 2 million requests/second on a single node; 10x cluster-level throughput vs. Cassandra (i.e., 1 ScyllaDB node replaces ~10 Cassandra nodes). Independent benchmarks vary — OCTO measured ~2x, Samsung measured 10–37x depending on YCSB workload and hardware.
- **Deployment models**: On-premises, public cloud, or DBaaS (ScyllaDB Cloud).
- **Licensing**: Moved from AGPL to source-available (Dec 2024); clusters beyond a certain size require a commercial license.
- **Vector database support**: Announced in 2026, using the open-source USearch library.

## Commands and Syntax

ScyllaDB uses CQL, so standard Cassandra CQL commands apply:

```sql
-- Create a keyspace
CREATE KEYSPACE my_ks WITH replication = {'class': 'NetworkTopologyStrategy', 'dc1': 3};

-- Create a table (wide-column)
CREATE TABLE my_ks.users (
    user_id UUID PRIMARY KEY,
    name TEXT,
    email TEXT
);

-- Insert and query
INSERT INTO my_ks.users (user_id, name, email) VALUES (uuid(), 'Alice', 'alice@example.com');
SELECT * FROM my_ks.users WHERE user_id = ?;
```

No unique ScyllaDB-specific query syntax was detailed in this source — the compatibility story is that existing CQL tooling and drivers work unchanged.

## Relationships

- **Apache Cassandra**: ScyllaDB is a ground-up C++ reimplementation of Cassandra; shares protocols (CQL) and storage formats (SSTable) but not code. Understanding Cassandra's data model, replication, and consistency levels is prerequisite.
- **Amazon DynamoDB**: ScyllaDB implements the DynamoDB API, positioning it as a self-hosted DynamoDB alternative.
- **Seastar**: The async I/O framework underpinning ScyllaDB's per-core architecture; also used in other high-performance C++ systems.
- **OSv**: ScyllaDB's founding team (Cloudius Systems) previously built the OSv unikernel — same lineage of hardware-aware, minimal-overhead systems design.
- **YCSB (Yahoo Cloud Serving Benchmark)**: Standard benchmark suite used to compare ScyllaDB against Cassandra and other NoSQL stores.
- **Vector databases**: ScyllaDB's 2026 vector search feature (via USearch) places it in competition with purpose-built vector stores for AI/ML workloads.

## Exam-Relevant Points

- ScyllaDB is **wire-compatible with Cassandra** (CQL protocol + SSTable format) — this is the primary architectural distinction to remember vs. being a fork.
- The **shared-nothing per-core shard** model is the key design choice that drives performance; each core owns its data partition and communicates via explicit messaging, not shared memory.
- Written in **C++20** using the **Seastar** async framework — replacing Java and threads is the mechanism behind the latency and throughput gains.
- Performance improvement over Cassandra is **workload- and hardware-dependent**: vendor claims 10x, independent results range from 2x to 37x.
- ScyllaDB also supports the **DynamoDB API**, not just CQL — this is a differentiator from other Cassandra-compatible databases.
- Licensing changed from **AGPL to source-available** in December 2024 — important for questions about open-source vs. proprietary database ecosystems.
- **Vector search** capability added in 2026 via the USearch library — relevant to convergence of operational and AI/ML database workloads.
