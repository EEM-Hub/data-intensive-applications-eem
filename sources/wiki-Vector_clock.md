---
source: https://en.wikipedia.org/wiki/Vector_clock
fetched: 2026-06-19
---

Algorithm for partial ordering of events and detecting causality in distributed systems Not to be confused with [Version vector](./Version_vector). 

A **vector clock** is a [data structure](./Data_structure) used for determining the [partial ordering](./Partial_ordering) of events in a [distributed system](./Distributed_system) and detecting [causality](./Causality) violations. Just as in [Lamport timestamps](./Lamport_timestamp), inter-process messages contain the state of the sending process's [logical clock](./Logical_clock). A vector clock of a system of *n* processes is a [vector](./Vector_(mathematics_and_physics)) (equivalentlly, a 1-dimensional [array](./Array_data_structure)) of *n* logical clocks, one clock per process. Besides maintaining its own clock, every process also keeps track of the largest value of each of the other processes' clocks that it has so far been informed of.

 

The clock updates proceed as follows,[[1]](./Vector_clock#cite_note-1) where     V  C  i     {\displaystyle VC_{i}}  ![{\displaystyle VC_{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5d74634dd8f7219275513533114df2f822f2258c) denotes the value of the vector clock maintained by process     i   {\displaystyle i}  ![{\displaystyle i}](https://wikimedia.org/api/rest_v1/media/math/render/svg/add78d8608ad86e54951b8c8bd6c8d8416533d20):

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/5/55/Vector_Clock.svg/500px-Vector_Clock.svg.png)](./File:Vector_Clock.svg)Example of a system of vector clocks. Events in the blue region are the causes leading to event B4, whereas those in the red region are the effects of event B4. 
- Initially all clocks are zero.
- Each time a process experiences an internal event, it increments its own [logical clock](./Logical_clock) in the vector by one. For instance, upon an event at process     i   {\displaystyle i}  ![{\displaystyle i}](https://wikimedia.org/api/rest_v1/media/math/render/svg/add78d8608ad86e54951b8c8bd6c8d8416533d20), it updates     V  C  i   [ i ] ← ←  V  C  i   [ i ] + 1   {\displaystyle VC_{i}[i]\leftarrow VC_{i}[i]+1}  ![{\displaystyle VC_{i}[i]\leftarrow VC_{i}[i]+1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/78139cb05a1b9374ca4e301ffb3df791234e8cf2).
- Each time a process sends a message, it increments its own logical clock in the vector by one (as in the bullet above, but not twice for the same event) then it pairs the message with a copy of its own vector and finally sends the pair.
- Each time a process receives a message-vector clock pair, it increments its own logical clock in the vector by one and updates each element in its vector by taking the maximum of the value in its own vector clock and the value in the vector in the received pair (for every element). For example, if process      P  i     {\displaystyle P_{i}}  ![{\displaystyle P_{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3ba1396129f7be3c7f828a571b6649e6807d10d3) receives a message     ( m , V  C  j   )   {\displaystyle (m,VC_{j})}  ![{\displaystyle (m,VC_{j})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/247128ec417f3ac08ee2494bed89a3c2a1619dc6) from      P  j     {\displaystyle P_{j}}  ![{\displaystyle P_{j}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4a5da6c3564a2129f714ef11acd8ba649d18e604), it first increments its own logical clock in the vector by one     V  C  i   [ i ] ← ←  V  C  i   [ i ] + 1   {\displaystyle VC_{i}[i]\leftarrow VC_{i}[i]+1}  ![{\displaystyle VC_{i}[i]\leftarrow VC_{i}[i]+1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/78139cb05a1b9374ca4e301ffb3df791234e8cf2) and then updates its entire vector by setting     V  C  i   [ k ] ← ←  max ( V  C  i   [ k ] , V  C  j   [ k ] ) , ∀ ∀  k   {\displaystyle VC_{i}[k]\leftarrow \max(VC_{i}[k],VC_{j}[k]),\forall k}  ![{\displaystyle VC_{i}[k]\leftarrow \max(VC_{i}[k],VC_{j}[k]),\forall k}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c913d1dfe00937f738bf6ae0cf71509ce5c6c117).

 

## History

 

Lamport originated the idea of logical [Lamport clocks](./Lamport_clock) in 1978.[[2]](./Vector_clock#cite_note-Lamport_1978-2) However, the logical clocks in that paper were scalars, not vectors. The generalization to vector time was developed several times, apparently independently, by different authors in the early 1980s.[[3]](./Vector_clock#cite_note-Schwarz-3) At least 6 papers contain the concept.[[4]](./Vector_clock#cite_note-4) The papers canonically cited in reference to vector clocks are Colin Fidge’s and [Friedemann Mattern](./Friedemann_Mattern)’s 1988 works,
[[5]](./Vector_clock#cite_note-5)[[6]](./Vector_clock#cite_note-Mattern1988-6) as they (independently) established the name "vector clock" and the mathematical properties of vector clocks.[[3]](./Vector_clock#cite_note-Schwarz-3) Mattern's paper also showed that vector timestamp comparisons can determine which in-transit messages belong to a [consistent global state](./Global_state_(computer_science)) recording without dedicated marker messages.[[6]](./Vector_clock#cite_note-Mattern1988-6)

 

## Partial ordering property

 

Vector clocks allow for the partial causal ordering of events. Defining the following:

 
-     V C ( x )   {\displaystyle VC(x)}  ![{\displaystyle VC(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f7924d22546612ab798742f91bc6b3d3a5a54dce) denotes the vector clock of event     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4), and     V C ( x  )  z     {\displaystyle VC(x)_{z}}  ![{\displaystyle VC(x)_{z}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2329640e4f3946e9d7a87d8958ae4d3f418eeffe) denotes the component of that clock for process     z   {\displaystyle z}  ![{\displaystyle z}](https://wikimedia.org/api/rest_v1/media/math/render/svg/bf368e72c009decd9b6686ee84a375632e11de98).
-     V C ( x ) < V C ( y )  ⟺ ⟺   ∀ ∀  z [ V C ( x  )  z   ≤ ≤  V C ( y  )  z   ] ∧ ∧  ∃ ∃   z ′  [ V C ( x  )   z ′    < V C ( y  )   z ′    ]   {\displaystyle VC(x)<VC(y)\iff \forall z[VC(x)_{z}\leq VC(y)_{z}]\land \exists z'[VC(x)_{z'}<VC(y)_{z'}]}  ![{\displaystyle VC(x)<VC(y)\iff \forall z[VC(x)_{z}\leq VC(y)_{z}]\land \exists z'[VC(x)_{z'}<VC(y)_{z'}]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/74db88ecb978e85eb1324d12a8c59d4c77bb44c9) 
- In English:     V C ( x )   {\displaystyle VC(x)}  ![{\displaystyle VC(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f7924d22546612ab798742f91bc6b3d3a5a54dce) is less than     V C ( y )   {\displaystyle VC(y)}  ![{\displaystyle VC(y)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/cb37d38d16ab4139b0470575d202587a51de8b4a), [if and only if](./If_and_only_if)     V C ( x  )  z     {\displaystyle VC(x)_{z}}  ![{\displaystyle VC(x)_{z}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2329640e4f3946e9d7a87d8958ae4d3f418eeffe) is less than or equal to     V C ( y  )  z     {\displaystyle VC(y)_{z}}  ![{\displaystyle VC(y)_{z}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3973bfb557584b032b821c4b4bbce79b7efa0068) for all process indices     z   {\displaystyle z}  ![{\displaystyle z}](https://wikimedia.org/api/rest_v1/media/math/render/svg/bf368e72c009decd9b6686ee84a375632e11de98), and at least one of those relationships is strictly smaller (that is,     V C ( x  )   z ′    < V C ( y  )   z ′      {\displaystyle VC(x)_{z'}<VC(y)_{z'}}  ![{\displaystyle VC(x)_{z'}<VC(y)_{z'}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6103d23ea610504498b97dd81a2df50139d2da99)).

-     x → →  y    {\displaystyle x\to y\;}  ![{\displaystyle x\to y\;}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a535e0ad9b4b16a7cb8f65d960b5d49e1fbf6046) denotes that event     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4) happened before event     y   {\displaystyle y}  ![{\displaystyle y}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b8a6208ec717213d4317e666f1ae872e00620a0d). It is defined as: if     x → →  y    {\displaystyle x\to y\;}  ![{\displaystyle x\to y\;}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a535e0ad9b4b16a7cb8f65d960b5d49e1fbf6046), then     V C ( x ) < V C ( y )   {\displaystyle VC(x)<VC(y)}  ![{\displaystyle VC(x)<VC(y)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/50ec20323a6407e76d87bb79518cc53efb29def8)

 

Properties:

 
- [Asymmetry](./Asymmetric_relation): if     V C ( a ) < V C ( b )   {\displaystyle VC(a)<VC(b)}  ![{\displaystyle VC(a)<VC(b)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2eeaf2ce1352729e84feb17359ad29d32752af77), then [¬](./Negation)    ( V C ( b ) < V C ( a ) )   {\displaystyle (VC(b)<VC(a))}  ![{\displaystyle (VC(b)<VC(a))}](https://wikimedia.org/api/rest_v1/media/math/render/svg/dfbaf3c8ce04c7241ed28d747ecfd57931651c9f)
- [Transitivity](./Transitive_relation): if     V C ( a ) < V C ( b )   {\displaystyle VC(a)<VC(b)}  ![{\displaystyle VC(a)<VC(b)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2eeaf2ce1352729e84feb17359ad29d32752af77) and     V C ( b ) < V C ( c )   {\displaystyle VC(b)<VC(c)}  ![{\displaystyle VC(b)<VC(c)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5fec7222ec72952a553783218c0d872f86fecefe), then     V C ( a ) < V C ( c )   {\displaystyle VC(a)<VC(c)}  ![{\displaystyle VC(a)<VC(c)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d6a1dced10307f662da8cc1c632716f6d64812be); or, if     a → →  b    {\displaystyle a\to b\;}  ![{\displaystyle a\to b\;}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0eb4e39f0dd0e749e2562b6d5b1a2421dea7ad9a) and     b → →  c    {\displaystyle b\to c\;}  ![{\displaystyle b\to c\;}](https://wikimedia.org/api/rest_v1/media/math/render/svg/46df605bd527eaa498fd4f75909ca1e3a51b31e2), then     a → →  c    {\displaystyle a\to c\;}  ![{\displaystyle a\to c\;}](https://wikimedia.org/api/rest_v1/media/math/render/svg/47f9826ecb112b5d9292c41eea2b84f71c2ad9cf)

 

## Relation with other orders

 
- Let     R T ( x )   {\displaystyle RT(x)}  ![{\displaystyle RT(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/77ce5d6afd1f7abf20dc5b7002816b28572db6de) be the real time when event     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4) occurs. If     V C ( a ) < V C ( b )   {\displaystyle VC(a)<VC(b)}  ![{\displaystyle VC(a)<VC(b)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2eeaf2ce1352729e84feb17359ad29d32752af77), then     R T ( a ) < R T ( b )   {\displaystyle RT(a)<RT(b)}  ![{\displaystyle RT(a)<RT(b)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/84492ae72ebdb0cf99c328a102b8fc0093aceba5)
- Let     C ( x )   {\displaystyle C(x)}  ![{\displaystyle C(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/7f6b53682fddbe3028ffd75bd75771b86c6c7bd9) be the [Lamport timestamp](./Lamport_timestamp) of event     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4). If     V C ( a ) < V C ( b )   {\displaystyle VC(a)<VC(b)}  ![{\displaystyle VC(a)<VC(b)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2eeaf2ce1352729e84feb17359ad29d32752af77), then     C ( a ) < C ( b )   {\displaystyle C(a)<C(b)}  ![{\displaystyle C(a)<C(b)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/61a75c7595dc224580384eddca657fd6ce251662)

 

## Limitations under Byzantine failures

 

Vector clocks can reliably detect causality in distributed systems subject to crash failures. However, when processes behave arbitrarily or maliciously—as in the [Byzantine failure](./Byzantine_failure) model—causality detection becomes fundamentally impossible [[7]](./Vector_clock#cite_note-7)
, rendering vector clocks ineffective in such environments. This impossibility result holds for all variants of vector clocks, as it stems from core limitations inherent to the problem of causality detection under Byzantine faults.

 

## Other mechanisms

 
|  | This list isincomplete; you can help byadding missing items.(June 2023) |
| --- | --- |

 
- In 1984, Wuu and Bernstein described a technique extended from vector clocks known as **Matrix Clocks**.[[8]](./Vector_clock#cite_note-8) By maintaining a matrix where each row corresponds to the vector clock of a peer, processes can estimate the minimum knowledge held by all other nodes. This allows for the calculation of a "lower bound" on global progress, enabling the safe truncation of operation logs (garbage collection) in replicated databases.
- In 1999, Torres-Rojas and Ahamad developed **Plausible Clocks**,[[9]](./Vector_clock#cite_note-9) a mechanism that takes less space than vector clocks but that, in some cases, will totally order events that are causally concurrent.
- In 2005, Agarwal and Garg created **Chain Clocks**,[[10]](./Vector_clock#cite_note-10) a system that tracks dependencies using vectors with size smaller than the number of processes and that adapts automatically to systems with dynamic number of processes.
- In 2008, Almeida *et al.* introduced **Interval Tree Clocks**.[[11]](./Vector_clock#cite_note-11)[[12]](./Vector_clock#cite_note-12)[[13]](./Vector_clock#cite_note-13) This mechanism generalizes Vector Clocks and allows operation in dynamic environments when the identities and number of processes in the computation is not known in advance.
- In 2019, Lum Ramabaja proposed **Bloom Clocks**, a probabilistic data structure based on [Bloom filters](./Bloom_filter).[[14]](./Vector_clock#cite_note-14)[[15]](./Vector_clock#cite_note-15)[[16]](./Vector_clock#cite_note-16) Compared to a vector clock, the space used per node is fixed and does not depend on the number of nodes in a system. Comparing two clocks either produces a true negative (the clocks are not comparable), or else a suggestion that one clock precedes the other, with the possibility of a false positive where the two clocks are unrelated. The false positive rate decreases as more storage is allowed.

 

## Applications

 

Modern distributed systems utilize variations of vector clocks to enforce causal ordering of transactions without relying on a central wall-clock time. For instance, the Cerberus protocol uses logical clocks to track the state "version" of each shard. When a transaction spans multiple shards, the vector of these logical clocks allows the network to validate that the transaction is interacting with the most current state of all involved assets, enabling atomic composability in an adversarial environment.[[17]](./Vector_clock#cite_note-VLDB2021-17)

 

## See also

 
- [Global state (computer science)](./Global_state_(computer_science))
- [Lamport timestamp](./Lamport_timestamp)
- [Matrix clock](./Matrix_clock)
- [Version vector](./Version_vector)

 

## References

 
1. [↑](./Vector_clock#cite_ref-1) ["Distributed Systems 3rd edition (2017)"](https://www.distributed-systems.net/index.php/books/ds3/). *DISTRIBUTED-SYSTEMS.NET*. Retrieved 2021-03-21.
2. [↑](./Vector_clock#cite_ref-Lamport_1978_2-0) [Lamport, L.](./Leslie_Lamport) (1978). ["Time, clocks, and the ordering of events in a distributed system"](https://lamport.azurewebsites.net/pubs/time-clocks.pdf) (PDF). *[Communications of the ACM](./Communications_of_the_ACM)*. **21** (7): 558–565. [doi](./Doi_(identifier)):[10.1145/359545.359563](https://doi.org/10.1145%2F359545.359563). [S2CID](./S2CID_(identifier)) [215822405](https://api.semanticscholar.org/CorpusID:215822405).
3. [1](./Vector_clock#cite_ref-Schwarz_3-0) [2](./Vector_clock#cite_ref-Schwarz_3-1) Schwarz, Reinhard; Mattern, Friedemann (March 1994). ["Detecting causal relationships in distributed computations: In search of the holy grail"](https://kluedo.ub.rptu.de/frontdoor/index/index/docId/429). *Distributed Computing*. **7** (3): 149–174. [doi](./Doi_(identifier)):[10.1007/BF02277859](https://doi.org/10.1007%2FBF02277859). [S2CID](./S2CID_(identifier)) [3065996](https://api.semanticscholar.org/CorpusID:3065996).
4. [↑](./Vector_clock#cite_ref-4) Kuper, Lindsey (8 April 2023). ["Who invented vector clocks?"](https://decomposition.al/blog/2023/04/08/who-invented-vector-clocks/). *decomposition ∘ al*. The papers are (in chronological order):

- Fischer, Michael J.; Michael, Alan (1982). "Sacrificing serializability to attain high availability of data in an unreliable network". *Proceedings of the 1st ACM SIGACT-SIGMOD symposium on Principles of database systems - PODS '82*. p. 70. [doi](./Doi_(identifier)):[10.1145/588111.588124](https://doi.org/10.1145%2F588111.588124). [ISBN](./ISBN_(identifier)) [0897910702](./Special:BookSources/0897910702). [S2CID](./S2CID_(identifier)) [8774876](https://api.semanticscholar.org/CorpusID:8774876).
- Parker, D.S.; Popek, G.J.; Rudisin, G.; Stoughton, A.; Walker, B.J.; Walton, E.; Chow, J.M.; Edwards, D.; Kiser, S.; Kline, C. (May 1983). "Detection of Mutual Inconsistency in Distributed Systems". *IEEE Transactions on Software Engineering*. **SE-9** (3): 240–247. [Bibcode](./Bibcode_(identifier)):[1983ITSEn...9..240P](https://ui.adsabs.harvard.edu/abs/1983ITSEn...9..240P). [doi](./Doi_(identifier)):[10.1109/TSE.1983.236733](https://doi.org/10.1109%2FTSE.1983.236733). [S2CID](./S2CID_(identifier)) [2483222](https://api.semanticscholar.org/CorpusID:2483222).
- Wuu, Gene T.J.; Bernstein, Arthur J. (1984). "Efficient solutions to the replicated log and dictionary problems". *Proceedings of the third annual ACM symposium on Principles of distributed computing - PODC '84*. pp. 233–242. [doi](./Doi_(identifier)):[10.1145/800222.806750](https://doi.org/10.1145%2F800222.806750). [ISBN](./ISBN_(identifier)) [0897911431](./Special:BookSources/0897911431). [S2CID](./S2CID_(identifier)) [2384672](https://api.semanticscholar.org/CorpusID:2384672).
- Strom, Rob; Yemini, Shaula (August 1985). ["Optimistic recovery in distributed systems"](https://doi.org/10.1145%2F3959.3962). *ACM Transactions on Computer Systems*. **3** (3): 204–226. [doi](./Doi_(identifier)):[10.1145/3959.3962](https://doi.org/10.1145%2F3959.3962). [S2CID](./S2CID_(identifier)) [1941122](https://api.semanticscholar.org/CorpusID:1941122).
- Schmuck, Frank B. (November 1985). *Software clocks and the order of events in a distributed system* (unpublished).
- Liskov, Barbara; Ladin, Rivka (1986). "Highly available distributed services and fault-tolerant distributed garbage collection". *Proceedings of the fifth annual ACM symposium on Principles of distributed computing - PODC '86*. pp. 29–39. [doi](./Doi_(identifier)):[10.1145/10590.10593](https://doi.org/10.1145%2F10590.10593). [ISBN](./ISBN_(identifier)) [0897911989](./Special:BookSources/0897911989). [S2CID](./S2CID_(identifier)) [16148617](https://api.semanticscholar.org/CorpusID:16148617).
- Raynal, Michel (February 1987). "A distributed algorithm to prevent mutual drift between n logical clocks". *Information Processing Letters*. **24** (3): 199–202. [doi](./Doi_(identifier)):[10.1016/0020-0190(87)90186-4](https://doi.org/10.1016%2F0020-0190%2887%2990186-4).

 
5. [↑](./Vector_clock#cite_ref-5) Fidge, Colin J. (February 1988). ["Timestamps in message-passing systems that preserve the partial ordering"](https://web.archive.org/web/20180517171438/http://zoo.cs.yale.edu/classes/cs426/2012/lab/bib/fidge88timestamps.pdf) (PDF). In K. Raymond (ed.). *Proceedings of the 11th Australian Computer Science Conference (ACSC'88)*. Vol. 10. pp. 56–66. Archived from [the original](http://zoo.cs.yale.edu/classes/cs426/2012/lab/bib/fidge88timestamps.pdf) (PDF) on 2018-05-17. Retrieved 2009-02-13.
6. [1](./Vector_clock#cite_ref-Mattern1988_6-0) [2](./Vector_clock#cite_ref-Mattern1988_6-1) Mattern, Friedemann (October 1988). "Virtual Time and Global States of Distributed systems". In Cosnard, M. (ed.). *Proc. Workshop on Parallel and Distributed Algorithms*. Chateau de Bonas, France: Elsevier. pp. 215–226.
7. [↑](./Vector_clock#cite_ref-7) Misra, Anshuman; Kshemkalyani, Ajay D. (2022). "Detecting Causality in the Presence of Byzantine Processes: There is No Holy Grail". *2022 IEEE 21st International Symposium on Network Computing and Applications (NCA)*. IEEE. pp. 73–80. [doi](./Doi_(identifier)):[10.1109/NCA57778.2022.10013644](https://doi.org/10.1109%2FNCA57778.2022.10013644).
8. [↑](./Vector_clock#cite_ref-8) Wuu, Gene T.J.; Bernstein, Arthur J. (1984). "Efficient solutions to the replicated log and dictionary problems". *Proceedings of the third annual ACM symposium on Principles of distributed computing - PODC '84*. pp. 233–242. [doi](./Doi_(identifier)):[10.1145/800222.806750](https://doi.org/10.1145%2F800222.806750). [ISBN](./ISBN_(identifier)) [0897911431](./Special:BookSources/0897911431).
9. [↑](./Vector_clock#cite_ref-9) Francisco Torres-Rojas; Mustaque Ahamad (1999), ["Plausible clocks: constant size logical clocks for distributed systems"](https://www.cc.gatech.edu/fac/Mustaque.Ahamad/pubs/plausible.ps), *Distributed Computing*, **12** (4): 179–195, [doi](./Doi_(identifier)):[10.1007/s004460050065](https://doi.org/10.1007%2Fs004460050065), [S2CID](./S2CID_(identifier)) [2936350](https://api.semanticscholar.org/CorpusID:2936350)
10. [↑](./Vector_clock#cite_ref-10) Agarwal, Anurag; Garg, Vijay K. (17 July 2005). ["Efficient dependency tracking for relevant events in shared-memory systems"](http://users.ece.utexas.edu/~garg/dist/agarwal-garg-DC.pdf) (PDF). *Proceedings of the twenty-fourth annual ACM symposium on Principles of distributed computing*. Association for Computing Machinery. pp. 19–28. [doi](./Doi_(identifier)):[10.1145/1073814.1073818](https://doi.org/10.1145%2F1073814.1073818). [ISBN](./ISBN_(identifier)) [1-58113-994-2](./Special:BookSources/1-58113-994-2). [S2CID](./S2CID_(identifier)) [11779779](https://api.semanticscholar.org/CorpusID:11779779). Retrieved 21 April 2021.
11. [↑](./Vector_clock#cite_ref-11) Almeida, Paulo; Baquero, Carlos; Fonte, Victor (2008), "Interval Tree Clocks: A Logical Clock for Dynamic Systems", in Baker, Theodore P.; Bui, Alain; Tixeuil, Sébastien (eds.), [*Principles of Distributed Systems*](http://gsd.di.uminho.pt/members/cbm/ps/itc2008.pdf) (PDF), Lecture Notes in Computer Science, vol. 5401, Springer-Verlag, Lecture Notes in Computer Science, pp. 259–274, [Bibcode](./Bibcode_(identifier)):[2008LNCS.5401.....B](https://ui.adsabs.harvard.edu/abs/2008LNCS.5401.....B), [doi](./Doi_(identifier)):[10.1007/978-3-540-92221-6](https://doi.org/10.1007%2F978-3-540-92221-6), [ISBN](./ISBN_(identifier)) [978-3-540-92220-9](./Special:BookSources/978-3-540-92220-9)
12. [↑](./Vector_clock#cite_ref-12) Almeida, Paulo; Baquero, Carlos; Fonte, Victor (2008), "Interval Tree Clocks: A Logical Clock for Dynamic Systems", [*Interval Tree Clocks: A Logical Clock for Dynamic Systems*](https://www.researchgate.net/publication/235246938), Lecture Notes in Computer Science, vol. 5401, p. 259, [doi](./Doi_(identifier)):[10.1007/978-3-540-92221-6_18](https://doi.org/10.1007%2F978-3-540-92221-6_18), [hdl](./Hdl_(identifier)):[1822/37748](https://hdl.handle.net/1822%2F37748), [ISBN](./ISBN_(identifier)) [978-3-540-92220-9](./Special:BookSources/978-3-540-92220-9)
13. [↑](./Vector_clock#cite_ref-13) Zhang, Yi (2014), "Background Preliminaries: Interval Tree Clock Results", [*Background Preliminaries: Interval Tree Clock Results*](https://cs.uwaterloo.ca/~mkarsten/cs755-F14/presentations/ITC.pdf) (PDF)
14. [↑](./Vector_clock#cite_ref-14) Pozzetti, Tommaso; Kshemkalyani, Ajay D. (1 April 2021). ["Resettable Encoded Vector Clock for Causality Analysis With an Application to Dynamic Race Detection"](https://doi.org/10.1109%2FTPDS.2020.3032293). *IEEE Transactions on Parallel and Distributed Systems*. **32** (4): 772–785. [Bibcode](./Bibcode_(identifier)):[2021ITPDS..32..772P](https://ui.adsabs.harvard.edu/abs/2021ITPDS..32..772P). [doi](./Doi_(identifier)):[10.1109/TPDS.2020.3032293](https://doi.org/10.1109%2FTPDS.2020.3032293). [S2CID](./S2CID_(identifier)) [220362525](https://api.semanticscholar.org/CorpusID:220362525).
15. [↑](./Vector_clock#cite_ref-15) Lum Ramabaja (2019), *The Bloom Clock*, [arXiv](./ArXiv_(identifier)):[1905.13064](https://arxiv.org/abs/1905.13064), [Bibcode](./Bibcode_(identifier)):[2019arXiv190513064R](https://ui.adsabs.harvard.edu/abs/2019arXiv190513064R)
16. [↑](./Vector_clock#cite_ref-16) Kulkarni, Sandeep S; Appleton, Gabe; Nguyen, Duong (4 January 2022). "Achieving Causality with Physical Clocks". *Proceedings of the 23rd International Conference on Distributed Computing and Networking*. pp. 97–106. [arXiv](./ArXiv_(identifier)):[2104.15099](https://arxiv.org/abs/2104.15099). [doi](./Doi_(identifier)):[10.1145/3491003.3491009](https://doi.org/10.1145%2F3491003.3491009). [ISBN](./ISBN_(identifier)) [9781450395601](./Special:BookSources/9781450395601). [S2CID](./S2CID_(identifier)) [233476293](https://api.semanticscholar.org/CorpusID:233476293).
17. [↑](./Vector_clock#cite_ref-VLDB2021_17-0) Hellings, Jelle; Sadoghi, Mohammad (2021). ["Cerberus: Minimalistic Multi-shard Byzantine-resilient Transaction Processing"](http://www.vldb.org/pvldb/vol14/p2230-hellings.pdf) (PDF). *Proceedings of the VLDB Endowment*. **14** (11): 2230–2243. [arXiv](./ArXiv_(identifier)):[2202.04522](https://arxiv.org/abs/2202.04522). [doi](./Doi_(identifier)):[10.14778/3476249.3476274](https://doi.org/10.14778%2F3476249.3476274).

 

## External links

 
- [Why Logical Clocks are Easy (Compares Causal Histories, Vector Clocks and Version Vectors)](https://queue.acm.org/detail.cfm?id=2917756)
- [Timestamp-based vector clock implementation in Erlang](https://github.com/moonpolysoft/dynomite/blob/master/elibs/vector_clock.erl)
- [Vector clock implementation in Objective-C](https://github.com/jeremytregunna/JVectorClock)
- [Vector clock implementation in Erlang](https://github.com/basho/riak_core/blob/develop/src/vclock.erl)
- [Why Vector Clocks are Easy](https://riak.com/why-vector-clocks-are-easy/), Bryan Fink, Riak Blog, January 29, 2010
- [Why Vector Clocks are Hard](https://riak.com/why-vector-clocks-are-hard/), Justin Sheehy, Riak Blog, April 5, 2010
- [Why Cassandra doesn’t need vector clocks](https://www.datastax.com/blog/why-cassandra-doesnt-need-vector-clocks)