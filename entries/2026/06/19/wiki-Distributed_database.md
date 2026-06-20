---
source: sources/wiki-Distributed_database.md
source_url: https://en.wikipedia.org/wiki/Distributed_database
---

## Distributed Database Fundamentals

A distributed database stores data across multiple physical locations — different machines in one data center or geographically dispersed nodes connected by a network. Unlike parallel systems with tightly coupled processors forming a single system, distributed databases consist of loosely coupled sites sharing no physical components. This architecture can improve end-user performance by distributing transaction processing across many machines.

## Key Concepts

- **Distributed database**: a database where data resides on multiple computers at different physical locations, connected via a network
- **Loosely coupled sites**: distributed DB nodes share no physical components, distinguishing them from tightly coupled parallel systems
- **Replication**: specialized software detects changes in the database and propagates them so all copies converge to the same state; can be complex and resource-intensive
- **Duplication**: designates one database as the master; periodically copies the master to all other locations (typically after hours); users may only modify the master to prevent local overwrites
- **Fragmentation**: splitting a database into fragments distributed across sites (complementary to replication)
- **Local autonomy**: each site can operate independently to some degree
- **Synchronous vs. asynchronous distribution**: synchronous updates all sites in real time within a transaction; asynchronous allows lag between sites
- **Distributed query**: a query (SELECT, INSERT, UPDATE, DELETE) that references tables across multiple external data sources (Microsoft terminology)
- **Distributed SQL**: Oracle's term encompassing distributed queries and distributed transactions as part of a unified SQL layer

## Architecture Types

- **Shared-memory**: all processors access the same memory; very rarely used for distributed databases
- **Shared-disk**: multiple compute nodes share a common storage layer; data is not partitioned; more common for cloud databases (e.g., AWS Aurora, Snowflake, Neon)
- **Shared-nothing**: each node has its own memory and storage; data must be partitioned across nodes (e.g., IBM Db2, Greenplum, MongoDB, Netezza, Teradata, TiDB, Vertica)
- **Hybrid architecture**: modern systems commonly combine shared-nothing compute with shared-disk storage (Snowflake, Aurora) — historically, shared-nothing came first in cloud environments before shared cloud storage made shared-disk viable

## Commands and Syntax

No specific CLI commands are defined by the source, but relevant SQL semantics include:

- **Distributed query example** (Microsoft/OLE DB context): any `SELECT`, `INSERT`, `UPDATE`, or `DELETE` referencing tables from one or more external OLE DB data sources
- **Distributed SQL** (Oracle context): SQL that synchronously accesses and updates data across multiple databases, encompassing both distributed queries and distributed transactions

## Relationships

- **Replication vs. Duplication**: two complementary strategies for keeping distributed copies current — replication is bidirectional and change-driven; duplication is unidirectional from a master
- **CAP theorem**: governs fundamental trade-offs in distributed databases (consistency, availability, partition tolerance)
- **ACID properties**: distributed transactions must maintain atomicity, consistency, isolation, and durability across sites
- **Sharding**: a form of horizontal partitioning required by shared-nothing architectures
- **Federated database systems**: related concept where autonomous databases cooperate under a unified interface
- **Cloud databases**: shared-disk architecture is now more common in cloud deployments than on-premise
- **Data consistency, integrity, and security**: key design considerations that influence the choice of distribution technology

## Exam-Relevant Points

- Shared-nothing requires data partitioning; shared-memory and shared-disk do not
- Replication is change-driven and bidirectional; duplication uses a single master and is typically scheduled (batch)
- In duplication, only the master database can be modified by users
- Modern cloud databases often use a hybrid: shared-nothing compute layer + shared-disk storage layer (Snowflake, Aurora)
- Shared-disk is more common in cloud; shared-nothing was historically the first cloud architecture
- Distributed databases are loosely coupled (vs. tightly coupled parallel systems)
- Microsoft uses "distributed query" (protocol-centric); Oracle uses "distributed SQL" (language-centric) — both describe cross-database operations
- Both replication and duplication serve the goal of keeping data current across all distributed locations, but differ in complexity, directionality, and timing
