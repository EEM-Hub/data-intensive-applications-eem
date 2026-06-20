---
source: https://en.wikipedia.org/wiki/Partition_(database)
fetched: 2026-06-19
---

Divisioning of a logical database Not to be confused with [Network partition](./Network_partition). [![](//upload.wikimedia.org/wikipedia/commons/thumb/7/76/Adminer04.png/250px-Adminer04.png)](./File:Adminer04.png)Partitioning options on a table in MySQL in the environment of the *[Adminer](./Adminer)* tool. 

A **partition** is a division of a logical [database](./Database) or its constituent elements into distinct independent parts. Database partitioning refers to intentionally breaking a large database into smaller ones for scalability purposes, distinct from [network partitions](./Network_partition) which are a type of network fault between nodes.[[1]](./Partition_(database)#cite_note-kleppmann-1) In a partitioned database, each piece of data belongs to exactly one partition, effectively making each partition a small database of its own.[[1]](./Partition_(database)#cite_note-kleppmann-1) Database partitioning is normally done for manageability, [performance](./Optimization_(computer_science)) or [availability](./Availability)[[2]](./Partition_(database)#cite_note-:0-2) reasons, or for [load balancing](./Load_balancing_(computing)). It is popular in [distributed database management systems](./Distributed_database_management_system), where each partition may be spread over multiple nodes, with users at the node performing local transactions on the partition. This increases performance for sites that have regular transactions involving certain views of data, whilst maintaining availability and security.

 

Partitioning enables distribution of datasets across multiple disks and query loads across multiple processors. For queries that operate on a single partition, each node executes queries independently on its local partition, enabling linear scaling of query throughput with additional nodes. More complex queries can be parallelized across multiple nodes, though this presents additional challenges.[[1]](./Partition_(database)#cite_note-kleppmann-1)

 

## History

 

Database partitioning emerged in the 1980s with systems like [Teradata](./Teradata) and [NonStop SQL](./NonStop_SQL). The approach was later adopted by [NoSQL](./NoSQL) databases and [Hadoop](./Apache_Hadoop)-based data warehouses. While implementations vary between [transactional](./Online_transaction_processing) and [analytical](./Data_analysis) workloads, the core principles of partitioning remain consistent across both use cases.[[1]](./Partition_(database)#cite_note-kleppmann-1)

 

## Terminology

 

Different [DBMSs](./Database_Management_System) [[3]](./Partition_(database)#cite_note-3)
use varying terminology for partitioning:

 
- **Shard** in [MongoDB](./MongoDB), [Elasticsearch](./Elasticsearch), and [SolrCloud](./Apache_Solr)
- **Region** in [HBase](./Apache_HBase)
- **Tablet** in [Bigtable](./Bigtable)
- **vnode** in [Cassandra](./Apache_Cassandra) and [Riak](./Riak)
- **vBucket** in [Couchbase](./Couchbase)

 

[[1]](./Partition_(database)#cite_note-kleppmann-1)

 

## Partitioning and Replication

 

Partitioning is commonly implemented alongside [replication](./Database_replication), storing partition copies across multiple nodes. Each record belongs to one partition but may exist on multiple nodes for fault tolerance. In [leader-follower replication systems](./Master-slave_replication), nodes can simultaneously serve as leaders for some partitions and followers for others.[[1]](./Partition_(database)#cite_note-kleppmann-1)

 

## Load Balancing and Hot Spots

 

Partitioning aims to distribute data and query load evenly across nodes. With ideal distribution, system capacity scales linearly with added nodes—ten nodes should process ten times the data and throughput of a single node. Uneven distribution, termed *skew*, reduces partitioning efficiency. Partitions with excessive load are called *hot spots*.[[1]](./Partition_(database)#cite_note-kleppmann-1)

 

Several strategies address hot spots:

 
- Random record assignment to nodes, at the cost of retrieval complexity
- Key-range partitioning with optimized boundaries
- Hash-based partitioning for even load distribution[[1]](./Partition_(database)#cite_note-kleppmann-1)

 

## Partitioning criteria

 

Current high-end [relational database management systems](./Relational_database_management_system) provide for different criteria to split the database. They take a *partitioning key* and assign a partition based on certain criteria. Some common criteria include:

 
- **Range partitioning**: assigns continuous key ranges to partitions, analogous to encyclopedia volumes. Known range boundaries enable direct request routing. Boundaries can be set manually or automatically for balanced distribution. While this enables efficient range scans, certain access patterns create hot spots. For instance, in sensor networks using timestamp keys, writes concentrate in the current time period's partition. Using compound keys—such as prefixing timestamps with sensor identifiers—can distribute this load.[[1]](./Partition_(database)#cite_note-kleppmann-1) An example could be a partition for all [rows](./Row_(database)) where the "zipcode" [column](./Column_(database)) has a value between 70000 and 79999.
- **List partitioning**: a partition is assigned a list of values. If the partitioning key has one of these values, the partition is chosen. For example, all rows where the column `Country` is either `Iceland`, `Norway`, `Sweden`, `Finland` or `Denmark` could build a partition for the [Nordic countries](./Nordic_countries).
- **Composite partitioning**: allows for certain combinations of the above partitioning schemes, by for example first applying a range partitioning and then a hash partitioning.  [Consistent hashing](./Consistent_hashing) could be considered a composite of hash and list partitioning where the hash reduces the key space to a size that can be listed.
- **Round-robin partitioning**: the simplest strategy, it ensures uniform data distribution. With `n` partitions, the `i`th tuple in insertion order is assigned to partition `(i mod n)`. This strategy enables the sequential access to a relation to be done in parallel. However, the direct access to individual tuples, based on a predicate, requires accessing the entire relation.
- **Hash partitioning**: applies a [hash function](./Hash_function) to convert skewed data into [uniform distributions](./Discrete_uniform_distribution) for even load distribution across partitions. While this effectively prevents hot spots, it sacrifices range query efficiency as adjacent keys scatter across partitions. Common implementations include MD5 in [Cassandra](./Apache_Cassandra) and [MongoDB](./MongoDB). Some systems, like Cassandra, combine approaches using compound primary keys: hashing the first component for partitioning while maintaining sort order for remaining components within partitions.[[1]](./Partition_(database)#cite_note-kleppmann-1)

 

In any partitioning scheme, data is typically arranged so that each piece of data (record, row, or document) belongs to exactly one partition.[[1]](./Partition_(database)#cite_note-kleppmann-1) While some databases support operations that span multiple partitions, this single-partition association is fundamental to the partitioning concept.

 

## Partitioning methods

 

The partitioning can be done by either building separate smaller databases (each with its own [tables](./Table_(database)), [indices](./Index_(database)), and [transaction](./Database_transaction) [logs](./Database_log)), or by splitting selected elements, for example just one table.

 

### Horizontal partitioning

 See also: [Shard (database architecture)](./Shard_(database_architecture)) 

Horizontal partitioning involves putting different rows into different tables. For example, customers with [ZIP codes](./ZIP_code) less than 50000 are stored in CustomersEast, while customers with ZIP codes greater than or equal to 50000 are stored in CustomersWest. The two partition tables are then CustomersEast and CustomersWest, while a [view](./View_(database)) with a [union](./Union_(SQL)) might be created over both of them to provide a complete view of all customers.

 

### Vertical partitioning

 

Vertical partitioning involves creating tables with fewer columns and using additional tables to store the remaining columns.[[2]](./Partition_(database)#cite_note-:0-2) Generally, this practice is known as [normalization](./Database_normalization). However, vertical partitioning extends further, and partitions columns even when already normalized. This type of partitioning is also called "row splitting", since rows get split by their columns, and might be performed explicitly or implicitly. Distinct physical machines might be used to realize vertical partitioning: storing infrequently used or very wide columns, taking up a significant amount of memory, on a different machine, for example, is a method of vertical partitioning. A common form of vertical partitioning is to split static data from dynamic data, since the former is faster to access than the latter, particularly for a table where the dynamic data is not used as often as the static. Creating a view across the two newly created tables restores the original table with a performance penalty, but accessing the static data alone will show higher performance. A [columnar database](./Columnar_database) can be regarded as a database that has been vertically partitioned until each column is stored in its own table.

 

## See also

 
- [Block Range Index](./Block_Range_Index)
- [CAP theorem](./CAP_theorem)
- [Data striping](./Data_striping) in RAIDs

 

## References

  
1. [1](./Partition_(database)#cite_ref-kleppmann_1-0) [2](./Partition_(database)#cite_ref-kleppmann_1-1) [3](./Partition_(database)#cite_ref-kleppmann_1-2) [4](./Partition_(database)#cite_ref-kleppmann_1-3) [5](./Partition_(database)#cite_ref-kleppmann_1-4) [6](./Partition_(database)#cite_ref-kleppmann_1-5) [7](./Partition_(database)#cite_ref-kleppmann_1-6) [8](./Partition_(database)#cite_ref-kleppmann_1-7) [9](./Partition_(database)#cite_ref-kleppmann_1-8) [10](./Partition_(database)#cite_ref-kleppmann_1-9) [11](./Partition_(database)#cite_ref-kleppmann_1-10) Kleppmann, Martin (2017). *Designing Data-Intensive Applications: The Big Ideas Behind Reliable, Scalable, and Maintainable Systems*. O'Reilly Media. pp. 199–200. [ISBN](./ISBN_(identifier)) [9781491903100](./Special:BookSources/9781491903100).
2. [1](./Partition_(database)#cite_ref-:0_2-0) [2](./Partition_(database)#cite_ref-:0_2-1) ["Vertical Partitioning Algorithms for Database Design"](http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.97.8306), by Shamkant Navathe, Stefano Ceri, Gio Wiederhold, and Jinglie Dou, Stanford University 1984
3. [↑](./Partition_(database)#cite_ref-3) Not to be confused with a [database](./Database), which is the standalone *repository of bytewise data* (rather than a set of *conventions or rules* describing how to change that data via [create, read, update, or delete](./CRUD) operations).

 
| vteDatabase management systems |
| --- |
| Types | Object-orientedcomparisonRelationallistcomparisonKey–valueColumn-orientedlistDocument-orientedWide-column storeGraphNoSQLNewSQLIn-memorylistMulti-modelcomparisonCloudBlockchain-based database |
| Concepts | DatabaseACIDArmstrong's axiomsCodd's 12 rulesCAP theoremCRUDNullCandidate keyForeign keyPACELC design principleSuperkeySurrogate keyUnique key |
| Objects | RelationtablecolumnrowViewTransactionTransaction logTriggerIndexStored procedureCursorPartition |
| Components | Concurrency controlData dictionaryJDBCXQJODBCQuery languageQuery optimizerQuery rewriting systemQuery plan |
| Functions | AdministrationQuery optimizationReplicationSharding |
| Related topics | Database modelsDatabase normalizationDatabase storageDistributed databaseFederated database systemReferential integrityRelational algebraRelational calculusRelational modelObject–relational databaseTransaction processingList of SQL software and tools |
| CategoryOutline |