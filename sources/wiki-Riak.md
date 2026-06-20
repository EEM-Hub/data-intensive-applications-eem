---
source: https://en.wikipedia.org/wiki/Riak
fetched: 2026-06-19
---

Distributed NoSQL key-value data store 
| Riak |
| --- |
|  |
| Developer | CommunityBasho Technologies |
| Release | August17, 2009;16 years ago(2009-08-17) |
|  |
| Stable release | 3.2.0
   / January1, 2023;3 years ago(2023-01-01)[1] |
|  |
| Written in | Erlang |
| Operating system | Linux,BSD,macOS,Solaris,Raspian |
| Platform | IA-32,x86-64,AArch32 |
| Type | NoSQLDatabase,data store,Cloud storage |
| License | Apache License 2.0 |
| Website | riak.com |
| Repository | github.com/basho/riak_core |

  

**Riak** (pronounced "ree-ack" [[2]](./Riak#cite_note-Riak_1.0_Release_Party-2)) is a distributed [NoSQL](./NoSQL) [key-value data store](./Key-value_data_store) that offers [high availability](./High_availability), [fault tolerance](./Fault_tolerance), operational simplicity, and [scalability](./Scalability).[[3]](./Riak#cite_note-Datamation-3) Riak moved to an entirely [open-source](./Open-source_software) project in August 2017, with many of the licensed Enterprise Edition features being incorporated.[[4]](./Riak#cite_note-Riak_KV_2.2.6_Release_Notes-4) Riak implements the principles from Amazon's [Dynamo](./Dynamo_(storage_system)) paper[[5]](./Riak#cite_note-5) with heavy influence from the [CAP theorem](./CAP_theorem). Written in [Erlang](./Erlang_(programming_language)), Riak has fault-tolerant data replication and automatic data distribution across the cluster for performance and resilience.[[6]](./Riak#cite_note-morgan-timothy-6)

 

Riak has a pluggable backend for its core storage, with the default storage backend being [Bitcask](./Bitcask).[[7]](./Riak#cite_note-7) [LevelDB](./LevelDB) is also supported, with other options (such as the pure-Erlang [Leveled](./Leveled_(key-value_datastore)?action=edit&redlink=1)) available depending on the version.

 

Riak was originally developed by engineers employed by Basho Technologies[[8]](./Riak#cite_note-8) and maintained by them until 2017 when the rights were sold to [bet365](./Bet365)[[9]](./Riak#cite_note-:0-9)[[10]](./Riak#cite_note-:3-10) after Basho went into receivership.[[11]](./Riak#cite_note-:1-11)

 

## Main features

 
|  | This sectiondoes notciteanysources.Please helpimprove this sectionbyadding citations to reliable sources. Unsourced material may be challenged andremoved.(March 2015)(Learn how and when to remove this message) |
| --- | --- |

 Fault-tolerant availabilityRiak replicates key/value stores across a cluster of nodes with a default n_val of three. In the case of node outages due to [network partition](./Network_partition) or hardware failures, data can still be written to a neighboring node beyond the initial three, and read-back due to its "masterless" peer-to-peer architecture. QueriesRiak provides a [REST-ful](./Representational_state_transfer) [API](./Application_programming_interface) through HTTP and [Protocol Buffers](./Protocol_Buffers) for basic PUT, GET, POST, and DELETE functions. More complex queries are also possible, including secondary indexes, search (via [Apache Solr](./Apache_Solr)), and [MapReduce](./MapReduce). MapReduce has native support for both [JavaScript](./JavaScript) (using the [SpiderMonkey](./SpiderMonkey) runtime) and Erlang. Predictable latencyRiak distributes data across nodes with hashing and can provide latency profile, even in the case of multiple node failures. Storage optionsKeys/values can be stored in memory, disk, or both. Multi-datacenter replicationMulti-Datacenter replication (MDC) provides uni-directional and bi-direction replication of data between Riak clusters, whether locally for resilience or globally for faster regional access. Uni-directional replication is useful for read-only sinks such as backups and Disaster Recovery sites. Bi-directional replication allows for multiple Riak cluster to have eventually consistent data across vast distances. Complex replication scenarios such as chains, hub-and-spoke and mesh networks are possible due to the Cascades feature, which allows replication of data between clusters that are not directly connected.  There are two primary modes of operation: fullsync and realtime. Fullsync mode ensures that all data on the source cluster is replicated to the sink cluster. Only the metadata and changes are transferred, making this fast and efficient. Realtime mode sends updates made to a source cluster to the sink cluster in realtime. These modes are designed to work together for best performance  All multi-datacenter replication occurs over multiple concurrent TCP connections to maximize performance and network utilization. Tunable consistencyOption to choose between eventual and strong consistency for each bucket. 

## Main products

 

All versions of Riak are now entirely open-source and free, and include the extra features that Basho charged license fees for.

 

Basho operated a freemium model, wherein they provided free versions of Riak in the form of Riak Core, Riak KV, Riak CS and Riak TS but made their money from licensing more advanced features and SLA-based support. The extra features from the Enterprise Editions have since been integrated into the open source version of Riak KV, as of Riak KV release 2.2.6.[[12]](./Riak#cite_note-:5-12) and Riak CS 2.1.2 [[13]](./Riak#cite_note-13)

 

### Riak Core and Riak Core Lite

 

#### Riak Core

 

riak_core[[14]](./Riak#cite_note-14) is the distributed systems framework that underpins Riak, forming the foundation for all Riak versions. It is being maintained as part of Riak.

 

#### Riak Core Lite

 

riak_core_lite[[15]](./Riak#cite_note-15) is intended for general use as a base for creating distributed systems.

 

### Riak KV (Key-Value)

 

Riak KV is a distributed NoSQL database designed to deliver maximum data availability by distributing data across multiple servers, meaning that if one client can reach one server, it should be able to read and write data.[[16]](./Riak#cite_note-16) KV went through a few names in its lifetime, starting as Riak then Riak DS (for Data Store) and finally Riak KV (for Key-Value).

 

When Basho Technologies went into receivership in 2017[[11]](./Riak#cite_note-:1-11) KV development was picked up by the open source community and has continued into 2021, with 2.2.6 released in 2018 being the first community release of KV. This release integrated some features that were originally restricted to Basho's Enterprise versions of Riak.[[12]](./Riak#cite_note-:5-12)

 

Version 2.9.0 was the first major community release by the open source community, releasing in November 2019,[[12]](./Riak#cite_note-:5-12) with version 3.0.1 following on August 20, 2020.[[12]](./Riak#cite_note-:5-12) Development has continued since then with the latest release being version 3.0.7.[[17]](./Riak#cite_note-:6-17)

 

#### Removed features

 

The current version of Riak no longer supports some features in the Enterprise edition of Riak, including:

 
- SNMP/JMX support

 

#### Separated features in Riak KV 3.0+

 

The following features of Riak KV 2.x have been removed by default from the Riak build. Specific builds including these features are available.

 
- Yokozuna

 

### Riak CS (Cloud Storage)

 

Originally known as Riak Moss[[18]](./Riak#cite_note-18)(Riak Multi-tenant Object Storage System - MOSS) but named as Riak CS (Cloud Storage) when released, Riak CS was first publicly released in January 2012.

 

Riak CS (Cloud Storage) is object storage software built on top of Riak KV, Riak's distributed database. Riak CS is designed to provide simple, highly-available, distributed cloud storage at any scale, and can be used to build cloud architectures or as storage infrastructure for heavy-duty applications and services.[[19]](./Riak#cite_note-19)

 

Riak CS also includes an application called Stanchion[[20]](./Riak#cite_note-20) which is used to manage the serialization of requests. This enables Riak CS to manage globally unique entities like users and bucket names. Serialization in this context means that the entire cluster agrees upon a single value for any globally unique entity at any given time; when that value is changed, the new value must be recognized throughout the entire cluster.

 

Riak CS was briefly rebranded as Riak S2 to make it more obviously compatible with Amazon S3 but the name did not catch on and it reverted to Riak CS.

 

In 2021 development for Riak CS was resumed with contributions from TI Tokyo.

 

### Riak TS (Time Series)

 

Riak TS is an extension to Riak KV optimized for time series data, in that:

 
- it supports [structured data](https://docs.riak.com/riak/ts/1.5.2/using/planning/index.html#ts-table-schema), with table definition (with a `CREATE TABLE` call) required before data can be written;
- data slices from contiguous regions in its primary index (“quanta”) are stored on the same partition;
- CRUD operations are optimized for speed, at the expense of consistency.

 

A limited [subset](https://docs.riak.com/riak/ts/1.5.2/using/querying/reference/index.html) of SQL commands was implemented in Riak TS. There is no provision for consistency guarantees between tables (no foreign indexes). In `SELECT` statements, `WHERE` clause is supported but `HAVING` is not. `ORDER BY` was to appear in a version that was never released.

 

Riak TS existed as a collection of branches (in separate components of Riak KV such as riak_kv, riak_pb, etc.) and not as product with a repository of its own. It was developed by a dedicated team consisting of Gordon Guthrie (leader), Andy Till and Andrei Zavada, with occasional contributions from other developers.

 

Riak TS was conceived, along with Riak Data Platform project, as an attempt to diversify Basho's product line, an undertaking many insiders regard as misguided and eventually contributing to Basho's demise.

 

## Licensing and support

 

Riak was originally licensed using a [freemium](./Freemium) model: open source versions of Riak KV, Riak CS and Riak TS are available, but end users can pay for additional features and support. However, since Basho entered receivership[[11]](./Riak#cite_note-:1-11) and bet365[[10]](./Riak#cite_note-:3-10) (purchasers of all IP) made all Riak products fully open source, all the premium features are now available in the open source versions. Since Basho's demise, community[[21]](./Riak#cite_note-21) ad-hoc and paid support options have arisen.

 

## Language support

 

Riak has official drivers for [Ruby](./Ruby_(programming_language)), [Java](./Java_(programming_language)), [Erlang](./Erlang_(programming_language)) and [Python](./Python_(programming_language)). There are also numerous community-supported drivers for other programming languages.[[22]](./Riak#cite_note-22)

 

## Community development

 

After bet365[[10]](./Riak#cite_note-:3-10) purchased the Riak IP,[[9]](./Riak#cite_note-:0-9) the Riak products were made full open source and work to integrate premium features into the open source versions was completed with the 2.2.6 release.

 

## History

 

Riak was originally written by Andy Gross and Justin Sheehy at [Basho Technologies](./Basho_Technologies)[[2]](./Riak#cite_note-Riak_1.0_Release_Party-2) to power a web Sales Force Automation application by former engineers and executives from [Akamai](./Akamai_Technologies). There was more interest in the datastore technology than the applications built on it, so the company decided to build a business around Riak itself, gaining adoption throughout the Fortune 100 and becoming a foundation to many of the world's fastest-growing Web-based, mobile and social networking applications, as well as cloud service providers. Releases after graduation include

 

### Riak KV

 

Riak 1.0 was released September 10, 2011

 
| Version! | Date Released | Changes |
| --- | --- | --- |
| 1.0 | September 10, 2011 | Inition 1.0 Release[23] |
| 1.1 | February 21, 2012 | Added Riaknostic, enhanced error logging and reporting, improved resiliency for large clusters, and a new graphical operations and monitoring interface called Riak Control. |
| 1.4 | July 10, 2013 | Added counters, secondary indexing improvements, reduced object storage overhead, handoff progress reporting, and enhancements to MDC replication |
| 2.0 | September 2, 2014 | Added new data types including sets, maps, registers, and flags simplifying application development. Strong consistency by bucket, full-text integration with Apache Solr, Security, and reduced replicas for Secondary sites. |
| 2.1 | April 16, 2015 | Added an optimization for many write-heavy workloads – “write once” buckets – buckets whose entries are intended to be written exactly once, and never updated or over-written. |
| 2.2 | November 17, 2016 | added Support forDebian8 andUbuntu16.04,Solrintegration improvements.[24] |
| 2.2.6 | May 21, 2018 | The first community release. Added support for Multi-Datacentre Replication which was not part of open-source Riak before, added a grow-only set data type, improved data distribution over nodes and cleaned up production test issues.[25] |
| 2.9.0 | November 20, 2019 | Added early support for TicTac Active Anti-Entropy, support for a new Riak specific backend called Leveled.[12] |
| 2.9.1 | February 17, 2020 | Implements next-gen replication,[26]various changes to tombstones and bucket listing.[12] |
| 2.9.7 | August 16, 2020 | Improved Active Anti-Entropy and improved Riak's overall stability. |
| 2.9.8 | December 7, 2020 | Improved leveled functions[27] |
| 2.9.9 | August 6, 2021 | Leveled stability improvements[28] |
| 3.0.1 | August 20, 2020 | Adds support for OTP 20, 21, 22 but is not backwards compatible with previous OTP versions.[12] |
| 3.0.2 | January 5, 2021 | Implements backend changes from 2.9.8, adds arange_checkin the Tictac AAE based full-sync replication[12] |
| 3.0.6 | May 8, 2021 | Adds location-awareness to cluster management,[29]along with bug fixes from 3.0.3 and 3.0.4.[12] |
| 3.0.7 | July 21, 2021 | Reverts Riak erlang runtime system in interactive mode, rather than the embedded mode it was changed to previously.[17] |
| 3.0.8 | October 12, 2021 | Support flushing of disk writes, implement read-repair for key ranges to accelerate recovery after known node outage[30] |
| 3.0.9 | November 12, 2021 | Improve latency and expand statistics of secondary-index queries, including information about result counts and overall query time[31] |
| 3.0.10 | March 30, 2022 | Improve memory management in leveled backend, add peer discovery without configuration changes, allow configuration of Erlang VM memory and scheduler settings viariak.conf[32] |
| 3.0.11 | October 11, 2022 | Fix a bottleneck in secondary index queries with the leveled backend and > 1000 queries per second[33] |
| 3.0.12 | December 20, 2022 | Improve memory management in the leveled backend, update leveldb snappy compression for wider platform support, introduce thereip_manualconsole command[34] |
| 3.2.0 | January 1, 2023 | Support Erlang/OTP 22, 24, and 25, update to Erlang/OTP's new logging API, update packaging to include support for Alpine Linux and FreeBSD[35] |
| 3.0.13 | February 4, 2023 | Improve reliability of handoffs, add administrative helper functions toriak_client[36] |
| 3.0.14 | February 13, 2023 | Fix an issue related to handling back-pressure correctly in the leveled backend, add support for handing off reap requests via thehandoff_deletesoption[37] |
| 3.0.15 | February 15, 2023 | Correct an issue introduced with theauto_checkfeature for TictacAAE full-sync introduced in 3.0.10[38] |

 

### Riak CS

 

Riak CS was made open source on March 20, 2013[[39]](./Riak#cite_note-39)

 
| Version! | Date Released | Changes |
| --- | --- | --- |
| 0.0.3 | January 26, 2012 | The first public release of Riak CS. Known as Riak MOSS at the time.[40] |
| 0.1.0 | February 25, 2012 | Bucket-level Access control, user record changes, Stanchion is now required.[41] |
| 1.0.0 | April 2, 2012 | Fixes some process/socket leaks, adds a fix to prevent deadlock conditions, new subsystem for user access & storage usage calculations.[42] |
| 1.0.1 | April 18, 2012 | Fixes a bug that caused requests to hang if a node in the cluster was unavailable[43] |
| 1.1.0 | August 20, 2012 | Updates user creation, configuration options for anonymous users, more user account controls for admins, Garbage collection for deleted objects, improved performance.[44] |
| 1.2.0 | October 23, 2012 | Early support for Multi-datacenter replication, support for riak_test integration, bug fixes.[45] |
| 1.2.1 | January 23, 2016 | Add reduce phase for listing bucket contents to provide backpressure when executing the MapReduce job, Use prereduce during storage calculations, fixed incorrect 404 error when attempting to list contents of nonexistent bucket.[46] |
| 1.2.2 | November 8, 2012 | Full support for MDC replication, fixed process leaks.[47] |
| 1.3.0 | March 20, 2013 | Support for multi-part file uploads, bucket polices for restricted principles/conditions, range header. More administrative command controls, support for FreeBSD, SmartOS and Solaris Packaging.[48] |
| 1.3.1 | April 4, 2013 | Bug fixes[49] |
| 1.4.0 | August 12, 2013 | Early support for Swift API/Keystone Authentication, improved performance, bug fixes.[50] |
| 1.5.0 | July 31, 2014 | Adds a multibag technical preview, new debug command, streamlines commands to new `riak-cs admin` command, improved garbage collection, updated lager, new API - Multiple objects, warning logs for manifests, siblings etc.[51] |
| 1.5.1 | September 10, 2014 | Adds Bucket restrictions, adds sleep interval for manifest updates, updates riak-cs-debug, changes to bucket resolution.[52] |
| 1.5.2 | October 9, 2014 | Improved logging for failures with Riak, Changes to log output for access stats, adds a script for invalid garbage collection manifest repairs.[53] |
| 1.5.3 | December 12, 2014 | Addread_before_last_manifest_writeoption, Adds configurable timeouts for CS interactions with Riak[54] |
| 1.5.4 | March 13, 2015 | Disable backpressure sleep, Fixes an incorrect path rewrite in S3 API[55] |
| 2.0.0 | March 27, 2015 | Updates Riak CS to work with Riak 2.0.5, Changes gc_max_workers to gc.max_workers and changed default setting, early support for AWS v4 authentication, adds cuttlefish, storage optimisations.[56] |
| 2.1.0 | October 14, 2015 | Final Basho release - Backwards compatible with KV 2.0.5, 21.1, Adds a large number of new metrics for health monitoring purposes along with storage usage metrics. Replaced commands with riak-cs-admin equivalents. Garbage collection improvements.[57] |
| 2.1.1 | October 14, 2015 | Compatible with KV 2.1.3, 2.1.4, 2.2.x and 2.9.x |
| 2.1.2 | April 9, 2019 | First post-basho release.[58] |

 

### Riak TS

 

Riak TS was originally released in October 2015 [[59]](./Riak#cite_note-59)

 
| Version! | Date Released | Changes |
| --- | --- | --- |
| 1.2.0 | February 23, 2016 | Implements Riak_shell to allow SWQL commands & logging in a single shell in Riak TS. Bug fixes, Multi-Datacenter replication and riak search not supported.[60] |
| 1.3.0 | May 4, 2016 | Open sources Riak TS, adds a HTTP API, additional SQL commands and support for MDC replication for enterprise users[61] |
| 1.3.1 | July 5, 2016 | Addresses Data loss bug in 1.3.0.[62] |
| 1.4.0 | August 24, 2016 | Adds new SQL features, Rolling upgrade/downgrade support, Global data expiry (per cluster).[63] |
| 1.5.0 | December 20, 2016 | Expands SQL implementation, Improves data storage and improved overall performance.[64] |
| 1.5.1 | January 24, 2017 | Bug fixes from 1.5.0[65] |
| 1.5.2 | February 21, 2017 | Bug Fixes from 1.5.1[66] |

 

## Users

 

Notable users include [AT&T](./AT&T), [Comcast](./Comcast),[[67]](./Riak#cite_note-gigaom-67) [GitHub](./GitHub),[[67]](./Riak#cite_note-gigaom-67) [Best Buy](./Best_Buy),[[67]](./Riak#cite_note-gigaom-67) [UK National Health Services (NHS)](./National_Health_Service),[[68]](./Riak#cite_note-68) [The Weather Channel](./The_Weather_Channel),[[69]](./Riak#cite_note-69) and [Riot Games](./Riot_Games).[[70]](./Riak#cite_note-70)

 

## See also

 
- ![](//upload.wikimedia.org/wikipedia/commons/thumb/3/31/Free_and_open-source_software_logo_%282009%29.svg/40px-Free_and_open-source_software_logo_%282009%29.svg.png)[Free and open-source software portal](./Portal:Free_and_open-source_software)

 
- [Basho Technologies](./Basho_Technologies)
- [Apache Accumulo](./Apache_Accumulo)
- [Oracle NoSQL Database](./Oracle_NoSQL_Database)
- [NoSQL](./NoSQL)
- [Structured storage](./Structured_storage)
- [Memcached](./Memcached)
- [Redis](./Redis)

 

## References

  
1. [↑](./Riak#cite_ref-1) [*Riak 3.2.0 release notes*](https://github.com/basho/riak/blob/develop/RELEASE-NOTES.md#riak-kv-320-release-notes), 2023-01-01
2. [1](./Riak#cite_ref-Riak_1.0_Release_Party_2-0) [2](./Riak#cite_ref-Riak_1.0_Release_Party_2-1) Sheehy, Justin. ["Riak 1.0 Release Party"](https://vimeo.com/31979504). *Vimeo*.
3. [↑](./Riak#cite_ref-Datamation_3-0) Harvey, Cynthia (23 May 2014). ["60 Open Source Apps You Can Use in the Cloud"](http://www.datamation.com/open-source/60-open-source-apps-you-can-use-in-the-cloud-2.html). Datamation. Retrieved 5 June 2014.
4. [↑](./Riak#cite_ref-Riak_KV_2.2.6_Release_Notes_4-0) ["Riak KV 2.2.6 Release Notes"](https://github.com/basho/riak/blob/riak-2.2.6/RELEASE-NOTES.md). *github.com*. April 26, 2018. Retrieved September 10, 2021.
5. [↑](./Riak#cite_ref-5) DeCandia, Giuseppe; Hastorun, Deniz; Jampani, Madan; Kakulapati, Gunavardhan; Lakshman, Avinash; Pilchin, Alex; Sivasubramanian, Swaminathan; Vosshall, Peter; Vogels, Werner (October 14–17, 2007). [*Dynamo: Amazon's Highly Available Key-value Store*](http://www.allthingsdistributed.com/files/amazon-dynamo-sosp2007.pdf) (PDF). [Proceedings of 21st ACM SIGOPS Symposium on Operating Systems Principles (SOSP '07)](http://www.sosp2007.org/). Stevenson, Washington, USA: ACM. pp. 205–220. [doi](./Doi_(identifier)):[10.1145/1294261.1294281](https://doi.org/10.1145%2F1294261.1294281). [ISBN](./ISBN_(identifier)) [978-1-59593-591-5](./Special:BookSources/978-1-59593-591-5). Retrieved 5 June 2014.
6. [↑](./Riak#cite_ref-morgan-timothy_6-0) Morgan, Timothy Prickett (7 May 2014). ["Eucalyptus Scales Out AWS Cloud Clone"](http://www.enterprisetech.com/2014/05/07/eucalyptus-scales-aws-cloud-clone/). Enterprise Tech. Retrieved 5 June 2014.
7. [↑](./Riak#cite_ref-7) ["Basho: Bitcask"](https://docs.riak.com/riak/kv/2.2.3/setup/planning/backend/bitcask/index.html). *docs.riak.com*. Retrieved 2021-09-14.
8. [↑](./Riak#cite_ref-8) ["Basho Technologies"](https://en.wikipedia.org/w/index.php?title=Basho_Technologies&oldid=989545576), *Wikipedia*, 2020-11-19, retrieved 2021-07-15
9. [1](./Riak#cite_ref-:0_9-0) [2](./Riak#cite_ref-:0_9-1) ["Riak NoSQL snapped up by Bet365"](https://www.computerweekly.com/news/450426130/Riak-NoSQL-snapped-up-by-bet365). *ComputerWeekly.com*. Retrieved 2021-07-15.
10. [1](./Riak#cite_ref-:3_10-0) [2](./Riak#cite_ref-:3_10-1) [3](./Riak#cite_ref-:3_10-2) ["Bet365"](https://en.wikipedia.org/w/index.php?title=Bet365&oldid=1033491214), *Wikipedia*, 2021-07-14, retrieved 2021-07-30
11. [1](./Riak#cite_ref-:1_11-0) [2](./Riak#cite_ref-:1_11-1) [3](./Riak#cite_ref-:1_11-2) Hill, Rebecca. ["End of the road for Basho: Court puts biz into receivership"](https://www.theregister.com/2017/07/31/end_of_the_road_for_basho_as_court_puts_biz_into_receivership/). *www.theregister.com*. Retrieved 2021-07-15.
12. [1](./Riak#cite_ref-:5_12-0) [2](./Riak#cite_ref-:5_12-1) [3](./Riak#cite_ref-:5_12-2) [4](./Riak#cite_ref-:5_12-3) [5](./Riak#cite_ref-:5_12-4) [6](./Riak#cite_ref-:5_12-5) [7](./Riak#cite_ref-:5_12-6) [8](./Riak#cite_ref-:5_12-7) [9](./Riak#cite_ref-:5_12-8) ["basho/riak"](https://github.com/basho/riak). *GitHub*. Retrieved 2021-07-15.
13. [↑](./Riak#cite_ref-13) ["basho/riak_cs"](https://github.com/basho/riak_cs/tree/2.1.2). *GitHub*. Retrieved 2021-07-24.
14. [↑](./Riak#cite_ref-14) ["Riak Core"](https://github.com/basho/riak_core/blob/develop-3.0/README.md). *[GitHub](./GitHub)*.
15. [↑](./Riak#cite_ref-15) ["Riak Core Lite"](https://github.com/riak-core-lite/riak_core_lite/blob/master/README.md). *[GitHub](./GitHub)*.
16. [↑](./Riak#cite_ref-16) ["Riak KV"](https://docs.riak.com/riak/kv/latest/index.html). *docs.Riak.com*. 15 July 2021.
17. [1](./Riak#cite_ref-:6_17-0) [2](./Riak#cite_ref-:6_17-1) ["Riak KV 3.0.7 Release notes"](https://github.com/basho/riak/blob/develop-3.0/RELEASE-NOTES.md#riak-kv-307-release-notes). *Riak Github*. 2021-07-21. Retrieved 2021-09-02.
18. [↑](./Riak#cite_ref-18) ["Riak Moss"](https://github.com/basho/riak_cs/tree/0.0.3). *Github*. 2012-01-26. Retrieved 2021-08-24.
19. [↑](./Riak#cite_ref-19) ["Riak Cloud Storage"](https://docs.riak.com/riak/cs/2.1.1/index.html). *docs.Riak.com*. 15 July 2021.
20. [↑](./Riak#cite_ref-20) ["Stanchion Application"](https://www.tiot.jp/riak-docs/riak/cs/2.1.1/theory/stanchion/index.html). *Tiot.jp*. Retrieved 2021-08-24.
21. [↑](./Riak#cite_ref-21) ["Riak Community site"](https://www.riak.info/). *Riak info*. 2021-09-14. Retrieved 2021-09-14.
22. [↑](./Riak#cite_ref-22) ["Riak Client Libraries and Community Code"](http://docs.basho.com/). Retrieved 5 June 2014.
23. [↑](./Riak#cite_ref-23) ["Riak 1.0 release"](https://riak.com/posts/business/riak-1-0-is-officially-released/index.html?p=6114.html). *Riak.com*. 2011-09-11. Retrieved 2021-08-26.
24. [↑](./Riak#cite_ref-2.2.0-release-notes_24-0) ["Riak KV 2.2.0 Release Notes"](http://docs.basho.com/riak/kv/2.2.0/release-notes/). Basho. 2016-11-17. Retrieved 2016-12-21.
25. [↑](./Riak#cite_ref-2.2.5-release-notes_25-0) ["Riak KV 2.2.5 Release Notes"](https://github.com/basho/riak/blob/riak-2.2.5/RELEASE-NOTES.md). *[GitHub](./GitHub)*. Retrieved 23 June 2018.
26. [↑](./Riak#cite_ref-26) ["basho/riak_kv"](https://github.com/basho/riak_kv). *GitHub*. Retrieved 2021-07-15.
27. [↑](./Riak#cite_ref-27) ["Riak KV 2.9.8 release notes"](https://github.com/basho/riak/blob/riak-2.9.8/RELEASE-NOTES.md). *Github*. 2020-12-07. Retrieved 2021-08-19.
28. [↑](./Riak#cite_ref-28) ["Release notes 2.9.9"](https://github.com/basho/riak_kv/releases/tag/riak_kv-2.9.9). *[GitHub](./GitHub)*. 2021-08-06. Retrieved 2021-08-24.
29. [↑](./Riak#cite_ref-29) ["basho/riak_core"](https://github.com/basho/riak_core). *GitHub*. Retrieved 2021-07-15.
30. [↑](./Riak#cite_ref-30) ["Riak KV 3.0.8 Release notes"](https://github.com/basho/riak/blob/develop/RELEASE-NOTES.md#riak-kv-308-release-notes). *Riak Github*. 2021-10-12. Retrieved 2023-05-12.
31. [↑](./Riak#cite_ref-31) ["Riak KV 3.0.9 Release notes"](https://github.com/basho/riak/blob/develop/RELEASE-NOTES.md#riak-kv-309-release-notes). *Riak Github*. 2021-11-12. Retrieved 2023-05-12.
32. [↑](./Riak#cite_ref-32) ["Riak KV 3.0.10 Release notes"](https://github.com/basho/riak/blob/develop/RELEASE-NOTES.md#riak-kv-3010-release-notes). *Riak Github*. 2022-03-30. Retrieved 2023-05-12.
33. [↑](./Riak#cite_ref-33) ["Riak KV 3.0.11 Release notes"](https://github.com/basho/riak/blob/develop/RELEASE-NOTES.md#riak-kv-3011-release-notes). *Riak Github*. 2022-10-11. Retrieved 2023-05-12.
34. [↑](./Riak#cite_ref-34) ["Riak KV 3.0.12 Release notes"](https://github.com/basho/riak/blob/develop/RELEASE-NOTES.md#riak-kv-3012-release-notes). *Riak Github*. 2022-12-20. Retrieved 2023-05-12.
35. [↑](./Riak#cite_ref-35) ["Riak KV 3.2.0 Release notes"](https://github.com/basho/riak/blob/develop/RELEASE-NOTES.md#riak-kv-320-release-notes). *Riak Github*. 2023-01-01. Retrieved 2023-05-12.
36. [↑](./Riak#cite_ref-36) ["Riak KV 3.0.13 Release notes"](https://github.com/basho/riak/blob/develop/RELEASE-NOTES.md#riak-kv-3013-release-notes). *Riak Github*. 2023-02-04. Retrieved 2023-05-12.
37. [↑](./Riak#cite_ref-37) ["Riak KV 3.0.14 Release notes"](https://github.com/basho/riak/blob/develop/RELEASE-NOTES.md#riak-kv-3014-release-notes). *Riak Github*. 2023-02-13. Retrieved 2023-05-12.
38. [↑](./Riak#cite_ref-38) ["Riak KV 3.0.15 Release notes"](https://github.com/basho/riak/blob/develop/RELEASE-NOTES.md#riak-kv-3015-release-notes). *Riak Github*. 2023-02-15. Retrieved 2023-05-12.
39. [↑](./Riak#cite_ref-39) ["Riak CS is now open source"](https://riak.com/riak-cs-is-now-open-source/). *Riak.com*. 2013-03-20. Retrieved 2021-08-26.
40. [↑](./Riak#cite_ref-40) ["Riak MOSS 0.0.3"](https://github.com/basho/riak_cs/releases/tag/0.0.3). *Github*. 2012-02-26. Retrieved 2021-09-02.
41. [↑](./Riak#cite_ref-41) ["Riak CS 0.1.0 Release notes"](https://github.com/basho/riak_cs/blob/1.1/RELEASE-NOTES.org#riak-cs-010-release-notes). *Github*. 2012-02-25. Retrieved 2021-09-02.
42. [↑](./Riak#cite_ref-42) ["Moss 1.0 Release notes"](https://github.com/basho/riak_cs/blob/1.0/RELEASE-NOTES.org#moss-100-release-notes). *Github*. 2012-04-02. Retrieved 2021-09-02.
43. [↑](./Riak#cite_ref-43) ["Moss 1.0.1 Release notes"](https://github.com/basho/riak_cs/blob/1.0/RELEASE-NOTES.org#moss-101-release-notes). *Github*. 2012-04-18. Retrieved 2021-09-02.
44. [↑](./Riak#cite_ref-44) ["Riak CS 1.1.0 release notes"](https://github.com/basho/riak_cs/blob/1.1/RELEASE-NOTES.org). *Riak CS Github*. 2012-08-20. Retrieved 2021-09-02.
45. [↑](./Riak#cite_ref-45) ["Riak CS 1.2 Release Notes"](https://github.com/basho/riak_cs/blob/1.2/RELEASE-NOTES.org#riak-cs-122-release-notes). *Riak CS Github*. 2012-10-23. Retrieved 2021-09-02.
46. [↑](./Riak#cite_ref-46) ["Riak CS 1.2.1 Release notes"](https://github.com/basho/riak_cs/blob/1.2/RELEASE-NOTES.org#riak-cs-121-release-notes). *Riak CS Github*. 2012-10-23. Retrieved 2021-09-02.
47. [↑](./Riak#cite_ref-47) ["Riak CS Release notes"](https://github.com/basho/riak_cs/blob/1.2/RELEASE-NOTES.org#riak-cs-122-release-notes). *Riak CS Github*. 2012-11-08. Retrieved 2021-09-02.
48. [↑](./Riak#cite_ref-48) ["Riak CS Release"](https://github.com/basho/riak_cs/releases/tag/1.3.0). *Riak CS Github*. 2013-03-20. Retrieved 2021-09-02.
49. [↑](./Riak#cite_ref-49) ["Riak CS 1.3.1 Release notes"](https://github.com/basho/riak_cs/releases/tag/1.3.1). *Riak CS Github*. 2013-04-04. Retrieved 2021-09-02.
50. [↑](./Riak#cite_ref-50) ["Riak CS 1.4.0 Release"](https://github.com/basho/riak_cs/releases/tag/1.4.0). *Riak CS Github*. 2013-08-12. Retrieved 2021-09-02.
51. [↑](./Riak#cite_ref-51) ["Riak CS Release"](https://github.com/basho/riak_cs/releases/tag/1.5.0). *Riak CS Github*. 2014-07-31. Retrieved 2021-09-02.
52. [↑](./Riak#cite_ref-52) ["Riak CS Release"](https://github.com/basho/riak_cs/releases/tag/1.5.1). *Riak CS Github*. 2014-09-10. Retrieved 2021-09-02.
53. [↑](./Riak#cite_ref-53) ["Riak CS Releases"](https://github.com/basho/riak_cs/releases/tag/1.5.2). *Riak CS github*. 2014-10-09. Retrieved 2021-09-02.
54. [↑](./Riak#cite_ref-54) ["Riak CS Release"](https://github.com/basho/riak_cs/releases/tag/1.5.3). *Riak CS Github*. 2014-12-12. Retrieved 2021-09-02.
55. [↑](./Riak#cite_ref-55) ["Riak CS Releases"](https://github.com/basho/riak_cs/releases/tag/1.5.4). *Riak CS Github*. 2015-03-13. Retrieved 2021-09-02.
56. [↑](./Riak#cite_ref-56) ["Docs.riak.com"](https://docs.riak.com/riak/cs/latest/cookbooks/release-notes/index.html#riak-cs-2-0-0). *Riak CS Release notes*. 2015-03-27. Retrieved 2021-09-02.
57. [↑](./Riak#cite_ref-57) ["Riak CS Release notes"](https://docs.riak.com/riak/cs/latest/cookbooks/release-notes/index.html#riak-s2-riak-cs-2-1-0-release-notes). *Docs.riak.com*. 2015-10-14. Retrieved 2021-09-02.
58. [↑](./Riak#cite_ref-58) ["Riak CS github"](https://github.com/basho/riak_cs/releases/tag/2.1.2). *Riak CS Github*. 2019-04-09. Retrieved 2021-09-02.
59. [↑](./Riak#cite_ref-59) ["Basho releases Riak TS (time-series)"](https://www.infoq.com/news/2015/10/basho-riak-ts/). *InfoQ*. 2015-10-27. Retrieved 2021-08-19.
60. [↑](./Riak#cite_ref-60) ["Riak TS release notes"](https://docs.riak.com/riak/ts/1.2.0/releasenotes/index.html). *docs.riak.com*. 2016-02-23. Retrieved 2021-09-14.
61. [↑](./Riak#cite_ref-61) ["Riak TS 1.3.0 Release notes"](https://docs.riak.com/riak/ts/1.3.0/releasenotes/). *docs.riak.com*. 2016-05-04. Retrieved 2021-09-14.
62. [↑](./Riak#cite_ref-62) ["Riak TS Release notes"](https://docs.riak.com/riak/ts/1.3.1/releasenotes/). *docs.riak.com*. 2016-07-05. Retrieved 2021-09-14.
63. [↑](./Riak#cite_ref-63) ["Riak TS 1.4.0 Release notes"](https://docs.riak.com/riak/ts/1.4.0/releasenotes/). *docs.riak.com*. 2016-08-24. Retrieved 2021-09-14.
64. [↑](./Riak#cite_ref-64) ["Riak TS 1.5.0 Release notes"](https://docs.riak.com/riak/ts/1.5.0/releasenotes/). *docs.riak.com*. 2016-12-20. Retrieved 2021-09-14.
65. [↑](./Riak#cite_ref-65) ["Riak TS 1.5.1 Release notes"](https://docs.riak.com/riak/ts/1.5.1/releasenotes/). *docs.riak.com*. 2017-01-24. Retrieved 2021-09-02.
66. [↑](./Riak#cite_ref-66) ["Riak TS 1.5.2 Release notes"](https://docs.riak.com/riak/ts/1.5.2/releasenotes/). *docs.riak.com*. 2017-02-21. Retrieved 2021-09-14.
67. [1](./Riak#cite_ref-gigaom_67-0) [2](./Riak#cite_ref-gigaom_67-1) [3](./Riak#cite_ref-gigaom_67-2) ["Basho Technologies takes aim at more enterprises with upgrades"](https://web.archive.org/web/20130224012630/http://gigaom.com/2013/02/21/basho-technologies-takes-aim-at-more-enterprises-with-upgrades/). 21 February 2013. Archived from [the original](https://gigaom.com/2013/02/21/basho-technologies-takes-aim-at-more-enterprises-with-upgrades/) on February 24, 2013. Retrieved 26 March 2015.
68. [↑](./Riak#cite_ref-68) Clark, Jack (10 October 2013). ["NHS tears out its Oracle Spine in favour of open source"](https://www.theregister.co.uk/2013/10/10/nhs_drops_oracle_for_riak/). The Register. Retrieved 5 June 2014.
69. [↑](./Riak#cite_ref-69) Henschen, Doug (2 June 2014). ["Why Big Data Tools Are Here To Stay: InformationWeek Video"](http://www.informationweek.com/big-data/big-data-analytics/why-big-data-tools-are-here-to-stay-informationweek-video/a/d-id/1269331?piddl_msgid=220785#msg_220785). InformationWeek. Retrieved 5 June 2014.
70. [↑](./Riak#cite_ref-70) Ptaszek, Michal (16 January 2016). ["Chat Service Architecture: Persistence"](https://engineering.riotgames.com/news/chat-service-architecture-persistence). RiotGames. Retrieved 2 February 2016.

 

## External links

 
- [Official website](https://riak.com/) [![Edit this at Wikidata](//upload.wikimedia.org/wikipedia/en/thumb/8/8a/OOjs_UI_icon_edit-ltr-progressive.svg/20px-OOjs_UI_icon_edit-ltr-progressive.svg.png)](https://www.wikidata.org/wiki/Q2328712#P856)