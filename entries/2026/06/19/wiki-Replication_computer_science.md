---
source: sources/wiki-Replication_computer_science.md
source_url: https://en.wikipedia.org/wiki/Replication_(computer_science)
---

## Replication in Computing: Strategies, Models, and Tradeoffs

Replication maintains multiple copies of data, processes, or resources across redundant components to improve availability, fault tolerance, and performance. It spans databases, file systems, and distributed systems, and sits at the center of the CAP theorem tradeoff between consistency, availability, and partition tolerance. This is one of the oldest and most important topics in distributed systems.

## Key Concepts

- **Data replication** stores the same data on multiple devices; **computation replication** executes the same task multiple times (in space across devices, or in time on a single device)
- **Active replication**: every replica processes every request independently
- **Passive replication**: one replica processes requests and transfers results to others
- **Primary-backup (single-leader)**: one leader handles all writes, replicas serve reads; simple but the backup is idle capacity
- **Multi-primary (multi-leader)**: any replica can accept writes; enables local writes in multi-datacenter deployments but introduces write conflicts and O(n³) degradation risk (per Jim Gray's analysis) unless data has a natural partition key
- **Replication lag**: the delay between a write on the leader and its visibility on replicas; replicas may serve stale data
- **Synchronous replication**: write not confirmed until all replicas acknowledge — guarantees zero data loss but latency is bounded by speed of light (10 km ≈ 67 μs minimum round-trip)
- **Asynchronous replication**: write confirmed after local acknowledgment — better performance but risk of data loss on failure
- **Semi-synchronous**: write confirmed after remote receipt/log but before remote write completes — a middle ground
- **Replication ≠ backup**: replicas are continuously updated and lose historical state; backups are point-in-time snapshots preserved long-term
- **Replication transparency**: access to replicated data should be indistinguishable from access to a single copy; failover should be hidden from users

## Three Replication Models in Distributed Systems

- **Transactional replication**: replicates transactional data using one-copy serializability to maintain ACID guarantees across replicas
- **State machine replication (SMR)**: treats each replica as a deterministic finite automaton; relies on atomic broadcast and distributed consensus (e.g., Paxos). Popularized by Google's Chubby lock service
- **Virtual synchrony**: processes join a group, receive a state checkpoint, then see multicasts in identical order; membership changes delivered as special "view" multicasts. Basis for the CORBA fault-tolerant computing standard

## Database Replication Techniques

- **Statement-based replication**: forwards write statements (e.g., SQL) to replicas — problematic with non-deterministic functions
- **Write-ahead log (WAL) shipping**: replicates the storage engine's low-level WAL — ensures identical data structures but tightly couples replicas to storage engine internals
- **Logical (row-based) replication**: describes changes at the row level in a dedicated log format — more flexible, decoupled from storage engine

## Conflict Handling

- **Eager (synchronous) systems**: detect conflicts before commit, abort one transaction
- **Lazy (asynchronous) systems**: allow both transactions to commit, resolve conflicts during resync
- Resolution methods: last-write-wins, application-specific logic, merge of concurrent updates

## Disk and File-Based Replication

- **Disk mirroring**: local block-level replication, typically via disk array controller or device driver
- **Point-in-time replication**: periodic snapshots of changed data, lower bandwidth requirements
- **Kernel driver capture**: intercepts filesystem calls at the filter driver level, transmits operations to remote machine
- **File system journal replication**: replays the filesystem journal on a replica
- **Batch replication** (e.g., rsync): periodically compares and synchronizes source and destination

## Commands and Syntax

No specific CLI commands defined in the source, but key tools referenced:
- **rsync** — batch file-based replication by comparing source/destination
- **iSCSI** — lower-cost bandwidth link for point-in-time replication
- **Microsoft DPM** — periodic file-level replication (not real-time)

## Relationships

- **CAP theorem / PACELC theorem**: replication forces tradeoffs between consistency, availability, and partition tolerance
- **Consensus protocols (Paxos, Raft)**: underpin state machine replication
- **Partitioning/Sharding**: Gray's solution to multi-primary degradation — partition data so each shard has a single effective leader
- **Change data capture (CDC)**: related mechanism for propagating data changes
- **Load balancing**: distributes different computations (vs. replication which copies the same data); may use multi-master replication internally
- **Failover**: replication enables automatic failover when a component fails
- **Distributed concurrency control / distributed lock managers**: required for multi-primary schemes
- **Leader election**: mechanism for designating the primary in single-leader schemes
- **Chain replication**: arranges replicas in a chain for writes — high throughput, strong consistency, but high write latency

## Exam-Relevant Points

- **Three replication approaches**: single-leader, multi-leader, leaderless — know the tradeoffs of each
- **Synchronous vs. asynchronous replication**: synchronous = zero data loss but higher latency; asynchronous = better performance but potential data loss
- **Three data change propagation methods**: statement-based, WAL shipping, logical (row-based) — know failure modes of each (e.g., non-deterministic functions break statement-based)
- **Jim Gray's O(n³) degradation**: multi-primary replication degrades cubically with replica count unless data has a natural partition key
- **Replication ≠ backup**: replicas are current-state; backups preserve historical state
- **CAP theorem constrains replicated databases**: NoSQL systems typically sacrifice consistency for availability and partition tolerance
- **Replication lag** causes replicas to serve stale data in single-leader setups — a key source of read-after-write inconsistency
- **Eager replication prevents conflicts; lazy replication resolves them after the fact**
- **State machine replication requires deterministic replicas and atomic broadcast** — implemented via consensus algorithms like Paxos
- **Virtual synchrony** provides identical message ordering within process groups — enables multi-primary with linear speedup for in-memory data
