---
source: https://en.wikipedia.org/wiki/Apache_Cassandra
fetched: 2026-06-19
---

Free and open-source database management system 
|  | This article'suse ofexternal linksmay not follow Wikipedia's policies or guidelines.Pleaseimprove this articleby removingexcessiveorinappropriateexternal links, and converting useful links where appropriate intofootnote references.(October 2023)(Learn how and when to remove this message) |
| --- | --- |

 

 

 
| Apache Cassandra |
| --- |
|  |
| Original authors | Avinash Lakshman, Prashant Malik /Facebook |
| Developer | Apache Software Foundation |
| Release | July2008;17years ago(2008-07) |
|  |
| Stable release | 5.0.8[1]/ April 16, 2026;2 months ago(April 16, 2026) |
|  |
| Written in | Java |
| Operating system | Cross-platform |
| Available in | English |
| Type | NoSQLDatabase,data store |
| License | Apache License 2.0 |
| Website | cassandra.apache.org |
| Repository | github.com/apache/cassandra |

  

**Apache Cassandra** is a [free and open-source](./Free_and_open-source_software) [database management system](./Database_management_system) designed to handle large volumes of data across multiple [commodity servers](./Commodity_computing). The system prioritizes availability and [scalability](./Scalability) over [consistency](./Consistency_(database_systems)), making it particularly suited for systems with high write throughput requirements due to its [LSM tree](./Log-structured_merge-tree) indexing storage layer.[[2]](./Apache_Cassandra#cite_note-carpenter2022-2) As a [wide-column database](./Wide_column_store), Cassandra supports flexible schemas and efficiently handles data models with numerous sparse columns. The system is optimized for applications with well-defined data access patterns that can be incorporated into the schema design.[[2]](./Apache_Cassandra#cite_note-carpenter2022-2) Cassandra supports [computer clusters](./Computer_cluster) which may span multiple [data centers](./Data_center),[[3]](./Apache_Cassandra#cite_note-3) featuring [asynchronous](./Asynchrony_(computer_programming)) and masterless replication. It enables [low-latency](./Latency_(engineering)) operations for all clients and incorporates [Amazon](./Amazon_(company))'s [Dynamo](./Dynamo_(storage_system)) [distributed storage](./Distributed_storage) and replication techniques, combined with [Google](./Google)'s [Bigtable](./Bigtable) data storage engine model.[[4]](./Apache_Cassandra#cite_note-4)

 

## History

 

Avinash Lakshman, a co-author of [Amazon](./Amazon_(company))'s [Dynamo](./Dynamo_(storage_system)), and Prashant Malik developed Cassandra at [Facebook](./Facebook) to support the [inbox](./Inbox) [search](./Search_engine) functionality. Facebook released Cassandra as open-source software on [Google Code](./Google_Code) in July 2008.[[5]](./Apache_Cassandra#cite_note-JH2008-5) In March 2009, it became an Apache Incubator project[[6]](./Apache_Cassandra#cite_note-6) and on February 17, 2010, it graduated to a top-level project.[[7]](./Apache_Cassandra#cite_note-GRAD-7)

 

The developers at [Facebook](./Facebook) named their database after [Cassandra](./Cassandra), the [mythological](./Mythological) [Trojan](./Troy) prophetess, referencing her curse of making prophecies that were never believed.[[8]](./Apache_Cassandra#cite_note-8)

 

## Features and limitations

 
|  | This sectionmay incorporate text from alarge language model, which isprohibited in Wikipedia articles.It may includehallucinatedinformation,copyright violations, claims notverifiedin cited sources,original research, orfictitious references. Any such material should beremoved. The reason given is:this 2024 rewrite; noteWP:AISIGNSin superficial analyses, vocab distro typical of LLM output etc(March 2026)(Learn how and when to remove this message) |
| --- | --- |

 

Cassandra uses a [distributed architecture](./Distributed_architecture) where all nodes perform identical functions, eliminating single points of failure. The system employs configurable replication strategies to distribute data across clusters, providing redundancy and disaster recovery capabilities. The system is capable of linear scaling, which increases read and write throughput with the addition of new nodes, while maintaining continuous service.

 

Cassandra is categorized as an AP ([Availability](./Availability_(system)) and Partition Tolerance) system, emphasizing availability and partition tolerance over [consistency](./Consistency_(database_systems)). While it offers tunable consistency levels for both read and write operations, its architecture makes it less suitable for use cases requiring strict consistency guarantees.[[2]](./Apache_Cassandra#cite_note-carpenter2022-2) Additionally, Cassandra's compatibility with [Hadoop](./Apache_Hadoop) and related tools allows for integration with existing big data processing workflows. Eventual consistency is maintained using [tombstones](./Tombstone_(data_store)) to manage reads, [upserts](./UPSERT), and deletes.

 

The system's query capabilities have notable limitations. Cassandra does not support advanced query patterns such as multi-table [JOINs](./Join_(SQL)), ad hoc aggregations, or complex queries.[[2]](./Apache_Cassandra#cite_note-carpenter2022-2) These limitations stem from its distributed architecture, which optimizes for scalability and availability rather than complex query operations.

 

## Data model

 

As a [wide-column store](./Wide_column_store), Cassandra combines features of both key-value and tabular database systems. It implements a partitioned row store model with adjustable consistency levels.[[9]](./Apache_Cassandra#cite_note-tunable_consistency-9) The following table compares Cassandra and [relational database management systems](./Relational_database_management_systems) (RDBMS).

 
| Feature | Cassandra | RDBMS |
| --- | --- | --- |
| Organization | Keyspace → Table → Row | Database → Table → Row |
| Row Structure | Dynamic columns | Fixed schema |
| Column Data | Name, type, value, timestamp | Name, type, value |
| Schema Changes | Runtime modifications | Usually requires downtime |
| Data Model | Denormalized | Normalized with JOINs |

 

The data model consists of several hierarchical components:

 

### Keyspace

 

A keyspace in Cassandra is analogous to a database in [relational systems](./Relational_database_management_system). It contains multiple tables and manages configuration information, including replication strategy and user-defined types (UDTs).[[2]](./Apache_Cassandra#cite_note-carpenter2022-2)

 

### Tables

 

Tables (formerly called [column families](./Column_family) prior to CQL 3) are containers for rows of data. Each table has a name and configuration information for its stored data. Tables may be created, dropped, or altered at run-time without blocking [updates](./Update_(SQL)) and queries.[[10]](./Apache_Cassandra#cite_note-10)

 

### Rows and columns

 

Each row is identified by a [primary key](./Primary_key) and contains columns. The first component of a table's primary key is the partition key; within a partition, rows are [clustered](./Clustered_index) by the remaining columns of the key.[[11]](./Apache_Cassandra#cite_note-11)

 

Columns contain data belonging to a row and consist of:

 
- A name
- A type
- A value
- Timestamp metadata (used for write conflict resolution via "last write wins")

 

Unlike traditional RDBMS tables, rows within the same table can have varying columns, providing a flexible structure. This flexibility distinguishes Cassandra from relational databases, as not all columns need to be specified for each row.[[2]](./Apache_Cassandra#cite_note-carpenter2022-2) Other columns may be indexed separately from the primary key.[[12]](./Apache_Cassandra#cite_note-12)

 

## Storage model

 

Cassandra uses a [Log Structured Merge Tree (LSM tree)](./Log-structured_merge-tree) index to optimize write throughput, in contrast to the [B-tree indexes](./B_tree_indexing) used by most databases.[[2]](./Apache_Cassandra#cite_note-carpenter2022-2)

 
| Feature | Cassandra | RDBMS |
| --- | --- | --- |
| Index Structure | LSM Tree | B-Tree |
| Write Process | Append-only with Memtable | In-place updates |
| Storage Components | Commit Log, Memtable, SSTable | Data files, Transaction Log |
| Update Strategy | New entry for each change | Modify existing data |
| Delete Handling | Tombstone markers | Direct removal |
| Read Optimization | Secondary | Primary |
| Write Optimization | Primary | Secondary |

 

The storage architecture consists of three main components:[[2]](./Apache_Cassandra#cite_note-carpenter2022-2)

 

### Core components

 
- **Commit Log**: A [write-ahead log](./Write-ahead_logging) that ensures write durability
- **Memtable**: An [in-memory](./In-memory_processing) data structure that stores writes, sorted by primary key
- **SSTable** (Sorted String Table): Immutable files containing data flushed from Memtables

 

### Write and read processes

 

Write operations follow a two-stage process:

 
1. The write is recorded in the commit log and added to the Memtable
2. When the Memtable reaches size or time thresholds, it flushes to an SSTable

 

Read operations:

 
1. Check Memtable for latest data
2. Search SSTables from newest to oldest using bloom filters for efficiency

 

### Data management

 

#### Tombstones

 

Every operation (create/update/delete) generates a new entry, with deletes handled via "[tombstones](./Tombstone_(data_store))". While common in many databases, tombstones can cause performance degradation in delete-heavy workloads.[[13]](./Apache_Cassandra#cite_note-13)

 

#### Compaction

 

Compaction consolidates multiple SSTables to:

 
- Reduce storage usage
- Remove deleted row tombstones
- Improve read performance

 

## Cassandra Query Language

 

Cassandra Query Language (CQL) is the interface for accessing Cassandra, as an alternative to the traditional [Structured Query Language](./SQL) (SQL). CQL adds an [abstraction layer](./Abstraction_layer) that hides implementation details of this structure and provides native syntaxes for collections and other common encodings. Language drivers are available for [Java](./Java_(programming_language)) ([JDBC](./Java_Database_Connectivity)), [Python](./Python_(programming_language)) (DBAPI2), [Node.JS](./Node.js) ([DataStax](./DataStax)), [Go](./Go_(programming_language)) (gocql), and [C++](./C++).[[14]](./Apache_Cassandra#cite_note-14)

The key space in Cassandra is a namespace that defines data replication across nodes. Therefore, replication is defined at the key space level. Below is an example of key space creation, including a column family in CQL 3.0:[[15]](./Apache_Cassandra#cite_note-15)

```
CREATE KEYSPACE MyKeySpace
  WITH REPLICATION = { 'class' : 'SimpleStrategy', 'replication_factor' : 3 };

USE MyKeySpace;

CREATE COLUMNFAMILY MyColumns (id text, lastName text, firstName text, PRIMARY KEY(id));

INSERT INTO MyColumns (id, lastName, firstName) VALUES ('1', 'Doe', 'John');

SELECT * FROM MyColumns;

```
 

Which gives:

 
```
 id | lastName | firstName
----+----------+----------
  1 | Doe      | John

(1 rows)

```
 

## Distributed architecture

 

### Gossip protocol

 

Cassandra uses a peer-to-peer gossip protocol for cluster communication. Nodes routinely exchange information about cluster state, including:

 
- Node availability status
- Schema versions
- Generation timestamps (node bootstrap time)
- Version numbers (logical clock values)

 

The system uses [vector clocks](./Vector_clock) to track information currency and ignore outdated state data.[[2]](./Apache_Cassandra#cite_note-carpenter2022-2)

 

### Seed nodes

 

The architecture designates certain nodes as "seed" nodes that:

 
- Bootstrap the cluster
- Serve as guaranteed gossip communication points
- Prevent cluster fragmentation
- Remain discoverable via service discovery methods

 

This design eliminates single points of failure while maintaining cluster-wide consistency of operational knowledge.[[2]](./Apache_Cassandra#cite_note-carpenter2022-2)

 

### Fault tolerance

 

Cassandra employs the Phi Accrual Failure Detector to manage node failures during cluster operation.[[16]](./Apache_Cassandra#cite_note-16) Through this system, each node independently assesses the availability of other nodes during gossip communication. When a node fails to respond, it is "convicted" and removed from write operations, though it can rejoin the cluster upon resuming heartbeat signals.[[2]](./Apache_Cassandra#cite_note-carpenter2022-2)

 

To maintain data integrity during node outages, Cassandra uses a "hinted handoff" mechanism. When writing to an offline node, the coordinator node temporarily stores the write data as a "hint." Once the offline node returns to service, these hints are forwarded to restore data consistency. Notably, Cassandra only permanently removes nodes through explicit administrative decommissioning or rebuilding, preventing temporary communication failures or restarts from triggering unnecessary data rebalancing.[[2]](./Apache_Cassandra#cite_note-carpenter2022-2)

 

## Management and monitoring

 

Cassandra is a Java-based system that can be managed and monitored via [Java Management Extensions](./Java_Management_Extensions) (JMX). The JMX-compliant *Nodetool* utility, for instance, can be used to manage a Cassandra cluster.[[17]](./Apache_Cassandra#cite_note-17) Nodetool also offers a number of commands to return Cassandra metrics pertaining to disk usage, latency, compaction, garbage collection, and more.[[18]](./Apache_Cassandra#cite_note-18)

 

Since the release of Cassandra 2.0.2 in 2013, measures of several metrics are produced via the Dropwizard metrics framework,[[19]](./Apache_Cassandra#cite_note-19) and may be queried via JMX using tools such as [JConsole](./JConsole) or passed to external monitoring systems via Dropwizard-compatible reporter plugins.[[20]](./Apache_Cassandra#cite_note-20)

 

## Releases

 

Releases after graduation include:

 
| Version | Original release date | Latest version | Release date | Status[21] |
| --- | --- | --- | --- | --- |
| Unsupported:0.6 | 2010-04-12 | 0.6.13 | 2011-04-18 | No longer maintained |
| Unsupported:0.7 | 2011-01-10 | 0.7.10 | 2011-10-31 | No longer maintained |
| Unsupported:0.8 | 2011-06-03 | 0.8.10 | 2012-02-13 | No longer maintained |
| Unsupported:1.0 | 2011-10-18 | 1.0.12 | 2012-10-04 | No longer maintained |
| Unsupported:1.1 | 2012-04-24 | 1.1.12 | 2013-05-27 | No longer maintained |
| Unsupported:1.2 | 2013-01-02 | 1.2.19 | 2014-09-18 | No longer maintained |
| Unsupported:2.0 | 2013-09-03 | 2.0.17 | 2015-09-21 | No longer maintained |
| Unsupported:2.1 | 2014-09-16 | 2.1.22 | 2020-08-31 | No longer maintained |
| Unsupported:2.2 | 2015-07-20 | 2.2.19 | 2020-11-04 | No longer maintained |
| Unsupported:3.0 | 2015-11-09 | 3.0.29 | 2023-05-15 | No longer maintained |
| Unsupported:3.11 | 2017-06-23 | 3.11.15 | 2023-05-05 | No longer maintained |
| Supported:4.0 | 2021-07-26 | 4.0.18 | 2025-05-28 | Maintained until 5.1.0 release |
| Supported:4.1 | 2022-06-17 | 4.1.9 | 2025-05-19 | Maintained until 5.2.0 release |
| Latest version:5.0 | 2024-09-05 | 5.0.6 | 2025-10-29 | Latest release. Maintained until 5.3.0 release |
| Legend:UnsupportedSupportedLatest versionPreview versionFuture version |

  o=Old&#x2D;Not&#x2D;Supported; co=Old&#x2D;Still&#x2D;Supported; c=Latest&#x2D;Stable; cp=Preview; p=Planned&#x2D;Future  

## See also

 
- ![](//upload.wikimedia.org/wikipedia/commons/thumb/3/31/Free_and_open-source_software_logo_%282009%29.svg/40px-Free_and_open-source_software_logo_%282009%29.svg.png)[Free and open-source software portal](./Portal:Free_and_open-source_software)

 
- [Bigtable](./Bigtable) – Original distributed database by Google
- [Distributed database](./Distributed_database)
- [Distributed hash table](./Distributed_hash_table) (DHT)
- [Dynamo (storage system)](./Dynamo_(storage_system)) – Cassandra borrows many elements from Dynamo

 

## References

 
1. [↑](./Apache_Cassandra#cite_ref-wikidata-35275c4d9c9993e8d946117bf5d6fdca47d96452-v20_1-0)  [https://github.com/apache/cassandra/releases/tag/cassandra-5.0.8](https://github.com/apache/cassandra/releases/tag/cassandra-5.0.8). Retrieved May 5, 2026. `{{cite web}}`: Missing or empty `|title=` ([help](./Help:CS1_errors#citation_missing_title))
2. [1](./Apache_Cassandra#cite_ref-carpenter2022_2-0) [2](./Apache_Cassandra#cite_ref-carpenter2022_2-1) [3](./Apache_Cassandra#cite_ref-carpenter2022_2-2) [4](./Apache_Cassandra#cite_ref-carpenter2022_2-3) [5](./Apache_Cassandra#cite_ref-carpenter2022_2-4) [6](./Apache_Cassandra#cite_ref-carpenter2022_2-5) [7](./Apache_Cassandra#cite_ref-carpenter2022_2-6) [8](./Apache_Cassandra#cite_ref-carpenter2022_2-7) [9](./Apache_Cassandra#cite_ref-carpenter2022_2-8) [10](./Apache_Cassandra#cite_ref-carpenter2022_2-9) [11](./Apache_Cassandra#cite_ref-carpenter2022_2-10) [12](./Apache_Cassandra#cite_ref-carpenter2022_2-11) Carpenter, Jeff; Hewitt, Eben (2022). *Cassandra: The Definitive Guide* (3rd ed.). [O'Reilly Media](./O'Reilly_Media). [ISBN](./ISBN_(identifier)) [978-1-4920-9710-5](./Special:BookSources/978-1-4920-9710-5).
3. [↑](./Apache_Cassandra#cite_ref-3) Casares, Joaquin (November 5, 2012). ["Multi-datacenter Replication in Cassandra"](http://www.datastax.com/dev/blog/multi-datacenter-replication). DataStax. Retrieved July 25, 2013. Cassandra's innate datacenter concepts are important as they allow multiple workloads to be run across multiple datacenters...
4. [↑](./Apache_Cassandra#cite_ref-4) ["Apache Cassandra Documentation Overview"](https://cassandra.apache.org/doc/latest/architecture/overview.html). Retrieved January 21, 2021.
5. [↑](./Apache_Cassandra#cite_ref-JH2008_5-0) Hamilton, James (July 12, 2008). ["Facebook Releases Cassandra as Open Source"](http://perspectives.mvdirona.com/2008/07/12/FacebookReleasesCassandraAsOpenSource.aspx). Retrieved June 4, 2009.
6. [↑](./Apache_Cassandra#cite_ref-6) ["Is this the new hotness now?"](http://www.mail-archive.com/cassandra-dev@incubator.apache.org/msg00004.html). Mail-archive.com. March 2, 2009. [Archived](https://web.archive.org/web/20100425071855/http://www.mail-archive.com/cassandra-dev%40incubator.apache.org/msg00004.html) from the original on April 25, 2010. Retrieved March 29, 2010.
7. [↑](./Apache_Cassandra#cite_ref-GRAD_7-0) ["Cassandra is an Apache top level project"](http://www.mail-archive.com/cassandra-dev@incubator.apache.org/msg01518.html). Mail-archive.com. February 18, 2010. [Archived](https://web.archive.org/web/20100328090322/http://www.mail-archive.com/cassandra-dev%40incubator.apache.org/msg01518.html) from the original on March 28, 2010. Retrieved March 29, 2010.
8. [↑](./Apache_Cassandra#cite_ref-8) ["The meaning behind the name of Apache Cassandra"](https://web.archive.org/web/20161101091045/http://kellabyte.com/2013/01/04/the-meaning-behind-the-name-of-apache-cassandra). Archived from [the original](http://kellabyte.com/2013/01/04/the-meaning-behind-the-name-of-apache-cassandra/) on November 1, 2016. Retrieved July 19, 2016. Apache Cassandra is named after the Greek mythological prophet Cassandra. [...] Because of her beauty Apollo granted her the ability of prophecy. [...] When Cassandra of Troy refused Apollo, he put a curse on her so that all of her and her descendants' predictions would not be believed. [...] Cassandra is the cursed Oracle[.]
9. [↑](./Apache_Cassandra#cite_ref-tunable_consistency_9-0) [DataStax](./DataStax) (January 15, 2013). ["About data consistency"](https://web.archive.org/web/20130726185743/http://www.datastax.com/docs/1.2/dml/data_consistency). Archived from [the original](http://www.datastax.com/docs/1.2/dml/data_consistency) on July 26, 2013. Retrieved July 25, 2013.
10. [↑](./Apache_Cassandra#cite_ref-10) Ellis, Jonathan (March 2, 2012). ["The Schema Management Renaissance in Cassandra 1.1"](http://www.datastax.com/dev/blog/the-schema-management-renaissance). DataStax. Retrieved July 25, 2013.
11. [↑](./Apache_Cassandra#cite_ref-11) Ellis, Jonathan (February 15, 2012). ["Schema in Cassandra 1.1"](http://www.datastax.com/dev/blog/schema-in-cassandra-1-1). DataStax. Retrieved July 25, 2013.
12. [↑](./Apache_Cassandra#cite_ref-12) Ellis, Jonathan (December 3, 2010). ["What's new in Cassandra 0.7: Secondary indexes"](http://www.datastax.com/dev/blog/whats-new-cassandra-07-secondary-indexes). DataStax. Retrieved July 25, 2013.
13. [↑](./Apache_Cassandra#cite_ref-13) Rodriguez, Alain (July 27, 2016). ["About Deletes and Tombstones in Cassandra"](https://thelastpickle.com/blog/2016/07/27/about-deletes-and-tombstones.html).
14. [↑](./Apache_Cassandra#cite_ref-14) ["DataStax C/C++ Driver for Apache Cassandra"](https://github.com/datastax/cpp-driver). *DataStax*. Retrieved December 15, 2014.
15. [↑](./Apache_Cassandra#cite_ref-15) ["CQL"](https://web.archive.org/web/20160113141740/http://cassandra.apache.org/doc/cql3/CQL.html). Archived from [the original](https://cassandra.apache.org/doc/cql3/CQL.html) on January 13, 2016. Retrieved January 5, 2016.
16. [↑](./Apache_Cassandra#cite_ref-16) Hayashibara, Naohiro; Défago, Xavier; Yared, Rami; Katayama, Takuya (2004). "The Φ Accrual Failure Detector". *IEEE Symposium on Reliable Distributed Systems*. pp. 66–78. [doi](./Doi_(identifier)):[10.1109/RELDIS.2004.1353004](https://doi.org/10.1109%2FRELDIS.2004.1353004).
17. [↑](./Apache_Cassandra#cite_ref-17) ["NodeTool"](https://web.archive.org/web/20160113122938/http://wiki.apache.org/cassandra/NodeTool). *Cassandra Wiki*. Archived from [the original](https://wiki.apache.org/cassandra/NodeTool) on January 13, 2016. Retrieved January 5, 2016.
18. [↑](./Apache_Cassandra#cite_ref-18) ["How to monitor Cassandra performance metrics"](https://www.datadoghq.com/blog/how-to-monitor-cassandra-performance-metrics/). Datadog. December 3, 2015. Retrieved January 5, 2016.
19. [↑](./Apache_Cassandra#cite_ref-19) ["Metrics"](https://web.archive.org/web/20151112112756/http://wiki.apache.org/cassandra/Metrics). *Cassandra Wiki*. Archived from [the original](https://wiki.apache.org/cassandra/Metrics) on November 12, 2015. Retrieved January 5, 2016.
20. [↑](./Apache_Cassandra#cite_ref-20) ["Monitoring"](https://cassandra.apache.org/doc/latest/operating/metrics.html). *Cassandra Documentation*. Retrieved February 1, 2018.
21. [↑](./Apache_Cassandra#cite_ref-21)  ["Cassandra Server Releases"](https://cassandra.apache.org/download/). *cassandra.apache.org*. Retrieved December 15, 2015. 

 

## Bibliography

  
- Carpenter, Jeff; Hewitt, Eben (January 23, 2022). *Cassandra: The Definitive Guide* (3rd ed.). [O'Reilly Media](./O'Reilly_Media). p. 432. [ISBN](./ISBN_(identifier)) [978-1-4920-9710-5](./Special:BookSources/978-1-4920-9710-5).
- Capriolo, Edward (July 15, 2011). [*Cassandra High Performance Cookbook*](http://www.packtpub.com/cassandra-apache-high-performance-cookbook/book) (1st ed.). [Packt Publishing](./Packt_Publishing). p. 324. [ISBN](./ISBN_(identifier)) [978-1-84951-512-2](./Special:BookSources/978-1-84951-512-2).
- Hewitt, Eben (December 15, 2010). [*Cassandra: The Definitive Guide*](http://shop.oreilly.com/product/0636920010852.do) (1st ed.). [O'Reilly Media](./O'Reilly_Media). p. 300. [ISBN](./ISBN_(identifier)) [978-1-4493-9041-9](./Special:BookSources/978-1-4493-9041-9).

  

## External links

   [![Wikimedia Commons logo](//upload.wikimedia.org/wikipedia/en/thumb/4/4a/Commons-logo.svg/40px-Commons-logo.svg.png)](./File:Commons-logo.svg) Wikimedia Commons has media related to [Apache Cassandra](https://commons.wikimedia.org/wiki/Category:Apache%20Cassandra).    [![Wikiversity logo](//upload.wikimedia.org/wikipedia/commons/thumb/0/0b/Wikiversity_logo_2017.svg/40px-Wikiversity_logo_2017.svg.png)](./File:Wikiversity_logo_2017.svg) Wikiversity has learning resources about ***[Big Data/Cassandra](https://en.wikiversity.org/wiki/Big%20Data/Cassandra)***  
- Lakshman, Avinash (August 25, 2008). ["Cassandra - A structured storage system on a P2P Network"](https://www.facebook.com/note.php?note_id=24413138919&id=9445547199&index=9). Engineering @ Facebook's Notes. Retrieved June 17, 2014.
- ["The Apache Cassandra Project"](https://cassandra.apache.org/). Forest Hill, MD, USA: [The Apache Software Foundation](./Apache_Software_Foundation). Retrieved June 17, 2014.
- ["Project Wiki"](https://web.archive.org/web/20140614175405/http://wiki.apache.org/cassandra/). Forest Hill, MD, USA: [The Apache Software Foundation](./Apache_Software_Foundation). Archived from [the original](https://wiki.apache.org/cassandra/) on June 14, 2014. Retrieved June 17, 2014.
- Hewitt, Eben (December 1, 2010). ["Adopting Apache Cassandra"](http://www.infoq.com/presentations/Adopting-Apache-Cassandra). *infoq.com*. InfoQ, C4Media Inc. Retrieved June 17, 2014.
- Lakshman, Avinash; Malik, Prashant (August 15, 2009). ["Cassandra - A Decentralized Structured Storage System"](https://www.cs.cornell.edu/projects/ladis2009/papers/lakshman-ladis2009.pdf) (PDF). *cs.cornell.edu*. The authors are from [Facebook](./Facebook). Retrieved June 17, 2014.
- Ellis, Jonathan (July 29, 2009). ["What Every Developer Should Know About Database Scalability"](https://www.slideshare.net/jbellis/what-every-developer-should-know-about-database-scalability). *slideshare.net*. Retrieved June 17, 2014. From the [OSCON](./O'Reilly_Open_Source_Convention) 2009 talk on RDBMS vs. Dynamo, Bigtable, and Cassandra.
- ["Cassandra-RPM - Red Hat Package Manager (RPM) build for the Apache Cassandra project"](https://code.google.com/p/cassandra-rpm/). *code.google.com*. Menlo Park, CA, USA: [Google Project Hosting](./Google_Code#Project_hosting). Retrieved June 17, 2014.
- Roth, Gregor (October 14, 2012). ["Cassandra by example - the path of read and write requests"](https://de.slideshare.net/grro/cassandra-by-example-the-path-of-read-and-write-requests). *slideshare.net*. Retrieved June 17, 2014.
- Mansoor, Umer (November 4, 2012). ["A collection of Cassandra tutorials"](http://10kloc.wordpress.com/category/cassandra-2/). Retrieved February 8, 2015.
- Bushik, Sergey (October 22, 2012). ["A vendor-independent comparison of NoSQL databases: Cassandra, HBase, MongoDB, Riak"](https://web.archive.org/web/20140528110238/http://www.networkworld.com/news/tech/2012/102212-nosql-263595.html). *[NetworkWorld](./Network_World)*. Framingham, MA, USA and Staines, Middlesex, UK: [IDG](./International_Data_Group). Archived from [the original](http://www.networkworld.com/news/tech/2012/102212-nosql-263595.html) on May 28, 2014. Retrieved June 17, 2014.
- ["Apache Cassandra System Properties"](https://db-engines.com/en/system/Apache+Cassandra). *DB-Engines*. Retrieved May 28, 2025.

 
| vteThe Apache Software Foundation |
| --- |
| Top-levelprojects | AccumuloActiveMQAiravataAirflowAlluraAmbariAntAriesArrowApache HTTP ServerAPRAvroAxisAxis2BeamBloodhoundBrooklynCalciteCamelCarbonDataCassandraCayenneCloudStackCordovaCouchDBcTAKESCXFDerbyDirectoryDrillDruidEmpire-dbFelixFlexFlinkFlumeFreeMarkerGeronimoGroovyGuacamoleGumpHadoopHBaseHelixHiveIcebergIgniteImpalaJackrabbitJamesJenaJMeterKafkaKuduKylinLuceneMahoutMavenMINAmod_perlMyFacesMynewtNiFiNetBeansNutchNuttXOFBizOozieOpenEJBOpenJPAOpenNLPOрenOfficeORCPDFBoxParquetPhoenixPOIPigPinotPivotQpidRollerRocketMQSamzaShiroSINGASlingSolrSparkStormSpamAssassinStruts1SubversionSupersetSystemDSTapestryThriftTikaTinkerPopTomcatTrafodionTraffic ServerUIMAVelocityWicketXalanXercesXMLBeansYetusZooKeeper |
| Commons | BCELBSFDaemonJellyLogging |
| Incubator | Taverna |
| Other projects | BatikFOPIvyLog4j |
| Attic | ApexAxKitBeehiveiBATISClickCocoonContinuumDeltacloudEtchGiraphHamaHarmonyJakartaMarmottaMXNetODERiverShaleSlideSqoopStanbolTuscanyWaveXML |
| Licenses | Apache License |
| Category |

 
| vteMeta Platforms |
| --- |
| Products,services | FacebookFeaturesBluetooth BeaconDatingFeedEdgeRankReelsGamingGraph SearchInstant ArticlesLike buttonLiveLookalike audienceOnion addressPlatformConnectSafety CheckStoriesWatchlist of original programsZeroInstagramHyperlapseIGTVThreadsHardwarePortalMeta QuestQuest 1Quest 2Quest 3ProTouchRay-Ban MetaOtherExpress Wi-FiFree BasicsMessengerKidsRoomsMapillaryMeta AIMeta Horizon OSMeta Superintelligence LabsMoltbookSupernaturalWhatsAppWorkplaceFormerAtlas SolutionsCreditsFriendFeedGiphyFacebook BeaconFacebook HomeHTC FirstMOculus GoOculus RiftCV1SOnavoPaperSlingshottbhWirehog | Facebook | FeaturesBluetooth BeaconDatingFeedEdgeRankReelsGamingGraph SearchInstant ArticlesLike buttonLiveLookalike audienceOnion addressPlatformConnectSafety CheckStoriesWatchlist of original programsZero | Instagram | HyperlapseIGTVThreads | Hardware | PortalMeta QuestQuest 1Quest 2Quest 3ProTouchRay-Ban Meta | Other | Express Wi-FiFree BasicsMessengerKidsRoomsMapillaryMeta AIMeta Horizon OSMeta Superintelligence LabsMoltbookSupernaturalWhatsAppWorkplace | Former | Atlas SolutionsCreditsFriendFeedGiphyFacebook BeaconFacebook HomeHTC FirstMOculus GoOculus RiftCV1SOnavoPaperSlingshottbhWirehog |
| Facebook | FeaturesBluetooth BeaconDatingFeedEdgeRankReelsGamingGraph SearchInstant ArticlesLike buttonLiveLookalike audienceOnion addressPlatformConnectSafety CheckStoriesWatchlist of original programsZero |
| Instagram | HyperlapseIGTVThreads |
| Hardware | PortalMeta QuestQuest 1Quest 2Quest 3ProTouchRay-Ban Meta |
| Other | Express Wi-FiFree BasicsMessengerKidsRoomsMapillaryMeta AIMeta Horizon OSMeta Superintelligence LabsMoltbookSupernaturalWhatsAppWorkplace |
| Former | Atlas SolutionsCreditsFriendFeedGiphyFacebook BeaconFacebook HomeHTC FirstMOculus GoOculus RiftCV1SOnavoPaperSlingshottbhWirehog |
| People | FoundersMark Zuckerberg(28% equity)Dustin Moskovitz(7%)Eduardo Saverin(5%, formerly)Chris Hughes(1%, formerly)Andrew McCollumBoardCurrentMark ZuckerbergMarc AndreessenJohn D. ArnoldPatrick CollisonJohn ElkannDrew HoustonNancy KilleferRobert M. KimmittDina PowellHock TanDana WhiteTony XuFormerSheryl SandbergPeter ThielExecutiveofficersCurrentMark Zuckerberg(Chairman and CEO)Javier Olivan(COO)Andrew Bosworth(CTO)Chris Cox(CPO)Joel Kaplan(Chief Global Affairs Officer)Jennifer Newstead(Chief Legal Officer)Alexandr Wang(Chief AI Officer)David Wehner(Chief Strategy Officer)FormerSean Parker(4%, formerly)Owen Van NattaGideon YuAdam D'AngeloNick CleggChris KellyBret TaylorSheryl SandbergMike SchroepferDavid EbersmanMarne LevineAlex StamosOversightBoardMembersCatalina Botero Marino, Co-Chair (2020–)Jamal Greene, Co-Chair (2020–)Michael W. McConnell, Co-Chair (2020–)Helle Thorning-Schmidt, Co-Chair (2020–)Afia Asantewaa Asare-Kyei(2020–)Evelyn Aswad(2020–)Endy Bayuni(2020–)Katherine Chen(2020–)Nighat Dad(2020–)Tawakkol Karman(2020–)Maina Kiai(2020–)Sudhir Krishnaswamy(2020–)Ronaldo Lemos(2020–)Julie Owono(2020–)Emi Palmor(2020–)Alan Rusbridger(2020–)András Sajó(2020–)John Samples(2020–)Nicolas Suzor(2020–)Suzanne Nossel(2021–)Khaled Mansour (2022–)Pamela San Martin (2022–)Paolo Carozza (2022–)Kenji Yoshino(2023–)Board ofTrusteesStephen Neal, Chair (2021–)Kristina Arriaga (2020–)Cherine Chalaby (2020–)Wanda Felton (2020–)Kate O'Regan(2020–)Robert Post(2020–)FormermembersPamela S. Karlan(Board Member, 2020–2021)Paul G. Haaga Jr.(Board of Trustees Chair, 2020–2021)NotableemployeesCurrentLars Rasmussen(Graph Search director)Naomi Gleit(head of product)Nicola Mendelsohn(head of Global Business Group)Adam Mosseri(head of Instagram)Thomas Reardon(Reality Labsdirector)FormerBlake Ross(Director of Product)Ted Ullyot(VP, General Counsel, and Secretary)Hugo Barra(VP ofReality Labs)John Carmack(CTO ofReality Labs)Matt CohlerCharlie CheeverRandi ZuckerbergYishan WongGeorge HotzJoe LockhartAndrei Alexandrescu(research scientist)Chamath Palihapitiya(VP of User Growth)Elliot Schrage(VP of Global Communications, Marketing and Public Policy)Frances Haugen(Product Manager of Civic Integrity Team)Sarah Wynn-Williams(Director of Public Policy) | Founders | Mark Zuckerberg(28% equity)Dustin Moskovitz(7%)Eduardo Saverin(5%, formerly)Chris Hughes(1%, formerly)Andrew McCollum | Board | CurrentMark ZuckerbergMarc AndreessenJohn D. ArnoldPatrick CollisonJohn ElkannDrew HoustonNancy KilleferRobert M. KimmittDina PowellHock TanDana WhiteTony XuFormerSheryl SandbergPeter Thiel | Current | Mark ZuckerbergMarc AndreessenJohn D. ArnoldPatrick CollisonJohn ElkannDrew HoustonNancy KilleferRobert M. KimmittDina PowellHock TanDana WhiteTony Xu | Former | Sheryl SandbergPeter Thiel | Executiveofficers | CurrentMark Zuckerberg(Chairman and CEO)Javier Olivan(COO)Andrew Bosworth(CTO)Chris Cox(CPO)Joel Kaplan(Chief Global Affairs Officer)Jennifer Newstead(Chief Legal Officer)Alexandr Wang(Chief AI Officer)David Wehner(Chief Strategy Officer)FormerSean Parker(4%, formerly)Owen Van NattaGideon YuAdam D'AngeloNick CleggChris KellyBret TaylorSheryl SandbergMike SchroepferDavid EbersmanMarne LevineAlex Stamos | Current | Mark Zuckerberg(Chairman and CEO)Javier Olivan(COO)Andrew Bosworth(CTO)Chris Cox(CPO)Joel Kaplan(Chief Global Affairs Officer)Jennifer Newstead(Chief Legal Officer)Alexandr Wang(Chief AI Officer)David Wehner(Chief Strategy Officer) | Former | Sean Parker(4%, formerly)Owen Van NattaGideon YuAdam D'AngeloNick CleggChris KellyBret TaylorSheryl SandbergMike SchroepferDavid EbersmanMarne LevineAlex Stamos | OversightBoard | MembersCatalina Botero Marino, Co-Chair (2020–)Jamal Greene, Co-Chair (2020–)Michael W. McConnell, Co-Chair (2020–)Helle Thorning-Schmidt, Co-Chair (2020–)Afia Asantewaa Asare-Kyei(2020–)Evelyn Aswad(2020–)Endy Bayuni(2020–)Katherine Chen(2020–)Nighat Dad(2020–)Tawakkol Karman(2020–)Maina Kiai(2020–)Sudhir Krishnaswamy(2020–)Ronaldo Lemos(2020–)Julie Owono(2020–)Emi Palmor(2020–)Alan Rusbridger(2020–)András Sajó(2020–)John Samples(2020–)Nicolas Suzor(2020–)Suzanne Nossel(2021–)Khaled Mansour (2022–)Pamela San Martin (2022–)Paolo Carozza (2022–)Kenji Yoshino(2023–)Board ofTrusteesStephen Neal, Chair (2021–)Kristina Arriaga (2020–)Cherine Chalaby (2020–)Wanda Felton (2020–)Kate O'Regan(2020–)Robert Post(2020–)FormermembersPamela S. Karlan(Board Member, 2020–2021)Paul G. Haaga Jr.(Board of Trustees Chair, 2020–2021) | Members | Catalina Botero Marino, Co-Chair (2020–)Jamal Greene, Co-Chair (2020–)Michael W. McConnell, Co-Chair (2020–)Helle Thorning-Schmidt, Co-Chair (2020–)Afia Asantewaa Asare-Kyei(2020–)Evelyn Aswad(2020–)Endy Bayuni(2020–)Katherine Chen(2020–)Nighat Dad(2020–)Tawakkol Karman(2020–)Maina Kiai(2020–)Sudhir Krishnaswamy(2020–)Ronaldo Lemos(2020–)Julie Owono(2020–)Emi Palmor(2020–)Alan Rusbridger(2020–)András Sajó(2020–)John Samples(2020–)Nicolas Suzor(2020–)Suzanne Nossel(2021–)Khaled Mansour (2022–)Pamela San Martin (2022–)Paolo Carozza (2022–)Kenji Yoshino(2023–) | Board ofTrustees | Stephen Neal, Chair (2021–)Kristina Arriaga (2020–)Cherine Chalaby (2020–)Wanda Felton (2020–)Kate O'Regan(2020–)Robert Post(2020–) | Formermembers | Pamela S. Karlan(Board Member, 2020–2021)Paul G. Haaga Jr.(Board of Trustees Chair, 2020–2021) | Notableemployees | CurrentLars Rasmussen(Graph Search director)Naomi Gleit(head of product)Nicola Mendelsohn(head of Global Business Group)Adam Mosseri(head of Instagram)Thomas Reardon(Reality Labsdirector)FormerBlake Ross(Director of Product)Ted Ullyot(VP, General Counsel, and Secretary)Hugo Barra(VP ofReality Labs)John Carmack(CTO ofReality Labs)Matt CohlerCharlie CheeverRandi ZuckerbergYishan WongGeorge HotzJoe LockhartAndrei Alexandrescu(research scientist)Chamath Palihapitiya(VP of User Growth)Elliot Schrage(VP of Global Communications, Marketing and Public Policy)Frances Haugen(Product Manager of Civic Integrity Team)Sarah Wynn-Williams(Director of Public Policy) | Current | Lars Rasmussen(Graph Search director)Naomi Gleit(head of product)Nicola Mendelsohn(head of Global Business Group)Adam Mosseri(head of Instagram)Thomas Reardon(Reality Labsdirector) | Former | Blake Ross(Director of Product)Ted Ullyot(VP, General Counsel, and Secretary)Hugo Barra(VP ofReality Labs)John Carmack(CTO ofReality Labs)Matt CohlerCharlie CheeverRandi ZuckerbergYishan WongGeorge HotzJoe LockhartAndrei Alexandrescu(research scientist)Chamath Palihapitiya(VP of User Growth)Elliot Schrage(VP of Global Communications, Marketing and Public Policy)Frances Haugen(Product Manager of Civic Integrity Team)Sarah Wynn-Williams(Director of Public Policy) |
| Founders | Mark Zuckerberg(28% equity)Dustin Moskovitz(7%)Eduardo Saverin(5%, formerly)Chris Hughes(1%, formerly)Andrew McCollum |
| Board | CurrentMark ZuckerbergMarc AndreessenJohn D. ArnoldPatrick CollisonJohn ElkannDrew HoustonNancy KilleferRobert M. KimmittDina PowellHock TanDana WhiteTony XuFormerSheryl SandbergPeter Thiel | Current | Mark ZuckerbergMarc AndreessenJohn D. ArnoldPatrick CollisonJohn ElkannDrew HoustonNancy KilleferRobert M. KimmittDina PowellHock TanDana WhiteTony Xu | Former | Sheryl SandbergPeter Thiel |
| Current | Mark ZuckerbergMarc AndreessenJohn D. ArnoldPatrick CollisonJohn ElkannDrew HoustonNancy KilleferRobert M. KimmittDina PowellHock TanDana WhiteTony Xu |
| Former | Sheryl SandbergPeter Thiel |
| Executiveofficers | CurrentMark Zuckerberg(Chairman and CEO)Javier Olivan(COO)Andrew Bosworth(CTO)Chris Cox(CPO)Joel Kaplan(Chief Global Affairs Officer)Jennifer Newstead(Chief Legal Officer)Alexandr Wang(Chief AI Officer)David Wehner(Chief Strategy Officer)FormerSean Parker(4%, formerly)Owen Van NattaGideon YuAdam D'AngeloNick CleggChris KellyBret TaylorSheryl SandbergMike SchroepferDavid EbersmanMarne LevineAlex Stamos | Current | Mark Zuckerberg(Chairman and CEO)Javier Olivan(COO)Andrew Bosworth(CTO)Chris Cox(CPO)Joel Kaplan(Chief Global Affairs Officer)Jennifer Newstead(Chief Legal Officer)Alexandr Wang(Chief AI Officer)David Wehner(Chief Strategy Officer) | Former | Sean Parker(4%, formerly)Owen Van NattaGideon YuAdam D'AngeloNick CleggChris KellyBret TaylorSheryl SandbergMike SchroepferDavid EbersmanMarne LevineAlex Stamos |
| Current | Mark Zuckerberg(Chairman and CEO)Javier Olivan(COO)Andrew Bosworth(CTO)Chris Cox(CPO)Joel Kaplan(Chief Global Affairs Officer)Jennifer Newstead(Chief Legal Officer)Alexandr Wang(Chief AI Officer)David Wehner(Chief Strategy Officer) |
| Former | Sean Parker(4%, formerly)Owen Van NattaGideon YuAdam D'AngeloNick CleggChris KellyBret TaylorSheryl SandbergMike SchroepferDavid EbersmanMarne LevineAlex Stamos |
| OversightBoard | MembersCatalina Botero Marino, Co-Chair (2020–)Jamal Greene, Co-Chair (2020–)Michael W. McConnell, Co-Chair (2020–)Helle Thorning-Schmidt, Co-Chair (2020–)Afia Asantewaa Asare-Kyei(2020–)Evelyn Aswad(2020–)Endy Bayuni(2020–)Katherine Chen(2020–)Nighat Dad(2020–)Tawakkol Karman(2020–)Maina Kiai(2020–)Sudhir Krishnaswamy(2020–)Ronaldo Lemos(2020–)Julie Owono(2020–)Emi Palmor(2020–)Alan Rusbridger(2020–)András Sajó(2020–)John Samples(2020–)Nicolas Suzor(2020–)Suzanne Nossel(2021–)Khaled Mansour (2022–)Pamela San Martin (2022–)Paolo Carozza (2022–)Kenji Yoshino(2023–)Board ofTrusteesStephen Neal, Chair (2021–)Kristina Arriaga (2020–)Cherine Chalaby (2020–)Wanda Felton (2020–)Kate O'Regan(2020–)Robert Post(2020–)FormermembersPamela S. Karlan(Board Member, 2020–2021)Paul G. Haaga Jr.(Board of Trustees Chair, 2020–2021) | Members | Catalina Botero Marino, Co-Chair (2020–)Jamal Greene, Co-Chair (2020–)Michael W. McConnell, Co-Chair (2020–)Helle Thorning-Schmidt, Co-Chair (2020–)Afia Asantewaa Asare-Kyei(2020–)Evelyn Aswad(2020–)Endy Bayuni(2020–)Katherine Chen(2020–)Nighat Dad(2020–)Tawakkol Karman(2020–)Maina Kiai(2020–)Sudhir Krishnaswamy(2020–)Ronaldo Lemos(2020–)Julie Owono(2020–)Emi Palmor(2020–)Alan Rusbridger(2020–)András Sajó(2020–)John Samples(2020–)Nicolas Suzor(2020–)Suzanne Nossel(2021–)Khaled Mansour (2022–)Pamela San Martin (2022–)Paolo Carozza (2022–)Kenji Yoshino(2023–) | Board ofTrustees | Stephen Neal, Chair (2021–)Kristina Arriaga (2020–)Cherine Chalaby (2020–)Wanda Felton (2020–)Kate O'Regan(2020–)Robert Post(2020–) | Formermembers | Pamela S. Karlan(Board Member, 2020–2021)Paul G. Haaga Jr.(Board of Trustees Chair, 2020–2021) |
| Members | Catalina Botero Marino, Co-Chair (2020–)Jamal Greene, Co-Chair (2020–)Michael W. McConnell, Co-Chair (2020–)Helle Thorning-Schmidt, Co-Chair (2020–)Afia Asantewaa Asare-Kyei(2020–)Evelyn Aswad(2020–)Endy Bayuni(2020–)Katherine Chen(2020–)Nighat Dad(2020–)Tawakkol Karman(2020–)Maina Kiai(2020–)Sudhir Krishnaswamy(2020–)Ronaldo Lemos(2020–)Julie Owono(2020–)Emi Palmor(2020–)Alan Rusbridger(2020–)András Sajó(2020–)John Samples(2020–)Nicolas Suzor(2020–)Suzanne Nossel(2021–)Khaled Mansour (2022–)Pamela San Martin (2022–)Paolo Carozza (2022–)Kenji Yoshino(2023–) |
| Board ofTrustees | Stephen Neal, Chair (2021–)Kristina Arriaga (2020–)Cherine Chalaby (2020–)Wanda Felton (2020–)Kate O'Regan(2020–)Robert Post(2020–) |
| Formermembers | Pamela S. Karlan(Board Member, 2020–2021)Paul G. Haaga Jr.(Board of Trustees Chair, 2020–2021) |
| Notableemployees | CurrentLars Rasmussen(Graph Search director)Naomi Gleit(head of product)Nicola Mendelsohn(head of Global Business Group)Adam Mosseri(head of Instagram)Thomas Reardon(Reality Labsdirector)FormerBlake Ross(Director of Product)Ted Ullyot(VP, General Counsel, and Secretary)Hugo Barra(VP ofReality Labs)John Carmack(CTO ofReality Labs)Matt CohlerCharlie CheeverRandi ZuckerbergYishan WongGeorge HotzJoe LockhartAndrei Alexandrescu(research scientist)Chamath Palihapitiya(VP of User Growth)Elliot Schrage(VP of Global Communications, Marketing and Public Policy)Frances Haugen(Product Manager of Civic Integrity Team)Sarah Wynn-Williams(Director of Public Policy) | Current | Lars Rasmussen(Graph Search director)Naomi Gleit(head of product)Nicola Mendelsohn(head of Global Business Group)Adam Mosseri(head of Instagram)Thomas Reardon(Reality Labsdirector) | Former | Blake Ross(Director of Product)Ted Ullyot(VP, General Counsel, and Secretary)Hugo Barra(VP ofReality Labs)John Carmack(CTO ofReality Labs)Matt CohlerCharlie CheeverRandi ZuckerbergYishan WongGeorge HotzJoe LockhartAndrei Alexandrescu(research scientist)Chamath Palihapitiya(VP of User Growth)Elliot Schrage(VP of Global Communications, Marketing and Public Policy)Frances Haugen(Product Manager of Civic Integrity Team)Sarah Wynn-Williams(Director of Public Policy) |
| Current | Lars Rasmussen(Graph Search director)Naomi Gleit(head of product)Nicola Mendelsohn(head of Global Business Group)Adam Mosseri(head of Instagram)Thomas Reardon(Reality Labsdirector) |
| Former | Blake Ross(Director of Product)Ted Ullyot(VP, General Counsel, and Secretary)Hugo Barra(VP ofReality Labs)John Carmack(CTO ofReality Labs)Matt CohlerCharlie CheeverRandi ZuckerbergYishan WongGeorge HotzJoe LockhartAndrei Alexandrescu(research scientist)Chamath Palihapitiya(VP of User Growth)Elliot Schrage(VP of Global Communications, Marketing and Public Policy)Frances Haugen(Product Manager of Civic Integrity Team)Sarah Wynn-Williams(Director of Public Policy) |
| Opensource | Apache CassandraApache HiveApache ThriftBuckFQLHackHHVMHipHop for PHPInferMyRocksOpen Compute ProjectPhabricatorReactReact NativeRocksDBScribeTelecom Infra ProjectTornado |
| Massmedia | The Facebook EffectThe Accidental BillionairesThe Social NetworkThe Great HackCareless People"Instagram" (Dean song)The Social Reckoning |
| Concepts | InfluencerActivity streamSocial graphFriending and followingRebloggingFan-gatingFacebook diplomacyInstapoetryModel (person)#Instagram modelFilterInstagram face |
| Business | History of FacebookIPOTimeline of Instagram#Graduation2020Timeline of WhatsAppAcquisitionsf8 conferenceCensorshipCriticismCambridge Analytica data scandal2020 ad boycotts2021 company files leakPrivacyContent managementProblematic social media useLitigationYoung v. Facebook, Inc.(2011)Fraley v. Facebook, Inc.(2016)Force v. Facebook, Inc.(2019)Facebook, Inc. v. Duguid(2021)Federal Trade Commission v. Meta Platforms, Inc.(ongoing)Unions |
| Lists | Most-followed Facebook pagesmost-followed Instagram accountsmost-liked Instagram posts |
| Related | Priscilla Chan(wife of Mark Zuckerberg)Chan Zuckerberg InitiativeAquila Internet relay droneWillow VillageWaveGroup Sound2021 Facebook outageInstagram tourism |