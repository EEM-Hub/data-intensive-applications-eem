---
source: sources/wiki-Atomic_broadcast.md
source_url: https://en.wikipedia.org/wiki/Atomic_broadcast
---

## Atomic Broadcast (Total Order Broadcast)

Atomic broadcast is a distributed computing primitive that guarantees all correct processes in a system receive the same set of messages in the same order. The term "atomic" reflects its all-or-nothing semantics: the broadcast either completes correctly at all participants or all participants abort without side effects. It is a fundamental building block for fault-tolerant distributed systems.

## Key Concepts

- **Atomic broadcast = total order broadcast**: all correct processes deliver the same messages in the same sequence
- **Four required properties**:
  - **Validity**: if a correct participant broadcasts, all correct participants eventually receive it
  - **Uniform Agreement**: if one correct participant receives a message, all correct participants eventually receive it
  - **Uniform Integrity**: each message received at most once, and only if previously broadcast
  - **Uniform Total Order**: all correct participants deliver messages in the identical order
- **Total order ≠ FIFO order**: total order only requires all participants see the same sequence — it does not require messages arrive in the order they were sent by any particular process
- **Total order ≠ causal order**: causal order respects happens-before relationships; total order may deliver messages in any consistent order as long as all participants agree on it
- **Equivalence to consensus**: in systems with crash failures, atomic broadcast and consensus are reducible to each other (proven by Chandra and Toueg)
- **FLP impossibility applies**: since atomic broadcast is equivalent to consensus, the Fischer-Lynch-Paterson result (1985) proves it is impossible to guarantee in a purely asynchronous system with even one crash failure
- **FLP does not prohibit practical implementations**: it requires relaxing strict asynchrony assumptions (e.g., using failure detectors or partial synchrony)

## Commands and Syntax

No specific CLI commands. This is a theoretical primitive. Practical implementations include:
- **ZAB (ZooKeeper Atomic Broadcast)**: protocol underlying Apache ZooKeeper, used for distributed coordination in Hadoop and other systems
- **Chandra-Toueg algorithm**: consensus-based solution using unreliable failure detectors
- **Virtual synchrony** (Ken Birman): execution model where all processes observe events in the same order; total order broadcast is one mechanism for achieving this

## Relationships

- **Consensus**: equivalent problem — consensus reduces to atomic broadcast and vice versa; any consensus algorithm can implement atomic broadcast and any atomic broadcast algorithm can implement consensus
- **FLP impossibility result**: directly limits atomic broadcast since it limits consensus
- **Failure detectors**: practical atomic broadcast implementations circumvent FLP by using unreliable failure detectors (Chandra-Toueg)
- **Apache ZooKeeper / ZAB**: most prominent real-world application; ZAB provides atomic broadcast for distributed coordination
- **Replication**: atomic broadcast enables state machine replication — if all replicas process the same messages in the same order, they stay consistent
- **FIFO and causal broadcast**: weaker ordering guarantees that are distinct from (and neither imply nor are implied by) total order

## Exam-Relevant Points

- Know the four properties by name: Validity, Uniform Agreement, Uniform Integrity, Uniform Total Order
- Total order ≠ FIFO ≠ causal order — these are distinct ordering guarantees; be able to distinguish them
- Atomic broadcast and consensus are **equivalent** in crash-failure models — this is a core result (Chandra-Toueg, 1996)
- The **FLP impossibility result** (Fischer, Lynch, Paterson, 1985) applies to atomic broadcast because of this equivalence
- A simple leader-based protocol solves atomic broadcast in failure-free systems, but leader failure makes the problem hard
- **ZAB** is the practical protocol to know — it underpins ZooKeeper, which underpins Hadoop and many distributed systems
- The reduction from consensus to atomic broadcast: propose a value by broadcasting it, decide by selecting the first message received
- The reduction from atomic broadcast to consensus: agree on messages one at a time via repeated consensus rounds
