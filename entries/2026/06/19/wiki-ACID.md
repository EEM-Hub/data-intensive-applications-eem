---
source: sources/wiki-ACID.md
source_url: https://en.wikipedia.org/wiki/ACID
---

## ACID Properties for Database Transactions

This page defines ACID — Atomicity, Consistency, Isolation, Durability — the four properties that database transactions must guarantee to ensure data validity despite errors, power failures, and crashes. It covers definitions, failure examples for each property, implementation techniques (WAL, shadow paging, locking, MVCC), and distributed transaction considerations.

## Key Concepts

- **ACID** acronym coined in 1983 by Andreas Reuter and Theo Härder, building on Jim Gray's earlier work (Gray named atomicity, consistency, and durability but not isolation)
- **Atomicity**: A transaction is an indivisible unit — it either succeeds completely or fails completely; no partial updates are visible. Prevents partial writes that could leave the database in a corrupt state.
- **Consistency**: A transaction can only bring the database from one valid state to another valid state, preserving all defined rules (constraints, cascades, triggers, referential integrity).
- **Isolation**: Concurrent transactions produce the same result as if they were executed sequentially. Isolation level determines visibility of incomplete transactions to others.
- **Durability**: Once committed, a transaction's effects persist even through system failures (power outage, crash). Achieved by writing to non-volatile memory.
- **BASE** (Basically Available, Soft state, Eventually consistent) is the conceptual opposite of ACID — prioritizes availability over consistency. Data may be temporarily inconsistent.
- ACID databases prioritize **consistency over availability**; BASE databases prioritize **availability over consistency** (linked to CAP theorem).
- IBM IMS supported ACID transactions as early as **1973**, predating the acronym.
- SQL databases (MySQL, PostgreSQL, AWS Redshift) follow the ACID model; NoSQL databases (DynamoDB, MongoDB) typically follow BASE, though some NoSQL databases exhibit certain ACID traits.

## Commands and Syntax

- Example constraint enforcing consistency:
  ```sql
  CREATE TABLE acidtest (A INTEGER, B INTEGER, CHECK (A + B = 100));
  ```
  This `CHECK` constraint ensures the invariant A + B = 100 is maintained across all transactions.

## Relationships

- **CAP Theorem**: A database leans toward either ACID (consistency) or BASE (availability); it cannot fully satisfy both. CAP theorem formalizes this trade-off.
- **Concurrency Control**: Isolation is the main goal of concurrency control mechanisms. Two major approaches:
  - **Locking / Two-Phase Locking (2PL)**: Transactions acquire locks on data before access; other transactions must wait. Guarantees full isolation but introduces overhead and blocking.
  - **Multiversion Concurrency Control (MVCC)**: Readers see a prior consistent snapshot while writers modify data. Readers don't block writers and vice versa. Snapshot isolation is one MVCC implementation that relaxes isolation slightly.
- **Write-Ahead Logging (WAL)**: Durability technique — prospective changes written to a persistent log before modifying the database, enabling crash recovery.
- **Shadow Paging**: Alternative durability technique — updates applied to a partial copy; the new copy is activated on commit.
- **Two-Phase Commit Protocol (2PC)**: Provides atomicity for distributed transactions across multiple nodes. Phase 1: coordinator asks participants if prepared; Phase 2: coordinator commits only if all agree. Distinct from two-phase locking.
- **Distributed Transactions**: ACID guarantees become harder across distributed databases due to network failures and partial node failures.
- **Eventual Consistency**: The consistency model used by BASE systems, contrasting with ACID's immediate consistency.

## Exam-Relevant Points

- Know each ACID property's exact definition and what failure looks like when it is violated (the page gives concrete failure scenarios for each)
- **Atomicity failure**: partial updates visible (e.g., money debited but not credited)
- **Consistency failure**: invariant violated (e.g., A + B != 100 after transaction)
- **Isolation failure**: write-write conflict from interleaved transactions causing unrecoverable state
- **Durability failure**: committed transaction lost because changes were only in disk buffer when power failed
- Distinguish **two-phase commit** (distributed transaction protocol for atomicity) from **two-phase locking** (concurrency control protocol for isolation)
- MVCC allows **readers to not block writers** and vice versa — a key distinction from lock-based approaches
- ACID vs BASE is framed by the **CAP theorem** trade-off between consistency and availability
- SQL databases = ACID model; NoSQL databases = typically BASE (but some NoSQL can exhibit ACID traits)
- WAL ensures durability by writing to a **persistent log before** modifying the database
