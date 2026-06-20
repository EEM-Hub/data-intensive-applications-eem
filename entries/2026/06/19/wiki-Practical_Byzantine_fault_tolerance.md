---
source: sources/wiki-Practical_Byzantine_fault_tolerance.md
source_url: https://en.wikipedia.org/wiki/Practical_Byzantine_fault_tolerance
---

## Byzantine Faults and Byzantine Fault Tolerance (BFT)

Byzantine faults are failures in distributed systems where a faulty component presents different symptoms to different observers, making it impossible for other components to simply agree on whether a failure has occurred. Named after the "Byzantine generals problem" allegory by Lamport, Shostak, and Pease (1982), this is the most general and most difficult class of failure modes in distributed computing. Byzantine fault tolerance (BFT) is the property of a system that can continue operating correctly despite such faults.

## Key Concepts

- **Byzantine fault**: any fault presenting different symptoms to different observers — not restricted to security attacks; can arise from physical or software faults
- **Byzantine failure**: loss of a system service due to a Byzantine fault in systems requiring consensus
- **Fail-stop vs. Byzantine**: fail-stop means a node simply crashes and is detected; Byzantine means a node can generate arbitrary, misleading data — the hardest failure class
- **The 3f+1 rule**: without message signing, BFT requires n > 3f nodes to tolerate f faulty nodes (proved by Shostak/Pease, 1980)
- **With digital signatures**: BFT can tolerate an arbitrary number of faulty nodes (proved by Lamport)
- **Full BFT requirements**: for F Byzantine failures, need at least 3F+1 nodes, 2F+1 independent communication paths, and F+1 rounds of communication
- **Broadcast consistency**: BFT ensures all correct nodes receive the same value from a broadcaster, or agree on a common value if the broadcaster is faulty — it does NOT validate the correctness of the value itself
- **Schrödinger CRC**: a CRC-protected message with a single Byzantine faulty bit can present different valid data to different observers — neither CRCs nor digital signatures fully protect against Byzantine faults from natural causes
- **PBFT** (Practical Byzantine Fault Tolerance): introduced by Castro and Liskov in 1999, enabled high-performance BFT state machine replication with thousands of requests/second
- **Blockchain caveat**: systems like Bitcoin don't guarantee agreement in the classical BFT sense — they use resource-intensive mechanisms (PoW) that make disagreement impractical to maintain, which is a weaker guarantee

## Commands and Syntax

No CLI commands per se, but critical formulas:

- **Minimum nodes without signatures**: `n > 3f` (n = total nodes, f = faulty nodes)
- **Minimum nodes with signatures**: any n, with unforgeable signatures
- **Full BFT resource requirements**: `3F+1` players, `2F+1` communication paths, `F+1` rounds
- **Hybrid fault model**: for each additional benign (non-Byzantine) fault tolerated, increment all above numbers by 1
- **Communication complexity**: traditional BFT is O(n^2); newer protocols like Cerberus achieve linear scalability through parallelized consensus

## Relationships

- **Consensus protocols**: BFT is a foundational problem underlying Paxos, Raft, and other consensus algorithms — Paxos solves consensus under crash faults, BFT extends to arbitrary faults
- **Two Generals' Problem**: a simpler impossibility result about reaching agreement over unreliable channels (two parties, not n)
- **Atomic commit**: requires agreement across nodes, subject to Byzantine failure modes
- **Blockchain/cryptocurrency**: Bitcoin (PoW), proof-of-stake chains, Hyperledger Fabric (PBFT), Cosmos (Tendermint BFT) all address Byzantine faults with different tradeoffs
- **Conflict-free replicated data types (CRDTs)**: an alternative approach that avoids consensus entirely by ensuring all operations commute
- **Dependability taxonomy**: Byzantine faults sit within the IEEE/IFIP framework of fault, error, and failure definitions
- **Safety-critical vs. security-critical systems**: security systems use digital signatures; safety systems prefer error-detecting codes (CRCs) — the two can conflict

## Exam-Relevant Points

- **The n > 3f bound is fundamental**: without signatures, you cannot tolerate 1/3 or more faulty nodes — know the proof sketch (1 commander, 2 lieutenants, commander is traitor)
- **3F+1 nodes, 2F+1 paths, F+1 rounds**: memorize the full BFT requirement triple
- **PBFT (Castro & Liskov, 1999)** is the landmark practical algorithm — know the name and that it enabled practical BFT for the first time
- **Byzantine faults are NOT limited to malicious actors** — hardware glitches, voltage errors, and software bugs can all produce Byzantine symptoms
- **BFT only provides broadcast consistency**, not value correctness — a consistently lying node is not caught
- **Blockchain does not provide classical BFT** — it provides probabilistic finality via economic incentives, not mathematical guarantees
- **History**: conceived by Robert Shostak (1978) at SRI International for the NASA SIFT project; formalized by Lamport, Shostak, and Pease; allegory name "Byzantine" suggested by Jack Goldberg; awarded the 2005 Dijkstra Prize
- **Real-world deployments**: Boeing 777/787 flight control, SpaceX Dragon, Space Launch System — safety-critical systems requiring microsecond-latency BFT
- **Digital signatures vs. CRCs**: signatures help with security threats; CRCs help with safety/natural faults; neither alone covers Byzantine faults from all causes
