---
source: sources/wiki-Paxos_computer_science.md
source_url: https://en.wikipedia.org/wiki/Paxos_(computer_science)
---

## Paxos Consensus Protocol Family

Paxos is a family of protocols for solving consensus in a network of unreliable processors, originally proposed by Leslie Lamport in 1989 and published in 1998. It is the foundational algorithm for state machine replication in distributed systems, ensuring that a group of nodes can agree on a single value even when some nodes or messages fail. Paxos guarantees safety (consistency) and fault tolerance but cannot guarantee liveness, consistent with the FLP impossibility result.

## Key Concepts

- **Consensus**: The process of agreeing on one result among a group of participants, made difficult by processor and communication failures.
- **State machine replication**: A technique for converting an algorithm into a fault-tolerant, distributed implementation; consensus protocols are its basis.
- **FLP impossibility result** (Fischer, Lynch, Paterson): No deterministic fault-tolerant consensus protocol can guarantee progress in an asynchronous network. A protocol can have only two of: safety, liveness, and fault tolerance. Paxos chooses safety + fault tolerance.
- **Quorum**: A majority subset of acceptors. Any two quorums must overlap, which is what guarantees consistency.
- **Fault tolerance formula**: Requires **n = 2F + 1** processors to tolerate F simultaneous failures — the non-faulty count must strictly exceed the faulty count.
- **Three roles**:
  - **Proposer**: Initiates proposals with unique, monotonically increasing proposal numbers.
  - **Acceptor**: Votes on proposals; stores accepted values in stable storage.
  - **Learner**: Learns the decided value after a majority of acceptors agree.
- **Safety properties** (always guaranteed):
  - **Validity (non-triviality)**: Only proposed values can be chosen.
  - **Agreement (consistency)**: No two learners can learn different values.
- **Liveness property** (NOT guaranteed): Termination — if a value is proposed, a learner will eventually learn some value. Paxos can livelock when multiple proposers conflict.
- **Crash-recovery model**: Processors may fail and rejoin but do not lie or collude (no Byzantine failures in basic Paxos).
- **Network assumptions**: Asynchronous delivery; messages may be lost, reordered, or duplicated, but are never corrupted.

## Commands and Syntax

### Basic Paxos Protocol (single value decision)

**Phase 1a — Prepare:**
- Proposer selects a unique proposal number `n` (greater than any it has previously used).
- Sends `Prepare(n)` to a quorum of acceptors.

**Phase 1b — Promise:**
- Acceptor receives `Prepare(n)`:
  - If `n` > all previously seen proposal numbers: responds with `Promise(n, {highest_accepted_proposal, value})` and commits to ignoring proposals ≤ n.
  - If `n` ≤ a previously seen number: may ignore or send `Nack(n)`.

**Phase 2a — Accept:**
- Proposer receives `Promise` from a quorum:
  - If any acceptor reported a previously accepted value: proposer must use the value from the highest-numbered accepted proposal (`v = z`).
  - If no acceptor had accepted any value: proposer uses its own value (`v = x`).
  - Sends `Accept!(n, v)` to a quorum.

**Phase 2b — Accepted:**
- Acceptor receives `Accept!(n, v)`:
  - If it has NOT promised to consider only proposals > n: accepts and sends `Accepted(n, v)` to proposer and all learners.
  - Otherwise: ignores the message.
- Learners learn the decided value only after receiving `Accepted` from a majority.

### Multi-Paxos (continuous stream of values)

- Adds instance number `I` alongside the round number `N`.
- If the leader is stable, **Phase 1 is skipped** for subsequent instances.
- Reduces message delay from 4 to 2 (proposal to learning).
- Typical collapsed deployment merges Proposer, Acceptor, and Learner into a single "Server" role.

```
# Multi-Paxos with stable leader (steady state):
Client      Servers
   X-------->|  |  |  Request
   |         X->|->|  Accept!(N,I+1,W)
   |         X<>X<>X  Accepted(N,I+1)
   |<--------X  |  |  Response
```

## Relationships

- **State machine replication**: Paxos is the consensus engine underneath replicated state machines; Multi-Paxos replicates a log of commands.
- **Leader election**: Paxos can itself be used to elect a leader (propose "I am the leader" and achieve consensus on it).
- **Raft**: A later consensus protocol designed to be more understandable than Paxos, solving the same problem with a different structure.
- **Viewstamped replication** (Oki, Liskov 1988): A contemporaneous protocol with similar agreement mechanisms, developed in the context of distributed transactions.
- **Byzantine fault tolerance (BFT)**: Basic Paxos does NOT handle Byzantine failures; Byzantine Paxos is a separate variant that does.
- **FLP impossibility**: Theoretical foundation explaining why Paxos cannot guarantee liveness.
- **Virtual synchrony / gbcast**: Related group communication protocols; Paxos differs in its stronger durability and partition-handling guarantees.
- **Databases and durable storage**: Paxos is commonly deployed for database replication where large durable state must remain consistent.

## Exam-Relevant Points

- **n = 2F + 1**: You need 2F+1 nodes to tolerate F simultaneous failures. This is the single most important formula.
- **Paxos guarantees safety but NOT liveness** — it can livelock when multiple proposers conflict with dueling proposal numbers (the "dueling proposers" problem).
- **The FLP impossibility result** proves you cannot have all three of safety, liveness, and fault tolerance in an asynchronous system.
- **Proposal numbers must be unique and monotonically increasing** per proposer. They are identifiers, not values.
- **The proposer must adopt the value from the highest-numbered previously accepted proposal** reported in Promise messages — it cannot freely choose its own value if any acceptor has already accepted something.
- **Consensus is on the identifier number, not the value directly** — since each identifier maps to exactly one value, this ensures consistency.
- **Once consensus is achieved, it is permanent** — new proposers who prepare a majority will always find the accepted value and must re-propose it.
- **Multi-Paxos optimization**: With a stable leader, Phase 1 (Prepare/Promise) can be skipped, reducing round-trip messages from 4 to 2.
- **Role collapsing**: In typical deployments, each node acts as Proposer + Acceptor + Learner simultaneously, simplifying to a client-server model.
- **Acceptors can accept multiple values** for different proposal numbers — this is correct behavior, not a bug. The quorum intersection property ensures only one value achieves consensus.
- **Messages may be lost, reordered, or duplicated** but not corrupted — this is a key assumption of the crash-recovery (non-Byzantine) model.
