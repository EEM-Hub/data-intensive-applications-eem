---
source: sources/wiki-Commit_data_management.md
source_url: https://en.wikipedia.org/wiki/Commit_(data_management)
---

## Commit Protocols in Distributed Data Management

This page covers the concept of **commit** in data management — the mechanism that marks the end of a transaction and enforces ACID guarantees. It traces the evolution of commit protocols from single-node transaction management in the 1970s through distributed two-phase commit, three-phase commit, presumed commit/abort optimizations, optimistic commit for mobile environments, and modern integration with blockchain consensus mechanisms.

## Key Concepts

- **Commit** marks a transaction as permanent; the opposite is **rollback**, which discards tentative changes.
- Commits enforce **ACID properties**: Atomicity, Consistency, Isolation, Durability.
- A **commit log** (transaction log) records submissions for failure recovery and consistency.
- **Two-Phase Commit (2PC)**: Preparation phase (coordinator asks all participants if ready) followed by commit phase (global commit if all agree, global rollback if not). Proposed by Jim Gray (1978). Simple and widely used but **blocking** — a failed node can stall the entire transaction indefinitely.
- **Three-Phase Commit (3PC)**: Adds a **pre-commit phase** between preparation and commit, plus a **timeout mechanism**. Non-blocking — avoids indefinite waits from single-point failures. Trades additional message overhead for improved reliability.
- **Presumed Commit (PC)**: Assumes transactions will succeed by default; only notifies on rollback. Reduces message and logging overhead for the normal (success) case.
- **Presumed Abort (PA)**: Assumes transactions will fail by default; only commits when all nodes explicitly agree. Better for low-success-probability or infrequently-updated transactions.
- **Optimistic Commit Protocol**: Allows transactions to temporarily access uncommitted data to avoid blocking waits. Requires **compensating transactions** if the transaction ultimately fails. Designed for mobile/unstable network environments. Proposed by Levy et al. (1991).
- **Compensating transactions**: Special transactions that undo the effects of a failed optimistic transaction, restoring data consistency without cascading aborts.

## Commands and Syntax

No specific CLI commands are described. The page covers protocol concepts rather than implementation syntax. Key protocol flows:

- **2PC flow**: Coordinator sends `PREPARE` → participants reply `READY/ABORT` → coordinator sends `COMMIT` or `ROLLBACK`
- **3PC flow**: Coordinator sends `PREPARE` → participants reply `READY` → coordinator sends `PRE-COMMIT` → participants acknowledge → coordinator sends `COMMIT`
- **Recovery mechanisms**: **Redo** (re-execute committed operations from log) and **Undo** (reverse uncommitted operations from log)

## Relationships

- **ACID properties** — commit is the mechanism that delivers atomicity and durability guarantees
- **Transaction processing** — commit is the terminal operation in a transaction lifecycle
- **Distributed computing** — commit protocols coordinate state across multiple nodes
- **Consensus mechanisms** — blockchain consensus (e.g., Hyperledger Fabric) merges commit protocols with Byzantine fault tolerance
- **Logging and recovery** — write-ahead logs enable redo/undo after failures
- **Rollback** — the inverse of commit; undoes tentative changes
- **IBM R* database** — pioneered Presumed Commit and Presumed Abort protocols in practice
- **Atomic commit** — the broader concept that commit protocols implement

## Exam-Relevant Points

- **2PC is blocking**: if the coordinator fails after sending PREPARE but before sending COMMIT/ROLLBACK, participants are stuck waiting indefinitely.
- **3PC solves blocking** by adding a pre-commit phase and timeout mechanism, but at the cost of additional message overhead.
- **Presumed Commit reduces overhead** for the success path; **Presumed Abort reduces overhead** for the failure path. PC and PA were introduced by IBM's R* system (Mohan, Lindsay, Obermarck, 1986).
- **Optimistic commit** trades strict isolation for availability — it allows reading uncommitted data but requires compensating transactions on failure to achieve **semantic atomicity**.
- **Redo vs. Undo recovery**: redo re-applies committed transactions after a crash; undo reverses uncommitted transactions. Both rely on the transaction log.
- **Jim Gray** proposed 2PC in 1978 — foundational figure in transaction management.
- **Timeout mechanism** in 3PC: if waiting exceeds a threshold, the system automatically rolls back and releases resources.
- Commit protocols in **blockchain** integrate with consensus mechanisms to ensure tamper-resistance and consistency across decentralized nodes (e.g., Hyperledger Fabric embeds consensus into transaction verification).
- **Compensating transactions** are independent and persistent — they can execute even after system crashes, avoiding cascading aborts.
