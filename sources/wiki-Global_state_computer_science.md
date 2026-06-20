---
source: https://en.wikipedia.org/wiki/Global_state_(computer_science)
fetched: 2026-06-19
---

Snapshot of distributed system state 

 

 

A **global state** of a [distributed system](./Distributed_computing) is the tuple of all [process](./Process_(computing)) local states and the contents of all [communication channels](./Communication_channel) at a particular instant. Because distributed systems lack shared memory and a [global clock](./Global_clock?action=edit&redlink=1), no single process can observe all local states and in-transit messages simultaneously.

 

A naive assembly of local states collected sequentially, without coordination, produces a global state that may not correspond to any state the system actually passed through. A message sent before one process's state is recorded but received after another's can appear to have vanished or been duplicated, yielding a logically impossible snapshot.

 

A global state is *consistent* if it corresponds to a state through which a possible execution of the system could have passed: formally, no message is recorded as received unless it is also recorded as sent. This notion, introduced by [K. Mani Chandy](./K._Mani_Chandy) and [Leslie Lamport](./Leslie_Lamport) in 1985, is also expressed as a *consistent cut* of the system's execution history. Chandy and Lamport proved that any consistent global state is reachable from the system's initial state, and the actual current state is reachable from any recorded consistent global state.

 

Consistent global states underpin [deadlock](./Deadlock_(computer_science)) detection, termination detection, distributed [garbage collection](./Garbage_collection_(computer_science)), checkpointing for fault tolerance, and distributed debugging. They are sufficient for evaluating *stable predicates*, properties that once true remain true, without requiring the system to pause.

 

## System model

 

The model adopted by Chandy and Lamport consists of a fixed set of *n* [processes](./Process_(computing)) *p*1, *p*2, …, *p**n* connected by directed [FIFO](./FIFO_(computing_and_electronics)) channels.[[1]](./Global_state_(computer_science)#cite_note-ChandyLamport1985-1)[[2]](./Global_state_(computer_science)#cite_note-LynchBook-2) Channel *c**ij* carries messages from *p**i* to *p**j*. Channels are reliable: they deliver messages in order without loss or duplication, and a directed path exists between every pair of processes.

 

Each process executes a sequence of three types of events: a *send* event on an outgoing channel, a *receive* event on an incoming channel, or an *internal* event that changes local state without communicating.[[1]](./Global_state_(computer_science)#cite_note-ChandyLamport1985-1)[[3]](./Global_state_(computer_science)#cite_note-TelBook-3) The **local state** *s**i* of process *p**i* after an event is the information sufficient to determine *p**i*'s future behaviour. The **channel state** *M**ij* is the [sequence](./Sequence) of messages sent on *c**ij* that have not yet been received; these are the messages in transit on that channel at a given instant.

 

The [happened-before](./Happened-before) relation on events, introduced by Lamport in 1978, provides a partial order: event *e* happened before event *f* if *e* and *f* are events of the same process and *e* precedes *f*, or if *e* is a send and *f* is the corresponding receive, or if there exists an event *g* such that *e* happened before *g* and *g* happened before *f*.[[2]](./Global_state_(computer_science)#cite_note-LynchBook-2)

 

## Global state

 

A **global state** of the system is a tuple

     G S = (  s  1   ,  s  2   , … …  ,  s  n   ,    M  12   ,  M  13   , … …  ,  M  n ( n − −  1 )   )   {\displaystyle GS=(s_{1},s_{2},\ldots ,s_{n},\ M_{12},M_{13},\ldots ,M_{n(n-1)})}  ![{\displaystyle GS=(s_{1},s_{2},\ldots ,s_{n},\ M_{12},M_{13},\ldots ,M_{n(n-1)})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ac02cbf7494aa873e31af1e1e9fa3c97cddaaa2b) 

consisting of a local state *s**i* for each process *p**i* and a channel state *M**ij* for each channel *c**ij*.[[1]](./Global_state_(computer_science)#cite_note-ChandyLamport1985-1)[[4]](./Global_state_(computer_science)#cite_note-GhoshBook-4) The channel state *M**ij* records the sequence of messages in transit on *c**ij*: those sent by *p**i* but not yet received by *p**j*.

 

As a mathematical object, a global state need not correspond to any instant that was simultaneously observable from a single vantage point.[[2]](./Global_state_(computer_science)#cite_note-LynchBook-2) Two processes may have their local states recorded at different real times, and messages in transit during that interval may appear in neither process's local state.

 

**Example.** Consider three processes *p*1, *p*2, *p*3. If *p*1 has sent message *m*12 but *p*2 has not yet received it, a global state recording *p*1's post-send state and *p*2's pre-receive state must record *M*12 containing *m*12 to account for the message in transit. Omitting *m*12 from the channel state would produce a global state no real execution could pass through.

 

## Consistent global state

 

### The consistency condition

 

An *execution history* of the system is the set of all events partially ordered by the happened-before relation. A **cut** *C* is a partition of the execution history into a past set and a future set such that if event *f* is in the past and *e* happened before *f*, then *e* is also in the past.[[3]](./Global_state_(computer_science)#cite_note-TelBook-3)[[2]](./Global_state_(computer_science)#cite_note-LynchBook-2) The *frontier* of the cut for process *p**i* is the last event of *p**i* in the past of *C*; the corresponding local state *s**i* is *p**i*'s contribution to the global state defined by *C*.

 

A cut is **consistent** if for every receive event in the past of *C*, the corresponding send event is also in the past of *C*.[[1]](./Global_state_(computer_science)#cite_note-ChandyLamport1985-1) Equivalently, the channel state *M**ij* contains exactly the messages sent on *c**ij* by events in the past of *p**i* that have not yet been received by events in the past of *p**j*. A global state defined by a consistent cut is a **consistent global state**, also called a *consistent snapshot*.[[1]](./Global_state_(computer_science)#cite_note-ChandyLamport1985-1)[[3]](./Global_state_(computer_science)#cite_note-TelBook-3)

 

### Why naive collection fails

 [![Diagram showing three process timelines with marker messages propagating along channels](//upload.wikimedia.org/wikipedia/commons/e/e7/Ejemplo_grafico_Chandy-Lamport.png)](./File:Ejemplo_grafico_Chandy-Lamport.png)Three-process illustration of consistent-cut marker propagation. 

If an observer records local states sequentially (first querying *p*1, then *p*2, without coordination), the result need not be a consistent global state.[[2]](./Global_state_(computer_science)#cite_note-LynchBook-2) Suppose *p*1 sends message *m* to *p*2 between the two observations: the observer records *p*1's state after the send (so *m* does not appear in *p*1's local state) and *p*2's state before the receive (so *m* does not appear in *p*2's local state or in the recorded channel state). Message *m* has vanished: the recorded global state has no trace of it, which no real execution could produce.

 

The corresponding cut is inconsistent: the receive of *m* by *p*2 is in the future of the cut, but the send of *m* by *p*1 is in the past. This violates the consistency condition.[[1]](./Global_state_(computer_science)#cite_note-ChandyLamport1985-1)

 

### Reachability theorem

 

Chandy and Lamport proved that any consistent global state recorded during an execution is reachable from the initial state of that execution, and the actual state of the system at the time recording completes is reachable from the recorded consistent global state.[[1]](./Global_state_(computer_science)#cite_note-ChandyLamport1985-1) Formally, if *S*0 is the initial state, *S* the consistent global state recorded by the algorithm, and *S*′ the actual state when recording finishes, then *S*0 can reach *S* and *S* can reach *S*′ in the system's execution order.

 

The recorded state need not coincide with any state that simultaneously existed during execution, but it represents a valid intermediate state through which a possible execution of the system could have passed.[[2]](./Global_state_(computer_science)#cite_note-LynchBook-2)[[3]](./Global_state_(computer_science)#cite_note-TelBook-3) This property makes the recorded state reliable for checking system properties (such as whether a deadlock exists) without freezing or pausing execution.

 

## Stable predicates

 

A [predicate](./Predicate_(logic)) Φ on global states is **stable** if Φ(*S*) = true implies Φ(*S*′) = true for every global state *S*′ reachable from *S*.[[1]](./Global_state_(computer_science)#cite_note-ChandyLamport1985-1)[[3]](./Global_state_(computer_science)#cite_note-TelBook-3) Deadlock, a condition in which no process can make progress, is stable; once all processes are blocked in a wait-for cycle, no unilateral action can break it. Termination, a condition in which all processes have halted and all channels are empty, is similarly stable. [Garbage-collection](./Garbage_collection_(computer_science)) eligibility, the condition that no live process holds a reference to a given object, is stable across the heap states of all processes.[[4]](./Global_state_(computer_science)#cite_note-GhoshBook-4)

 

By the reachability theorem, if a stable predicate Φ holds in a recorded consistent global state *S*, it holds in the actual current state *S*′, because *S*′ is reachable from *S* and stability guarantees Φ cannot become false along any reachable path.[[1]](./Global_state_(computer_science)#cite_note-ChandyLamport1985-1)[[2]](./Global_state_(computer_science)#cite_note-LynchBook-2) A snapshot algorithm can therefore detect stable conditions without interrupting execution.

 

Unstable predicates, those that can become false after becoming true, cannot be reliably evaluated from a single snapshot. Detecting transient conditions such as whether a particular message is currently in transit requires continuous monitoring or multiple observations, outside the scope of snapshot-based techniques.[[3]](./Global_state_(computer_science)#cite_note-TelBook-3)

 

## Recording a global state

 Main articles: [Snapshot algorithm](./Snapshot_algorithm) and [Chandy–Lamport algorithm](./Chandy–Lamport_algorithm) 

Recording a consistent global state requires a coordinated protocol because messages may be in transit when local states are collected; an uncoordinated collection can produce an inconsistent cut.[[1]](./Global_state_(computer_science)#cite_note-ChandyLamport1985-1) Any correct protocol must guarantee that the set of recorded local states and channel contents satisfies the consistency condition.

 

The marker-based protocol of Chandy and Lamport (1985) proceeds as follows.[[1]](./Global_state_(computer_science)#cite_note-ChandyLamport1985-1) The initiating process records its own local state and sends a special control message, a *marker*, on every outgoing channel before sending any further application messages on those channels. When a process *p**i* receives a marker on channel *c**ji* for the first time, it records its own local state, records the state of *c**ji* as empty, and sends a marker on all its own outgoing channels. Messages received on any incoming channel *c**ki* after *p**i*'s state is recorded but before the marker arrives on *c**ki* are recorded as the state of that channel. The algorithm terminates when every process has received a marker on all incoming channels; the collected local states and channel states form a consistent global state.[[1]](./Global_state_(computer_science)#cite_note-ChandyLamport1985-1)[[2]](./Global_state_(computer_science)#cite_note-LynchBook-2)

 

The marker-based protocol assumes FIFO channel ordering. For systems with non-FIFO channels, the Lai–Yang algorithm (1987) uses message *colouring*, tagging each application message as pre-snapshot or post-snapshot, to avoid the need for explicit markers.[[5]](./Global_state_(computer_science)#cite_note-LaiYang1987-5) Mattern's algorithm (1989) uses [vector clocks](./Vector_clock) to determine which messages belong to which snapshot, enabling multiple concurrent snapshots without dedicated marker messages.[[6]](./Global_state_(computer_science)#cite_note-Mattern1989-6)

 

## Applications

 

Consistent global states, and the stable-predicate property they support, have been applied across distributed systems research and practice.[[1]](./Global_state_(computer_science)#cite_note-ChandyLamport1985-1)[[4]](./Global_state_(computer_science)#cite_note-GhoshBook-4)

 
- **Deadlock detection.** A distributed deadlock is a cycle of processes each waiting for a resource held by the next; this is a stable property. Recording a consistent global state and checking the recorded wait-for graph for cycles detects deadlock without false negatives: if a cycle exists in the recorded state, it exists in the actual current state by stability.[[1]](./Global_state_(computer_science)#cite_note-ChandyLamport1985-1)[[2]](./Global_state_(computer_science)#cite_note-LynchBook-2)

 
- **Termination detection.** Termination, no process active and no messages in transit, is stable. A consistent global snapshot in which all process states are idle and all channel states are empty confirms that the computation has finished.[[3]](./Global_state_(computer_science)#cite_note-TelBook-3)[[4]](./Global_state_(computer_science)#cite_note-GhoshBook-4)

 
- **Distributed garbage collection.** An object with no live references is eligible for collection; this property is stable across the combined heap states of all processes. Snapshot-based garbage collectors identify unreachable objects by recording a consistent global state of all process heaps.[[4]](./Global_state_(computer_science)#cite_note-GhoshBook-4)

 
- **Checkpointing and rollback recovery.** Periodically recording consistent global states creates recovery points from which execution can restart after a process failure, without replaying the full execution from the beginning. The reachability theorem guarantees that restarting from a recorded consistent state leads to a valid continuation.[[4]](./Global_state_(computer_science)#cite_note-GhoshBook-4)[[2]](./Global_state_(computer_science)#cite_note-LynchBook-2)

 
- **Distributed debugging.** Assertion violations and invariant failures are stable if framed as conditions that, once triggered, are not automatically cleared. Replaying recorded consistent global states allows a debugger to check whether such conditions held during an execution.[[4]](./Global_state_(computer_science)#cite_note-GhoshBook-4)

 

## Extensions

 

Subsequent work has relaxed the assumptions of the original Chandy–Lamport model.[[3]](./Global_state_(computer_science)#cite_note-TelBook-3)[[4]](./Global_state_(computer_science)#cite_note-GhoshBook-4)

 

**Non-FIFO channels.** The original protocol requires channels to deliver messages in order. Lai and Yang (1987) extended snapshot recording to non-FIFO channels by colouring messages: each process colours all application messages it sends after recording its own state with a post-snapshot colour, allowing receivers to distinguish pre-snapshot from post-snapshot messages without markers.[[5]](./Global_state_(computer_science)#cite_note-LaiYang1987-5) Mattern (1989) achieved a similar result using vector clocks, which provide each message with a timestamp sufficient to determine its relationship to the snapshot without explicit colouring or markers.[[6]](./Global_state_(computer_science)#cite_note-Mattern1989-6)

 

**Systems with process failures.** If a process fails during snapshot recording, its local state cannot be captured; messages in transit on channels to or from the failed process may never be delivered. Coordinated checkpointing protocols and message-logging schemes extend snapshot recording for fault-tolerant systems by combining local state recording with logging of sent and received messages, enabling recovery even when some recorded states are lost.[[3]](./Global_state_(computer_science)#cite_note-TelBook-3)[[4]](./Global_state_(computer_science)#cite_note-GhoshBook-4)

 

**Dynamic process sets.** Variants exist for systems in which processes may join or leave the computation during execution. These protocols track process membership as part of the snapshot, recording which processes existed at the time of each local state observation.[[3]](./Global_state_(computer_science)#cite_note-TelBook-3)

 

## See also

 
- [Chandy–Lamport algorithm](./Chandy–Lamport_algorithm)
- [Snapshot algorithm](./Snapshot_algorithm)
- [Vector clock](./Vector_clock)
- [Lamport timestamp](./Lamport_timestamp)
- [Happened-before](./Happened-before)
- [Deadlock](./Deadlock_(computer_science))
- [Distributed computing](./Distributed_computing)

 

## References

  
1. [1](./Global_state_(computer_science)#cite_ref-ChandyLamport1985_1-0) [2](./Global_state_(computer_science)#cite_ref-ChandyLamport1985_1-1) [3](./Global_state_(computer_science)#cite_ref-ChandyLamport1985_1-2) [4](./Global_state_(computer_science)#cite_ref-ChandyLamport1985_1-3) [5](./Global_state_(computer_science)#cite_ref-ChandyLamport1985_1-4) [6](./Global_state_(computer_science)#cite_ref-ChandyLamport1985_1-5) [7](./Global_state_(computer_science)#cite_ref-ChandyLamport1985_1-6) [8](./Global_state_(computer_science)#cite_ref-ChandyLamport1985_1-7) [9](./Global_state_(computer_science)#cite_ref-ChandyLamport1985_1-8) [10](./Global_state_(computer_science)#cite_ref-ChandyLamport1985_1-9) [11](./Global_state_(computer_science)#cite_ref-ChandyLamport1985_1-10) [12](./Global_state_(computer_science)#cite_ref-ChandyLamport1985_1-11) [13](./Global_state_(computer_science)#cite_ref-ChandyLamport1985_1-12) [14](./Global_state_(computer_science)#cite_ref-ChandyLamport1985_1-13) [Chandy, K. Mani](./K._Mani_Chandy); [Lamport, Leslie](./Leslie_Lamport) (February 1985). "Distributed snapshots: Determining global states of distributed systems". *[ACM Transactions on Computer Systems](./ACM_Transactions_on_Computer_Systems)*. **3** (1): 63–75. [doi](./Doi_(identifier)):[10.1145/214451.214456](https://doi.org/10.1145%2F214451.214456).
2. [1](./Global_state_(computer_science)#cite_ref-LynchBook_2-0) [2](./Global_state_(computer_science)#cite_ref-LynchBook_2-1) [3](./Global_state_(computer_science)#cite_ref-LynchBook_2-2) [4](./Global_state_(computer_science)#cite_ref-LynchBook_2-3) [5](./Global_state_(computer_science)#cite_ref-LynchBook_2-4) [6](./Global_state_(computer_science)#cite_ref-LynchBook_2-5) [7](./Global_state_(computer_science)#cite_ref-LynchBook_2-6) [8](./Global_state_(computer_science)#cite_ref-LynchBook_2-7) [9](./Global_state_(computer_science)#cite_ref-LynchBook_2-8) [10](./Global_state_(computer_science)#cite_ref-LynchBook_2-9) [Lynch, Nancy A.](./Nancy_Lynch) (1996). *Distributed Algorithms*. San Francisco: Morgan Kaufmann. [ISBN](./ISBN_(identifier)) [978-1-55860-348-6](./Special:BookSources/978-1-55860-348-6).
3. [1](./Global_state_(computer_science)#cite_ref-TelBook_3-0) [2](./Global_state_(computer_science)#cite_ref-TelBook_3-1) [3](./Global_state_(computer_science)#cite_ref-TelBook_3-2) [4](./Global_state_(computer_science)#cite_ref-TelBook_3-3) [5](./Global_state_(computer_science)#cite_ref-TelBook_3-4) [6](./Global_state_(computer_science)#cite_ref-TelBook_3-5) [7](./Global_state_(computer_science)#cite_ref-TelBook_3-6) [8](./Global_state_(computer_science)#cite_ref-TelBook_3-7) [9](./Global_state_(computer_science)#cite_ref-TelBook_3-8) [10](./Global_state_(computer_science)#cite_ref-TelBook_3-9) Tel, Gerard (2001). *Introduction to Distributed Algorithms* (2nd ed.). Cambridge: Cambridge University Press. [ISBN](./ISBN_(identifier)) [978-0-521-79483-1](./Special:BookSources/978-0-521-79483-1).
4. [1](./Global_state_(computer_science)#cite_ref-GhoshBook_4-0) [2](./Global_state_(computer_science)#cite_ref-GhoshBook_4-1) [3](./Global_state_(computer_science)#cite_ref-GhoshBook_4-2) [4](./Global_state_(computer_science)#cite_ref-GhoshBook_4-3) [5](./Global_state_(computer_science)#cite_ref-GhoshBook_4-4) [6](./Global_state_(computer_science)#cite_ref-GhoshBook_4-5) [7](./Global_state_(computer_science)#cite_ref-GhoshBook_4-6) [8](./Global_state_(computer_science)#cite_ref-GhoshBook_4-7) [9](./Global_state_(computer_science)#cite_ref-GhoshBook_4-8) Ghosh, Sukumar (2014). *Distributed Systems: An Algorithmic Approach* (2nd ed.). Boca Raton: CRC Press. [ISBN](./ISBN_(identifier)) [978-1-4665-5298-2](./Special:BookSources/978-1-4665-5298-2).
5. [1](./Global_state_(computer_science)#cite_ref-LaiYang1987_5-0) [2](./Global_state_(computer_science)#cite_ref-LaiYang1987_5-1) Lai, Ten-Hwang; Yang, Tao H. (June 1987). "On distributed snapshots". *Information Processing Letters*. **25** (3): 153–158. [doi](./Doi_(identifier)):[10.1016/0020-0190(87)90008-7](https://doi.org/10.1016%2F0020-0190%2887%2990008-7).
6. [1](./Global_state_(computer_science)#cite_ref-Mattern1989_6-0) [2](./Global_state_(computer_science)#cite_ref-Mattern1989_6-1) Mattern, Friedemann (1989). "Virtual time and global states of distributed systems". *Parallel and Distributed Algorithms*. North-Holland. pp. 215–226.