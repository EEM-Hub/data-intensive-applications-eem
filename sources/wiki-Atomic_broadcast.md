---
source: https://en.wikipedia.org/wiki/Atomic_broadcast
fetched: 2026-06-19
---

Distributed computing primitive 

In [fault-tolerant](./Fault-tolerant) [distributed computing](./Distributed_systems), an **atomic broadcast** or **total order broadcast** is a [broadcast](./Broadcasting_(networking)) where all correct processes in a system of multiple processes receive the same set of messages in the same order; that is, the same sequence of messages.[[1]](./Atomic_broadcast#cite_note-Kshemkalyani-1)[[2]](./Atomic_broadcast#cite_note-Defago2004-2)  The broadcast is termed "[atomic](./Atomic_(computer_science))" because it either eventually completes correctly at all participants, or all participants abort without [side effects](./Side_effect_(computer_science)).  Atomic broadcasts are an important distributed computing primitive.

 

## Properties

 

The following properties are usually required from an atomic broadcast protocol:

 
1. Validity: if a correct participant broadcasts a message, then all correct participants will eventually receive it.
2. Uniform Agreement: if one correct participant receives a message, then all correct participants will eventually receive that message.
3. Uniform Integrity: a message is received by each participant at most once, and only if it was previously broadcast.
4. Uniform Total Order: the messages are [totally ordered](./Total_order) in the mathematical sense; that is, if any correct participant receives message 1 first and message 2 second, then every other correct participant must receive message 1 before message 2.

 

Rodrigues and Raynal[[3]](./Atomic_broadcast#cite_note-RR-3) and Schiper et al.[[4]](./Atomic_broadcast#cite_note-Schiper-4) define the integrity and validity properties of atomic broadcast slightly differently.

 

Note that total order is not equivalent to [FIFO](./FIFO_(computing_and_electronics)) order, which requires that if a process sent message 1 before it sent message 2, then all participants must receive message 1 before receiving message 2.  It is also not equivalent to "causal order", where if message 2 "depends on" or "occurs after" message 1 then all participants must receive message 2 after receiving message 1. While a strong and useful condition, total order requires only that all participants receive the messages in the same order, but does not place other constraints on that order such as that in which the messages are sent.[[5]](./Atomic_broadcast#cite_note-Dermot_Kelly-5)

 

## Fault tolerance

 

Designing an algorithm for atomic broadcasts is relatively easy if it can be assumed that computers will not fail.  For example, if there are no failures, atomic broadcast can be achieved simply by having all participants communicate with one "leader" which determines the order of the messages, with the other participants following the leader.

 

However, real computers are faulty; they fail and recover from failure at unpredictable, possibly inopportune, times.  For example, in the follow-the-leader algorithm, what if the leader fails at the wrong time?  In such an environment achieving atomic broadcasts is difficult.[[1]](./Atomic_broadcast#cite_note-Kshemkalyani-1)  A number of protocols have been proposed for performing atomic broadcast, under various assumptions about the network, failure models, availability of hardware support for [multicast](./Multicast), and so forth.[[2]](./Atomic_broadcast#cite_note-Defago2004-2)

 

## Equivalent to consensus

 

In order for the conditions for atomic broadcast to be satisfied, the participants must effectively "agree" on the order of receipt of the messages. Participants recovering from failure, after the other participants have "agreed" on an order and started to receive the messages, must be able to learn and comply with the agreed order. Such considerations indicate that in systems with crash failures, atomic broadcast and [consensus](./Consensus_(computing)) are equivalent problems.[[6]](./Atomic_broadcast#cite_note-Chandra-Toueg-6)

 

A value can be proposed by a process for consensus by atomically broadcasting it, and a process can decide a value by selecting the value of the first message which it atomically receives. Thus, consensus can be reduced to atomic broadcast.

 

Conversely, a group of participants can atomically broadcast messages by achieving consensus regarding the first message to be received, followed by achieving consensus on the next message, and so forth until all the messages have been received.  Thus, atomic broadcast reduces to consensus. This was demonstrated more formally and in greater detail by Xavier Défago, et al.[[2]](./Atomic_broadcast#cite_note-Defago2004-2)

 

A fundamental result in distributed computing is that achieving consensus in asynchronous systems in which even one crash failure can occur is impossible in the most general case.  This was shown in 1985 by [Michael J. Fischer](./Michael_J._Fischer), [Nancy Lynch](./Nancy_Lynch), and [Mike Paterson](./Mike_Paterson), and is sometimes called the [FLP result](./Consensus_(computer_science)#The_FLP_impossibility_result_for_asynchronous_deterministic_consensus).[[7]](./Atomic_broadcast#cite_note-FLP-7) Since consensus and atomic broadcast are equivalent, FLP applies also to atomic broadcast.[[5]](./Atomic_broadcast#cite_note-Dermot_Kelly-5) The FLP result does not prohibit the implementation of atomic broadcast in practice, but it does require making less stringent assumptions than FLP in some respect, such as about processor and communication timings.

 

## Algorithms

 

The [Chandra-Toueg algorithm](./Chandra–Toueg_consensus_algorithm)[[6]](./Atomic_broadcast#cite_note-Chandra-Toueg-6) is a consensus-based solution to atomic broadcast. Another solution has been put forward by Rodrigues and Raynal.[[3]](./Atomic_broadcast#cite_note-RR-3)

 

The Zookeeper Atomic Broadcast (ZAB) protocol is the basic building block for [Apache ZooKeeper](./Apache_ZooKeeper), a fault-tolerant distributed coordination service which underpins [Hadoop](./Hadoop) and many other important distributed systems.[[8]](./Atomic_broadcast#cite_note-Zab-8)[[9]](./Atomic_broadcast#cite_note-Medeiros-9)

 

[Ken Birman](./Ken_Birman) has proposed the [virtual synchrony](./Virtual_synchrony) execution model for distributed systems, the idea of which is that all processes observe the same events in the same order. A total ordering of the messages being received, as in atomic broadcast, is one (though not the only) method for attaining virtually synchronous message receipt.

 

## References

 
1. [1](./Atomic_broadcast#cite_ref-Kshemkalyani_1-0) [2](./Atomic_broadcast#cite_ref-Kshemkalyani_1-1) Kshemkalyani, Ajay; Singhal, Mukesh (2008). [*Distributed Computing: Principles, Algorithms, and Systems*](https://www.cs.uic.edu/~ajayk/DCS-Book). Cambridge University Press. pp. 583–585. [ISBN](./ISBN_(identifier)) [9781139470315](./Special:BookSources/9781139470315).
2. [1](./Atomic_broadcast#cite_ref-Defago2004_2-0) [2](./Atomic_broadcast#cite_ref-Defago2004_2-1) [3](./Atomic_broadcast#cite_ref-Defago2004_2-2) Défago, Xavier; Schiper, André; Urbán, Péter (2004). ["Total order broadcast and multicast algorithms"](https://infoscience.epfl.ch/record/52563/files/IC_TECH_REPORT_200356.pdf) (PDF). *ACM Computing Surveys*. **36** (4): 372–421. [doi](./Doi_(identifier)):[10.1145/1041680.1041682](https://doi.org/10.1145%2F1041680.1041682). [S2CID](./S2CID_(identifier)) [207155989](https://api.semanticscholar.org/CorpusID:207155989).
3. [1](./Atomic_broadcast#cite_ref-RR_3-0) [2](./Atomic_broadcast#cite_ref-RR_3-1) Rodrigues L, Raynal M.: Atomic Broadcast in Asynchronous Crash-Recovery Distributed Systems [](https://doi.org/10.1109/ICDCS.2000.840941), ICDCS '00: Proceedings of the 20th International Conference on Distributed Computing Systems ( ICDCS 2000)
4. [↑](./Atomic_broadcast#cite_ref-Schiper_4-0) Ekwall, R.; Schiper, A. (2006). "Solving Atomic Broadcast with Indirect Consensus". [*International Conference on Dependable Systems and Networks (DSN'06)*](https://infoscience.epfl.ch/record/83547/files/TechReport_LSR_2006_01.pdf) (PDF). pp. 156–165. [doi](./Doi_(identifier)):[10.1109/dsn.2006.65](https://doi.org/10.1109%2Fdsn.2006.65). [ISBN](./ISBN_(identifier)) [0-7695-2607-1](./Special:BookSources/0-7695-2607-1). [S2CID](./S2CID_(identifier)) [14315628](https://api.semanticscholar.org/CorpusID:14315628).
5. [1](./Atomic_broadcast#cite_ref-Dermot_Kelly_5-0) [2](./Atomic_broadcast#cite_ref-Dermot_Kelly_5-1) Dermot Kelly. ["Group Communication"](http://www.cs.nuim.ie/~dkelly/CS402-06/Group%20Communication.htm).
6. [1](./Atomic_broadcast#cite_ref-Chandra-Toueg_6-0) [2](./Atomic_broadcast#cite_ref-Chandra-Toueg_6-1) Chandra, Tushar Deepak; Toueg, Sam (1996). ["Unreliable failure detectors for reliable distributed systems"](https://doi.org/10.1145%2F226643.226647). *Journal of the ACM*. **43** (2): 225–267. [doi](./Doi_(identifier)):[10.1145/226643.226647](https://doi.org/10.1145%2F226643.226647). [hdl](./Hdl_(identifier)):[1813/7192](https://hdl.handle.net/1813%2F7192). [S2CID](./S2CID_(identifier)) [9835158](https://api.semanticscholar.org/CorpusID:9835158).
7. [↑](./Atomic_broadcast#cite_ref-FLP_7-0) Michael J. Fischer, Nancy A. Lynch, and Michael S. Paterson (1985). ["Impossibility of Distributed Consensus with One Faulty Process"](https://groups.csail.mit.edu/tds/papers/Lynch/jacm85.pdf) (PDF). *Journal of the ACM*. **32** (2): 374–382. [doi](./Doi_(identifier)):[10.1145/3149.214121](https://doi.org/10.1145%2F3149.214121). [S2CID](./S2CID_(identifier)) [207660233](https://api.semanticscholar.org/CorpusID:207660233).`{{cite journal}}`:  CS1 maint: multiple names: authors list ([link](./Category:CS1_maint:_multiple_names:_authors_list))
8. [↑](./Atomic_broadcast#cite_ref-Zab_8-0) Flavio P. Junqueira, Benjamin C. Reed, and Marco Serafini, Yahoo! Research (2011). "Zab: High-performance broadcast for primary-backup systems". *2011 IEEE/IFIP 41st International Conference on Dependable Systems & Networks (DSN)*. pp. 245–256. [doi](./Doi_(identifier)):[10.1109/DSN.2011.5958223](https://doi.org/10.1109%2FDSN.2011.5958223). [ISBN](./ISBN_(identifier)) [978-1-4244-9233-6](./Special:BookSources/978-1-4244-9233-6). [S2CID](./S2CID_(identifier)) [206611670](https://api.semanticscholar.org/CorpusID:206611670).`{{cite book}}`:  CS1 maint: multiple names: authors list ([link](./Category:CS1_maint:_multiple_names:_authors_list))
9. [↑](./Atomic_broadcast#cite_ref-Medeiros_9-0) André Medeiros (March 20, 2012). ["ZooKeeper's atomic broadcast protocol: Theory and practice"](http://www.tcs.hut.fi/Studies/T-79.5001/reports/2012-deSouzaMedeiros.pdf) (PDF). *Helsinki University of Technology - Laboratory of Theoretical Computer Science*.