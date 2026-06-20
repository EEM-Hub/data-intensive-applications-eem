---
source: sources/wiki-Linearizability.md
source_url: https://en.wikipedia.org/wiki/Linearizability
---

## Linearizability in Concurrent Systems

Linearizability is a correctness condition for concurrent programming, introduced by Herlihy and Wing in 1987. It guarantees that even though operations on shared objects may overlap in time, each operation appears to take effect instantaneously at some point between its invocation and response. This provides the strongest practical consistency model for reasoning about concurrent systems, and is often used interchangeably with the term "atomic."

## Key Concepts

- **Linearizability** means a concurrent history can be reordered into a valid sequential history while preserving the real-time ordering of non-overlapping operations
- **Linearization point**: the single instant between invocation and response at which an operation appears to take effect; proving linearizability reduces to identifying these points
- **History**: an ordered sequence of invocation and response events on a shared object by multiple threads/processes
- **Sequential history**: a history where every invocation is immediately followed by its response (no concurrency)
- A history is linearizable if: (1) it can be reordered into a correct sequential history (serializability), and (2) if op1's response precedes op2's invocation, op1 must precede op2 in the reordering (real-time order preservation)
- **Linearizability vs. serializability**: serializability allows arbitrary reordering of operations; linearizability additionally requires that the real-time order of non-overlapping operations is preserved
- **Composability**: linearizability composes — multiple individually linearizable objects remain linearizable when considered together; serializability does not have this property
- An **object** is linearizable if all valid histories of its use can be linearized
- Linearizability is a **safety property** — it ensures operations do not produce unexpected results

## Commands and Syntax

**Primitive atomic instructions** (hardware-level):
- `atomic read-write` — single indivisible memory access
- `XCHG` (x86) — atomic swap
- `test-and-set` — read, test, conditionally set
- `fetch-and-add` / `fetch-and-increment` — atomically read and update
- `compare-and-swap` (CAS) — write new value only if current matches expected
- `LDREX` / `STREX` (ARM) — load-exclusive / store-exclusive using monitor
- `LDXR` / `STXR` (ARMv8-A) — 64-bit exclusive load/store
- `sig_atomic_t` (C standard) — guaranteed atomic reads/writes
- `stdatomic.h` (C11) — full atomic operations library

**CAS-based counter pattern**:
1. Read value from memory location
2. Add one to the value
3. Use compare-and-swap to write incremented value back
4. If CAS fails (value changed concurrently), retry from step 1

**Lock-based counter pattern**:
1. Acquire lock
2. Read value
3. Add one
4. Write incremented value back
5. Release lock

## Relationships

- **Serializability**: linearizability is strictly stronger — it adds real-time ordering constraints on top of serializability's requirement for a valid sequential reordering
- **ACID (Atomicity)**: the "all-or-nothing" principle in databases is the same concept; linearizability is ACID atomicity applied to individual object operations
- **Consistency models**: linearizability sits at the strong end of the consistency spectrum, stronger than sequential consistency, causal consistency, and eventual consistency
- **CRDTs (Conflict-free Replicated Data Types)**: the per-process register counter example resembles a grow-only counter CRDT
- **Transactional memory**: a hybrid approach providing linearizable semantics via critical-section-like abstractions without explicit locking
- **Lock-free and wait-free algorithms**: use atomic primitives (CAS, LL/SC) to achieve linearizability without locks, maximizing parallelism
- **Non-blocking synchronization**: CAS and fetch-and-increment enable lock-free linearizable implementations that avoid lock contention overhead

## Exam-Relevant Points

- Linearizability = serializability + real-time ordering of non-overlapping operations; this is the key distinction to remember
- Linearizability **composes** across objects; serializability does **not** — this is a major practical advantage
- The **linearization point** is the single atomic instant where an operation takes effect; for CAS-based algorithms it is the successful CAS; for lock-based algorithms it is any point while the lock is held
- The lost-update problem (two increments yielding +1 instead of +2) is the classic demonstration of why naive read-modify-write is not linearizable
- CAS and fetch-and-increment have different computational power: some algorithms require CAS and cannot be implemented with fetch-and-increment alone (Herlihy), while fetch-and-increment is more efficient (fewer memory references) for others (Fich, Hendler, Shavit 2004)
- Disabling interrupts achieves atomicity on uniprocessors but is **insufficient for multiprocessors** — each CPU can interfere independently
- `sig_atomic_t` guarantees atomic reads/writes in C but does **not** guarantee atomic increment/decrement
- ARM's `LDREX`/`STREX` will fail on context switch, requiring retry — this is by design for correctness
