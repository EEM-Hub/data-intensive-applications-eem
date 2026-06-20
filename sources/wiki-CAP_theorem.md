---
source: https://en.wikipedia.org/wiki/CAP_theorem
fetched: 2026-06-19
---

Need to sacrifice consistency or availability in the presence of network partitions 

In [database theory](./Database_theory), the **CAP theorem**, also named **Brewer's theorem** after computer scientist [Eric Brewer](./Eric_Brewer_(scientist)), states that any [distributed data store](./Distributed_data_store) can provide at most [two of the following three](./Inconsistent_triad) guarantees:[[1]](./CAP_theorem#cite_note-Gilbert_Lynch-1)[[2]](./CAP_theorem#cite_note-2)[[3]](./CAP_theorem#cite_note-3)

 [Consistency](./Consistency_model)Every read receives the most recent write or an error. Consistency means that all clients see the same data at the same time, no matter which node they connect to. For this to happen, whenever data is written to one node, it must be instantly forwarded or [replicated](./Replication_(computing)) to all the other nodes in the system before the write is deemed ‘successful’[[4]](./CAP_theorem#cite_note-:1-4). Consistency as defined in the CAP theorem is quite different from the consistency guaranteed in [ACID](./ACID) [database transactions](./Database_transaction).[[5]](./CAP_theorem#cite_note-5) [Availability](./Availability)Every request received by a non-failing node in the system must result in a response, without the guarantee that it contains the most recent version of the data[[6]](./CAP_theorem#cite_note-:3-6). This is the definition of availability in CAP theorem as defined by Gilbert and Lynch.[[1]](./CAP_theorem#cite_note-Gilbert_Lynch-1)  Availability as defined in CAP theorem is different from [high availability](./High_availability) in software architecture.[[7]](./CAP_theorem#cite_note-Fowler_2015-7) [Partition tolerance](./Network_partitioning)The system continues to operate despite an arbitrary number of messages being dropped (or delayed) by the network between nodes.[[8]](./CAP_theorem#cite_note-8) 

When a [network partition](./Network_partition) failure happens, it must be decided whether to do one of the following:

 
- cancel the operation and thus decrease the availability but ensure consistency
- proceed with the operation and thus provide availability but risk inconsistency.  This does not necessarily mean that system is [highly available](./High_availability) to its users.[[7]](./CAP_theorem#cite_note-Fowler_2015-7)

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/9/98/CAP_Theorem_Euler_Diagram.png/250px-CAP_Theorem_Euler_Diagram.png)](./File:CAP_Theorem_Euler_Diagram.png)CAP theorem Euler diagram 

Thus, if there is a network partition, one has to choose between consistency or availability.

 

During times of normal operations, a data store covers all three.[[9]](./CAP_theorem#cite_note-:2-9)

 

## Explanation

 

No distributed system is safe from network failures, thus network partitioning generally has to be tolerated.[[10]](./CAP_theorem#cite_note-10)[[11]](./CAP_theorem#cite_note-11) In the presence of a partition, one is then left with two options: consistency or [availability](./Availability). When choosing consistency over availability, the system will return an error or a time out if particular information cannot be guaranteed to be up to date due to network partitioning. When choosing availability over consistency, the system will always process the query and try to return the most recent available version of the information, even if it cannot guarantee it is up to date due to network partitioning.[[12]](./CAP_theorem#cite_note-12)

 

In the absence of a network partition, both availability and consistency can be satisfied.[[13]](./CAP_theorem#cite_note-paclec-13)

 

Database systems designed with traditional [ACID](./ACID) guarantees in mind such as [RDBMS](./Relational_database_management_system) choose [consistency](./Consistency_(database_systems)) over availability, whereas systems designed around the [BASE](./Eventual_consistency) philosophy, common in the [NoSQL](./NoSQL) movement for example, choose availability over consistency,[[14]](./CAP_theorem#cite_note-Brewer2012-14) but [MongoDB](./MongoDB) and [Redis](./Redis) resolve network partitions by maintaining consistency while compromising on availability.[[4]](./CAP_theorem#cite_note-:1-4)[[9]](./CAP_theorem#cite_note-:2-9) [CouchDB](./Apache_CouchDB), [Cassandra](./Apache_Cassandra), and [ScyllaDB](./ScyllaDB) are examples of AP databases.[[9]](./CAP_theorem#cite_note-:2-9) There are no NoSQL databases one would classify as CA.[[9]](./CAP_theorem#cite_note-:2-9) Most modern distributed databases offer configuration options for both consistency and availability.[[6]](./CAP_theorem#cite_note-:3-6)

 

Some cloud services choose strong consistency but use worldwide private fiber networks and GPS clock synchronization to minimize the frequency of network partitions[*[citation needed](./Wikipedia:Citation_needed)*]. Finally, consistent [shared-nothing architectures](./Shared-nothing_architecture) may use techniques such as geographic [sharding](./Shard_(database_architecture)) to maintain availability of data owned by the queried node, but without being available for arbitrary requests during a network partition[*[citation needed](./Wikipedia:Citation_needed)*].

 

## History

 

According to computer scientist [Eric Brewer](./Eric_Brewer_(scientist)) of the [University of California, Berkeley](./University_of_California,_Berkeley), the theorem first appeared in autumn 1998.[[14]](./CAP_theorem#cite_note-Brewer2012-14) It was published as the CAP principle in 1999[[15]](./CAP_theorem#cite_note-Brewer1999-15) and presented as a [conjecture](./Conjecture) by Brewer at the 2000 [Symposium on Principles of Distributed Computing](./Symposium_on_Principles_of_Distributed_Computing) (PODC).[[16]](./CAP_theorem#cite_note-Brewer2000-16) In 2002, Seth Gilbert and [Nancy Lynch](./Nancy_Lynch) of [MIT](./MIT) published a formal proof of Brewer's conjecture, rendering it a [theorem](./Theorem).[[1]](./CAP_theorem#cite_note-Gilbert_Lynch-1)

 

In 2012, Brewer clarified some of his positions, including why the often-used "two out of three" concept can be somewhat misleading because system designers only need to sacrifice consistency or availability in the presence of partitions; partition management and recovery techniques exist. Brewer also noted the different definition of consistency used in the CAP theorem relative to the definition used in [ACID](./ACID).[[14]](./CAP_theorem#cite_note-Brewer2012-14)[[17]](./CAP_theorem#cite_note-:0-17)

 

A similar theorem stating the trade-off between consistency and availability in distributed systems had been published by Birman and Friedman in 1996.[[18]](./CAP_theorem#cite_note-18) Birman and Friedman's result had restricted this lower bound to non-commuting operations.

 

The [PACELC theorem](./PACELC_theorem), introduced in 2010,[[13]](./CAP_theorem#cite_note-paclec-13) builds on CAP by stating that even in the absence of partitioning, there is another trade-off between latency and consistency. PACELC means, if partition (P) happens, the trade-off is between availability (A) and consistency (C); Else (E), the trade-off is between latency (L) and consistency (C). Some experts like Marc Brooker argue that the CAP theorem is particularly relevant in intermittently connected environments, such as those related to the [Internet of Things](./Internet_of_things) (IoT) and [mobile applications](./Mobile_app). In these contexts, devices may become partitioned due to challenging physical conditions, such as [power outages](./Power_outage) or when entering confined spaces like elevators. For [distributed systems](./Distributed_computing), such as [cloud applications](./Cloud_computing), it is more appropriate to use the [PACELC theorem](./PACELC_theorem), which is more comprehensive and considers trade-offs such as [latency](./Latency_(engineering)) and [consistency](./Consistency_(database_systems)) even in the absence of network partitions.[[19]](./CAP_theorem#cite_note-19)

 

## See also

 
- [Fallacies of distributed computing](./Fallacies_of_distributed_computing)
- [Lambda architecture](./Lambda_architecture) (solution)
- [PACELC theorem](./PACELC_theorem)
- [Paxos (computer science)](./Paxos_(computer_science))
- [Raft (computer science)](./Raft_(computer_science))
- [Zooko's triangle](./Zooko's_triangle)
- [Inconsistent triad](./Inconsistent_triad)
- [Trilemma](./Trilemma)

 

## References

  
1. [1](./CAP_theorem#cite_ref-Gilbert_Lynch_1-0) [2](./CAP_theorem#cite_ref-Gilbert_Lynch_1-1) [3](./CAP_theorem#cite_ref-Gilbert_Lynch_1-2) Gilbert, Seth; Lynch, Nancy (2002). "Brewer's conjecture and the feasibility of consistent, available, partition-tolerant web services". *ACM SIGACT News*. **33** (2). Association for Computing Machinery (ACM): 51–59. [doi](./Doi_(identifier)):[10.1145/564585.564601](https://doi.org/10.1145%2F564585.564601). [ISSN](./ISSN_(identifier)) [0163-5700](https://search.worldcat.org/issn/0163-5700). [S2CID](./S2CID_(identifier)) [15892169](https://api.semanticscholar.org/CorpusID:15892169).
2. [↑](./CAP_theorem#cite_ref-2) ["Brewer's CAP Theorem"](https://www.julianbrowne.com/article/brewers-cap-theorem/). *julianbrowne.com*. 2009-01-11.
3. [↑](./CAP_theorem#cite_ref-3) Eric A. Brewer (2000). [*Towards Robust Distributed Systems*](https://sites.cs.ucsb.edu/~rich/class/cs293b-cloud/papers/Brewer_podc_keynote_2000.pdf) (PDF). Principles on Distributed Computing (PODC).
4. [1](./CAP_theorem#cite_ref-:1_4-0) [2](./CAP_theorem#cite_ref-:1_4-1) ["What Is the CAP Theorem? | IBM"](https://www.ibm.com/think/topics/cap-theorem). *www.ibm.com*. 2022-12-20. Retrieved 2025-12-05.
5. [↑](./CAP_theorem#cite_ref-5) Liochon, Nicolas. ["The confusing CAP and ACID wording"](http://blog.thislongrun.com/2015/03/the-confusing-cap-and-acid-wording.html). *This long run*. Retrieved 1 February 2019.
6. [1](./CAP_theorem#cite_ref-:3_6-0) [2](./CAP_theorem#cite_ref-:3_6-1) ["Hello Interview | System Design in a Hurry"](https://www.hellointerview.com/learn/system-design/core-concepts/cap-theorem). *Hello Interview*. Retrieved 2025-12-07.
7. [1](./CAP_theorem#cite_ref-Fowler_2015_7-0) [2](./CAP_theorem#cite_ref-Fowler_2015_7-1) Fowler, Adam (2015). *NoSQL For Dummies*. For Dummies. [ISBN](./ISBN_(identifier)) [978-8126554904](./Special:BookSources/978-8126554904).
8. [↑](./CAP_theorem#cite_ref-8) Gilbert, Seth; Lynch, Nancy (2012). ["Perspectives on the CAP Theorem"](https://ieeexplore.ieee.org/document/6122006/). *Computer*. **45** (2): 30–36. [doi](./Doi_(identifier)):[10.1109/mc.2011.389](https://doi.org/10.1109%2Fmc.2011.389). [hdl](./Hdl_(identifier)):[1721.1/79112](https://hdl.handle.net/1721.1%2F79112). [ISSN](./ISSN_(identifier)) [0018-9162](https://search.worldcat.org/issn/0018-9162).
9. [1](./CAP_theorem#cite_ref-:2_9-0) [2](./CAP_theorem#cite_ref-:2_9-1) [3](./CAP_theorem#cite_ref-:2_9-2) [4](./CAP_theorem#cite_ref-:2_9-3) alastairn. ["CAP Theorem"](https://www.scylladb.com/glossary/cap-theorem/). *ScyllaDB*. Retrieved 2025-12-06.
10. [↑](./CAP_theorem#cite_ref-10) Kleppmann, Martin (2015-09-18). [A Critique of the CAP Theorem](https://www.repository.cam.ac.uk/handle/1810/267054) (Report). Apollo - University of Cambridge Repository. [arXiv](./ArXiv_(identifier)):[1509.05393](https://arxiv.org/abs/1509.05393). [Bibcode](./Bibcode_(identifier)):[2015arXiv150905393K](https://ui.adsabs.harvard.edu/abs/2015arXiv150905393K). [doi](./Doi_(identifier)):[10.17863/CAM.13083](https://doi.org/10.17863%2FCAM.13083). [S2CID](./S2CID_(identifier)) [1991487](https://api.semanticscholar.org/CorpusID:1991487). Retrieved 24 November 2019.
11. [↑](./CAP_theorem#cite_ref-11) Martin, Kleppmann. ["Please stop calling databases CP or AP"](https://martin.kleppmann.com/2015/05/11/please-stop-calling-databases-cp-or-ap.html). *Martin Kleppmann's Blog*. Retrieved 24 November 2019.
12. [↑](./CAP_theorem#cite_ref-12) ["CAP theorem - Availability and Beyond: Understanding and Improving the Resilience of Distributed Systems on AWS"](https://docs.aws.amazon.com/whitepapers/latest/availability-and-beyond-improving-resilience/cap-theorem.html). *docs.aws.amazon.com*. Retrieved 2025-12-07.
13. [1](./CAP_theorem#cite_ref-paclec_13-0) [2](./CAP_theorem#cite_ref-paclec_13-1) Abadi, Daniel (2010-04-23). ["DBMS Musings: Problems with CAP, and Yahoo's little known NoSQL system"](http://dbmsmusings.blogspot.com/2010/04/problems-with-cap-and-yahoos-little.html). *DBMS Musings*. Retrieved 2018-01-23.
14. [1](./CAP_theorem#cite_ref-Brewer2012_14-0) [2](./CAP_theorem#cite_ref-Brewer2012_14-1) [3](./CAP_theorem#cite_ref-Brewer2012_14-2) Brewer, Eric (2012). ["CAP twelve years later: How the "rules" have changed"](http://www.infoq.com/articles/cap-twelve-years-later-how-the-rules-have-changed). *Computer*. **45** (2). Institute of Electrical and Electronics Engineers (IEEE): 23–29. [doi](./Doi_(identifier)):[10.1109/mc.2012.37](https://doi.org/10.1109%2Fmc.2012.37). [ISSN](./ISSN_(identifier)) [0018-9162](https://search.worldcat.org/issn/0018-9162). [S2CID](./S2CID_(identifier)) [890105](https://api.semanticscholar.org/CorpusID:890105).
15. [↑](./CAP_theorem#cite_ref-Brewer1999_15-0) Armando Fox; Eric Brewer (1999). *Harvest, Yield and Scalable Tolerant Systems*. Proc. 7th Workshop Hot Topics in Operating Systems (HotOS 99). IEEE CS. pp. 174–178. [doi](./Doi_(identifier)):[10.1109/HOTOS.1999.798396](https://doi.org/10.1109%2FHOTOS.1999.798396).
16. [↑](./CAP_theorem#cite_ref-Brewer2000_16-0) Eric Brewer. ["Towards Robust Distributed Systems"](http://www.cs.berkeley.edu/~brewer/cs262b-2004/PODC-keynote.pdf) (PDF).
17. [↑](./CAP_theorem#cite_ref-:0_17-0) Carpenter, Jeff; Hewitt, Eben (July 2016). [*Cassandra: The Definitive Guide*](https://www.oreilly.com/library/view/cassandra-the-definitive/9781491933657/) (2nd ed.). O'Reilly Media. [ISBN](./ISBN_(identifier)) [9781491933657](./Special:BookSources/9781491933657). In February 2012, Eric Brewer provided an updated perspective on his CAP theorem ... Brewer now describes the "2 out of 3" axiom as somewhat misleading. He notes that designers only need sacrifice consistency or availability in the presence of partitions, and that advances in partition recovery techniques have made it possible for designers to achieve high levels of both consistency and availability.
18. [↑](./CAP_theorem#cite_ref-18) Ken Birman; Roy Friedman (April 1996). ["Trading Consistency for Availability in Distributed Systems"](https://ecommons.cornell.edu/handle/1813/7235). [hdl](./Hdl_(identifier)):[1813/7235](https://hdl.handle.net/1813%2F7235).
19. [↑](./CAP_theorem#cite_ref-19) *Designing Data-Intensive Applications: The Big Ideas Behind Reliable, Scalable, and Maintainable Systems*. O'Reilly Media. [ISBN](./ISBN_(identifier)) [978-1449373320](./Special:BookSources/978-1449373320).

 
| vteDatabase management systems |
| --- |
| Types | Object-orientedcomparisonRelationallistcomparisonKey–valueColumn-orientedlistDocument-orientedWide-column storeGraphNoSQLNewSQLIn-memorylistMulti-modelcomparisonCloudBlockchain-based database |
| Concepts | DatabaseACIDArmstrong's axiomsCodd's 12 rulesCAP theoremCRUDNullCandidate keyForeign keyPACELC design principleSuperkeySurrogate keyUnique key |
| Objects | RelationtablecolumnrowViewTransactionTransaction logTriggerIndexStored procedureCursorPartition |
| Components | Concurrency controlData dictionaryJDBCXQJODBCQuery languageQuery optimizerQuery rewriting systemQuery plan |
| Functions | AdministrationQuery optimizationReplicationSharding |
| Related topics | Database modelsDatabase normalizationDatabase storageDistributed databaseFederated database systemReferential integrityRelational algebraRelational calculusRelational modelObject–relational databaseTransaction processingList of SQL software and tools |
| CategoryOutline |