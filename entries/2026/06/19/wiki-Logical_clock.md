---
source: sources/wiki-Logical_clock.md
source_url: https://en.wikipedia.org/wiki/Logical_clock
---

## Logical Clocks in Distributed Systems

Logical clocks are mechanisms for capturing chronological and causal relationships in distributed systems that lack a physically synchronous global clock. Introduced by Leslie Lamport in 1978, logical clocks allow processes to agree on event ordering without requiring wall-clock synchronization. This is sufficient for many applications where non-interacting processes don't need to observe synchronization.

## Key Concepts

- **Logical clock**: A mechanism to capture chronological and causal ordering of events without a shared physical clock
- **Logical local time**: A per-process data structure used to timestamp its own events
- **Logical global time**: A per-process data structure representing that process's local view of global time
- A special protocol updates logical local time after each local event, and logical global time when processes exchange data
- If two processes never interact, lack of synchronization is unobservable — agreement on event ordering is sufficient
- Logical clocks establish ordering, not wall-clock timestamps

## Commands and Syntax

No specific commands — logical clocks are algorithmic concepts implemented in application code. The core protocol pattern is:
1. Increment local clock on each local event
2. Attach clock value to outgoing messages
3. On message receipt, update local clock based on received value

## Relationships

- **Lamport timestamps**: Monotonically increasing software counters; the foundational logical clock algorithm
- **Vector clocks**: Enable partial ordering of events (stronger than Lamport's total ordering with ties)
- **Version vectors**: Order replicas by updates in optimistic replication systems
- **Matrix clocks**: Extend vector clocks to include information about other processes' views of the system
- Underpins causality tracking in distributed databases, conflict resolution, and consistency protocols
- Directly related to the **happens-before** relation defined by Lamport

## Exam-Relevant Points

- Logical clocks were introduced by **Leslie Lamport in 1978**
- Two data structures per process: **logical local time** and **logical global time**
- Logical clocks solve ordering, not time measurement — they answer "which event happened first" not "when did it happen"
- Know the four algorithms and their relative power: Lamport timestamps (total order with arbitrary tie-breaking) → Vector clocks (partial order, detect causality) → Version vectors (replica ordering) → Matrix clocks (global view of vector clocks)
- Key use cases: computation analysis, distributed algorithm design, event tracking, exploring computational progress
- Non-interacting processes do not need synchronization — this is the motivating insight
