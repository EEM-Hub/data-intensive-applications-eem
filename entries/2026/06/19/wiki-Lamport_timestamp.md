---
source: sources/wiki-Lamport_timestamp.md
source_url: https://en.wikipedia.org/wiki/Lamport_timestamp
---

## Lamport Timestamps: Logical Ordering of Events in Distributed Systems

Lamport timestamps are a logical clock algorithm invented by Leslie Lamport for determining the order of events across nodes in a distributed system where physical clocks cannot be perfectly synchronized. The algorithm assigns monotonically increasing counter values to events, providing a partial ordering with minimal overhead. It is the conceptual foundation for more advanced mechanisms like vector clocks.

## Key Concepts

- **Happened-before relation**: Event *a* happened-before event *b* if you can trace from *a* to *b* by moving forward within a process or following a message from send to receive. This captures *potential* causality, not true causality.
- **Logical clock**: A simple integer counter maintained per process — it has no relation to wall-clock time.
- **Partial ordering**: Lamport timestamps establish a partial order over events. Events in processes that never exchange messages (directly or indirectly) are **concurrent** — no ordering can be determined.
- **Clock consistency condition** (one-way): If *a* → *b*, then C(a) < C(b). The converse is **not** guaranteed — C(a) < C(b) does not imply *a* → *b*.
- **Strong clock consistency** (two-way): Achieved by vector clocks, not Lamport clocks. Vector clocks can determine: if C(a) < C(b) then *a* → *b*.
- **Contrapositive rule**: If C(a) >= C(b), then *a* did **not** happen-before *b*. This is the useful negation Lamport clocks provide.
- **Total ordering via tie-breaking**: A total order can be constructed artificially by breaking ties with process IDs, but this ordering does not imply causality.
- **Concurrent events**: Events in processes that do not exchange messages — nothing can be said about their relative order.
- **Limitations**: Lamport clocks show non-causality but do not capture all causality. Knowing *a* → *c* and *b* → *c* proves *c* did not cause *a* or *b*, but cannot determine whether *a* or *b* initiated *c*.

## Commands and Syntax

**Sending algorithm:**
```
time = time + 1;        # increment before the event
send(message, time);    # attach timestamp to message
```

**Receiving algorithm:**
```
(message, timestamp) = receive();
time = max(timestamp, time) + 1;   # sync then increment
```

**Three rules of the algorithm:**
1. Increment counter before each local event (including sends)
2. Include counter value in every sent message
3. On receive: set counter to `max(local_counter, message_timestamp) + 1`

## Relationships

- **Vector clocks** generalize Lamport timestamps to track causality per-process, providing the strong clock consistency condition that Lamport clocks lack
- **Matrix clocks** further extend vector clocks by tracking each process's knowledge of every other process's knowledge
- **Version vectors** apply similar logical clock concepts to data versioning in replicated systems
- **Happened-before relation** (Lamport, 1978) is the theoretical foundation that Lamport timestamps implement numerically
- **Clock synchronization** — Lamport timestamps exist precisely because physical clock synchronization is impractical in distributed systems
- **Information protocols** (Singh, 2011) offer an alternative based on true causality and application semantics rather than potential causality, enabling use of unordered transports like UDP

## Exam-Relevant Points

- The implication is **one-way only**: *a* → *b* implies C(a) < C(b), but C(a) < C(b) does **not** imply *a* → *b). This is the single most important distinction to understand.
- Two events with the same timestamp are possible across different processes — tie-breaking with process ID creates a total order but not a causal one.
- Each local event requires at least one tick to guarantee unique timestamps within a process.
- On message receipt, the counter is set to `max(local, received) + 1` — not just incremented.
- Lamport clocks cannot distinguish between "a caused b" and "a and b are concurrent but happen to have ordered timestamps" — vector clocks are needed for that.
- Replaying events for crash recovery requires causal relationships that Lamport clocks alone cannot fully provide.
- The seminal paper is Lamport, "Time, Clocks, and the Ordering of Events in a Distributed System" (1978), Communications of the ACM.
