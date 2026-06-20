---
source: https://en.wikipedia.org/wiki/Leader_election
fetched: 2026-06-19
---

Concept in distributed computing Not to be confused with [Leadership election](./Leadership_election). 

In [distributed computing](./Distributed_computing), **leader election** is the process of designating a single [process](./Process_(computing)) as the organizer of some task distributed among several computers (nodes). Before the task has begun, all network nodes are either unaware which node will serve as the "leader" (or [coordinator](./Distributed_computing#Coordinator_election)) of the task, or unable to communicate with the current coordinator. After a leader election algorithm has been run, however, each node throughout the network recognizes a particular, unique node as the task leader.

 

The network nodes communicate among themselves in order to decide which of them will get into the "leader" state. For that, they need some method in order to break the symmetry among them. For example, if each node has unique and comparable identities, then the nodes can compare their identities, and decide that the node with the highest identity is the leader.

 

The definition of this problem is often attributed to LeLann, who formalized it as a method to create a new token in a token [ring network](./Ring_network) in which the token has been lost.

 

Leader election algorithms are designed to be economical in terms of total [bytes](./Byte) transmitted, and time. The algorithm suggested by Gallager, Humblet, and Spira[[1]](./Leader_election#cite_note-1) for general undirected graphs has had a strong impact on the design of distributed algorithms in general, and won the [Dijkstra Prize](./Dijkstra_Prize) for an influential paper in distributed computing.

 

Many other algorithms have been suggested for different kinds of network [graphs](./Graph_(discrete_mathematics)), such as undirected rings, unidirectional rings, complete graphs, grids, directed Euler graphs, and others. A general method that decouples the issue of the graph family from the design of the leader election algorithm was suggested by Korach, [Kutten](./Shay_Kutten), and [Moran](./Shlomo_Moran).[[2]](./Leader_election#cite_note-2)

 

## Definition

 

The problem of leader election is for each processor eventually to decide whether it is a leader or not, subject to the constraint that exactly one processor decides that it is the leader.[[3]](./Leader_election#cite_note-AttiyaWelch3-3) An algorithm solves the leader election problem if:

 
1. States of processors are divided into elected and not-elected states. Once elected, each processor remains as elected (similarly if not elected).
2. In every execution, exactly one processor becomes elected and the rest determine that they are not elected.

 

A valid leader election algorithm must meet the following conditions:[[4]](./Leader_election#cite_note-4)

 
1. **Termination**: the algorithm should finish within a finite time once the leader is selected. In randomized approaches this condition is sometimes weakened (for example, requiring termination with probability 1).
2. **Uniqueness**: there is exactly one processor that considers itself as leader.
3. **Agreement**: all other processors know who the leader is.

 

An algorithm for leader election may vary in the following aspects:[[5]](./Leader_election#cite_note-5)

 
- Communication mechanism: the processors are either [synchronous](./Synchronization_(computer_science)) in which processes are synchronized by a [clock signal](./Clock_signal) or [asynchronous](./Asynchronous_system) where processes run at arbitrary speeds.
- Process names: whether processes have a unique identity or are indistinguishable (anonymous).
- Network topology: for instance, [ring](./Ring_network), [acyclic graph](./Directed_acyclic_graph) or [complete graph](./Complete_graph).
- Size of the network: the algorithm may or may not use knowledge of the number of processes in the system.

 

## Algorithms

 

### Leader election in rings

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/f/f8/Ring_graph.png/250px-Ring_graph.png)](./File:Ring_graph.png)Ring network topology 

A ring network is a connected-graph topology in which each node is exactly connected to two other nodes, i.e., for a graph with n nodes, there are exactly n edges connecting the nodes. A ring can be unidirectional, which means processors only communicate in one direction (a node could only send messages to the left or only send messages to the right), or bidirectional, meaning processors may transmit and receive messages in both directions (a node could send messages to the left and right).

 

#### Anonymous rings

 

A ring is said to be anonymous if every processor is identical. More formally, the system has the same state machine for every processor.[[3]](./Leader_election#cite_note-AttiyaWelch3-3) There is no [deterministic algorithm](./Deterministic_algorithm) to elect a leader in anonymous rings, even when the size of the network is known to the processes.[[3]](./Leader_election#cite_note-AttiyaWelch3-3)[[6]](./Leader_election#cite_note-6)  This is due to the fact that there is no possibility of breaking symmetry in an anonymous ring if all processes run at the same speed. The state of processors after some steps only depends on the initial state of neighbouring nodes. So, because their states are identical and execute the same procedures, in every round the same messages are sent by each processor. Therefore, each processor state also changes identically and as a result if one processor is elected as a leader, so are all the others.

 

For simplicity, here is a proof in anonymous synchronous rings. It is a proof by contradiction. Consider an anonymous ring R with size n>1. Assume there exists an algorithm "A" to solve leader election in this anonymous ring R.[[3]](./Leader_election#cite_note-AttiyaWelch3-3)

 ***Lemma**: after round     k   {\displaystyle k}  ![{\displaystyle k}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3c9a2c7b599b37105512c5d570edc034056dd40) of the admissible execution of A in R, all the processes have the same states.* 

**Proof.** Proof by induction on     k   {\displaystyle k}  ![{\displaystyle k}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3c9a2c7b599b37105512c5d570edc034056dd40).

 

**Base case:**     k = 0   {\displaystyle k=0}  ![{\displaystyle k=0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6307c8a99dad7d0bcb712352ae0a748bd99a038b): all the processes are in the initial state, so all the processes are identical.

 

**Induction hypothesis:** assume the lemma is true for     k − −  1   {\displaystyle k-1}  ![{\displaystyle k-1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/21363ebd7038c93aae93127e7d910fc1b2e2c745) rounds.

 

**Inductive step:** in round     k   {\displaystyle k}  ![{\displaystyle k}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3c9a2c7b599b37105512c5d570edc034056dd40), every process send the same message      m  r     {\displaystyle m_{r}}  ![{\displaystyle m_{r}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/55cb6f47d826e98ab3f09fba26148d2f7ad17be9) to the right and send the same message      m  l     {\displaystyle m_{l}}  ![{\displaystyle m_{l}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a3f945c408d692391284a629617fe0b301776222) to the left. Since all the processes are in the same state after round     k − −  1   {\displaystyle k-1}  ![{\displaystyle k-1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/21363ebd7038c93aae93127e7d910fc1b2e2c745), in round k, every process will receive the message      m  r     {\displaystyle m_{r}}  ![{\displaystyle m_{r}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/55cb6f47d826e98ab3f09fba26148d2f7ad17be9) from the left edge, and will receive the message      m  l     {\displaystyle m_{l}}  ![{\displaystyle m_{l}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a3f945c408d692391284a629617fe0b301776222) from the right edge. Since all processes are receiving the same messages in round     k   {\displaystyle k}  ![{\displaystyle k}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3c9a2c7b599b37105512c5d570edc034056dd40), they are in the same state after round     k   {\displaystyle k}  ![{\displaystyle k}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3c9a2c7b599b37105512c5d570edc034056dd40).

 

The above lemma contradicts the fact that after some finite number of rounds in an execution of A, one process entered the elected state and other processes entered the non-elected state.

 

#### Randomized (probabilistic) leader election

 

A common approach to solve the problem of leader election in anonymous rings is the use of [probabilistic algorithms](./Probabilistic_algorithm). In such approaches, generally processors assume some identities based on a probabilistic function and communicate it to the rest of the network. At the end, through the application of an algorithm, a leader is selected (with high probability).

 

##### Asynchronous ring

 

Source:[[3]](./Leader_election#cite_note-AttiyaWelch3-3)

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/9/9c/Nlogn.png/120px-Nlogn.png)](./File:Nlogn.png)O(nlogn) algorithm for asynchronous ring 

Since there is no algorithm for anonymous rings (proved above), the asynchronous rings would be considered as asynchronous non-anonymous rings. In non-anonymous rings, each process has a unique     i d   {\displaystyle id}  ![{\displaystyle id}](https://wikimedia.org/api/rest_v1/media/math/render/svg/514c0ded05af41857b8728628c0a664c1b9b1b37), and they don't know the size of the ring. Leader election in asynchronous rings can be solved by some algorithm with using     O (  n  2   )   {\displaystyle O(n^{2})}  ![{\displaystyle O(n^{2})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6cd9594a16cb898b8f2a2dff9227a385ec183392) messages or     O ( n log ⁡ ⁡  n )   {\displaystyle O(n\log n)}  ![{\displaystyle O(n\log n)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9d2320768fb54880ca4356e61f60eb02a3f9d9f1) messages.

 

In the     O (  n  2   )   {\displaystyle O(n^{2})}  ![{\displaystyle O(n^{2})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6cd9594a16cb898b8f2a2dff9227a385ec183392) algorithm, every process sends a message with its     i d   {\displaystyle id}  ![{\displaystyle id}](https://wikimedia.org/api/rest_v1/media/math/render/svg/514c0ded05af41857b8728628c0a664c1b9b1b37) to the left edge. Then waits until a message from the right edge. If the     i d   {\displaystyle id}  ![{\displaystyle id}](https://wikimedia.org/api/rest_v1/media/math/render/svg/514c0ded05af41857b8728628c0a664c1b9b1b37) in the message is greater than its own     i d   {\displaystyle id}  ![{\displaystyle id}](https://wikimedia.org/api/rest_v1/media/math/render/svg/514c0ded05af41857b8728628c0a664c1b9b1b37), then forwards the message to the left edge; else ignore the message, and does nothing. If the     i d   {\displaystyle id}  ![{\displaystyle id}](https://wikimedia.org/api/rest_v1/media/math/render/svg/514c0ded05af41857b8728628c0a664c1b9b1b37) in the message is equal to its own     i d   {\displaystyle id}  ![{\displaystyle id}](https://wikimedia.org/api/rest_v1/media/math/render/svg/514c0ded05af41857b8728628c0a664c1b9b1b37), then sends a message to the left announcing myself is elected. Other processes forward the announcement to the left and turn themselves to non-elected. It is clear that the upper bound is     O (  n  2   )   {\displaystyle O(n^{2})}  ![{\displaystyle O(n^{2})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6cd9594a16cb898b8f2a2dff9227a385ec183392) for this algorithm.

 

In the     O ( n log ⁡ ⁡  n )   {\displaystyle O(n\log n)}  ![{\displaystyle O(n\log n)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9d2320768fb54880ca4356e61f60eb02a3f9d9f1) algorithm, it is running in phases. On the     k   {\displaystyle k}  ![{\displaystyle k}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3c9a2c7b599b37105512c5d570edc034056dd40)th phase, a process will determine whether it is the winner among the left side      2  k     {\displaystyle 2^{k}}  ![{\displaystyle 2^{k}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2d82641ae2702b0db07dd11830af27b9ee0cd196) and right side      2  k     {\displaystyle 2^{k}}  ![{\displaystyle 2^{k}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2d82641ae2702b0db07dd11830af27b9ee0cd196) neighbors. If it is a winner, then the process can go to next phase. In phase     0   {\displaystyle 0}  ![{\displaystyle 0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2aae8864a3c1fec9585261791a809ddec1489950), each process     P   {\displaystyle P}  ![{\displaystyle P}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b4dc73bf40314945ff376bd363916a738548d40a) needs to determine itself is a winner or not by sending a message with its     i d   {\displaystyle id}  ![{\displaystyle id}](https://wikimedia.org/api/rest_v1/media/math/render/svg/514c0ded05af41857b8728628c0a664c1b9b1b37) to the left and right neighbors (neighbor do not forward the message). The neighbor replies an     A C K   {\displaystyle ACK}  ![{\displaystyle ACK}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fca3cc65b46eb35cb7efa0a951506d685caca49c) only if the     i d   {\displaystyle id}  ![{\displaystyle id}](https://wikimedia.org/api/rest_v1/media/math/render/svg/514c0ded05af41857b8728628c0a664c1b9b1b37) in the message is larger than the neighbor's     i d   {\displaystyle id}  ![{\displaystyle id}](https://wikimedia.org/api/rest_v1/media/math/render/svg/514c0ded05af41857b8728628c0a664c1b9b1b37), else replies an     A C  K  f a u l t     {\displaystyle ACK_{fault}}  ![{\displaystyle ACK_{fault}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/45d83ba57dd226965453ed904979e1d8325ad7b1). If     P   {\displaystyle P}  ![{\displaystyle P}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b4dc73bf40314945ff376bd363916a738548d40a) receives two     A C K   {\displaystyle ACK}  ![{\displaystyle ACK}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fca3cc65b46eb35cb7efa0a951506d685caca49c)s, one from the left, one from the right, then     P   {\displaystyle P}  ![{\displaystyle P}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b4dc73bf40314945ff376bd363916a738548d40a) is the winner in phase     0   {\displaystyle 0}  ![{\displaystyle 0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2aae8864a3c1fec9585261791a809ddec1489950). In phase     k   {\displaystyle k}  ![{\displaystyle k}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3c9a2c7b599b37105512c5d570edc034056dd40), the winners in phase     k − −  1   {\displaystyle k-1}  ![{\displaystyle k-1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/21363ebd7038c93aae93127e7d910fc1b2e2c745) need to send a message with its     i d   {\displaystyle id}  ![{\displaystyle id}](https://wikimedia.org/api/rest_v1/media/math/render/svg/514c0ded05af41857b8728628c0a664c1b9b1b37) to the      2  k     {\displaystyle 2^{k}}  ![{\displaystyle 2^{k}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2d82641ae2702b0db07dd11830af27b9ee0cd196) left and      2  k     {\displaystyle 2^{k}}  ![{\displaystyle 2^{k}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2d82641ae2702b0db07dd11830af27b9ee0cd196) right neighbors. If the neighbors in the path receive the     i d   {\displaystyle id}  ![{\displaystyle id}](https://wikimedia.org/api/rest_v1/media/math/render/svg/514c0ded05af41857b8728628c0a664c1b9b1b37) in the message larger than their     i d   {\displaystyle id}  ![{\displaystyle id}](https://wikimedia.org/api/rest_v1/media/math/render/svg/514c0ded05af41857b8728628c0a664c1b9b1b37), then forward the message to the next neighbor, otherwise reply an     A C  K  f a u l t     {\displaystyle ACK_{fault}}  ![{\displaystyle ACK_{fault}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/45d83ba57dd226965453ed904979e1d8325ad7b1). If the      2  k     {\displaystyle 2^{k}}  ![{\displaystyle 2^{k}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2d82641ae2702b0db07dd11830af27b9ee0cd196)th neighbor receives the     i d   {\displaystyle id}  ![{\displaystyle id}](https://wikimedia.org/api/rest_v1/media/math/render/svg/514c0ded05af41857b8728628c0a664c1b9b1b37) larger than its     i d   {\displaystyle id}  ![{\displaystyle id}](https://wikimedia.org/api/rest_v1/media/math/render/svg/514c0ded05af41857b8728628c0a664c1b9b1b37), then sends back an     A C K   {\displaystyle ACK}  ![{\displaystyle ACK}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fca3cc65b46eb35cb7efa0a951506d685caca49c), otherwise replies an     A C  K  f a u l t     {\displaystyle ACK_{fault}}  ![{\displaystyle ACK_{fault}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/45d83ba57dd226965453ed904979e1d8325ad7b1). If the process receives two     A C K   {\displaystyle ACK}  ![{\displaystyle ACK}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fca3cc65b46eb35cb7efa0a951506d685caca49c)s, then it is the winner in phase     k   {\displaystyle k}  ![{\displaystyle k}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3c9a2c7b599b37105512c5d570edc034056dd40). In the last phase, the final winner will receive its own     i d   {\displaystyle id}  ![{\displaystyle id}](https://wikimedia.org/api/rest_v1/media/math/render/svg/514c0ded05af41857b8728628c0a664c1b9b1b37) in the message, then terminates and send termination message to the other processes. In the worst case, each phase there are at most       n   2  k   + 1      {\displaystyle {\frac {n}{2^{k}+1}}}  ![{\displaystyle {\frac {n}{2^{k}+1}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0a00a7ba2b1777e024071c7031438523e333bd6e) winners, where     k   {\displaystyle k}  ![{\displaystyle k}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3c9a2c7b599b37105512c5d570edc034056dd40) is the phase number. There are     ⌈ ⌈  log ⁡ ⁡  ( n − −  1 ) ⌉ ⌉    {\displaystyle \lceil \log(n-1)\rceil }  ![{\displaystyle \lceil \log(n-1)\rceil }](https://wikimedia.org/api/rest_v1/media/math/render/svg/f9f65461db286bc781ed4e559a69496ff124d7ec) phases in total. Each winner sends in the order of      2  k     {\displaystyle 2^{k}}  ![{\displaystyle 2^{k}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2d82641ae2702b0db07dd11830af27b9ee0cd196) messages in each phase. So, the messages complexity is     O ( n log ⁡ ⁡  n )   {\displaystyle O(n\log n)}  ![{\displaystyle O(n\log n)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9d2320768fb54880ca4356e61f60eb02a3f9d9f1).

 

##### Synchronous ring

 

In Attiya and Welch's Distributed Computing book,[[3]](./Leader_election#cite_note-AttiyaWelch3-3) they described a non-uniform algorithm using     O ( n )   {\displaystyle O(n)}  ![{\displaystyle O(n)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/34109fe397fdcff370079185bfdb65826cb5565a) messages in synchronous ring with known ring size     n   {\displaystyle n}  ![{\displaystyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b). The algorithm is operating in phases, each phase has     n   {\displaystyle n}  ![{\displaystyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b) rounds, each round is one time unit. In phase     0   {\displaystyle 0}  ![{\displaystyle 0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2aae8864a3c1fec9585261791a809ddec1489950), if there is a process with     i d = 0   {\displaystyle id=0}  ![{\displaystyle id=0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c4707a144b2870cad01a907fd15e284c5932fcd2), then process     0   {\displaystyle 0}  ![{\displaystyle 0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2aae8864a3c1fec9585261791a809ddec1489950) sends termination message to the other processes (sending termination messages cost     n   {\displaystyle n}  ![{\displaystyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b) rounds). Else, go to the next phase. The algorithm will check if there is a phase number equals to a process     i d   {\displaystyle id}  ![{\displaystyle id}](https://wikimedia.org/api/rest_v1/media/math/render/svg/514c0ded05af41857b8728628c0a664c1b9b1b37), then does the same steps as phase     0   {\displaystyle 0}  ![{\displaystyle 0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2aae8864a3c1fec9585261791a809ddec1489950). At the end of the execution, the minimal     i d   {\displaystyle id}  ![{\displaystyle id}](https://wikimedia.org/api/rest_v1/media/math/render/svg/514c0ded05af41857b8728628c0a664c1b9b1b37) will be elected as the leader. It used exactly     n   {\displaystyle n}  ![{\displaystyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b) messages and     n ( m i n i m u m _ _  i d + 1 )   {\displaystyle n(minimum\_id+1)}  ![{\displaystyle n(minimum\_id+1)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9f960f386a7b1a6ac7b4f5acbf78fc0260fc0bdd) rounds.

 

Itai and Rodeh[[7]](./Leader_election#cite_note-7) introduced an algorithm for a unidirectional ring with synchronized processes. They assume the size of the ring (number of nodes) is known to the processes.  For a ring of size n, a≤n processors are active. Each processor decides with probability of a^(-1) whether to become a candidate. At the end of each phase, each processor calculates the number of candidates c and if it is equal to 1, it becomes the leader.
To determine the value of c, each candidate sends a token (pebble) at the start of the phase which is passed around the ring, returning after exactly n time units to its sender. Every processor determines c by counting the number of pebbles which passed through. This algorithm achieves leader election with expected message complexity of O(nlogn). A similar approach is also used in which a time-out mechanism is employed to detect deadlocks in the system.[[8]](./Leader_election#cite_note-8) There are also algorithms for rings of special sizes such as prime size[[9]](./Leader_election#cite_note-9)[[10]](./Leader_election#cite_note-10) and odd size.[[11]](./Leader_election#cite_note-11)

 

##### Uniform algorithm

 

In typical approaches to leader election, the size of the ring is assumed to be known to the processes. In the case of anonymous rings, without using an external entity, it is not possible to elect a leader. Even assuming an algorithm exists, the leader could not estimate the size of the ring. i.e. in any anonymous ring, there is a positive probability that an algorithm computes a wrong ring size.[[12]](./Leader_election#cite_note-12) To overcome this problem, Fisher and Jiang used a so-called leader oracle Ω?  that each processor can ask whether there is a unique leader. They show that from some point upward, it is guaranteed to return the same answer to all processes.[[13]](./Leader_election#cite_note-13)

 

#### Rings with unique IDs

 

In one of the early works, Chang and Roberts[[14]](./Leader_election#cite_note-14) proposed a uniform algorithm in which a processor with the highest ID is selected as the leader. Each processor sends its ID in a clockwise direction. A processor receives a message and compares the ID with its own. If the ID is bigger than the processor passes it through, otherwise it discards the message. The authors show that this algorithm uses     O (  n  2   )   {\displaystyle O(n^{2})}  ![{\displaystyle O(n^{2})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6cd9594a16cb898b8f2a2dff9227a385ec183392) messages in the worst case and     O ( n log ⁡ ⁡  n )   {\displaystyle O(n\log n)}  ![{\displaystyle O(n\log n)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9d2320768fb54880ca4356e61f60eb02a3f9d9f1) in the average case.
 [Hirschberg and Sinclair](./Hirschberg–Sinclair_algorithm)[[15]](./Leader_election#cite_note-15) improved this algorithm with     O ( n log ⁡ ⁡  n )   {\displaystyle O(n\log n)}  ![{\displaystyle O(n\log n)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9d2320768fb54880ca4356e61f60eb02a3f9d9f1) message complexity by introducing a bidirectional message-passing scheme.

 

### Leader election in a mesh

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/5/58/Mesh_graph.png/250px-Mesh_graph.png)](./File:Mesh_graph.png)Mesh network topology. Red nodes denote corners, blue border and gray interior. 

The [mesh](./Lattice_graph) is another popular form of network topology, especially in parallel systems, redundant memory systems and interconnection networks.[[16]](./Leader_election#cite_note-N._Santoro,_2006-16)
 
In a mesh structure, nodes are either corner (only two neighbours), border (only three neighbours) or interior (with four neighbours). The number of edges in a mesh of size  a x b is m=2ab-a-b.

 

#### Unoriented mesh

 

A typical algorithm to solve the leader election in an unoriented mesh is to only elect one of the four corner nodes as the leader. Since the corner nodes might not be aware of the state of other processes, the algorithm should first wake up the corner nodes. A leader can be elected as follows.[[17]](./Leader_election#cite_note-17)

 
1. *Wake-up process*: in which     k   {\displaystyle k}  ![{\displaystyle k}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3c9a2c7b599b37105512c5d570edc034056dd40) nodes initiate the election process. Each initiator sends a wake-up message to all its neighbouring nodes. If a node is not initiator, it simply forwards the messages to the other nodes. In this stage at most     3 n + k   {\displaystyle 3n+k}  ![{\displaystyle 3n+k}](https://wikimedia.org/api/rest_v1/media/math/render/svg/bbb84cfc93afbfa574c91401ef46f05e86a9abbb) messages are sent.
2. *Election process*: the election in outer ring takes two stages at most with     6 ( a + b ) − −  16   {\displaystyle 6(a+b)-16}  ![{\displaystyle 6(a+b)-16}](https://wikimedia.org/api/rest_v1/media/math/render/svg/42ed4a1fd01d7b7afc78b4ff0632df5409edd1ae) messages.
3. *Termination*: leader sends a terminating message to all nodes. This requires at most 2n messages.

 

The message complexity is at most     6 ( a + b ) − −  16   {\displaystyle 6(a+b)-16}  ![{\displaystyle 6(a+b)-16}](https://wikimedia.org/api/rest_v1/media/math/render/svg/42ed4a1fd01d7b7afc78b4ff0632df5409edd1ae), and if the mesh is square-shaped,     O (   n   )   {\displaystyle O({\sqrt {n}})}  ![{\displaystyle O({\sqrt {n}})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f5526ab1252c0f682bbe07c0ad67c0f29de5522b).

 

#### Oriented mesh

 

An oriented mesh is a special case where port numbers are compass labels, i.e. north, south, east and west. Leader election in an oriented mesh is trivial. We only need to nominate a corner, e.g. "north" and "east" and make sure that node knows it is a leader.

 

#### Torus

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/a/a7/Torus_graph.png/250px-Torus_graph.png)](./File:Torus_graph.png)Torus network structure. 

A special case of mesh architecture is a torus which is a mesh with "wrap-around". In this structure, every node has exactly 4 connecting edges.
One approach to elect a leader in such a structure is known as electoral stages. Similar to procedures in ring structures, this method in each stage eliminates potential candidates until eventually one candidate node is left. This node becomes the leader and then notifies all other processes of termination.[[16]](./Leader_election#cite_note-N._Santoro,_2006-16) This approach can be used to achieve a complexity of O(n). There also more practical approaches introduced for dealing with presence of faulty links in the network.[[18]](./Leader_election#cite_note-18)[[19]](./Leader_election#cite_note-19)

 

### Election in hypercubes

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/2/22/4x4_hypercube.png/250px-4x4_hypercube.png)](./File:4x4_hypercube.png)H_4 hypercube network topology. 

A [Hypercube](./Hypercube)      H  k     {\displaystyle H_{k}}  ![{\displaystyle H_{k}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4c8af69c8cae9ee6ba302b6b3f4b0618ac08e427) is a network consisting of     n =  2  k     {\displaystyle n=2^{k}}  ![{\displaystyle n=2^{k}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a8242689a132230c6c847ae901f6f32dba8181ab) nodes, each with degree of     k   {\displaystyle k}  ![{\displaystyle k}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3c9a2c7b599b37105512c5d570edc034056dd40) and     O ( n log ⁡ ⁡  n )   {\displaystyle O(n\log n)}  ![{\displaystyle O(n\log n)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9d2320768fb54880ca4356e61f60eb02a3f9d9f1) edges. 
A similar electoral stages as before can be used to solve the problem of leader election. In each stage two nodes (called duelists) compete and the winner is promoted to the next stage. This means in each stage only half of the duelists enter the next stage. This procedure continues until only one duelist is left, and it becomes the leader. Once selected, it notifies all other processes. This algorithm requires     O ( n )   {\displaystyle O(n)}  ![{\displaystyle O(n)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/34109fe397fdcff370079185bfdb65826cb5565a) messages. In the case of unoriented hypercubes, a similar approach can be used but with a higher message complexity of     O ( n log ⁡ ⁡  log ⁡ ⁡  n )   {\displaystyle O(n\log \log n)}  ![{\displaystyle O(n\log \log n)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8147032e355336e05cf34c58407bd2380afb6f22).[[16]](./Leader_election#cite_note-N._Santoro,_2006-16)

 

### Election in complete networks

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/1/1f/Full_graph.png/250px-Full_graph.png)](./File:Full_graph.png)Complete network structure. 

[Complete networks](./Network_topology) are structures in which all processes are connected to one another, i.e., the degree of each node is n-1, n being the size of the network. An optimal solution with O(n) message and [space complexity](./Space_complexity) is known.[[20]](./Leader_election#cite_note-orginalcompalgo-20) In this algorithm, processes have the following states:

 
1. Dummy: nodes that do not participate in the leader election algorithm.
2. Passive: the initial state of processes before start.
3. Candidate: the status of nodes after waking up. The candidate nodes will be considered to become the leader.

 

There is an assumption that although a node does not know the total set of nodes in the system, it is required that in this arrangement every node knows the identifier of its single successor, which is called neighbor,[[20]](./Leader_election#cite_note-orginalcompalgo-20) and every node is known by another one.[[21]](./Leader_election#cite_note-modifiedcompalgo-21)

 

All processors initially start in a passive state until they are woken up.  Once the nodes are awake, they are candidates to become the leader. Based on a priority scheme, candidate nodes collaborate in the virtual ring. At some point, candidates become aware of the identity of candidates that precede them in the ring. The higher priority candidates ask the lower ones about their predecessors. The candidates with lower priority become dummies after replying to the candidates with higher priority. Based on this scheme, the highest priority candidate eventually knows that all nodes in the system are dummies except itself, at which point it knows it is the leader.

 

The above algorithm is not correct — it needs further improvement.[[21]](./Leader_election#cite_note-modifiedcompalgo-21)

 

### Universal leader election techniques

 

As the name implies, these algorithms are designed to be used in any process network without prior knowledge of the network's topology or properties (such as size).[[16]](./Leader_election#cite_note-N._Santoro,_2006-16)

 

#### Shout

 

The Shout protocol builds a spanning tree on a generic graph and elects its root as leader. The algorithm has a total cost linear in the edges cardinality.

 

#### [Mega-Merger](./Mega-Merger)

 

This technique is similar to finding a [Minimum Spanning Tree](./Minimum_spanning_tree) (MST) in which the root of the tree becomes the leader. The idea is that individual nodes "merge" with each other to form bigger structures. The result of this algorithm is a tree (a graph with no cycles) whose root is the leader of the entire system. The cost of the mega-merger method is     O ( m + n log ⁡ ⁡  n )   {\displaystyle O(m+n\log n)}  ![{\displaystyle O(m+n\log n)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/48dc2f8baf452be00faa98b33c37c4c0fb843849), where m is the number of edges and n is the number of nodes.

 

#### Yo-yo

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/f/f6/YOYO.png/250px-YOYO.png)](./File:YOYO.png)An example of YO-YO procedure. a) The network, b) Oriented network after *setup* phase, c) YO- phase in which source values are passed, d)-YO phase sending responses from sinks, e) updated structure after -YO phase. 

[Yo-yo (algorithm)](./Yo-yo_(algorithm)) is a minimum finding algorithm consisting of two parts: a preprocessing phase and a series of iterations.[[16]](./Leader_election#cite_note-N._Santoro,_2006-16) In the first phase or *setup*, each node exchanges its id with all its neighbours and based on the value it orients its incident edges. For instance, if node x has a smaller id than y, x orients towards y. If a node has a smaller id than all its neighbours it becomes a **source**. In contrast, a node with all inward edges (i.e., with id larger than all of its neighbours) is a **sink**. All other nodes are **internal** nodes.
   
Once all the edges are oriented, the *iteration* phase starts. Each iteration is an electoral stage in which some candidates will be removed. Each iteration has two phases: *YO-* and *–YO*. In this phase sources start the process to propagate to each sink the smallest values of the sources connected to that sink.

 

***Yo-***

 
1. A source (local minima) transmits its value to all its out-neighbours
2. An internal node waits to receive a value from all its in-neighbours. It calculates the minimum and sends it to out-neighbour.
3. A sink (a node with no outgoing edge) receives all the values and compute their minimum.

 

***-yo***

 
1. A sink sends YES to neighbours from which saw the smallest value and NO to others
2. An internal node sends YES to all in-neighbours from which it received the smallest value and NO to others. If it receives only one NO, it sends NO to all.
3. A source waits until it receives all votes. If all YES, it survives and if not, it is no longer a candidate.
4. When a node x sends NO to an in-neighbour y, the logical direction of that edge is reversed.
5. When a node y receives NO from an out-neighbour, it flips the direction of that link.

 

After the final stage, any source who receives a NO is no longer a source and becomes a sink.
An additional stage, *pruning*, also is introduced to remove the nodes that are useless, i.e. their existence has no impact on the next iterations. 

 
1. If a sink is leaf, then it is useless and therefore is removed.
2. If, in the YO- phase the same value is received by a node from more than one in-neighbour, it will ask all but one to remove the link connecting them.

 

This method has a total cost of O(m log n) messages. Its real message complexity including pruning is an open research problem and is unknown.

 

## Applications

 
|  | This sectionneeds expansionwith: examples and additional citations. You can help byadding missing information.(October 2014) |
| --- | --- |

 

### Radio networks

 

In radio network protocols, leader election is often used as a first step to approach more advanced communication primitives, such as message gathering or broadcasts.[[22]](./Leader_election#cite_note-22) The very nature of wireless networks induces collisions when adjacent nodes transmit at the same time; electing a leader allows to better coordinate this process. While the [diameter](./Diameter_(graph_theory)) *D* of a network is a natural lower bound for the time needed to elect a leader, [upper and lower bounds](./Upper_and_lower_bounds) for the leader election problem depend on the specific radio model studied.

 

#### Models and runtime

 

In radio networks, the *n* nodes may in every round choose to either transmit or receive a message. If *no collision detection* is available, then a node cannot distinguish between silence or receiving more than one message at a time. Should *collision detection* be available, then a node may detect more than one incoming message at the same time, even though the messages itself cannot be decoded in that case. In the *beeping model*, nodes can only distinguish between silence or at least one message via [carrier sensing](./Carrier_sense).

 

Known runtimes for [single-hop](./Hop_(networking)) networks range from a constant (expected with collision detection) to *O(n log n)* rounds (deterministic and no collision detection). In [multi-hop](./Hop_(networking)) networks, known runtimes differ from roughly *O((D+ log n)(log2 log n))* rounds (with high probability in the beeping model), *O(D log n)* (deterministic in the beeping model), *O(n)* (deterministic with collision detection) to *O(n log3/2 n (log log n)0.5)* rounds (deterministic and no collision detection).

 

## See also

 
- [Distributed computing § Election](./Distributed_computing#Election)
- [Bully algorithm](./Bully_algorithm)
- [Chang and Roberts algorithm](./Chang_and_Roberts_algorithm)
- [HS algorithm](./HS_algorithm)
- [Voting system](./Voting_system)

 

## References

 
1. [↑](./Leader_election#cite_ref-1) [R. G. Gallager](./Robert_G._Gallager), P. A. Humblet, and P. M. Spira (January 1983). ["A Distributed Algorithm for Minimum-Weight Spanning Trees"](https://wayback.archive-it.org/all/20161012010516/http://theory.csail.mit.edu/classes/6.852/05/papers/p66-gallager.pdf) (PDF). *ACM Transactions on Programming Languages and Systems*. **5** (1): 66–77. [doi](./Doi_(identifier)):[10.1145/357195.357200](https://doi.org/10.1145%2F357195.357200). [S2CID](./S2CID_(identifier)) [2758285](https://api.semanticscholar.org/CorpusID:2758285). Archived from [the original](http://theory.csail.mit.edu/classes/6.852/05/papers/p66-gallager.pdf) (PDF) on 2016-10-12. Retrieved 2007-09-30.`{{cite journal}}`:  CS1 maint: multiple names: authors list ([link](./Category:CS1_maint:_multiple_names:_authors_list))
2. [↑](./Leader_election#cite_ref-2) Ephraim Korach, Shay Kutten, [Shlomo Moran](./Shlomo_Moran) (1990). "A Modular Technique for the Design of Efficient Distributed Leader Finding Algorithms". *ACM Transactions on Programming Languages and Systems*. **12** (1): 84–101. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.139.7342](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.139.7342). [doi](./Doi_(identifier)):[10.1145/77606.77610](https://doi.org/10.1145%2F77606.77610). [S2CID](./S2CID_(identifier)) [9175968](https://api.semanticscholar.org/CorpusID:9175968).`{{cite journal}}`:  CS1 maint: multiple names: authors list ([link](./Category:CS1_maint:_multiple_names:_authors_list))
3. [1](./Leader_election#cite_ref-AttiyaWelch3_3-0) [2](./Leader_election#cite_ref-AttiyaWelch3_3-1) [3](./Leader_election#cite_ref-AttiyaWelch3_3-2) [4](./Leader_election#cite_ref-AttiyaWelch3_3-3) [5](./Leader_election#cite_ref-AttiyaWelch3_3-4) [6](./Leader_election#cite_ref-AttiyaWelch3_3-5) H. Attiya and J. Welch, *Distributed Computing: Fundamentals, Simulations and Advance Topics*, John Wiley & Sons Inc., 2004, chap. 3
4. [↑](./Leader_election#cite_ref-4) I. Gupta, R. van Renesse, and K. P. Birman, 2000, A Probabilistically Correct Leader Election Protocol for Large Groups, *Technical Report*, Cornell University
5. [↑](./Leader_election#cite_ref-5) R. Bakhshi, W. Fokkink, J. pang, and J. Van de Pol, c2008 "Leader Election in Anonymous Rings:Franklin Goes Probabilistic", *TCS*, Vol. 273, pp. 57-72.
6. [↑](./Leader_election#cite_ref-6) H. Attiya and M. Snir, 1988,"Computing on an anonymous ring",*JACM*, Vol. 35, issue. 4, pp. 845-875
7. [↑](./Leader_election#cite_ref-7) A. Itai and M. Rodeh, 1990,"Symmetry breaking in distributed networks", Vol. 88, issue 1, pp. 60-87.
8. [↑](./Leader_election#cite_ref-8) L. Higham and S. Myers, 1998, "Self-Stabilizing Token Circulation on Anonymous Message Passing Rings", *Second International Conference On Principles Of Distributed Systems*.
9. [↑](./Leader_election#cite_ref-9) G. Itkis, C. Lin, and J. Simon,1995,"Deterministic, constant space, self-stabilizing leader election on uniform rings.", * In Proc. 9th Workshop on Distributed Algorithms*, Vol. 972, pp. 288-302.
10. [↑](./Leader_election#cite_ref-10) J. Burns and J. Pachl,1989,"Uniform self-stabilizing rings",*ACM Trans. Program. Lang. Systems*, Vol. 11, issue. 2, pp.330-344
11. [↑](./Leader_election#cite_ref-11) T. Herman, 1990, "Probabilistic self-stabilization", *Inf. Process. Lett.*, Vol. 35, issue 2, pp.63-67.
12. [↑](./Leader_election#cite_ref-12) G. Tel,*Introduction to Distributed Algorithms*. Cambridge University Press, 2000.2nd edition
13. [↑](./Leader_election#cite_ref-13) M. Fischer and H. Jiang, 2006,"Self-stabilizing leader election in networks of _nite-state anonymous agents", *In Proc. 10th Conf. on Principles of Distributed Systems*, Vol. 4305, pp. 395-409.
14. [↑](./Leader_election#cite_ref-14) E. Chang and R. Roberts, 1979, "An improved algorithm for decentralized extrema-finding in circular configurations of processes", *ACM*, Vol. 22, issue 5, pp. 281-283.
15. [↑](./Leader_election#cite_ref-15) D. S. Hirschberg and J. B. Sinclair, 1980, "Decentralized extrema-finding in circular configurations of processors", *ACM*, Vol. 23, issue 11, pp. 627-628.
16. [1](./Leader_election#cite_ref-N._Santoro,_2006_16-0) [2](./Leader_election#cite_ref-N._Santoro,_2006_16-1) [3](./Leader_election#cite_ref-N._Santoro,_2006_16-2) [4](./Leader_election#cite_ref-N._Santoro,_2006_16-3) [5](./Leader_election#cite_ref-N._Santoro,_2006_16-4) N. Santoro, *Design and Analysis of Distributed Algorithms*, Wiley, 2006.
17. [↑](./Leader_election#cite_ref-17) H. Kallasjoki, 2007, "Election in Mesh, Cube and Complete Networks", *Seminar on Theoretical Computer Science*.
18. [↑](./Leader_election#cite_ref-18) M. Refai, A. Sharieh and . Alsmmari, 2010, "Leader Election Algorithm in 2D Torus Network with the Presence of One Link Failure", *The International Arab Journal of Information Technology*, Vol. 7, No. 2.
19. [↑](./Leader_election#cite_ref-19) M Al Refai,2014, "Dynamic Leader Election Algorithm in 2D Torus Network with Multi Links Failure", *IJCST*, Vol. 2, issue 5.
20. [1](./Leader_election#cite_ref-orginalcompalgo_20-0) [2](./Leader_election#cite_ref-orginalcompalgo_20-1) J. Villadangos, A. Cordoba, F. Farina, and M. Prieto, 2005, "Efficient leader election in complete networks", *PDP*, pp.136-143.
21. [1](./Leader_election#cite_ref-modifiedcompalgo_21-0) [2](./Leader_election#cite_ref-modifiedcompalgo_21-1) Castillo, Maria, et al. "A Modified O(n) Leader Election Algorithm for Complete Networks." 15th EUROMICRO International Conference on Parallel, Distributed and Network-Based Processing (PDP'07). IEEE, 2007.
22. [↑](./Leader_election#cite_ref-22) Haeupler, Bernhard; Ghaffari, Mohsen (2013). *Near Optimal Leader Election in Multi-Hop Radio Networks*. pp. 748–766. [arXiv](./ArXiv_(identifier)):[1210.8439](https://arxiv.org/abs/1210.8439). [doi](./Doi_(identifier)):[10.1137/1.9781611973105.54](https://doi.org/10.1137%2F1.9781611973105.54). [ISBN](./ISBN_(identifier)) [978-1-61197-251-1](./Special:BookSources/978-1-61197-251-1). [S2CID](./S2CID_(identifier)) [9976342](https://api.semanticscholar.org/CorpusID:9976342). `{{cite book}}`: `|journal=` ignored ([help](./Help:CS1_errors#periodical_ignored))