---
source: sources/wiki-Raft_algorithm.md
source_url: https://en.wikipedia.org/wiki/Raft_(algorithm)
---

## Raft Consensus Algorithm

Raft is a consensus algorithm designed as an understandable alternative to Paxos. It distributes a replicated state machine across a cluster by electing a single leader responsible for log replication. The name stands for Reliable, Replicated, Redundant, And Fault-Tolerant. Raft is **not** Byzantine fault tolerant — all participants are assumed trustworthy.

## Key Concepts

- **Three roles**: every server is a **leader**, **follower**, or **candidate** (only during elections)
- **Term**: an arbitrary period of time beginning with a leader election; terms are numbered monotonically
- **Heartbeat**: leader sends periodic messages to followers; followers have a randomized timeout (typically 150–300 ms) after which they assume the leader is dead
- **Leader-based consensus**: the single elected leader is fully responsible for accepting client requests and replicating log entries to followers
- **Committed entry**: a log entry replicated to a majority of servers; once committed, it is applied to the state machine
- **Log Matching property**: if two logs contain an entry with the same index and term, all preceding entries are identical
- **Leader Completeness**: a committed entry will be present in every future leader's log
- **Joint consensus**: a transitional phase (Cold ∪ Cnew) used during cluster membership changes, requiring majorities from both old and new configurations
- **Log compaction**: servers take snapshots of committed state to reclaim storage; leaders can send snapshots to lagging followers
- **Pre-Vote extension**: prevents a rejoining member from triggering unnecessary elections by first checking with other members
- **Leadership transfer**: allows orderly handoff without waiting for timeout

## Commands and Syntax

No CLI commands per se — Raft defines RPCs:

- **RequestVote RPC**: candidate requests votes from other servers; includes candidate's log info so voters can reject candidates with less up-to-date logs
- **AppendEntries RPC**: leader replicates log entries to followers (also serves as heartbeat when empty)
- **InstallSnapshot RPC** (implied): leader sends snapshots to followers that have fallen far behind

**Timing requirement**: `broadcastTime << electionTimeout << MTBF`
- broadcastTime: 0.5–20 ms (infrastructure-dependent)
- electionTimeout: 10–500 ms (programmer-chosen)
- MTBF: weeks to months

## Relationships

- **Paxos**: Raft is the understandability-focused alternative; solves the same distributed consensus problem but decomposes it into leader election + log replication
- **State machine replication**: Raft is a mechanism for implementing replicated state machines — every node applies the same sequence of commands
- **Byzantine fault tolerance**: Raft explicitly does not provide BFT; systems needing BFT require different algorithms (PBFT, etc.)
- **Production systems using Raft**: etcd (Kubernetes coordination), CockroachDB, TiDB/TiKV, MongoDB (variant), Kafka KRaft, RabbitMQ quorum queues, ScyllaDB, YugabyteDB, Neo4j, ClickHouse Keeper, Redpanda, NATS JetStream, Hazelcast CP subsystem, Camunda Zeebe

## Exam-Relevant Points

- **Five safety guarantees**: Election safety, Leader append-only, Log matching, Leader completeness, State machine safety — know all five
- A candidate **cannot win** unless its log contains all committed entries (this enforces State Machine Safety)
- Votes are **first-come-first-served**, one vote per term per server
- **Randomized election timeout** resolves split votes quickly
- An entry is committed once replicated to a **majority** (not all) followers
- After leader crash, the new leader forces followers to match its log by finding the last agreeing entry and overwriting everything after it
- Raft is **not Byzantine fault tolerant** — nodes trust the elected leader
- Cluster membership changes use **joint consensus** requiring majorities from both old and new configurations simultaneously
- The timing invariant `broadcastTime << electionTimeout << MTBF` is required for stability
- The leader is a **single point of failure and performance bottleneck** — Raft does not scale writes with cluster size
- The reconfiguration mechanism has **not been formally verified**; a safety bug was found in single-server membership changes (2014)
