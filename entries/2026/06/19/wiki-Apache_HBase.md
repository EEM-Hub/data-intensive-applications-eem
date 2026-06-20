---
source: sources/wiki-Apache_HBase.md
source_url: https://en.wikipedia.org/wiki/Apache_HBase
---

## Apache HBase: Open-Source Distributed Wide-Column Store

Apache HBase is an open-source, non-relational distributed database modeled after Google's Bigtable, written in Java. It runs on top of HDFS (Hadoop Distributed File System) as part of the Apache Hadoop ecosystem, providing fault-tolerant storage for large quantities of sparse data with high throughput and low latency.

## Key Concepts

- **Wide-column store** — HBase organizes data in a column-oriented format, not rows like traditional RDBMS; this is the same data model as Google Bigtable
- **CP system (CAP theorem)** — HBase favors Consistency and Partition tolerance over Availability
- **Sparse data optimized** — designed for datasets where most cells are empty (e.g., finding 50 items in 2 billion records, or non-zero items representing <0.1% of a collection)
- **Per-column features** — compression, in-memory operation, and Bloom filters can be configured on individual columns, following the original Bigtable paper
- **Not a SQL replacement** — HBase does not support SQL natively; equivalent operations are written in Java using a MapReduce-like approach
- **SQL layers exist** — Apache Phoenix provides SQL + JDBC on top of HBase; Apache Trafodion adds ODBC/JDBC and distributed ACID transactions
- **Multiple access APIs** — Java API (primary), REST, Avro, and Thrift gateway APIs
- **MapReduce integration** — HBase tables can serve as both input and output for Hadoop MapReduce jobs
- **Storage backends** — runs on HDFS or Alluxio

## Commands and Syntax

No specific CLI commands were detailed in this source. HBase interaction is primarily through:
- **Java API** — primary programmatic interface
- **REST gateway** — HTTP-based access
- **Thrift gateway** — RPC-based access
- **Avro gateway** — serialization-based access
- **Apache Phoenix** — provides SQL shell and JDBC driver for SQL-like queries over HBase

## Relationships

- **Google Bigtable** — HBase is the open-source implementation of the Bigtable data model
- **HDFS / Hadoop** — HBase runs on top of HDFS; it is a core Hadoop ecosystem project
- **MapReduce** — HBase tables integrate directly as MapReduce inputs/outputs
- **Apache Phoenix** — adds SQL query capability and JDBC connectivity to HBase
- **Apache Trafodion** — adds distributed ACID transactions with ODBC/JDBC over HBase
- **Apache Cassandra** — alternative wide-column store (AP system vs. HBase's CP)
- **Apache Accumulo** — another Bigtable-derived system with cell-level security
- **NoSQL family** — HBase belongs to the NoSQL / wide-column store category alongside Cassandra, Hypertable, and others
- **Alluxio** — alternative storage layer to HDFS that HBase can run on
- **MyRocks** — Facebook migrated from HBase to MyRocks in 2018 for their messaging platform

## Exam-Relevant Points

- HBase is a **CP system** under the CAP theorem (consistency + partition tolerance)
- HBase is a **wide-column store**, not a key-value store or document store
- HBase is modeled after **Google Bigtable** and is the open-source equivalent
- HBase runs on **HDFS** and is part of the **Hadoop ecosystem**
- HBase does **not** support SQL natively — Apache Phoenix or Trafodion are needed for SQL access
- HBase supports **Bloom filters**, **compression**, and **in-memory operation** on a per-column basis
- HBase is optimized for **sparse data** with fast read/write on large datasets
- HBase tables can serve as **MapReduce input and output**
- Facebook adopted HBase for messaging in 2010 but **migrated to MyRocks in 2018** — a notable case study in choosing the right storage engine for workload evolution
- HBase is written in **Java** and licensed under **Apache License 2.0**
- The current stable release line is **2.5.x** (with 3.0 in beta preview)
