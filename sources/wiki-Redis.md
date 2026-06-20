---
source: https://en.wikipedia.org/wiki/Redis
fetched: 2026-06-19
---

Source available in-memory key–value database For other uses, see [Redis (disambiguation)](./Redis_(disambiguation)). 
|  | This article has multiple issues.Please helpimprove itor discuss these issues on thetalk page.(Learn how and when to remove these messages)This articlecontainspromotional content.Please helpimprove itby removingpromotional languageand inappropriateexternal links, and by adding encyclopedic text written from aneutral point of view.See ouradvice if the article is about youand read ourscam warningin case someone asks for money to edit this article.(July 2025)(Learn how and when to remove this message)This articlerelies excessively onreferencestoprimary sources.Please improve this article by addingsecondary or tertiary sources.Find sources:"Redis"–news·newspapers·books·scholar·JSTOR(July 2025)(Learn how and when to remove this message)(Learn how and when to remove this message) |  | This articlecontainspromotional content.Please helpimprove itby removingpromotional languageand inappropriateexternal links, and by adding encyclopedic text written from aneutral point of view.See ouradvice if the article is about youand read ourscam warningin case someone asks for money to edit this article.(July 2025)(Learn how and when to remove this message) |  | This articlerelies excessively onreferencestoprimary sources.Please improve this article by addingsecondary or tertiary sources.Find sources:"Redis"–news·newspapers·books·scholar·JSTOR(July 2025)(Learn how and when to remove this message) |
| --- | --- | --- | --- | --- | --- |
|  | This articlecontainspromotional content.Please helpimprove itby removingpromotional languageand inappropriateexternal links, and by adding encyclopedic text written from aneutral point of view.See ouradvice if the article is about youand read ourscam warningin case someone asks for money to edit this article.(July 2025)(Learn how and when to remove this message) |
|  | This articlerelies excessively onreferencestoprimary sources.Please improve this article by addingsecondary or tertiary sources.Find sources:"Redis"–news·newspapers·books·scholar·JSTOR(July 2025)(Learn how and when to remove this message) |

 
| Redis |
| --- |
|  |
| Original author | Salvatore Sanfilippo[1][2] |
| Developer | Redis[1][2] |
| Release | February26, 2009;17 years ago(2009-02-26)[3] |
|  |
| Stable release | 8.8.0[4]/ May 25, 2026;26 days ago(May 25, 2026) |
|  |
| Written in | C |
| Operating system | Unix-like[5] |
| Available in | English |
| Type | Data structure store,key–value database |
| License | Redis Source Available License,SSPL[6]orAGPL[7] |
| Website | redis.io |
| Repository | github.com/redis/redis |

  

**Redis** ([/ˈrɛdɪs/](./Help:IPA/English);[[8]](./Redis#cite_note-RedisFAQ-8)[[9]](./Redis#cite_note-9) **Remote Dictionary Server**)[[8]](./Redis#cite_note-RedisFAQ-8) is an [in-memory](./In-memory_database) [key–value](./Key–value_database) [database](./Database), used as a [distributed cache](./Distributed_cache) and [message broker](./Message_broker), with optional [durability](./Durability_(database_systems)).[[10]](./Redis#cite_note-:9-10) Because it holds all data in [memory](./Random-access_memory) and because of its design, Redis offers low-[latency](./Latency_(engineering)) reads and writes, making it particularly suitable for use cases that require a cache. 

 

The project was developed and maintained by [Salvatore Sanfilippo](./Salvatore_Sanfilippo), starting in 2009.[[11]](./Redis#cite_note-11) From 2015 until 2020, he led a project core team sponsored by [Redis Labs](./Redis_(company)).[[12]](./Redis#cite_note-network-world-201507-12) Salvatore Sanfilippo left Redis as the maintainer in 2020.[[13]](./Redis#cite_note-theregister-13) In 2021 Redis Labs dropped the Labs from its name and now is known simply as "Redis".[[14]](./Redis#cite_note-14)

 

In 2018, some modules for Redis adopted a modified [Apache 2.0](./Apache_License) license with a [Commons Clause](./Commons_Clause).[[15]](./Redis#cite_note-theregister.com-15) In 2024, the main Redis code switched from the [open-source](./Open_source) [BSD-3 license](./BSD_licenses#3-clause) to being dual-licensed under the Redis [Source Available](./Source-available_software) License v2 and the [Server Side Public License](./Server_Side_Public_License) v1.[[6]](./Redis#cite_note-github20240420-6) On May 1, 2025, Redis became tri-licensed beginning with version 8.0, with the [GNU Affero General Public License](./GNU_Affero_General_Public_License) as the third option.[[7]](./Redis#cite_note-agpl-7)

 

## History

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/d/d5/Salvatore_Sanfilippo.png/250px-Salvatore_Sanfilippo.png)](./File:Salvatore_Sanfilippo.png)Salvatore Sanfilippo, the original developer of Redis (photo taken in 2015) 

The name *Redis* means Remote Dictionary Server.[[8]](./Redis#cite_note-RedisFAQ-8) The Redis project began when Salvatore Sanfilippo (nicknamed *antirez*) was trying to improve the scalability of his Italian startup and developed a [real-time](./Real-time_computing) web log analyzer. After encountering significant problems in scaling some types of workloads using traditional database systems, Sanfilippo began in 2009 to prototype a first proof of concept version of Redis in [Tcl](./Tcl_(programming_language)).[[16]](./Redis#cite_note-16) Later, Sanfilippo translated that prototype to the C language and implemented the first data type, the list. After a few weeks of using the project internally with success, Sanfilippo decided to open source it, announcing the project on [Hacker News](./Hacker_News). The project began to get traction, particularly among the Ruby community, with [GitHub](./GitHub) and [Instagram](./Instagram) being among the first companies adopting it.[[17]](./Redis#cite_note-17)[[18]](./Redis#cite_note-18)

 

Sanfilippo was hired by [VMware](./VMware) in March 2010.[[19]](./Redis#cite_note-19)[[20]](./Redis#cite_note-20)[[21]](./Redis#cite_note-21)

 

In May 2013, Redis was sponsored by [Pivotal Software](./Pivotal_Software) (a VMware spin-off).[[22]](./Redis#cite_note-22)

 

In June 2015, development became sponsored by [Redis Ltd.](./Redis_(company))[[23]](./Redis#cite_note-23)

 

In August 2018, to control usage of the software by [managed](./Managed_services) cloud providers without adequate compensation, Redis Ltd. announced that it would relicense the optional Redis modules from the [GNU Affero General Public License](./GNU_Affero_General_Public_License) (AGPL) to the [Apache License](./Apache_License), but subject to an addendum known as the "[Commons Clause](./Commons_Clause)" that restricts commercial usage. This made the modules source-available and no longer [free software](./Free_software). The core Redis software remained under a [BSD license](./BSD_licenses), with Redis Ltd. committing to maintaining these terms.[[15]](./Redis#cite_note-theregister.com-15)[[24]](./Redis#cite_note-24)[[25]](./Redis#cite_note-25)

 

In October 2018, Redis 5.0 was released, introducing Redis Stream – a new data structure that allows storage of multiple fields and string values with an automatic, time-based sequence at a single key.[[26]](./Redis#cite_note-redis.com-26)

 

In February 2019, citing confusion over the licensing terms, the Apache License with Commons Clause licensing terms for Redis modules was replaced with the "Redis Source Available License" (RSAL), which explicitly prohibits commercial use of the modules as part of "a database, a caching engine, a stream processing engine, a search engine, an indexing engine or an ML/DL/AI serving engine."[[27]](./Redis#cite_note-:12-27)[[28]](./Redis#cite_note-28) The last revision of the modules under a [free and open source](./Free_and_open-source_software) license were [forked](./Fork_(software_development)) by community members as the GoodFORM project.[[29]](./Redis#cite_note-:02-29)

 

In June 2020, Salvatore Sanfilippo stepped down as Redis' sole maintainer. Sanfilippo was succeeded by Yossi Gottlieb and Oran Agra.[[13]](./Redis#cite_note-theregister-13)[[30]](./Redis#cite_note-30)

 

In March 2024, Redis Ltd. announced that beginning with version 7.4, the core Redis software would be relicensed under the RSAL and [Server Side Public License](./Server_Side_Public_License) (SSPL), both of which are source-available and non-free.[[31]](./Redis#cite_note-31) The [Linux Foundation](./Linux_Foundation) subsequently announced that it would fork the last BSD-licensed version of Redis as [Valkey](./Valkey).[[32]](./Redis#cite_note-32) In May 2025, Redis Ltd. announced that it would change the license again to the AGPL beginning on version 8.0, citing that forks had achieved their goal of creating a "level playing field" of differentiated products, and that Redis has achieved "record growth" since the change in license.[[7]](./Redis#cite_note-agpl-7)

 

Sanfilippo returned to Redis in December 2024.[[33]](./Redis#cite_note-Register2025Redis-33)

 

## Differences from other database systems

 
|  | This sectionneeds additional citations forverification.Please helpimprove this articlebyadding citations to reliable sourcesin this section. Unsourced material may be challenged and removed.Find sources:"Redis"–news·newspapers·books·scholar·JSTOR(July 2025)(Learn how and when to remove this message) |
| --- | --- |

 

Redis is a system that functions as both a data store and a [cache](./Cache_(computing)). Data is modified and read from the main computer memory while also being persisted to disk in a format optimized for sequential access rather than random access. The formatted data is only reconstructed into memory once the system restarts.

 

Redis uses a data model that differs from [relational database management system](./Relational_database_management_system) (RDBMS). 
Commands specify operations on abstract data types rather than queries to be executed by a [database engine](./Database_engine). Data is stored in structures designed for direct retrieval. It does not rely on secondary indexes, aggregations, or other features common in traditional RDBMS. The Redis implementation uses the [fork](./Fork_(system_call)) [system call](./System_call) to duplicate the process holding the data. This allows the parent process to continue serving clients while the child process persists the in-memory data to disk.

 

## Features

 

Redis maps keys to types of values. Redis supports a number of data types including [Strings](./String_(computer_science)), [JavaScript Object Notation](./JSON) (JSON) documents, Hashes (a collection of fields, each field is a name-value string pair),[[34]](./Redis#cite_note-34) [lists](./List_(abstract_data_type)), [sets](./Set_(abstract_data_type)), vector sets,[[35]](./Redis#cite_note-35) and more.

 

The Redis Query Engine allows users to use Redis as a [document database](./Document_database), a [vector database](./Vector_database), a secondary index, and a search engine. With Redis Query Engine, users can define indexes for hash and JSON documents, and use a rich [query language](./Query_language) for vector search, full-text search, geospatial queries, and aggregations.[[36]](./Redis#cite_note-36)

 

Redis [Pub/Sub](./Publish–subscribe_pattern) (short for publish/subscribe) is a lightweight messaging capability. Publishers send messages to a channel, and subscribers receive messages from that channel.[[37]](./Redis#cite_note-37)

 

A Redis transaction allows the execution of a group of commands in a single step. A request sent by another client will never be served during the execution of a transaction. This guarantees that the commands are executed as a single isolated operation.[[38]](./Redis#cite_note-38)

 

Redis users can also upload and execute Lua scripts on the server.[[39]](./Redis#cite_note-39)

 

As of May 1, 2025, for all version of Redis starting with 8.0, all data types are included in the same package[[40]](./Redis#cite_note-40) and available under the Redis Source Available license v2.[[41]](./Redis#cite_note-41) Previously some data types were separate and therefore available under difference licenses.

 

## Persistence

 

Redis typically holds the whole dataset in memory. Versions up to 2.4 could be configured to use what they refer to as virtual memory[[42]](./Redis#cite_note-42) in which some of the dataset is stored on disk, but this feature is deprecated. [Persistence](./Persistence_(computer_science)) in Redis can be achieved through two different methods: snapshotting, where the dataset is asynchronously transferred from memory to disk at regular intervals as a binary dump, using the Redis RDB Dump File Format; or [journaling](./Transaction_log), where a record of each operation that modifies the dataset is added to an [append](./Append)-only file (AOF) in a background process. Redis can rewrite the append-only file in the background to avoid an indefinite growth of the journal. Journaling was introduced in version 1.1 and is generally considered the safer approach.

 

By default, Redis writes data to a file system at least every two seconds, with more or less robust options available if needed. In the case of a complete system failure on default settings, only a few seconds of data will be lost.

 

## Replication

 

Redis supports [master–replica replication](./Replication_(computing)). Data from any Redis server can replicate to any number of replicas. A replica may be a master to another replica. This allows Redis to implement a single-rooted replication tree. Redis replicas can be configured to accept writes, permitting intentional and unintentional inconsistency between instances. The [publish–subscribe](./Publish–subscribe_pattern) feature is fully implemented, so a client of a replica may subscribe to a channel and receive a full feed of messages published to the master, anywhere up the replication tree. Replication is useful for read (but not write) scalability or data redundancy.[[43]](./Redis#cite_note-43)

 

## Performance

 

When the [durability](./Durability_(database_systems)) of data is not needed, the in-memory nature of Redis allows it to perform well compared to database systems that write every change to disk before considering a transaction committed.[[8]](./Redis#cite_note-RedisFAQ-8) Redis operates as a single process and is single-threaded or double-threaded when it rewrites the AOF (append-only file).[[44]](./Redis#cite_note-44) Thus, a single Redis instance cannot use parallel execution of tasks such as [stored procedures](./Stored_procedure).

 

## Clustering

 

Redis introduced clustering in April 2015 with the release of version 3.0.[[45]](./Redis#cite_note-cluster-release-45) The [cluster](./Computer_cluster) specification implements a subset of Redis commands: all single-key commands are available, multi-key operations (commands related to unions and intersections) are restricted to keys belonging to the same node, and commands related to database selection operations are unavailable.[[46]](./Redis#cite_note-clustercommands-46) A Redis cluster can scale up to 1,000 nodes, achieve "acceptable" write safety and to continue operations when some nodes fail.[[47]](./Redis#cite_note-cluster-commands-47)[[48]](./Redis#cite_note-cluster-partitions-48)

 

## Users and use cases

 

Redis has been used by [Adobe](./Adobe_Inc.),[[49]](./Redis#cite_note-:6-49) [Airbnb](./Airbnb),[[50]](./Redis#cite_note-:3-50) [Amazon](./Amazon_(company)),[[51]](./Redis#cite_note-:8-51) [Hulu](./Hulu),[[52]](./Redis#cite_note-:7-52) [OpenAI](./OpenAI),[[53]](./Redis#cite_note-53) [Salesforce](./Salesforce),[[54]](./Redis#cite_note-54) [Shopify](./Shopify),[[55]](./Redis#cite_note-55) [Tinder](./Tinder_(app)),[[56]](./Redis#cite_note-:4-56) [Twitter](./Twitter),[[57]](./Redis#cite_note-:1-57)[[58]](./Redis#cite_note-:2-58) and [Yahoo](./Yahoo!_Inc._(2017–present)).[[59]](./Redis#cite_note-:5-59)

 

Typical use cases of Redis are session caching, full page cache, message queue applications, leaderboards and counting among others.[[60]](./Redis#cite_note-objectrocket-60) The publish–subscribe messaging paradigm allows real-time communication between servers.

 

[Amazon Web Services](./Amazon_Web_Services) offers a managed Redis service called [ElastiCache](./Amazon_ElastiCache) for Redis, [Google](./Google_Cloud_Platform) offers a managed Redis service called Cloud Memorystore,[[61]](./Redis#cite_note-61) [Microsoft](./Microsoft) offers Azure Cache for Redis in [Azure](./Microsoft_Azure),[[62]](./Redis#cite_note-Redis_Azure-62) and [Alibaba](./Alibaba_Group) offers ApsaraDB for Redis in [Alibaba Cloud](./Alibaba_Cloud).[[63]](./Redis#cite_note-Redis_AlibabaCloud-63)

 

## Library interfacing

 

Redis is interfaced with by various libraries. For example, [POCO C++ Libraries](./POCO_C++_Libraries) supports interfacing with Redis through its `Poco::Redis` library.[[64]](./Redis#cite_note-64)

 

## See also

 
- [Conflict-free replicated data type](./Conflict-free_replicated_data_type)
- [Memcached](./Memcached)
- [Infinispan](./Infinispan)
- [Valkey](./Valkey)

 

## References

  
1. [1](./Redis#cite_ref-creator1_1-0) [2](./Redis#cite_ref-creator1_1-1) Bernardi, Stefano (January 4, 2011). ["An interview with Salvatore Sanfilippo, creator of Redis, working out of Sicily"](http://www.eu-startups.com/2011/01/an-interview-with-salvatore-sanfilippo-creator-of-redis-working-out-of-sicily/). *EU-Startups*. Menlo Media.
2. [1](./Redis#cite_ref-creator2_2-0) [2](./Redis#cite_ref-creator2_2-1) Haber, Itamar (July 15, 2015). ["Salvatore Sanfilippo: Welcome to Redis Labs"](https://redis.com/blog/salvatore-sanfilippo-welcome-to-redis-labs). *Redis*.
3. [↑](./Redis#cite_ref-3) ["Page 7 of 7 - Redis - Google Code Archive - Long-term storage for Google Code Project Hosting"](https://code.google.com/archive/p/redis/downloads?page=7). *code.google.com*. Retrieved 22 March 2024.
4. [↑](./Redis#cite_ref-wikidata-c8c3a3f808c3e89b667ab67e4879f49ba1ecb126-v20_4-0) ["Release 8.8.0"](https://github.com/redis/redis/releases/tag/8.8.0). 25 May 2026. Retrieved 25 May 2026.
5. [↑](./Redis#cite_ref-5) ["Introduction to Redis"](https://redis.io/topics/introduction). Redis is written in ANSI C and works in most POSIX systems like Linux, *BSD, OS X without external dependencies.
6. [1](./Redis#cite_ref-github20240420_6-0) [2](./Redis#cite_ref-github20240420_6-1) ["LICENSE.txt"](https://github.com/redis/redis/blob/0b34396924eca4edc524469886dc5be6c77ec4ed/LICENSE.txt). *GitHub*. 20 March 2024.
7. [1](./Redis#cite_ref-agpl_7-0) [2](./Redis#cite_ref-agpl_7-1) [3](./Redis#cite_ref-agpl_7-2) ["Redis bets big on an open source return"](https://www.infoworld.com/article/3975620/redis-bets-big-on-an-open-source-return.html). *InfoWorld*. Retrieved 2025-05-01.
8. [1](./Redis#cite_ref-RedisFAQ_8-0) [2](./Redis#cite_ref-RedisFAQ_8-1) [3](./Redis#cite_ref-RedisFAQ_8-2) [4](./Redis#cite_ref-RedisFAQ_8-3) ["FAQ: Redis"](https://redis.io/topics/faq). *Redis.io*. Retrieved 12 February 2022.
9. [↑](./Redis#cite_ref-9) ["Google Groups"](https://groups.google.com/d/msg/redis-db/MtwjZC5gCeE/f-5T-OIcCW8J). *groups.google.com*. Retrieved 25 February 2022.
10. [↑](./Redis#cite_ref-:9_10-0) ["Redis"](https://redis.io/). *Redis*. Retrieved 2023-07-22.
11. [↑](./Redis#cite_ref-11) ["A conversation with Salvatore Sanfilippo, creator of the open-source database Redis"](https://venturebeat.com/2016/06/19/redis-creator/). *VentureBeat*. 2016-06-20. Retrieved 2021-06-29.
12. [↑](./Redis#cite_ref-network-world-201507_12-0) Kepes, Ben (July 15, 2015). ["Redis Labs hires the creator of Redis, Salvatore Sanfilippo"](https://www.networkworld.com/article/941072/redis-labs-hires-the-creator-of-redis-salvatore-sanfilippo.html). *Network World*. Retrieved August 30, 2015.
13. [1](./Redis#cite_ref-theregister_13-0) [2](./Redis#cite_ref-theregister_13-1) Francisco, Thomas Claburn in San. ["Database maestro Antirez says arrivederci to Redis: Seems he wants an unstructured life writing code, not a structured one managing software"](https://www.theregister.com/2020/06/30/redis_creator_antirez_quits/). *www.theregister.com*. Retrieved 2021-06-29.
14. [↑](./Redis#cite_ref-14) ["Database startup Redis Labs rebrands as ... just Redis"](https://siliconangle.com/2021/08/11/redis-labs-rebrands-redis/). *SiliconANGLE*. 2021-08-11. Retrieved 2021-08-11.
15. [1](./Redis#cite_ref-theregister.com_15-0) [2](./Redis#cite_ref-theregister.com_15-1) Claburn, Thomas. ["Redis has a license to kill: Open-source database maker takes some code proprietary"](https://www.theregister.com/2018/08/23/redis_database_license_change/). *The Register*. Retrieved 2024-03-21.
16. [↑](./Redis#cite_ref-16) Sanfilippo, Salvatore (April 28, 2017). ["Tcl prototype of Redis"](https://gist.github.com/antirez/6ca04dd191bdb82aad9fb241013e88a8). *GitHub Gist*. Retrieved October 8, 2018.
17. [↑](./Redis#cite_ref-17) Wanstrath, Chris (November 3, 2009). ["Introducing Resque"](https://blog.github.com/2009-11-03-introducing-resque/). *Blog*. Retrieved October 8, 2018.
18. [↑](./Redis#cite_ref-18) Krieger, Mike (October 31, 2011). ["Storing hundreds of millions of simple key-value pairs in Redis"](https://instagram-engineering.com/storing-hundreds-of-millions-of-simple-key-value-pairs-in-redis-1091ae80f74c). *Instagram Engineering Blog*. Retrieved October 8, 2018.
19. [↑](./Redis#cite_ref-19) Shapira, Gwen (March 17, 2010). ["VMware Hires Redis Key Developer – But Why?"](https://prodlife.wordpress.com/2010/03/17/vmware-hires-redis-key-developer-but-why/). *Blog*. Retrieved September 25, 2016.
20. [↑](./Redis#cite_ref-20) Sanfilippo, Salvatore (March 15, 2010). ["VMware: the new Redis home"](http://antirez.com/post/vmware-the-new-redis-home.html). *Blog*. Retrieved September 25, 2016.
21. [↑](./Redis#cite_ref-21) Collison, Derek (March 15, 2010). ["VMware: The Console: VMware hires key developer for Redis"](https://web.archive.org/web/20100322191425/http://blogs.vmware.com/console/2010/03/vmware-hires-key-developer-for-redis.html). *VMware Blog*. Archived from [the original](http://blogs.vmware.com/console/2010/03/vmware-hires-key-developer-for-redis.html) on March 22, 2010. Retrieved September 25, 2016.
22. [↑](./Redis#cite_ref-22) Sanfilippo, Salvatore. ["Redis Sponsors"](https://redis.io/topics/sponsors). *Redis.io*. Redis. Retrieved April 11, 2019.
23. [↑](./Redis#cite_ref-23) Sanfilippo, Salvatore (July 15, 2015). ["Thanks Pivotal, Hello Redis Labs"](http://antirez.com/news/91). *antirez.com*. Retrieved 2019-04-03.
24. [↑](./Redis#cite_ref-24) Baer, Tony (October 16, 2018). ["It's MongoDB's turn to change its open source license"](https://www.zdnet.com/article/its-mongodbs-turn-to-change-its-open-source-license/). *ZDNet*. Retrieved 2019-08-01.
25. [↑](./Redis#cite_ref-25) Shoolman, Yiftach (August 22, 2018). ["Redis' License is BSD and will remain BSD"](https://redis.io/blog/redis-license-bsd-will-remain-bsd/). *Redis.io*. Redis. Retrieved September 30, 2024.
26. [↑](./Redis#cite_ref-redis.com_26-0) ["Redis 5.0 is here!"](https://redis.com/blog/redis-5-0-is-here/). 22 October 2018.
27. [↑](./Redis#cite_ref-:12_27-0) Finley, Klint (July 31, 2019). ["When Open Source Software Comes With a Few Catches"](https://www.wired.com/story/when-open-source-software-comes-with-catches/). *Wired*. [ISSN](./ISSN_(identifier)) [1059-1028](https://search.worldcat.org/issn/1059-1028). Retrieved 2019-08-01.
28. [↑](./Redis#cite_ref-28) Vaughan-Nichols, Steven J. ["Redis Labs drops Commons Clause for a new license"](https://www.zdnet.com/article/redis-labs-drops-commons-clause-for-a-new-license/). *ZDNet*. Retrieved 2019-08-01.
29. [↑](./Redis#cite_ref-:02_29-0) Gilbertson, Scott (2019-10-16). ["In 2019, multiple open source companies changed course—is it the right move?"](https://arstechnica.com/information-technology/2019/10/is-the-software-world-taking-too-much-from-the-open-source-community/). *Ars Technica*. Retrieved 2019-10-16.
30. [↑](./Redis#cite_ref-30) ["The end of the Redis adventure -"](http://antirez.com/news/133). *antirez.com*. Retrieved 2020-11-10.
31. [↑](./Redis#cite_ref-31) ["Redis tightens its license terms, pleasing no one"](https://www.theregister.com/2024/03/22/redis_changes_license/). *The Register*. [Archived](https://web.archive.org/web/20250206143748/https://www.theregister.com/2024/03/22/redis_changes_license/) from the original on 2025-02-06. Retrieved 2025-05-01.
32. [↑](./Redis#cite_ref-32) ["Linux Foundation Launches Valkey As A Redis Fork"](https://www.phoronix.com/news/Linux-Foundation-Valkey). *Phoronix*. Retrieved 2025-05-01.
33. [↑](./Redis#cite_ref-Register2025Redis_33-0)  Clark, Lindsay (10 April 2025). ["Return of Redis creator bears fruit with vector set data type"](https://www.theregister.com/2025/04/10/return_of_redis_creator/). *The Register*. Retrieved 30 September 2025. 
34. [↑](./Redis#cite_ref-34) ["Redis hashes"](https://redis.io/docs/latest/develop/data-types/hashes/). *Docs*. Retrieved 2025-07-13.
35. [↑](./Redis#cite_ref-35) ["Redis vector sets"](https://redis.io/docs/latest/develop/data-types/vector-sets/). *Docs*. Retrieved 2025-07-13.
36. [↑](./Redis#cite_ref-36) ["Redis Query Engine"](https://redis.io/docs/latest/develop/ai/search-and-query/). *Docs*. Retrieved 2025-07-13.
37. [↑](./Redis#cite_ref-37) ["Redis Pub/sub"](https://redis.io/docs/latest/develop/pubsub/). *Docs*. Retrieved 2025-07-13.
38. [↑](./Redis#cite_ref-38) ["Transactions"](https://redis.io/docs/latest/develop/using-commands/transactions/). *Docs*. Retrieved 2025-07-13.
39. [↑](./Redis#cite_ref-39) ["Scripting with Lua"](https://redis.io/docs/latest/develop/programmability/eval-intro/). *Docs*. Retrieved 2025-07-13.
40. [↑](./Redis#cite_ref-40) ["Redis 8.0"](https://redis.io/docs/latest/develop/whats-new/8-0/). *Docs*. Retrieved 2025-07-13.
41. [↑](./Redis#cite_ref-41) Redis. ["Licenses"](https://redis.io/). *Redis*. Retrieved 2025-07-13.
42. [↑](./Redis#cite_ref-42) ["Virtual Memory"](https://redis.io/topics/virtual-memory). *Redis.io*. Retrieved April 11, 2019.
43. [↑](./Redis#cite_ref-43) ["Google Code Archive - Long-term storage for Google Code Project Hosting"](https://code.google.com/p/redis/wiki/ReplicationHowto). *code.google.com*.
44. [↑](./Redis#cite_ref-44) ["Redis on the Raspberry Pi: adventures in unaligned lands - antirez"](http://antirez.com/news/111). *antirez.com*.
45. [↑](./Redis#cite_ref-cluster-release_45-0) ["Redis 3.0 Release Notes"](https://github.com/antirez/redis/blob/3.0/00-RELEASENOTES). *[GitHub](./GitHub)*. Retrieved 2017-03-10.
46. [↑](./Redis#cite_ref-clustercommands_46-0) ["Cluster Spec"](https://redis.io/topics/cluster-spec#implemented-subset). Retrieved 2017-03-10.
47. [↑](./Redis#cite_ref-cluster-commands_47-0) ["Cluster Spec"](https://redis.io/topics/cluster-spec). Retrieved 2017-03-10.
48. [↑](./Redis#cite_ref-cluster-partitions_48-0) ["Cluster Tutorial"](https://redis.io/topics/cluster-tutorial). Retrieved 2017-03-10.
49. [↑](./Redis#cite_ref-:6_49-0) ["AWS re:Invent 2014 | (SDD402) Amazon ElastiCache Deep Dive"](https://www.youtube.com/watch?v=cEkHBqhQnog). *[YouTube](./YouTube)*. 17 November 2014. Retrieved 2023-07-22.
50. [↑](./Redis#cite_ref-:3_50-0) ["AWS re:Invent 2018: Airbnb's Journey from Self-Managed Redis to ElastiCache for Redis (DAT319)"](https://www.youtube.com/watch?v=eyd_8efUCwM). *[YouTube](./YouTube)*. 28 November 2018. Retrieved 2023-07-22.
51. [↑](./Redis#cite_ref-:8_51-0) ["Amazon GameOn Database Migration Case Study – Amazon Web Services (AWS)"](https://aws.amazon.com/solutions/case-studies/amazon-gameon/). *Amazon Web Services, Inc*. Retrieved 2023-07-22.
52. [↑](./Redis#cite_ref-:7_52-0) ["Hulu Case Study"](https://aws.amazon.com/solutions/case-studies/hulu/). *Amazon Web Services, Inc*. Retrieved 2023-07-22.
53. [↑](./Redis#cite_ref-53) ["Elevated API Errors"](https://status.openai.com/incidents/fk0tcbydtybr). *status.openai.com*. 19 October 2023. Retrieved 2023-10-28.
54. [↑](./Redis#cite_ref-54) ["Using Redis Hash Instead of Set to Reduce Cache Size and Operating Costs"](https://engineering.salesforce.com/using-redis-hash-instead-of-set-to-reduce-cache-size-and-operating-costs-2a1f7b847ded/). *Salesforce Engineering*. 25 February 2021. Retrieved 2025-09-30.
55. [↑](./Redis#cite_ref-55) ["Simplify: Batch + Cache Optimized Server-Side Storefront Rendering"](https://shopify.engineering/simplify-batch-cache-optimized-server-side-storefront-rendering). *Shopify Engineering*. 3 May 2023. Retrieved 2025-09-30.
56. [↑](./Redis#cite_ref-:4_56-0) ["Building resiliency at scale at Tinder with Amazon ElastiCache | AWS Database Blog"](https://aws.amazon.com/blogs/database/building-resiliency-at-scale-at-tinder-with-amazon-elasticache/). *aws.amazon.com*. 2020-01-30. Retrieved 2023-07-22.
57. [↑](./Redis#cite_ref-:1_57-0) ["Scaling Redis at Twitter"](https://www.youtube.com/watch?v=rP9EKvWt0zo). *[YouTube](./YouTube)*. 31 August 2014. Retrieved 2023-07-22.
58. [↑](./Redis#cite_ref-:2_58-0) ["Using Redis at Scale at Twitter - by Rashmi Ramesh of Twitter - RedisConf17 -"](https://www.youtube.com/watch?v=QznaOSk20nU). *[YouTube](./YouTube)*. 5 July 2017. Retrieved 2023-07-22.
59. [↑](./Redis#cite_ref-:5_59-0) ["AWS re:Invent 2022 - How Yahoo cost optimizes their in-memory workloads with AWS (DAT321)"](https://www.youtube.com/watch?v=jEwrcpq2mLM). *[YouTube](./YouTube)*. 2 December 2022. Retrieved 2023-07-22.
60. [↑](./Redis#cite_ref-objectrocket_60-0) ["Top 5 Redis use cases - ObjectRocket"](http://objectrocket.com/blog/how-to/top-5-redis-use-cases). *ObjectRocket*. Rackspace. 7 November 2017.
61. [↑](./Redis#cite_ref-61) ["Memorystore: in-memory data store"](https://cloud.google.com/memorystore). *Google Cloud*. Retrieved 2023-02-03.
62. [↑](./Redis#cite_ref-Redis_Azure_62-0) ["Azure Redis Cache - Redis cache cloud service - Microsoft Azure"](https://azure.microsoft.com/en-us/services/cache/). *azure.microsoft.com*.
63. [↑](./Redis#cite_ref-Redis_AlibabaCloud_63-0) ["ApsaraDB for Redis: A Key Value Database Service - Alibaba Cloud"](https://www.alibabacloud.com/product/apsaradb-for-redis). *www.alibabacloud.com*.
64. [↑](./Redis#cite_ref-64) ["Namespace Poco::Redis"](https://docs.pocoproject.org/current/Poco.Redis.html). *docs.pocoproject.org*. POCO Project. Retrieved 18 October 2025.

 

## Further reading

  
- Isabel Drost and Jan Lehnard (29 October 2009), [Happenings: NoSQL Conference, Berlin](http://www.h-online.com/open/features/Happenings-NoSQL-Conference-Berlin-843597.html), [The H](./The_H). [Slides](http://nosqlberlin.de/slides/NoSQLBerlin-Redis.pdf) for the Redis presentation. [Summary](http://www.paperplanes.de/2009/10/27/theres_something_about_redis.html).
- Billy Newport (IBM): "[Evolving the Key/Value Programming Model to a Higher Level](http://www.infoq.com/presentations/newport-evolving-key-value-programming-model)" Qcon Conference 2009 San Francisco.
- A Mishra: "[Install and configure Redis on Centos/ Fedora server](http://blog.andolasoft.com/2013/07/how-to-install-and-configure-redis-server-on-centosfedora-server.html)".
- E. Mouzakitis: "[Monitoring Redis Performance](https://www.datadoghq.com/blog/how-to-monitor-redis-performance-metrics/)"

 

## External links

 
- [Official website](https://redis.io)
- [Valkey: Ongoing development home of the original BSD-licensed Redis software](https://github.com/valkey-io/valkey)

 
| Authority control databases | GND |
| --- | --- |