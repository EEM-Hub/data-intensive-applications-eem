---
source: https://en.wikipedia.org/wiki/Apache_Kafka
fetched: 2026-06-19
---

Software bus for high-volume data feeds 
|  | This article has multiple issues.Please helpimprove itor discuss these issues on thetalk page.(Learn how and when to remove these messages)This articlecontainsinstructions or advice.Wikipedia is not a guidebook; please helprewrite such contentto be encyclopedic or move it toWikiversity,Wikibooks, orWikivoyage.(November 2023)This articlemay rely excessively on sourcestoo closely associated with the subject, potentially preventing the article from beingverifiableandneutral.Please helpimprove itby replacing them with more appropriatecitationstoreliable, independent sources.(November 2023)(Learn how and when to remove this message)(Learn how and when to remove this message) |  | This articlecontainsinstructions or advice.Wikipedia is not a guidebook; please helprewrite such contentto be encyclopedic or move it toWikiversity,Wikibooks, orWikivoyage.(November 2023) |  | This articlemay rely excessively on sourcestoo closely associated with the subject, potentially preventing the article from beingverifiableandneutral.Please helpimprove itby replacing them with more appropriatecitationstoreliable, independent sources.(November 2023)(Learn how and when to remove this message) |
| --- | --- | --- | --- | --- | --- |
|  | This articlecontainsinstructions or advice.Wikipedia is not a guidebook; please helprewrite such contentto be encyclopedic or move it toWikiversity,Wikibooks, orWikivoyage.(November 2023) |
|  | This articlemay rely excessively on sourcestoo closely associated with the subject, potentially preventing the article from beingverifiableandneutral.Please helpimprove itby replacing them with more appropriatecitationstoreliable, independent sources.(November 2023)(Learn how and when to remove this message) |

 
| Apache Kafka[1] |
| --- |
|  |
| Original author | LinkedIn |
| Developer | Apache Software Foundation |
| Release | January2011;15years ago(2011-01)[2] |
|  |
| Stable release | 4.3.0[3]/ 20 May 2026 |
|  |
| Written in | Scala,Java |
| Operating system | Cross-platform |
| Type | Stream processing,Message broker |
| License | Apache License 2.0 |
| Website | kafka.apache.org |
| Repository | github.com/apache/kafka |

  

**Apache Kafka** is a [distributed](./Distributed_computing) [event store](./Event_store) and [stream-processing](./Stream_processing) platform. It is an [open-source](./Open-source_software) system developed by the [Apache Software Foundation](./Apache_Software_Foundation) written in [Java](./Java_(programming_language)) and [Scala](./Scala_(programming_language)). The project aims to provide a unified, high-throughput, low-latency platform for handling real-time data feeds. Kafka can connect to external systems (for data import/export) via Kafka Connect, and provides the Kafka Streams [libraries](./Library_(computing)) for stream processing applications. Kafka uses a binary [TCP](./Transmission_Control_Protocol)-based protocol that is optimized for efficiency and relies on a "message set" abstraction that naturally groups messages together to reduce the overhead of the network roundtrip. This "leads to larger network packets, larger sequential disk operations, contiguous memory blocks [...] which allows Kafka to turn a bursty stream of random message writes into linear writes."[[4]](./Apache_Kafka#cite_note-4)

 

## History

 

Kafka was originally developed at [LinkedIn](./LinkedIn), and was subsequently open sourced in early 2011. Jay Kreps, [Neha Narkhede](./Neha_Narkhede) and Jun Rao helped co-create Kafka.[[5]](./Apache_Kafka#cite_note-ForbesKreps-5) Graduation from the Apache Incubator occurred on 23 October 2012.[[6]](./Apache_Kafka#cite_note-6)  Jay Kreps chose to name the software after the author [Franz Kafka](./Franz_Kafka) because it is "a system optimized for writing", and he liked Kafka's work.[[7]](./Apache_Kafka#cite_note-7)

 

## Operation

 

Apache Kafka is a distributed log-based messaging system that guarantees ordering within individual partitions rather than across the entire topic. Unlike queue-based systems, Kafka retains messages in a durable, append-only log, allowing multiple consumers to read at different offsets. Kafka uses manual offset management, giving consumers control over retries and failure handling. If a consumer fails to process a message, it can delay committing the offset, preventing further progress in that partition while other partitions remain unaffected. This partition-based design enables fault isolation and parallel processing while allowing ordering to be maintained within partitions, depending on consumer handling.[[8]](./Apache_Kafka#cite_note-8)[*[page needed](./Wikipedia:Citing_sources)*]

 

In 2025, Apache Kafka introduced "Queues for Kafka",[[9]](./Apache_Kafka#cite_note-9) adding share groups as an alternative to consumer groups. This feature enables queue-like semantics where consumers can cooperatively process records from the same partitions, with individual message acknowledgment and delivery tracking. Unlike traditional consumer groups where partitions are exclusively assigned, share groups allow the number of consumers to exceed partition count, making it ideal for work-queue patterns while maintaining Kafka's durability and scalability benefits. This development addresses the common challenge of "over-partitioning" that many Kafka users face.[*[citation needed](./Wikipedia:Citation_needed)*]

 

## Kafka APIs

 

### Connect API

 
|  | This sectionneeds additional citations forverification.Please helpimprove this articlebyadding citations to reliable sourcesin this section. Unsourced material may be challenged and removed.(May 2025)(Learn how and when to remove this message) |
| --- | --- |

 

Kafka Connect (or Connect API) is a framework to import/export data from/to other systems.[[10]](./Apache_Kafka#cite_note-10) It was added in the Kafka 0.9.0.0 release and uses the Producer and Consumer API internally. The Connect framework itself executes so-called "connectors" that implement the actual logic to read/write data from other systems.[*[citation needed](./Wikipedia:Citation_needed)*]

 

### Streams API

 

Kafka Streams (or Streams API) is a stream-processing library written in Java. It was added in the Kafka 0.10.0.0 release. The library allows for the development of stateful stream-processing applications that are scalable, elastic, and fully fault-tolerant. The main API is a stream-processing [domain-specific language](./Domain-specific_language) (DSL) that offers high-level operators like filter, [map](./Map_(higher-order_function)), grouping, windowing, aggregation, joins, and the notion of tables. Additionally, the Processor API can be used to implement custom operators for a more low-level development approach. The DSL and Processor API can be mixed, too. For stateful stream processing, Kafka Streams uses [RocksDB](./RocksDB) to maintain local operator state. Because RocksDB can write to disk, the maintained state can be larger than available main memory. For fault-tolerance, all updates to local state stores are also written into a topic in the Kafka cluster. This allows recreating state by reading those topics and feed all data into RocksDB.[[11]](./Apache_Kafka#cite_note-11)

 

## See also

 
- ![](//upload.wikimedia.org/wikipedia/commons/thumb/3/31/Free_and_open-source_software_logo_%282009%29.svg/40px-Free_and_open-source_software_logo_%282009%29.svg.png)[Free and open-source software portal](./Portal:Free_and_open-source_software)

 
- [RabbitMQ](./RabbitMQ)
- [Redis](./Redis)
- [NATS](./NATS_Messaging)
- [Apache Flink](./Apache_Flink)
- [Apache Samza](./Apache_Samza)
- [Apache Spark Streaming](./Apache_Spark)
- [Data Distribution Service](./Data_Distribution_Service)
- [Enterprise Integration Patterns](./Enterprise_Integration_Patterns)
- [Enterprise messaging system](./Enterprise_messaging_system)
- [Streaming analytics](./Event_stream_processing)
- [Event-driven SOA](./Event-driven_SOA)
- [Hortonworks DataFlow](./Hortonworks_DataFlow)
- [Message-oriented middleware](./Message-oriented_middleware)
- [Service-oriented architecture](./Service-oriented_architecture)

 

## References

 
1. [↑](./Apache_Kafka#cite_ref-1) ["Apache Kafka at GitHub"](https://github.com/apache/kafka). *github.com*. [Archived](https://web.archive.org/web/20230116213842/https://github.com/apache/kafka) from the original on 16 January 2023. Retrieved 5 March 2018.
2. [↑](./Apache_Kafka#cite_ref-2) ["Open-sourcing Kafka, LinkedIn's distributed message queue"](https://blog.linkedin.com/2011/01/11/open-source-linkedin-kafka). [Archived](https://web.archive.org/web/20221226020822/https://blog.linkedin.com/2011/01/11/open-source-linkedin-kafka/) from the original on 26 December 2022. Retrieved 27 October 2016.
3. [↑](./Apache_Kafka#cite_ref-wikidata-bb6b4fefd007ee2530da38dd14eb40d76bc70dbb-v20_3-0) ["Release 4.3.0"](https://github.com/apache/kafka/releases/tag/4.3.0). 20 May 2026. Retrieved 22 May 2026.
4. [↑](./Apache_Kafka#cite_ref-4) ["Efficiency"](https://kafka.apache.org/documentation/#maximizingefficiency). *kafka.apache.org*. Retrieved 2019-09-19.
5. [↑](./Apache_Kafka#cite_ref-ForbesKreps_5-0) Li, Steven. ["He Left His High-Paying Job At LinkedIn And Then Built A $4.5 Billion Business In A Niche You've Never Heard Of"](https://www.forbes.com/sites/stevenli1/2020/05/11/confluent-jay-kreps-kafka-4-billion-2020/?sh=1a82e619709d). *Forbes*. Retrieved 2025-12-02.
6. [↑](./Apache_Kafka#cite_ref-6) ["Apache Incubator: Kafka Incubation Status"](https://incubator.apache.org/projects/kafka.html). [Archived](https://web.archive.org/web/20221017081525/https://incubator.apache.org/projects/kafka.html) from the original on 2022-10-17. Retrieved 2022-10-17.
7. [↑](./Apache_Kafka#cite_ref-7) Narkhede, Neha; Shapira, Gwen; Palino, Todd (2017). "Chapter 1". [*Kafka: The Definitive Guide*](https://books.google.com/books?id=dXwzDwAAQBAJ). O'Reilly. [ISBN](./ISBN_(identifier)) [978-1-4919-3611-5](./Special:BookSources/978-1-4919-3611-5). People often ask how Kafka got its name and if it has anything to do with the application itself. Jay Kreps offered the following insight: "I thought that since Kafka was a system optimized for writing using, a writer's name would make sense. I had taken a lot of lit classes in college and liked Franz Kafka."
8. [↑](./Apache_Kafka#cite_ref-8) Narkhede, Neha; Shapira, Gwen; Palino, Todd (2017). *Kafka: the definitive guide: real-time data and stream processing at scale*. Sebastopol, CA: O'Reilly Media. [ISBN](./ISBN_(identifier)) [978-1-4919-3616-0](./Special:BookSources/978-1-4919-3616-0). [OCLC](./OCLC_(identifier)) [933521388](https://search.worldcat.org/oclc/933521388).
9. [↑](./Apache_Kafka#cite_ref-9) ["KIP-932: Queues for Kafka - Apache Kafka - Apache Software Foundation"](https://cwiki.apache.org/confluence/display/KAFKA/KIP-932:+Queues+for+Kafka). *cwiki.apache.org*. Retrieved 2025-12-02.
10. [↑](./Apache_Kafka#cite_ref-10) ["Apache Kafka Documentation: Kafka Connect"](https://kafka.apache.org/documentation/#connect). *Apache*.
11. [↑](./Apache_Kafka#cite_ref-11) ["Kafka Connect – Import Export for Apache Kafka"](https://softwaremill.com/import-export-through-kafka-connectors/). *SoftwareMill*. Retrieved 2025-05-08.

 

## External links

 
- [Official website](https://kafka.apache.org/) [![Edit this at Wikidata](//upload.wikimedia.org/wikipedia/en/thumb/8/8a/OOjs_UI_icon_edit-ltr-progressive.svg/20px-OOjs_UI_icon_edit-ltr-progressive.svg.png)](https://www.wikidata.org/wiki/Q16235208#P856)

 
| vteThe Apache Software Foundation |
| --- |
| Top-levelprojects | AccumuloActiveMQAiravataAirflowAlluraAmbariAntAriesArrowApache HTTP ServerAPRAvroAxisAxis2BeamBloodhoundBrooklynCalciteCamelCarbonDataCassandraCayenneCloudStackCordovaCouchDBcTAKESCXFDerbyDirectoryDrillDruidEmpire-dbFelixFlexFlinkFlumeFreeMarkerGeronimoGroovyGuacamoleGumpHadoopHBaseHelixHiveIcebergIgniteImpalaJackrabbitJamesJenaJMeterKafkaKuduKylinLuceneMahoutMavenMINAmod_perlMyFacesMynewtNiFiNetBeansNutchNuttXOFBizOozieOpenEJBOpenJPAOpenNLPOрenOfficeORCPDFBoxParquetPhoenixPOIPigPinotPivotQpidRollerRocketMQSamzaShiroSINGASlingSolrSparkStormSpamAssassinStruts1SubversionSupersetSystemDSTapestryThriftTikaTinkerPopTomcatTrafodionTraffic ServerUIMAVelocityWicketXalanXercesXMLBeansYetusZooKeeper |
| Commons | BCELBSFDaemonJellyLogging |
| Incubator | Taverna |
| Other projects | BatikFOPIvyLog4j |
| Attic | ApexAxKitBeehiveiBATISClickCocoonContinuumDeltacloudEtchGiraphHamaHarmonyJakartaMarmottaMXNetODERiverShaleSlideSqoopStanbolTuscanyWaveXML |
| Licenses | Apache License |
| Category |

 
| vteMessage-oriented middleware |
| --- |
| Apache ActiveMQApache CamelApache KafkaApache QpidOpen Message QueueRabbitMQZeroMQmore... |

 
| Authority control databases: National | FranceBnF data |
| --- | --- |