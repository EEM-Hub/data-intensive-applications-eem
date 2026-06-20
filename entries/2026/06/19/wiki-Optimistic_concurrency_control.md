---
source: sources/wiki-Optimistic_concurrency_control.md
source_url: https://en.wikipedia.org/wiki/Optimistic_concurrency_control
---

## Optimistic Concurrency Control (OCC)

Optimistic concurrency control is a non-locking concurrency control method for transactional systems. It allows transactions to execute without acquiring locks, instead verifying at commit time that no conflicting modifications occurred. First proposed by H.T. Kung and John T. Robinson in 1979, OCC works best in low-contention environments where conflicts are rare, avoiding the overhead of lock management and lock-wait delays that pessimistic methods impose.

## Key Concepts

- **Core assumption**: Multiple transactions can frequently complete without interfering with each other — conflicts are the exception, not the rule.
- **No locks acquired during execution**: Transactions read and tentatively write data without holding locks, then validate before committing.
- **Conflict detection at commit time**: Before committing, the transaction checks whether any other transaction modified data it read or wrote.
- **Rollback on conflict**: If validation detects a conflict, the transaction is aborted and may be restarted.
- **Best for low-contention workloads**: When conflicts are rare, OCC delivers higher throughput than pessimistic locking by eliminating lock management overhead.
- **Degrades under high contention**: Frequent conflicts cause repeated restarts, which can hurt performance more than pessimistic approaches.
- **Pessimistic locking also has costs**: Even without deadlocks, locking can drastically limit effective concurrency.
- **TOCTOU vulnerability**: The validate and commit phases must be performed atomically to avoid time-of-check to time-of-use bugs.

## Phases of OCC

1. **Begin** — Record a timestamp marking the transaction's start.
2. **Modify** — Read database values and tentatively write changes.
3. **Validate** — Check whether other transactions (completed after this transaction's start, or still active) modified data this transaction used.
4. **Commit/Rollback** — If no conflict, make changes permanent. If conflict detected, abort (or apply another resolution scheme). Validate + Commit must be atomic to prevent TOCTOU bugs.

## Commands and Syntax

- **HTTP ETag-based OCC**: GET response includes an `ETag`; subsequent PUT uses `If-Match: <etag>` header. Server rejects PUTs with stale ETags.
- **Web form pattern**: Include a hidden field with the record's original content, timestamp, or sequence number. On submit, compare against the database; invoke conflict resolution if they differ.
- **Redis**: `WATCH` command provides OCC for transactions.
- **DynamoDB**: Conditional updates (`ConditionExpression`) implement OCC.
- **Elasticsearch**: Uses `_seq_no` and `_primary_term` fields; newer versions get higher sequence numbers to prevent stale overwrites.
- **Kubernetes**: Resource updates use `resourceVersion` for OCC — update rejected if version has changed since read.
- **CouchDB**: Document revisions (`_rev` field) implement OCC.
- **Apache Solr**: `_version_` field enables OCC.

## Relationships

- **vs. Pessimistic Concurrency Control**: OCC avoids locks entirely; pessimistic methods acquire locks before accessing data. OCC wins on throughput in low-contention; pessimistic wins when conflicts are frequent.
- **Multiversion Concurrency Control (MVCC)**: Related but distinct — MVCC maintains multiple versions of data. Firebird uses MVCC as its OCC implementation.
- **Software Transactional Memory (STM)**: Most STM implementations use OCC internally.
- **Revision Control Systems**: The "merge" model in VCS (e.g., Git) is conceptually OCC — work proceeds independently, conflicts resolved at merge time.
- **Linearizability/Atomicity**: The validate-and-commit phase requires atomic execution to be correct.
- **Stateless protocols (HTTP)**: OCC is a natural fit because locking is infeasible — users may abandon sessions without releasing locks.

## Exam-Relevant Points

- OCC has four phases: **Begin, Modify, Validate, Commit/Rollback** — know them in order.
- OCC is preferred when **data contention is low**; pessimistic locking is preferred when contention is high.
- The validate and commit phases must be **atomic** to avoid TOCTOU bugs.
- HTTP's `ETag` + `If-Match` header mechanism is a **built-in OCC implementation** in the web protocol.
- OCC was first proposed in **1979 by Kung and Robinson**.
- OCC transactions **never wait on locks** — they either succeed or restart, which means no deadlocks but possible starvation under high contention.
- Systems using OCC natively include: Elasticsearch (sequence numbers), CouchDB (document revisions), Redis (WATCH), DynamoDB (conditional writes), Kubernetes (resourceVersion), Apache Iceberg, Firestore.
- The **cost tradeoff**: OCC saves the overhead of lock acquisition/release but pays the cost of transaction restart on conflict. The break-even depends on conflict frequency.
