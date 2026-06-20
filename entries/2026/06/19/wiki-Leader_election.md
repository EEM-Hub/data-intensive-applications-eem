---
source: sources/wiki-Leader_election.md
source_url: https://en.wikipedia.org/wiki/Leader_election
---

## Leader Election in Distributed Systems

Leader election is the process of designating a single node as the coordinator of a distributed task when no pre-assigned leader exists or the current leader has become unreachable. All nodes communicate to break symmetry — typically using unique identifiers — so that exactly one node enters the "elected" state and all others recognize it. The problem was formalized by LeLann in the context of token ring networks and has been studied across many network topologies.

## Key Concepts

- **Formal definition**: Each processor eventually decides elected or not-elected; exactly one becomes elected, and that decision is irrevocable.
- **Three correctness properties**: Termination (finishes in finite time), Uniqueness (exactly one leader), Agreement (all others know who the leader is).
- **Symmetry breaking** is the core challenge — without distinguishing information (unique IDs, randomness), election is impossible.
- **Anonymous rings impossibility**: No deterministic algorithm can elect a leader in anonymous rings, even with known ring size. Proof by induction: identical initial states produce identical transitions at every round, so all nodes reach the same final state — contradicting uniqueness.
- **Probabilistic algorithms** overcome anonymity by having nodes randomly assume identities, achieving election with high probability.
- **Algorithm design dimensions**: synchronous vs. asynchronous communication; unique vs. anonymous processes; known vs. unknown network size; network topology (ring, mesh, hypercube, complete graph, torus).
- **Message complexity** is the primary cost metric — total messages sent across all nodes.

## Commands and Syntax

No CLI commands; this is a theoretical topic. Key algorithmic procedures:

- **O(n²) ring algorithm (Chang-Roberts)**: Each node sends its ID clockwise. Forward any received ID greater than your own; discard smaller ones. If you receive your own ID back, you are the leader — announce termination.
- **O(n log n) ring algorithm (Hirschberg-Sinclair)**: Runs in phases. In phase k, a candidate probes 2^k neighbors in both directions. Neighbors ACK only if the candidate's ID exceeds theirs. Candidates surviving all phases become leader. At most n/(2^k + 1) winners per phase; ceil(log(n-1)) total phases.
- **O(n) synchronous ring algorithm**: Requires known ring size n. Runs in phases of n rounds each. Phase i checks if any node has id=i; the first match sends a termination message. Exactly n messages total.
- **Mesh election**: Wake-up phase (3n+k messages), election on outer ring (6(a+b)-16 messages), termination broadcast (2n messages). Square mesh: O(√n).
- **Hypercube election**: Dueling pairs at each stage; losers drop out, winners advance. O(n) messages for oriented; O(n log log n) for unoriented.
- **Complete network election**: O(n) messages achievable since every node can communicate directly with every other.

## Relationships

- **Token ring networks**: Leader election originated as a method to regenerate a lost token in token ring protocols.
- **Consensus and coordination**: Leader election is a building block for consensus protocols — once a leader is elected, it can coordinate agreement.
- **Failure detection**: In practice, leader election is triggered by failure detectors that identify a crashed or unreachable coordinator.
- **Network topology**: Algorithm choice and message complexity are tightly coupled to topology — ring, mesh, hypercube, torus, and complete graph each have specialized algorithms.
- **Randomized algorithms**: Anonymous ring impossibility drives the use of probabilistic approaches, connecting to broader themes of randomization in distributed computing.
- **Dijkstra Prize**: The Gallager-Humblet-Spira algorithm for general undirected graphs won this prize, underscoring the foundational importance of leader election.

## Exam-Relevant Points

- **Impossibility result**: No deterministic leader election exists for anonymous rings — this is a classic exam question. Know the symmetry argument: identical states, identical messages, identical transitions, therefore all nodes reach the same decision.
- **Message complexity by topology and algorithm**:
  - Ring: O(n²) worst-case (Chang-Roberts), O(n log n) (Hirschberg-Sinclair), O(n) (synchronous with known size)
  - Mesh: O(√n) for square mesh
  - Hypercube: O(n) oriented, O(n log log n) unoriented
  - Complete graph: O(n)
- **Three required properties**: Termination, Uniqueness, Agreement — know these precisely.
- **Four algorithm variation dimensions**: Communication mechanism (sync/async), process names (unique/anonymous), topology, network size knowledge.
- **Chang-Roberts vs. Hirschberg-Sinclair**: Both for rings with unique IDs; Hirschberg-Sinclair improves worst-case from O(n²) to O(n log n) using bidirectional probing in exponentially growing neighborhoods.
- **Randomized approaches** for anonymous rings: Itai-Rodeh algorithm uses random candidate selection with O(n log n) expected message complexity.
- **Leader oracle Ω?**: Used by Fisher and Jiang to circumvent the anonymous ring impossibility — processors query an oracle about leader uniqueness.
