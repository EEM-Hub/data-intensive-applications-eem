---
source: https://en.wikipedia.org/wiki/Byzantine_fault
fetched: 2026-06-19
---

Fault in a computer system that presents different symptoms to different observers For other uses, see [Byzantine (disambiguation)](./Byzantine_(disambiguation)). 

A **Byzantine fault** is a condition of a system, particularly a [distributed computing](./Distributed_computing) system, where a fault occurs such that different symptoms are presented to different observers, including imperfect information on whether a system component has failed. The term takes its name from an [allegory](./Allegory), the "Byzantine generals problem",[[1]](./Byzantine_fault#cite_note-:1-1) developed to describe a situation in which, to avoid catastrophic failure of a system, the system's actors must agree on a strategy, but some of these actors are unreliable in  a way which causes other (good) actors to disagree on the strategy and they may be unaware of the disagreement.

 

A Byzantine fault is also known as a **Byzantine generals problem**, a **Byzantine agreement problem**, or a **Byzantine failure**.

 

**Byzantine fault tolerance** (**BFT**) is the resilience of a [fault-tolerant computer system](./Fault-tolerant_computer_system) or similar system to such conditions.

 

## Definition

 

A Byzantine fault is any fault presenting different symptoms to different observers.[[2]](./Byzantine_fault#cite_note-DriscollHall2004-2) A Byzantine failure is the loss of a system service due to a Byzantine fault in systems that require [consensus](./Consensus_(computer_science)) among multiple components.[[3]](./Byzantine_fault#cite_note-DriscollHall2003-3)

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/f/fc/Byzantine_Generals.png/330px-Byzantine_Generals.png)](./File:Byzantine_Generals.png)If all generals attack in coordination, the battle is won (left). If two generals falsely declare that they intend to attack, but instead retreat, the battle is lost (right). 

The Byzantine allegory considers a number of generals who are attacking a fortress. The generals must decide as a group whether to attack or retreat; some may prefer to attack, while others prefer to retreat. The important thing is that all generals agree on a common decision, for a half-hearted attack by a few generals would become a [rout](./Rout), and would be worse than either a coordinated attack or a coordinated retreat.

 

The problem is complicated by the presence of treacherous generals who may not only cast a vote for a suboptimal strategy; they may do so selectively. For instance, if nine generals are voting, four of whom support attacking while four others are in favor of retreat, the ninth general may send a vote of retreat to those generals in favor of retreat, and a vote of attack to the rest. Those who received a retreat vote from the ninth general will retreat, while the rest will attack (which may not go well for the attackers). The problem is complicated further by the generals being physically separated and having to send their votes via messengers who may fail to deliver votes or may forge false votes.

 

Without message signing, Byzantine fault tolerance can only be achieved if the total number of generals is greater than three times the number of disloyal (faulty) generals. There can be a default vote value given to missing messages. For example, missing messages can be given a ["null" value](./Uninitialized_variable). Further, if the agreement is that the null votes are in the majority, a pre-assigned default strategy can be used (e.g., retreat).[[4]](./Byzantine_fault#cite_note-BGP_Paper-4)

 

The typical mapping of this allegory onto computer systems is that the computers are the generals and their digital communication system links are the messengers. Although the problem is formulated in the allegory as a decision-making and security problem, in electronics, it cannot be solved by [cryptographic](./Cryptographic) [digital signatures](./Digital_signature) alone, because failures such as incorrect voltages can propagate through the encryption process. Thus, a faulty message could be sent such that some recipients detect the message as faulty (bad signature), others see it is having a good signature, and a third group also sees a good signature but with different message contents than the second group.[[2]](./Byzantine_fault#cite_note-DriscollHall2004-2)

 

## History

 

The problem of obtaining Byzantine consensus was conceived and formalized by [Robert Shostak](./Robert_Shostak), who dubbed it the *interactive consistency* problem. This work was done in 1978 in the context of the NASA-sponsored SIFT[[5]](./Byzantine_fault#cite_note-:0-5) project in the Computer Science Lab at [SRI International](./SRI_International). SIFT (for Software Implemented Fault Tolerance) was the brainchild of John Wensley, and was based on the idea of using multiple general-purpose computers that would communicate through pairwise messaging in order to reach a consensus, even if some of the computers were faulty.

 

At the beginning of the project, it was not clear how many computers in total were needed to guarantee that a conspiracy of *n* faulty computers could not "thwart" the efforts of the correctly-operating ones to reach consensus. Shostak showed that a minimum of 3*n+*1 are needed, and devised a two-round 3*n+1* messaging protocol that would work for *n*=1. His colleague Marshall Pease generalized the algorithm for any n > 0, proving that 3*n*+1 is both necessary and sufficient. These results, together with a later proof by [Leslie Lamport](./Leslie_Lamport) of the sufficiency of 3*n* using digital signatures, were published in the seminal paper, *Reaching Agreement in the Presence of Faults.*[[6]](./Byzantine_fault#cite_note-6) The authors were awarded the 2005 [Edsger W. Dijkstra Prize](./Edsger_W._Dijkstra_Prize) for this paper.

 

To make the interactive consistency problem easier to understand, Lamport devised a colorful allegory in which a group of army generals formulate a plan for attacking a city. In its original version, the story cast the generals as commanders of the [Albanian](./Albania) army. The name was changed, eventually settling on "[Byzantine](./Byzantine_Empire)", at the suggestion of Jack Goldberg to future-proof any potential offense-giving.[[7]](./Byzantine_fault#cite_note-7) This formulation of the problem, together with some additional results, were presented by the same authors in their 1982 paper, "The Byzantine Generals Problem".[[4]](./Byzantine_fault#cite_note-BGP_Paper-4)

 

## Mitigation

 

The objective of Byzantine fault tolerance is to be able to defend against failures of system components with or without symptoms that prevent other components of the system from reaching an agreement among themselves, where such an agreement is needed for the correct operation of the system.

 

The remaining operationally correct components of a Byzantine fault tolerant system will be able to continue providing the system's service as originally intended, assuming there are a sufficient number of accurately-operating components to maintain the service.

 

When considering failure propagation only via errors, Byzantine failures are considered the most general and most difficult class of failures among the [failure modes](./Failure_cause). The so-called fail-stop failure mode occupies the simplest end of the spectrum. Whereas the fail-stop failure mode simply means that the only way to fail is a [node](./Node_(computer_science)) crash, detected by other nodes, Byzantine failures imply no restrictions on what errors can be created, which means that a failed node can generate arbitrary data, including data that makes it appear like a functioning node to a subset of other nodes. Thus, Byzantine failures can confuse failure detection systems, which makes fault tolerance difficult. Despite the allegory, a Byzantine failure is not necessarily a [security](./Security) problem involving hostile human interference: it can arise purely from physical or software faults.

 

The terms fault and failure are used here according to the standard definitions[[8]](./Byzantine_fault#cite_note-AvizienisLaprie2004-8) originally created by a joint committee on "Fundamental Concepts and Terminology" formed by the [IEEE](./IEEE) Computer Society's Technical Committee on Dependable Computing and Fault-Tolerance and [IFIP](./IFIP) Working Group 10.4 on Dependable Computing and Fault Tolerance.[[9]](./Byzantine_fault#cite_note-9) See also [dependability](./Dependability).

 

Byzantine fault tolerance is only concerned with broadcast consistency, that is, the property that when a component broadcasts a value to all the other components, they all receive exactly this same value, or in the case that the broadcaster is not consistent, the other components agree on a common value themselves. This kind of fault tolerance does not encompass the correctness of the value itself; for example, an adversarial component that deliberately sends an incorrect value, but sends that same value consistently to all components, will not be caught in the Byzantine fault tolerance scheme.

 

## Solutions

 

Several early solutions were described by Lamport, Shostak, and Pease in 1982.[[4]](./Byzantine_fault#cite_note-BGP_Paper-4) They began by noting that the Generals' Problem can be reduced to solving a "Commander and Lieutenants" problem where loyal Lieutenants must all act in unison and that their action must correspond to what the Commander ordered in the case that the Commander is loyal:

 
- One solution considers scenarios in which messages may be forged, but which will be *Byzantine-fault-tolerant* as long as the number of disloyal generals is less than one third of the generals. The impossibility of dealing with one-third or more traitors ultimately reduces to proving that the one Commander and two Lieutenants problem cannot be solved, if the Commander is traitorous. To see this, suppose we have a traitorous Commander A, and two Lieutenants, B and C: when A tells B to attack and C to retreat, and B and C send messages to each other, forwarding A's message, neither B nor C can figure out who is the traitor, since it is not necessarily A—the other Lieutenant could have forged the message purportedly from A. It can be shown that if *n* is the number of generals in total, and *t* is the number of traitors in that *n*, then there are solutions to the problem only when *n* > 3*t* and the communication is synchronous (bounded delay).[[10]](./Byzantine_fault#cite_note-10) The full set of BFT requirements are: For *F* number of Byzantine failures, there needs to be at least 3*F*+1 players (fault containment zones), 2*F*+1 independent communication paths, and *F*+1 rounds of communication. There can be hybrid fault models in which benign (non-Byzantine) faults as well as Byzantine faults may exist simultaneously. For each additional benign fault that must be tolerated, the above numbers need to be incremented by one. If the BFT rounds of communication do not exist, Byzantine failures can occur even with no faulty hardware.
- A second solution requires unforgeable message signatures. For [security-critical systems](./Critical_system#Security_critical), [digital signatures](./Digital_signature) (in modern computer systems, this may be achieved, in practice, by using [public-key cryptography](./Public-key_cryptography)) can provide Byzantine fault tolerance in the presence of an arbitrary number of traitorous generals. However, for [safety-critical systems](./Safety-critical_system) (where "security" addresses intelligent threats while "safety" addresses the inherent dangers of an activity or mission, i.e., faults due to natural phenomena), error detecting codes, such as [CRCs](./Cyclic_redundancy_check), provide stronger coverage at a much lower cost. (Note that CRCs can provide guaranteed coverage for errors that cryptography cannot. If an encryption scheme could provide some guarantee of coverage for message errors, it would have a structure that would make it insecure.[[11]](./Byzantine_fault#cite_note-11) [*[dubious](./Wikipedia:Accuracy_dispute#Disputed_statement) – [discuss](./Talk:Byzantine_fault#Dubious)*]) But neither [digital signatures](./Digital_signature) nor error detecting codes such as CRCs provide a known level of protection against Byzantine errors from natural causes. More generally, security measures can weaken safety and vice versa. Thus, cryptographic digital signature methods are not a good choice for safety-critical systems, unless there is also a specific security threat as well.[[12]](./Byzantine_fault#cite_note-PaulitschMorris2005-12) While error detecting codes, such as CRCs, are better than cryptographic techniques, neither provide adequate coverage for active electronics in safety-critical systems. This is illustrated by the *Schrödinger CRC* scenario where a CRC-protected message with a single Byzantine faulty bit presents different data to different observers and each observer sees a valid CRC.[[2]](./Byzantine_fault#cite_note-DriscollHall2004-2)[[3]](./Byzantine_fault#cite_note-DriscollHall2003-3)
- Also presented is a variation on the first two solutions allowing Byzantine-fault-tolerant behavior in some situations where not all generals can communicate directly with each other.[[1]](./Byzantine_fault#cite_note-:1-1)

 

There are many systems that claim BFT without meeting the above minimum requirements (e.g., blockchain). Given that there is [mathematical proof](./Mathematical_proof) that this is impossible, these claims need to include a caveat that their definition of BFT strays from the original. That is, systems such as blockchain don't guarantee agreement. They use resource-intensive mechanisms that make disagreements impractical to maintain.

 

Several system architectures were designed c. 1980 that implemented Byzantine fault tolerance. These include: Draper's FTMP,[[13]](./Byzantine_fault#cite_note-HopkinsLala1987-13) Honeywell's MMFCS,[[14]](./Byzantine_fault#cite_note-MMFCS-14) and SRI's SIFT.[[5]](./Byzantine_fault#cite_note-:0-5)

 

In 1999, Miguel Castro and [Barbara Liskov](./Barbara_Liskov) introduced the "Practical Byzantine Fault Tolerance" (PBFT) algorithm,[[15]](./Byzantine_fault#cite_note-15) which provides high-performance Byzantine state machine replication, processing thousands of requests per second with sub-millisecond increases in latency.

 

After PBFT, several BFT protocols were introduced to improve its robustness and performance. For instance, Q/U,[[16]](./Byzantine_fault#cite_note-16) HQ,[[17]](./Byzantine_fault#cite_note-17) Zyzzyva,[[18]](./Byzantine_fault#cite_note-18) and ABsTRACTs,[[19]](./Byzantine_fault#cite_note-19) addressed the performance and cost issues; whereas other protocols, like Aardvark[[20]](./Byzantine_fault#cite_note-20) and RBFT,[[21]](./Byzantine_fault#cite_note-21) addressed its robustness issues. Furthermore, Adapt[[22]](./Byzantine_fault#cite_note-22) tried to make use of existing BFT protocols, through switching between them in an adaptive way, to improve system robustness and performance as the underlying conditions change. Furthermore, BFT protocols were introduced that leverage trusted components to reduce the number of replicas, e.g., A2M-PBFT-EA[[23]](./Byzantine_fault#cite_note-23) and MinBFT.[[24]](./Byzantine_fault#cite_note-24)

 

Recent research addresses the scalability limits of traditional BFT implementations (which often incur     O (  n  2   )   {\displaystyle O(n^{2})}  ![{\displaystyle O(n^{2})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6cd9594a16cb898b8f2a2dff9227a385ec183392) [communication complexity](./Communication_complexity)) by parallelizing consensus. For example, the Cerberus protocol maps data to a large, fixed state space to couple consensus instances with specific transaction sets. This allows BFT processes to run independently in parallel, enabling linear scalability relative to the network size.[[25]](./Byzantine_fault#cite_note-VLDB2021-25)

 

## Applications

 

Several examples of Byzantine failures that have occurred are given in two equivalent journal papers.[[2]](./Byzantine_fault#cite_note-DriscollHall2004-2)[[3]](./Byzantine_fault#cite_note-DriscollHall2003-3) These and other examples are described on the [NASA](./NASA) DASHlink web pages.[[26]](./Byzantine_fault#cite_note-26)

 

### Applications in computing

 

Byzantine fault tolerance mechanisms use components that repeat an incoming message (or just its signature, which can be reduced to just a single bit of information if self-checking pairs are used for nodes) to other recipients of that incoming message. All these mechanisms make the assumption that the act of repeating a message blocks the propagation of Byzantine symptoms. For systems that have a high degree of safety or security criticality, these assumptions must be proven to be true to an acceptable level of [fault coverage](./Fault_coverage). When providing proof through testing, one difficulty is creating a sufficiently wide range of signals with Byzantine symptoms.[[27]](./Byzantine_fault#cite_note-NanyaGoosen1989-27) Such testing will likely require specialized [fault injectors](./Fault_injection).[[28]](./Byzantine_fault#cite_note-MartinsGandhi2013-28)[[29]](./Byzantine_fault#cite_note-29)

 

### Military applications

 

Byzantine errors were observed infrequently and at irregular points during endurance testing for the newly constructed [*Virginia*-class submarine](./Virginia-class_submarine), at least through 2005 (when the issues were publicly reported).[[30]](./Byzantine_fault#cite_note-WalterEllis2005-30)

 

### Cryptocurrency applications

 

The [Bitcoin network](./Bitcoin_network) works in parallel to generate a [blockchain](./Blockchain) with [proof of work](./Proof_of_work) allowing the system to overcome Byzantine failures and reach a coherent global view of the system's state.[[31]](./Byzantine_fault#cite_note-31)[[32]](./Byzantine_fault#cite_note-32) Some [proof of stake](./Proof_of_stake) blockchains also use BFT algorithms.[[33]](./Byzantine_fault#cite_note-FOOTNOTEDeirmentzoglouPapakyriakopoulosPatsakis201928716-33)

 

### Blockchain

 

Byzantine fault tolerance is a crucial concept in [blockchain](./Blockchain) technology, ensuring that a network can continue to function even when some nodes[[34]](./Byzantine_fault#cite_note-34)[*[full citation needed](./Wikipedia:Citing_sources#What_information_to_include)*] (participants) fail or act maliciously. This tolerance is necessary because blockchains are decentralized systems with no central authority, making it essential to achieve consensus among nodes, even if some try to disrupt the process.

 

### Artificial Intelligence

 

Ensuring that an [AI](./AI) system behaves reliably and as intended, especially in the presence of unexpected faults or adversarial conditions, is a complex challenge. By accepting that components may fail, and further that frontier AI models may deceive, Byzantine fault tolerance has been proposed as an approach towards [AI safety](./AI_safety).[[35]](./Byzantine_fault#cite_note-35) Structuring AI systems as ensembles of AI artifacts or modules that check and balance each other leads to strong assurances that no single errant or deceptive component can easily steer the system into an unsafe state.

 

#### Applications and examples

 Safety mechanismsDifferent blockchains use various BFT-based consensus mechanisms like Practical Byzantine Fault Tolerance (PBFT), Tendermint, and [Delegated Proof of Stake (DPoS)](./Delegated_Proof_of_Stake_(DPoS)) to handle Byzantine faults. These protocols ensure that the majority of honest nodes can agree on the next block in the chain, securing the network against attacks and preventing [double-spending](./Double-spending) and other types of fraud. Practical examples of networks include [Hyperledger Fabric](./Hyperledger), [Cosmos](./Cosmos_Blockchain?action=edit&redlink=1) and [Klever](./Klever_blockchain?action=edit&redlink=1) in this sequence. 51% attack mitigationWhile traditional blockchains like Bitcoin use proof of work (PoW), which is susceptible to a [51% attack](./51%25_attack), BFT-based systems are designed to tolerate up to one-third of faulty or malicious nodes without compromising the network's integrity. Decentralized trustByzantine fault tolerance underpins the trust model in [decentralized](./Decentralization) networks. Instead of relying on a central authority, the network's security depends on the ability of honest nodes to outnumber and outmaneuver malicious ones. Private and permissioned blockchainsBFT is especially important in private or permissioned blockchains, where a limited number of known participants need to reach a consensus quickly and securely. These networks often use BFT protocols to enhance performance and security. 

### In aviation

 

Some aircraft systems, such as the Boeing 777 [Aircraft Information Management System](./Aircraft_Information_Management_System) (via its [ARINC](./ARINC) 659 SAFEbus network), the Boeing 777 flight control system, and the Boeing 787 flight control systems, use Byzantine fault tolerance; because these are real-time systems, their Byzantine fault tolerance solutions must have very low latency. For example, SAFEbus can achieve Byzantine fault tolerance within the order of a microsecond of added latency.[[36]](./Byzantine_fault#cite_note-Zurawski2015-36)[[37]](./Byzantine_fault#cite_note-HenzingerKirsch2001-37)[[38]](./Byzantine_fault#cite_note-Yeh2001-38)

 

### In space systems

 

The [SpaceX Dragon](./SpaceX_Dragon) considers Byzantine fault tolerance in its design.[[39]](./Byzantine_fault#cite_note-39) The [Ares](./Ares_I) rocket avionics, now the [Space Launch System](./Space_Launch_System) (SLS),  utilizes a triplex with an interstage of accomplish Byzantine resilience.[[40]](./Byzantine_fault#cite_note-40)[[41]](./Byzantine_fault#cite_note-41) The [Orion](./Orion_(spacecraft)) spacecraft utilizes self-checking pairs to detect and mask Byzantine faults.[[42]](./Byzantine_fault#cite_note-42)

 

### In democracy and civil societies

 

In [legislatures](./Legislatures), [civil societies](./Civil_societies), [polls](./Elections), [statistical surveys](./Survey_methodology), and so forth, systems that require a minimum supermajority threshold agreement greater than [two-thirds](./Two-thirds_rule) are similar to consensus reflective of Byzantine Fault Tolerant -like characteristics. By contrast, systems that operate on the sub-supermajority basis of [simple majorities](./Majority) or a [minority government](./Minority_government) could be vulnerable to Byzantine fault -like behavior.

 

## See also

 
- [Atomic commit](./Atomic_commit) – Operation that applies a set of distinct changes as a single operation
- [Brooks–Iyengar algorithm](./Brooks–Iyengar_algorithm) – Distributed algorithm for sensor networks
- [Conflict-free replicated data type](./Conflict-free_replicated_data_type) – Type of data structure
- [List of terms relating to algorithms and data structures](./List_of_terms_relating_to_algorithms_and_data_structures?action=edit&redlink=1)
- [Paxos (computer science)](./Paxos_(computer_science)) – Family of protocols for solving consensus
- [Quantum Byzantine agreement](./Quantum_Byzantine_agreement) – Quantum version of the Byzantine agreement protocol
- [Two Generals' Problem](./Two_Generals'_Problem) – Thought experiment
- [Two-thirds supermajority rule](./Two-thirds_rule) – Voting requirement above 2⁄3 for passage

 

## References

  
1. [1](./Byzantine_fault#cite_ref-:1_1-0) [2](./Byzantine_fault#cite_ref-:1_1-1) [Lamport, L.](./Leslie_Lamport); Shostak, R.; Pease, M. (1982). ["The Byzantine Generals Problem"](https://www.microsoft.com/en-us/research/publication/byzantine-generals-problem/?from=http%3A%2F%2Fresearch.microsoft.com%2Fen-us%2Fum%2Fpeople%2Flamport%2Fpubs%2Fbyz.pdf) (PDF). *ACM Transactions on Programming Languages and Systems*. **4** (3): 382–401. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.64.2312](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.64.2312). [doi](./Doi_(identifier)):[10.1145/357172.357176](https://doi.org/10.1145%2F357172.357176). [S2CID](./S2CID_(identifier)) [55899582](https://api.semanticscholar.org/CorpusID:55899582). [Archived](https://web.archive.org/web/20180613015025/https://www.microsoft.com/en-us/research/publication/byzantine-generals-problem/?from=http%3A%2F%2Fresearch.microsoft.com%2Fen-us%2Fum%2Fpeople%2Flamport%2Fpubs%2Fbyz.pdf) (PDF) from the original on 13 June 2018.
2. [1](./Byzantine_fault#cite_ref-DriscollHall2004_2-0) [2](./Byzantine_fault#cite_ref-DriscollHall2004_2-1) [3](./Byzantine_fault#cite_ref-DriscollHall2004_2-2) [4](./Byzantine_fault#cite_ref-DriscollHall2004_2-3) Driscoll, K.; Hall, B.; Paulitsch, M.; Zumsteg, P.; Sivencrona, H. (2004). "The Real Byzantine Generals". *The 23rd Digital Avionics Systems Conference (IEEE Cat. No. 04CH37576)*. pp. 6.D.4–61–11. [doi](./Doi_(identifier)):[10.1109/DASC.2004.1390734](https://doi.org/10.1109%2FDASC.2004.1390734). [ISBN](./ISBN_(identifier)) [978-0-7803-8539-9](./Special:BookSources/978-0-7803-8539-9). [S2CID](./S2CID_(identifier)) [15549497](https://api.semanticscholar.org/CorpusID:15549497).
3. [1](./Byzantine_fault#cite_ref-DriscollHall2003_3-0) [2](./Byzantine_fault#cite_ref-DriscollHall2003_3-1) [3](./Byzantine_fault#cite_ref-DriscollHall2003_3-2) Driscoll, Kevin; Hall, Brendan; Sivencrona, Håkan; Zumsteg, Phil (2003). "Byzantine Fault Tolerance, from Theory to Reality". *Computer Safety, Reliability, and Security*. Lecture Notes in Computer Science. Vol. 2788. pp. 235–248. [doi](./Doi_(identifier)):[10.1007/978-3-540-39878-3_19](https://doi.org/10.1007%2F978-3-540-39878-3_19). [ISBN](./ISBN_(identifier)) [978-3-540-20126-7](./Special:BookSources/978-3-540-20126-7). [ISSN](./ISSN_(identifier)) [0302-9743](https://search.worldcat.org/issn/0302-9743). [S2CID](./S2CID_(identifier)) [12690337](https://api.semanticscholar.org/CorpusID:12690337).
4. [1](./Byzantine_fault#cite_ref-BGP_Paper_4-0) [2](./Byzantine_fault#cite_ref-BGP_Paper_4-1) [3](./Byzantine_fault#cite_ref-BGP_Paper_4-2) [Lamport, L.](./Leslie_Lamport); Shostak, R.; Pease, M. (1982). ["The Byzantine Generals Problem"](https://web.archive.org/web/20170207104645/http://research.microsoft.com/en-us/um/people/lamport/pubs/byz.pdf) (PDF). *ACM Transactions on Programming Languages and Systems*. **4** (3): 387–389. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.64.2312](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.64.2312). [doi](./Doi_(identifier)):[10.1145/357172.357176](https://doi.org/10.1145%2F357172.357176). [S2CID](./S2CID_(identifier)) [55899582](https://api.semanticscholar.org/CorpusID:55899582). Archived from [the original](http://research.microsoft.com/en-us/um/people/lamport/pubs/byz.pdf) (PDF) on 7 February 2017.
5. [1](./Byzantine_fault#cite_ref-:0_5-0) [2](./Byzantine_fault#cite_ref-:0_5-1) "SIFT: design and analysis of a fault-tolerant computer for aircraft control". *Microelectronics Reliability*. **19** (3): 190. 1979. [doi](./Doi_(identifier)):[10.1016/0026-2714(79)90211-7](https://doi.org/10.1016%2F0026-2714%2879%2990211-7). [ISSN](./ISSN_(identifier)) [0026-2714](https://search.worldcat.org/issn/0026-2714).
6. [↑](./Byzantine_fault#cite_ref-6) Pease, Marshall; Shostak, Robert; Lamport, Leslie (April 1980). "Reaching Agreement in the Presence of Faults". *Journal of the Association for Computing Machinery*. **27** (2): 228–234. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.68.4044](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.68.4044). [doi](./Doi_(identifier)):[10.1145/322186.322188](https://doi.org/10.1145%2F322186.322188). [S2CID](./S2CID_(identifier)) [6429068](https://api.semanticscholar.org/CorpusID:6429068).
7. [↑](./Byzantine_fault#cite_ref-7) Lamport, Leslie (2016-12-19). ["The Byzantine Generals Problem"](https://www.microsoft.com/en-us/research/publication/byzantine-generals-problem/). *ACM Transactions on Programming Languages and Systems*. SRI International. Retrieved 18 March 2019.
8. [↑](./Byzantine_fault#cite_ref-AvizienisLaprie2004_8-0) Avizienis, A.; Laprie, J.-C.; [Randell, Brian](./Brian_Randell); Landwehr, C. (2004). "Basic concepts and taxonomy of dependable and secure computing". *IEEE Transactions on Dependable and Secure Computing*. **1** (1): 11–33. [Bibcode](./Bibcode_(identifier)):[2004ITDSC...1...11A](https://ui.adsabs.harvard.edu/abs/2004ITDSC...1...11A). [doi](./Doi_(identifier)):[10.1109/TDSC.2004.2](https://doi.org/10.1109%2FTDSC.2004.2). [hdl](./Hdl_(identifier)):[1903/6459](https://hdl.handle.net/1903%2F6459). [ISSN](./ISSN_(identifier)) [1545-5971](https://search.worldcat.org/issn/1545-5971). [S2CID](./S2CID_(identifier)) [215753451](https://api.semanticscholar.org/CorpusID:215753451).
9. [↑](./Byzantine_fault#cite_ref-9) ["Dependable Computing and Fault Tolerance"](http://www.dependability.org). IEEE Computer Society. [Archived](https://web.archive.org/web/20150402141319/http://www.dependability.org/) from the original on 2015-04-02. Retrieved 2015-03-02.
10. [↑](./Byzantine_fault#cite_ref-10) Feldman, P.; Micali, S. (1997). ["An optimal probabilistic protocol for synchronous Byzantine agreement"](http://people.csail.mit.edu/silvio/Selected%20Scientific%20Papers/Distributed%20Computation/An%20Optimal%20Probabilistic%20Algorithm%20for%20Byzantine%20Agreement.pdf) (PDF). *SIAM Journal on Computing*. **26** (4): 873–933. [doi](./Doi_(identifier)):[10.1137/s0097539790187084](https://doi.org/10.1137%2Fs0097539790187084). [Archived](https://web.archive.org/web/20160305012505/http://people.csail.mit.edu/silvio/Selected%20Scientific%20Papers/Distributed%20Computation/An%20Optimal%20Probabilistic%20Algorithm%20for%20Byzantine%20Agreement.pdf) (PDF) from the original on 2016-03-05. Retrieved 2012-06-14.
11. [↑](./Byzantine_fault#cite_ref-11) Koopman, Philip; Driscoll, Kevin; Hall, Brendan (March 2015). "Cyclic Redundancy Code and Checksum Algorithms to Ensure Critical Data Integrity" (PDF). Federal Aviation Administration. DOT/FAA/TC-14/49.
12. [↑](./Byzantine_fault#cite_ref-PaulitschMorris2005_12-0) Paulitsch, M.; Morris, J.; Hall, B.; Driscoll, K.; Latronico, E.; Koopman, P. (2005). "Coverage and the Use of Cyclic Redundancy Codes in Ultra-Dependable Systems". [*2005 International Conference on Dependable Systems and Networks (DSN'05)*](https://figshare.com/articles/journal_contribution/6621788). pp. 346–355. [doi](./Doi_(identifier)):[10.1109/DSN.2005.31](https://doi.org/10.1109%2FDSN.2005.31). [ISBN](./ISBN_(identifier)) [978-0-7695-2282-1](./Special:BookSources/978-0-7695-2282-1). [S2CID](./S2CID_(identifier)) [14096385](https://api.semanticscholar.org/CorpusID:14096385).
13. [↑](./Byzantine_fault#cite_ref-HopkinsLala1987_13-0) Hopkins, Albert L.; Lala, Jaynarayan H.; Smith, T. Basil (1987). "The Evolution of Fault Tolerant Computing at the Charles Stark Draper Laboratory, 1955–85". *The Evolution of Fault-Tolerant Computing*. Dependable Computing and Fault-Tolerant Systems. Vol. 1. pp. 121–140. [doi](./Doi_(identifier)):[10.1007/978-3-7091-8871-2_6](https://doi.org/10.1007%2F978-3-7091-8871-2_6). [ISBN](./ISBN_(identifier)) [978-3-7091-8873-6](./Special:BookSources/978-3-7091-8873-6). [ISSN](./ISSN_(identifier)) [0932-5581](https://search.worldcat.org/issn/0932-5581).
14. [↑](./Byzantine_fault#cite_ref-MMFCS_14-0) Driscoll, Kevin; Papadopoulos, Gregory; Nelson, Scott; Hartmann, Gary; Ramohalli, Gautham (1984), *Multi-Microprocessor Flight Control System* (Technical Report), Wright-Patterson Air Force Base, Ohio: AFWAL/FIGL U.S. Air Force Systems Command, AFWAL-TR-84-3076
15. [↑](./Byzantine_fault#cite_ref-15) Castro, M.; Liskov, B. (2002). "Practical Byzantine Fault Tolerance and Proactive Recovery". *ACM Transactions on Computer Systems*. **20** (4). [Association for Computing Machinery](./Association_for_Computing_Machinery): 398–461. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.127.6130](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.127.6130). [doi](./Doi_(identifier)):[10.1145/571637.571640](https://doi.org/10.1145%2F571637.571640). [S2CID](./S2CID_(identifier)) [18793794](https://api.semanticscholar.org/CorpusID:18793794).
16. [↑](./Byzantine_fault#cite_ref-16) Abd-El-Malek, M.; Ganger, G.; Goodson, G.; Reiter, M.; Wylie, J. (2005). "Fault-scalable Byzantine Fault-Tolerant Services". *ACM SIGOPS Operating Systems Review*. **39** (5). [Association for Computing Machinery](./Association_for_Computing_Machinery): 59. [doi](./Doi_(identifier)):[10.1145/1095809.1095817](https://doi.org/10.1145%2F1095809.1095817).
17. [↑](./Byzantine_fault#cite_ref-17) Cowling, James; Myers, Daniel; [Liskov, Barbara](./Barbara_Liskov); Rodrigues, Rodrigo; Shrira, Liuba (2006). [*HQ Replication: A Hybrid Quorum Protocol for Byzantine Fault Tolerance*](http://portal.acm.org/citation.cfm?id=1298455.1298473). Proceedings of the 7th [USENIX](./USENIX) Symposium on Operating Systems Design and Implementation. pp. 177–190. [ISBN](./ISBN_(identifier)) [1-931971-47-1](./Special:BookSources/1-931971-47-1).
18. [↑](./Byzantine_fault#cite_ref-18) Kotla, Ramakrishna; Alvisi, Lorenzo; Dahlin, Mike; Clement, Allen; Wong, Edmund (December 2009). "Zyzzyva: Speculative Byzantine Fault Tolerance". *ACM Transactions on Computer Systems*. **27** (4). [Association for Computing Machinery](./Association_for_Computing_Machinery): 1–39. [doi](./Doi_(identifier)):[10.1145/1658357.1658358](https://doi.org/10.1145%2F1658357.1658358).
19. [↑](./Byzantine_fault#cite_ref-19) Guerraoui, Rachid; Kneževic, Nikola; Vukolic, Marko; Quéma, Vivien (2010). [*The Next 700 BFT Protocols*](http://infoscience.epfl.ch/record/144158). Proceedings of the 5th European conference on Computer systems. EuroSys. [Archived](https://web.archive.org/web/20111002225957/http://infoscience.epfl.ch/record/144158) from the original on 2011-10-02. Retrieved 2011-10-04.
20. [↑](./Byzantine_fault#cite_ref-20) Clement, A.; Wong, E.; Alvisi, L.; Dahlin, M.; Marchetti, M. (April 22–24, 2009). [*Making Byzantine Fault Tolerant Systems Tolerate Byzantine Faults*](http://www.usenix.org/events/nsdi09/tech/full_papers/clement/clement.pdf) (PDF). Symposium on Networked Systems Design and Implementation. [USENIX](./USENIX). [Archived](https://web.archive.org/web/20101225155052/https://www.usenix.org/events/nsdi09/tech/full_papers/clement/clement.pdf) (PDF) from the original on 2010-12-25. Retrieved 2010-02-17.
21. [↑](./Byzantine_fault#cite_ref-21) Aublin, P.-L.; Ben Mokhtar, S.; Quéma, V. (July 8–11, 2013). [*RBFT: Redundant Byzantine Fault Tolerance*](https://web.archive.org/web/20130805115252/http://www.temple.edu/cis/icdcs2013/program.html). 33rd IEEE International Conference on Distributed Computing Systems. [International Conference on Distributed Computing Systems](./International_Conference_on_Distributed_Computing_Systems). Archived from [the original](http://www.temple.edu/cis/icdcs2013/program.html) on August 5, 2013.
22. [↑](./Byzantine_fault#cite_ref-22) Bahsoun, J. P.; Guerraoui, R.; Shoker, A. (2015-05-01). ["Making BFT Protocols Really Adaptive"](http://repositorio.inesctec.pt/handle/123456789/4107). [*2015 IEEE International Parallel and Distributed Processing Symposium*](https://infoscience.epfl.ch/handle/20.500.14299/120735). pp. 904–913. [doi](./Doi_(identifier)):[10.1109/IPDPS.2015.21](https://doi.org/10.1109%2FIPDPS.2015.21). [ISBN](./ISBN_(identifier)) [978-1-4799-8649-1](./Special:BookSources/978-1-4799-8649-1). [S2CID](./S2CID_(identifier)) [16310807](https://api.semanticscholar.org/CorpusID:16310807).
23. [↑](./Byzantine_fault#cite_ref-23) Chun, Byung-Gon; Maniatis, Petros; Shenker, Scott; Kubiatowicz, John (2007-01-01). "Attested append-only memory". *Proceedings of twenty-first ACM SIGOPS symposium on Operating systems principles*. SOSP '07. New York City: ACM. pp. 189–204. [doi](./Doi_(identifier)):[10.1145/1294261.1294280](https://doi.org/10.1145%2F1294261.1294280). [ISBN](./ISBN_(identifier)) [9781595935915](./Special:BookSources/9781595935915). [S2CID](./S2CID_(identifier)) [6685352](https://api.semanticscholar.org/CorpusID:6685352).
24. [↑](./Byzantine_fault#cite_ref-24) Veronese, G. S.; Correia, M.; Bessani, A. N.; Lung, L. C.; Verissimo, P. (2013-01-01). "Efficient Byzantine Fault-Tolerance". *IEEE Transactions on Computers*. **62** (1): 16–30. [Bibcode](./Bibcode_(identifier)):[2013ITCmp..62...16V](https://ui.adsabs.harvard.edu/abs/2013ITCmp..62...16V). [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.408.9972](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.408.9972). [doi](./Doi_(identifier)):[10.1109/TC.2011.221](https://doi.org/10.1109%2FTC.2011.221). [ISSN](./ISSN_(identifier)) [0018-9340](https://search.worldcat.org/issn/0018-9340). [S2CID](./S2CID_(identifier)) [8157723](https://api.semanticscholar.org/CorpusID:8157723).
25. [↑](./Byzantine_fault#cite_ref-VLDB2021_25-0) Hellings, Jelle; Sadoghi, Mohammad (2021). ["ByShard: sharding in a byzantine environment"](http://www.vldb.org/pvldb/vol14/p2230-hellings.pdf) (PDF). *Proceedings of the VLDB Endowment*. **14** (11): 2230–2243. [doi](./Doi_(identifier)):[10.14778/3476249.3476275](https://doi.org/10.14778%2F3476249.3476275).
26. [↑](./Byzantine_fault#cite_ref-26) Driscoll, Kevin (2012-12-11). ["Real System Failures"](https://c3.nasa.gov/dashlink/resources/624/). *DASHlink*. [NASA](./NASA). [Archived](https://web.archive.org/web/20150402190610/https://c3.nasa.gov/dashlink/resources/624/) from the original on 2015-04-02. Retrieved 2015-03-02.
27. [↑](./Byzantine_fault#cite_ref-NanyaGoosen1989_27-0) Nanya, T.; Goosen, H. A. (1989). "The Byzantine hardware fault model". *IEEE Transactions on Computer-Aided Design of Integrated Circuits and Systems*. **8** (11): 1226–1231. [Bibcode](./Bibcode_(identifier)):[1989ITCAD...8.1226N](https://ui.adsabs.harvard.edu/abs/1989ITCAD...8.1226N). [doi](./Doi_(identifier)):[10.1109/43.41508](https://doi.org/10.1109%2F43.41508). [ISSN](./ISSN_(identifier)) [0278-0070](https://search.worldcat.org/issn/0278-0070).
28. [↑](./Byzantine_fault#cite_ref-MartinsGandhi2013_28-0) Martins, Rolando; Gandhi, Rajeev; Narasimhan, Priya; Pertet, Soila; Casimiro, António; Kreutz, Diego; Veríssimo, Paulo (2013). ["Experiences with Fault-Injection in a Byzantine Fault-Tolerant Protocol"](https://inria.hal.science/hal-01480791). *Middleware 2013*. Lecture Notes in Computer Science. Vol. 8275. pp. 41–61. [doi](./Doi_(identifier)):[10.1007/978-3-642-45065-5_3](https://doi.org/10.1007%2F978-3-642-45065-5_3). [ISBN](./ISBN_(identifier)) [978-3-642-45064-8](./Special:BookSources/978-3-642-45064-8). [ISSN](./ISSN_(identifier)) [0302-9743](https://search.worldcat.org/issn/0302-9743). [S2CID](./S2CID_(identifier)) [31337539](https://api.semanticscholar.org/CorpusID:31337539).
29. [↑](./Byzantine_fault#cite_ref-29) [US patent 7475318](https://worldwide.espacenet.com/textdoc?DB=EPODOC&IDX=US7475318), Kevin R. Driscoll, "Method for testing the sensitive input range of Byzantine filters", issued 2009-01-06,  assigned to Honeywell International Inc. 
30. [↑](./Byzantine_fault#cite_ref-WalterEllis2005_30-0) Walter, C.; Ellis, P.; LaValley, B. (2005). "The Reliable Platform Service: A Property-Based Fault Tolerant Service Architecture". *Ninth IEEE International Symposium on High-Assurance Systems Engineering (HASE'05)*. pp. 34–43. [doi](./Doi_(identifier)):[10.1109/HASE.2005.23](https://doi.org/10.1109%2FHASE.2005.23). [ISBN](./ISBN_(identifier)) [978-0-7695-2377-4](./Special:BookSources/978-0-7695-2377-4). [S2CID](./S2CID_(identifier)) [21468069](https://api.semanticscholar.org/CorpusID:21468069).
31. [↑](./Byzantine_fault#cite_ref-31) Rubby, Matt (20 January 2024). ["How Byzantine Generals Problem Relates to You in 2024"](https://www.swanbitcoin.com/byzantine-generals-problem/). *Swan Bitcoin*. Retrieved 2024-01-27.
32. [↑](./Byzantine_fault#cite_ref-32) Tholoniat, Pierre; Gramoli, Vincent (2022), Tran, Duc A.; Thai, My T.; Krishnamachari, Bhaskar (eds.), ["Formal Verification of Blockchain Byzantine Fault Tolerance"](https://doi.org/10.1007/978-3-031-07535-3_12), *Handbook on Blockchain*, Springer Optimization and Its Applications, Cham: Springer, pp. 389–412, [arXiv](./ArXiv_(identifier)):[1909.07453](https://arxiv.org/abs/1909.07453), [doi](./Doi_(identifier)):[10.1007/978-3-031-07535-3_12](https://doi.org/10.1007%2F978-3-031-07535-3_12), [ISBN](./ISBN_(identifier)) [978-3-031-07535-3](./Special:BookSources/978-3-031-07535-3), retrieved 2024-01-27`{{citation}}`:  CS1 maint: work parameter with ISBN ([link](./Category:CS1_maint:_work_parameter_with_ISBN))
33. [↑](./Byzantine_fault#cite_ref-FOOTNOTEDeirmentzoglouPapakyriakopoulosPatsakis201928716_33-0) [Deirmentzoglou, Papakyriakopoulos & Patsakis 2019](./Byzantine_fault#CITEREFDeirmentzoglouPapakyriakopoulosPatsakis2019), p. 28716.
34. [↑](./Byzantine_fault#cite_ref-34) ["Node Operations"](https://docs.klever.org/node-operations).
35. [↑](./Byzantine_fault#cite_ref-35) deVadoss, John (2025). "A Byzantine Fault Tolerance Approach towards AI Safety". [arXiv](./ArXiv_(identifier)):[2504.14668](https://arxiv.org/abs/2504.14668) [[cs.DC](https://arxiv.org/archive/cs.DC)].
36. [↑](./Byzantine_fault#cite_ref-Zurawski2015_36-0) M., Paulitsch; Driscoll, K. (9 January 2015). ["Chapter 48:SAFEbus"](https://books.google.com/books?id=ppzNBQAAQBAJ). In Zurawski, Richard (ed.). *Industrial Communication Technology Handbook* (2nd ed.). CRC Press. pp. 48–1–48–26. [ISBN](./ISBN_(identifier)) [978-1-4822-0733-0](./Special:BookSources/978-1-4822-0733-0).
37. [↑](./Byzantine_fault#cite_ref-HenzingerKirsch2001_37-0) Rushby, John (26 September 2001). Henzinger, Thomas A.; Kirsch, Christoph M. (eds.). [*Bus Architectures For Safety-Critical Embedded Systems*](http://www.csl.sri.com/papers/emsoft01/emsoft01.pdf) (PDF). Embedded Software: First International Workshop, October 8–10, 2001. Tahoe City, California: Springer Science & Business Media. pp. 307–. [ISBN](./ISBN_(identifier)) [978-3-540-42673-8](./Special:BookSources/978-3-540-42673-8). [Archived](https://web.archive.org/web/20150922114036/http://www.csl.sri.com/papers/emsoft01/emsoft01.pdf) (PDF) from the original on 2015-09-22. Retrieved 2015-03-05.
38. [↑](./Byzantine_fault#cite_ref-Yeh2001_38-0) Yeh, Y. C. (2001). *Safety critical avionics for the 777 primary flight controls system*. 20th DASC. 20th Digital Avionics Systems Conference (Cat. No. 01CH37219). Vol. 1. pp. 1C2/1–1C2/11. [doi](./Doi_(identifier)):[10.1109/DASC.2001.963311](https://doi.org/10.1109%2FDASC.2001.963311). [ISBN](./ISBN_(identifier)) [978-0-7803-7034-0](./Special:BookSources/978-0-7803-7034-0). [S2CID](./S2CID_(identifier)) [61489128](https://api.semanticscholar.org/CorpusID:61489128).
39. [↑](./Byzantine_fault#cite_ref-39) ["ELC: SpaceX lessons learned"](https://lwn.net/Articles/540368/). *LWN*. [Archived](https://web.archive.org/web/20160805064218/http://lwn.net/Articles/540368/) from the original on 2016-08-05. Retrieved 2016-07-21.
40. [↑](./Byzantine_fault#cite_ref-40) ["SLS (Space Launch System) Avionics: The "Brains" of SLS"](https://www.nasa.gov/wp-content/uploads/2024/12/sls-4964-sls-avionics-fact-sheet-dec2024-508.pdf?emrc=442235) (PDF). *nasa.gov*. MSFS-12-2024-SLS-4964.
41. [↑](./Byzantine_fault#cite_ref-41) Loveless, Andrew (7 November 2016). ["Notional 1FT Voting Architecture with Time-Triggered Ethernet"](https://ntrs.nasa.gov/api/citations/20170001652/downloads/20170001652.pdf) (PDF). *nasa.gov*.
42. [↑](./Byzantine_fault#cite_ref-42) Baggerman, Clint (2 August 2013). ["Avionics System Architecture for NASA Orion Vehicle"](https://ntrs.nasa.gov/citations/20100040584). *ntrs.nasa.gov*.

 

## Sources

 
- Deirmentzoglou, Evangelos; Papakyriakopoulos, Georgios; Patsakis, Constantinos (2019). ["A Survey on Long-Range Attacks for Proof of Stake Protocols"](https://doi.org/10.1109%2FACCESS.2019.2901858). *IEEE Access*. **7**: 28712–28725. [Bibcode](./Bibcode_(identifier)):[2019IEEEA...728712D](https://ui.adsabs.harvard.edu/abs/2019IEEEA...728712D). [doi](./Doi_(identifier)):[10.1109/ACCESS.2019.2901858](https://doi.org/10.1109%2FACCESS.2019.2901858). [eISSN](./EISSN_(identifier)) [2169-3536](https://search.worldcat.org/issn/2169-3536). [S2CID](./S2CID_(identifier)) [84185792](https://api.semanticscholar.org/CorpusID:84185792).
- Bashir, Imran. "Blockchain Consensus." *Blockchain Consensus - An Introduction to Classical, Blockchain, and Quantum Consensus Protocols*. [ISBN](./ISBN_(identifier)) [978-1-4842-8178-9](./Special:BookSources/978-1-4842-8178-9) Apress, Berkeley, CA, 2022. [doi](./Doi_(identifier)):[10.1007/978-1-4842-8179-6](https://doi.org/10.1007%2F978-1-4842-8179-6)

 

## External links

 
- [Byzantine Fault Tolerance in the RKBExplorer](https://web.archive.org/web/20080828060019/http://www.rkbexplorer.com/explorer/#display=mechanism%2D{http://resex.rkbexplorer.com/id/resilience-mechanism-65b5cef4})