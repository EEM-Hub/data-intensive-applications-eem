---
source: https://en.wikipedia.org/wiki/Lamport_timestamp
fetched: 2026-06-19
---

Algorithm used to determine the order of events in a distributed computer system 

The **Lamport timestamp** algorithm is a simple [logical clock algorithm](./Logical_clock_algorithm) used to determine the order of events in a [distributed computer system](./Distributed_computer_system). As different nodes or processes will typically not be perfectly synchronized, this algorithm is used to provide a [partial ordering](./Partially_ordered_set) of events with minimal overhead, and conceptually provide a starting point for the more advanced [vector clock](./Vector_clock) method. The algorithm is named after its creator, [Leslie Lamport](./Leslie_Lamport).

 

Distributed algorithms such as resource synchronization often depend on some method of ordering events to function. For example, consider a system with two processes and a disk. The processes send messages to each other, and also send messages to the disk requesting access. The disk grants access in the order the messages were *received*. For example process     A   {\displaystyle A}  ![{\displaystyle A}](https://wikimedia.org/api/rest_v1/media/math/render/svg/7daff47fa58cdfd29dc333def748ff5fa4c923e3) sends a message to the disk requesting write access, and then sends a read instruction message to process     B   {\displaystyle B}  ![{\displaystyle B}](https://wikimedia.org/api/rest_v1/media/math/render/svg/47136aad860d145f75f3eed3022df827cee94d7a). Process     B   {\displaystyle B}  ![{\displaystyle B}](https://wikimedia.org/api/rest_v1/media/math/render/svg/47136aad860d145f75f3eed3022df827cee94d7a) receives the message, and as a result sends its own read request message to the disk. If there is a timing delay causing the disk to receive both messages at the same time, it can determine which message *[happened-before](./Happened-before)* the other:     A   {\displaystyle A}  ![{\displaystyle A}](https://wikimedia.org/api/rest_v1/media/math/render/svg/7daff47fa58cdfd29dc333def748ff5fa4c923e3) *happens-before*     B   {\displaystyle B}  ![{\displaystyle B}](https://wikimedia.org/api/rest_v1/media/math/render/svg/47136aad860d145f75f3eed3022df827cee94d7a) if one can get from     A   {\displaystyle A}  ![{\displaystyle A}](https://wikimedia.org/api/rest_v1/media/math/render/svg/7daff47fa58cdfd29dc333def748ff5fa4c923e3) to     B   {\displaystyle B}  ![{\displaystyle B}](https://wikimedia.org/api/rest_v1/media/math/render/svg/47136aad860d145f75f3eed3022df827cee94d7a) by a sequence of moves of two types: moving forward while remaining in the same process, and following a message from its sending to its reception. A logical clock algorithm provides a mechanism to determine facts about the order of such events. Note that if two events happen in different processes that do not exchange messages directly or indirectly via third-party processes, then we say that the two processes are concurrent, that is, nothing can be said about the ordering of the two events.[[1]](./Lamport_timestamp#cite_note-1)

 

Lamport invented a simple mechanism by which the *happened-before* ordering can be captured numerically. A Lamport logical clock is a numerical software counter value maintained in each process.

 

Conceptually, this logical clock can be thought of as a clock that only has meaning in relation to messages moving between processes. When a process receives a message, it re-synchronizes its logical clock with that sender. The above-mentioned vector clock is a generalization of the idea into the context of an arbitrary number of parallel, independent processes.

 

## Algorithm

 

The algorithm follows some simple rules:

 
1. A process increments its counter before each local event (e.g., message sending event);
2. When a process sends a message, it includes its counter value with the message after executing step 1;
3. On receiving a message, the counter of the recipient is updated, if necessary, to the greater of its current counter and the timestamp in the received message. The counter is then incremented by 1 before the message is considered received.[[2]](./Lamport_timestamp#cite_note-Lamport_1978-2)

 

In [pseudocode](./Pseudocode), the algorithm for sending is:

 
```
# event is known
time = time + 1;
# event happens
send(message, time);
```
 

The algorithm for receiving a message is:

 
```
(message, timestamp) = receive();
time = max(timestamp, time) + 1;
```
 

## Considerations

 

For every two different events     a   {\displaystyle a}  ![{\displaystyle a}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ffd2487510aa438433a2579450ab2b3d557e5edc) and     b   {\displaystyle b}  ![{\displaystyle b}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f11423fbb2e967f986e36804a8ae4271734917c3) occurring in the same process, and     C ( x )   {\displaystyle C(x)}  ![{\displaystyle C(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/7f6b53682fddbe3028ffd75bd75771b86c6c7bd9) being the timestamp for a certain event     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4), it is necessary that     C ( a )   {\displaystyle C(a)}  ![{\displaystyle C(a)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6b56d60b084e7a60e5d95f3a7c64a79945616431) never equals     C ( b )   {\displaystyle C(b)}  ![{\displaystyle C(b)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/107d66df8a250b694e33028c7c50f6a91cc4dea4).

 

Therefore it is necessary that:

 
- The logical clock be set so that there is a minimum of one clock "tick" (increment of the counter) between events     a   {\displaystyle a}  ![{\displaystyle a}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ffd2487510aa438433a2579450ab2b3d557e5edc) and     b   {\displaystyle b}  ![{\displaystyle b}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f11423fbb2e967f986e36804a8ae4271734917c3);
- In a multi-process or multi-threaded environment, it might be necessary to attach the process ID (PID) or any other unique ID to the timestamp so that it is possible to differentiate between events     a   {\displaystyle a}  ![{\displaystyle a}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ffd2487510aa438433a2579450ab2b3d557e5edc) and     b   {\displaystyle b}  ![{\displaystyle b}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f11423fbb2e967f986e36804a8ae4271734917c3) which may occur simultaneously in different processes.

 

## Causal ordering

 

For any two events,     a   {\displaystyle a}  ![{\displaystyle a}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ffd2487510aa438433a2579450ab2b3d557e5edc) and     b   {\displaystyle b}  ![{\displaystyle b}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f11423fbb2e967f986e36804a8ae4271734917c3), if there is any way that     a   {\displaystyle a}  ![{\displaystyle a}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ffd2487510aa438433a2579450ab2b3d557e5edc) could have influenced     b   {\displaystyle b}  ![{\displaystyle b}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f11423fbb2e967f986e36804a8ae4271734917c3), then the Lamport timestamp of     a   {\displaystyle a}  ![{\displaystyle a}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ffd2487510aa438433a2579450ab2b3d557e5edc) will be less than the Lamport timestamp of     b   {\displaystyle b}  ![{\displaystyle b}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f11423fbb2e967f986e36804a8ae4271734917c3). It’s also possible to have two events where we can’t say which came first; when that happens, it means that they couldn’t have affected each other. If     a   {\displaystyle a}  ![{\displaystyle a}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ffd2487510aa438433a2579450ab2b3d557e5edc) and     b   {\displaystyle b}  ![{\displaystyle b}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f11423fbb2e967f986e36804a8ae4271734917c3) can’t have any effect on each other, then it doesn’t matter which one came first.

 

## Implications

 

A Lamport clock may be used to create a [partial ordering](./Partially_ordered_set#:~:text=A_partial_order_defines_a,(also_called_a_poset).) of events between processes. Given a logical clock following these rules, the following relation is true: if     a → →  b   {\displaystyle a\rightarrow b}  ![{\displaystyle a\rightarrow b}](https://wikimedia.org/api/rest_v1/media/math/render/svg/390afdb0d8e933dbc4eee8022d8c91b2015f0522) then     C ( a ) < C ( b )   {\displaystyle C(a)<C(b)}  ![{\displaystyle C(a)<C(b)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/61a75c7595dc224580384eddca657fd6ce251662), where     → →     {\displaystyle \rightarrow \,}  ![{\displaystyle \rightarrow \,}](https://wikimedia.org/api/rest_v1/media/math/render/svg/30c77b3d020a207c12a2e96794b739223a647089) means *happened-before*.

 

This relation only goes one way, and is called the *clock consistency condition*: if one event comes before another, then that event's logical clock comes before the other's. The *strong clock consistency condition*, which is two way (if     C ( a ) < C ( b )   {\displaystyle C(a)<C(b)}  ![{\displaystyle C(a)<C(b)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/61a75c7595dc224580384eddca657fd6ce251662) then     a → →  b   {\displaystyle a\rightarrow b}  ![{\displaystyle a\rightarrow b}](https://wikimedia.org/api/rest_v1/media/math/render/svg/390afdb0d8e933dbc4eee8022d8c91b2015f0522)), can be obtained by other techniques such as vector clocks. Using only a simple Lamport clock, only a partial causal ordering can be inferred from the clock.

 

However, via the [contrapositive](./Contrapositive), it's true that     C ( a ) ≮ ≮  C ( b )   {\displaystyle C(a)\nless C(b)}  ![{\displaystyle C(a)\nless C(b)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/186c9626b0523862ce845cd727c046710c211804) implies     a ↛ ↛  b   {\displaystyle a\nrightarrow b}  ![{\displaystyle a\nrightarrow b}](https://wikimedia.org/api/rest_v1/media/math/render/svg/bcf07bf280d7da508f3464c5c9a8a76b82d07ad8). So, for example, if     C ( a ) ≥ ≥  C ( b )   {\displaystyle C(a)\geq C(b)}  ![{\displaystyle C(a)\geq C(b)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/982338a5c3552c8fa2f6957459c4d1004e24340a) then     a   {\displaystyle a}  ![{\displaystyle a}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ffd2487510aa438433a2579450ab2b3d557e5edc) cannot have *happened-before*     b   {\displaystyle b}  ![{\displaystyle b}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f11423fbb2e967f986e36804a8ae4271734917c3).

 

Another way of putting this is that     C ( a ) < C ( b )   {\displaystyle C(a)<C(b)}  ![{\displaystyle C(a)<C(b)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/61a75c7595dc224580384eddca657fd6ce251662) means that     a   {\displaystyle a}  ![{\displaystyle a}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ffd2487510aa438433a2579450ab2b3d557e5edc) may have *happened-before*     b   {\displaystyle b}  ![{\displaystyle b}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f11423fbb2e967f986e36804a8ae4271734917c3), or be incomparable with     b   {\displaystyle b}  ![{\displaystyle b}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f11423fbb2e967f986e36804a8ae4271734917c3) in the *happened-before* ordering, but     a   {\displaystyle a}  ![{\displaystyle a}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ffd2487510aa438433a2579450ab2b3d557e5edc) did not happen after     b   {\displaystyle b}  ![{\displaystyle b}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f11423fbb2e967f986e36804a8ae4271734917c3).

 

Nevertheless, Lamport timestamps can be used to create a [total ordering](./Total_ordering) of events in a distributed system by using some arbitrary mechanism to break ties (e.g., the ID of the process). The caveat is that this ordering is artificial and cannot be depended on to imply a causal relationship.

 

## Lamport's logical clock in distributed systems

 

In a distributed system, it is not possible in practice to [synchronize time](./Clock_synchronization) across entities (typically thought of as processes) within the system; hence, the entities can use the concept of a logical clock based on the events through which they communicate.

 

If two entities do not exchange any messages, then they probably do not need to share a common clock; events occurring on those entities are termed concurrent events.

 

Among the processes on the same local machine we can order the events based on the local clock of the system.

 

When two entities communicate by [message passing](./Message_passing), then the send event is said to *happen-before* the receive event, and the logical order can be established among the events.

 

A distributed system is said to have partial order if we can have a partial order relationship among the events in the system. If "totality", i.e., causal relationship among all events in the system, can be established, then the system is said to have total order.

 

A single entity cannot have two events occur simultaneously. If the system has total order we can determine the order among all events in the system. If the system has partial order between processes, which is the type of order Lamport's logical clock provides, then we can only tell the ordering between entities that interact. Lamport addressed ordering two events with the same timestamp (or counter): "To break ties, we use any arbitrary total ordering     <   {\displaystyle <}  ![{\displaystyle <}](https://wikimedia.org/api/rest_v1/media/math/render/svg/33737c89a17785dacc8638b4d66db3d5c8670de1) of the processes."[[2]](./Lamport_timestamp#cite_note-Lamport_1978-2) Thus two timestamps or counters may be the same within a distributed system, but in applying the logical clocks algorithm events that occur will always maintain at least a strict partial ordering.

 

Lamport clocks lead to a situation where all events in a distributed system are totally ordered. That is, if     a → →  b   {\displaystyle a\rightarrow b}  ![{\displaystyle a\rightarrow b}](https://wikimedia.org/api/rest_v1/media/math/render/svg/390afdb0d8e933dbc4eee8022d8c91b2015f0522), then we can say     a   {\displaystyle a}  ![{\displaystyle a}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ffd2487510aa438433a2579450ab2b3d557e5edc) actually happened before     b   {\displaystyle b}  ![{\displaystyle b}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f11423fbb2e967f986e36804a8ae4271734917c3).

 

Note that with Lamport’s clocks, nothing can be said about the actual time of     a   {\displaystyle a}  ![{\displaystyle a}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ffd2487510aa438433a2579450ab2b3d557e5edc) and     b   {\displaystyle b}  ![{\displaystyle b}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f11423fbb2e967f986e36804a8ae4271734917c3). If the logical clock says     C ( a ) < C ( b )   {\displaystyle C(a)<C(b)}  ![{\displaystyle C(a)<C(b)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/61a75c7595dc224580384eddca657fd6ce251662), that does not mean in reality that     a   {\displaystyle a}  ![{\displaystyle a}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ffd2487510aa438433a2579450ab2b3d557e5edc) actually happened before     b   {\displaystyle b}  ![{\displaystyle b}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f11423fbb2e967f986e36804a8ae4271734917c3) in terms of real time.

 

Lamport clocks show non-causality, but do not capture all causality. Knowing     a → →  c   {\displaystyle a\rightarrow c}  ![{\displaystyle a\rightarrow c}](https://wikimedia.org/api/rest_v1/media/math/render/svg/de8f69264bbc4ad99a97d815a607210e2bdd56ec) and     b → →  c   {\displaystyle b\rightarrow c}  ![{\displaystyle b\rightarrow c}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5f56ed0cf3c535544111c1f4f367eec31ec5e4b5) shows     c   {\displaystyle c}  ![{\displaystyle c}](https://wikimedia.org/api/rest_v1/media/math/render/svg/86a67b81c2de995bd608d5b2df50cd8cd7d92455) did not cause     a   {\displaystyle a}  ![{\displaystyle a}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ffd2487510aa438433a2579450ab2b3d557e5edc) or     b   {\displaystyle b}  ![{\displaystyle b}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f11423fbb2e967f986e36804a8ae4271734917c3) but we cannot say which initiated     c   {\displaystyle c}  ![{\displaystyle c}](https://wikimedia.org/api/rest_v1/media/math/render/svg/86a67b81c2de995bd608d5b2df50cd8cd7d92455).

 

This kind of information can be important when trying to replay events in a distributed system (such as when trying to recover after a crash). If one node goes down, and we know the causal relationships between messages, then we can replay those messages and respect the causal relationship to get that node back up to the state it needs to be in.[[3]](./Lamport_timestamp#cite_note-3)

 

## Alternatives to potential causality

 

The happened-before relation captures potential causality, not true causality. In 2011–2012, [Munindar Singh](./Munindar_Singh) proposed a declarative, multiagent approach based on true causality called information protocols. An information protocol specifies the constraints on communications between the agents that constitute a distributed system.[[4]](./Lamport_timestamp#cite_note-4) However, instead of specifying message ordering (e.g., via a state machine, a common way of representing protocols in computing), an information protocol specifies the information dependencies between the communications that agents (the protocol's endpoints) may send. An agent may send a communication in a local state (its communication history) only if the communication and the state together satisfy the relevant information dependencies. For example, an information protocol for an e-commerce application may specify that to send a quote with parameters ID (a uniquifier), item, and price, seller must already know the ID and item from its state but can generate whatever price it wants. A remarkable thing about information protocols is that although emissions are constrained, receptions are not. Specifically, agents may receive communications in any order whatsoever –  receptions simply bring information and there is no point delaying them. This means that information protocols can be enacted over unordered communication services such as [UDP](./User_Datagram_Protocol).

 

The bigger idea is that of application semantics, the idea of designing distributed systems based on the content of the messages, an idea implicated in the [end-to-end principle](./End-to-end_principle). Current approaches largely ignore semantics and focus on providing application-agnostic ("syntactic") message delivery and ordering guarantees in communication services, which is where ideas like potential causality help. But if we had a suitable way of doing application semantics, then we wouldn't need such communication services. An unordered, unreliable communication service would suffice. The real value of the information protocols approach is that it provides the foundations for an application semantics approach.

 

## See also

 
- [Matrix clock](./Matrix_clock)
- [Vector clock](./Vector_clock)
- [Version vector](./Version_vector)

 

## References

 
1. [↑](./Lamport_timestamp#cite_ref-1) ["Distributed Systems 3rd edition (2017)"](https://www.distributed-systems.net/index.php/books/ds3/). *DISTRIBUTED-SYSTEMS.NET*. Retrieved 2021-03-20.
2. [1](./Lamport_timestamp#cite_ref-Lamport_1978_2-0) [2](./Lamport_timestamp#cite_ref-Lamport_1978_2-1) [Lamport, L.](./Leslie_Lamport) (1978). ["Time, clocks, and the ordering of events in a distributed system"](http://research.microsoft.com/users/lamport/pubs/time-clocks.pdf) (PDF). *[Communications of the ACM ](./Communications_of_the_ACM)*. **21** (7): 558–565. [doi](./Doi_(identifier)):[10.1145/359545.359563](https://doi.org/10.1145%2F359545.359563). [S2CID](./S2CID_(identifier)) [215822405](https://api.semanticscholar.org/CorpusID:215822405).
3. [↑](./Lamport_timestamp#cite_ref-3) George K. Thiruvathukal and Joe Kaylor (2013). ["Clocks and Synchronization"](https://web.archive.org/web/20190227181204/http://books.cs.luc.edu/distributedsystems/clocks.html). *Distributed Systems*. Archived from [the original](http://books.cs.luc.edu/distributedsystems/clocks.html) on 2019-02-27. Retrieved 2017-12-13.
4. [↑](./Lamport_timestamp#cite_ref-4) Munindar P. Singh (2011). ["Information-Driven Interaction-Oriented Programming: BSPL, the Blindingly Simple Protocol Language"](https://web.archive.org/web/20240413125733/http://www.csc2.ncsu.edu/faculty/mpsingh/papers/mas/AAMAS-11-IBIOP.pdf) (PDF). Archived from [the original](http://www.csc2.ncsu.edu/faculty/mpsingh/papers/mas/AAMAS-11-IBIOP.pdf) (PDF) on 2024-04-13. Retrieved 21 October 2025.