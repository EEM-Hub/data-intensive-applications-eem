---
source: sources/wiki-Replication_computing.md
source_url: https://en.wikipedia.org/wiki/Replication_(computing)
---

## Replication in Computing: Models, Techniques, and Tradeoffs

Replication maintains multiple copies of data, processes, or resources across redundant components to improve availability, fault tolerance, and performance. This topic is central to distributed systems design, covering everything from database replication strategies (single-leader, multi-leader, leaderless) to disk and file-level replication, with deep connections to the CAP theorem and consistency models.

## Key Concepts

- **Data replication** stores the same data on multiple devices; **computation replication** executes the same task multiple times (in space across devices, or in time on one device)
- **Active replication**: every replica processes the same request independently
- **Passive replication**: one replica processes requests and transfers results to others
- **Primary-backup (single-leader)**: one designated leader handles all writes; replicas serve reads but may return stale data due to **replication lag**
- **Multi-leader (multi-master)**: any node can accept writes; enables local write processing in multi-datacenter deployments but introduces **write conflict** complexity
- **Synchronous replication**: write not considered complete until acknowledged by all replicas — guarantees zero data loss but increases latency proportional to distance (10 km minimum roundtrip ~67 μs vs local write ~10-20 μs)
- **Asynchronous replication**: write completes on local acknowledgment; better performance but risks data loss on local failure
- **Semi-synchronous**: write completes when local storage acknowledges and remote server receives/logs it; actual remote write is async
- Replication should be **transparent** to external users — failover should be hidden with respect to quality of service
- **Backup ≠ replication**: backups remain unchanged for long periods; replicas undergo frequent updates and lose historical state quickly
- Jim Gray's analysis: multi-primary replication under transactional model can degrade as **O(n³)** unless data has a natural partitioning key

## Three Replication Models in Distributed Systems

- **Transactional replication**: replicates transactional data using **one-copy serializability** to maintain ACID properties across replicas
- **State machine replication (SMR)**: assumes replicated process is a deterministic finite automaton with atomic broadcast; typically implemented via replicated log using **Paxos** consensus rounds (popularized by Google's Chubby)
- **Virtual synchrony**: processes cooperate in a group, receiving checkpoints of current state; multicasts are delivered in identical order to all members; membership changes delivered as special "view change" multicasts

## Database Replication Techniques

- **Statement-based replication**: SQL statements logged and replayed on replicas — problematic with non-deterministic functions or side effects
- **Write-ahead log (WAL) shipping**: low-level storage engine WAL replicated to ensure identical data structures across nodes
- **Logical (row-based) replication**: changes described at row level in dedicated format — more flexible, decoupled from storage engine internals

## Conflict Handling

- **Eager (synchronous)** systems perform **conflict prevention** — detect conflicts before commit, abort one transaction
- **Lazy (asynchronous)** systems perform **conflict resolution** after both transactions commit — methods include last-write-wins, application-specific logic, or merging concurrent updates

## Disk and File-Level Replication

- **Disk mirroring**: local, short-distance block-level replication
- **Storage replication**: extends across networks for disaster recovery; implemented in hardware (disk array controller) or software (device driver)
- **Point-in-time replication**: periodic snapshots replicated instead of continuous — less bandwidth required
- **Kernel driver (filter driver) capture**: intercepts filesystem calls, transmits operations to remote machine — allows granular, file-level decisions (exclude temp files, send only changed bytes)
- **File system journal replication**: journal sent periodically or streamed in real time to replica for replay
- **Batch replication** (e.g., rsync): periodically compares and synchronizes source/destination — inexpensive but system-intensive

## Relationships

- **CAP theorem / PACELC theorem**: replication is fundamentally constrained by the tradeoff between consistency, availability, and partition tolerance
- **Consensus protocols** (Paxos, Raft): underpin state machine replication and leader election
- **Partitioning/sharding**: Gray's solution to multi-master scaling — complementary to replication
- **Change data capture (CDC)**: mechanism for detecting and propagating data changes, often used with logical replication
- **Load balancing**: distributes different computations across machines; sometimes uses multi-master replication internally
- **Failover**: replication enables transparent failover when components fail
- **Distributed concurrency control / distributed lock managers**: required for multi-master schemes
- **Chain replication**: arranges replicas in a chain for writes — high throughput and strong consistency but higher write latency
- **Hermes protocol**: combines invalidations and logical timestamps for strong consistency with high-performance reads and writes from all replicas

## Exam-Relevant Points

- Know the three replication models: transactional, state machine, virtual synchrony — and when each applies
- Synchronous vs asynchronous replication tradeoffs: zero data loss vs performance; latency bounded by speed of light
- Single-leader vs multi-leader vs leaderless: each has distinct consistency and availability characteristics
- Three database replication techniques (statement-based, WAL shipping, logical/row-based) and their tradeoffs
- Eager replication → conflict prevention; lazy replication → conflict resolution
- Gray's O(n³) degradation warning for multi-master without natural data partitioning
- Replication lag causes stale reads in single-leader setups
- Backup is NOT replication — backups preserve historical state, replicas do not
- Active replication = all replicas process same request; passive = one processes, others receive result
- CAP and PACELC theorems constrain replication design choices
- Semi-synchronous replication: compromise between sync and async — no durability guarantee on local failure
