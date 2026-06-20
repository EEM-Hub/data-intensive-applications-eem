---
source: sources/wiki-Two-phase_locking.md
source_url: https://en.wikipedia.org/wiki/Two-phase_locking
---

## Two-Phase Locking (2PL) — Pessimistic Concurrency Control

Two-phase locking (2PL) is a pessimistic concurrency control method used in databases and transaction processing that guarantees conflict-serializability. It governs how transactions acquire and release locks on data items, ensuring that concurrent transactions produce results equivalent to some serial execution order. The protocol divides each transaction's lock management into two distinct phases: an expanding phase where locks are only acquired, and a shrinking phase where locks are only released.

## Key Concepts

- **Two-Phase Locking Rule**: A transaction must never acquire a lock after it has released any lock. This single invariant guarantees conflict-serializability.
- **Expanding (Growing) Phase**: Locks are acquired; no locks are released. The number of held locks can only increase.
- **Shrinking (Contracting) Phase**: Locks are released; no locks are acquired. The number of held locks can only decrease.
- **Read-lock (Shared lock)**: Required to read an object. Multiple transactions can hold read-locks on the same object simultaneously.
- **Write-lock (Exclusive lock)**: Required to write an object. No other lock (read or write) can be held on the same object by another transaction.
- **Lock compatibility matrix**: Read-read is compatible; read-write and write-write are incompatible (blocked).
- **Deadlocks**: 2PL, S2PL, and SS2PL are all susceptible to deadlocks due to mutual blocking. Only C2PL eliminates deadlocks.
- **Conflict-serializability**: All 2PL variants guarantee this. All conflict-serializable schedules are also view-serializable (but not vice versa).

## Variants

- **Basic 2PL**: Guarantees conflict-serializability only. Does not guarantee recoverability, strictness, or prevent phantom/dirty reads.
- **Conservative 2PL (C2PL)**: Transaction acquires all locks before execution begins. Prevents deadlocks but requires declaring the full read/write set upfront, which is often impractical. Rarely used in practice.
- **Strict 2PL (S2PL)**: Write (exclusive) locks held until transaction commits or aborts; read (shared) locks released during the shrinking phase. Guarantees recoverability, strictness, and prevents phantom and dirty reads. Not suitable for B-tree indexes due to bottlenecks from holding locks on root nodes.
- **Strong Strict 2PL (SS2PL / Rigorous 2PL)**: Both read and write locks held until transaction ends. Effectively has no shrinking phase until commit/abort. Every SS2PL schedule is also S2PL, but not vice versa. Provides the strongest guarantees.

## Commands and Syntax

No specific commands — 2PL is a protocol implemented internally by database engines. The key operational rules are:

- Before reading object X: acquire read-lock(X)
- Before writing object X: acquire write-lock(X)
- After the first lock release, no new locks may be acquired (basic 2PL)
- For S2PL: hold write-locks until COMMIT or ABORT
- For SS2PL: hold all locks until COMMIT or ABORT
- For C2PL: acquire all needed locks atomically before any execution

## Relationships

- **Concurrency control**: 2PL is one of several concurrency control methods; contrasts with optimistic approaches (OCC) and MVCC
- **Serializability**: 2PL guarantees conflict-serializability, a subset of view-serializability
- **Deadlocks**: Mutual lock blocking can cause deadlocks, requiring detection (wait-for graphs) or prevention (C2PL, timeouts)
- **Two-phase commit (2PC)**: Distinct protocol — 2PC is about distributed commit consensus, not locking; the "two phases" are unrelated
- **Transaction isolation levels**: S2PL and SS2PL effectively implement SERIALIZABLE isolation
- **B-trees**: S2PL causes bottlenecks in B-tree traversal since parent nodes must be locked; specialized protocols like lock coupling are used instead
- **Recovery**: S2PL and SS2PL provide strictness, which simplifies crash recovery by ensuring uncommitted writes are never visible

## Exam-Relevant Points

- The fundamental 2PL rule: **no lock may be acquired after any lock has been released**
- Basic 2PL guarantees conflict-serializability but **not** recoverability or strictness
- **C2PL is the only variant that prevents deadlocks** — it requires all locks upfront
- S2PL holds **write locks until commit/abort** but releases read locks early
- SS2PL holds **all locks until commit/abort** — strongest guarantees, simplest to reason about
- SS2PL ⊂ S2PL ⊂ 2PL (every SS2PL schedule is S2PL; every S2PL schedule is 2PL)
- Lock compatibility: shared-shared is OK; any combination involving an exclusive lock blocks
- **Do not confuse 2PL with 2PC** — two-phase locking is concurrency control; two-phase commit is distributed transaction consensus
- C2PL is rarely used because transactions must declare their complete read/write set in advance
- All 2PL variants (except C2PL) are subject to deadlocks
