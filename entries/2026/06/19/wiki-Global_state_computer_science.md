---
source: sources/wiki-Global_state_computer_science.md
source_url: https://en.wikipedia.org/wiki/Global_state_(computer_science)
---

## Consistent Global State and Distributed Snapshots

This page covers the theory and algorithms for capturing a meaningful snapshot of a distributed system's state. Because distributed systems lack shared memory and a global clock, no single process can observe the entire system at one instant. The Chandy-Lamport framework (1985) defines what it means for a recorded global state to be *consistent* — corresponding to a state the system could actually have passed through — and provides a marker-based protocol to capture one without pausing execution.

## Key Concepts

- **Global state** is the tuple of all process local states plus all channel states (messages in transit): GS = (s₁, s₂, …, sₙ, M₁₂, M₁₃, …, Mₙ₍ₙ₋₁₎)
- **Local state** of process pᵢ is the information sufficient to determine its future behavior after an event
- **Channel state** Mᵢⱼ is the sequence of messages sent on cᵢⱼ but not yet received — the in-transit messages
- **Cut** partitions execution history into past and future sets; the frontier is each process's last event in the past
- **Consistent cut**: for every receive event in the past, the corresponding send event is also in the past — no message appears received without being sent
- **Consistent global state** (consistent snapshot): the global state defined by a consistent cut
- **Naive sequential collection fails** because a message can be sent before one process is observed but received after another is observed, causing the message to "vanish" from the recorded state
- **Reachability theorem**: any consistent global state S is reachable from the initial state S₀, and the actual current state S' is reachable from S — the snapshot represents a valid intermediate state even if it never simultaneously existed
- **Stable predicate**: a property Φ where Φ(S) = true implies Φ(S') = true for all states S' reachable from S — once true, stays true
- Examples of stable predicates: deadlock, termination, garbage-collection eligibility
- Unstable predicates (transient conditions) cannot be reliably evaluated from a single snapshot
- **System model assumptions**: fixed set of n processes, directed FIFO channels, reliable delivery (in order, no loss, no duplication)
- Three event types: send, receive, internal

## Commands and Syntax

No CLI commands. The core formal definitions:

- **Happened-before relation** (Lamport 1978): e → f if (1) e and f are on the same process and e precedes f, or (2) e is a send and f is the matching receive, or (3) transitivity via some intermediate event g
- **Chandy-Lamport marker protocol**:
  1. Initiator records its local state, sends a **marker** on every outgoing channel before any further application messages
  2. On first marker receipt on channel cⱼᵢ, process pᵢ records its own local state, records cⱼᵢ as empty, sends markers on all its outgoing channels
  3. Messages received on any incoming channel cₖᵢ after pᵢ's state is recorded but before the marker arrives on cₖᵢ are recorded as that channel's state
  4. Algorithm terminates when every process has received a marker on all incoming channels
- **Lai-Yang algorithm** (1987): for non-FIFO channels, uses message **colouring** (pre-snapshot vs. post-snapshot tags) instead of markers
- **Mattern's algorithm** (1989): uses **vector clocks** to determine message-snapshot relationships, enabling concurrent snapshots without markers

## Relationships

- **Happened-before / Lamport timestamps**: the partial ordering that defines consistency of cuts
- **Vector clocks**: used by Mattern's extension for non-FIFO snapshot recording
- **Chandy-Lamport algorithm**: the concrete protocol implementing consistent snapshot capture
- **Deadlock detection**: a primary application — check wait-for graph in recorded snapshot
- **Termination detection**: another stable-predicate application — all idle, all channels empty
- **Checkpointing / fault tolerance**: periodic snapshots create recovery points; reachability theorem guarantees valid restart
- **Distributed garbage collection**: snapshot of all process heaps identifies unreachable objects
- **FIFO channels**: a core assumption of the original protocol; relaxed by Lai-Yang and Mattern

## Exam-Relevant Points

- A consistent cut requires that no message is recorded as received unless it is also recorded as sent — this is the defining condition
- The reachability theorem has two parts: S₀ → S and S → S' (initial reaches snapshot, snapshot reaches actual current state)
- Stable predicates can be detected from a single consistent snapshot without pausing the system; unstable predicates cannot
- Deadlock, termination, and GC eligibility are all stable predicates
- The Chandy-Lamport protocol requires FIFO channels; Lai-Yang (colouring) and Mattern (vector clocks) handle non-FIFO
- A recorded consistent state need not correspond to any state that simultaneously existed — it is a *possible* intermediate state
- Naive sequential observation fails because messages can vanish (sent before one observation, not yet received at the next)
- The marker must be sent before any further application messages on outgoing channels — ordering is critical
- Channel state is recorded as the messages arriving between local state capture and marker arrival on that channel
- Chandy and Lamport introduced the consistent global state concept in 1985 (ACM TOCS)
