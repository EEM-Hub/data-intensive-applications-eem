---
source: https://en.wikipedia.org/wiki/Raft_(algorithm)
fetched: 2026-06-19
---

Consensus algorithm 
| The Raft consensus algorithm mascot. |
| --- |
| Class | Consensus algorithm |

 

**Raft** is a [consensus](./Consensus_(computer_science)) algorithm designed as an alternative to the [Paxos](./Paxos_(computer_science)) family of algorithms. It was meant to be more understandable than Paxos by means of separation of logic, but it is also formally proven safe and offers some additional features.[[1]](./Raft_(algorithm)#cite_note-paper-1) Raft offers a generic way to distribute a [state machine](./Finite-state_machine) across a [cluster](./Computer_cluster) of computing systems, ensuring that each node in the cluster agrees upon the same series of state transitions. It has a number of open-source reference implementations, with full-specification implementations in [Go](./Go_(programming_language)), [C++](./C++), [Java](./Java_(programming_language)), [JavaScript](./JavaScript), and [Scala](./Scala_(programming_language)).[[2]](./Raft_(algorithm)#cite_note-website-2) It is named after Reliable, Replicated, Redundant, And Fault-Tolerant.[[3]](./Raft_(algorithm)#cite_note-3)

 

Raft is not [Byzantine fault tolerant](./Byzantine_fault); the nodes trust the elected leader, and the algorithm assumes all participants are trustworthy.

 

## Basics

 

Raft achieves consensus via an elected leader. A server in a raft cluster is either a *leader* or a *follower*, and can be a *candidate* in the precise case of an election (leader unavailable). The leader is responsible for log replication to the followers. It regularly informs the followers of its existence by sending a heartbeat message. Each follower has a timeout (typically between 150 and 300 ms) in which it expects the heartbeat from the leader. The timeout is reset on receiving the heartbeat. If no heartbeat is received the follower changes its status to candidate and starts a [leader election](./Leader_election).[[1]](./Raft_(algorithm)#cite_note-paper-1)[[4]](./Raft_(algorithm)#cite_note-secretlives-4)

 

### Approach of the consensus problem in Raft

 

Raft implements consensus by a leader approach. The cluster has one and only one elected leader which is fully responsible for managing log replication on the other servers of the cluster. It means that the leader can decide on new entries' placement and establishment of data flow between it and the other servers without consulting other servers. A leader leads until it fails or disconnects, in which case surviving servers elect a new leader.

 

The consensus problem is decomposed in Raft into two relatively independent subproblems listed down below.

 

#### Leader election

 

When the existing leader fails or when the algorithm initializes, a new leader needs to be elected.

 

In this case, a new *term* starts in the cluster. A term is an arbitrary period of time on the server for which a new leader needs to be elected. Each term starts with a leader election. If the election is completed successfully (i.e. a single leader is elected) the term keeps going with normal operations orchestrated by the new leader. If the election is a failure, a new term starts, with a new election.

 

A leader election is started by a *candidate* server. A server becomes a candidate if it receives no communication by the leader over a period called the *election timeout*, so it assumes there is no acting leader anymore. It starts the election by increasing the term counter, voting for itself as new leader, and sending a message to all other servers requesting their vote. A server will vote only once per term, on a first-come-first-served basis. If a candidate receives a message from another server with a term number larger than the candidate's current term, then the candidate's election is defeated and the candidate changes into a follower and recognizes the leader as legitimate. If a candidate receives a majority of votes, then it becomes the new leader. If neither happens, e.g., because of a split vote, then a new term starts, and a new election begins.[[1]](./Raft_(algorithm)#cite_note-paper-1)

 

Raft uses a randomized election timeout to ensure that split vote problems are resolved quickly. This should reduce the chance of a split vote because servers won't become candidates at the same time: a single server will time out, win the election, then become leader and send heartbeat messages to other servers before any of the followers can become candidates.[[1]](./Raft_(algorithm)#cite_note-paper-1)

 

#### Log replication

 

The leader is responsible for the log replication. It accepts client requests. Each client request consists of a command to be executed by the replicated state machines in the cluster. After being appended to the leader's log as a new entry, each of the requests is forwarded to the followers as AppendEntries messages. In case of unavailability of the followers, the leader retries AppendEntries messages indefinitely, until the log entry is eventually stored by all of the followers.

 

Once the leader receives confirmation from half or more of its followers that the entry has been replicated, the leader applies the entry to its local state machine, and the request is considered *committed*.[[1]](./Raft_(algorithm)#cite_note-paper-1)[[4]](./Raft_(algorithm)#cite_note-secretlives-4) This event also commits all previous entries in the leader's log. Once a follower learns that a log entry is committed, it applies the entry to its local state machine. This ensures consistency of the logs between all the servers through the cluster, ensuring that the safety rule of Log Matching is respected.

 

In the case of a leader crash, the logs can be left inconsistent, with some logs from the old leader not being fully replicated through the cluster. The new leader will then handle inconsistency by forcing the followers to duplicate its own log. To do so, for each of its followers, the leader will compare its log with the log from the follower, find the last entry where they agree, then delete all the entries coming after this critical entry in the follower log and replace it with its own log entries. This mechanism will restore log consistency in a cluster subject to failures.

 

### Safety

 

#### Safety rules in Raft

 

Raft guarantees each of these safety properties:

 
- **Election safety:** at most one leader can be elected in a given term.
- **Leader append-only:** a leader can only append new entries to its logs (it can neither overwrite nor delete entries).
- **Log matching:** if two logs contain an entry with the same index and term, then the logs are identical in all entries up through the given index.
- **Leader completeness:** if a log entry is committed in a given term then it will be present in the logs of the leaders since this term.
- **State machine safety:** if a server has applied a particular log entry to its state machine, then no other server may apply a different command for the same log.

 

The first four rules are guaranteed by the details of the algorithm described in the previous section. The State Machine Safety is guaranteed by a restriction on the election process.

 

#### State machine safety

 

This rule is ensured by a simple restriction: a candidate can't win an election unless its log contains all committed entries. In order to be elected, a candidate has to contact a majority of the cluster, and given the rules for logs to be committed, it means that every committed entry is going to be present on at least one of the servers the candidates contact.

 

Raft determines which of two logs (carried by two distinct servers) is more up-to-date by comparing the index term of the last entries in the logs. If the logs have a last entry with different terms, then the log with the later term is more up-to-date. If the logs end with the same term, then whichever log is longer is more up-to-date.

 

In Raft, the request from a candidate to a voter includes information about the candidate's log. If its own log is more up-to-date than the candidate's log, the voter denies its vote to the candidate. This implementation ensures the State Machine Safety rule.

 

#### Follower crashes

 

If a follower crashes, *AppendEntries* and *vote* requests sent by other servers will fail.  Such failures are handled by the servers trying indefinitely to reach the downed follower. If the follower restarts, the pending requests will complete. If the request has already been taken into account before the failure, the restarted follower will just ignore it.

 

#### Timing and availability

 

Timing is critical in Raft to elect and maintain a steady leader over time, in order to have a perfect availability of the cluster. Stability is ensured by respecting the *timing requirement* of the algorithm:

 

*broadcastTime << electionTimeout << MTBF*

 
- *broadcastTime* is the average time it takes a server to send a request to every server in the cluster and receive responses. It is relative to the infrastructure used.
- *MTBF (Mean Time Between Failures)* is the average time between failures for a server. It is also relative to the infrastructure.
- *electionTimeout* is the same as described in the Leader Election section. It is something the programmer must choose.

 

Typical numbers for these values can be 0.5 ms to 20 ms for *broadcastTime*, which implies that the programmer sets the *electionTimeout* somewhere between 10 ms and 500 ms. It can take several weeks or months between single server failures, which means the values are sufficient for a stable cluster.

 

### Cluster Membership Changes

 

To address cluster membership change issues that can arise in Raft, the algorithm introduces joint consensus, a transitional configuration phase. Joint consensus works as follows:[[5]](./Raft_(algorithm)#cite_note-:0-5)

 

Given server configuration Cold, the old server configuration, and Cnew, the new configuration:[[5]](./Raft_(algorithm)#cite_note-:0-5)

 
- Log entries are committed to every server in Cold and Cnew.[[5]](./Raft_(algorithm)#cite_note-:0-5)
- Any server from Cold and Cnew can be leader.[[5]](./Raft_(algorithm)#cite_note-:0-5)
- Agreement for elections and log entry commits requires majorities from both Cold and Cnew.[[5]](./Raft_(algorithm)#cite_note-:0-5)

 

Once the joint consensus is done (that is, the special Cnew configuration entry is replicated to a majority of Cnew servers' logs), the system fully transitions to the new configuration.[[5]](./Raft_(algorithm)#cite_note-:0-5)

 

However, there are three issues that arise with this new configuration, of which Raft addresses:[[6]](./Raft_(algorithm)#cite_note-:02-6)

 
1. New servers with no log entries. Raft introduces a phase before the configuration change where servers with no log entries are not considered part of the majority in elections, but they will have entries replicated to them. This happens until the server is fully caught up with entries.[[6]](./Raft_(algorithm)#cite_note-:02-6)
2. Cluster leader isn't in Cnew. The cluster leader will stop being leader and return to follower state. Specifically, it will continue to replicate log entries, but will not count itself as majorities.[[6]](./Raft_(algorithm)#cite_note-:02-6)
3. Disruptions from servers in Cold. If a server believes that a current leader exists, any RequestVote RPCs (RPCs to gather votes for a leader election) will be disregarded.[[6]](./Raft_(algorithm)#cite_note-:02-6)

 

### Log Compaction

 

An extension to Raft is log compaction, where each server takes snapshots of its committed entries and saves it to [stable storage](./Stable_storage), along with the index of its last entry and the term in the snapshotted log. The leader occasionally sends its snapshots to servers that are lagging behind in its log. When the server receives this snapshot, it will either discard its entire log if it's superseded by the snapshot, or only the entries up to the latest one in the snapshot.[[7]](./Raft_(algorithm)#cite_note-:03-7)

 

### Issues

 

While Raft aims to be an alternative of Paxos and more understandable than Paxos, several issues arise.

 

#### Leader Bottleneck

 

Raft uses a single leader model, where client requests, reads and writes, and log replications goes through a single leader. This means that there is a [single point of failure](./Single_point_of_failure) and a bottleneck in performance. Furthermore, it does not scale with increasing server workload.[[8]](./Raft_(algorithm)#cite_note-8)

 

#### Reconfiguration

 

Raft's membership change system has not been formally verified to be correct. This means that implementing it is very risky, as there can be many potential bugs and errors. Diego Ongaro, one of the co-authors, has tried to create a formal safety proof, but there are no plans to continue developing it due to how complicated it is.[[9]](./Raft_(algorithm)#cite_note-:1-9) In 2014, a safety bug was found relating to single server membership changes.[[9]](./Raft_(algorithm)#cite_note-:1-9)

 

#### Byzantine Faults

 

Raft, like other consensus algorithms, ensures that there can never be an incorrect result under all non-Byzantine conditions.[[10]](./Raft_(algorithm)#cite_note-:04-10) This means that Raft is not a Byzantine fault tolerant algorithm. A 2023 study found that [blockchain systems](./Blockchain) based on Raft are vulnerable to Byzantine attacks because of the lack of authentication on the client side.[[11]](./Raft_(algorithm)#cite_note-11)

 

## Extensions

 

The dissertation “Consensus: Bridging Theory and Practice” by one of the co-authors of the original paper describes extensions to the original algorithm:[[12]](./Raft_(algorithm)#cite_note-12)

 
- Pre-Vote: when a member rejoins the cluster, it can depending on timing trigger an election although there is already a leader. To avoid this, pre-vote will first check in with the other members. Avoiding the unnecessary election improves the availability of cluster, therefore this extension is usually present in production implementations.
- Leadership transfer: a leader that is shutting down orderly can explicitly transfer the leadership to another member. This can be faster than waiting for a timeout. Also, a leader can step down when another member would be a better leader, for example when that member is on a faster machine.

 

## Production use of Raft

 
- [CockroachDB](./CockroachDB) uses Raft in the Replication Layer.[[13]](./Raft_(algorithm)#cite_note-13)
- [Etcd](./Etcd) uses Raft to manage a highly-available replicated log [[14]](./Raft_(algorithm)#cite_note-14)
- [Hazelcast](./Hazelcast) uses Raft to provide its CP Subsystem, a strongly consistent layer for distributed data structures. [[15]](./Raft_(algorithm)#cite_note-15)
- [IBM MQ](./IBM_MQ) uses Raft to manage a highly-available replicated log. [[16]](./Raft_(algorithm)#cite_note-16)
- [MongoDB](./MongoDB) uses a variant of Raft in the replication set.
- [Neo4j](./Neo4j) uses Raft to ensure consistency and safety. [[17]](./Raft_(algorithm)#cite_note-17)
- [RabbitMQ](./RabbitMQ) uses Raft to implement durable, replicated FIFO queues. [[18]](./Raft_(algorithm)#cite_note-18)
- [ScyllaDB](./ScyllaDB) uses Raft for metadata (schema and topology changes) [[19]](./Raft_(algorithm)#cite_note-19)
- [Splunk](./Splunk) Enterprise uses Raft in a Search Head Cluster (SHC) [[20]](./Raft_(algorithm)#cite_note-20)
- [TiDB](./TiDB) uses Raft with the storage engine TiKV.[[21]](./Raft_(algorithm)#cite_note-21)
- [YugabyteDB](./YugabyteDB) uses Raft in the DocDB Replication [[22]](./Raft_(algorithm)#cite_note-22)
- [ClickHouse](./ClickHouse) uses Raft for in-house implementation of [ZooKeeper](./ZooKeeper)-like service [[23]](./Raft_(algorithm)#cite_note-23)
- Redpanda uses the Raft consensus algorithm for data replication [[24]](./Raft_(algorithm)#cite_note-24)
- [Apache Kafka](./Apache_Kafka) Raft (KRaft) uses Raft for metadata management.[[25]](./Raft_(algorithm)#cite_note-25)
- [NATS Messaging](./NATS_Messaging) uses the Raft consensus algorithm for Jetstream cluster management and data replication [[26]](./Raft_(algorithm)#cite_note-26)
- [Camunda](./Camunda) uses the Raft consensus algorithm for data replication [[27]](./Raft_(algorithm)#cite_note-27)

 

## References

  
1. [1](./Raft_(algorithm)#cite_ref-paper_1-0) [2](./Raft_(algorithm)#cite_ref-paper_1-1) [3](./Raft_(algorithm)#cite_ref-paper_1-2) [4](./Raft_(algorithm)#cite_ref-paper_1-3) [5](./Raft_(algorithm)#cite_ref-paper_1-4) Ongaro, Diego; [Ousterhout, John](./John_Ousterhout) (2013). ["In Search of an Understandable Consensus Algorithm"](https://raft.github.io/raft.pdf) (PDF).
2. [↑](./Raft_(algorithm)#cite_ref-website_2-0) ["Raft Consensus Algorithm"](https://raft.github.io/). 2014.
3. [↑](./Raft_(algorithm)#cite_ref-3) [Why the "Raft" name?](https://groups.google.com/forum/#!topic/raft-dev/95rZqptGpmU)
4. [1](./Raft_(algorithm)#cite_ref-secretlives_4-0) [2](./Raft_(algorithm)#cite_ref-secretlives_4-1) Ben B. Johnson. ["Raft: Understandable Distributed Consensus"](http://thesecretlivesofdata.com/raft/). *The Secret Lives of Data website*. Retrieved August 4, 2021.
5. [1](./Raft_(algorithm)#cite_ref-:0_5-0) [2](./Raft_(algorithm)#cite_ref-:0_5-1) [3](./Raft_(algorithm)#cite_ref-:0_5-2) [4](./Raft_(algorithm)#cite_ref-:0_5-3) [5](./Raft_(algorithm)#cite_ref-:0_5-4) [6](./Raft_(algorithm)#cite_ref-:0_5-5) ["In Search of an Understandable Consensus Algorithm (Extended Version)"](https://raft.github.io/raft.pdf) (PDF). *raft.github.io*. Retrieved 2025-10-01.
6. [1](./Raft_(algorithm)#cite_ref-:02_6-0) [2](./Raft_(algorithm)#cite_ref-:02_6-1) [3](./Raft_(algorithm)#cite_ref-:02_6-2) [4](./Raft_(algorithm)#cite_ref-:02_6-3) ["In Search of an Understandable Consensus Algorithm (Extended Version)"](https://raft.github.io/raft.pdf) (PDF). *raft.github.io*. Retrieved 2025-10-01.
7. [↑](./Raft_(algorithm)#cite_ref-:03_7-0) ["In Search of an Understandable Consensus Algorithm (Extended Version)"](https://raft.github.io/raft.pdf) (PDF). *raft.github.io*. Retrieved 2025-10-01.
8. [↑](./Raft_(algorithm)#cite_ref-8) Deyerl, Christian; Distler, Tobias (2019-03-25). ["In Search of a Scalable Raft-based Replication Architecture"](https://doi.org/10.1145/3301419.3323968). *Proceedings of the 6th Workshop on Principles and Practice of Consistency for Distributed Data*. PaPoC '19. New York, NY, USA: Association for Computing Machinery. pp. 1–7. [doi](./Doi_(identifier)):[10.1145/3301419.3323968](https://doi.org/10.1145%2F3301419.3323968). [ISBN](./ISBN_(identifier)) [978-1-4503-6276-4](./Special:BookSources/978-1-4503-6276-4).
9. [1](./Raft_(algorithm)#cite_ref-:1_9-0) [2](./Raft_(algorithm)#cite_ref-:1_9-1) ["bug in single-server membership changes"](https://groups.google.com/g/raft-dev/c/t4xj6dJTP6E/m/d2D9LrWRza8J?pli=1). *groups.google.com*. Retrieved 2025-10-06.
10. [↑](./Raft_(algorithm)#cite_ref-:04_10-0) ["In Search of an Understandable Consensus Algorithm (Extended Version)"](https://raft.github.io/raft.pdf) (PDF). *raft.github.io*. Retrieved 2025-10-01.
11. [↑](./Raft_(algorithm)#cite_ref-11) ["Poster: Client-Side Byzantine Attacks on Raft Algorithm in Blockchain"](https://www.ndss-symposium.org/wp-content/uploads/2023/02/NDSS2023Poster_paper_9949.pdf) (PDF).
12. [↑](./Raft_(algorithm)#cite_ref-12) ["CONSENSUS: BRIDGING THEORY AND PRACTICE"](https://web.stanford.edu/~ouster/cgi-bin/papers/OngaroPhD.pdf) (PDF).
13. [↑](./Raft_(algorithm)#cite_ref-13) ["Replication Layer | CockroachDB Docs"](https://www.cockroachlabs.com/docs/stable/architecture/replication-layer.html). *www.cockroachlabs.com*. Retrieved 2022-06-21.
14. [↑](./Raft_(algorithm)#cite_ref-14) ["Raft README"](https://github.com/etcd-io/raft/blob/main/README.md). *github.com*. Retrieved 2022-08-25.
15. [↑](./Raft_(algorithm)#cite_ref-15) ["CP Subsystem"](https://docs.hazelcast.com/imdg/4.2/cp-subsystem/cp-subsystem). *docs.hazelcast.com*. Retrieved 2022-12-24.
16. [↑](./Raft_(algorithm)#cite_ref-16) ["Cloud native high availability with IBM MQ"](https://community.ibm.com/community/user/blogs/david-ware1/2021/03/23/native-ha-cloud-native-high-availability). *community.ibm.com*. 25 March 2021. Retrieved 2021-05-25.
17. [↑](./Raft_(algorithm)#cite_ref-17) ["Leadership, routing and load balancing - Operations Manual"](https://neo4j.com/docs/operations-manual/5/clustering/setup/routing/). *Neo4j Graph Data Platform*. Retrieved 2022-11-30.
18. [↑](./Raft_(algorithm)#cite_ref-18) ["Quorum Queues"](https://www.rabbitmq.com/quorum-queues.html). *RabbitMQ*. Retrieved 2022-12-14.
19. [↑](./Raft_(algorithm)#cite_ref-19) ["ScyllaDB's Path to Strong Consistency: A New Milestone"](https://www.scylladb.com/2023/05/04/scylladbs-path-to-strong-consistency-a-new-milestone/). 4 May 2023.
20. [↑](./Raft_(algorithm)#cite_ref-20) ["Handle Raft issues"](https://docs.splunk.com/Documentation/Splunk/9.0.0/DistSearch/Handleraftissues). *Splunk*. 2022-08-24. Retrieved 2022-08-24.
21. [↑](./Raft_(algorithm)#cite_ref-21) ["Raft and High Availability"](https://en.pingcap.com/blog/raft-and-high-availability/). *PingCAP*. 2021-09-01. Retrieved 2022-06-21.
22. [↑](./Raft_(algorithm)#cite_ref-22) ["Replication | YugabyteDB Docs"](https://docs.yugabyte.com/preview/architecture/docdb-replication/replication/). *www.yugabyte.com*. Retrieved 2022-08-19.
23. [↑](./Raft_(algorithm)#cite_ref-23) ["ClickHouse Keeper"](https://clickhouse.com/docs/en/guides/sre/keeper/clickhouse-keeper). *clickhouse.com*. Retrieved 2023-04-26.
24. [↑](./Raft_(algorithm)#cite_ref-24) ["Raft consensus algorithm"](https://docs.redpanda.com/docs/get-started/architecture/#raft-consensus-algorithm).
25. [↑](./Raft_(algorithm)#cite_ref-25) ["KRaft Overview | Confluent Documentation"](https://docs.confluent.io/platform/current/kafka-metadata/kraft.html). *docs.confluent.io*. Retrieved 2024-04-13.
26. [↑](./Raft_(algorithm)#cite_ref-26) ["JetStream Clustering"](https://docs.nats.io/running-a-nats-service/configuration/clustering/jetstream_clustering).
27. [↑](./Raft_(algorithm)#cite_ref-27) ["Raft consensus and replication protocol"](https://docs.camunda.io/docs/components/zeebe/technical-concepts/clustering/#raft-consensus-and-replication-protocol).

 

## External links

 
- [Official website](https://raft.github.io/) [![Edit this at Wikidata](//upload.wikimedia.org/wikipedia/en/thumb/8/8a/OOjs_UI_icon_edit-ltr-progressive.svg/20px-OOjs_UI_icon_edit-ltr-progressive.svg.png)](https://www.wikidata.org/wiki/Q17100313#P856)