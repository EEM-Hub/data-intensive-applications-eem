---
source: sources/wiki-Apache_Cassandra.md
source_url: https://en.wikipedia.org/wiki/Apache_Cassandra
---

It seems write permissions aren't being granted. Here's the structured summary for Apache Cassandra:

---

## Apache Cassandra — Distributed Wide-Column NoSQL Database

Apache Cassandra is a free, open-source distributed database management system designed for handling large volumes of data across commodity servers. Originally developed at Facebook by Avinash Lakshman (co-author of Amazon's Dynamo) and Prashant Malik for inbox search, it was open-sourced in 2008 and became an Apache top-level project in 2010. Cassandra combines Amazon Dynamo's distributed storage and replication techniques with Google Bigtable's data storage engine model. It is classified as an AP system under the CAP theorem, prioritizing availability and partition tolerance over strong consistency. Written in Java, the current stable release is 5.0.x.

## Key Concepts

- **Wide-column store**: Combines features of key-value and tabular databases; rows within the same table can have different columns, enabling flexible/sparse schemas
- **AP system (CAP theorem)**: Prioritizes availability and partition tolerance; offers tunable consistency levels but is not suited for strict consistency requirements
- **Masterless architecture**: All nodes perform identical functions — no single point of failure, no master/slave distinction
- **Linear scalability**: Read and write throughput increase linearly with the addition of new nodes
- **LSM tree storage**: Uses Log-Structured Merge Trees (not B-trees) optimizing for write throughput via append-only operations
- **Eventual consistency**: Maintained using tombstones for deletes, hinted handoff for node outages, and configurable consistency levels per operation
- **Data model hierarchy**: Keyspace → Table → Row (analogous to Database → Table → Row in RDBMS)
- **Partition key**: First component of the primary key; determines data distribution across nodes. Remaining primary key columns define clustering order within a partition
- **Denormalized data model**: No JOINs, no ad hoc aggregations — schema must be designed around known access patterns
- **Last-write-wins conflict resolution**: Column timestamps determine which write prevails

## Commands and Syntax

### CQL (Cassandra Query Language)

```sql
CREATE KEYSPACE MyKeySpace
  WITH REPLICATION = { 'class' : 'SimpleStrategy', 'replication_factor' : 3 };

USE MyKeySpace;

CREATE COLUMNFAMILY MyColumns (id text, lastName text, firstName text, PRIMARY KEY(id));

INSERT INTO MyColumns (id, lastName, firstName) VALUES ('1', 'Doe', 'John');

SELECT * FROM MyColumns;
```

### Management

- **Nodetool**: JMX-compliant CLI utility for managing Cassandra clusters — reports disk usage, latency, compaction, garbage collection metrics
- Monitoring via JMX using JConsole or Dropwizard metrics framework (since Cassandra 2.0.2)
- Language drivers available for Java (JDBC), Python (DBAPI2), Node.js (DataStax), Go (gocql), C++

## Relationships

- **Amazon Dynamo**: Cassandra borrows its distributed storage, replication, and consistent hashing techniques from Dynamo
- **Google Bigtable**: The data storage engine model (wide-column, SSTable-based) derives from Bigtable
- **Apache Hadoop**: Cassandra integrates with Hadoop and related big data processing tools
- **LSM trees vs B-trees**: Cassandra's choice of LSM tree indexing is a fundamental architectural distinction from most RDBMS, directly impacting its write-optimized performance profile
- **CAP theorem**: Cassandra is the canonical example of an AP system, contrasting with CP systems like HBase
- **CQL vs SQL**: CQL provides SQL-like syntax but deliberately omits JOINs, subqueries, and complex aggregations

## Exam-Relevant Points

- Cassandra is an **AP system** — availability + partition tolerance, eventual consistency
- Storage uses **LSM trees** (commit log → memtable → SSTable), NOT B-trees. Writes are append-only, never in-place updates
- **Write path**: Write → commit log + memtable → flush to SSTable when threshold reached
- **Read path**: Check memtable first → search SSTables newest-to-oldest using **bloom filters**
- Deletes use **tombstones** (not direct removal) — can cause performance issues in delete-heavy workloads
- **Compaction** merges SSTables, removes tombstones, reclaims space, and improves read performance
- **Gossip protocol** for peer-to-peer cluster communication; **seed nodes** bootstrap the cluster and prevent fragmentation
- **Phi Accrual Failure Detector** for node failure detection (probabilistic, not binary alive/dead)
- **Hinted handoff**: Coordinator stores writes destined for offline nodes as "hints" and replays them when the node returns
- Nodes are only permanently removed via explicit administrative action — temporary failures do NOT trigger data rebalancing
- Data model is **denormalized** — schema must be designed around access patterns
- Keyspace defines replication strategy — replication is configured at the keyspace level, not per-table
- Tables can be created, dropped, or altered at runtime without blocking queries
- Rows in the same table can have different columns (flexible/sparse schema)
