---
source: sources/wiki-Stable_storage.md
source_url: https://en.wikipedia.org/wiki/Stable_storage
---

## Stable Storage: Atomicity Guarantees for Write Operations

Stable storage is a classification of computer data storage technology that guarantees atomicity for any given write operation, enabling software to be written that is robust against hardware and power failures. The core invariant is that reading back a just-written portion of disk must return either the new write data or the data that existed before the write — never corrupted or partial data.

## Key Concepts

- **Stable storage** guarantees atomicity: a write is all-or-nothing from the reader's perspective.
- **Atomicity requirement**: on read-back, the subsystem must return either the new data or the prior data — never a torn or corrupted intermediate state.
- Most conventional disk drives are **not** stable storage because they do not guarantee atomic writes; a read after write could return an error rather than either the old or new data.
- Stable storage is a foundation for building **robust** (fault-tolerant) software that can recover correctly from hardware and power failures.

## Commands and Syntax

No specific commands or configuration syntax — stable storage is an architectural property achieved through hardware (RAID) or software techniques, not a user-facing command interface.

## Implementation Techniques

- **Dual-write (software technique)**: Writing data to two separate areas of the same disk in a specific protocol. Can be implemented in application software. Only protects against certain internal media failures (e.g., bad sectors) on a single disk.
- **Disk mirroring via RAID** (level 1 or greater): The most common approach. A RAID controller implements disk-writing algorithms that make separate physical disks act collectively as stable storage. Robust against single disk failure in an array, providing stronger guarantees than the software dual-write technique.

## Relationships

- **Atomicity (database systems)**: Stable storage provides the atomic write primitive that databases depend on for crash recovery and transaction durability (the "D" in ACID).
- **RAID**: The primary implementation mechanism; RAID levels 1+ provide the redundancy needed.
- **Disk mirroring**: A specific RAID technique (level 1) directly tied to stable storage.
- **Computer data storage**: Stable storage is a classification within the broader storage taxonomy, distinguished by its atomicity guarantee.
- **Robustness / fault tolerance**: Stable storage enables software-level robustness against hardware and power failures.
- **Write-ahead logging (WAL)**: Databases use WAL protocols that assume stable storage semantics to guarantee recoverability.

## Exam-Relevant Points

- **Definition**: Stable storage guarantees that a read after a write returns either the new data or the old data — never corrupted or partial results.
- **Standard disks are NOT stable storage** — they can return errors on read-back rather than old or new data.
- **Two implementation approaches**: software dual-write (same disk, two locations) vs. RAID mirroring (separate disks). Know the tradeoff: dual-write protects against bad sectors; RAID protects against entire disk failures.
- **RAID level 1 or greater** is required for stable storage via mirroring.
- The concept is foundational to crash recovery in databases — without stable storage guarantees, recovery protocols cannot ensure correctness.
