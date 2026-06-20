---
source: sources/wiki-Bully_algorithm.md
source_url: https://en.wikipedia.org/wiki/Bully_algorithm
---

## Bully Algorithm for Leader Election in Distributed Systems

The bully algorithm is a method for dynamically electing a coordinator (leader) from a group of distributed processes. It works by selecting the process with the highest process ID among all non-failed processes as the coordinator. The algorithm operates in a synchronous system model with reliable message delivery and a failure detector.

## Key Concepts

- **Core principle**: The highest-ID non-failed process always becomes coordinator — hence "bully," as the biggest process always wins.
- **System model**: Synchronous, crash-recovery (processes fail by stopping, recover by restarting).
- **Failure detector**: The algorithm assumes an external mechanism detects failed processes.
- **Complete knowledge**: Every process knows the ID and address of every other process.
- **Three message types**:
  - **Election** — announces a new election
  - **Answer (Alive)** — response to an Election message, indicating a higher-ID process is alive
  - **Coordinator (Victory)** — declares the sender as the new leader
- **Safety**: At no point can two non-faulty processes disagree on who the leader is (outside of an active election). Proven by contradiction — two victory messages would require both senders to have skipped the election exchange, which is impossible.
- **Liveness**: Guaranteed in the synchronous crash-recovery model. Timeout mechanisms ensure that if a would-be leader crashes before sending Victory, a lower-ID process will eventually take over.
- **Worst-case message complexity**: Θ(N²) — triggered when the lowest-ID process initiates the election, producing Θ(N²) Election messages + Θ(N²) Alive messages + Θ(N) Coordinator messages.

## Commands and Syntax

The algorithm procedure for a process P:

1. **If P has the highest ID** → send Victory to all, become Coordinator.
2. **Otherwise** → send Election to all processes with higher IDs.
3. **If no Answer received** → send Victory to all, become Coordinator.
4. **If Answer received from higher-ID process** → stop and wait for Victory message (restart election if Victory times out).
5. **If Election received from lower-ID process** → send Answer back, then start own election if not already running.
6. **If Coordinator message received** → accept sender as coordinator.

## Relationships

- **Leader election**: The bully algorithm is one specific solution to the general leader election problem in distributed systems.
- **Chang and Roberts algorithm**: An alternative leader election algorithm that operates on a logical ring topology (more message-efficient at O(N log N) average case).
- **Failure detectors**: The algorithm depends on a reliable failure detector — the properties of the detector (completeness, accuracy) directly affect correctness.
- **Synchronous vs. asynchronous models**: The bully algorithm requires synchrony (bounded message delays) for its timeout mechanisms. It does not work in purely asynchronous systems (related to the FLP impossibility result).
- **Byzantine fault tolerance**: The bully algorithm handles crash faults only, not Byzantine (arbitrary) faults. Lamport's Byzantine Generals Problem addresses the harder case.

## Exam-Relevant Points

- The bully algorithm requires a **synchronous** system model — this is a critical assumption.
- Worst-case message complexity is **Θ(N²)**, occurring when the lowest-ID process triggers the election.
- The algorithm guarantees **safety** (no two leaders simultaneously, except during election) and **liveness** (an election always terminates with a leader).
- A process only sends a Victory message if it receives **no Answer** from any higher-ID process.
- When a process recovers from failure, it initiates a new election — it does not simply rejoin passively.
- The algorithm assumes **reliable message delivery** and a **failure detector** — without these, correctness breaks down.
- Know the distinction: the bully algorithm is for **crash-recovery** faults, not **Byzantine** faults.
