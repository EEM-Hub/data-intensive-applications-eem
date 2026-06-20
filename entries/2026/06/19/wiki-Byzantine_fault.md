---
source: sources/wiki-Byzantine_fault.md
source_url: https://en.wikipedia.org/wiki/Byzantine_fault
---

## Byzantine Faults and Byzantine Fault Tolerance (BFT)

Byzantine faults are a class of failure in distributed systems where a faulty component presents different, inconsistent symptoms to different observers. Named after the "Byzantine generals problem" allegory by Lamport, Shostak, and Pease (1982), the concept captures the hardest category of distributed system failure: one where faulty nodes can produce arbitrary, potentially contradictory outputs that confuse other nodes and defeat naive failure detection. Byzantine fault tolerance (BFT) is the ability of a system to continue operating correctly despite such faults.

## Key Concepts

- **Byzantine fault**: any fault that presents different symptoms to different observers — the most general and difficult failure mode in distributed systems
- **Byzantine failure**: loss of system service due to a Byzantine fault in a system requiring consensus
- **Fail-stop vs. Byzantine**: fail-stop is the simplest failure mode (node crashes and is detected); Byzantine is the hardest (node produces arbitrary data, may appear functional to some observers)
- **The 3f+1 rule**: without message signing, BFT requires n > 3f nodes to tolerate f faulty nodes. This is both necessary and sufficient (proven by Pease, Shostak, Lamport)
- **Full BFT requirements**: for F Byzantine failures, need at least 3F+1 nodes, 2F+1 independent communication paths, and F+1 rounds of communication
- **With digital signatures**: BFT can tolerate an arbitrary number of faulty nodes (Lamport's proof using 3n nodes with signatures)
- **Broadcast consistency**: BFT ensures that when a component broadcasts a value, all receivers get the same value — it does NOT verify the correctness of the value itself
- **Not only a security problem**: Byzantine failures can arise from purely physical or software faults (e.g., incorrect voltages propagating through encryption), not just adversarial behavior
- **Schrödinger CRC**: a CRC-protected message with a single Byzantine faulty bit can present different valid data to different observers — neither CRCs nor digital signatures fully protect against Byzantine errors from natural causes
- **PBFT (Practical Byzantine Fault Tolerance)**: introduced by Castro and Liskov (1999), processes thousands of requests per second with sub-millisecond latency overhead — made BFT practical for real systems
- **Blockchain caveat**: systems like Bitcoin don't guarantee BFT agreement in the classical sense; they use resource-intensive mechanisms (proof of work) that make sustained disagreement impractical rather than impossible

## Commands and Syntax

No CLI commands — this is a theoretical/architectural concept. However, the key formulas are:

- **Minimum nodes without signatures**: `n > 3f` (n = total nodes, f = faulty nodes)
- **Minimum nodes with signatures**: `n >= 3f` (arbitrary f tolerable)
- **Full requirements**: `3F+1 nodes`, `2F+1 communication paths`, `F+1 communication rounds`
- **Hybrid fault model**: for each additional benign (non-Byzantine) fault tolerated, increment each of the above by one

## Relationships

- **Consensus protocols**: BFT is the hardest case that consensus algorithms (Paxos, Raft, PBFT, Tendermint) must address; Paxos handles crash faults but not Byzantine faults
- **Two Generals' Problem**: a simpler impossibility result about consensus with unreliable communication — Byzantine Generals generalizes it to unreliable participants
- **Replication and state machine replication**: PBFT enables Byzantine-tolerant state machine replication, foundational for replicated databases and services
- **Blockchain/cryptocurrency**: Bitcoin's proof-of-work and proof-of-stake protocols are practical (weaker) approximations of BFT consensus
- **Quorum systems**: the 3f+1 threshold directly determines quorum sizes in BFT-tolerant distributed storage
- **Atomic commit**: relates to ensuring all-or-nothing operations across distributed nodes
- **CRDTs (Conflict-free Replicated Data Types)**: an alternative approach that avoids consensus entirely by using mathematically convergent data structures
- **Safety-critical systems**: aviation (Boeing 777/787 flight control, SAFEbus) and space (SpaceX Dragon, Orion, SLS) use BFT with microsecond-level latency constraints

## Exam-Relevant Points

- **The 3f+1 bound is exact**: you need strictly more than 3 times the faulty nodes to tolerate Byzantine faults without signatures — memorize `n > 3f` (or `n >= 3f+1`)
- **Three requirements together**: 3F+1 players, 2F+1 communication paths, F+1 rounds — all three must be met simultaneously
- **With unforgeable signatures, arbitrary failures are tolerable** — but digital signatures don't protect against physical-layer Byzantine faults
- **PBFT (Castro & Liskov, 1999)** was the breakthrough making BFT practical — know the name and its significance
- **BFT only guarantees broadcast consistency**, not value correctness — a node consistently sending the same wrong value to everyone is not caught by BFT
- **Byzantine faults are the most general failure class** — they subsume crash faults, omission faults, and timing faults
- **History**: formalized by Robert Shostak (1978) at SRI International for the NASA SIFT project; the allegory was created by Leslie Lamport; the seminal 1982 paper won the 2005 Dijkstra Prize
- **O(n²) communication complexity** is the traditional BFT bottleneck — newer protocols (e.g., Cerberus) achieve linear scalability through parallelized consensus
- **Real-world BFT deployments**: Boeing 777 SAFEbus (microsecond latency), SpaceX Dragon, Virginia-class submarines — these are not just theoretical
