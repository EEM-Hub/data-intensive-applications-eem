---
source: https://en.wikipedia.org/wiki/RocksDB
fetched: 2026-06-19
---

Embedded key-value database 
| RocksDB |
| --- |
|  |
| Original author | Dhruba Borthakur |
| Developers | Meta Platforms(was Facebook, Inc.) |
| Release | May2012;14years ago(2012-05) |
|  |
| Stable release | 10.2.1[1]/ 24 April 2025 |
|  |
| Written in | C++ |
| Operating system | Windows,macOS,Linux,FreeBSD,OpenBSD,Solaris,AIX |
| Platform | Cross-platform |
| Type | Embedded database |
| License | Apache 2.0orGPL 2 |
| Website | rocksdb.org |
| Repository | github.com/facebook/rocksdb |

  

**RocksDB** is a high performance[[2]](./RocksDB#cite_note-2)[[3]](./RocksDB#cite_note-3)[[4]](./RocksDB#cite_note-4)[[5]](./RocksDB#cite_note-5)[[6]](./RocksDB#cite_note-6) [embedded database](./Embedded_database) for [key-value](./Key-value_database) data. It is a [fork](./Fork_(software_development)) of Google's [LevelDB](./LevelDB) optimized to exploit [multi-core processors](./Multi-core_processor) (CPUs), and make efficient use of fast storage, such as [solid-state drives](./Solid-state_drive) (SSD), for [input/output](./Input/output) (I/O) [bound](./I/O_bound) workloads. It is based on a [log-structured merge-tree](./Log-structured_merge-tree) (LSM tree) data structure. It is written in [C++](./C++) and provides official [language bindings](./Language_binding) for [C++](./C++), [C](./C_(programming_language)), and [Java](./Java_(programming_language)). Many [third-party language bindings](./RocksDB#Third-party_language_bindings) exist. RocksDB is [free and open-source software](./Free_and_open-source_software), released originally under a [BSD 3-clause](./BSD_licenses) license.[[7]](./RocksDB#cite_note-7)[[8]](./RocksDB#cite_note-8)[[9]](./RocksDB#cite_note-9) However, in July 2017 the project was migrated to a dual license of both [Apache 2.0](./Apache_2.0) and [GPLv2](./GPLv2) license.[[10]](./RocksDB#cite_note-10) This change helped its adoption in Apache Software Foundation's projects after blacklist of the previous BSD+Patents license clause.[[11]](./RocksDB#cite_note-11)[[12]](./RocksDB#cite_note-12)

 

RocksDB is used in production systems at various [web-scale](./Scalability) enterprises[[13]](./RocksDB#cite_note-13) including [Facebook](./Facebook,_Inc.), [Yahoo!](./Yahoo!),[[14]](./RocksDB#cite_note-14) and [LinkedIn](./LinkedIn).[[15]](./RocksDB#cite_note-15)

 

## Features

 

RocksDB, like [LevelDB](./LevelDB), stores keys and values in arbitrary byte arrays, and data is sorted byte-wise by key or by providing a custom comparator.

 

RocksDB provides all of the features of LevelDB, plus:

 
- [Transactions](./Database_transaction)[[16]](./RocksDB#cite_note-16)
- [Backups](./Backup)[[17]](./RocksDB#cite_note-17) and [snapshots](./Snapshot_(computer_storage))[[18]](./RocksDB#cite_note-18)
- [Column families](./Column_family)[[19]](./RocksDB#cite_note-19)
- [Bloom filters](./Bloom_filter)[[20]](./RocksDB#cite_note-20)
- Time to live (TTL) support[[21]](./RocksDB#cite_note-21)
- Universal compaction[[22]](./RocksDB#cite_note-22)
- Merge operators[[23]](./RocksDB#cite_note-23)
- Statistics collection[[24]](./RocksDB#cite_note-24)
- Geospatial indexing[[25]](./RocksDB#cite_note-25)

 

and others.[[26]](./RocksDB#cite_note-26)

 

RocksDB is not an [SQL](./SQL) database (although [MyRocks](./MyRocks) combines RocksDB with [MySQL](./MySQL)). Like other [NoSQL](./NoSQL) and [dbm](./DBM_(computing)) stores, it has no [relational data model](./Relational_model), and it does not support SQL queries. Also, it has no direct support for secondary indexes, however a user may build their own internally using Column Families or externally. Applications use RocksDB as a [library](./Library_(computing)), as it provides no server or [command-line interface](./Command-line_interface).

 

## History

 

RocksDB was created at [Facebook](./Facebook) by Dhruba Borthakur[[27]](./RocksDB#cite_note-27)[[28]](./RocksDB#cite_note-28) in April 2012, as a fork of [LevelDB](./LevelDB) with the initial stated goal of improving performance for server workloads.[[29]](./RocksDB#cite_note-29)[[30]](./RocksDB#cite_note-30)

 

## Integration

 

As an embeddable database, RocksDB can be used as a storage engine within a larger [database](./Database) management system (DBMS). For example, [Rockset](./Rockset?action=edit&redlink=1) uses RocksDB[[31]](./RocksDB#cite_note-31) mostly for analytical data processing.

 

### Alternative backend

 

The following projects have been started to replace or offer alternative storage engines for already-established database systems with RocksDB:

 

#### ArangoDB

 

[ArangoDB](./ArangoDB) has added RocksDB to its previous storage engine ("mmfiles").[[32]](./RocksDB#cite_note-32) RocksDB is be the default storage engine since ArangoDB 3.4.[[33]](./RocksDB#cite_note-33)

 

#### Cassandra

 

The Instagram team at Facebook developed and open-sourced their code, along with benchmarks of their performance results.[[34]](./RocksDB#cite_note-34)

 

#### MariaDB

 

[MariaDB](./MariaDB) can use the MyRocks storage engine (which is forked from RocksDB) since MariaDB 10.2.5 (Alpha status) [[35]](./RocksDB#cite_note-35) and stable since MariaDB 10.2.16 in 2018.[[36]](./RocksDB#cite_note-36)

 

#### MongoDB

 

The MongoRocks project provides a storage module for [MongoDB](./MongoDB) where the storage engine is RocksDB.[[37]](./RocksDB#cite_note-37)[[38]](./RocksDB#cite_note-38)[[39]](./RocksDB#cite_note-39)

 

A related program is Rocks Strata, a tool written in [Go](./Go_(programming_language)), which allows managing incremental backups of MongoDB when RocksDB is used as the storage engine.[[40]](./RocksDB#cite_note-40)

 

#### MySQL

 

The MyRocks project created a new RocksDB-based storage engine for [MySQL](./MySQL).[[41]](./RocksDB#cite_note-41)[[42]](./RocksDB#cite_note-42) In-depth details about MyRocks were presented at Percona Live 2016.[[43]](./RocksDB#cite_note-43)

 

#### Oxigraph

 

[Oxigraph](./Oxigraph?action=edit&redlink=1)[[44]](./RocksDB#cite_note-44) is a [graph database](./Graph_database) implementing the [SPARQL](./SPARQL) standard, based on RocksDB

 

#### UKV

 

The UKV[[45]](./RocksDB#cite_note-ukv-45) project allows users to use RocksDB on par with [LevelDB](./LevelDB) as the underlying [key-value store](./Key–value_database). It represents a shared abstraction for [create, read, update and delete](./Create,_read,_update_and_delete) (CRUD) operations common to every storage engine. It augments it with structured bindings for several high-level languages, including [Python](./Python_(programming_language)), [Java](./Java_(programming_language)), and [Go](./Go_(programming_language)).

 

### Embedded

 

The following database systems and applications have chosen to use RocksDB as their embedded storage engine:

 

#### Ceph's BlueStore

 

The [Ceph's](./Ceph_(software)) BlueStore storage layer uses RocksDB for metadata management in OSD devices.[[46]](./RocksDB#cite_note-46)

 

#### Apache Flink

 

Apache Flink uses RocksDB to store checkpoints.[[47]](./RocksDB#cite_note-47)

 

#### FusionDB

 

FusionDB[[48]](./RocksDB#cite_note-48) uses RocksDB as its storage engine for XML, Key/Value, and JSON.[[49]](./RocksDB#cite_note-49)

 

#### LogDevice LogsDB

 

LogDevice's LogsDB is built atop RocksDB.[[50]](./RocksDB#cite_note-50)

 

#### Kafka Streams

 

Kafka Streams uses RocksDB for its state stores.[[51]](./RocksDB#cite_note-51)

 

#### Manhattan

 

The Manhattan Distributed Key-Value Store has used RocksDB as its primary engine to store Twitter data since 2018.[[52]](./RocksDB#cite_note-52)

 

#### Rockset

 

The [Rockset](./Rockset?action=edit&redlink=1)[[53]](./RocksDB#cite_note-53) service that is used for operational data analytics uses RocksDB as its storage engine.[[54]](./RocksDB#cite_note-54)

 

#### SSDB

 

The ssdb-rocks[[55]](./RocksDB#cite_note-55) project uses RocksDB as the storage engine for the SSDB[[56]](./RocksDB#cite_note-56) NoSQL Database.

 

#### TiDB

 

The TiDB[[57]](./RocksDB#cite_note-57) project uses RocksDB as its storage engine.[[58]](./RocksDB#cite_note-58)

 

#### YugabyteDB

 

The [YugabyteDB](./YugabyteDB) database uses a modified version of RocksDB as part of its DocDB storage engine.[[59]](./RocksDB#cite_note-59)

 

## Third-party language bindings

 

Third-party programming language bindings available for RocksDB include:

   All links in alphabetic order please  
- [C](./C_(programming_language))[[45]](./RocksDB#cite_note-ukv-45)
- [C#](./C_Sharp_(programming_language))[[60]](./RocksDB#cite_note-60)
- [Chicken Scheme](./Chicken_(Scheme_implementation))[[61]](./RocksDB#cite_note-61)
- [D](./D_(programming_language))[[62]](./RocksDB#cite_note-62)
- [Elixir](./Elixir_(programming_language))[[63]](./RocksDB#cite_note-63)
- [Erlang](./Erlang_(programming_language))[[64]](./RocksDB#cite_note-64)[[65]](./RocksDB#cite_note-65)
- [Go](./Go_(programming_language))[[45]](./RocksDB#cite_note-ukv-45)[[66]](./RocksDB#cite_note-66)
- [Haskell](./Haskell)[[67]](./RocksDB#cite_note-67)
- [Java](./Java_(programming_language))[[45]](./RocksDB#cite_note-ukv-45)[[68]](./RocksDB#cite_note-68)[[69]](./RocksDB#cite_note-69)
- [Kotlin](./Kotlin_(programming_language))[[70]](./RocksDB#cite_note-70)
- [Node.js](./Node.js)[[71]](./RocksDB#cite_note-71)
- [Nim](./Nim_(programming_language))[[72]](./RocksDB#cite_note-72)
- [Objective-C](./Objective-C), and [Swift](./Swift_(programming_language))[[73]](./RocksDB#cite_note-73)
- [OCaml](./OCaml)[[74]](./RocksDB#cite_note-74)[[75]](./RocksDB#cite_note-75)
- [Perl](./Perl)[[76]](./RocksDB#cite_note-76)
- [PHP](./PHP)[[77]](./RocksDB#cite_note-77)
- [Prolog](./Prolog)[[78]](./RocksDB#cite_note-78)
- [Python](./Python_(programming_language))[[45]](./RocksDB#cite_note-ukv-45)[[79]](./RocksDB#cite_note-79)
- [Ruby](./Ruby_(programming_language))[[80]](./RocksDB#cite_note-80)
- [Rust](./Rust_(programming_language))[[81]](./RocksDB#cite_note-81)

  

## See also

 
- [Ordered Key-Value Store](./Ordered_Key-Value_Store)

 

## References

  
1. [↑](./RocksDB#cite_ref-wikidata-31c46370b3627e9f08e53054d7870df42190b806-v20_1-0) . 24 April 2025 [https://github.com/facebook/rocksdb/releases/tag/v10.2.1](https://github.com/facebook/rocksdb/releases/tag/v10.2.1). Retrieved 24 April 2025. `{{cite web}}`: Missing or empty `|title=` ([help](./Help:CS1_errors#citation_missing_title))
2. [↑](./RocksDB#cite_ref-2) ["Performance Benchmarks"](https://github.com/facebook/rocksdb/wiki/Performance-Benchmarks). *[GitHub](./GitHub)*. Retrieved November 29, 2015.
3. [↑](./RocksDB#cite_ref-3) ["Benchmarking the leveldb family"](http://smalldatum.blogspot.com/2014/07/benchmarking-leveldb-family.html). 7 July 2014. Retrieved March 10, 2016.
4. [↑](./RocksDB#cite_ref-4) ["Comparing LevelDB and RocksDB, take 2"](http://smalldatum.blogspot.com/2015/04/comparing-leveldb-and-rocksdb-take-2.html). 27 April 2015. Retrieved March 10, 2016.
5. [↑](./RocksDB#cite_ref-5) ["Benchmarking LevelDB vs. RocksDB vs. HyperLevelDB vs. LMDB Performance for InfluxDB"](https://influxdata.com/blog/benchmarking-leveldb-vs-rocksdb-vs-hyperleveldb-vs-lmdb-performance-for-influxdb/). 20 June 2014. Retrieved March 10, 2016.
6. [↑](./RocksDB#cite_ref-6) Golan-Gueta, Guy; Bortnikov, Edward; Hillel, Eschar; [Keidar, Idit](./Idit_Keidar) (April 21, 2015). "Scaling concurrent log-structured data stores". *Proceedings of the Tenth European Conference on Computer Systems*. pp. 1–14. [doi](./Doi_(identifier)):[10.1145/2741948.2741973](https://doi.org/10.1145%2F2741948.2741973). [ISBN](./ISBN_(identifier)) [9781450332385](./Special:BookSources/9781450332385). [S2CID](./S2CID_(identifier)) [5849146](https://api.semanticscholar.org/CorpusID:5849146).
7. [↑](./RocksDB#cite_ref-7) ["Facebook's latest open source effort: a flash-powered database called RocksDB"](https://web.archive.org/web/20200224065917/https://gigaom.com/2013/11/21/facebooks-latest-open-source-effort-a-flash-powered-database-called-rocksdb/). 21 November 2013. Archived from [the original](https://gigaom.com/2013/11/21/facebooks-latest-open-source-effort-a-flash-powered-database-called-rocksdb/) on 24 February 2020. Retrieved March 10, 2016.
8. [↑](./RocksDB#cite_ref-8) ["Under the Hood: Building and open-sourcing RocksDB"](https://www.facebook.com/notes/facebook-engineering/under-the-hood-building-and-open-sourcing-rocksdb/10151822347683920/). *[Facebook](./Facebook)*. Retrieved March 10, 2016.
9. [↑](./RocksDB#cite_ref-9) ["RocksDB - Facebook's Database Now Open Source"](http://www.i-programmer.info/news/84-database/6624-rocksdb-facebooks-database-now-open-source.html). Retrieved March 10, 2016.
10. [↑](./RocksDB#cite_ref-10) ["GitHub pull request"](https://github.com/facebook/rocksdb/tree/3c327ac2d0fd50bbd82fe1f1af5de909dad769e6/env). *[GitHub](./GitHub)*. Retrieved July 20, 2017.
11. [↑](./RocksDB#cite_ref-11) ["Apache says 'no' to Facebook code libraries"](https://www.theregister.co.uk/2017/07/17/apache_says_no_to_facebook_code_libraries/). *[The Register](./The_Register)*. Retrieved July 20, 2017.
12. [↑](./RocksDB#cite_ref-12) ["GitHub issue"](https://github.com/facebook/rocksdb/issues/2605). *[GitHub](./GitHub)*. Retrieved July 20, 2017.
13. [↑](./RocksDB#cite_ref-13) ["Users.md"](https://github.com/facebook/rocksdb/blob/master/USERS.md). *[GitHub](./GitHub)*. Retrieved December 1, 2015.
14. [↑](./RocksDB#cite_ref-14) ["RocksDB on Steroids"](http://www.i-programmer.info/news/84-database/8542-rocksdb-on-steroids.html). Retrieved March 10, 2016.
15. [↑](./RocksDB#cite_ref-15) ["Benchmarking Apache Samza: 1.2 million messages per second on a single node"](https://engineering.linkedin.com/performance/benchmarking-apache-samza-12-million-messages-second-single-node). Retrieved March 10, 2016.
16. [↑](./RocksDB#cite_ref-16) ["RocksDB transactions"](https://github.com/facebook/rocksdb/wiki/Transactions). *GitHub*. Retrieved 2016-04-04.
17. [↑](./RocksDB#cite_ref-17) ["How to backup RocksDB?"](https://github.com/facebook/rocksdb/wiki/How-to-backup-RocksDB). *[GitHub](./GitHub)*. Retrieved 2017-07-19.
18. [↑](./RocksDB#cite_ref-18) ["Checkpoints"](https://github.com/facebook/rocksdb/wiki/Checkpoints). *[GitHub](./GitHub)*. Retrieved 2017-07-19.
19. [↑](./RocksDB#cite_ref-19) ["Column families in RocksDB"](https://github.com/facebook/rocksdb/wiki/Column-Families). *GitHub*. Retrieved 2016-04-04.
20. [↑](./RocksDB#cite_ref-20) ["RocksDB bloom filters"](https://github.com/facebook/rocksdb/wiki/RocksDB-Bloom-Filter). *GitHub*. Retrieved 2016-04-04.
21. [↑](./RocksDB#cite_ref-21) ["RocksDB TTL support"](https://github.com/facebook/rocksdb/wiki/Time-to-Live). *GitHub*. Retrieved 2016-04-04.
22. [↑](./RocksDB#cite_ref-22) ["Universal compaction"](https://github.com/facebook/rocksdb/wiki/Universal-Compaction). *GitHub*. Retrieved 2016-04-04.
23. [↑](./RocksDB#cite_ref-23) ["RocksDB merge operator"](https://github.com/facebook/rocksdb/wiki/Merge-Operator-Implementation). *GitHub*. Retrieved 2016-04-04.
24. [↑](./RocksDB#cite_ref-24) ["RocksDB perf context and IO stats context"](https://github.com/facebook/rocksdb/wiki/Perf-Context-and-IO-Stats-Context). *GitHub*. Retrieved 2016-04-04.
25. [↑](./RocksDB#cite_ref-25) ["Spatial indexing in RocksDB"](https://rocksdb.org/blog/2015/07/17/spatial-indexing-in-rocksdb.html). *rocksdb.org*. Retrieved 2018-07-19.
26. [↑](./RocksDB#cite_ref-26) ["Features Not in LevelDB"](https://github.com/facebook/rocksdb/wiki/Features-Not-in-LevelDB). *GitHub*.
27. [↑](./RocksDB#cite_ref-27) ["First commit where RocksDB diverges from LevelDB"](https://github.com/facebook/rocksdb/commit/cc6c32535aec596036c56fe742a39182539f76fa). *[GitHub](./GitHub)*. May 10, 2012. Retrieved March 15, 2016.
28. [↑](./RocksDB#cite_ref-28) ["Rocksdb readme file"](https://github.com/facebook/rocksdb/commit/6eb5ed9a4922ec2d121768adfa3ab3b6ead5d627). *[GitHub](./GitHub)*. Nov 30, 2012. Retrieved March 15, 2016.
29. [↑](./RocksDB#cite_ref-29) ["The History of RocksDB"](http://rocksdb.blogspot.com/2013/11/the-history-of-rocksdb.html). November 24, 2013. Retrieved March 10, 2016.
30. [↑](./RocksDB#cite_ref-30) Borthakur, Dhruba (November 22, 2013). ["RocksDB: A High Performance Embedded Key-Value Store for Flash Storage - Data@Scale"](https://www.youtube.com/watch?v=V_C-T5S-w8g). *[YouTube](./YouTube)*. Retrieved March 10, 2016. ... The story of why we decided to do RocksDB ...
31. [↑](./RocksDB#cite_ref-31) Dhoot, Sandeep (2019-06-27). ["How We Use RocksDB at Rockset"](https://rockset.com/blog/how-we-use-rocksdb-at-rockset/). *rockset.com*. Retrieved 2023-03-01.
32. [↑](./RocksDB#cite_ref-32) ["Comparing new RocksDB and MMFiles storage engines"](https://arangodb.com/community-server/rocksdb-storage-engine/). *ArangoDB*.
33. [↑](./RocksDB#cite_ref-33) ["RC1 ArangoDB 3.4 - Whats new?"](https://www.arangodb.com/2018/09/rc1-arangodb-3-4-whats-new/). 6 September 2018.
34. [↑](./RocksDB#cite_ref-34) ["Open-sourcing a 10x reduction in Apache Cassandra tail latency"](https://instagram-engineering.com/open-sourcing-a-10x-reduction-in-apache-cassandra-tail-latency-d64f86b43589). 5 March 2018.
35. [↑](./RocksDB#cite_ref-35) ["MyRocks"](https://mariadb.com/kb/en/library/myrocks/). *MariaDB KnowledgeBase*. Retrieved 2019-04-28.
36. [↑](./RocksDB#cite_ref-36) ["MariaDB 10.2.16 Release Notes"](https://mariadb.com/kb/en/mariadb-10216-release-notes/). *MariaDB KnowledgeBase*.
37. [↑](./RocksDB#cite_ref-37) ["mongodb-partners/mongo-rocks"](https://github.com/mongodb-partners/mongo-rocks). *[GitHub](./GitHub)*. 29 October 2021.
38. [↑](./RocksDB#cite_ref-38) ["Integrating RocksDB with MongoDB"](https://rocksdb.org/blog/2015/04/22/integrating-rocksdb-with-mongodb-2.html). Retrieved July 19, 2018.
39. [↑](./RocksDB#cite_ref-39) ["MongoDB + RocksDB at Parse"](http://blog.parse.com/announcements/mongodb-rocksdb-parse/). Retrieved December 1, 2015.
40. [↑](./RocksDB#cite_ref-40) ["facebookgo/rocks-strata"](https://github.com/facebookgo/rocks-strata). *[GitHub](./GitHub)*. 31 October 2021.
41. [↑](./RocksDB#cite_ref-41) ["facebook/mysql-5.6"](https://github.com/facebook/mysql-5.6). *[GitHub](./GitHub)*. 2 November 2021.
42. [↑](./RocksDB#cite_ref-42) ["MyRocks: MySQL on RocksDB"](https://www.percona.com/live/europe-amsterdam-2015/sites/default/files/slides/MyRocksAtFacebook_201509.pdf) (PDF). Retrieved November 29, 2015.
43. [↑](./RocksDB#cite_ref-43) ["MyRocks Deep Dive"](https://www.slideshare.net/matsunobu/myrocks-deep-dive/). 19 April 2016. Retrieved May 9, 2016.
44. [↑](./RocksDB#cite_ref-44) Pellissier Tanon, Thomas (July 12, 2024). ["Oxigraph"](https://github.com/oxigraph/oxigraph). [doi](./Doi_(identifier)):[10.5281/zenodo.7408022](https://doi.org/10.5281%2Fzenodo.7408022) – via GitHub.
45. [1](./RocksDB#cite_ref-ukv_45-0) [2](./RocksDB#cite_ref-ukv_45-1) [3](./RocksDB#cite_ref-ukv_45-2) [4](./RocksDB#cite_ref-ukv_45-3) [5](./RocksDB#cite_ref-ukv_45-4) ["unum-cloud/ukv"](https://github.com/unum-cloud/ukv). *[GitHub](./GitHub)*. 28 December 2022.
46. [↑](./RocksDB#cite_ref-46) ["Storage Devices -- Ceph Documentation"](https://web.archive.org/web/20200224065932/https://docs.ceph.com/docs/luminous/rados/configuration/storage-devices/). Archived from [the original](http://docs.ceph.com/docs/luminous/rados/configuration/storage-devices/) on 2020-02-24. Retrieved 2017-11-08.
47. [↑](./RocksDB#cite_ref-47) ["Apache Flink 1.8 Documentation: State Backends"](https://ci.apache.org/projects/flink/flink-docs-stable/ops/state/state_backends.html#the-rocksdbstatebackend). *ci.apache.org*. Retrieved 2019-08-11.
48. [↑](./RocksDB#cite_ref-48) ["FusionDB"](https://fusiondb.com). Evolved Binary.
49. [↑](./RocksDB#cite_ref-49) ["The Design and Implementation of FusionDB"](https://archive.xmlprague.cz/2019/files/xmlprague-2019-proceedings.pdf#page179) (PDF). XML Prague.
50. [↑](./RocksDB#cite_ref-50) ["LogDevice: a distributed data store for logs"](https://code.facebook.com/posts/357056558062811/logdevice-a-distributed-data-store-for-logs/). Mark Marchukov, Facebook. 31 August 2017.
51. [↑](./RocksDB#cite_ref-51) ["Configuring a streams application"](https://kafka.apache.org/33/documentation/streams/developer-guide/config-streams.html#id20). *kafka.apache.org*. Retrieved 2024-03-11.
52. [↑](./RocksDB#cite_ref-52) ["Adopting RocksDB within Manhattan"](https://blog.twitter.com/engineering/en_us/topics/infrastructure/2021/adopting-rocksdb-within-manhattan). *[Twitter](./Twitter)*. 28 December 2022.
53. [↑](./RocksDB#cite_ref-53) ["Rockset: Search and analytics database"](https://rockset.com/). *rockset.com*.
54. [↑](./RocksDB#cite_ref-54) ["How we use RocksDB at Rockset"](https://rockset.com/blog/how-we-use-rocksdb-at-rockset/). *rockset.com*. Retrieved 2019-07-10.
55. [↑](./RocksDB#cite_ref-55) ["ideawu/ssdb-rocks"](https://github.com/ideawu/ssdb-rocks). *[GitHub](./GitHub)*. 21 August 2021.
56. [↑](./RocksDB#cite_ref-56) ["Home"](https://ssdb.io/). *ID-2Sbo*.
57. [↑](./RocksDB#cite_ref-57) ["pingcap/tidb"](https://github.com/pingcap/tidb). *[GitHub](./GitHub)*. 4 November 2021.
58. [↑](./RocksDB#cite_ref-58) ["TiDB Internal (I) - Data Storage"](https://pingcap.com/blog/2017-07-11-tidbinternal1). Shen Li. 11 July 2017.
59. [↑](./RocksDB#cite_ref-59) ["How We Built a High Performance Document Store on RocksDB?"](https://blog.yugabyte.com/how-we-built-a-high-performance-document-store-on-rocksdb/). 20 February 2019.
60. [↑](./RocksDB#cite_ref-60) ["warrenfalk/rocksdb-sharp"](https://github.com/warrenfalk/rocksdb-sharp). *[GitHub](./GitHub)*. 28 September 2021.
61. [↑](./RocksDB#cite_ref-61) ["RocksDB bindings for CHICKEN Scheme 5"](http://wiki.call-cc.org/eggref/5/rocksdb). *wiki.call-cc.org*. Retrieved 2024-07-13.
62. [↑](./RocksDB#cite_ref-62) ["b1naryth1ef/rocksdb"](https://github.com/b1naryth1ef/rocksdb). *[GitHub](./GitHub)*. 22 October 2019.
63. [↑](./RocksDB#cite_ref-63) ["urbint/rox"](https://github.com/urbint/rox). *[GitHub](./GitHub)*. September 2021.
64. [↑](./RocksDB#cite_ref-64) ["leo-project/erocksdb"](https://github.com/leo-project/erocksdb). *[GitHub](./GitHub)*. September 2021.
65. [↑](./RocksDB#cite_ref-65) ["barrel-db / erlang-rocksdb · GitLab"](https://gitlab.com/barrel-db/erlang-rocksdb). *GitLab*.
66. [↑](./RocksDB#cite_ref-66) ["tecbot/gorocksdb"](https://github.com/tecbot/gorocksdb). *[GitHub](./GitHub)*. 29 October 2021.
67. [↑](./RocksDB#cite_ref-67) ["rocksdb-haskell"](https://hackage.haskell.org/package/rocksdb-haskell). *Hackage*.
68. [↑](./RocksDB#cite_ref-68) ["RocksJava"](https://github.com/facebook/rocksdb/wiki/RocksJava-Basics). *[GitHub](./GitHub)*.
69. [↑](./RocksDB#cite_ref-69) ["RocksDB-Android"](https://github.com/marykdb/rocksdb-android). *[GitHub](./GitHub)*.
70. [↑](./RocksDB#cite_ref-70) ["RocksDB Kotlin Multiplatform"](https://github.com/marykdb/rocksdb-multiplatform). *[GitHub](./GitHub)*.
71. [↑](./RocksDB#cite_ref-71) ["rocksdb"](https://npmjs.org/package/rocksdb). 25 March 2022.
72. [↑](./RocksDB#cite_ref-72) ["rocksdb"](https://github.com/status-im/nim-rocksdb). *[GitHub](./GitHub)*.
73. [↑](./RocksDB#cite_ref-73) ["iabudiab/ObjectiveRocks"](https://github.com/iabudiab/ObjectiveRocks). *[GitHub](./GitHub)*. 2 August 2021.
74. [↑](./RocksDB#cite_ref-74) ["OCaml bindings for RocksDB"](https://github.com/ahrefs/ocaml-ahrocksdb). *[GitHub](./GitHub)*. 8 October 2021.
75. [↑](./RocksDB#cite_ref-75) ["An OCaml RocksDb binding using ocaml-ctypes"](https://github.com/domsj/orocksdb). *[GitHub](./GitHub)*. 28 September 2020.
76. [↑](./RocksDB#cite_ref-76) ["RocksDB"](https://metacpan.org/pod/RocksDB). *MetaCPAN*.
77. [↑](./RocksDB#cite_ref-77) ["Photonios/rocksdb-php"](https://github.com/Photonios/rocksdb-php). *[GitHub](./GitHub)*. 11 August 2021.
78. [↑](./RocksDB#cite_ref-78) [""rocksdb" pack for SWI-Prolog"](https://www.swi-prolog.org/pack/list?p=rocksdb). *www.swi-prolog.org*.
79. [↑](./RocksDB#cite_ref-79) ["stephan-hof/pyrocksdb"](https://github.com/stephan-hof/pyrocksdb). *[GitHub](./GitHub)*. 27 October 2021.
80. [↑](./RocksDB#cite_ref-80) ["rocksdb-ruby | RubyGems.org | your community gem host"](https://rubygems.org/gems/rocksdb-ruby). *rubygems.org*.
81. [↑](./RocksDB#cite_ref-81) ["rust-rocksdb/rust-rocksdb"](https://github.com/rust-rocksdb/rust-rocksdb). *[GitHub](./GitHub)*. 11 July 2024.

 

## External links

 
- [Official website](http://rocksdb.org)

 
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