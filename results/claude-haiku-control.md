# Exam Results: ddia.md

**Date:** 2026-06-22 14:51
**Model:** claude:haiku
**Score:** 42/42 (100%)

## Per-Question Results

- **Q1**: CORRECT — What is the key property of Bitcask's storage design?
- **Q2**: CORRECT — In a Log-Structured Merge-tree (LSM), what triggers a flush from the memtable to disk?
- **Q3**: CORRECT — What is the difference between size-tiered and leveled compaction strategies?
- **Q4**: CORRECT — What property distinguishes a B+ tree from a standard B-tree?
- **Q5**: CORRECT — Why does a B-tree storage engine use write-ahead logging?
- **Q6**: CORRECT — What does fsync guarantee that a normal write does not?
- **Q7**: CORRECT — What is the ARIES algorithm?
- **Q8**: CORRECT — How does shadow paging achieve atomicity without a WAL?
- **Q9**: CORRECT — What does a Bloom filter guarantee?
- **Q10**: CORRECT — How does a counting Bloom filter differ from a standard Bloom filter?
- **Q11**: CORRECT — What advantage does a cuckoo filter have over a standard Bloom filter?
- **Q12**: CORRECT — What is the primary use of a Merkle tree in distributed storage?
- **Q13**: CORRECT — What is the expected time complexity of search, insertion, and deletion in a skip list?
- **Q14**: CORRECT — What does the HyperLogLog algorithm estimate?
- **Q15**: CORRECT — In Apache Avro, how is schema evolution handled when a reader has a different schema than the writer?
- **Q16**: CORRECT — What type of error does a CRC (Cyclic Redundancy Check) detect?
- **Q17**: CORRECT — What property must a CRDT merge function satisfy to guarantee convergence?
- **Q18**: CORRECT — In a leaderless replication system, what condition on read (R) and write (W) quorums ensures strong consistency given N replicas?
- **Q19**: CORRECT — What is hinted handoff in a Dynamo-style system?
- **Q20**: CORRECT — What is the purpose of read repair in a distributed database?
- **Q21**: CORRECT — In the Raft consensus algorithm, what triggers a new leader election?
- **Q22**: CORRECT — What is the fundamental limitation of two-phase commit (2PC)?
- **Q23**: CORRECT — How does Practical Byzantine Fault Tolerance (PBFT) differ from crash-fault-tolerant consensus?
- **Q24**: CORRECT — What is the relationship between atomic broadcast and consensus?
- **Q25**: CORRECT — What does a Lamport timestamp provide?
- **Q26**: CORRECT — What can vector clocks detect that Lamport timestamps cannot?
- **Q27**: CORRECT — What property does consistent hashing provide when a node is added or removed?
- **Q28**: CORRECT — What problem do virtual nodes solve in consistent hashing?
- **Q29**: CORRECT — How does rendezvous hashing (HRW) differ from consistent hashing?
- **Q30**: CORRECT — How does a gossip protocol disseminate information through a cluster?
- **Q31**: CORRECT — What isolation anomaly does snapshot isolation permit that serializable isolation does not?
- **Q32**: CORRECT — How does MVCC (Multiversion Concurrency Control) avoid readers blocking writers?
- **Q33**: CORRECT — What does Serializable Snapshot Isolation (SSI) add on top of snapshot isolation?
- **Q34**: CORRECT — What is two-phase locking (2PL)?
- **Q35**: CORRECT — What is change data capture (CDC)?
- **Q36**: CORRECT — What is a materialized view?
- **Q37**: CORRECT — In MapReduce, what happens between the map and reduce phases?
- **Q38**: CORRECT — What ordering guarantee does Apache Kafka provide?
- **Q39**: CORRECT — In the CAP theorem, what must a distributed system sacrifice during a network partition?
- **Q40**: CORRECT — How does the PACELC theorem extend CAP?
- **Q41**: CORRECT — What does linearizability guarantee?
- **Q42**: CORRECT — What does the FLP impossibility result state?

## By Objective

- **Bitcask Storage Engine**: 1/1 (100%)
- **LSM Tree Flush**: 1/1 (100%)
- **Compaction Strategies**: 1/1 (100%)
- **B+ Tree**: 1/1 (100%)
- **Write-Ahead Logging**: 1/1 (100%)
- **fsync and Durability**: 1/1 (100%)
- **ARIES Recovery**: 1/1 (100%)
- **Shadow Paging**: 1/1 (100%)
- **Bloom Filter**: 1/1 (100%)
- **Counting Bloom Filter**: 1/1 (100%)
- **Cuckoo Filter**: 1/1 (100%)
- **Merkle Tree**: 1/1 (100%)
- **Skip List**: 1/1 (100%)
- **HyperLogLog**: 1/1 (100%)
- **Avro Schema Evolution**: 1/1 (100%)
- **CRC Error Detection**: 1/1 (100%)
- **CRDT Convergence**: 1/1 (100%)
- **Quorum Consistency**: 1/1 (100%)
- **Hinted Handoff**: 1/1 (100%)
- **Read Repair**: 1/1 (100%)
- **Raft Leader Election**: 1/1 (100%)
- **Two-Phase Commit**: 1/1 (100%)
- **PBFT**: 1/1 (100%)
- **Atomic Broadcast and Consensus**: 1/1 (100%)
- **Lamport Timestamps**: 1/1 (100%)
- **Vector Clocks**: 1/1 (100%)
- **Consistent Hashing**: 1/1 (100%)
- **Virtual Nodes**: 1/1 (100%)
- **Rendezvous Hashing**: 1/1 (100%)
- **Gossip Protocol**: 1/1 (100%)
- **Snapshot Isolation and Write Skew**: 1/1 (100%)
- **MVCC**: 1/1 (100%)
- **Serializable Snapshot Isolation**: 1/1 (100%)
- **Two-Phase Locking**: 1/1 (100%)
- **Change Data Capture**: 1/1 (100%)
- **Materialized View**: 1/1 (100%)
- **MapReduce Shuffle**: 1/1 (100%)
- **Kafka Ordering**: 1/1 (100%)
- **CAP Theorem**: 1/1 (100%)
- **PACELC Theorem**: 1/1 (100%)
- **Linearizability**: 1/1 (100%)
- **FLP Impossibility**: 1/1 (100%)
