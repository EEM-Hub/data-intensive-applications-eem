---
source: https://en.wikipedia.org/wiki/Bully_algorithm
fetched: 2026-06-19
---

Method for electing a coordinator in distributed computing 

In [distributed computing](./Distributed_computing), the **bully algorithm** is a method for dynamically [electing](./Leader_election) a [coordinator](./Distributed_computing#Election) or leader from a group of distributed computer processes. The process with the highest process ID number from amongst the non-failed processes is selected as the coordinator.

 

## Assumptions

 

The algorithm assumes that:[[1]](./Bully_algorithm#cite_note-1)

 
- the system is synchronous.
- processes may fail at any time, including during execution of the algorithm.
- a process fails by stopping and returns from failure by restarting.
- there is a failure detector which detects failed processes.
- message delivery between processes is reliable.
- each process knows its own process id and address, and that of every other process.

 

## Algorithm

 

The [algorithm](./Algorithm) uses the following message types:

 
- Election Message: Sent to announce election.
- Answer (Alive) Message: Responds to the Election message.
- Coordinator (Victory) Message: Sent by winner of the election to announce victory.

 

When a process P recovers from failure, or the failure detector indicates that the current coordinator has failed, P performs the following actions:

 
1. If P has the highest process ID, it sends a Victory message to all other processes and becomes the new Coordinator. Otherwise, P broadcasts an Election message to all other processes with higher process IDs than itself.
2. If P receives no Answer after sending an Election message, then it broadcasts a Victory message to all other processes and becomes the Coordinator.
3. If P receives an Answer from a process with a higher ID, it sends no further messages for this election and waits for a Victory message.  (If there is no Victory message after a period of time, it restarts the process at the beginning.)
4. If P receives an Election message from another process with a lower ID it sends an Answer message back and if it has not already started an election, it starts the election process at the beginning, by sending an Election message to higher-numbered processes.
5. If P receives a Coordinator message, it treats the sender as the coordinator.

 

### Analysis

 

#### Safety

 

The safety property expected of [leader election](./Leader_election) protocols is that every non-faulty process either elects a process Q, or elects none at all. Note that all [processes](./Process_(computing)) that elect a leader must decide on the same process Q as the leader. The Bully algorithm satisfies this property (under the system model specified), and at no point in time is it possible for two processes in the group to have
a conflicting view of who the leader is, except during an election. This is true because if it weren't, there are two processes X and Y such that both sent the Coordinator (victory) message to the group. This means X and Y must also have sent each other victory messages. But this cannot happen, since before sending the victory message, Election messages would have been exchanged between the two, and the process with a lower process ID among the two would never send out victory messages. We have a contradiction, and hence our initial assumption that there are two leaders in the system at any given time is false, and that shows that the bully algorithm is safe.

 

#### Liveness

 

[Liveness](./Liveness) is also guaranteed in the [synchronous](./Synchronous), crash-recovery model. Consider the would-be leader failing after sending an Answer (Alive) message but before sending a Coordinator (victory) message. If it does not recover before the set timeout on lower ID processes, one of them will become leader eventually (even if some of the other processes crash). If the failed process recovers in time, it simply sends a Coordinator (victory) message to all of the group.

 

#### Network bandwidth utilization

 See also: [network bandwidth](./Network_bandwidth) 

Assuming that the bully algorithm messages are of a fixed (known, invariant) sizes, the most number of messages are exchanged in the group when the process with the lowest ID initiates an election. This process sends (N−1) Election messages, the next higher ID sends (N−2) messages, and so on, resulting in     Θ Θ   (  N  2   )    {\displaystyle \Theta \left(N^{2}\right)}  ![{\displaystyle \Theta \left(N^{2}\right)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2b80aaaf1ee027d094109717c77f7ab1e8882373) election messages. There are also the     Θ Θ   (  N  2   )    {\displaystyle \Theta \left(N^{2}\right)}  ![{\displaystyle \Theta \left(N^{2}\right)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2b80aaaf1ee027d094109717c77f7ab1e8882373) Alive messages, and     Θ Θ   ( N )    {\displaystyle \Theta \left(N\right)}  ![{\displaystyle \Theta \left(N\right)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/edaa7032a213984dc16f5ea2275a928492f771ad) co-ordinator messages, thus making the overall number messages exchanged in the worst case be     Θ Θ   (  N  2   )    {\displaystyle \Theta \left(N^{2}\right)}  ![{\displaystyle \Theta \left(N^{2}\right)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2b80aaaf1ee027d094109717c77f7ab1e8882373).

 

## See also

 
- [Leader election](./Leader_election)
- [Chang and Roberts algorithm](./Chang_and_Roberts_algorithm)

 

## References

  
1. [↑](./Bully_algorithm#cite_ref-1) Coulouris, George; Dollimore, Jean; Kindberg, Tim (2000). *Distributed Systems: Concepts and Design* (3rd ed.). Addison Wesley. [ISBN](./ISBN_(identifier)) [978-0201619188](./Special:BookSources/978-0201619188).

 
- Witchel, Emmett (2005).  ["Distributed Coordination"](http://www.cs.utexas.edu/users/witchel/372/lectures/25.DistributedCoordination.ppt). Retrieved May 4, 2005.
- Hector Garcia-Molina, Elections in a Distributed Computing System, IEEE Transactions on Computers, Vol. C-31, No. 1, January (1982) 48–59
- L. Lamport, R. Shostak, and M. Pease,  ["The Byzantine Generals Problem"](http://research.microsoft.com/en-us/um/people/lamport/pubs/byz.pdf) ACM Transactions on Programming Languages and Systems, Vol. 4, No. 3, July 1982.

 

## External links

 
- [![Wikimedia Commons logo](//upload.wikimedia.org/wikipedia/en/thumb/4/4a/Commons-logo.svg/20px-Commons-logo.svg.png)](./File:Commons-logo.svg) Media related to [Bully algorithm](https://commons.wikimedia.org/wiki/Category:Bully%20algorithm) at Wikimedia Commons