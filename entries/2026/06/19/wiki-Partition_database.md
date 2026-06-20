---
source: sources/wiki-Partition_database.md
source_url: https://en.wikipedia.org/wiki/Partition_(database)
---

## Database Partitioning: Strategies, Methods, and Load Distribution

Database partitioning is the intentional division of a logical database into smaller, independent parts for scalability, manageability, performance, or availability. Each piece of data belongs to exactly one partition, making each partition effectively a small database of its own. This is distinct from network partitions (a type of network fault). Partitioning is fundamental to distributed database management systems, where partitions are spread across multiple nodes to enable local transactions, parallel query execution, and linear scaling of throughput.

## Key Concepts

- **Partition**: A distinct, independent subset of a database where each record belongs to exactly one partition
- **Partitioning key**: The attribute used to determine which partition a record belongs to
- **Skew**: Uneven distribution of data or query load across partitions, reducing partitioning efficiency
- **Hot spot**: A partition receiving disproportionately high load compared to others
- **Partitioning is not network partitioning**: Database partitioning is an intentional design choice for scalability; network partitions are faults between nodes
- **Linear scaling**: With ideal (even) distribution, ten nodes should handle ten times the data and throughput of one node
- **Each record belongs to exactly one partition**, though cross-partition operations may be supported
- **Partitioning and replication are complementary**: Partition copies are stored on multiple nodes for fault tolerance; a node can be leader for some partitions and follower for others simultaneously

## Commands and Syntax

No specific CLI commands are defined in this topic, but key configuration concepts include:

- **Range partitioning example** (SQL-style): Partition by zipcode ranges (e.g., 70000–79999)
- **List partitioning example**: Partition by explicit value lists (e.g., `Country IN ('Iceland', 'Norway', 'Sweden', 'Finland', 'Denmark')`)
- **Hash partitioning**: Apply a hash function (e.g., MD5 in Cassandra/MongoDB) to the partitioning key
- **Compound primary keys** (Cassandra pattern): Hash the first key component for partition assignment, maintain sort order on remaining components within partitions
- **Composite partitioning**: Combine strategies, e.g., range then hash
- **Round-robin**: Assign the i-th tuple to partition `(i mod n)`

## Relationships

- **Replication**: Partitioning is typically combined with replication for fault tolerance; leader-follower replication applies per-partition
- **Consistent hashing**: A composite of hash and list partitioning; reduces key space to a listable size
- **Sharding**: Synonym for partitioning in MongoDB, Elasticsearch, SolrCloud contexts
- **CAP theorem**: Partitioning interacts with availability and consistency trade-offs
- **Columnar databases**: Can be viewed as an extreme form of vertical partitioning (each column in its own table)
- **Database normalization**: Vertical partitioning extends normalization principles further
- **Distributed databases**: Partitioning is a core enabling technique
- **Load balancing**: Partitioning is a primary mechanism for distributing query and data load

## Terminology Across Systems

| Term | System(s) |
|------|-----------|
| Shard | MongoDB, Elasticsearch, SolrCloud |
| Region | HBase |
| Tablet | Bigtable |
| vnode | Cassandra, Riak |
| vBucket | Couchbase |

## Partitioning Methods

- **Horizontal partitioning (sharding)**: Different rows go to different tables/nodes. Example: customers split by ZIP code into CustomersEast and CustomersWest, with a union view for the complete dataset.
- **Vertical partitioning (row splitting)**: Tables split by columns. Goes beyond normalization. Common pattern: separate static data from dynamic data for faster access. Infrequently used or wide columns can be stored on different machines.

## Exam-Relevant Points

- Each record belongs to **exactly one partition** — this is fundamental and always tested
- Know the difference between **database partitioning** (intentional, for scalability) and **network partitions** (faults)
- **Skew** = uneven distribution; **hot spot** = overloaded partition — know both terms
- **Range partitioning** enables efficient range scans but risks hot spots (e.g., timestamp keys concentrating writes); mitigation: compound keys (prefix with another identifier)
- **Hash partitioning** prevents hot spots but **sacrifices range query efficiency** — this trade-off is heavily tested
- **Cassandra's compound primary key** approach: hash first component for partitioning, sort remaining components within partitions — a hybrid that gets both distribution and local ordering
- **Round-robin** guarantees uniform distribution but requires accessing the **entire relation** for predicate-based lookups
- Know the terminology mapping: shard (MongoDB), region (HBase), tablet (Bigtable), vnode (Cassandra/Riak), vBucket (Couchbase)
- **Partitioning + replication**: A single node can be leader for some partitions and follower for others simultaneously
- **Vertical partitioning** separates static from dynamic data for performance; columnar databases are the extreme case
- **Horizontal partitioning** = different rows in different tables; **vertical partitioning** = different columns in different tables
- History: Emerged in the 1980s with Teradata and NonStop SQL; later adopted by NoSQL and Hadoop-based systems
- Primary source: Kleppmann, *Designing Data-Intensive Applications* (2017), pp. 199–200
