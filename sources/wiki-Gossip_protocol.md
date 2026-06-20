---
source: https://en.wikipedia.org/wiki/Gossip_protocol
fetched: 2026-06-19
---

Concept in computing 
|  | This article has multiple issues.Please helpimprove itor discuss these issues on thetalk page.(Learn how and when to remove these messages)This article includes alist of references,related reading, orexternal links,but its sources remain unclear because it lacksinline citations.Please helpimprovethis article byintroducingmore precise citations.(March 2009)(Learn how and when to remove this message)This articlemay need to be rewrittento comply with Wikipedia'squality standards.Relevant discussion may be found on thetalk page.You can help. The talk page may contain suggestions.(October 2021)This articlehas an unclearcitation style.The references used may be made clearer with a different or consistent style ofcitationandfootnoting.(November 2015)(Learn how and when to remove this message)(Learn how and when to remove this message) |  | This article includes alist of references,related reading, orexternal links,but its sources remain unclear because it lacksinline citations.Please helpimprovethis article byintroducingmore precise citations.(March 2009)(Learn how and when to remove this message) |  | This articlemay need to be rewrittento comply with Wikipedia'squality standards.Relevant discussion may be found on thetalk page.You can help. The talk page may contain suggestions.(October 2021) |  | This articlehas an unclearcitation style.The references used may be made clearer with a different or consistent style ofcitationandfootnoting.(November 2015)(Learn how and when to remove this message) |
| --- | --- | --- | --- | --- | --- | --- | --- |
|  | This article includes alist of references,related reading, orexternal links,but its sources remain unclear because it lacksinline citations.Please helpimprovethis article byintroducingmore precise citations.(March 2009)(Learn how and when to remove this message) |
|  | This articlemay need to be rewrittento comply with Wikipedia'squality standards.Relevant discussion may be found on thetalk page.You can help. The talk page may contain suggestions.(October 2021) |
|  | This articlehas an unclearcitation style.The references used may be made clearer with a different or consistent style ofcitationandfootnoting.(November 2015)(Learn how and when to remove this message) |

 

A **gossip protocol** or **epidemic protocol** is a procedure or process of computer peer-to-peer communication that is based on the way [epidemics](./Epidemic) spread.[[1]](./Gossip_protocol#cite_note-1) Some [distributed systems](./Distributed_computing) use peer-to-peer gossip to ensure that data is disseminated to all members of a group. Some [ad-hoc networks](./Wireless_ad_hoc_network) have no central registry and the only way to spread common data is to rely on each member to pass it along to their neighbors.

 

## Communication

 

The concept of *gossip communication* can be illustrated by the analogy of office workers spreading rumors. Let's say each hour the office workers congregate around the water cooler. Each employee pairs off with another, chosen at random, and shares the latest gossip. At the start of the day, Dave starts a new rumor: he comments to Bob that he believes that Charlie dyes his mustache. At the next meeting, Bob tells Alice, while Dave repeats the idea to Eve. After each water cooler rendezvous, the number of individuals who have heard the rumor roughly doubles (though this doesn't account for gossiping twice to the same person; perhaps Dave tries to tell the story to Frank, only to find that Frank already heard it from Alice). Computer systems typically implement this type of protocol with a form of random "peer selection": with a given frequency, each machine picks another machine at random and shares any rumors.

 

## Variants and styles

 

There are probably hundreds of variants of specific gossip-like protocols because each use-scenario is likely to be customized to the organization's specific needs.

 

For example, a gossip protocol might employ some of these ideas:

 
- The core of the protocol involves periodic, pairwise, inter-process interactions.
- The information exchanged during these interactions is of bounded size.
- When [agents](./Agent-based_model#In_computer_science_and_artificial_intelligence) interact, the state of at least one agent changes to reflect the state of the other.
- Reliable communication is not assumed.
- The frequency of the interactions is low compared to typical message latencies so that the protocol costs are negligible.
- There is some form of randomness in the peer selection. Peers might be selected from the full set of nodes or from a smaller set of [neighbors](./Neighbourhood_(graph_theory)).
- Due to the replication there is an implicit [redundancy](./Redundancy_(engineering)) of the delivered information.

 

## Protocol types

 

It is useful to distinguish two prevailing styles of gossip protocol:[[2]](./Gossip_protocol#cite_note-2)

 
- **Dissemination protocols** (or rumor-mongering protocols). These use gossip to spread information; they basically work by flooding agents in the network, but in a manner that produces bounded worst-case loads:

1. *Event dissemination protocols* use gossip to carry out [multicasts](./Multicast). They report events, but the gossip occurs periodically and events don't actually trigger the gossip. One concern here is the potentially high latency from when the event occurs until it is delivered.
2. *Background data dissemination protocols* continuously gossip about information associated with the participating nodes. Typically, propagation latency isn't a concern, perhaps because the information in question changes slowly or there is no significant penalty for acting upon slightly stale data.

- **Protocols that compute aggregates**. These compute a network-wide aggregate by sampling information at the nodes in the network and combining the values to arrive at a system-wide value – the largest value for some measurement nodes are making, smallest, etc. The key requirement is that the aggregate must be computable by fixed-size pairwise information exchanges; these typically terminate after a number of rounds of information exchange logarithmic in the system size, by which time an all-to-all information flow pattern will have been established. As a side effect of aggregation, it is possible to solve other kinds of problems using gossip; for example, there are gossip protocols that can arrange the nodes in a gossip overlay into a list sorted by node-id (or some other attribute) in logarithmic time using aggregation-style exchanges of information. Similarly, there are gossip algorithms that arrange nodes into a tree and compute aggregates such as "sum" or "count" by gossiping in a pattern biased to match the tree structure.

 

Many protocols that predate the earliest use of the term "gossip" fall within this rather inclusive definition. For example, Internet [routing protocols](./Routing_protocol) often use gossip-like information exchanges. A gossip substrate can be used to implement a standard routed network: nodes "gossip" about traditional point-to-point messages, effectively pushing traffic through the gossip layer. Bandwidth permitting, this implies that a gossip system can potentially support any classic protocol or implement any classical distributed service. However, such a broadly inclusive interpretation is rarely intended. More typically gossip protocols are those that specifically run in a regular, periodic, relatively lazy, symmetric and decentralized manner; the high degree of symmetry among nodes is particularly characteristic. Thus, while one could run a [2-phase commit protocol](./Two-phase_commit_protocol) over a gossip substrate, doing so would be at odds with the spirit, if not the wording, of the definition.

 

The term *convergently consistent* is sometimes used to describe protocols that achieve exponentially rapid spread of information. For this purpose, a protocol must propagate any new information to all nodes that will be affected by the information within time logarithmic in the size of the system (the "mixing time" must be logarithmic in system size).

 

## Examples

 

Suppose that we want to find the object that most closely matches some search pattern, within a network of unknown size, but where the computers are linked to one another and where each machine is running a small *agent* program that implements a gossip protocol.

 
- To start the search, a user would ask the local agent to begin to gossip about the search string. (We're assuming that agents either start with a known list of peers, or retrieve this information from some kind of a shared store.)
- Periodically, at some rate (let's say ten times per second, for simplicity), each agent picks some other agent at random, and gossips with it. Search strings known to A will now also be known to B, and vice versa. In the next "round" of gossip A and B will pick additional random peers, maybe C and D. This round-by-round doubling phenomenon makes the protocol very robust, even if some messages get lost, or some of the selected peers are the same or already know about the search string.
- On receipt of a search string for the first time, each agent checks its local machine for matching documents.
- Agents also gossip about the best match, to date. Thus, if A gossips with B, after the interaction, A will know of the best matches known to B, and vice versa. Best matches will "spread" through the network.

 

If the messages might get large (for example, if many searches are active all at the same time), a size limit should be introduced. Also, searches should "age out" of the network.

 

It follows that within logarithmic time in the size of the network (the number of agents), any new search string will have reached all agents. Within an additional delay of the same approximate length, every agent will learn where the best match can be found. In particular, the agent that started the search will have found the best match.

 

For example, in a network with 25,000 machines, we can find the best match after about 30 rounds of gossip: 15 to spread the search string and 15 more to discover the best match. A gossip exchange could occur as often as once every tenth of a second without imposing undue load, hence this form of network search could search a big [data center](./Data_center) in about three seconds.

 

In this scenario, searches might automatically age out of the network after, say, 10 seconds. By then, the initiator knows the answer and there is no point in further gossip about that search.

 

Gossip protocols have also been used for achieving and maintaining [distributed database](./Distributed_database) [consistency](./Consistency) or with other types of data in consistent states, counting the number of nodes in a network of unknown size, spreading news robustly, organizing nodes according to some structuring policy, building so-called [overlay networks](./Overlay_network), computing aggregates, sorting the nodes in a network, electing leaders, etc.

 

## Epidemic algorithms

 

Gossip protocols can be used to propagate information in a manner rather similar to the way that a viral infection spreads in a biological population. Indeed, the [mathematics](./Mathematics) of epidemics are often used to model the mathematics of gossip communication. The term *epidemic algorithm* is sometimes employed when describing a [software system](./Software_system) in which this kind of gossip-based information propagation is employed.

 

## See also

 
- Gossip protocols are just one class among many classes of networking protocols. See also [virtual synchrony](./Virtual_synchrony), distributed [state machines](./State_machine), [Paxos algorithm](./Paxos_algorithm), database [transactions](./Database_transaction). Each class contains tens or even hundreds of protocols, differing in their details and performance properties but similar at the level of the guarantees offered to users.
- Some gossip protocols replace the random peer selection mechanism with a more deterministic scheme. For example, in the [NeighbourCast](http://www.actapress.com/PDFViewer.aspx?paperId=31994) algorithm, instead of talking to random nodes, information is spread by talking only to neighbouring nodes. There are a number of algorithms that use similar ideas. A key requirement when designing such protocols is that the neighbor set trace out an [expander graph](./Expander_graph).
- [Routing](./Routing)
- [Tribler](./Tribler), BitTorrent peer-to-peer client using gossip protocol.

 

## References

  
1. [↑](./Gossip_protocol#cite_ref-1) Demers, Alan; Greene, Dan; Hauser, Carl; Irish, Wes; Larson, John (1987). "Epidemic algorithms for replicated database maintenance". *Proceedings of the sixth annual ACM Symposium on Principles of distributed computing - PODC '87*. pp. 1–12. [doi](./Doi_(identifier)):[10.1145/41840.41841](https://doi.org/10.1145%2F41840.41841). [ISBN](./ISBN_(identifier)) [978-0-89791-239-6](./Special:BookSources/978-0-89791-239-6). [OCLC](./OCLC_(identifier)) [8876960204](https://search.worldcat.org/oclc/8876960204). [S2CID](./S2CID_(identifier)) [1889203](https://api.semanticscholar.org/CorpusID:1889203).
2. [↑](./Gossip_protocol#cite_ref-2) Jelasity, Márk (2011-01-01). ["Gossip"](http://publicatio.bibl.u-szeged.hu/1529/1/gossip11.pdf) (PDF). In Serugendo, Giovanna Di Marzo; Gleizes, Marie-Pierre; Karageorgos, Anthony (eds.). *Self-organising Software*. Natural Computing Series. Springer Berlin Heidelberg. pp. 139–162. [doi](./Doi_(identifier)):[10.1007/978-3-642-17348-6_7](https://doi.org/10.1007%2F978-3-642-17348-6_7). [ISBN](./ISBN_(identifier)) [978-3-642-17347-9](./Special:BookSources/978-3-642-17347-9). [S2CID](./S2CID_(identifier)) [214970849](https://api.semanticscholar.org/CorpusID:214970849).

 

## Further reading

  
- Allavena, André; Demers, Alan; Hopcroft, John E. (2005). "Correctness of a gossip based membership protocol". *Proceedings of the twenty-fourth annual ACM SIGACT-SIGOPS symposium on Principles of distributed computing - PODC '05*. p. 292. [doi](./Doi_(identifier)):[10.1145/1073814.1073871](https://doi.org/10.1145%2F1073814.1073871). [ISBN](./ISBN_(identifier)) [978-1-58113-994-5](./Special:BookSources/978-1-58113-994-5). [OCLC](./OCLC_(identifier)) [8876665695](https://search.worldcat.org/oclc/8876665695). [S2CID](./S2CID_(identifier)) [9378092](https://api.semanticscholar.org/CorpusID:9378092).
- Birman, Kenneth P.; Hayden, Mark; Ozkasap, Oznur; Xiao, Zhen; Budiu, Mihai; Minsky, Yaron (May 1999). ["Bimodal multicast"](https://doi.org/10.1145%2F312203.312207). *ACM Transactions on Computer Systems*. **17** (2): 41–88. [doi](./Doi_(identifier)):[10.1145/312203.312207](https://doi.org/10.1145%2F312203.312207). [S2CID](./S2CID_(identifier)) [207744063](https://api.semanticscholar.org/CorpusID:207744063).
- Eugster, P. Th.; Guerraoui, R.; Handurukande, S. B.; Kouznetsov, P.; Kermarrec, A.-M. (November 2003). ["Lightweight probabilistic broadcast"](https://infoscience.epfl.ch/record/52369/files/IC_TECH_REPORT_200102.pdf) (PDF). *ACM Transactions on Computer Systems*. **21** (4): 341–374. [doi](./Doi_(identifier)):[10.1145/945506.945507](https://doi.org/10.1145%2F945506.945507). [S2CID](./S2CID_(identifier)) [6875620](https://api.semanticscholar.org/CorpusID:6875620).
- Gupta, Indranil; Birman, Ken; Linga, Prakash; Demers, Al; Van Renesse, Robbert (2003). "Kelips: Building an Efficient and Stable P2P DHT through Increased Memory and Background Overhead". *Peer-to-Peer Systems II*. Lecture Notes in Computer Science. Vol. 2735. pp. 160–169. [doi](./Doi_(identifier)):[10.1007/978-3-540-45172-3_15](https://doi.org/10.1007%2F978-3-540-45172-3_15). [ISBN](./ISBN_(identifier)) [978-3-540-40724-9](./Special:BookSources/978-3-540-40724-9).
- Systematic Design of P2P Technologies for Distributed Systems. Indranil Gupta, Global Data Management, eds: R. Baldoni, G. Cortese, F. Davide and A. Melpignano, 2006.
- Leitao, Joao; Pereira, Jose; Rodrigues, Luis (2007). "HyParView: A Membership Protocol for Reliable Gossip-Based Broadcast". *37th Annual IEEE/IFIP International Conference on Dependable Systems and Networks (DSN'07)*. pp. 419–429. [doi](./Doi_(identifier)):[10.1109/DSN.2007.56](https://doi.org/10.1109%2FDSN.2007.56). [hdl](./Hdl_(identifier)):[1822/38895](https://hdl.handle.net/1822%2F38895). [ISBN](./ISBN_(identifier)) [978-0-7695-2855-7](./Special:BookSources/978-0-7695-2855-7). [S2CID](./S2CID_(identifier)) [9060122](https://api.semanticscholar.org/CorpusID:9060122).
- Gupta, I.; Kermarrec, A.-M.; Ganesh, A.J. (July 2006). "Efficient and adaptive epidemic-style protocols for reliable and scalable multicast". *IEEE Transactions on Parallel and Distributed Systems*. **17** (7): 593–605. [doi](./Doi_(identifier)):[10.1109/TPDS.2006.85](https://doi.org/10.1109%2FTPDS.2006.85). [S2CID](./S2CID_(identifier)) [1148979](https://api.semanticscholar.org/CorpusID:1148979).
- Jelasity, Márk; Montresor, Alberto; Babaoglu, Ozalp (August 2009). ["T-Man: Gossip-based fast overlay topology construction"](http://www.cs.unibo.it/babaoglu/papers/pdf/comnet09.pdf) (PDF). *Computer Networks*. **53** (13): 2321–2339. [doi](./Doi_(identifier)):[10.1016/j.comnet.2009.03.013](https://doi.org/10.1016%2Fj.comnet.2009.03.013).
- Leitao, Joao; Pereira, Jose; Rodrigues, Luis (2007). "Epidemic Broadcast Trees". *2007 26th IEEE International Symposium on Reliable Distributed Systems (SRDS 2007)*. pp. 301–310. [doi](./Doi_(identifier)):[10.1109/SRDS.2007.27](https://doi.org/10.1109%2FSRDS.2007.27). [hdl](./Hdl_(identifier)):[1822/38894](https://hdl.handle.net/1822%2F38894). [ISBN](./ISBN_(identifier)) [978-0-7695-2995-0](./Special:BookSources/978-0-7695-2995-0). [S2CID](./S2CID_(identifier)) [7210467](https://api.semanticscholar.org/CorpusID:7210467).
- Jelasity, Márk; Montresor, Alberto; Babaoglu, Ozalp (August 2005). ["Gossip-based aggregation in large dynamic networks"](http://publicatio.bibl.u-szeged.hu/1501/1/212788%20%202.pdf) (PDF). *ACM Transactions on Computer Systems*. **23** (3): 219–252. [doi](./Doi_(identifier)):[10.1145/1082469.1082470](https://doi.org/10.1145%2F1082469.1082470). [S2CID](./S2CID_(identifier)) [2608879](https://api.semanticscholar.org/CorpusID:2608879).
- Ordered slicing of very large overlay networks. Márk Jelasity and Anne-Marie Kermarrec. IEEE P2P, 2006.
- Proximity-aware superpeer overlay topologies. Gian Paolo Jesi, Alberto Montresor, and Ozalp Babaoglu.  IEEE Transactions on Network and Service Management, 4(2):74–83, September 2007.
- X-BOT: A Protocol for Resilient Optimization of Unstructured Overlays. João Leitão, João Marques, José Pereira, Luís Rodrigues. Proc. 28th IEEE [International Symposium on Reliable Distributed Systems](./International_Symposium_on_Reliable_Distributed_Systems) (SRDS'09).
- Spatial gossip and resource location protocols. David Kempe, Jon Kleinberg, Alan Demers. [Journal of the ACM](./Journal_of_the_ACM) (JACM) 51: 6 (Nov 2004).
- Gossip-Based Computation of Aggregate Information. David Kempe, Alin Dobra, Johannes Gehrke. Proc. 44th Annual IEEE [Symposium on Foundations of Computer Science](./Symposium_on_Foundations_of_Computer_Science) (FOCS). 2003.
- Active and Passive Techniques for Group Size Estimation in Large-Scale and Dynamic Distributed Systems. Dionysios Kostoulas, Dimitrios Psaltoulis, Indranil Gupta, Ken Birman, Al Demers. Elsevier [Journal of Systems and Software](./Journal_of_Systems_and_Software), 2007.
- Build One, Get One Free: Leveraging the Coexistence of Multiple P2P Overlay Networks. Balasubramaneyam Maniymaran, Marin Bertier and Anne-Marie Kermarrec. Proc. [ICDCS](./International_Conference_on_Distributed_Computing_Systems), June 2007.
- Peer counting and sampling in overlay networks: random walk methods. Laurent Massoulié, Erwan Le Merrer, Anne-Marie Kermarrec, Ayalvadi Ganesh. Proc. 25th ACM [PODC](./Symposium_on_Principles_of_Distributed_Computing). Denver, 2006.
- Chord on Demand. Alberto Montresor, Márk Jelasity, and Ozalp Babaoglu. Proc. 5th Conference on Peer-to-Peer Computing (P2P),  Konstanz, Germany, August 2005.
- Nielsen, Michael A. (2005). ["Introduction to expander graphs"](https://web.archive.org/web/20110715104440/https://michaelnielsen.org/blog/archive/notes/expander_graphs.pdf) (PDF). *Michael Nielsen*. [S2CID](./S2CID_(identifier)) [3045708](https://api.semanticscholar.org/CorpusID:3045708). Archived from [the original](https://michaelnielsen.org/blog/archive/notes/expander_graphs.pdf) (PDF) on 2011-07-15.
- Building low-diameter P2P networks. G. Pandurangan, P. Raghavan, [Eli Upfal](./Eli_Upfal). In Proceedings of the 42nd [Symposium on Foundations of Computer Science](./Symposium_on_Foundations_of_Computer_Science) (FOCS),  2001.
- Van Renesse, Robbert; Birman, Kenneth P.; Vogels, Werner (May 2003). "Astrolabe: A robust and scalable technology for distributed system monitoring, management, and data mining". *ACM Transactions on Computer Systems*. **21** (2): 164–206. [doi](./Doi_(identifier)):[10.1145/762483.762485](https://doi.org/10.1145%2F762483.762485). [S2CID](./S2CID_(identifier)) [6204358](https://api.semanticscholar.org/CorpusID:6204358).
- Voulgaris, S.; Kermarrec, A.-M.; Massoulie, L.; Van Steen, M. (2004). "Exploiting semantic proximity in peer-to-peer content searching". [*Proceedings. 10th IEEE International Workshop on Future Trends of Distributed Computing Systems, 2004. FTDCS 2004*](https://research.vu.nl/en/publications/bd1b1469-29cd-4b4a-a549-f2dfc2acdd64). pp. 238–243. [doi](./Doi_(identifier)):[10.1109/FTDCS.2004.1316622](https://doi.org/10.1109%2FFTDCS.2004.1316622). [hdl](./Hdl_(identifier)):[1871/12832](https://hdl.handle.net/1871%2F12832). [ISBN](./ISBN_(identifier)) [0-7695-2118-5](./Special:BookSources/0-7695-2118-5). [S2CID](./S2CID_(identifier)) [9464168](https://api.semanticscholar.org/CorpusID:9464168).
- Gupta, Ruchir; Singh, Yatindra Nath (2015). "Reputation Aggregation in Peer-to-Peer Network Using Differential Gossip Algorithm". *IEEE Transactions on Knowledge and Data Engineering*. **27** (10): 2812–2823. [arXiv](./ArXiv_(identifier)):[1210.4301](https://arxiv.org/abs/1210.4301). [doi](./Doi_(identifier)):[10.1109/TKDE.2015.2427793](https://doi.org/10.1109%2FTKDE.2015.2427793). [S2CID](./S2CID_(identifier)) [650473](https://api.semanticscholar.org/CorpusID:650473).
- Bailey, Norman T. J. (1957). *The Mathematical Theory of Epidemics*. Hafner. [ISBN](./ISBN_(identifier)) [978-0-85264-113-2](./Special:BookSources/978-0-85264-113-2). `{{cite book}}`: ISBN / Date incompatibility ([help](./Help:CS1_errors#invalid_isbn_date))

  

 Interwikies 

 Categories