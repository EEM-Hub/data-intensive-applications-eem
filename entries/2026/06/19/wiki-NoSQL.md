---
source: sources/wiki-NoSQL.md
source_url: https://en.wikipedia.org/wiki/NoSQL
---

## NoSQL Database Systems: Types, Trade-offs, and Data Modeling

NoSQL ("Not Only SQL") refers to a broad category of non-relational database systems that store and retrieve data using structures other than traditional relational tables. Emerging from Web 2.0 demands in the early 2000s, NoSQL databases are designed for horizontal scalability, flexible schemas, and high availability, typically trading off strict consistency guarantees. They encompass key–value stores, document stores, wide-column stores, graph databases, and several other data models.

## Key Concepts

- **NoSQL** is a colloquial term meaning "not only SQL" or "non-relational" — these databases can coexist with SQL systems in **polyglot-persistent** architectures
- Four primary data models: **key–value**, **document**, **wide-column**, and **graph** — each optimized for different access patterns
- **Schema-free design**: no fixed schema required, enabling storage of unstructured and semi-structured data
- **Horizontal scaling**: data distributed across clusters of commodity machines, unlike vertical scaling typical of relational systems
- **CAP theorem trade-off**: most NoSQL systems prioritize availability and partition tolerance over strong consistency, using **eventual consistency** — updates propagate to all nodes eventually (typically milliseconds) but may produce **stale reads**
- **ACID support is partial**: some systems (MongoDB, ArangoDB, Couchbase, DynamoDB) claim ACID compliance, but the depth and scope varies significantly from relational guarantees
- **Multi-model databases** (ArangoDB, Azure Cosmos DB, MarkLogic) support multiple data models within a single system
- The term "NoSQL" was first used by Carlo Strozzi in 1998 for a relational DB without SQL interface; reintroduced by Johan Oskarsson in 2009 for the modern non-relational movement
- Strozzi himself argued the movement should be called **"NoREL"** since it departs from the relational model, not just SQL

## Commands and Syntax

No universal query language exists — this is a key differentiator and adoption barrier. Query approaches vary by type:

- **Key–value stores**: simple GET/PUT/DELETE by key; some support ordered key ranges for range scans
- **Document stores**: query by document contents via database-specific APIs (e.g., MongoDB Query Language, CouchDB MapReduce)
- **Graph databases**: specialized query languages — **Cypher** (Neo4j, AgensGraph), **Gremlin** (Amazon Neptune, Cosmos DB), **SPARQL** (for RDF triple stores like AllegroGraph)
- **Wide-column stores**: CQL (Cassandra), HBase shell/Java API

### Handling Relational Data in NoSQL (Three Techniques)

1. **Multiple queries**: issue several simple queries instead of one join — viable because individual NoSQL queries are fast
2. **Denormalization**: store foreign values alongside the record (e.g., embed username with each comment, not just user ID) — optimized for read-heavy workloads but creates update anomalies
3. **Nesting/embedding**: store related data within a single document (e.g., comments inside a blog post document) — single retrieval gets all needed data

## Relationships

- **CAP theorem**: the theoretical foundation for understanding NoSQL consistency trade-offs — choosing between Consistency, Availability, and Partition tolerance
- **ACID properties**: NoSQL systems partially overlap with relational guarantees; understanding where they diverge is critical
- **Eventual consistency** vs. **serializability**: the consistency spectrum that NoSQL databases operate on
- **Horizontal scaling / sharding**: the scaling model that motivates NoSQL adoption over vertical-scaling relational systems
- **Polyglot persistence**: architectural pattern where multiple database types coexist, each used for what it does best
- **Write-ahead logging (WAL)**: durability mechanism some NoSQL systems use to prevent data loss
- **YCSB (Yahoo Cloud Serving Benchmark)**: standard benchmark for comparing NoSQL performance
- **Distributed transaction processing / X/Open XA**: cross-database consistency remains hard for both NoSQL and relational systems
- **MapReduce / Bigtable / DynamoDB**: the Google and Amazon systems that inspired the NoSQL movement

## Exam-Relevant Points

- **Know the four primary NoSQL types and their characteristics**: key–value (simplest, highest performance), document (flexible schema, content-addressable), wide-column (high scalability), graph (relationship-rich data)
- **Ben Scofield's comparison matrix**: key–value and column stores rate highest on performance and scalability; relational databases rate highest on data integrity; graph databases are the most complex NoSQL type
- **Eventual consistency produces stale reads** — updates propagate in milliseconds but are not instantaneous
- **Three techniques for handling relational data** without joins: multiple queries, denormalization, and nesting
- **Denormalization trade-off**: faster reads but requires updating data in many places when source values change — best when reads >> writes
- **Adoption barriers**: low-level query languages, no ad hoc joins, no standardized interfaces, existing relational investments
- **Query optimization varies by type**: MongoDB uses compound indexes, Cassandra uses secondary indexes and materialized views, Elasticsearch uses inverted indexes — but non-indexed field queries typically require full scans
- **ACID + join support is not uniform**: MongoDB only supported joins from sharded collections starting in v5.1; MarkLogic uses semantics for joins; OrientDB uses direct record links
- **Data loss risk**: some NoSQL systems can lose data through lost writes; WAL mitigates this
- **Performance metric**: throughput measured as operations/second; must benchmark with production-realistic configurations and workloads
