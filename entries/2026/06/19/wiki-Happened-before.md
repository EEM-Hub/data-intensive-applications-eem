---
source: sources/wiki-Happened-before.md
source_url: https://en.wikipedia.org/wiki/Happened-before
---

## Lamport's Happened-Before Relation in Distributed Systems

The happened-before relation (denoted `→`) is a foundational concept in distributed systems, formulated by Leslie Lamport in 1978. It defines a partial ordering of events based on potential causal relationships, ensuring that if one event should logically precede another, the result reflects that ordering — even if events are physically executed out of order. It is the theoretical basis for reasoning about time and causality in asynchronous distributed systems.

## Key Concepts

- **Happened-before (`→`)** is the least strict partial order on events satisfying two base rules plus transitivity.
- **Rule 1 — Same process:** If events `a` and `b` occur on the same process and `a` occurs before `b`, then `a → b`.
- **Rule 2 — Message passing:** If `a` is the sending of a message and `b` is the reception of that same message, then `a → b`.
- **Concurrency:** If two events are in different processes that do not exchange messages (directly or indirectly), they are **concurrent** — neither `a → b` nor `b → a` holds.
- **Strict partial order properties:**
  - **Transitive:** if `a → b` and `b → c`, then `a → c`.
  - **Irreflexive:** no event can happen before itself (`a ↛ a`).
  - **Asymmetric:** if `a → b`, then `b ↛ a` (follows from transitivity + irreflexivity by contradiction).
- **Causal vs. concurrent:** The relation captures *potential* causality, not physical time. Two events are concurrent when no causal chain connects them.
- **Language-level analogue:** In Java, C, C++, and Rust, a "happens-before" edge means a memory write by statement A is visible to statement B (A completes its write before B starts its read). This is the basis of their memory models.
- **Byzantine impossibility:** Under Byzantine faults, it is fundamentally impossible to detect the happened-before relation, because Byzantine processes can forge or manipulate causal metadata.

## Commands and Syntax

No CLI commands per se — this is a theoretical concept. However, the relation is operationalized through clock mechanisms:

- **Lamport clocks:** Each process maintains a counter; on send, attach counter; on receive, set counter to `max(local, received) + 1`. If `a → b`, then `L(a) < L(b)`, but the converse does not hold.
- **Vector clocks:** Each process maintains a vector of counters (one per process). Provides exact happened-before detection: `a → b` iff `VC(a) < VC(b)` component-wise.

## Relationships

- **Logical clocks / Lamport timestamps:** The mechanism that makes the happened-before relation observable to processes; without a logical clock, processes have no knowledge of causal order.
- **Vector clocks:** Extend Lamport clocks to precisely capture the happened-before relation (not just one direction of the implication).
- **Mutual exclusion:** Happened-before ordering enables distributed mutual exclusion algorithms (e.g., Lamport's bakery-style algorithm for distributed locks).
- **Consistent global snapshots:** Snapshot algorithms (e.g., Chandy-Lamport) rely on happened-before to define consistency — a snapshot is consistent if no captured event happened-before a non-captured event that causally precedes it.
- **Race conditions:** Two concurrent accesses to shared state with no happened-before ordering constitute a data race.
- **Memory models (Java, C++, Rust):** The happens-before relation is the formal backbone of language memory models, determining which writes are visible to which reads.
- **Byzantine fault tolerance:** BFT protocols cannot rely on happened-before detection since Byzantine nodes can forge causal metadata.

## Exam-Relevant Points

- The happened-before relation is a **strict partial order** (transitive, irreflexive, asymmetric) — not a total order. Know why each property holds.
- Two events are **concurrent** if and only if neither happened before the other. Concurrency does not mean "simultaneous" — it means "causally unrelated."
- **Lamport clocks** satisfy `a → b ⟹ L(a) < L(b)` but **not** the converse; **vector clocks** satisfy the biconditional.
- Without a logical clock mechanism, processes in a distributed system **cannot determine** the happened-before relation.
- The original paper is Lamport 1978, "Time, Clocks, and the Ordering of Events in a Distributed System" — one of the most cited papers in distributed systems.
- Under **Byzantine faults**, happened-before detection is provably impossible (Misra & Kshemkalyani, 2022).
- The relation can be extended with additional causal rules (e.g., process creation → first event in that process).
- Asymmetry is **not an independent axiom** — it is derived from transitivity + irreflexivity by contradiction (a common exam proof question).
