---
source: https://en.wikipedia.org/wiki/Eventual_consistency
fetched: 2026-06-19
---

Consistency model used in distributed computing to achieve high availability 
|  | This articlemay be too technical for most readers to understand.Pleasehelp improve ittomake it understandable to non-experts, without removing the technical details.(January 2017)(Learn how and when to remove this message) |
| --- | --- |

 

**Eventual consistency** is a [consistency model](./Consistency_model) used in [distributed computing](./Distributed_computing) to achieve [high availability](./High_availability). An eventually consistent system ensures that if no new updates are made to a given data item, *eventually* all read accesses to that item will return the last updated value.[[1]](./Eventual_consistency#cite_note-Vogels-1) Eventual consistency, also called [optimistic replication](./Optimistic_replication),[[2]](./Eventual_consistency#cite_note-2) is widely deployed in distributed systems and has origins in early mobile computing projects.[[3]](./Eventual_consistency#cite_note-Bayou-3) A system that has achieved eventual consistency is said to have **converged**, or achieved **replica convergence**.[[4]](./Eventual_consistency#cite_note-Bayou-Conflicts-4) Eventual consistency is a weak guarantee – most stronger models, like [linearizability](./Linearizability), are trivially eventually consistent.

 

Eventually-consistent services are often classified as providing BASE semantics (basically-available, soft-state, eventual consistency), in contrast to traditional [ACID (atomicity, consistency, isolation, durability)](./ACID). The rough definitions of each term in BASE are:[[5]](./Eventual_consistency#cite_note-5)[[6]](./Eventual_consistency#cite_note-6)

 
- **Basically available**: it is the database’s concurrent accessibility by users at all times. One user doesn’t need to wait for others to finish the transaction before updating the record.[[7]](./Eventual_consistency#cite_note-:0-7)
- **Soft-state**: refers to the notion that data can have transient or temporary states that may change over time, even without external triggers or inputs. Thus, even without further external updates, until an update converges, it is possible that different queries for a record see different values.[[7]](./Eventual_consistency#cite_note-:0-7)
- **Eventually consistent**: this means the record will achieve consistency when all the concurrent updates have been completed. At this point, applications querying the record will see the same value.[[7]](./Eventual_consistency#cite_note-:0-7)

 

Eventual consistency faces criticism[[8]](./Eventual_consistency#cite_note-8) for adding complexity to distributed software applications. This complexity arises because eventual consistency provides only a [liveness](./Liveness) guarantee (ensuring reads eventually return the same value) without [safety](./Safety_(distributed_computing)) guarantees—allowing any intermediate value before convergence. Application developers find this challenging because it differs from single-threaded programming, where variables reliably return their assigned values immediately. With weak consistency guarantees, developers must carefully consider these limitations, as incorrect assumptions about consistency levels can lead to subtle bugs that only surface during network failures or high concurrency.[[9]](./Eventual_consistency#cite_note-kleppmann-9)

 

## Conflict resolution

 

In order to ensure replica convergence, a system must reconcile differences between multiple copies of distributed data. This consists of two parts:

 
- exchanging versions or updates of data between servers (often known as **anti-entropy**);[[10]](./Eventual_consistency#cite_note-10) and
- choosing an appropriate final state when concurrent updates have occurred, called **reconciliation**.

 

The most appropriate approach to reconciliation depends on the application.  A widespread approach is "last writer wins".[[1]](./Eventual_consistency#cite_note-Vogels-1)  Another is to invoke a user-specified conflict handler.[[4]](./Eventual_consistency#cite_note-Bayou-Conflicts-4) [Timestamps](./Lamport_timestamps) and [vector clocks](./Vector_clock) are often used to detect concurrency between updates. Some people use "first writer wins" in situations where "last writer wins" is unacceptable.[[11]](./Eventual_consistency#cite_note-11)

 

Reconciliation of concurrent writes must occur sometime before the next read, and can be scheduled at different instants:[[3]](./Eventual_consistency#cite_note-Bayou-3)[[12]](./Eventual_consistency#cite_note-Confront-12)

 
- Read repair: The correction is done when a read finds an inconsistency. This slows down the read operation.
- Write repair: The correction takes place during a write operation, slowing down the write operation.
- Asynchronous repair: The correction is not part of a read or write operation.

 

## Strong eventual consistency

 

Whereas eventual consistency is only a [liveness](./Liveness) guarantee (updates will be observed eventually), **strong eventual consistency** (SEC) adds the [safety](./Safety_(distributed_computing)) guarantee that any two nodes that have received the same (unordered) set of updates will be in the same state. A common approach to ensure SEC is [conflict-free replicated data types](./Conflict-free_replicated_data_type).[[13]](./Eventual_consistency#cite_note-13)

 

## See also

 
- [CAP theorem](./CAP_theorem)

 

## References

  
1. [1](./Eventual_consistency#cite_ref-Vogels_1-0) [2](./Eventual_consistency#cite_ref-Vogels_1-1) [Vogels, W.](./Werner_Vogels) (2009). ["Eventually consistent"](https://doi.org/10.1145%2F1435417.1435432). *Communications of the ACM*. **52**: 40–44. [doi](./Doi_(identifier)):[10.1145/1435417.1435432](https://doi.org/10.1145%2F1435417.1435432).
2. [↑](./Eventual_consistency#cite_ref-2) [Vogels, W.](./Werner_Vogels) (2008). ["Eventually Consistent"](https://doi.org/10.1145%2F1466443.1466448). *ACM Queue*. **6** (6): 14–19. [doi](./Doi_(identifier)):[10.1145/1466443.1466448](https://doi.org/10.1145%2F1466443.1466448).
3. [1](./Eventual_consistency#cite_ref-Bayou_3-0) [2](./Eventual_consistency#cite_ref-Bayou_3-1) Terry, D. B.; Theimer, M. M.; Petersen, K.; Demers, A. J.; Spreitzer, M. J.; Hauser, C. H. (1995). "Managing update conflicts in Bayou, a weakly connected replicated storage system". *Proceedings of the fifteenth ACM symposium on Operating systems principles - SOSP '95*. p. 172. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.12.7323](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.12.7323). [doi](./Doi_(identifier)):[10.1145/224056.224070](https://doi.org/10.1145%2F224056.224070). [ISBN](./ISBN_(identifier)) [978-0897917155](./Special:BookSources/978-0897917155). [S2CID](./S2CID_(identifier)) [7834967](https://api.semanticscholar.org/CorpusID:7834967).
4. [1](./Eventual_consistency#cite_ref-Bayou-Conflicts_4-0) [2](./Eventual_consistency#cite_ref-Bayou-Conflicts_4-1) Petersen, K.; Spreitzer, M. J.; Terry, D. B.; Theimer, M. M.; Demers, A. J. (1997). "Flexible update propagation for weakly consistent replication". *ACM SIGOPS Operating Systems Review*. **31** (5): 288. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.17.555](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.17.555). [doi](./Doi_(identifier)):[10.1145/269005.266711](https://doi.org/10.1145%2F269005.266711).
5. [↑](./Eventual_consistency#cite_ref-5) Pritchett, D. (2008). ["Base: An Acid Alternative"](https://doi.org/10.1145%2F1394127.1394128). *ACM Queue*. **6** (3): 48–55. [doi](./Doi_(identifier)):[10.1145/1394127.1394128](https://doi.org/10.1145%2F1394127.1394128).
6. [↑](./Eventual_consistency#cite_ref-6) Bailis, P.; Ghodsi, A. (2013). ["Eventual Consistency Today: Limitations, Extensions, and Beyond"](https://doi.org/10.1145%2F2460276.2462076). *ACM Queue*. **11** (3): 20. [doi](./Doi_(identifier)):[10.1145/2460276.2462076](https://doi.org/10.1145%2F2460276.2462076).
7. [1](./Eventual_consistency#cite_ref-:0_7-0) [2](./Eventual_consistency#cite_ref-:0_7-1) [3](./Eventual_consistency#cite_ref-:0_7-2) ["What's the Difference Between an ACID and a BASE Database?"](https://aws.amazon.com/compare/the-difference-between-acid-and-base-database/).
8. [↑](./Eventual_consistency#cite_ref-8) [H](./XSKT_Cần_Thơ_F.C.)Yaniv Pessach (2013), *Distributed Storage* (Distributed Storage: Concepts, Algorithms, and Implementations ed.), Amazon, [OL](./OL_(identifier)) [25423189M](https://openlibrary.org/books/OL25423189M), Systems using Eventual Consistency result in decreased system load and increased system availability but result in increased cognitive complexity for users and developers
9. [↑](./Eventual_consistency#cite_ref-kleppmann_9-0) Kleppmann, Martin (2017). *Designing data-intensive applications: the big ideas behind reliable, scalable, and maintainable systems* (1 ed.). Beijing Boston Farnham Sebastopol Tokyo: O'Reilly. [ISBN](./ISBN_(identifier)) [978-1449373320](./Special:BookSources/978-1449373320).
10. [↑](./Eventual_consistency#cite_ref-10) Demers, A.; Greene, D.; Hauser, C.; Irish, W.; Larson, J. (1987). "Epidemic algorithms for replicated database maintenance". *Proceedings of the sixth annual ACM Symposium on Principles of distributed computing - PODC '87*. p. 1. [doi](./Doi_(identifier)):[10.1145/41840.41841](https://doi.org/10.1145%2F41840.41841). [ISBN](./ISBN_(identifier)) [978-0-89791-239-6](./Special:BookSources/978-0-89791-239-6). [S2CID](./S2CID_(identifier)) [1889203](https://api.semanticscholar.org/CorpusID:1889203).
11. [↑](./Eventual_consistency#cite_ref-11) Rockford Lhotka.
["Concurrency techniques"](http://www.lhotka.net/Article.aspx?id=890d3e3c-8a49-486c-ae48-a44e7e1f7844) [Archived](https://web.archive.org/web/20180511145619/http://www.lhotka.net/Article.aspx?id=890d3e3c-8a49-486c-ae48-a44e7e1f7844) 2018-05-11 at the [Wayback Machine](./Wayback_Machine).
2003.
12. [↑](./Eventual_consistency#cite_ref-Confront_12-0)  Olivier Mallassi (2010-06-09). ["Let's play with Cassandra… (Part 1/3)"](http://blog.octo.com/en/nosql-lets-play-with-cassandra-part-13/). OCTO Talks!. Retrieved 2011-03-23. Of course, at a given time, chances are high that each node has its own version of the data. Conflict resolution is made during the read requests (called read-repair) and the current version of Cassandra does not provide a Vector Clock conflict resolution mechanisms [sic] (should be available in the version 0.7). Conflict resolution is so based on timestamp (the one set when you insert the row or the column): the higher timestamp win[s] and the node you are reading the data [from] is responsible for that. This is an important point because the timestamp is specified by the client, at the moment the column is inserted. Thus, all Cassandra clients' [sic] need to be synchronized... 
13. [↑](./Eventual_consistency#cite_ref-13) Shapiro, Marc; Preguiça, Nuno; Baquero, Carlos; Zawirski, Marek (2011-10-10). "Conflict-free replicated data types". *SSS'11 Proceedings of the 13th International Conference on Stabilization, Safety, and the Security of Distributed Systems*. Springer-Verlag Berlin, Heidelberg: 386–400.

 

## Further reading

 
- Burckhardt, Sebastian (2014-10-09). ["Principles of Eventual Consistency"](https://doi.org/10.1561/2500000011). *Foundations and Trends in Programming Languages*. **1** (1–2): 1–150. [doi](./Doi_(identifier)):[10.1561/2500000011](https://doi.org/10.1561%2F2500000011). [ISSN](./ISSN_(identifier)) [2325-1107](https://search.worldcat.org/issn/2325-1107).