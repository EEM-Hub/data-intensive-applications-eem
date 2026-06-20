---
source: sources/wiki-Multi-master_replication.md
source_url: https://en.wikipedia.org/wiki/Multi-master_replication
---

## Multi-Master Replication in Distributed Databases

Multi-master replication is a database replication method where data is stored across a group of computers and any member can accept writes. The system propagates modifications to all members and resolves conflicts from concurrent changes. This contrasts with master-slave replication (single writer) and failover clustering (passive replicas). The primary goals are increased availability and faster response times.

## Key Concepts

- **Multi-master replication**: All nodes accept reads AND writes; the system handles propagation and conflict resolution
- **Master-slave replication**: Only one designated master can modify a given data item; simpler consistency but less flexible
- **Failover clustering**: Passive replicas prepare to take over if the master fails; only the master serves client interactions
- **Consensus algorithms** are often used to coordinate replication and communication between nodes
- **Lazy/asynchronous replication**: Most multi-master systems are loosely consistent, violating ACID properties in favor of availability
- **Eager/synchronous replication**: Maintains strong consistency but adds complexity and latency (e.g., two-phase commit)
- **Conflict resolution** becomes intractable as node count and latency increase — this is a fundamental scaling challenge
- **Trade-off triangle**: Availability and distributed access (advantages) vs. consistency, performance, and integrity (disadvantages)

## Commands and Syntax

No specific CLI commands, but key architectural patterns appear across implementations:

- **Synchronous (two-phase commit)**: eXtremeDB Cluster, Oracle synchronous mode, Galera Cluster — guarantees ACID, no conflicts possible
- **Asynchronous with conflict resolution**: OpenDS/OpenDJ (publish-subscribe log), CouchDB (MVCC + revision IDs), BDR for PostgreSQL (column-level conflict detection, CRDTs)
- **Circular replication**: MySQL 3.23+ basic multi-master via circular topology
- **Peer-to-peer transactional replication**: Microsoft SQL Server's approach — propagates transactionally consistent changes in near real-time
- **Amazon Aurora model**: Writer nodes send redo records to 6 storage nodes; each storage node checks for conflicts and confirms or rejects

## Relationships

- **Replication spectrum**: Multi-master sits at the most flexible end; master-slave in the middle; failover clustering at the most restricted
- **CAP theorem connection**: ArangoDB explicitly chooses CP (consistency + partition tolerance over availability); CouchDB leans AP with eventual consistency
- **ACID vs. BASE**: Synchronous multi-master (eXtremeDB, Galera) maintains ACID; asynchronous systems (most others) operate under BASE/eventual consistency
- **MVCC**: CouchDB and Cloudant use multiversion concurrency control with revision IDs as their conflict detection mechanism
- **CRDTs**: BDR for PostgreSQL uses conflict-free replicated data types — connects to broader distributed systems theory
- **Directory services** (LDAP, Active Directory) are major consumers of multi-master replication, separate from RDBMS use cases
- **Flexible Single Master Operation (FSMO)**: Active Directory sometimes falls back to single-master for specific operations even within a multi-master architecture

## Exam-Relevant Points

- Multi-master = all nodes accept writes; master-slave = one writer; failover = passive replicas only
- **Main advantage**: High availability (if one master fails, others continue) and distributed geographic access
- **Main disadvantages**: Weak consistency (most implementations are asynchronous/eventually consistent), performance overhead for eager replication, conflict resolution complexity scales poorly
- Synchronous replication uses **two-phase commit** to ensure ACID compliance across nodes
- Asynchronous replication uses a **deferred transaction queue** processed periodically
- CouchDB replication is HTTP-based, uses append-only storage with MVCC, and replicates only the **last revision** of each document
- ArangoDB clusters are **CP** (consistent + partition-tolerant), preferring consistency over availability during network partitions
- Galera Cluster provides synchronous replication so **no conflicts are possible** by design
- MySQL Group Replication (5.7.17+) provides virtual synchronous multi-master with built-in conflict handling
- MariaDB multi-master (10.0+) does **not** support conflict resolution — each master must contain different databases
- PostgreSQL BDR supports column-level conflict detection, CRDTs, eager replication, DDL replication, and online upgrades
- Active Directory uses multi-master replication between Domain Controllers but avoids full-mesh topology to reduce network traffic
- **Transaction replication** (eXtremeDB, Ingres) vs. log-file or SQL-statement replication — transaction-level guarantees atomicity of the replicated unit
