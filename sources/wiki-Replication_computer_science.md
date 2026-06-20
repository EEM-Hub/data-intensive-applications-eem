---
source: https://en.wikipedia.org/wiki/Replication_(computer_science)
fetched: 2026-06-19
---

Sharing information to ensure consistency in computing 
|  | This article includes a list ofgeneral references, butit lacks sufficient correspondinginline citations.Please help toimprovethis article byintroducingmore precise citations.(October 2012)(Learn how and when to remove this message) |
| --- | --- |

 

**Replication** in [computing](./Computing) refers to maintain multiple copies of data, processes, or resources to ensure consistency across redundant components. This fundamental technique spans [databases](./Database_management_system), [file systems](./File_system), and [distributed systems](./Distributed_computing), serving to improve [availability](./High_availability), [fault-tolerance](./Fault-tolerance), accessibility, and performance.[[1]](./Replication_(computing)#cite_note-kleppmann-1) Through replication, systems can continue operating when components fail ([failover](./Failover)), serve requests from geographically distributed locations, and balance load across multiple machines. The challenge lies in maintaining consistency between replicas while managing the fundamental tradeoffs between data consistency, system availability, and [network partition tolerance](./Network_partition) – constraints known as the [CAP theorem](./CAP_theorem).[[2]](./Replication_(computing)#cite_note-2)

 

## Terminology

 

Replication in computing can refer to:

 
- *Data replication*, where the same data is stored on multiple [storage devices](./Data_storage_device)
- *Computation replication*, where the same computing task is executed many times.  Computational tasks may be:

- *Replicated in space*, where tasks are executed on separate devices
- *Replicated in time*, where tasks are executed repeatedly on a single device

 

Replication in space or in time is often linked to scheduling algorithms.[[3]](./Replication_(computing)#cite_note-3)

 

Access to a replicated entity is typically uniform with access to a single non-replicated entity. The replication itself should be [transparent](./Transparency_(human-computer_interaction)) to an external user. In a failure scenario, a [failover](./Failover) of replicas should be hidden as much as possible with respect to [quality of service](./Quality_of_service).[[4]](./Replication_(computing)#cite_note-4)

 

Computer scientists further describe replication as being either:

 
- **Active replication**, which is performed by processing the same request at every replica
- **Passive replication**, which involves processing every request on a single replica and transferring the result to the other replicas

 

When one leader replica is designated via [leader election](./Leader_election) to process all the requests, the system is using a primary-backup or [primary-replica](./Master-slave_(computers)) scheme, which is predominant in [high-availability clusters](./High-availability_cluster). In comparison, if any replica can process a request and distribute a new state, the system is using a multi-primary or [multi-master](./Multi-master_replication) scheme. In the latter case, some form of [distributed concurrency control](./Distributed_concurrency_control) must be used, such as a [distributed lock manager](./Distributed_lock_manager).

 

[Load balancing](./Load_balancing_(computing)) differs from task replication, since it distributes a load of different computations across machines, and allows a single computation to be dropped in case of failure. Load balancing, however, sometimes uses data replication (especially [multi-master replication](./Multi-master_replication)) internally, to distribute its data among machines.

 

[Backup](./Backup) differs from replication in that the saved copy of data remains unchanged for a long period of time.[[5]](./Replication_(computing)#cite_note-5) Replicas, on the other hand, undergo frequent updates and quickly lose any historical state. Replication is one of the oldest and most important topics in the overall area of [distributed systems](./Distributed_computing).

 

Data replication and computation replication both require processes to handle incoming events. Processes for data replication are passive and operate only to maintain the stored data, reply to read requests and apply updates. Computation replication is usually performed to provide fault-tolerance, and take over an operation if one component fails. In both cases, the underlying needs are to ensure that the replicas see the same events in equivalent orders, so that they stay in consistent states and any replica can respond to queries.

 

### Replication models in distributed systems

 

Three widely cited models exist for data replication, each having its own properties and performance:

 
- **Transactional replication**: used for replicating [transactional data](./Transactional_data), such as a database. The [one-copy serializability](./One-copy_serializability) model is employed, which defines valid outcomes of a transaction on replicated data in accordance with the overall [ACID](./ACID) (atomicity, consistency, isolation, durability) properties that transactional systems seek to guarantee.
- **[State machine replication](./State_machine_replication)**: assumes that the replicated process is a [deterministic finite automaton](./Deterministic_finite_automaton) and that [atomic broadcast](./Atomic_broadcast) of every event is possible. It is based on [distributed consensus](./Consensus_(computer_science)) and has a great deal in common with the transactional replication model. This is sometimes mistakenly used as a synonym of active replication. State machine replication is usually implemented by a replicated log consisting of multiple subsequent rounds of the [Paxos algorithm](./Paxos_algorithm). This was popularized by Google's Chubby system, and is the core behind the open-source [Keyspace data store](./Keyspace_(data_store)).[[6]](./Replication_(computing)#cite_note-keyspace-6)[[7]](./Replication_(computing)#cite_note-chubby-7)
- **[Virtual synchrony](./Virtual_synchrony)**: involves a group of processes which cooperate to replicate in-memory data or to coordinate actions. The model defines a distributed entity called a *process group*. A process can join a group and is provided with a checkpoint containing the current state of the data replicated by group members. Processes can then send [multicasts](./Multicast) to the group and will see incoming multicasts in the identical order. Membership changes are handled as a special multicast that delivers a new "membership view" to the processes in the group.[[8]](./Replication_(computing)#cite_note-8)

 

## Database replication

 

[Database](./Database) replication involves maintaining copies of the same data on multiple machines, typically implemented through three main approaches: single-leader, multi-leader, and leaderless replication.[[1]](./Replication_(computing)#cite_note-kleppmann-1)

 

In [single-leader](./Master–slave_(technology)) (also called primary/replica) replication, one database instance is designated as the leader (primary), which handles all write operations. The leader logs these updates, which then propagate to replica nodes. Each replica acknowledges receipt of updates, enabling subsequent write operations. Replicas primarily serve read requests, though they may serve stale data due to replication lag – the delay in propagating changes from the leader.

 

In [multi-master replication](./Multi-master_replication) (also called multi-leader), updates can be submitted to any database node, which then propagate to other servers. This approach is particularly beneficial in multi-data center deployments, where it enables local write processing while masking inter-data center network latency.[[1]](./Replication_(computing)#cite_note-kleppmann-1) However, it introduces substantially increased costs and complexity which may make it impractical in some situations. The most common challenge that exists in multi-master replication is transactional conflict prevention or [resolution](./Conflict_resolution) when concurrent modifications occur on different leader nodes.

 

Most synchronous (or eager) replication solutions perform conflict prevention, while asynchronous (or lazy) solutions have to perform conflict resolution. For instance, if the same record is changed on two nodes simultaneously, an eager replication system would detect the conflict before confirming the commit and abort one of the transactions. A [lazy replication](./Lazy_replication) system would allow both [transactions](./Database_transaction) to commit and run a conflict resolution during re-synchronization. Conflict resolution methods can include techniques like last-write-wins, application-specific logic, or merging concurrent updates.[[1]](./Replication_(computing)#cite_note-kleppmann-1)

 

However, replication transparency can not always be achieved. When data is replicated in a database, they will be constrained by [CAP theorem](./CAP_theorem) or [PACELC theorem](./PACELC_theorem). In the [NoSQL](./NoSQL) movement, data consistency is usually sacrificed in exchange for other more desired properties, such as availability (A), partition tolerance (P), etc. Various [data consistency models](./Consistency_model) have also been developed to serve as Service Level Agreement (SLA) between service providers and the users.

 

There are several techniques for replicating data changes between nodes:[[1]](./Replication_(computing)#cite_note-kleppmann-1)

 
- **Statement-based replication**: Write requests (such as SQL statements) are logged and transmitted to replicas for execution. This can be problematic with non-deterministic functions or statements having side effects.
- **[Write-ahead log](./Write-ahead_logging) (WAL) shipping**: The storage engine's low-level write-ahead log is replicated, ensuring identical data structures across nodes.
- **Logical (row-based) replication**: Changes are described at the row level using a dedicated log format, providing greater flexibility and independence from storage engine internals.

 

## Disk storage replication

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/a/ad/Storage_replication-en.svg/250px-Storage_replication-en.svg.png)](./File:Storage_replication-en.svg)Storage replication 

Active (real-time) storage replication is usually implemented by distributing updates of a [block device](./Block_device) to several physical [hard disks](./Hard_disk). This way, any [file system](./File_system) supported by the [operating system](./Operating_system) can be replicated without modification, as the file system code works on a level above the block device driver layer. It is implemented either in hardware (in a [disk array controller](./Disk_array_controller)) or in software (in a [device driver](./Device_driver)).

 

The most basic method is [disk mirroring](./Disk_mirroring), which is typical for locally connected disks. The storage industry narrows the definitions, so *mirroring* is a local (short-distance) operation. A replication is extendable across a [computer network](./Computer_network), so that the disks can be located in physically distant locations, and the primary/replica database replication model is usually applied. The purpose of replication is to prevent damage from failures or [disasters](./Disaster_Recovery) that may occur in one location – or in case such events do occur, to improve the ability to recover data. For replication, latency is the key factor because it determines either how far apart the sites can be or the type of replication that can be employed.

 

The main characteristic of such cross-site replication is how write operations are handled, through either asynchronous or synchronous replication; synchronous replication needs to wait for the destination server's response in any write operation whereas asynchronous replication does not.

 

[Synchronous](./Synchronization) replication guarantees "zero [data loss](./Data_loss)" by the means of [atomic](./Atomic_operation) write operations, where the write operation is not considered complete until acknowledged by both the local and remote storage. Most applications wait for a write transaction to complete before proceeding with further work, hence overall performance decreases considerably. Inherently, performance drops proportionally to distance, as minimum [latency](./Latency_(engineering)) is dictated by the [speed of light](./Speed_of_light). For 10 km distance, the fastest possible roundtrip takes 67 μs, whereas an entire local cached write completes in about 10–20 μs.

 

In [asynchronous](./Asynchronous_I/O) replication, the write operation is considered complete as soon as local storage acknowledges it. Remote storage is updated with a small [lag](./Latency_(engineering)). Performance is greatly increased, but in case of a local storage failure, the remote storage is not guaranteed to have the current copy of data (the most recent data may be lost).

 

Semi-synchronous replication typically considers a write operation complete when acknowledged by local storage and received or logged by the remote server. The actual remote write is performed asynchronously, resulting in better performance but remote storage will lag behind the local storage, so that there is no guarantee of durability (i.e., seamless transparency) in the case of local storage failure.[*[citation needed](./Wikipedia:Citation_needed)*]

 

Point-in-time replication produces periodic [snapshots](./Snapshot_(computer_storage)) which are replicated instead of primary storage. This is intended to replicate only the changed data instead of the entire volume. As less information is replicated using this method, replication can occur over less-expensive bandwidth links such as [iSCSI](./ISCSI) or T1 instead of fiberoptic lines.

 

### Implementations

 Main articles: [distributed fault-tolerant file systems](./Distributed_fault-tolerant_file_systems) and [distributed parallel fault-tolerant file systems](./Distributed_parallel_fault-tolerant_file_systems) 

Many [distributed filesystems](./Distributed_filesystem) use replication to ensure fault tolerance and avoid a single point of failure.

 

Many commercial synchronous replication systems do not freeze when the remote replica fails or loses connection – behaviour which guarantees zero data loss – but proceed to operate locally, losing the desired zero [recovery point objective](./Recovery_point_objective).

 

Techniques of [wide-area network (WAN) optimization](./WAN_optimization) can be applied to address the limits imposed by latency.

 

## File-based replication

 

File-based replication conducts data replication at the logical level (i.e., individual data files) rather than at the storage block level. There are many different ways of performing this, which almost exclusively rely on software.

 

### Capture with a kernel driver

 

A [kernel driver](./Kernel_driver) (specifically a [filter driver](./Filter_driver)) can be used to intercept calls to the filesystem functions, capturing any activity as it occurs. This uses the same type of technology that real-time active virus checkers employ. At this level, logical file operations are captured like file open, write, delete, etc. The kernel driver transmits these commands to another process, generally over a network to a different machine, which will mimic the operations of the source machine. Like block-level storage replication, the file-level replication allows both synchronous and asynchronous modes. In synchronous mode, write operations on the source machine are held and not allowed to occur until the destination machine has acknowledged the successful replication. Synchronous mode is less common with file replication products although a few solutions exist.

 

File-level replication solutions allow for informed decisions about replication based on the location and type of the file. For example, temporary files or parts of a filesystem that hold no business value could be excluded. The data transmitted can also be more granular; if an application writes 100 bytes, only the 100 bytes are transmitted instead of a complete disk block (generally 4,096 bytes). This substantially reduces the amount of data sent from the source machine and the storage burden on the destination machine.

 

Drawbacks of this software-only solution include the requirement for implementation and maintenance on the operating system level, and an increased burden on the machine's processing power.

 

#### File system journal replication

 

Similarly to database [transaction logs](./Transaction_log), many [file systems](./File_system) have the ability to [journal](./Journaling_file_system) their activity. The journal can be sent to another machine, either periodically or in real time by streaming. On the replica side, the journal can be used to play back file system modifications.

 

One of the notable implementations is [Microsoft](./Microsoft)'s [System Center Data Protection Manager](./System_Center_Data_Protection_Manager) (DPM), released in 2005, which performs periodic updates but does not offer real-time replication.[*[citation needed](./Wikipedia:Citation_needed)*]

 

### Batch replication

 

This is the process of comparing the source and destination file systems and ensuring that the destination matches the source. The key benefit is that such solutions are generally free or inexpensive. The downside is that the process of synchronizing them is quite system-intensive, and consequently this process generally runs infrequently.

 

One of the notable implementations is [rsync](./Rsync).

 

## Replication within file

 

In a [paging](./Paging) operating system, pages in a paging file are sometimes replicated within a track to reduce rotational latency.

 

In [IBM](./IBM)'s [VSAM](./VSAM), index data are sometimes replicated within a track to reduce rotational latency.

 

## Distributed shared memory replication

 
|  | This sectionneeds expansion. You can help byadding missing information.(November 2018) |
| --- | --- |

 

Another example of using replication appears in [distributed shared memory](./Distributed_shared_memory) systems, where many nodes of the system share the same [page](./Page_(computer_memory)) of memory. This usually means that each node has a separate copy (replica) of a specific page.

 

## Primary-backup and multi-primary replication

 

Many classical approaches to replication are based on a primary-backup model where one device or process has unilateral control over one or more other processes or devices. For example, the primary might perform some computation, streaming a log of updates to a backup (standby) process, which can then take over if the primary fails. This approach is common for replicating databases, despite the risk that if a portion of the log is lost during a failure, the backup might not be in a state identical to the primary, and transactions could then be lost.

 

A weakness of primary-backup schemes is that only one is actually performing operations. Fault-tolerance is gained, but the identical backup system doubles the costs. For this reason, starting c. 1985, the distributed systems research community began to explore alternative methods of replicating data. An outgrowth of this work was the emergence of schemes in which a group of replicas could cooperate, with each process acting as a backup while also handling a share of the workload.

 

Computer scientist [Jim Gray](./Jim_Gray_(computer_scientist)) analyzed multi-primary replication schemes under the transactional model and published a widely cited paper skeptical of the approach "The Dangers of Replication and a Solution".[[9]](./Replication_(computing)#cite_note-9)[[10]](./Replication_(computing)#cite_note-10) He argued that unless the data splits in some natural way so that the database can be treated as *n* disjoint sub-databases, concurrency control conflicts will result in seriously degraded performance and the group of replicas will probably slow as a function of *n*. Gray suggested that the most common approaches are likely to result in degradation that scales as *O(n³)*.  His solution, which is to partition the data, is only viable in situations where data actually has a natural partitioning key.

 

In the 1985–1987, the [virtual synchrony](./Virtual_synchrony) model was proposed and emerged as a widely adopted standard (it was used in the Isis Toolkit, Horus, Transis, Ensemble, Totem, [Spread](./Spread_Toolkit), C-Ensemble, Phoenix and Quicksilver systems, and is the basis for the [CORBA](./Common_Object_Request_Broker_Architecture) fault-tolerant computing standard). Virtual synchrony permits a multi-primary approach in which a group of processes cooperates to parallelize some aspects of request processing. The scheme can only be used for some forms of in-memory data, but can provide linear speedups in the size of the group.

 

A number of modern products support similar schemes. For example, the Spread Toolkit supports this same virtual synchrony model and can be used to implement a multi-primary replication scheme; it would also be possible to use C-Ensemble or Quicksilver in this manner. [WANdisco](./WANdisco) permits active replication where every node on a network is an exact copy or replica and hence every node on the network is active at one time; this scheme is optimized for use in a [wide area network](./Wide_area_network) (WAN).

 

Modern multi-primary replication protocols optimize for the common failure-free operation. Chain replication[[11]](./Replication_(computing)#cite_note-11) is a  popular family of such protocols. State-of-the-art protocol variants[[12]](./Replication_(computing)#cite_note-12) of chain replication offer high throughput and strong consistency by arranging replicas in a chain for writes. This approach enables local reads on all replica nodes but has high latency for writes that must traverse multiple nodes sequentially.

 

A more recent multi-primary protocol, [Hermes](https://hermes-protocol.com/),[[13]](./Replication_(computing)#cite_note-13) combines cache-coherent-inspired invalidations and logical timestamps to achieve strong consistency with local reads and high-performance writes from all replicas. During fault-free operation, its broadcast-based writes are non-conflicting and commit after just one multicast round-trip to replica nodes. This design results in high throughput and low latency for both reads and writes.

 

## See also

 
- [Change data capture](./Change_data_capture)
- [Fault-tolerant computer system](./Fault-tolerant_computer_system)
- [Log shipping](./Log_shipping)
- [Multi-master replication](./Multi-master_replication)
- [Optimistic replication](./Optimistic_replication)
- [Shard (data)](./Shard_(data))
- [State machine replication](./State_machine_replication)
- [Virtual synchrony](./Virtual_synchrony)

 

## References

 
1. [1](./Replication_(computing)#cite_ref-kleppmann_1-0) [2](./Replication_(computing)#cite_ref-kleppmann_1-1) [3](./Replication_(computing)#cite_ref-kleppmann_1-2) [4](./Replication_(computing)#cite_ref-kleppmann_1-3) [5](./Replication_(computing)#cite_ref-kleppmann_1-4) Kleppmann, Martin (2017). *Designing Data-Intensive Applications: The Big Ideas Behind Reliable, Scalable, and Maintainable Systems*. O'Reilly Media. pp. 151–185. [ISBN](./ISBN_(identifier)) [9781491903100](./Special:BookSources/9781491903100).
2. [↑](./Replication_(computing)#cite_ref-2) Brewer, Eric A. (2000). "Towards robust distributed systems (Abstract)". *Proceedings of the nineteenth annual ACM symposium on Principles of distributed computing*. p. 7. [doi](./Doi_(identifier)):[10.1145/343477.343502](https://doi.org/10.1145%2F343477.343502). [ISBN](./ISBN_(identifier)) [1-58113-183-6](./Special:BookSources/1-58113-183-6).
3. [↑](./Replication_(computing)#cite_ref-3) Mansouri, Najme, Gholam, Hosein Dastghaibyfard, and Ehsan Mansouri. "Combination of data replication and scheduling algorithm for improving data availability in Data Grids", *Journal of Network and Computer Applications* (2013)
4. [↑](./Replication_(computing)#cite_ref-4) V. Andronikou, K. Mamouras, K. Izan, D. Kyriazis, T. Varvarigou, "Dynamic QoS-aware Data Replication in Grid Environments", *Elsevier Future Generation Computer Systems - The International Journal of Grid Computing and eScience*, 2012
5. [↑](./Replication_(computing)#cite_ref-5) ["Backup and Replication: What is the Difference?"](https://www.zerto.com/replication/backup-and-replication-what-is-the-difference/). *Zerto*. February 6, 2012.
6. [↑](./Replication_(computing)#cite_ref-keyspace_6-0) Marton Trencseni, Attila Gazso (2009). ["Keyspace: A Consistently Replicated, Highly-Available Key-Value Store"](http://scalien.com/whitepapers). Retrieved 2010-04-18.
7. [↑](./Replication_(computing)#cite_ref-chubby_7-0) Mike Burrows (2006). ["The Chubby Lock Service for Loosely-Coupled Distributed Systems"](https://web.archive.org/web/20100209225931/http://labs.google.com/papers/chubby.html). Archived from [the original](http://labs.google.com/papers/chubby.html) on 2010-02-09. Retrieved 2010-04-18.
8. [↑](./Replication_(computing)#cite_ref-8) Birman, K.; Joseph, T. (1987-11-01). ["Exploiting virtual synchrony in distributed systems"](https://doi.org/10.1145/41457.37515). *Proceedings of the eleventh ACM Symposium on Operating systems principles - SOSP '87*. New York, NY, USA: Association for Computing Machinery. pp. 123–138. [doi](./Doi_(identifier)):[10.1145/41457.37515](https://doi.org/10.1145%2F41457.37515). [ISBN](./ISBN_(identifier)) [978-0-89791-242-6](./Special:BookSources/978-0-89791-242-6). [S2CID](./S2CID_(identifier)) [7739589](https://api.semanticscholar.org/CorpusID:7739589).
9. [↑](./Replication_(computing)#cite_ref-9) ["The Dangers of Replication and a Solution"](http://research.microsoft.com/~gray/replicas.ps)
10. [↑](./Replication_(computing)#cite_ref-10) *Proceedings of the 1999 ACM SIGMOD International Conference on Management of Data: SIGMOD '99*, Philadelphia, PA, US; June 1–3, 1999, Volume 28; p. 3.
11. [↑](./Replication_(computing)#cite_ref-11) van Renesse, Robbert; Schneider, Fred B. (2004-12-06). ["Chain replication for supporting high throughput and availability"](https://dl.acm.org/doi/abs/10.5555/1251254.1251261). *Proceedings of the 6th Conference on Symposium on Operating Systems Design & Implementation - Volume 6*. OSDI'04. USA: USENIX Association: 7.
12. [↑](./Replication_(computing)#cite_ref-12) Terrace, Jeff; Freedman, Michael J. (2009-06-14). ["Object storage on CRAQ: high-throughput chain replication for read-mostly workloads"](https://dl.acm.org/doi/abs/10.5555/1855807.1855818). *USENIX Annual Technical Conference*. USENIX'09. USA: 11.
13. [↑](./Replication_(computing)#cite_ref-13) Katsarakis, Antonios; Gavrielatos, Vasilis; Katebzadeh, M.R. Siavash; Joshi, Arpit; Dragojevic, Aleksandar; Grot, Boris; Nagarajan, Vijay (2020-03-13). ["Hermes: A Fast, Fault-Tolerant and Linearizable Replication Protocol"](https://doi.org/10.1145/3373376.3378496). [*Proceedings of the Twenty-Fifth International Conference on Architectural Support for Programming Languages and Operating Systems*](https://www.pure.ed.ac.uk/ws/files/130434070/Hermes_a_Fast_KATASARAKIS_DOA02122019_AFV.pdf) (PDF). ASPLOS '20. New York, NY, USA: Association for Computing Machinery. pp. 201–217. [doi](./Doi_(identifier)):[10.1145/3373376.3378496](https://doi.org/10.1145%2F3373376.3378496). [hdl](./Hdl_(identifier)):[20.500.11820/c8bd74e1-5612-4b81-87fe-175c1823d693](https://hdl.handle.net/20.500.11820%2Fc8bd74e1-5612-4b81-87fe-175c1823d693). [ISBN](./ISBN_(identifier)) [978-1-4503-7102-5](./Special:BookSources/978-1-4503-7102-5). [S2CID](./S2CID_(identifier)) [210921224](https://api.semanticscholar.org/CorpusID:210921224).

 
| Authority control databases | GND |
| --- | --- |