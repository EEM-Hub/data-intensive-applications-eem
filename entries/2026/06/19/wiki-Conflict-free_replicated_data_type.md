---
source: sources/wiki-Conflict-free_replicated_data_type.md
source_url: https://en.wikipedia.org/wiki/Conflict-free_replicated_data_type
---

## Conflict-Free Replicated Data Types (CRDTs)

CRDTs are data structures replicated across multiple computers in a network that allow any replica to be updated independently and concurrently without coordination, automatically resolve inconsistencies, and guarantee eventual convergence. Formally defined in 2011 by Shapiro, Preguiça, Baquero, and Zawirski, CRDTs enable optimistic replication where all concurrent updates are allowed and merged later without conflicts.

## Key Concepts

- **Core invariant**: Replicas may diverge temporarily but are guaranteed to eventually converge — this is strong eventual consistency.
- **Optimistic replication**: All concurrent updates are allowed; inconsistencies are resolved by deterministic merge rather than prevented by coordination.
- **Two fundamental approaches**:
  - **State-based CRDTs (CvRDTs)**: Send full local state to other replicas; merge function must be commutative, associative, and idempotent (a join-semilattice). Update function must be monotone w.r.t. the partial order.
  - **Operation-based CRDTs (CmRDTs)**: Transmit update operations instead of state. Operations must be commutative and associative. Require reliable, exactly-once, causally-ordered delivery.
- **Delta state CRDTs**: Optimization of state-based CRDTs that disseminate only recent changes rather than full state.
- **Pure operation-based CRDTs**: Variant that reduces metadata size.
- **Semilattice requirement**: The merge function must form a semilattice — this mathematical structure is what guarantees convergence regardless of message ordering or duplication.
- **Monotonicity**: Internal state must only grow (monotonically increase), even if external query values can decrease (as in PN-Counter).
- **Tombstone set**: A set tracking removed elements; once tombstoned, an element is considered deleted. Used in 2P-Set and OR-Set.

## Commands and Syntax

### Known CRDT Data Structures

**G-Counter (Grow-only Counter)**: Each of n nodes maintains its own slot in array P, incrementing locally. Merge takes element-wise `max()`. Value is sum of all slots.

**PN-Counter**: Two G-Counters — P for increments, N for decrements. Value = ΣP - ΣN. Internal state grows monotonically even though external value can decrease.

**G-Set (Grow-only Set)**: Add-only set. Merge = set union. Elements cannot be removed.

**2P-Set (Two-Phase Set)**: Two G-Sets — add-set A and tombstone-set R. Element is member if in A and not in R. Once removed, cannot be re-added. Remove-wins semantics.

**LWW-Element-Set**: Add-set and remove-set with timestamps per element. Membership determined by comparing latest add vs. latest remove timestamp. Configurable bias (add-wins or remove-wins) for equal timestamps. Allows re-insertion after removal.

**OR-Set (Observed-Remove Set)**: Uses unique tags instead of timestamps. Each add generates a new tag; remove copies all current add-tags to remove-tags. Member if add-tags minus remove-tags is nonempty. Can be optimized with per-replica timestamp vectors to avoid unbounded tombstone growth.

**Sequence CRDTs**: Treedoc, RGA, Woot, Logoot, LSEQ, LogootSplit. Used for collaborative text editing as alternative to Operational Transformation. Yjs is the leading industrial implementation, using a plain list rather than a tree structure.

## Relationships

- **Eventual consistency / Strong eventual consistency**: CRDTs provide the strongest form of eventual consistency — replicas that have received the same set of updates are guaranteed identical, with no conflict resolution needed.
- **Optimistic replication**: CRDTs are the key enabling data structure for optimistic replication strategies.
- **Operational Transformation (OT)**: Sequence CRDTs are a competing approach to OT for collaborative editing. CRDTs avoid OT's complexity around transformation functions but may carry more metadata.
- **Gossip protocols**: Natural dissemination mechanism for state-based CRDTs; handles topology changes and reduces network use.
- **CAP theorem context**: CRDTs enable AP (available, partition-tolerant) systems that still converge — they sacrifice strong consistency for availability without losing eventual convergence guarantees.
- **Semilattice theory**: The mathematical foundation — merge as join, states as a partially ordered set — connects CRDTs to order theory and abstract algebra.
- **Composition**: Complex CRDTs are built by combining simpler ones (PN-Counter = two G-Counters; 2P-Set = two G-Sets).

## Exam-Relevant Points

- **State-based vs. operation-based tradeoff**: State-based requires only gossip (weaker network assumptions) but transmits more data. Operation-based transmits less data but requires exactly-once, causally-ordered delivery.
- **The two approaches are theoretically equivalent** — each can emulate the other.
- **Merge function properties**: Must be commutative, associative, and idempotent (for state-based). These properties make the CRDT invariant under message reordering and duplication.
- **Monotonicity distinction**: Internal state must always grow monotonically, but externally visible query results need not (PN-Counter value can decrease).
- **2P-Set limitation**: Once removed, an element can never be re-added. LWW-Element-Set and OR-Set overcome this.
- **OR-Set tombstone problem**: Naive implementation has unbounded tombstone growth; optimizable via per-replica timestamp vectors.
- **Delta CRDTs** solve the bandwidth problem of state-based CRDTs by sending only recent mutations.
- **Real-world scale**: League of Legends uses Riak CRDTs for chat handling 7.5M concurrent users and 11K messages/second.
- **Industry adoption**: Redis, Riak, Cosmos DB have native CRDT support. Apple Notes, Figma, Facebook (Apollo), and Phoenix framework all use CRDTs.
- **Figma's approach**: Server-authoritative LWW registers per property with fractional indexing for ordered sequences — a practical hybrid rather than pure peer-to-peer CRDT.
- **Industrial vs. academic implementations**: Industrial sequence CRDTs (e.g., Yjs) outperform academic ones due to optimizations and realistic testing.
