---
source: sources/wiki-Database_transaction.md
source_url: https://en.wikipedia.org/wiki/Database_transaction
---

## Database Transactions

A database transaction is a unit of work performed within a database management system (DBMS) that is treated as a single, coherent, and reliable operation independent of other transactions. Transactions serve two fundamental purposes: providing reliable units of work that allow correct recovery from failures while keeping the database consistent, and providing isolation between programs accessing a database concurrently.

## Key Concepts

- A transaction represents any change in a database and may consist of multiple operations treated as a single logical unit
- Transactions must satisfy the **ACID** properties: **Atomic** (all-or-nothing), **Consistent** (conforms to database constraints), **Isolated** (does not affect other transactions), **Durable** (persisted to storage)
- A **transactional database** is a DBMS that provides ACID properties for a bracketed set of operations (begin-commit)
- The highest isolation level is **serializability**, which guarantees concurrent transaction effects are equivalent to serial execution
- **Nested transactions** contain statements that start sub-transactions within them
- **Multi-level transactions** are a variant where sub-transactions operate at different levels of a layered system architecture (e.g., database-engine level vs. operating-system level)
- **Compensating transactions** undo the effects of a previously committed transaction
- **Distributed transactions** access data over multiple nodes while enforcing ACID properties across all of them; typically require a coordinating entity
- Autocommit, if disabled at transaction start, is re-enabled when the transaction ends

## Commands and Syntax

- **Begin a transaction**: `BEGIN` (or SQL standard `START TRANSACTION`)
- **Commit**: `COMMIT` — persists all results of data manipulations within the transaction scope
- **Rollback**: `ROLLBACK` — discards all partial results, leaving the database unchanged
- **Set isolation level**: can be set per-transaction or globally
  - `READ COMMITTED` — changes invisible to others until transaction ends
  - `READ UNCOMMITTED` — changes immediately visible (highest concurrency, lowest isolation)
- Standard transaction pattern:
  1. Begin the transaction
  2. Execute data manipulations and/or queries
  3. If no error: commit
  4. If error: rollback

## Relationships

- **ACID properties** — transactions are the mechanism that enforces atomicity, consistency, isolation, and durability
- **Concurrency control** — transactions provide the isolation guarantees needed when multiple programs access a database simultaneously
- **Isolation levels** — define the degree to which transactions are isolated from each other (READ UNCOMMITTED through SERIALIZABLE)
- **Distributed systems** — distributed transactions extend ACID across multiple nodes, relevant to cloud-based data stores and Storage as a Service (StaaS)
- **Recovery and fault tolerance** — transactions enable correct recovery from system failures by guaranteeing all-or-nothing semantics
- **Double-entry bookkeeping** — classic analogy: a debit and its corresponding credit must both succeed or both fail
- **Transactional filesystems** — the transaction concept extends beyond databases (e.g., Reiser4, NTFS distributed transactions)
- **SQL** — the standard language for expressing transactions in relational databases
- **NoSQL databases** — increasingly support transactions alongside their scalability focus

## Exam-Relevant Points

- A transaction must be **atomic** — partial commits are never allowed; either all changes persist or none do
- ACID stands for Atomicity, Consistency, Isolation, Durability — know each property's definition
- The two main purposes of transactions: (1) reliable recovery from failures, (2) isolation between concurrent programs
- `BEGIN`/`START TRANSACTION`, `COMMIT`, and `ROLLBACK` are the core transaction control statements
- Serializability is the **highest** isolation level — equivalent to serial execution
- `READ UNCOMMITTED` is the **lowest** isolation level — allows dirty reads but maximizes concurrency
- A transaction ID (XID) is used internally to store and process transactions
- Distributed transactions enforce ACID across multiple nodes and require a coordinator
- MySQL's InnoDB supports transactions; MyISAM does **not**
- In no case can a partial transaction be committed — this would leave the database inconsistent
- Object databases and relational databases share the same fundamental transaction semantics: start, then commit or rollback atomically
