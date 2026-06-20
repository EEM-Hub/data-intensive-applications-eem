---
source: https://en.wikipedia.org/wiki/Conflict-free_replicated_data_type
fetched: 2026-06-19
---

Type of data structure "CRDT" redirects here. For Centenary Rural Development Trust, see [Centenary Bank](./Centenary_Bank). 

In [distributed computing](./Distributed_computing), a **conflict-free replicated data type** (**CRDT**) is a [data structure](./Data_structure) that is [replicated](./Replication_(computing)) across multiple computers in a [network](./Computer_network), with the following features:[[1]](./Conflict-free_replicated_data_type#cite_note-2011CRDT-1)[[2]](./Conflict-free_replicated_data_type#cite_note-2011CRDTSurvey-2)[[3]](./Conflict-free_replicated_data_type#cite_note-2007CRDTOriginal-3)[[4]](./Conflict-free_replicated_data_type#cite_note-OsterUrso2006-4)[[5]](./Conflict-free_replicated_data_type#cite_note-2009CRDT-5)[[6]](./Conflict-free_replicated_data_type#cite_note-2009CRDTTreedoc-6)[[7]](./Conflict-free_replicated_data_type#cite_note-1997scadt-7)[[8]](./Conflict-free_replicated_data_type#cite_note-Schneider-8)

 
1. The application can update any replica independently, [concurrently](./Concurrent_computing) and without [coordinating](./Concurrency_control) with other replicas.
2. An algorithm (itself part of the data type) automatically resolves any inconsistencies that might occur.
3. Although replicas may have different state at any particular point in time, they are guaranteed to eventually converge.

 

The CRDT concept was formally defined in 2011 by Marc Shapiro, Nuno Preguiça, Carlos Baquero and Marek Zawirski.[[9]](./Conflict-free_replicated_data_type#cite_note-CRDT_paper-9)  Development was initially motivated by [collaborative text editing](./Collaborative_real-time_editor) and [mobile computing](./Mobile_computing). CRDTs have also been used in [online chat](./Online_chat) systems, [online gambling](./Online_gambling), and in the [SoundCloud](./SoundCloud) audio distribution platform. The [NoSQL](./NoSQL) [distributed databases](./Distributed_databases) [Redis](./Redis), [Riak](./Riak) and [Cosmos DB](./Cosmos_DB) have CRDT data types.

 

## Background

 

Concurrent updates to multiple replicas of the same data, without coordination between the computers hosting the replicas, can result in [inconsistencies](./Consistency_(database_systems)) between the replicas, which in the general case may not be resolvable. Restoring consistency and [data integrity](./Data_integrity) when there are conflicts between updates may require some or all of the updates to be entirely or partially dropped.

 

Accordingly, much of distributed computing focuses on the problem of how to prevent concurrent updates to replicated data. But another possible approach is [optimistic replication](./Optimistic_replication), where all concurrent updates are allowed to go through, with inconsistencies possibly created, and the results are merged or "resolved" later. In this approach, consistency between the replicas is [eventually](./Eventual_consistency) re-established via "merges" of differing replicas.  While optimistic replication might not work in the general case, there is a significant and practically useful class of data structures, CRDTs, where it does work — where it is always possible to merge or resolve concurrent updates on different replicas of the data structure without conflicts.  This makes CRDTs ideal for optimistic replication.

 

As an example, a one-way [boolean](./Boolean_data_type) event flag is a trivial CRDT: one bit, with a value of true or false. True means some particular event has occurred at least once.  False means the event has not occurred.  Once set to true, the flag cannot be set back to false (an event having occurred cannot un-occur).  The resolution method is "true wins": when merging a replica where the flag is true (that replica has observed the event), and another one where the flag is false (that replica hasn't observed the event), the resolved result is true — the event has been observed.

 

## Types of CRDTs

 

There are two approaches to CRDTs, both of which can provide [strong eventual consistency](./Strong_eventual_consistency): state-based CRDTs[[10]](./Conflict-free_replicated_data_type#cite_note-1999StateBased-10)[[11]](./Conflict-free_replicated_data_type#cite_note-:1-11) and operation-based CRDTs.[[12]](./Conflict-free_replicated_data_type#cite_note-2010OpBased-12)[[13]](./Conflict-free_replicated_data_type#cite_note-:0-13)

 

### State-based CRDTs

 

State-based CRDTs (also called *convergent replicated data types*, or *CvRDTs*) are defined by two types, a type for local states and a type for actions on the state, together with three functions: a function to produce an *initial state*, a *merge* function of states, and a function to apply an action to *update* a state. State-based CRDTs simply send their full local state to other replicas on every update, where the received new state is then merged into the local state. To ensure eventual convergence the functions should fulfill the following properties:
The *merge* function should compute the [join](./Join_(mathematics)) for any pair of replica states, and should form a [semilattice](./Semilattice) with the initial state as the neutral element. In particular, this means that the merge function must be [commutative](./Commutative), [associative](./Associative), and [idempotent](./Idempotent). The intuition behind commutativity, associativity and idempotence is that these properties are used to make the CRDT invariant under package re-ordering and duplication. Furthermore, the *update* function must be [monotone](./Monotonic_function) with regard to the [partial order](./Partial_order) defined by said semilattice.

 

*Delta state* CRDTs[[11]](./Conflict-free_replicated_data_type#cite_note-:1-11)[[14]](./Conflict-free_replicated_data_type#cite_note-Almeida-14) (or simply delta CRDTs) are optimized state-based CRDTs where only recently applied changes to a state are disseminated instead of the entire state.

 

### Operation-based CRDTs

 

Operation-based CRDTs (also called *commutative replicated data types*, or *CmRDTs*) are defined without a merge function. Instead of transmitting states, the update actions are transmitted directly to replicas and applied. For example, an operation-based CRDT of a single integer might broadcast the operations “+10” or “−20”. The application of operations should still be [commutative](./Commutative) and [associative](./Associative). However, instead of requiring that application of operations is [idempotent](./Idempotent), stronger assumptions on the communications infrastructure are expected — all operations must be delivered to the other replicas without duplication.

 

*Pure* operation-based CRDTs[[13]](./Conflict-free_replicated_data_type#cite_note-:0-13) are a variant of operation-based CRDTs that reduces the metadata size.

 

### Comparison

 

The two alternatives are theoretically equivalent, as each can emulate the other.[[1]](./Conflict-free_replicated_data_type#cite_note-2011CRDT-1) However, there are practical differences. State-based CRDTs are often simpler to design and to implement; their only requirement from the communication substrate is some kind of [gossip protocol](./Gossip_protocol). Their drawback is that the entire state of every CRDT must be transmitted eventually to every other replica, which may be costly. In contrast, operation-based CRDTs transmit only the update operations, which are typically small. However, operation-based CRDTs require guarantees from the [communication middleware](./Communications_protocol); that the operations are not dropped or duplicated when transmitted to the other replicas, and that they are delivered in [causal order](./Causal_order?action=edit&redlink=1).[[1]](./Conflict-free_replicated_data_type#cite_note-2011CRDT-1)

 

While operations-based CRDTs place more requirements on the protocol for transmitting operations between replicas, they use less bandwidth than state-based CRDTs when the number of transactions is small in comparison to the size of internal state. However, since the state-based CRDT merge function is associative, merging with the state of some replica yields all previous updates to that replica. Gossip protocols work well for propagating state-based CRDT state to other replicas while reducing network use and handling topology changes.

 

Some lower bounds[[15]](./Conflict-free_replicated_data_type#cite_note-Burckhardt-15) on the storage complexity of state-based CRDTs are known.

 

## Known CRDTs

 

### G-Counter (Grow-only Counter)

 
```
payload integer[n] P
    initial [0,0,...,0]

update ''increment''()
    let g = ''myId''()
    P[g] := P[g] + 1

query ''value''() : integer v
    let v = Σi P[i]

compare (X, Y) : boolean b
    let b = (∀i ∈ [0, n - 1] : X.P[i] ≤ Y.P[i])

merge (X, Y) : payload Z
    let ∀i ∈ [0, n - 1] : Z.P[i] = ''max''(X.P[i], Y.P[i])
```
 

This state-based CRDT implements a counter for a cluster of ***n*** nodes. Each node in the cluster is assigned an ID from 0 to ***n*** - 1, which is retrieved with a call to `myId()`. Thus each node is assigned its own slot in the array ***P***, which it increments locally. Updates are propagated in the background, and merged by taking the `max()` of every element in ***P***. The compare function is included to illustrate a partial order on the states. The merge function is commutative, associative, and idempotent. The update function monotonically increases the internal state according to the compare function. This is thus a correctly defined state-based CRDT and will provide strong eventual consistency. The operations-based CRDT equivalent broadcasts increment operations as they are received.[[2]](./Conflict-free_replicated_data_type#cite_note-2011CRDTSurvey-2)

 

### PN-Counter (Positive-Negative Counter)

 
```
payload integer[n] P, integer[n] N
    initial [0,0,...,0], [0,0,...,0]
update ''increment''()
    let g = ''myId''()
    P[g] := P[g] + 1
update ''decrement''()
    let g = ''myId''()
    N[g] := N[g] + 1
query ''value''() : integer v
    let v = Σi P[i] - Σi N[i]
compare (X, Y) : boolean b
    let b = (∀i ∈ [0, n - 1] : X.P[i] ≤ Y.P[i] ∧ ∀i ∈ [0, n - 1] : X.N[i] ≤ Y.N[i])
merge (X, Y) : payload Z
    let ∀i ∈ [0, n - 1] : Z.P[i] = ''max''(X.P[i], Y.P[i])
    let ∀i ∈ [0, n - 1] : Z.N[i] = ''max''(X.N[i], Y.N[i])
```
 

A common strategy in CRDT development is to combine multiple CRDTs to make a more complex CRDT. In this case, two G-Counters are combined to create a data type supporting both increment and decrement operations. The "P" G-Counter counts increments; and the "N" G-Counter counts decrements.  The value of the PN-Counter is the value of the P counter minus the value of the N counter.  Merge is handled by letting the merged P counter be the merge of the two P G-Counters, and similarly for N counters.  Note that the CRDT's internal state must increase monotonically, even though its external state as exposed through *query* can return to previous values.[[2]](./Conflict-free_replicated_data_type#cite_note-2011CRDTSurvey-2)

 

### G-Set (Grow-only Set)

 
```
payload set A
    initial ∅
update ''add''(element e)
    A := A ∪ {e}
query ''lookup''(element e) : boolean b
    let b = (e ∈ A)
compare (S, T) : boolean b
    let b = (S.A ⊆ T.A)
merge (S, T) : payload U
    let U.A = S.A ∪ T.A
```
 

The G-Set (grow-only set) is a set which only allows adds. An element, once added, cannot be removed.  The merger of two G-Sets is their union.[[2]](./Conflict-free_replicated_data_type#cite_note-2011CRDTSurvey-2)

 

### 2P-Set (Two-Phase Set)

 
```
payload set A, set R
    initial ∅, ∅
query ''lookup''(element e) : boolean b
    let b = (e ∈ A ∧ e ∉ R)
update ''add''(element e)
    A := A ∪ {e}
update ''remove''(element e)
    pre ''lookup''(e)
    R := R ∪ {e}
compare (S, T) : boolean b
    let b = (S.A ⊆ T.A ∨ S.R ⊆ T.R)
merge (S, T) : payload U
    let U.A = S.A ∪ T.A
    let U.R = S.R ∪ T.R
```
 

Two G-Sets (grow-only sets) are combined to create the 2P-set. With the addition of a remove set (called the "tombstone" set), elements can be added and also removed.  Once removed, an element cannot be re-added; that is, once an element ***e*** is in the tombstone set, **query** will never again return True for that element. The 2P-set uses "remove-wins" semantics, so `remove(e)` takes precedence over `add(e)`.[[2]](./Conflict-free_replicated_data_type#cite_note-2011CRDTSurvey-2)

 

### LWW-Element-Set (Last-Write-Wins-Element-Set)

 

LWW-Element-Set is similar to 2P-Set in that it consists of an "add set" and a "remove set", with a timestamp for each element.   Elements are added to an LWW-Element-Set by inserting the element into the add set, with a timestamp.   Elements are removed from the LWW-Element-Set by being added to the remove set, again with a timestamp.  An element is a member of the LWW-Element-Set if it is in the add set, and either not in the remove set, or in the remove set but with an earlier timestamp than the latest timestamp in the add set.   Merging two replicas of the LWW-Element-Set consists of taking the union of the add sets and the union of the remove sets.   When timestamps are equal, the "bias" of the LWW-Element-Set comes into play.  A LWW-Element-Set can be biased towards additions or removals.  The advantage of LWW-Element-Set over 2P-Set is that, unlike 2P-Set, LWW-Element-Set allows an element to be reinserted after having been removed.[[2]](./Conflict-free_replicated_data_type#cite_note-2011CRDTSurvey-2)

 

### OR-Set (Observed-Remove Set)

 

OR-Set resembles LWW-Element-Set, but using unique tags instead of timestamps. For each element in the set, a list of add-tags and a list of remove-tags are maintained.  An element is inserted into the OR-Set by having a new unique tag generated and added to the add-tag list for the element.   Elements are removed from the OR-Set by having all the tags in the element's add-tag list added to the element's remove-tag (tombstone) list. To merge two OR-Sets, for each element, let its add-tag list be the union of the two add-tag lists, and likewise for the two remove-tag lists. An element is a member of the set if and only if the add-tag list less the remove-tag list is nonempty.[[2]](./Conflict-free_replicated_data_type#cite_note-2011CRDTSurvey-2) An optimization that eliminates the need for maintaining a tombstone set is possible; this avoids the potentially unbounded growth of the tombstone set. The optimization is achieved by maintaining a vector of timestamps for each replica.[[16]](./Conflict-free_replicated_data_type#cite_note-16)

 

### Sequence CRDTs

 

A sequence, list, or [ordered set](./Ordered_set) CRDT can be used to build a [collaborative real-time editor](./Collaborative_real-time_editor), as an alternative to [operational transformation](./Operational_transformation) (OT).

 

Some known Sequence CRDTs are Treedoc,[[5]](./Conflict-free_replicated_data_type#cite_note-2009CRDT-5) 
RGA,[[17]](./Conflict-free_replicated_data_type#cite_note-Roh-JPDC-2011-17) Woot,[[4]](./Conflict-free_replicated_data_type#cite_note-OsterUrso2006-4) 
Logoot,[[18]](./Conflict-free_replicated_data_type#cite_note-WeissUrso2010-18) and LSEQ.[[19]](./Conflict-free_replicated_data_type#cite_note-NédelecMolli2013-19)
CRATE[[20]](./Conflict-free_replicated_data_type#cite_note-Nédelec2016-20) is a decentralized real-time editor built on top of LSEQSplit (an extension of LSEQ) and runnable on a network of browsers using [WebRTC](./WebRTC).
LogootSplit [[21]](./Conflict-free_replicated_data_type#cite_note-Andre2013-21) was proposed as an extension of Logoot in order to reduce the metadata for sequence CRDTs. MUTE [[22]](./Conflict-free_replicated_data_type#cite_note-MUTE-22)[[23]](./Conflict-free_replicated_data_type#cite_note-Nicolas2017-23) is an online web-based peer-to-peer real-time collaborative editor relying on the LogootSplit algorithm.

 

Industrial sequence CRDTs, including open-source ones, are known to out-perform academic implementations due to optimizations and a more realistic testing methodology.[[24]](./Conflict-free_replicated_data_type#cite_note-Gentle2021-24) The main popular example is Yjs CRDT, a pioneer in using a plainlist instead of a tree (ala Kleppmann's *automerge*).[[25]](./Conflict-free_replicated_data_type#cite_note-25)

 

## Industry use

 
- [Fluid Framework](./Fluid_Framework) is an open-source collaborative platform built by [Microsoft](./Microsoft) that provides both server reference implementations and client-side SDKs for creating modern [real-time web](./Real-time_web) applications using CRDTs.
- [Nimbus Note](./Nimbus_Note) is a collaborative note-taking application that uses the Yjs CRDT for collaborative editing.[[26]](./Conflict-free_replicated_data_type#cite_note-26)
- [Redis](./Redis) is a distributed, highly available, and scalable [in-memory database](./In-memory_database) with a "CRDT-enabled database" feature.[[27]](./Conflict-free_replicated_data_type#cite_note-27)
- [SoundCloud](./SoundCloud) open-sourced Roshi, a LWW-element-set CRDT for the SoundCloud stream implemented on top of Redis.[[28]](./Conflict-free_replicated_data_type#cite_note-Roshi-28)
- [Riak](./Riak) is a distributed NoSQL key-value [data store](./Data_store) based on CRDTs.[[29]](./Conflict-free_replicated_data_type#cite_note-Riak-29) *[League of Legends](./League_of_Legends)* uses the Riak CRDT implementation for its in-game chat system, which handles 7.5 million concurrent users and 11,000 messages per second.[[30]](./Conflict-free_replicated_data_type#cite_note-LoL-30)
- [Bet365](./Bet365) stores hundreds of megabytes of data in the Riak implementation of OR-Set.[[31]](./Conflict-free_replicated_data_type#cite_note-bet365-31)
- [TomTom](./TomTom) employs CRDTs to synchronize navigation data between the devices of a user.[[32]](./Conflict-free_replicated_data_type#cite_note-TomTom-32)
- [Phoenix](./Phoenix_(web_framework)), a [web framework](./Web_framework) written in [Elixir](./Elixir_(programming_language)), uses CRDTs to support real-time multi-node information sharing in version 1.2.[[33]](./Conflict-free_replicated_data_type#cite_note-Phoenix-33)
- [Facebook](./Facebook) implements CRDTs in their Apollo low-latency "consistency at scale" database.[[34]](./Conflict-free_replicated_data_type#cite_note-Apollo-34)
- [Facebook](./Facebook) uses CRDTs in their FlightTracker system for managing the Facebook graph internally.[[35]](./Conflict-free_replicated_data_type#cite_note-FlightTracker-35)
- Teletype for [Atom](./Atom_(text_editor)) employs CRDTs to enable developers share their workspace with team members and collaborate on code in real time.[[36]](./Conflict-free_replicated_data_type#cite_note-atom_teletype-36)
- [Apple](./Apple_Inc.) implements CRDTs in the Notes app for syncing offline edits between multiple devices.[[37]](./Conflict-free_replicated_data_type#cite_note-37)
- [Novell, Inc.](./Novell) introduced a state-based CRDT with "loosely consistent" directory replication ([NetWare](./NetWare) Directory Services), included in NetWare 4.0 in 1995.[[38]](./Conflict-free_replicated_data_type#cite_note-38) The successor product, eDirectory, delivered improvements to the replication process.[[39]](./Conflict-free_replicated_data_type#cite_note-39)
- [Figma](./Figma)'s real-time multiplayer editing uses a server-authoritative, per-property last-writer-wins replication scheme (akin to an LWW register in CRDT literature); for ordered sequences (e.g., layer ordering) it uses fractional indexing with server tie-breaking for concurrent inserts (rather than [operational transformation](./Operational_transformation)-style transforms).[[40]](./Conflict-free_replicated_data_type#cite_note-40)[[41]](./Conflict-free_replicated_data_type#cite_note-41)

 

## See also

 
- [Data synchronization](./Data_synchronization)
- [Collaborative real-time editors](./Collaborative_real-time_editor)
- [Consistency models](./Consistency_model)
- [Optimistic replication](./Optimistic_replication)
- [Operational transformation](./Operational_transformation)
- [Self-stabilizing algorithms](./Self-stabilization)

 

## References

 
1. [1](./Conflict-free_replicated_data_type#cite_ref-2011CRDT_1-0) [2](./Conflict-free_replicated_data_type#cite_ref-2011CRDT_1-1) [3](./Conflict-free_replicated_data_type#cite_ref-2011CRDT_1-2)  Shapiro, Marc; Preguiça, Nuno; Baquero, Carlos; Zawirski, Marek (2011). "Conflict-Free Replicated Data Types". [*Stabilization, Safety, and Security of Distributed Systems*](https://hal.inria.fr/hal-00932836/file/CRDTs_SSS-2011.pdf) (PDF). Lecture Notes in Computer Science. Vol. 6976. Grenoble, France: Springer Berlin Heidelberg. pp. 386–400. [doi](./Doi_(identifier)):[10.1007/978-3-642-24550-3_29](https://doi.org/10.1007%2F978-3-642-24550-3_29). [ISBN](./ISBN_(identifier)) [978-3-642-24549-7](./Special:BookSources/978-3-642-24549-7). [S2CID](./S2CID_(identifier)) [51995307](https://api.semanticscholar.org/CorpusID:51995307). 
2. [1](./Conflict-free_replicated_data_type#cite_ref-2011CRDTSurvey_2-0) [2](./Conflict-free_replicated_data_type#cite_ref-2011CRDTSurvey_2-1) [3](./Conflict-free_replicated_data_type#cite_ref-2011CRDTSurvey_2-2) [4](./Conflict-free_replicated_data_type#cite_ref-2011CRDTSurvey_2-3) [5](./Conflict-free_replicated_data_type#cite_ref-2011CRDTSurvey_2-4) [6](./Conflict-free_replicated_data_type#cite_ref-2011CRDTSurvey_2-5) [7](./Conflict-free_replicated_data_type#cite_ref-2011CRDTSurvey_2-6)  Shapiro, Marc; Preguiça, Nuno; Baquero, Carlos; Zawirski, Marek (13 January 2011). "A Comprehensive Study of Convergent and Commutative Replicated Data Types". *Rr-7506*. 
3. [↑](./Conflict-free_replicated_data_type#cite_ref-2007CRDTOriginal_3-0)  Shapiro, Marc; Preguiça, Nuno (2007). "Designing a Commutative Replicated Data Type". [arXiv](./ArXiv_(identifier)):[0710.1784](https://arxiv.org/abs/0710.1784) [[cs.DC](https://arxiv.org/archive/cs.DC)].
4. [1](./Conflict-free_replicated_data_type#cite_ref-OsterUrso2006_4-0) [2](./Conflict-free_replicated_data_type#cite_ref-OsterUrso2006_4-1) Oster, Gérald; Urso, Pascal; Molli, Pascal; Imine, Abdessamad (2006). *Proceedings of the 2006 20th anniversary conference on Computer supported cooperative work - CSCW '06*. p. 259. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.554.3168](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.554.3168). [doi](./Doi_(identifier)):[10.1145/1180875.1180916](https://doi.org/10.1145%2F1180875.1180916). [ISBN](./ISBN_(identifier)) [978-1595932495](./Special:BookSources/978-1595932495). [S2CID](./S2CID_(identifier)) [14596943](https://api.semanticscholar.org/CorpusID:14596943).
5. [1](./Conflict-free_replicated_data_type#cite_ref-2009CRDT_5-0) [2](./Conflict-free_replicated_data_type#cite_ref-2009CRDT_5-1)  Letia, Mihai; Preguiça, Nuno; Shapiro, Marc (2009). "CRDTs: Consistency without Concurrency Control". *Computing Research Repository*. [arXiv](./ArXiv_(identifier)):[0907.0929](https://arxiv.org/abs/0907.0929).
6. [↑](./Conflict-free_replicated_data_type#cite_ref-2009CRDTTreedoc_6-0)  Preguiça, Nuno; Marques, Joan Manuel; Shapiro, Marc; Letia, Mihai (June 2009), ["A Commutative Replicated Data Type for Cooperative Editing"](https://hal.inria.fr/inria-00445975/file/icdcs09-treedoc.pdf) (PDF), [*Proc 29th IEEE International Conference on Distributed Computing Systems*](https://inria.hal.science/inria-00445975), Montreal, Quebec, Canada: IEEE Computer Society, pp. 395–403, [doi](./Doi_(identifier)):[10.1109/ICDCS.2009.20](https://doi.org/10.1109%2FICDCS.2009.20), [ISBN](./ISBN_(identifier)) [978-0-7695-3659-0](./Special:BookSources/978-0-7695-3659-0), [S2CID](./S2CID_(identifier)) [8956372](https://api.semanticscholar.org/CorpusID:8956372)
7. [↑](./Conflict-free_replicated_data_type#cite_ref-1997scadt_7-0)  Baquero, Carlos; Moura, Francisco (1997), *Specification of Convergent Abstract Data Types for Autonomous Mobile Computing*, Universidade do Minho
8. [↑](./Conflict-free_replicated_data_type#cite_ref-Schneider_8-0)  Schneider, Fred (December 1990). ["Implementing Fault-Tolerant Services Using the State Machine Approach: A Tutorial"](https://doi.org/10.1145%2F98163.98167). *ACM Computing Surveys*. **22** (4): 299–319. [doi](./Doi_(identifier)):[10.1145/98163.98167](https://doi.org/10.1145%2F98163.98167). [S2CID](./S2CID_(identifier)) [678818](https://api.semanticscholar.org/CorpusID:678818).
9. [↑](./Conflict-free_replicated_data_type#cite_ref-CRDT_paper_9-0)  ["Conflict-free Replicated Data Types"](https://hal.science/inria-00609399). inria.fr. July 19, 2011. 
10. [↑](./Conflict-free_replicated_data_type#cite_ref-1999StateBased_10-0)  Baquero, Carlos; Moura, Francisco (1 October 1999). "Using Structural Characteristics for Autonomous Operation". *SIGOPS Oper. Syst. Rev*. **33** (4): 90–96. [doi](./Doi_(identifier)):[10.1145/334598.334614](https://doi.org/10.1145%2F334598.334614). [hdl](./Hdl_(identifier)):[1822/34984](https://hdl.handle.net/1822%2F34984). [S2CID](./S2CID_(identifier)) [13882850](https://api.semanticscholar.org/CorpusID:13882850). 
11. [1](./Conflict-free_replicated_data_type#cite_ref-:1_11-0) [2](./Conflict-free_replicated_data_type#cite_ref-:1_11-1)  Almeida, Paulo Sérgio; Shoker, Ali; Baquero, Carlos (2015-05-13). "Efficient State-Based CRDTS by Delta-Mutation". In Bouajjani, Ahmed; Fauconnier, Hugues (eds.). *Networked Systems*. Lecture Notes in Computer Science. Vol. 9466. Springer International Publishing. pp. 62–76. [arXiv](./ArXiv_(identifier)):[1410.2803](https://arxiv.org/abs/1410.2803). [doi](./Doi_(identifier)):[10.1007/978-3-319-26850-7_5](https://doi.org/10.1007%2F978-3-319-26850-7_5). [ISBN](./ISBN_(identifier)) [9783319268491](./Special:BookSources/9783319268491). [S2CID](./S2CID_(identifier)) [7852769](https://api.semanticscholar.org/CorpusID:7852769).
12. [↑](./Conflict-free_replicated_data_type#cite_ref-2010OpBased_12-0)  Letia, Mihai; Preguiça, Nuno; Shapiro, Marc (1 April 2010). ["Consistency without Concurrency Control in Large, Dynamic Systems"](https://hal.inria.fr/hal-01248270/file/LS-consistency-ladis-2009.pdf) (PDF). *SIGOPS Oper. Syst. Rev*. **44** (2): 29–34. [doi](./Doi_(identifier)):[10.1145/1773912.1773921](https://doi.org/10.1145%2F1773912.1773921). [S2CID](./S2CID_(identifier)) [6255174](https://api.semanticscholar.org/CorpusID:6255174). 
13. [1](./Conflict-free_replicated_data_type#cite_ref-:0_13-0) [2](./Conflict-free_replicated_data_type#cite_ref-:0_13-1)  Baquero, Carlos; Almeida, Paulo Sérgio; Shoker, Ali (2014-06-03). "Making Operation-Based CRDTS Operation-Based". In Magoutis, Kostas; Pietzuch, Peter (eds.). *Distributed Applications and Interoperable Systems*. Lecture Notes in Computer Science. Vol. 8460. Springer Berlin Heidelberg. pp. 126–140. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.492.8742](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.492.8742). [doi](./Doi_(identifier)):[10.1007/978-3-662-43352-2_11](https://doi.org/10.1007%2F978-3-662-43352-2_11). [ISBN](./ISBN_(identifier)) [9783662433515](./Special:BookSources/9783662433515).
14. [↑](./Conflict-free_replicated_data_type#cite_ref-Almeida_14-0)  Almeida, Paulo Sérgio; Shoker, Ali; Baquero, Carlos (2016-03-04). "Delta State Replicated Data Types". *Journal of Parallel and Distributed Computing*. **111**: 162–173. [arXiv](./ArXiv_(identifier)):[1603.01529](https://arxiv.org/abs/1603.01529). [doi](./Doi_(identifier)):[10.1016/j.jpdc.2017.08.003](https://doi.org/10.1016%2Fj.jpdc.2017.08.003). [S2CID](./S2CID_(identifier)) [7990602](https://api.semanticscholar.org/CorpusID:7990602).
15. [↑](./Conflict-free_replicated_data_type#cite_ref-Burckhardt_15-0)  Burckhardt, Sebastian; Gotsman, Alexey; Yang, Hongseok; Zawirski, Marek (23 January 2014). "Replicated Data Types: Specification, Verification, Optimality". [*Proceedings of the 41st ACM SIGPLAN-SIGACT Symposium on Principles of Programming Languages*](https://hal.inria.fr/hal-00934311/file/Replicated_Data_Types-_Specification_Verification_Optimality_Marek_Alexey_Burckhardt_popl14.pdf) (PDF). pp. 271–284. [doi](./Doi_(identifier)):[10.1145/2535838.2535848](https://doi.org/10.1145%2F2535838.2535848). [ISBN](./ISBN_(identifier)) [9781450325448](./Special:BookSources/9781450325448). [S2CID](./S2CID_(identifier)) [15023909](https://api.semanticscholar.org/CorpusID:15023909). 
16. [↑](./Conflict-free_replicated_data_type#cite_ref-16) Bieniusa, Annette; Zawirski, Marek; Preguiça, Nuno; Shapiro, Marc; Baquero, Carlos; Balegas, Valter; Duarte, Sérgio (2012). "An optimized conflict-free replicated set". [arXiv](./ArXiv_(identifier)):[1210.3368](https://arxiv.org/abs/1210.3368) [[cs.DC](https://arxiv.org/archive/cs.DC)].
17. [↑](./Conflict-free_replicated_data_type#cite_ref-Roh-JPDC-2011_17-0) Roh, Huyn-Gul; Jeon, Myeongjae; Kim, Jin-Soo; Lee, Joonwon (2011). "Replicated Abstract Data Types: Building Blocks for Collaborative Applications". *Journal of Parallel and Distributed Computing*. **71** (2): 354–368. [doi](./Doi_(identifier)):[10.1016/j.jpdc.2010.12.006](https://doi.org/10.1016%2Fj.jpdc.2010.12.006).
18. [↑](./Conflict-free_replicated_data_type#cite_ref-WeissUrso2010_18-0)  Weiss, Stephane; Urso, Pascal; Molli, Pascal (2010). "Logoot-Undo: Distributed Collaborative Editing System on P2P Networks". *IEEE Transactions on Parallel and Distributed Systems*. **21** (8): 1162–1174. [Bibcode](./Bibcode_(identifier)):[2010ITPDS..21.1162W](https://ui.adsabs.harvard.edu/abs/2010ITPDS..21.1162W). [doi](./Doi_(identifier)):[10.1109/TPDS.2009.173](https://doi.org/10.1109%2FTPDS.2009.173). [ISSN](./ISSN_(identifier)) [1045-9219](https://search.worldcat.org/issn/1045-9219). [S2CID](./S2CID_(identifier)) [14172605](https://api.semanticscholar.org/CorpusID:14172605).
19. [↑](./Conflict-free_replicated_data_type#cite_ref-NédelecMolli2013_19-0)  Nédelec, Brice; Molli, Pascal; Mostefaoui, Achour; Desmontils, Emmanuel (2013). "LSEQ: An adaptive structure for sequences in distributed collaborative editing". [*Proceedings of the 2013 ACM symposium on Document engineering*](https://hal.archives-ouvertes.fr/hal-00921633/file/fp025-nedelec.pdf) (PDF). pp. 37–46. [doi](./Doi_(identifier)):[10.1145/2494266.2494278](https://doi.org/10.1145%2F2494266.2494278). [ISBN](./ISBN_(identifier)) [9781450317894](./Special:BookSources/9781450317894). [S2CID](./S2CID_(identifier)) [9215663](https://api.semanticscholar.org/CorpusID:9215663).
20. [↑](./Conflict-free_replicated_data_type#cite_ref-Nédelec2016_20-0) Nédelec, Brice; Molli, Pascal; Mostefaoui, Achour (2016). "CRATE: Writing Stories Together with our Browsers". [*Proceedings of the 25th International Conference Companion on World Wide Web*](https://web.archive.org/web/20200101022752/https://hal.archives-ouvertes.fr/hal-01303333/document). p. 231. [doi](./Doi_(identifier)):[10.1145/2872518.2890539](https://doi.org/10.1145%2F2872518.2890539). [S2CID](./S2CID_(identifier)) [5096789](https://api.semanticscholar.org/CorpusID:5096789). Archived from [the original](https://hal.archives-ouvertes.fr/hal-01303333/document) on 2020-01-01. Retrieved 2020-01-01.
21. [↑](./Conflict-free_replicated_data_type#cite_ref-Andre2013_21-0)  André, Luc; Martin, Stéphane; Oster, Gérald; Ignat, Claudia-Lavinia (2013). "Supporting Adaptable Granularity of Changes for Massive-scale Collaborative Editing". *Proceedings of the International Conference on Collaborative Computing: Networking, Applications and Worksharing – CollaborateCom 2013*. pp. 50–59. [doi](./Doi_(identifier)):[10.4108/icst.collaboratecom.2013.254123](https://doi.org/10.4108%2Ficst.collaboratecom.2013.254123). [ISBN](./ISBN_(identifier)) [978-1-936968-92-3](./Special:BookSources/978-1-936968-92-3).
22. [↑](./Conflict-free_replicated_data_type#cite_ref-MUTE_22-0)  ["MUTE"](https://coedit.re/). Coast Team. March 24, 2016. 
23. [↑](./Conflict-free_replicated_data_type#cite_ref-Nicolas2017_23-0)  Nicolas, Matthieu; Elvinger, Victorien; Oster, Gérald; Ignat, Claudia-Lavinia; Charoy, François (2017). "MUTE: A Peer-to-Peer Web-based Real-time Collaborative Editor". *Proceedings of ECSCW Panels, Demos and Posters 2017*. [doi](./Doi_(identifier)):[10.18420/ecscw2017_p5](https://doi.org/10.18420%2Fecscw2017_p5). [S2CID](./S2CID_(identifier)) [43984228](https://api.semanticscholar.org/CorpusID:43984228).
24. [↑](./Conflict-free_replicated_data_type#cite_ref-Gentle2021_24-0) Gentle, Seph. ["Faster CRDTs: An Adventure in Optimization"](https://josephg.com/blog/crdts-go-brrr/). *josephg.com*. Retrieved 1 August 2021.
25. [↑](./Conflict-free_replicated_data_type#cite_ref-25) ["yjs/yjs: Shared data types for building collaborative software"](https://github.com/yjs/yjs). *GitHub*.
26. [↑](./Conflict-free_replicated_data_type#cite_ref-26) ["About CRDTs"](https://crdt.tech/implementations#yjs-users). Retrieved 2020-06-18.
27. [↑](./Conflict-free_replicated_data_type#cite_ref-27) ["Diving into CRDTs"](https://redis.io/blog/diving-into-crdts/). *[Redis](./Redis)*. 17 March 2022. Retrieved 2024-05-22.
28. [↑](./Conflict-free_replicated_data_type#cite_ref-Roshi_28-0)  Bourgon, Peter (9 May 2014). ["Roshi: a CRDT system for timestamped events"](https://developers.soundcloud.com/blog/roshi-a-crdt-system-for-timestamped-events). SoundCloud. 
29. [↑](./Conflict-free_replicated_data_type#cite_ref-Riak_29-0)  ["Introducing Riak 2.0: Data Types, Strong Consistency, Full-Text Search, and Much More"](http://basho.com/introducing-riak-2-0/). Basho Technologies, Inc. 29 October 2013. 
30. [↑](./Conflict-free_replicated_data_type#cite_ref-LoL_30-0)  Hoff, Todd (13 October 2014). ["How League of Legends Scaled Chat to 70 Million Players - It Takes Lots of Minions"](http://highscalability.com/blog/2014/10/13/how-league-of-legends-scaled-chat-to-70-million-players-it-t.html). *High Scalability*. 
31. [↑](./Conflict-free_replicated_data_type#cite_ref-bet365_31-0)  Macklin, Dan. ["bet365: Why bet365 chose Riak"](http://basho.com/bet365/). Basho. 
32. [↑](./Conflict-free_replicated_data_type#cite_ref-TomTom_32-0)  Ivanov, Dmitry. ["Practical Demystification of CRDTs"](https://speakerdeck.com/ajantis/practical-demystification-of-crdts). 
33. [↑](./Conflict-free_replicated_data_type#cite_ref-Phoenix_33-0)  McCord, Chris (25 March 2016). ["What makes Phoenix Presence Special"](https://dockyard.com/blog/2016/03/25/what-makes-phoenix-presence-special-sneak-peek). 
34. [↑](./Conflict-free_replicated_data_type#cite_ref-Apollo_34-0)  Mak, Sander. ["Facebook Announces Apollo at QCon NY 2014"](https://dzone.com/articles/facebook-announces-apollo-qcon). 
35. [↑](./Conflict-free_replicated_data_type#cite_ref-FlightTracker_35-0) ["FlightTracker: Consistency across Read-Optimized Online Stores at Facebook"](https://research.facebook.com/publications/flighttracker-consistency-across-read-optimized-online-stores-at-facebook/). research.facebook.com. Retrieved 8 December 2022.
36. [↑](./Conflict-free_replicated_data_type#cite_ref-atom_teletype_36-0)  ["Code together in real time with Teletype for Atom"](https://blog.atom.io/2017/11/15/code-together-in-real-time-with-teletype-for-atom.html). Atom.io. November 15, 2017. 
37. [↑](./Conflict-free_replicated_data_type#cite_ref-37) ["IOS Objective-C headers as derived from runtime introspection: NST/IOS-Runtime-Headers"](https://github.com/nst/iOS-Runtime-Headers/blob/master/PrivateFrameworks/NotesShared.framework/TTMergeableString.h). *[GitHub](./GitHub)*. 2019-07-25.
38. [↑](./Conflict-free_replicated_data_type#cite_ref-38) ["Understanding NetWare Directory Services"](https://support.novell.com/techcenter/articles/dnd19950101.html). *support.novell.com*. Retrieved 2024-11-02.
39. [↑](./Conflict-free_replicated_data_type#cite_ref-39) ["eDirectory Synchronization and Background Processes"](https://support.novell.com/techcenter/articles/anp20021101.html). *support.novell.com*. Retrieved 2024-11-02.
40. [↑](./Conflict-free_replicated_data_type#cite_ref-40) ["How Figma's multiplayer technology works"](https://www.figma.com/blog/how-figmas-multiplayer-technology-works/). *Figma Blog*. Retrieved 2026-01-02.
41. [↑](./Conflict-free_replicated_data_type#cite_ref-41) ["Realtime Editing of Ordered Sequences"](https://www.figma.com/blog/realtime-editing-of-ordered-sequences/). *Figma Blog*. Retrieved 2026-01-02.

 

## External links

 
- [A collection of resources and papers on CRDTs](https://crdt.tech/)
- ["Strong Eventual Consistency and Conflict-free Replicated Data Types" (A talk on CRDTs)](https://archive.org/details/Microsoft_Research_Video_153540) by Marc Shapiro
- [Readings in conflict-free replicated data types](http://christophermeiklejohn.com/crdt/2014/07/22/readings-in-crdts.html) by Christopher Meiklejohn
- [CAP theorem and CRDTs: CAP 12 years later. How the rules have changed ](https://www.infoq.com/articles/cap-twelve-years-later-how-the-rules-have-changed) by Eric Brewer