---
source: https://en.wikipedia.org/wiki/Happened-before
fetched: 2026-06-19
---

Relation between two events in computer science 

In [computer science](./Computer_science), the **happened-before** [relation](./Binary_relation) (denoted:     → →     {\displaystyle \to \;}  ![{\displaystyle \to \;}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3806fd5a395550c9e85c0aeabd8c3196e223ede5)) is a relation between the result of two events, such that if one event should happen before another event, the result must reflect that, even if those events are in reality executed out of order (usually to optimize program flow). This involves [ordering](./Partially_ordered_set) events based on the potential [causal relationship](./Causal_relationships) of pairs of events in a concurrent system, especially [asynchronous](./Asynchronous_communication) [distributed systems](./Distributed_systems). It was formulated by [Leslie Lamport](./Leslie_Lamport).[[1]](./Happened-before#cite_note-1)

 

The happened-before relation is formally defined as the least [strict partial order](./Strict_partial_order) on events such that:

 
- If events     a    {\displaystyle a\;}  ![{\displaystyle a\;}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ac43f811d675e91eb98db33b8d59ed11866220a1) and     b    {\displaystyle b\;}  ![{\displaystyle b\;}](https://wikimedia.org/api/rest_v1/media/math/render/svg/636dcf8d0b14c23e87a35c672d3939936dab5671) occur on the same process,     a → →  b    {\displaystyle a\to b\;}  ![{\displaystyle a\to b\;}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0eb4e39f0dd0e749e2562b6d5b1a2421dea7ad9a) if the occurrence of event     a    {\displaystyle a\;}  ![{\displaystyle a\;}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ac43f811d675e91eb98db33b8d59ed11866220a1) preceded the occurrence of event     b    {\displaystyle b\;}  ![{\displaystyle b\;}](https://wikimedia.org/api/rest_v1/media/math/render/svg/636dcf8d0b14c23e87a35c672d3939936dab5671).
- If event     a    {\displaystyle a\;}  ![{\displaystyle a\;}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ac43f811d675e91eb98db33b8d59ed11866220a1) is the sending of a message and event     b    {\displaystyle b\;}  ![{\displaystyle b\;}](https://wikimedia.org/api/rest_v1/media/math/render/svg/636dcf8d0b14c23e87a35c672d3939936dab5671) is the reception of the message sent in event     a    {\displaystyle a\;}  ![{\displaystyle a\;}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ac43f811d675e91eb98db33b8d59ed11866220a1),     a → →  b    {\displaystyle a\to b\;}  ![{\displaystyle a\to b\;}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0eb4e39f0dd0e749e2562b6d5b1a2421dea7ad9a).

 

If two events happen in different isolated processes (that do not exchange messages directly or indirectly via third-party processes), then the two processes are said to be concurrent, that is neither     a → →  b   {\displaystyle a\to b}  ![{\displaystyle a\to b}](https://wikimedia.org/api/rest_v1/media/math/render/svg/7989b7da84c001dc910a97023b8fcdcfd8f97353) nor     b → →  a   {\displaystyle b\to a}  ![{\displaystyle b\to a}](https://wikimedia.org/api/rest_v1/media/math/render/svg/693a52e723c19b436432b11c4c8aaf4d6cbe234f) is true.[[2]](./Happened-before#cite_note-2)

 

If there are other causal relationships between events in a given system, such as between the creation of a process and its first event, these relationships are also added to the definition.

 

For example, in some programming languages such as Java,[[3]](./Happened-before#cite_note-FOOTNOTEGoetzPeierlsBlochBowbeer2006339–342§16.1.3_The_Java_Memory_Model_in_500_words_or_less-3) C, C++ or Rust, a **happens-before** edge exists if memory written to by statement A is visible to statement B, that is, if statement A completes its write before statement B starts its read.

 

Like all strict partial orders, the happened-before relation is *[transitive](./Transitive_relation)*, *[irreflexive](./Irreflexive_relation)*, (and, vacuously, *[asymmetric](./Asymmetric_relation)*), i.e.:

 
-     ∀ ∀  a , b , c   {\displaystyle \forall a,b,c}  ![{\displaystyle \forall a,b,c}](https://wikimedia.org/api/rest_v1/media/math/render/svg/7ee64314a9415258f6038e2c60d4d5f089bc27b0), if     a → →  b    {\displaystyle a\to b\;}  ![{\displaystyle a\to b\;}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0eb4e39f0dd0e749e2562b6d5b1a2421dea7ad9a) and     b → →  c    {\displaystyle b\to c\;}  ![{\displaystyle b\to c\;}](https://wikimedia.org/api/rest_v1/media/math/render/svg/46df605bd527eaa498fd4f75909ca1e3a51b31e2), then     a → →  c    {\displaystyle a\to c\;}  ![{\displaystyle a\to c\;}](https://wikimedia.org/api/rest_v1/media/math/render/svg/47f9826ecb112b5d9292c41eea2b84f71c2ad9cf) (transitivity). This means that for any three events     a , b , c   {\displaystyle a,b,c}  ![{\displaystyle a,b,c}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f13f068df656c1b1911ae9f81628c49a6181194d), if     a   {\displaystyle a}  ![{\displaystyle a}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ffd2487510aa438433a2579450ab2b3d557e5edc) happened before     b   {\displaystyle b}  ![{\displaystyle b}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f11423fbb2e967f986e36804a8ae4271734917c3), and     b   {\displaystyle b}  ![{\displaystyle b}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f11423fbb2e967f986e36804a8ae4271734917c3) happened before     c   {\displaystyle c}  ![{\displaystyle c}](https://wikimedia.org/api/rest_v1/media/math/render/svg/86a67b81c2de995bd608d5b2df50cd8cd7d92455), then     a   {\displaystyle a}  ![{\displaystyle a}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ffd2487510aa438433a2579450ab2b3d557e5edc) must have happened before     c   {\displaystyle c}  ![{\displaystyle c}](https://wikimedia.org/api/rest_v1/media/math/render/svg/86a67b81c2de995bd608d5b2df50cd8cd7d92455).
-     ∀ ∀  a , a ↛ ↛  a   {\displaystyle \forall a,a\nrightarrow a}  ![{\displaystyle \forall a,a\nrightarrow a}](https://wikimedia.org/api/rest_v1/media/math/render/svg/adc22e2aeaad696dcaf1fc4801ed068ee1c9af5a) (irreflexivity). This means that no event can happen before itself.
-     ∀ ∀  a , b ,   {\displaystyle \forall a,b,}  ![{\displaystyle \forall a,b,}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87fb0da30bb196d901f15fce7adbf51c65f7352b) if     a → →  b   {\displaystyle a\to b}  ![{\displaystyle a\to b}](https://wikimedia.org/api/rest_v1/media/math/render/svg/7989b7da84c001dc910a97023b8fcdcfd8f97353) then     b ↛ ↛  a   {\displaystyle b\nrightarrow a}  ![{\displaystyle b\nrightarrow a}](https://wikimedia.org/api/rest_v1/media/math/render/svg/7a179a9118e717950627d67b681a60707cee85aa) (asymmetry). This means that for any two events     a , b   {\displaystyle a,b}  ![{\displaystyle a,b}](https://wikimedia.org/api/rest_v1/media/math/render/svg/181523deba732fda302fd176275a0739121d3bc8), if     a   {\displaystyle a}  ![{\displaystyle a}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ffd2487510aa438433a2579450ab2b3d557e5edc) happened before     b   {\displaystyle b}  ![{\displaystyle b}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f11423fbb2e967f986e36804a8ae4271734917c3) then     b   {\displaystyle b}  ![{\displaystyle b}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f11423fbb2e967f986e36804a8ae4271734917c3) cannot have happened before     a   {\displaystyle a}  ![{\displaystyle a}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ffd2487510aa438433a2579450ab2b3d557e5edc).

 

Let us observe that the asymmetry property directly follows from the previous properties: by contradiction, let us suppose that     ∀ ∀  a , b ,   {\displaystyle \forall a,b,}  ![{\displaystyle \forall a,b,}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87fb0da30bb196d901f15fce7adbf51c65f7352b) we have     a → →  b    {\displaystyle a\to b\;}  ![{\displaystyle a\to b\;}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0eb4e39f0dd0e749e2562b6d5b1a2421dea7ad9a) and     b → →  a   {\displaystyle b\to a}  ![{\displaystyle b\to a}](https://wikimedia.org/api/rest_v1/media/math/render/svg/693a52e723c19b436432b11c4c8aaf4d6cbe234f). Then by transitivity we have     a → →  a ,   {\displaystyle a\to a,}  ![{\displaystyle a\to a,}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b95df105e78964e8f4ed102bed5469530d35aeb7) which contradicts irreflexivity.

 

The processes that make up a distributed system have no knowledge of the happened-before relation unless they use a [logical clock](./Logical_clock), like a [Lamport clock](./Lamport_clock) or a [vector clock](./Vector_clock). This allows one to design algorithms for [mutual exclusion](./Mutual_exclusion), tasks like debugging or optimising distributed systems, and protocols for recording [consistent global states](./Global_state_(computer_science)) via snapshot algorithms.

 

## Byzantine faults and the impossibility of detection

 

In distributed systems, the happened-before relation can be accurately tracked under crash failures using vector clocks, their variants, and other causality tracking mechanisms. However, under [Byzantine faults](./Byzantine_fault), where processes may behave arbitrarily or maliciously, it is fundamentally impossible to detect the happened-before relation.[[4]](./Happened-before#cite_note-4) The intuitive reasoning for this is that Byzantine processes can forge or manipulate metadata, making it impossible to determine true causal dependencies.

 

## See also

 
- [Global state (computer science)](./Global_state_(computer_science))
- [Java memory model](./Java_memory_model)
- [Lamport timestamp](./Lamport_timestamp)
- [Logical clock](./Logical_clock)
- [Race condition](./Race_condition)
- [Vector clock](./Vector_clock)

 

## Citations

  
1. [↑](./Happened-before#cite_ref-1) Lamport, Leslie (1978). ["Time, Clocks and the Ordering of Events in a Distributed System"](https://research.microsoft.com/en-us/um/people/lamport/pubs/time-clocks.pdf), *Communications of the ACM*, 21(7), 558-565.
2. [↑](./Happened-before#cite_ref-2) ["Distributed Systems 3rd edition (2017)"](https://www.distributed-systems.net/index.php/books/ds3/). *DISTRIBUTED-SYSTEMS.NET*. Retrieved 2021-03-20.
3. [↑](./Happened-before#cite_ref-FOOTNOTEGoetzPeierlsBlochBowbeer2006339–342§16.1.3_The_Java_Memory_Model_in_500_words_or_less_3-0) [Goetz et al. 2006](./Happened-before#CITEREFGoetzPeierlsBlochBowbeer2006), pp. 339–342, §16.1.3 The Java Memory Model in 500 words or less.
4. [↑](./Happened-before#cite_ref-4) Misra, Anshuman; Kshemkalyani, Ajay D. (2022). "Detecting Causality in the Presence of Byzantine Processes: There is No Holy Grail". *2022 IEEE 21st International Symposium on Network Computing and Applications (NCA)*. IEEE. pp. 73–80. [doi](./Doi_(identifier)):[10.1109/NCA57778.2022.10013644](https://doi.org/10.1109%2FNCA57778.2022.10013644).

 

## References

 
- Goetz, Brian; Peierls, Tim; Bloch, Joshua; Bowbeer, Joseph; Holmes, David; Lea, Doug (2006). [*Java Concurrency in Practice*](https://archive.org/details/javaconcurrencyi00goet). Addison Wesley. [ISBN](./ISBN_(identifier)) [0-321-34960-1](./Special:BookSources/0-321-34960-1).