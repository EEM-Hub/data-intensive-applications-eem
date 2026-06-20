---
source: sources/wiki-Durability_database_systems.md
source_url: https://en.wikipedia.org/wiki/Durability_(database_systems)
---

## Durability in Database Systems

Durability is the "D" in ACID, guaranteeing that once a transaction is committed, its effects survive permanently — even through crashes, power outages, and catastrophic hardware failures. A durable system must tolerate three failure classes: transaction failures (application-level aborts), system failures (volatile memory loss), and media failures (non-volatile storage damage). The system must ensure committed transactions are resilient (their effects survive) while incomplete transactions are recoverable (their partial changes can be undone).

## Key Concepts

- **Durability** guarantees committed transaction effects persist permanently, regardless of subsequent failures
- **Three failure types** a durable system must tolerate:
  - **Transaction failure**: interrupted execution due to errors, cancellation, timeouts, or constraint violations
  - **System failure**: loss of volatile storage contents (crashes, power outages, out-of-memory)
  - **Media failure**: loss of non-volatile storage (disk failures, hardware damage)
- **Resilience**: committed transactions survive failures (possibly via reconstruction)
- **Recoverability**: incomplete transactions can be rolled back without affecting database state
- **Serializability** at the transaction level allows distinguishing committed from uncommitted changes, enabling safe undo of non-committed work
- **In-place overwrites are discouraged** — systems should maintain change history (via timestamps, logging, or locking)
- **Volatile vs. non-volatile storage tradeoff**: volatile storage (RAM) is faster but vulnerable to system failures; non-volatile storage (disk/SSD) is slower but survives crashes
- **Stable memory**: an idealized failure-resistant memory achieved through replication and robust write protocols
- **Jim Gray (1981)** formally proposed the concept of system reliability encompassing durability, linking it to atomicity and consistency

## Commands and Syntax

No specific CLI commands, but key mechanisms and protocols:

- **Write-Ahead Log (WAL)**: Buffer changes to non-volatile storage *before* acknowledging commit. On recovery:
  1. Replay log to **redo** committed transactions
  2. **Undo** operations from non-committed transactions
  3. Re-execute incomplete transactions that should have committed
- **Two-Phase Commit Protocol (2PC)**: Coordinates distributed transaction commits across multiple nodes — all nodes must agree before commit is acknowledged
- **ARIES (Algorithms for Recovery and Isolation Exploiting Semantics)**: Widely adopted recovery algorithm family for distributed databases, supporting fine-granularity locking and partial rollbacks
- **Recovery optimization techniques**: Incremental dumping, differential files, and checkpoints reduce the cost of log-based state reconstruction

## Relationships

- **ACID properties**: Durability is one of four; closely tied to **atomicity** (transactions as unit of work) and **consistency** (valid state transitions). Reliability mechanisms require primitives for transaction begin, end, and rollback — shared with atomicity
- **Write-Ahead Logging (WAL)**: The primary mechanism enabling system-level durability; logs must be flushed to non-volatile storage before commit acknowledgment
- **Replication and redundancy**: Enable media-level durability by creating stable memory abstractions (e.g., RAID mirroring)
- **Distributed transactions**: Require coordination protocols (2PC) and distributed recovery algorithms (ARIES) to maintain durability guarantees across nodes
- **Backup and disaster recovery**: Offline copies provide last-resort durability against catastrophic media failure
- **Non-volatile memory (NVM)**: Emerging technology that may blur the volatile/non-volatile boundary, potentially simplifying durability mechanisms
- **Serializability and isolation**: Enable transaction-level durability by allowing the system to distinguish and discard uncommitted changes

## Exam-Relevant Points

- Durability requires tolerating **three failure levels**: transaction, system, and media — know examples of each
- **WAL (Write-Ahead Logging)** is the core mechanism for system-level durability: changes are logged to non-volatile storage *before* being applied, enabling redo of committed and undo of uncommitted transactions
- **Two-phase commit (2PC)** is required for durability in distributed databases — a single node cannot unilaterally commit
- **ARIES** is the standard recovery algorithm family for distributed database durability
- **Stable memory** is achieved through replication, not through any single physical device
- Recovery involves both **redo** (reapply committed transactions) and **undo** (reverse uncommitted transactions)
- **Checkpoints, incremental dumps, and differential files** optimize recovery by avoiding full log replay
- In-place updates without history are **not durable** — change tracking (logging, timestamps) is essential
- Jim Gray's 1981 "The Transaction Concept" paper is the foundational reference for reliability in transaction-based systems
- Durability is distinct from but dependent on atomicity — atomicity provides the transaction boundary that durability preserves
