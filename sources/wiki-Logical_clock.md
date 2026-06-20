---
source: https://en.wikipedia.org/wiki/Logical_clock
fetched: 2026-06-19
---

Mechanism for capturing chronological and causal relationships 

A **logical clock** is a mechanism for capturing chronological and causal relationships in a [distributed system](./Distributed_system). Often, distributed systems may have no physically synchronous global clock. In many applications (such as distributed [GNU make](./GNU_make)), if two processes never interact, the lack of synchronization is unobservable and in these applications it is enough for the processes to agree on the event ordering (i.e., logical clock) rather than the wall-clock time.[[1]](./Logical_clock#cite_note-1) The idea of logical clocks is due to [Leslie Lamport](./Leslie_Lamport), who introduced it in 1978 with [his system of timestamps](./Lamport_timestamp).

 

## Local vs global time

 

In logical clock systems each process has two data structures: *logical local time* and *logical global time*. Logical local time is used by the process to mark its own events, and logical global time is the local information about global time. A special protocol is used to update logical local time after each local event, and logical global time when processes exchange data.[[2]](./Logical_clock#cite_note-ch3-2)

 

## Applications

 

Logical clocks are useful in computation analysis, distributed algorithm design, individual event tracking, and exploring computational progress.

 

## Algorithms

 

Some noteworthy logical clock algorithms are:

 
- [Lamport timestamps](./Lamport_timestamp), which are monotonically increasing software counters.
- [Vector clocks](./Vector_clock), that allow for partial ordering of events in a distributed system.
- [Version vectors](./Version_vector), order replicas, according to updates, in an [optimistic replicated system](./Optimistic_replication).
- [Matrix clocks](./Matrix_clock), an extension of vector clocks that also contains information about other processes' views of the system.

 

## References

  
1. [↑](./Logical_clock#cite_ref-1) ["Distributed Systems 3rd edition (2017)"](https://www.distributed-systems.net/index.php/books/ds3/). *DISTRIBUTED-SYSTEMS.NET*. [Archived](https://web.archive.org/web/20200812174339/https://www.distributed-systems.net/index.php/books/ds3/) from the original on 2020-08-12. Retrieved 2021-03-20.
2. [↑](./Logical_clock#cite_ref-ch3_2-0) [Chapter 3: Logical Time](http://www.cs.uic.edu/~ajayk/Chapter3.pdf) [Archived](https://web.archive.org/web/20150923211943/http://www.cs.uic.edu/~ajayk/Chapter3.pdf) 2015-09-23 at the [Wayback Machine](./Wayback_Machine) // Ajay Kshemkalyani and Mukesh Singhal, Distributed Computing: Principles, Algorithms, and Systems, Cambridge University Press, 2008

 

## External links

 
- [Distributed System Logical Time](https://web.archive.org/web/20150122075241/http://www.dis.uniroma1.it/~baldoni/Logical_Time.pdf) // Roberto Baldoni, Silvia Bonomi. MIDLAB, Sapienza University of Rome
- [Chapter 3: Logical Time](http://www.cs.uic.edu/~ajayk/Chapter3.pdf) // Ajay Kshemkalyani and Mukesh Singhal, Distributed Computing: Principles, Algorithms, and Systems, Cambridge University Press, 2008
- [Distributed Systems 06. Logical Clocks](https://www.cs.rutgers.edu/~pxk/417/notes/content/06-logical-clocks-slides.pdf) // Paul Krzyzanowski, Rutgers University, Fall 2014

 
| Authority control databases | GND |
| --- | --- |