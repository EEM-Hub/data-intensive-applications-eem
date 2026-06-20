---
source: sources/wiki-Database_system.md
source_url: https://en.wikipedia.org/wiki/Database_system
---

## Databases: Foundations, History, and Classification

This page provides a comprehensive overview of databases as organized collections of data managed by database management systems (DBMS). It covers the evolution from navigational databases in the 1960s through relational systems in the 1970s-80s to NoSQL and NewSQL in the 2000s, along with the core terminology, functional groups of DBMS operations, database models, and design considerations including concurrency, fault tolerance, and distributed computing.

## Key Concepts

- A **database** is an organized collection of data; a **DBMS** is the software that manages it; together with applications they form a **database system**
- Four functional groups of DBMS operations: **data definition**, **update**, **retrieval**, and **administration**
- **Navigational databases** (1960s): hierarchical model (IMS) and network model (CODASYL) — used pointers/disk addresses to traverse records
- **Relational model** (1970, Edgar F. Codd): organizes data into tables (relations) with rows (tuples) and columns (domains); uses primary keys instead of disk addresses for cross-references
- **Normalization**: splitting data so each fact is stored once, simplifying updates
- **Declarative query languages** (SQL): express *what* data is needed, not *how* to find it — the DBMS handles query optimization
- **Object-relational impedance mismatch**: the difficulty of translating between programmed objects and relational tables; addressed by object databases, object-relational databases, and ORMs
- **NoSQL** (2000s): non-relational databases using denormalized data, no fixed schemas, horizontal scaling; includes key-value stores and document-oriented databases
- **NewSQL**: relational databases that retain SQL and ACID guarantees while targeting NoSQL-level scalability
- **CAP theorem**: a distributed system cannot simultaneously guarantee consistency, availability, and partition tolerance — pick two. NoSQL often chooses eventual consistency
- Database servers typically use multiprocessor hardware with RAID disk arrays for stable storage

## Commands and Syntax

- **SQL** is the dominant query language for relational databases (standardized)
- **QUEL** was the query language for INGRES (historical)
- **XQuery** is used for XML databases
- CODASYL record access methods: (1) primary key lookup via hashing (CALC key), (2) navigating relationships (sets), (3) sequential scan
- Relational queries use **joins** based on key relationships, grounded in **relational calculus**
- **Views**: virtual tables presenting data differently for different users (not directly updatable in Codd's original model)

## Relationships

- **Data modeling and database design**: the entity-relationship model (1976) became the standard design tool, later retrofitted onto the relational model
- **Distributed computing**: databases must handle concurrent access, fault tolerance, and partition tolerance (connects to CAP theorem, eventual consistency)
- **Query optimization**: enabled by the mathematical foundations of the relational model (first-order predicate calculus)
- **Storage evolution**: sequential magnetic tape -> direct-access magnetic disks (mid-1960s) -> computer clusters and cloud storage
- **Application development**: ORMs bridge the gap between object-oriented programming and relational storage
- Key systems lineage: CODASYL/IMS (navigational) -> System R/INGRES (relational) -> PostgreSQL/Oracle/MySQL (production relational) -> NoSQL/NewSQL (post-relational)

## Exam-Relevant Points

- **Codd's relational model (1970)**: data organized as tables, cross-references via primary keys (not disk addresses), queries via relational calculus — know why this was a departure from navigational models
- **CAP theorem**: impossible for a distributed system to provide consistency, availability, and partition tolerance simultaneously — NoSQL typically sacrifices consistency (eventual consistency)
- **ACID vs. BASE**: NewSQL retains ACID guarantees; NoSQL systems often use eventual consistency for availability + partition tolerance
- **Three eras of database technology**: navigational (1960s), relational/SQL (1970s-80s), post-relational/NoSQL (2000s)
- **Normalization** ensures each fact stored once; **denormalization** (NoSQL) trades this for read performance and horizontal scalability
- **Query optimization** is possible because relational queries have clean mathematical definitions — the DBMS, not the programmer, finds the efficient access path
- **IMS** (IBM, 1966): hierarchical model, developed for Apollo program, still in use
- **Key RDBMS products**: IBM Db2, Oracle, MySQL, Microsoft SQL Server, PostgreSQL
- **NoSQL characteristics**: no fixed schemas, avoid joins, denormalized data, horizontal scaling
- **NewSQL goal**: combine relational/SQL model with NoSQL-level performance for OLTP workloads
