# Data Intensive Applications Practice Questions

## Q1: What is the key property of Bitcask's storage design?
- a) All data is sorted on disk for range queries
- b) An append-only log with an in-memory hash table mapping every key to its disk offset
- c) A B-tree with write-ahead logging
- d) A columnar format optimized for analytical queries
Answer: b
Objective: Bitcask Storage Engine

## Q2: In a Log-Structured Merge-tree (LSM), what triggers a flush from the memtable to disk?
- a) A timer expires after a fixed interval
- b) A read request finds a cache miss
- c) The memtable reaches a configured size threshold
- d) The WAL file is rotated
Answer: c
Objective: LSM Tree Flush

## Q3: What is the difference between size-tiered and leveled compaction strategies?
- a) Size-tiered merges SSTables of similar size; leveled maintains sorted runs per level with bounded overlap
- b) Size-tiered sorts by key; leveled sorts by timestamp
- c) Size-tiered is for B-trees; leveled is for LSM trees
- d) There is no meaningful difference; they are aliases
Answer: a
Objective: Compaction Strategies

## Q4: What property distinguishes a B+ tree from a standard B-tree?
- a) B+ trees use binary search instead of linear scan
- b) B+ trees store data pointers only at leaf nodes, with leaves linked for range scans
- c) B+ trees do not require balanced height
- d) B+ trees support only point lookups, not range queries
Answer: b
Objective: B+ Tree

## Q5: Why does a B-tree storage engine use write-ahead logging?
- a) To compress data before writing to disk
- b) To provide atomicity and durability by recording changes before modifying data pages
- c) To support multi-threaded reads
- d) To eliminate the need for fsync
Answer: b
Objective: Write-Ahead Logging

## Q6: What does fsync guarantee that a normal write does not?
- a) Data is compressed before storage
- b) Data reaches stable storage rather than just the OS page cache
- c) Data is replicated to a remote server
- d) Data is encrypted before writing
Answer: b
Objective: fsync and Durability

## Q7: What is the ARIES algorithm?
- a) A consensus protocol for distributed transactions
- b) A canonical WAL-based crash recovery algorithm using redo and undo passes
- c) A compaction strategy for LSM trees
- d) A replication protocol for multi-leader setups
Answer: b
Objective: ARIES Recovery

## Q8: How does shadow paging achieve atomicity without a WAL?
- a) By writing to a copy of the page and atomically switching a pointer to the new version
- b) By locking all pages during a transaction
- c) By using checksums to detect partial writes
- d) By replicating every write to three disks
Answer: a
Objective: Shadow Paging

## Q9: What does a Bloom filter guarantee?
- a) No false positives, possible false negatives
- b) No false negatives, possible false positives
- c) Neither false positives nor false negatives
- d) Exact membership testing with O(1) space
Answer: b
Objective: Bloom Filter

## Q10: How does a counting Bloom filter differ from a standard Bloom filter?
- a) It uses a different hash function
- b) It replaces single bits with counters, enabling deletion of elements
- c) It eliminates false positives entirely
- d) It supports range queries on keys
Answer: b
Objective: Counting Bloom Filter

## Q11: What advantage does a cuckoo filter have over a standard Bloom filter?
- a) It uses less memory for the same false positive rate
- b) It supports deletion and often achieves better space efficiency at low false positive rates
- c) It guarantees zero false positives
- d) It supports ordered iteration over elements
Answer: b
Objective: Cuckoo Filter

## Q12: What is the primary use of a Merkle tree in distributed storage?
- a) Sorting data for range queries
- b) Efficient detection of data divergence between replicas by comparing hash subtrees
- c) Compressing data for network transfer
- d) Encrypting data at rest
Answer: b
Objective: Merkle Tree

## Q13: What is the expected time complexity of search, insertion, and deletion in a skip list?
- a) O(n) for all operations
- b) O(log n) with high probability
- c) O(1) amortized
- d) O(n log n)
Answer: b
Objective: Skip List

## Q14: What does the HyperLogLog algorithm estimate?
- a) The median value in a data stream
- b) The number of distinct elements (cardinality) using sub-linear space
- c) The frequency of the most common element
- d) The top-k most frequent elements
Answer: b
Objective: HyperLogLog

## Q15: In Apache Avro, how is schema evolution handled when a reader has a different schema than the writer?
- a) The read fails with an error
- b) Avro resolves differences by matching fields by name, using defaults for missing fields
- c) The writer's schema is always used verbatim
- d) Schema differences are handled at the network layer
Answer: b
Objective: Avro Schema Evolution

## Q16: What type of error does a CRC (Cyclic Redundancy Check) detect?
- a) Only single-bit errors
- b) Burst errors up to the CRC polynomial degree, and most longer bursts
- c) Only errors in the first byte of data
- d) Errors caused by malicious tampering (cryptographic integrity)
Answer: b
Objective: CRC Error Detection

## Q17: What property must a CRDT merge function satisfy to guarantee convergence?
- a) It must be commutative only
- b) It must form a join semilattice — commutative, associative, and idempotent
- c) It must use timestamps for ordering
- d) It must be reversible
Answer: b
Objective: CRDT Convergence

## Q18: In a leaderless replication system, what condition on read (R) and write (W) quorums ensures strong consistency given N replicas?
- a) R = W = 1
- b) R + W > N
- c) R = N and W = 1
- d) R + W = N
Answer: b
Objective: Quorum Consistency

## Q19: What is hinted handoff in a Dynamo-style system?
- a) A technique for data compression
- b) Temporarily storing a write on a different node when the target is unavailable, forwarding when it recovers
- c) A method for partitioning data by key range
- d) A protocol for leader election
Answer: b
Objective: Hinted Handoff

## Q20: What is the purpose of read repair in a distributed database?
- a) To fix corrupted disk sectors
- b) To detect and resolve stale replicas by comparing responses during a read and writing the latest value back
- c) To re-index data after a schema change
- d) To retry failed read operations automatically
Answer: b
Objective: Read Repair

## Q21: In the Raft consensus algorithm, what triggers a new leader election?
- a) A node receives a write request
- b) A follower's election timeout expires without receiving a heartbeat from the current leader
- c) The leader voluntarily steps down after each operation
- d) A client explicitly requests a leader change
Answer: b
Objective: Raft Leader Election

## Q22: What is the fundamental limitation of two-phase commit (2PC)?
- a) It cannot handle more than two participants
- b) It is a blocking protocol — participants are stuck if the coordinator crashes after the prepare phase
- c) It does not support read operations
- d) It requires Byzantine fault tolerance
Answer: b
Objective: Two-Phase Commit

## Q23: How does Practical Byzantine Fault Tolerance (PBFT) differ from crash-fault-tolerant consensus?
- a) PBFT is faster but less reliable
- b) PBFT tolerates arbitrary (Byzantine) faults, requiring 3f+1 nodes to tolerate f faults vs 2f+1 for crash faults
- c) PBFT only works with two nodes
- d) PBFT does not require a quorum
Answer: b
Objective: PBFT

## Q24: What is the relationship between atomic broadcast and consensus?
- a) Atomic broadcast is weaker than consensus
- b) They are equivalent — each can be reduced to the other
- c) Consensus is strictly weaker than atomic broadcast
- d) They are unrelated problems
Answer: b
Objective: Atomic Broadcast and Consensus

## Q25: What does a Lamport timestamp provide?
- a) A global wall-clock time
- b) A logical ordering where if event A happened before B, then timestamp(A) < timestamp(B) — but not the converse
- c) An exact count of messages in the system
- d) A unique node identifier
Answer: b
Objective: Lamport Timestamps

## Q26: What can vector clocks detect that Lamport timestamps cannot?
- a) Network latency
- b) Whether two events are concurrent (causally unrelated)
- c) The physical time of events
- d) The total number of nodes in the system
Answer: b
Objective: Vector Clocks

## Q27: What property does consistent hashing provide when a node is added or removed?
- a) All keys are redistributed equally
- b) Only approximately K/N keys need to be remapped (minimal disruption)
- c) No keys need to move
- d) The hash function changes
Answer: b
Objective: Consistent Hashing

## Q28: What problem do virtual nodes solve in consistent hashing?
- a) They reduce memory usage
- b) They improve load balance by giving each physical node multiple positions on the ring
- c) They provide encryption
- d) They eliminate the need for replication
Answer: b
Objective: Virtual Nodes

## Q29: How does rendezvous hashing (HRW) differ from consistent hashing?
- a) Rendezvous hashing does not use hash functions
- b) Each key computes a score for every candidate node and picks the highest — no ring or virtual nodes needed
- c) Rendezvous hashing only works with two nodes
- d) Rendezvous hashing requires a central coordinator
Answer: b
Objective: Rendezvous Hashing

## Q30: How does a gossip protocol disseminate information through a cluster?
- a) A central server broadcasts to all nodes simultaneously
- b) Each node periodically selects random peers and exchanges state, achieving epidemic-style convergence in O(log N) rounds
- c) Nodes form a strict tree hierarchy for message passing
- d) Only the leader node can initiate communication
Answer: b
Objective: Gossip Protocol

## Q31: What isolation anomaly does snapshot isolation permit that serializable isolation does not?
- a) Dirty reads
- b) Write skew — where two concurrent transactions each read the other's write set and make decisions that conflict
- c) Non-repeatable reads
- d) Phantom reads only
Answer: b
Objective: Snapshot Isolation and Write Skew

## Q32: How does MVCC (Multiversion Concurrency Control) avoid readers blocking writers?
- a) By using exclusive locks on all rows
- b) By maintaining multiple versions of each row so readers see a consistent snapshot without acquiring locks
- c) By aborting all concurrent transactions
- d) By serializing all operations through a single thread
Answer: b
Objective: MVCC

## Q33: What does Serializable Snapshot Isolation (SSI) add on top of snapshot isolation?
- a) Stronger locking guarantees
- b) Dependency tracking that detects dangerous read-write conflicts and aborts transactions to prevent serialization anomalies
- c) A faster commit protocol
- d) Multi-datacenter replication
Answer: b
Objective: Serializable Snapshot Isolation

## Q34: What is two-phase locking (2PL)?
- a) A variant of two-phase commit
- b) A concurrency control protocol where a transaction acquires all locks before releasing any, guaranteeing serializability
- c) A technique for partitioning data into two phases
- d) A replication strategy for two datacenters
Answer: b
Objective: Two-Phase Locking

## Q35: What is change data capture (CDC)?
- a) A technique for compressing database backups
- b) The process of observing changes in a database and extracting them as a stream of events for downstream consumers
- c) A security audit log
- d) A method for encrypting data in transit
Answer: b
Objective: Change Data Capture

## Q36: What is a materialized view?
- a) A virtual table that executes a query on every access
- b) A precomputed result of a query stored on disk and updated as the underlying data changes
- c) A type of database index
- d) A log of all queries executed against a database
Answer: b
Objective: Materialized View

## Q37: In MapReduce, what happens between the map and reduce phases?
- a) Data is compressed and archived
- b) A shuffle and sort step groups all values by key and sends each key group to a reducer
- c) The map output is discarded and recomputed
- d) A consensus round determines which reducers to use
Answer: b
Objective: MapReduce Shuffle

## Q38: What ordering guarantee does Apache Kafka provide?
- a) Total order across all partitions
- b) Order is guaranteed within a single partition but not across partitions
- c) No ordering guarantees at all
- d) Ordering only for the first consumer in a group
Answer: b
Objective: Kafka Ordering

## Q39: In the CAP theorem, what must a distributed system sacrifice during a network partition?
- a) Either consistency or availability — it cannot guarantee both
- b) Partition tolerance
- c) Durability
- d) Throughput
Answer: a
Objective: CAP Theorem

## Q40: How does the PACELC theorem extend CAP?
- a) It adds a "Performance" dimension
- b) It says even when there is no partition (Else), the system must trade off between latency and consistency
- c) It removes the partition tolerance requirement
- d) It adds a fourth property: Encryption
Answer: b
Objective: PACELC Theorem

## Q41: What does linearizability guarantee?
- a) That all operations complete in constant time
- b) That every operation appears to take effect atomically at some point between its invocation and response, as if there were a single copy
- c) That reads always return the oldest value
- d) That writes are batched for efficiency
Answer: b
Objective: Linearizability

## Q42: What does the FLP impossibility result state?
- a) That Byzantine fault tolerance is impossible
- b) That deterministic consensus is impossible in an asynchronous system with even one crash failure
- c) That partition tolerance is optional
- d) That eventual consistency is stronger than linearizability
Answer: b
Objective: FLP Impossibility
