---
source: sources/wiki-Consensus_computer_science.md
source_url: https://en.wikipedia.org/wiki/Consensus_(computer_science)
---

## Consensus in Distributed Systems

Consensus is the fundamental problem of getting multiple processes in a distributed system to agree on a single data value, even when some processes may fail. It underpins transaction ordering in databases, state machine replication, atomic broadcasts, blockchain, and cloud computing. The problem is deceptively hard: the FLP impossibility result proves that deterministic consensus is impossible in fully asynchronous systems with even one crash failure.

## Key Concepts

- **Consensus properties** — a correct protocol must satisfy three requirements: **Termination** (every correct process eventually decides), **Integrity** (if all correct processes propose the same value v, they must decide v), and **Agreement** (every correct process decides the same value).
- **t-resilient protocol** — a protocol that guarantees consensus among n processes when at most t fail.
- **Crash failure** — a process abruptly stops and never resumes. **Byzantine failure** — a process behaves arbitrarily (sending contradictory data, sleeping then waking, acting maliciously). Byzantine failures are strictly harder to tolerate.
- **FLP impossibility result** (Fischer, Lynch, Paterson, 1985) — no deterministic algorithm can guarantee consensus in a fully asynchronous message-passing system if even one process can crash. This does not mean consensus is never reached, only that no algorithm can *always* reach it in bounded time.
- **Randomized consensus** can circumvent FLP by achieving safety and liveness with overwhelming probability.
- **Oral vs. written communication models** — oral (authenticated channels, receiver knows immediate source) vs. written (digitally signed messages, full provenance chain). Written models tolerate more faults.
- **Single-value consensus** (e.g., Paxos) — agree on one value. **Binary consensus** — input/output restricted to {0,1}, used as building block. **Multi-valued consensus** (e.g., Multi-Paxos, Raft) — agree on a growing series of values over time.
- **Permissioned consensus** — fixed, known set of authenticated participants. **Permissionless consensus** — anyone can join dynamically; requires Sybil resistance mechanisms (proof of work, proof of stake, etc.).
- **Consensus number** — the maximum number of processes that can reach wait-free consensus using a given concurrent object. Forms a hierarchy: atomic read/write registers = 1, test-and-set = 2, compare-and-swap = infinity.

## Commands and Syntax

No CLI commands per se, but key algorithmic procedures:

- **Phase King algorithm** (Garay & Berman) — Byzantine-tolerant, synchronous, requires n > 4f:
  - f+1 phases, 2 rounds per phase
  - Round 1: each process broadcasts preferred value, computes majority and count
  - Round 2: the "king" (process whose ID matches phase number) broadcasts its observed majority as tie-breaker
  - Update rule: if own majority count > n/2 + f, use own majority; otherwise use king's value
  - After f+1 phases, output preferred value

- **Ripple Protocol Consensus Algorithm (RPCA)**:
  1. Each server compiles candidate transactions
  2. Amalgamate candidates from Unique Nodes List (UNL), vote on veracity
  3. Transactions passing minimum threshold advance
  4. Final round requires 80% agreement

## Relationships

- **State machine replication** — consensus enables replicated state machines by ensuring all replicas process the same commands in the same order
- **Atomic broadcast** — equivalent to consensus; solving one solves the other
- **Byzantine Generals Problem** — a specific formulation of consensus; solvable when n > 3f (oral) or n > f+1 (written/signed)
- **Paxos and Raft** — the dominant practical consensus algorithms for crash-tolerant distributed systems; used in Chubby, ZooKeeper, etcd
- **Blockchain/distributed ledger** — permissionless consensus applied at scale; Bitcoin (proof of work), Ethereum (proof of stake)
- **Wait-freedom and lock-freedom** — consensus number hierarchy connects shared-memory synchronization primitives to their power to solve consensus
- **Equivalency of agreement problems** — Terminating Reliable Broadcast, Consensus, and Weak Interactive Consistency are reducible to each other across models

## Exam-Relevant Points

- **Byzantine fault tolerance threshold**: oral/unauthenticated model requires **n > 3f**; written/signed model requires only **n > f+1** (Dolev-Strong)
- **FLP impossibility**: no deterministic consensus in asynchronous systems with even **one** crash failure. Authors: Fischer, Lynch, Paterson (1985). Won the Dijkstra Prize.
- **Randomized algorithms bypass FLP** — they achieve safety and liveness with overwhelming probability
- **Consensus number hierarchy**: read/write registers = 1, test-and-set/swap/fetch-and-add = 2, compare-and-swap (CAS) = **infinity** (universal). This is a strict hierarchy — no wait-free consensus for n+1 processes from objects with consensus number n.
- **Universality**: an object with infinite consensus number (like CAS) can implement any concurrent object in a wait-free manner
- **Phase King**: tolerates Byzantine faults, runs in f+1 phases, requires **n > 4f**
- **Permissioned vs. permissionless**: permissioned assumes known, fixed membership; permissionless must resist **Sybil attacks** via proof of work, proof of stake, proof of space, proof of authority, or proof of personhood
- **Paxos/Raft** are synchronous, leader-based, crash-tolerant (not Byzantine-tolerant); **PBFT** handles Byzantine faults with n > 3f
- **Performance metrics**: running time (rounds of message exchange) and message complexity; these vary dramatically across protocols (see comparison table)
- **Three equivalent agreement problems**: Terminating Reliable Broadcast, Consensus, Weak Interactive Consistency — a solution to one can be transformed into a solution for the others
