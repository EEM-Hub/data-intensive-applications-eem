---
source: sources/wiki-Serializability.md
source_url: https://en.wikipedia.org/wiki/Serializability
---

## Database Transaction Schedules and Serializability

A **schedule** (or history) is an abstract model describing the execution order of operations across a set of concurrent transactions in a database system. Schedules are the foundational formalism for reasoning about concurrency control correctness. They capture reads, writes, commits, and aborts as an ordered sequence (total or partial), and the properties of a schedule determine whether concurrent execution produces correct, recoverable results. In practice, most general-purpose databases enforce **conflict-serializable** and **strict recoverable** schedules.

## Key Concepts

- **Schedule**: An ordered list (or partial order) of operations from multiple transactions executing concurrently. Operations include R(X), W(X), Commit, Abort.
- **Serial schedule**: Transactions execute one at a time with no interleaving — trivially correct but poor for performance.
- **Serializable schedule**: Produces the same outcome as *some* serial schedule — the gold standard for correctness.
- **Conflicting actions**: Two operations conflict iff (1) they belong to different transactions, (2) at least one is a write, and (3) they access the same data object. Conflict types: read-write, write-read, write-write.
- **Conflict equivalence**: Two schedules are conflict-equivalent if they involve the same transactions with the same operations in the same per-transaction order, and all conflicting pairs are ordered identically. Equivalently, one can be transformed into the other by swapping non-conflicting operations.
- **Conflict-serializable**: A schedule is conflict-serializable iff its **precedence graph** (over committed transactions) is acyclic.
- **View equivalence**: Preserves (1) which transaction reads each initial value, (2) which transaction's write is read by each read, and (3) which transaction performs the final write on each object.
- **View-serializable**: View-equivalent to some serial schedule. Strictly weaker than conflict-serializability (allows blind writes). Determining view-serializability is **NP-complete**, so it has little practical use.
- **Blind write**: A write not preceded by a read of the same object by the same transaction — the distinguishing case between view- and conflict-serializability.
- **Recoverable schedule**: A transaction commits only after all transactions whose writes it has read have committed. Violating this makes a schedule **unrecoverable** — committed data depends on an aborted transaction.
- **Cascadeless (ACA) schedule**: No dirty reads — a transaction only reads values written by already-committed transactions. Prevents cascading aborts.
- **Strict schedule**: If T1 writes an object, no conflicting operation from T2 can occur until T1 commits or aborts. Enables efficient crash recovery. Strict => cascadeless => recoverable.
- **Materialized vs. non-materialized conflict**: A conflict is materialized only when the conflicting operation actually executes against the database (not just requested/queued).

## Commands and Syntax

**Schedule notation** (list form):
```
D = R1(X) W1(X) Com1 R2(Y) W2(Y) Com2 R3(Z) W3(Z) Com3
```
- `Ri(X)` — transaction i reads object X
- `Wi(X)` — transaction i writes object X
- `Comi` — transaction i commits

**Grid notation**: columns = transactions, rows = operations in time order.

**Precedence graph test for conflict-serializability**:
1. Create a node for each committed transaction.
2. Add directed edge Ti → Tj for each conflicting pair where Ti's operation precedes Tj's.
3. Schedule is conflict-serializable iff the graph is **acyclic** (a DAG).

**Enforcement mechanisms** for conflict serializability:
- Two-phase locking (2PL)
- Timestamp ordering
- Serializable snapshot isolation (SSI)
- Restarting any transaction involved in a cycle in the precedence graph

## Relationships

- **Containment hierarchy (serializability)**: Serial ⊂ conflict-serializable ⊂ view-serializable ⊂ all schedules
- **Containment hierarchy (recoverability)**: Serial ⊂ strict ⊂ cascadeless (ACA) ⊂ recoverable ⊂ all schedules
- **Two-phase locking** enforces conflict-serializability; **strict 2PL (SS2PL)** additionally enforces strictness.
- **Snapshot isolation** is not serializable by default; **serializable snapshot isolation (SSI)** adds conflict detection to close the gap (Cahill, Röhm, Fekete 2008).
- **Linearizability** is a more general correctness criterion from concurrent computing that subsumes serializability for single-object operations.
- **Global serializability** extends these concepts to distributed/multi-database systems.
- Conflicts are the root cause of delays (lock waits) and aborts (deadlock resolution); reducing conflicts via **commutativity** improves throughput.

## Exam-Relevant Points

- Know the three conditions for conflicting actions: different transactions, at least one write, same object. Read-read is **not** a conflict.
- The precedence graph acyclicity test is the standard method for checking conflict-serializability — expect to construct graphs and identify cycles.
- Every conflict-serializable schedule is view-serializable, but **not** vice versa. The gap is blind writes.
- View-serializability testing is **NP-complete** — this is why practical systems use conflict-serializability instead.
- A schedule can be serializable but **not recoverable** — these are orthogonal properties. Systems must enforce both.
- Strict ⊂ cascadeless ⊂ recoverable — know examples distinguishing each level. A cascadeless schedule prevents dirty reads; a strict schedule additionally prevents dirty writes.
- An **unrecoverable** schedule is one where a transaction commits after reading from a transaction that later aborts — the database cannot be restored to a consistent state.
- Cascading aborts occur when one abort forces other transactions to abort because they performed dirty reads. ACA schedules prevent this.
- Conflict equivalence can be tested by swapping adjacent non-conflicting operations from different transactions — if you can reach a serial schedule, it is conflict-serializable.
- SS2PL (strong strict two-phase locking, a.k.a. rigorousness) produces schedules that are both conflict-serializable **and** strict.
