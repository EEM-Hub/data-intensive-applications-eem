---
source: https://en.wikipedia.org/wiki/Apache_HBase
fetched: 2026-06-19
---

Open-source distributed database 

 
| Apache HBase |
| --- |
|  |
| Original author | Powerset |
| Developer | Apache Software Foundation |
| Release | 28March 2008;18 years ago(2008-03-28) |
|  |
| Stable release | 2.5.x2.5.13 / 14November 2025;7 months ago(2025-11-14)[1]2.6.x2.6.4 / 14November 2025;7 months ago(2025-11-14)[1] | 2.5.x | 2.5.13 / 14November 2025;7 months ago(2025-11-14)[1] | 2.6.x | 2.6.4 / 14November 2025;7 months ago(2025-11-14)[1] |
| 2.5.x | 2.5.13 / 14November 2025;7 months ago(2025-11-14)[1] |
| 2.6.x | 2.6.4 / 14November 2025;7 months ago(2025-11-14)[1] |
| Preview release | 3.0.0-beta-1
   / 14January 2024;2 years ago(2024-01-14)[1] |
|  |
| Written in | Java |
| Operating system | Cross-platform |
| Type | Distributed database |
| License | Apache License 2.0 |
| Website | hbase.apache.org |
| Repository | GitHub Repository,Gitbox Repository |

  

**HBase** is an [open-source](./Open-source_software) [non-relational](./Non-relational_database) [distributed database](./Distributed_database) modeled after [Google's](./Google) [Bigtable](./Bigtable) and written in [Java](./Java_(programming_language)). It is developed as part of [Apache Software Foundation](./Apache_Software_Foundation)'s [Apache Hadoop](./Hadoop) project and runs on top of [HDFS (Hadoop Distributed File System)](./Hadoop_Distributed_File_System) or [Alluxio](./Alluxio), providing Bigtable-like capabilities for Hadoop. That is, it provides a [fault-tolerant](./Fault-tolerant) way of storing large quantities of [sparse](./Sparse_file) data (small amounts of information caught within a large collection of empty or unimportant data, such as finding the 50 largest items in a group of 2 billion records, or finding the non-zero items representing less than 0.1% of a huge collection).

 

HBase features compression, in-memory operation, and [Bloom filters](./Bloom_filter) on a per-column basis as outlined in the original Bigtable paper.[[2]](./Apache_HBase#cite_note-2) Tables in HBase can serve as the input and output for [MapReduce](./Mapreduce) jobs run in Hadoop, and may be accessed through the Java API but also through [REST](./REST), [Avro](./Avro_(serialization_system)) or [Thrift](./Thrift_(protocol)) gateway APIs. HBase is a [wide-column store](./Wide-column_store) and has been widely adopted because of its lineage with Hadoop and HDFS. HBase runs on top of HDFS and is well-suited for fast read and write operations on large datasets with high throughput and low input/output latency.

 

HBase is not a direct replacement for a classic [SQL](./SQL) [database](./Database), however [Apache Phoenix](./Apache_Phoenix) project provides a SQL layer for HBase as well as [JDBC](./JDBC) driver that can be integrated with various [analytics](./Analytics) and [business intelligence](./Business_intelligence) applications.  The [Apache Trafodion](./Apache_Trafodion) project provides a SQL query engine with [ODBC](./ODBC) and [JDBC](./JDBC) drivers and [distributed ACID transaction protection](./ACID#Distributed_transactions) across multiple statements, tables and rows that use HBase as a storage engine.

 

HBase is now serving several data-driven websites[[3]](./Apache_HBase#cite_note-3) but [Facebook](./Facebook)'s Messaging Platform migrated from HBase to [MyRocks](./MyRocks) in 2018.[[4]](./Apache_HBase#cite_note-the-underlying-technology-of-messages-4)[[5]](./Apache_HBase#cite_note-theregister-5) Unlike relational and traditional databases, HBase does not support SQL scripting; instead the equivalent is written in Java, employing similarity with a MapReduce application.

 

In the parlance of Eric Brewer's [CAP Theorem](./CAP_Theorem), HBase is a CP type system.[[6]](./Apache_HBase#cite_note-adabi-6)

 

## History

 

Apache HBase began as a project by the company [Powerset](./Powerset_(company)) out of a need to process massive amounts of data for the purposes of [natural-language search](./Natural-language_user_interface). Since 2010 it is a top-level Apache project.

 

[Facebook](./Facebook) elected to implement its new messaging platform using HBase in November 2010, but migrated away from HBase in 2018.[[4]](./Apache_HBase#cite_note-the-underlying-technology-of-messages-4)

 

The 2.5.x series is the current stable release line, it supersedes earlier release lines.

 

## Use cases & production deployments

 

### Enterprises that use HBase

 

The following is a list of notable enterprises that have used or are using HBase:

  
- [23andMe](./23andMe)
- [Adobe](./Adobe_Systems)
- [Airbnb](./Airbnb) uses HBase as part of its AirStream realtime stream computation framework[[7]](./Apache_HBase#cite_note-7)
- [Alibaba Group](./Alibaba_Group)
- [Amadeus IT Group](./Amadeus_IT_Group), as its main long-term storage DB.
- [Bloomberg](./Bloomberg_L.P.), for time series data storage
- [Facebook](./Facebook) used HBase for its messaging platform between 2010 and 2018
- [Flipkart](./Flipkart) uses HBase for its search index[[8]](./Apache_HBase#cite_note-8) and user insights.[[9]](./Apache_HBase#cite_note-9)
- [Flurry](./Flurry_(company))
- [HubSpot](./HubSpot)
- [Imgur](./Imgur) uses HBase to power its notifications system[[10]](./Apache_HBase#cite_note-10)[[11]](./Apache_HBase#cite_note-11)
- [Kakao](./Kakao),[[12]](./Apache_HBase#cite_note-12) operator of [KakaoTalk](./KakaoTalk)
- [LY](./LY_Corporation),[[13]](./Apache_HBase#cite_note-13) operator of [Line](./Line_(software))
- [Netflix](./Netflix)[[14]](./Apache_HBase#cite_note-14)
- [Pinterest](./Pinterest)[[15]](./Apache_HBase#cite_note-15)
- [Quicken Loans](./Quicken_Loans)
- [Rocket Fuel](./Rocket_Fuel_Inc.)
- [Salesforce.com](./Salesforce.com)[[16]](./Apache_HBase#cite_note-16)
- [Sears](./Sears)
- [Sophos](./Sophos), for some of their back-end systems.
- [Spotify](./Spotify) uses HBase as base for Hadoop and machine learning jobs.[[17]](./Apache_HBase#cite_note-17)
- [Twitter](./Twitter)
- [Tuenti](./Tuenti) uses HBase for its messaging platform.[[18]](./Apache_HBase#cite_note-18)[[19]](./Apache_HBase#cite_note-19)
- [Xiaomi](./Xiaomi)
- [Yahoo!](./Yahoo!)

  

## See also

 
- ![](//upload.wikimedia.org/wikipedia/commons/thumb/3/31/Free_and_open-source_software_logo_%282009%29.svg/40px-Free_and_open-source_software_logo_%282009%29.svg.png)[Free and open-source software portal](./Portal:Free_and_open-source_software)
- [![icon](//upload.wikimedia.org/wikipedia/commons/thumb/6/6f/Octicons-terminal.svg/40px-Octicons-terminal.svg.png)](./File:Octicons-terminal.svg)[Computer programming portal](./Portal:Computer_programming)

 
- [NoSQL](./NoSQL)
- [Wide column store](./Wide_column_store)
- [Bigtable](./Bigtable)
- [Apache Cassandra](./Apache_Cassandra)
- [Oracle NOSQL](./Oracle_NoSQL_Database)
- [Hypertable](./Hypertable)
- [Apache Accumulo](./Apache_Accumulo)
- [MongoDB](./MongoDB)
- [Project Voldemort](./Project_Voldemort)
- [Riak](./Riak)
- [Sqoop](./Sqoop)
- [Elasticsearch](./Elasticsearch)
- [Apache Phoenix](./Apache_Phoenix)

 

## References

  
1. [1](./Apache_HBase#cite_ref-releases_1-0) [2](./Apache_HBase#cite_ref-releases_1-1) [3](./Apache_HBase#cite_ref-releases_1-2) ["Apache HBase – Apache HBase Downloads"](https://hbase.apache.org/downloads.html). Retrieved 12 January 2025.
2. [↑](./Apache_HBase#cite_ref-2) [Chang, et al. (2006). Bigtable: A Distributed Storage System for Structured Data](https://db.usenix.org//events/osdi06/tech/chang/chang_html/)
3. [↑](./Apache_HBase#cite_ref-3) ["Apache HBase – Powered By Apache HBase"](https://hbase.apache.org/poweredbyhbase.html). *hbase.apache.org*. Retrieved 8 April 2018.
4. [1](./Apache_HBase#cite_ref-the-underlying-technology-of-messages_4-0) [2](./Apache_HBase#cite_ref-the-underlying-technology-of-messages_4-1) ["Migrating Messenger storage to optimize performance"](https://code.fb.com/data-infrastructure/migrating-messenger-storage-to-optimize-performance/). *www.facebook.com*. 26 June 2018. Retrieved 5 July 2018.
5. [↑](./Apache_HBase#cite_ref-theregister_5-0) [Facebook: Why our 'next-gen' comms ditched MySQL](https://www.theregister.co.uk/2010/12/17/facebook_messages_tech/) Retrieved: 17 December 2010
6. [↑](./Apache_HBase#cite_ref-adabi_6-0) ["Consistency Tradeoffs in Modern Distributed Database System Design"](https://www.cs.umd.edu/~abadi/papers/abadi-pacelc.pdf) (PDF). February 2012. Retrieved 23 October 2024.
7. [↑](./Apache_HBase#cite_ref-7) HBaseCon (2 August 2016). ["Apache HBase at Airbnb"](https://www.slideshare.net/HBaseCon/apache-hbase-at-airbnb). *slideshare.net*. Retrieved 8 April 2018.
8. [↑](./Apache_HBase#cite_ref-8) ["Near Real Time Search Indexing"](https://link.medium.com/eVl4l3XRTvb). 4 January 2018.
9. [↑](./Apache_HBase#cite_ref-9) ["Is data locality always out of the box in Hadoop?"](https://link.medium.com/72m6gLvSTvb). 10 March 2018.
10. [↑](./Apache_HBase#cite_ref-10) ["Why Imgur Dropped MySQL in Favor of HBase - DZone Database"](https://dzone.com/articles/why-imgur-dropped-mysql-in-favor-of-hbase). *dzone.com*. Retrieved 8 April 2018.
11. [↑](./Apache_HBase#cite_ref-11) ["Tech Tuesday: Imgur Notifications: From MySQL to HBase - The Imgur Blog"](http://blog.imgur.com/2015/09/15/tech-tuesday-imgur-notifications-from-mysql-to-hbase/). *blog.imgur.com*. Retrieved 8 April 2018.
12. [↑](./Apache_HBase#cite_ref-12) Doyung Yoon. ["S2Graph : A Large-Scale Graph Database with HBase"](http://apachebigdata2015.sched.org/event/de6abfbd8f0b9e66b1c03feb2b9e2078?iframe=yes&w=i:100;&sidebar=yes&bg=no).
13. [↑](./Apache_HBase#cite_ref-13) Esen Sagynov (2012). ["The Story behind Line App Development"](https://web.archive.org/web/20130816105751/http://www.cubrid.org/blog/dev-platform/the-story-behind-line-app-development/). *CUBRID.org*. Archived from [the original](http://www.cubrid.org/blog/dev-platform/the-story-behind-line-app-development/) on 16 August 2013. Retrieved 8 July 2013.
14. [↑](./Apache_HBase#cite_ref-14) Cheolsoo Park and Ashwin Shankar. ["Netflix: Integrating Spark at Petabyte Scale"](https://apachebigdata2015.sched.com/event/3ztw/netflix-integrating-spark-at-petabyte-scale-cheolsoo-park-netflix-and-ashwin-shankar-netflix).
15. [↑](./Apache_HBase#cite_ref-15) ["Improving HBase backup efficiency at Pinterest"](https://medium.com/pinterest-engineering/improving-hbase-backup-efficiency-at-pinterest-86159da4b954). *Medium*. 30 March 2018. Retrieved 14 April 2020.
16. [↑](./Apache_HBase#cite_ref-16) ["Hbase at Salesforce.com"](https://www.slideshare.net/salesforceeng/hbase-at-salesforcecom).
17. [↑](./Apache_HBase#cite_ref-17) Josh Baer. ["How Apache Drives Spotify's Music Recommendations"](http://apachebigdata2015.sched.org/event/2a65daf0baa4cfbc227a8cb74a9103a2?iframe=no&w=i:100;&sidebar=yes&bg=no).
18. [↑](./Apache_HBase#cite_ref-18) ["Tuenti Group Chat: Simple, yet complex"](https://web.archive.org/web/20121124132459/http://corporate.tuenti.com/en/dev/blog/tuenti-group-chat-simple-yet-complex). Archived from [the original](http://corporate.tuenti.com/en/dev/blog/tuenti-group-chat-simple-yet-complex) on 24 November 2012. Retrieved 29 September 2015.
19. [↑](./Apache_HBase#cite_ref-19) ["Tuenti Asyncthrift"](https://github.com/tuenti/asyncthrift). *[GitHub](./GitHub)*. 6 November 2013.

 

## Bibliography

  
- Dimiduk, Nick; Khurana, Amandeep (28 November 2012). *HBase in Action* (1st ed.). [Manning Publications](./Manning_Publications). p. 350. [ISBN](./ISBN_(identifier)) [978-1617290527](./Special:BookSources/978-1617290527).
- George, Lars (20 September 2011). [*HBase: The Definitive Guide*](https://shop.oreilly.com/product/0636920014348.do) (1st ed.). [O'Reilly Media](./O'Reilly_Media). p. 556. [ISBN](./ISBN_(identifier)) [978-1449396107](./Special:BookSources/978-1449396107).
- Jiang, Yifeng (16 August 2012). [*HBase Administration Cookbook*](http://www.packtpub.com/hbase-administration-for-optimum-database-performance-cookbook/book) (1st ed.). [Packt Publishing](./Packt_Publishing). p. 332. [ISBN](./ISBN_(identifier)) [978-1849517140](./Special:BookSources/978-1849517140).

  

## External links

 
- [Official Apache HBase homepage](https://hbase.apache.org/)

 
| vteThe Apache Software Foundation |
| --- |
| Top-levelprojects | AccumuloActiveMQAiravataAirflowAlluraAmbariAntAriesArrowApache HTTP ServerAPRAvroAxisAxis2BeamBloodhoundBrooklynCalciteCamelCarbonDataCassandraCayenneCloudStackCordovaCouchDBcTAKESCXFDerbyDirectoryDrillDruidEmpire-dbFelixFlexFlinkFlumeFreeMarkerGeronimoGroovyGuacamoleGumpHadoopHBaseHelixHiveIcebergIgniteImpalaJackrabbitJamesJenaJMeterKafkaKuduKylinLuceneMahoutMavenMINAmod_perlMyFacesMynewtNiFiNetBeansNutchNuttXOFBizOozieOpenEJBOpenJPAOpenNLPOрenOfficeORCPDFBoxParquetPhoenixPOIPigPinotPivotQpidRollerRocketMQSamzaShiroSINGASlingSolrSparkStormSpamAssassinStruts1SubversionSupersetSystemDSTapestryThriftTikaTinkerPopTomcatTrafodionTraffic ServerUIMAVelocityWicketXalanXercesXMLBeansYetusZooKeeper |
| Commons | BCELBSFDaemonJellyLogging |
| Incubator | Taverna |
| Other projects | BatikFOPIvyLog4j |
| Attic | ApexAxKitBeehiveiBATISClickCocoonContinuumDeltacloudEtchGiraphHamaHarmonyJakartaMarmottaMXNetODERiverShaleSlideSqoopStanbolTuscanyWaveXML |
| Licenses | Apache License |
| Category |

 
| Authority control databases: National | Czech Republic |
| --- | --- |