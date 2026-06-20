---
source: sources/wiki-Optimistic_replication.md
source_url: https://en.wikipedia.org/wiki/Optimistic_replication
---

## Optimistic (Lazy) Replication Strategy

Optimistic replication is a replication strategy that allows replicas to diverge temporarily, trading strong consistency for improved concurrency and parallelism. Unlike pessimistic replication (which enforces identical replicas at all times), optimistic replication relies on eventual consistency — replicas converge only after the system has been quiesced. The trade-off is that divergent replicas may require explicit reconciliation that can be difficult or even insoluble.

## Key Concepts

- **Pessimistic vs. optimistic replication**: Pessimistic guarantees all replicas are identical at all times (as if single copy); optimistic allows divergence and guarantees convergence only after quiescence.
- **Eventual consistency**: The consistency model underpinning optimistic replication — replicas converge given sufficient quiet time.
- **Five-element algorithm**: Operation submission, propagation, scheduling, conflict resolution, commitment.
- **Propagation strategies**: State transfer (ship current state) vs. operation transfer (ship operations/instructions to reach new state).
- **Scheduling and conflict resolution**: Can be syntactic (based on general info like timestamps/location) or semantic (uses application-specific knowledge). State transfer systems are limited to syntactic approaches because they lack semantic information.
- **Synchronization as a special case**: When there are exactly two replicas (e.g., PDA and computer), replication reduces to synchronization. Replication is the broader problem.
- **Idempotency matters**: Non-idempotent operations (e.g., incrementing a value) combined with replication lag can cause disaster when users retry operations they believe failed.
- **Validity constraint hazard**: Two individually legal updates (A and B) may conflict when applied together (AB or BA both illegal), requiring the system to pick a winner and revert the loser on some nodes.

## Commands and Syntax

No specific commands. The conceptual algorithm structure is:

1. **Operation submission** — users submit at independent sites
2. **Propagation** — sites share known operations (state transfer or operation transfer)
3. **Scheduling** — each site orders operations it knows about
4. **Conflict resolution** — conflicting operations are modified/resolved
5. **Commitment** — sites agree on final schedule and resolution; operations become permanent

## Relationships

- **Eventual consistency** — the consistency guarantee optimistic replication provides
- **Conflict-free replicated data types (CRDTs)** — a data structure approach that sidesteps conflicts entirely, an evolution of optimistic replication ideas
- **Operational transformation (OT)** — theoretical framework for collaborative editing, uses operation transfer
- **Multi-master replication** — a database topology that employs optimistic replication
- **Copy-modify-merge paradigm** — used by version control systems (CVS, SVN) as a practical instance of optimistic replication
- **Thomas Write Rule** — conflict resolution rule used by Usenet and similar systems
- **Quiescence** — the system state required before convergence is guaranteed

## Exam-Relevant Points

- Optimistic replication trades **strong consistency for availability and concurrency** — a direct manifestation of the CAP theorem trade-off.
- The five algorithm elements (submit, propagate, schedule, resolve, commit) are a useful framework for analyzing any replication system.
- **State transfer vs. operation transfer** is a fundamental propagation distinction: state transfer is simpler but loses semantic information; operation transfer preserves intent but is more complex.
- **Syntactic vs. semantic** conflict resolution: semantic is smarter but requires application knowledge; state transfer forces syntactic.
- Applications must handle **replication lag** carefully — non-idempotent retries and validity constraint violations are classic pitfalls.
- **Testing environments may mask replication bugs** because they are smaller and less loaded, producing less lag than production.
- Key reference: Saito & Shapiro (2005), "Optimistic Replication" in ACM Computing Surveys — the canonical survey paper.
- CVS is the textbook example mapping all five algorithm elements to a concrete system.
