---
source: sources/wiki-Atomicity_database_systems.md
source_url: https://en.wikipedia.org/wiki/Atomicity_(database_systems)
---

## Atomicity in Database Systems

Atomicity is one of the four ACID transaction properties. It guarantees that a database transaction is treated as a single indivisible unit: either all operations within the transaction complete successfully, or none of them take effect. This prevents partial updates that could leave the database in an inconsistent state.

## Key Concepts

- **Atomicity** means "undividable" — a transaction's operations are an irreducible series where all occur or none occur
- An atomic transaction is **never observable in a partial state** by another client — it either hasn't happened yet or has fully completed
- **Classic example**: bank transfer debiting account A and crediting account B — both must succeed or both must fail to prevent unaccountable credits/debits
- **Non-orthogonality with other ACID properties**: isolation relies on atomicity for rollback on deadlock; consistency relies on atomicity for rollback on constraint violations — a failure to roll back can cascade into isolation or consistency failures
- The term "atomic" also appears in **First Normal Form (1NF)**, where it means field values must not contain decomposable sub-values (different meaning from transaction atomicity)

## Commands and Syntax

- POSIX file-level atomicity primitives: `open(2)`, `flock(2)` — allow applications to atomically open or lock files
- POSIX Threads provide process-level synchronization primitives
- Hardware-level atomic operations: **Test-and-set**, **Fetch-and-add**, **Compare-and-swap (CAS)**, **Load-Link/Store-Conditional (LL/SC)**, used together with **memory barriers**

## Relationships

- **ACID properties**: Atomicity is the "A" in ACID, alongside Consistency, Isolation, and Durability — they are interdependent, not fully orthogonal
- **Logging/journaling**: databases implement atomicity via write-ahead logs; file systems use journaling (journaling file system) or read-copy-update (RCU)
- **Distributed systems**: cross-shard atomicity traditionally uses **Two-Phase Commit (2PC)**, which introduces performance bottlenecks; newer approaches like **braided synchronization** (Cerberus protocol) interleave consensus phases across shards to avoid global transaction ordering
- **Transaction processing / long-running transactions**: atomicity becomes harder to maintain as transaction scope grows; long-running transactions may use compensating transactions (sagas) instead of traditional rollback
- **First Normal Form (1NF)**: shares the term "atomic" but refers to value indivisibility in schema design, not transaction indivisibility

## Exam-Relevant Points

- Atomicity = all-or-nothing execution of a transaction's operations
- A partially completed atomic transaction is **never visible** to other clients
- Atomicity is **not orthogonal** to isolation and consistency — both depend on atomicity's rollback capability
- Implementation mechanisms: **logging/journaling** (databases), **write-ahead logs**, **RCU** (copy-before-modify)
- After crash, recovery uses synchronized logs and **ignores incomplete entries**
- Distributed atomicity via **2PC** introduces bottlenecks; **braided synchronization** is an alternative that avoids global ordering
- Hardware atomicity relies on **CAS**, **Test-and-set**, **Fetch-and-add**, **LL/SC** plus **memory barriers**
- Don't confuse transaction atomicity (all-or-nothing operations) with 1NF atomicity (indivisible field values)
