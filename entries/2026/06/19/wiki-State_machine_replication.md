---
source: sources/wiki-State_machine_replication.md
source_url: https://en.wikipedia.org/wiki/State_machine_replication
---

## State Machine Replication (SMR)

State machine replication is a general method for building fault-tolerant distributed services by running identical copies of a deterministic state machine on multiple independent servers. Clients send requests (inputs) to all replicas, a protocol ensures all replicas process inputs in the same order, and faulty outputs are filtered by majority vote. The approach provides a unified framework for reasoning about replication, consensus, and failure handling in distributed systems.

## Key Concepts

- **Deterministic state machine**: A tuple of (States, Inputs, Outputs, transition function, output function, Start state). Multiple copies given the same inputs in the same order produce identical states and outputs.
- **2F+1 replicas needed** to tolerate F arbitrary failures — the extra copies serve as evidence to distinguish correct from faulty replicas.
- **Fail-stop special case**: If failed replicas are guaranteed to halt silently, only F+1 replicas are needed.
- **Byzantine failure**: A replica sends different values to different peers. Tolerating non-malicious Byzantine faults requires 2F+1 replicas with non-cryptographic hashes; malicious Byzantine faults require either cryptographic signatures (2F+1) or 3F+1 replicas without crypto.
- **Visible vs. hidden channels**: Visible channels are communication paths the system can observe (client-server, server-server). Hidden channels (e.g., client-client via phone) are invisible to the protocol and weaken ordering guarantees.
- **Causal order**: When all channels are visible, a partial global order can be inferred from communication patterns. Each replica derives this independently.
- **Consensus order**: In open systems with hidden channels, replicas use a consensus protocol (e.g., Paxos) to agree on input ordering. Each consensus instance decides one slot in the sequence.
- **Output filtering**: Clients accept the output agreed upon by a majority of replicas. If no majority exists, the system returns FAIL.
- **Auditing**: Replicas exchange checksums of state and recent outputs; deviating replicas are detected and restarted.

## Commands and Syntax

The SMR approach is a protocol pattern, not a specific tool. The six-step procedure:

1. Place copies of the state machine on multiple independent servers.
2. Receive client requests as inputs.
3. Choose an ordering for inputs (causal order or consensus order).
4. Execute inputs in chosen order on each replica.
5. Respond to clients with majority-agreed output.
6. Monitor replicas for state/output divergence.

**Reconfiguration commands** (modeled as state machine inputs):
- `QUIT` — a replica submits this to remove itself from the group; all non-faulty replicas process the removal.
- `JOIN` — a new or restarted replica submits this to enter the group (requires state transfer first).
- `CHECKPOINT` — submitted like a client request to snapshot current state and truncate the log.

## Relationships

- **Consensus protocols**: SMR depends on consensus (Paxos, Raft, PBFT, Tendermint) for input ordering. Paxos requires an eventual leader for liveness; Raft formalizes leader election.
- **Byzantine fault tolerance (BFT)**: SMR with Byzantine failure handling leads to PBFT and BFT-SMaRt; Tendermint BFT adapts this for proof-of-stake blockchains.
- **Virtual synchrony**: Ken Birman's model (Isis Toolkit) provides an alternative ordering approach using group communication with causal delivery.
- **Generalized Paxos**: Exploits operation semantics (commutativity) to allow concurrent execution of non-conflicting operations, relaxing total order to partial order.
- **Sharded ledgers**: Cerberus protocol demonstrates that partial ordering suffices when transactions don't conflict, using graph-based dependency models.
- **FLP impossibility**: Fischer-Lynch-Paterson result proves consensus is impossible in asynchronous systems with even one faulty process — SMR protocols work around this via eventual leader assumptions or partial synchrony.
- **Checkpoints and state transfer**: Enable log truncation and new-replica bootstrapping, critical for practical SMR deployments.

## Exam-Relevant Points

- **2F+1 formula**: A system tolerating F arbitrary failures requires 2F+1 replicas. For fail-stop: F+1. For malicious Byzantine without crypto: 3F+1.
- **Determinism requirement**: All replicas must be deterministic — same inputs in same order produce same state and outputs. This is the foundational invariant of SMR.
- **Three replicas is the minimum** for any fault tolerance (one faulty, two to compare). Two copies cannot identify which is faulty.
- **Consensus vs. causal ordering**: Causal order works only when all channels are visible. Hidden channels require consensus-based ordering.
- **Paxos leader**: Required for liveness, not safety. Multiple replicas may believe they are leader simultaneously without violating correctness.
- **Checkpoint purpose**: Bounds log growth by snapshotting state; log entries before the checkpoint can be discarded.
- **State transfer**: New/restarted replicas receive a checkpoint copy plus any subsequent log entries before joining. They observe the ordering protocol during transfer to collect new inputs.
- **System failure condition**: Occurs when no majority of replicas return the same output.
- **Key historical figures**: Lamport (state machine approach, Paxos, Byzantine generals), Schneider (tutorial formalization), Birman (virtual synchrony/Isis), Castro & Liskov (PBFT), Borg (early OS-level SMR, 1983).
- **Failed replicas don't have to stop** — they may continue producing spurious outputs, which is why majority voting on outputs is essential.
