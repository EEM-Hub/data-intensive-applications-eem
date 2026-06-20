---
source: sources/wiki-Distributed_transaction.md
source_url: https://en.wikipedia.org/wiki/Distributed_transaction
---

## Distributed Transactions

Distributed transactions operate across multiple nodes in a distributed environment, ensuring that a transaction spanning several networked resources completes entirely or not at all. This page covers the fundamental mechanisms, standards, and challenges of coordinating transactions across distributed databases and services, including both short-lived and long-lived transaction patterns.

## Key Concepts

- A **distributed transaction** executes across multiple nodes in a network; atomicity guarantees all-or-nothing completion
- Distributed transactions are not limited to databases — they apply to any transactional resource in a distributed environment
- When spanning multiple databases, the transaction must maintain **ACID properties** across all participants
- The **isolation** property is especially challenging: **global serializability** can be violated even when each individual database provides local serializability
- **Strong strict two-phase locking (SS2PL)** is used by most commercial databases for concurrency control and ensures global serializability when all participants employ it
- **Long-lived distributed transactions** (e.g., booking a trip involving flight, car, hotel) cannot use 2PC because holding locks for hours or days is impractical
- Long-lived transactions use **compensating transactions**, optimism, and isolation without locking — analogous to cancelling a hotel reservation to "undo" a step
- The **X/Open XA** standard (from The Open Group) is the de facto standard for distributed transaction processing but does not cover long-lived transactions

## Commands and Syntax

No specific CLI commands. The key protocol is:

- **Two-Phase Commit (2PC)**: The standard algorithm for short-lived distributed transactions
  - **Phase 1 (Prepare)**: Coordinator asks all participants if they can commit
  - **Phase 2 (Commit/Abort)**: If all agree, coordinator sends commit; otherwise, abort
  - Suitable for transactions that complete in milliseconds to minutes

- **Synchronization in event-driven architectures** uses request-response patterns:
  - **Dual-queue approach**: Separate request and reply queues; producer waits for response
  - **Ephemeral queue approach**: One dedicated temporary queue per request

## Relationships

- **Atomicity** — the foundational guarantee that distributed transactions must provide
- **ACID properties** — distributed transactions must synchronize these across all participating databases
- **Two-phase commit (2PC)** — the primary coordination algorithm for short-lived distributed transactions
- **Compensating transactions** — the undo mechanism for long-lived distributed transactions where 2PC is impractical
- **Global serializability** — the correctness criterion that can break across multiple databases even when each is individually serializable
- **Concurrency control / SS2PL** — the locking mechanism that ensures global serializability in practice
- **X/Open XA** — the industry standard transaction processing model
- **Event-driven architecture** — alternative synchronization approach using message queues
- **Web services** — the typical implementation substrate for long-lived distributed transactions
- Technologies: **Jakarta Enterprise Beans (EJB)** and **Microsoft Transaction Server (MTS)** provide full distributed transaction support

## Exam-Relevant Points

- 2PC is designed for **short-lived** transactions (milliseconds to minutes) — it is not suitable for long-lived transactions because it holds locks too long
- Global serializability can be violated even when every individual database provides serializability — this is a critical distinction
- SS2PL ensures global serializability **only if all participating databases employ it**
- Long-lived distributed transactions use **compensating transactions** (not 2PC) — know the difference
- X/Open XA is the de facto standard but **does not cover** long-lived distributed transactions
- In event-driven architectures, distributed transaction synchronization can use either dual queues (request + reply) or ephemeral per-request queues
- Distributed transactions are **not limited to databases** — any distributed transactional resource qualifies
