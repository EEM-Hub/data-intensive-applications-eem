---
source: sources/wiki-Vector_clock.md
source_url: https://en.wikipedia.org/wiki/Vector_clock
---

## Vector Clocks: Causality Detection in Distributed Systems

Vector clocks are a data structure for determining the partial ordering of events in a distributed system and detecting causality violations. A vector clock for a system of *n* processes is an array of *n* logical clocks — one per process. Each process maintains its own clock and tracks the largest known value of every other process's clock. Unlike scalar Lamport timestamps, vector clocks can distinguish between causally related and concurrent events.

## Key Concepts

- **Structure**: An array of *n* logical clocks (one per process) maintained by each process in the system
- **Partial ordering**: Vector clocks establish a partial order — some event pairs are comparable (causally related), others are not (concurrent)
- **Comparison rule**: VC(x) < VC(y) iff every component of VC(x) is ≤ the corresponding component of VC(y), AND at least one component is strictly less
- **Causality detection**: If event x happened before event y (x → y), then VC(x) < VC(y). If neither VC(x) < VC(y) nor VC(y) < VC(x), the events are concurrent
- **Asymmetry**: If VC(a) < VC(b), then it is NOT the case that VC(b) < VC(a)
- **Transitivity**: If VC(a) < VC(b) and VC(b) < VC(c), then VC(a) < VC(c)
- **Consistency with real time**: If VC(a) < VC(b), then RT(a) < RT(b) (real time agrees)
- **Consistency with Lamport timestamps**: If VC(a) < VC(b), then C(a) < C(b)
- **Byzantine limitation**: Vector clocks are ineffective under Byzantine failures — causality detection is fundamentally impossible when processes behave arbitrarily or maliciously

## Commands and Syntax

**Clock update algorithm:**

1. **Initialize**: All clocks start at zero
2. **Internal event** at process *i*: Increment own clock — `VC_i[i] ← VC_i[i] + 1`
3. **Send message** from process *i*: Increment own clock, then send `(message, copy of VC_i)`
4. **Receive message** `(m, VC_j)` at process *i*:
   - Increment own clock: `VC_i[i] ← VC_i[i] + 1`
   - Merge: `VC_i[k] ← max(VC_i[k], VC_j[k])` for all *k*

**Concurrency test** (not explicitly a command, but the key operation):
- Events *a* and *b* are concurrent if neither `VC(a) < VC(b)` nor `VC(b) < VC(a)`

## Relationships

- **Lamport timestamps**: Vector clocks generalize scalar Lamport timestamps (1978). Lamport timestamps provide total order but cannot detect concurrency; vector clocks provide partial order and can
- **Version vectors**: Related but distinct — version vectors track data versions for conflict detection in replicated storage, while vector clocks track event causality
- **Matrix clocks** (Wuu & Bernstein, 1984): Extension where each process maintains a matrix of vector clocks, enabling estimation of minimum global knowledge and safe log truncation / garbage collection
- **Interval Tree Clocks** (Almeida et al., 2008): Generalization for dynamic systems where process count and identities are unknown in advance
- **Bloom Clocks** (Ramabaja, 2019): Probabilistic alternative using Bloom filters — fixed space per node regardless of system size, but with possible false positives on ordering
- **Chain Clocks** (Agarwal & Garg, 2005): Use vectors smaller than the number of processes, adapt to dynamic process counts
- **Plausible Clocks** (Torres-Rojas & Ahamad, 1999): Constant-size alternative that may incorrectly order concurrent events

## Exam-Relevant Points

- Vector clocks use O(n) space per process where n is the number of processes — a key scalability limitation
- The merge operation on receive is element-wise maximum, NOT addition
- The send operation increments the sender's own clock ONCE (not twice — the increment and the send are the same event)
- Vector clocks can detect concurrency; Lamport timestamps cannot — this is the critical advantage
- Two events are concurrent iff their vector clocks are incomparable (neither is less than the other)
- Vector clocks are strictly stronger than Lamport timestamps: VC(a) < VC(b) implies C(a) < C(b), but not vice versa
- Canonically attributed to Fidge and Mattern (both 1988, independently), though the concept appeared in at least 6 earlier papers from 1982–1987
- Vector clocks fail under Byzantine fault models — this is a fundamental impossibility, not just an implementation gap
- Modern applications include cross-shard transaction validation (e.g., Cerberus protocol) without relying on wall-clock time
