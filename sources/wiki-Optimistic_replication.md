---
source: https://en.wikipedia.org/wiki/Optimistic_replication
fetched: 2026-06-19
---

Strategy for replication 

**Optimistic replication**, also known as **lazy replication**,[[1]](./Optimistic_replication#cite_note-Ladin1992-1)[[2]](./Optimistic_replication#cite_note-Ladin1990-2) is a strategy for [replication](./Replication_(computer_science)), in which replicas are allowed to diverge.[[3]](./Optimistic_replication#cite_note-saito2005-3)

 

Traditional pessimistic replication systems try to guarantee from the beginning that all of the replicas are identical to each other, as if there was only a single copy of the data all along. Optimistic replication does away with this in favor of [eventual consistency](./Eventual_consistency), meaning that replicas are guaranteed to converge only when the system has been [quiesced](./Quiesce) for a period of time. As a result, there is no longer a need to wait for all of the copies to be synchronized when updating data, which helps [concurrency](./Concurrency_(computer_science)) and [parallelism](./Parallel_computing). The trade-off is that different replicas may require explicit reconciliation later on, which might then prove difficult or even insoluble.

 

## Algorithms

 

An optimistic replication algorithm consists of five elements:

 
1. **Operation submission**: Users submit operations at independent sites.
2. **Propagation**: Each site shares the operations it knows about with the rest of the system.
3. **Scheduling**: Each site decides on an order for the operations it knows about.
4. **Conflict resolution**: If there are any conflicts among the operations a site has scheduled, it must modify them in some way.
5. **Commitment**: The sites agree on a final schedule and conflict resolution result, and the operations are made permanent.

 

There are two strategies for propagation: state transfer, where sites propagate a representation of the current state, and operation transfer, where sites propagate the operations that were performed (essentially, a list of instructions on how to reach the new state).

 

Scheduling and conflict resolution can either be syntactic or semantic. Syntactic systems rely on general information, such as when or where an operation was submitted. Semantic systems are able to make use of application-specific information to make smarter decisions. Note that state transfer systems generally have no information about the semantics of the data being transferred, and so they have to use syntactic scheduling and conflict resolution.

 

## Examples

 

One well-known example of a system based on optimistic replication is the [CVS](./Concurrent_Versions_System) [version control system](./Revision_control), or any other version control system which uses the [copy-modify-merge](http://tortoisesvn.net/docs/release/TortoiseSVN_en/tsvn-basics-versioning.html) paradigm. CVS covers each of the five elements:

 
1. Operation submission: Users edit local versions of files.
2. Propagation: Users manually pull updates from a central server, or push changes out once the user feels they are ready.
3. Scheduling: Operations are scheduled in the order that they are received by the central server.
4. Conflict resolution: When a user pushes to or pulls from the central repository, any conflicts will be flagged for that user to fix manually.
5. Commitment: Once the central server accepts the changes which a user pushes, they are permanently committed.

 

A special case of replication is [synchronization](./Data_synchronization), where there are only two replicas. For example, [personal digital assistants (PDAs)](./Personal_Digital_Assistant) allow users to edit data either on the PDA or a computer, and then to [merge](./Merge_(revision_control)) these two datasets together. Note, however, that replication is a broader problem than synchronization, since there may be more than two replicas.

 

Other examples include:

 
- [Usenet](./Usenet), and other systems which use the [Thomas Write Rule](./Thomas_write_rule) (See [Rfc677](http://tools.ietf.org/html/rfc677))
- [Multi-master database replication](./Multi-master_replication)[[4]](./Optimistic_replication#cite_note-Gray1996-4)
- The [Coda](./Coda_(file_system)) distributed filesystem
- [Operational Transformation](./Operational_transformation), a theoretical framework for group editing
- [Peer-to-peer wikis](./Peer-to-peer_wiki)
- [Conflict-free replicated data types](./Conflict-free_replicated_data_type)
- The Bayou[[5]](./Optimistic_replication#cite_note-Terry1995-5) distributed database
- IceCube[[6]](./Optimistic_replication#cite_note-Kermarrec2001-6)

 

## Implications

 

Applications built on top of optimistic replicated databases need to be careful about ensuring that the delayed updates observed do not impair the correctness of the application.

 

As a simple example, if an application contains a way of viewing some part of the database state, and a way of editing it, then users may edit that state but then not see it changing in the viewer. Alarmed that their edit "didn't work", they may try it again, potentially more than once. If the updates are not [idempotent](./Idempotence) (e.g., they increment a value), this can lead to disaster. Even if they are idempotent, the spurious database updates can lead to performance bottlenecks, especially when the database systems are processing heavy loads; this can become a vicious circle.

 

Testing of applications is often done on a testing environment, smaller in size (perhaps only a single server) and less loaded than the "live" environment. The replication behaviour of such an installation may differ from a live environment in ways that mean that replication lag is unlikely to be observed in testing, masking replication-sensitive bugs. Application developers must be very careful about the assumptions they make about the effect of a database update, and must be sure to simulate lag in their testing environments.

 

Optimistically replicated databases have to be very careful about offering features such as validity constraints on data. If any given update may or may not be accepted based on the current state of the record, then two updates (A and B) may be individually legal against the starting state of the system, but one or more of the updates may not be legal against the state of the system after the other update (e.g., A and B are both legal, but AB or BA are illegal). If A and B are both initiated at roughly the same time within the database, then A may be successfully applied on some nodes and B on others, but as soon as A and B "meet" and one is attempted on a node which has already applied the other, a conflict will be found. The system must, in this case, decide which update finally "wins", and arrange for any nodes that have already applied the losing update to revert it. However, some nodes may temporarily expose the state with the reverted update, and there may be no way to inform the user who initiated the update of its failure, without requiring them to wait (potentially forever) for confirmation of acceptance at every node.

 

## References

  
1. [↑](./Optimistic_replication#cite_ref-Ladin1992_1-0) Ladin, R.; Liskov, B.; Shrira, L.; Ghemawat, S. (1992). "Providing high availability using lazy replication". *ACM Transactions on Computer Systems*. **10** (4): 360–391. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.586.7749](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.586.7749). [doi](./Doi_(identifier)):[10.1145/138873.138877](https://doi.org/10.1145%2F138873.138877). [S2CID](./S2CID_(identifier)) [2219840](https://api.semanticscholar.org/CorpusID:2219840).
2. [↑](./Optimistic_replication#cite_ref-Ladin1990_2-0) Ladin, R.; Liskov, B.; Shrira, L. (1990). *Lazy replication: exploiting the semantics of distributed services*. Proceedings of the Ninth Annual ACM [Symposium on Principles of Distributed Computing](./Symposium_on_Principles_of_Distributed_Computing). pp. 43–57. [doi](./Doi_(identifier)):[10.1145/93385.93399](https://doi.org/10.1145%2F93385.93399). [hdl](./Hdl_(identifier)):[1721.1/149694](https://hdl.handle.net/1721.1%2F149694).
3. [↑](./Optimistic_replication#cite_ref-saito2005_3-0)  Saito, Yasushi; Shapiro, Marc (2005). "Optimistic replication". *[ACM Computing Surveys](./ACM_Computing_Surveys)*. **37** (1): 42–81. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.324.3599](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.324.3599). [doi](./Doi_(identifier)):[10.1145/1057977.1057980](https://doi.org/10.1145%2F1057977.1057980). [S2CID](./S2CID_(identifier)) [1503367](https://api.semanticscholar.org/CorpusID:1503367). 
4. [↑](./Optimistic_replication#cite_ref-Gray1996_4-0) [Gray, J.](./Jim_Gray_(computer_scientist)); Helland, P.; [O’Neil, P.](./Patrick_O'Neil); [Shasha, D.](./Dennis_Shasha) (1996). [*The dangers of replication and a solution*](ftp://ftp.research.microsoft.com/pub/tr/tr-96-17.pdf) (PDF). Proceedings of the 1996 [ACM SIGMOD International Conference on Management of Data](./ACM_SIGMOD_International_Conference_on_Management_of_Data). pp. 173–182. [doi](./Doi_(identifier)):[10.1145/233269.233330](https://doi.org/10.1145%2F233269.233330).[*[permanent dead link](./Wikipedia:Link_rot)*]
5. [↑](./Optimistic_replication#cite_ref-Terry1995_5-0) Terry, D.B.; Theimer, M.M.; Petersen, K.; Demers, A.J.; Spreitzer, M.J.; Hauser, C.H. (1995). *Managing update conflicts in Bayou, a weakly connected replicated storage system*. Proceedings of the Fifteenth ACM Symposium on Operating Systems Principles. pp. 172–182. [doi](./Doi_(identifier)):[10.1145/224056.224070](https://doi.org/10.1145%2F224056.224070).
6. [↑](./Optimistic_replication#cite_ref-Kermarrec2001_6-0) Kermarrec, A.M.; Rowstron, A.; Shapiro, M.; Druschel, P. (2001). *The IceCube approach to the reconciliation of divergent replicas*. Proceedings of the Twentieth Annual ACM [Symposium on Principles of Distributed Computing](./Symposium_on_Principles_of_Distributed_Computing). pp. 210–218. [doi](./Doi_(identifier)):[10.1145/383962.384020](https://doi.org/10.1145%2F383962.384020).

 

## External links

 
- Saito, Yasushi; Shapiro, Marc (September 2003). ["Optimistic Replication"](https://www.microsoft.com/en-us/research/wp-content/uploads/2016/02/tr-2003-60.pdf) (PDF). Microsoft.