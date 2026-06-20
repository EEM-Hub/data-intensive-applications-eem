---
source: https://en.wikipedia.org/wiki/ScyllaDB
fetched: 2026-06-19
---

Source-available distributed NoSQL wide-column data store 
| ScyllaDB |
| --- |
| Scylla monster, mascot of the Scylla database |
| Developer | ScyllaDB Inc. |
| Release | September22, 2015;10 years ago(2015-09-22) |
|  |
| Stable release | ScyllaDB 2025.1
   / April8, 2025;14 months ago(2025-04-08) |
|  |
| Written in | C++ |
| Operating system | Linux |
| Type | distributeddata store |
| License | ScyllaDB Software License Agreement, previouslyGNU AGPL |
| Website | www.scylladb.com |
| Repository | github.com/scylladb/scylladb |

  

**ScyllaDB** is a [source-available](./Source-available) [distributed](./Distributed_database) [NoSQL](./NoSQL) [wide-column](./Wide-column_store) [data store](./Data_store). It was designed to be compatible with [Apache Cassandra](./Apache_Cassandra) while achieving significantly higher throughputs and lower latencies. It supports the same protocols as Cassandra ([CQL](./Apache_Cassandra#Main_features)) and the same file formats (SSTable), but is a completely rewritten implementation, using the [C++20](./C++20) language replacing Cassandra's Java, and the [Seastar](./Seastar_Project?action=edit&redlink=1)[[1]](./ScyllaDB#cite_note-1) asynchronous programming library replacing classic Linux programming techniques such as threads, shared memory and mapped files. In addition to implementing Cassandra's protocols, ScyllaDB also implements the [Amazon DynamoDB](./Amazon_DynamoDB) API.[[2]](./ScyllaDB#cite_note-2)

 

ScyllaDB uses a [sharded](./Shard_(database_architecture)) design on each node, meaning that each [CPU](./CPU) core handles a different subset of data. Cores do not share data, but rather communicate explicitly when they need to. The ScyllaDB authors claim that this design allows ScyllaDB to achieve much better performance on modern [NUMA](./Non-uniform_memory_access) [SMP](./Symmetric_multiprocessor_system) machines, and to scale very well with the number of cores. They have measured as much as 2 million requests per second on a single machine,[[3]](./ScyllaDB#cite_note-3) and also claim that a ScyllaDB cluster can serve as many requests as a Cassandra cluster 10 times its size – and do so with lower latencies.[[4]](./ScyllaDB#cite_note-4) Independent testing has not always been able to confirm such 10-fold throughput improvements, and sometimes measured smaller speedups, such as 2x.[[5]](./ScyllaDB#cite_note-5) A 2017 benchmark from [Samsung](./Samsung) observed the 10x speedup on high-end machines – the Samsung benchmark reported that ScyllaDB outperformed Cassandra on a cluster of 24-core machines by a margin of 10–37x depending on the [YCSB](./YCSB) workload.[[6]](./ScyllaDB#cite_note-6)

 

ScyllaDB is available on-premises, on major public cloud providers, or as a DBaaS (ScyllaDB Cloud).[[7]](./ScyllaDB#cite_note-7)

 

## History

 

ScyllaDB was started in December 2014 by the [startup](./Startup_company) [Cloudius Systems](./Cloudius_Systems?action=edit&redlink=1) (later renamed ScyllaDB Inc.), previously known for having created [OSv](./OSv). Co-founders were [Avi Kivity](./Avi_Kivity) and Dor Laor. ScyllaDB was released as open source in September 2015,[[8]](./ScyllaDB#cite_note-8) under the [AGPL](./GNU_Affero_General_Public_License) license. In December 2024, ScyllaDB moved to a [source available](./Source_available) license.[[9]](./ScyllaDB#cite_note-9) Its source code and development process is still open to the public on public [GitHub](./GitHub) repositories, but usage on a cluster beyond a certain size requires purchasing a license.  In 2026, ScyllaDB announced  [vector database](./Vector_database) support.[[10]](./ScyllaDB#cite_note-10)[[11]](./ScyllaDB#cite_note-11)

 

## See also

 
- [Avi Kivity](./Avi_Kivity)
- [Glauber Costa](./Glauber_Costa)
- [Kernel-based Virtual Machine (KVM)](./Kernel-based_Virtual_Machine)
- [OSv](./OSv)

 

## References

  
1. [↑](./ScyllaDB#cite_ref-1) ["Seastar - Seastar"](https://seastar.io/). *seastar.io*. Retrieved 2025-02-26.
2. [↑](./ScyllaDB#cite_ref-2) Angell, Julia. ["ScyllaDB Secures $25 Million to Open Source Amazon DynamoDB-compatible API"](https://www.scylladb.com/press-release/scylladb-secures-25-million-open-source-amazon-dynamodb-compatible-api/). *ScyllaDB*. Retrieved 2025-02-26.
3. [↑](./ScyllaDB#cite_ref-3) [ScyllaDB: Cassandra compatibility at 1.8 million requests per node](https://www.socallinuxexpo.org/scale/14x/presentations/scylladb-cassandra-compatibility-18-million-requests-node) by [Don Marti](./Don_Marti) (then a ScyllaDB Inc. employee), presented at the Fourteenth Annual [Southern California Linux Expo](./Southern_California_Linux_Expo), January 24, 2016.
4. [↑](./ScyllaDB#cite_ref-4) Angell, Julia. ["Benchmarks"](https://www.scylladb.com/product/benchmarks/). *ScyllaDB*. Retrieved 2025-02-26.
5. [↑](./ScyllaDB#cite_ref-5) ["ScyllaDB vs Cassandra: towards a new myth?"](https://blog.octo.com/scylladb-vs-cassandra-towards-a-new-myth). *OCTO Talks !* (in French). 2015-12-15. Retrieved 2025-02-26.
6. [↑](./ScyllaDB#cite_ref-6) Rezaei, Arash; Guz, Zvika; Balakrishnan, Vijay (February 2017), [*ScyllaDB and Samsung NVMe SSDs Accelerate NoSQL Database Performance*](http://tools.voicesatsamsungsemiconductor.com/r_and_d_labs/tools/toolbox.php?id=6e15b7f4-1f09-4487-b9c0-7842fca81627&dl=1&t=1487264796) (PDF), Samsung Semiconductor Inc., p. 12, retrieved 2019-02-07
7. [↑](./ScyllaDB#cite_ref-7) Wiggins, Kyle (2024-10-17). ["ScyllaDB raises $43M to scale its NoSQL database platform"](https://techcrunch.com/2023/10/17/scylladb-raises-43m-to-scale-its-nosql-database-platform/). Tech Crunch. Retrieved 2025-12-11.
8. [↑](./ScyllaDB#cite_ref-8) ["Cassandra Rewritten In C++, Ten Times Faster - Slashdot"](https://developers.slashdot.org/story/15/09/22/2145258/cassandra-rewritten-in-c-ten-times-faster). *developers.slashdot.org*. 2015-09-22. Retrieved 2025-02-26.
9. [↑](./ScyllaDB#cite_ref-9) ["Why We're Moving to a Source Available License"](https://www.scylladb.com/2024/12/18/why-were-moving-to-a-source-available-license/). 2024-12-18.
10. [↑](./ScyllaDB#cite_ref-10) ["ScyllaDB adds vector search to managed database platform"](https://www.techtarget.com/searchdatamanagement/news/366637573/ScyllaDB-adds-vector-search-to-managed-database-platform). *www.techtarget.com/*. 2026-01-20. Retrieved 2026-02-23.
11. [↑](./ScyllaDB#cite_ref-11) ["Open source USearch library jumpstarts ScyllaDB vector search"](https://thenewstack.io/open-source-usearch-library-jumpstarts-scylladb-vector-search/). *thenewstack.io/*. 2026-02-05. Retrieved 2026-02-23.

 

## External links

 
- [Scylla public GitHub repository](https://github.com/scylladb/scylla), with source code repository and bug tracker
- [ScyllaDB Inc. homepage](http://www.scylladb.com/)
- [ScyllaDB another contender to the open source NoSQL database crown](https://www.networkworld.com/article/3171924/database-administration/scylladb-another-contender-to-the-open-source-nosql-database-crown)
- [How Scylla Scaled to One Billion Rows a Second](https://www.scylladb.com/2019/12/12/how-scylla-scaled-to-one-billion-rows-a-second/)