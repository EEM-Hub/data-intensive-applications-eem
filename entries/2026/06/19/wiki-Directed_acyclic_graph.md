---
source: sources/wiki-Directed_acyclic_graph.md
source_url: https://en.wikipedia.org/wiki/Directed_acyclic_graph
---

## Directed Acyclic Graphs (DAGs): Structure, Properties, and Applications

A directed acyclic graph (DAG) is a directed graph containing no directed cycles — following edge directions from any vertex will never return to that vertex. DAGs are equivalent to graphs that admit a topological ordering, and they formalize partial order relationships. They appear across data-intensive systems in scheduling, dependency resolution, data pipelines, version control, and causal modeling.

## Key Concepts

- **DAG definition**: A directed graph where no sequence of directed edges forms a closed loop. Vertices connected by directed edges (arcs), with the constraint that no directed walk returns to its starting vertex.
- **Walk vs. path vs. cycle**: A walk is a sequence of vertices connected by directed edges; a path is a walk with all distinct vertices; a cycle is a walk where only the first and last vertex repeat.
- **Reachability relation**: Forms a **partial order** on vertices — u ≤ v iff there exists a directed path from u to v. Different DAGs can encode the same partial order.
- **Transitive closure**: The DAG with the **most edges** preserving the same reachability relation — adds a direct edge for every reachable pair.
- **Transitive reduction**: The DAG with the **fewest edges** preserving the same reachability relation — removes redundant edges where longer paths exist. Unique for DAGs (not for cyclic directed graphs).
- **Hasse diagram**: A visual representation of a transitive reduction where edge orientation is shown by vertical position (lower = earlier).
- **Topological ordering**: A linear sequence of vertices such that every edge goes from earlier to later in the sequence. A directed graph is a DAG **if and only if** it has a topological ordering. Ordering is unique iff the DAG contains a Hamiltonian path (directed path through all vertices).
- **Condensation**: Any directed graph can be converted to a DAG by contracting each strongly connected component into a single supervertex.
- **Feedback vertex/arc set**: Removing these sets from a cyclic graph produces a DAG; finding the minimum set is NP-hard.
- **Related graph families**: Multitree (at most one directed path between any two vertices), polytree (oriented undirected tree), arborescence (polytree rooted at a single vertex).

## Commands and Syntax

- **Topological sort — Kahn's algorithm**: Maintain a list of vertices with no remaining incoming edges; repeatedly remove one, append to ordering, update neighbor in-degrees. Runs in **O(V + E)** linear time.
- **Topological sort — DFS-based**: Reverse a postorder DFS traversal to obtain a valid topological ordering. Also **O(V + E)**.
- **DAG recognition**: Attempt topological sort; if it succeeds for all vertices, the graph is a DAG. Linear time.
- **Transitive closure computation**: O(mn) via BFS/DFS from each vertex, or O(n^ω) via matrix multiplication (ω < 2.373).
- **Transitive reduction**: Computable in the same asymptotic time as transitive closure.
- **Shortest/longest paths in DAGs**: Process vertices in topological order, relax edges — **O(V + E)** linear time. Contrast: shortest paths in general graphs require Dijkstra (O(E + V log V)) or Bellman-Ford (O(VE)); longest paths in general graphs are NP-hard.

## Relationships

- **Partial orders ↔ DAGs**: Every finite partial order corresponds to a unique transitively closed DAG, and vice versa. This is the mathematical foundation for dependency graphs.
- **Scheduling and dependency graphs**: DAGs model task dependencies (spreadsheets, makefiles, instruction scheduling). Circular dependencies = cycles = not a DAG = unschedulable.
- **PERT/Critical Path Method**: Vertices represent milestones, edges represent tasks with durations. The longest path = critical path = minimum project duration.
- **Data processing pipelines**: Dataflow programming, compiler intermediate representations (common subexpression elimination), combinational logic circuits, and feedforward neural networks are all DAG-structured.
- **Bayesian networks**: Probabilistic causal models structured as DAGs where each node's probability depends only on its parents.
- **Version control (Git)**: Commit history forms a DAG — not a tree, because merges create multiple parents. Vertices = revisions, edges = derivation relationships.
- **Family trees / genealogy**: Parent-child relationships form a DAG (not a tree due to pedigree collapse from intermarriage).
- **Citation networks**: Papers can only cite earlier papers, naturally forming a DAG ordered by publication time.

## Exam-Relevant Points

- A directed graph is a DAG **if and only if** it admits a topological ordering — this bidirectional equivalence is fundamental.
- Topological sort runs in **O(V + E)** time using either Kahn's algorithm or reverse-postorder DFS.
- Shortest and longest paths in DAGs are solvable in **linear time** by processing in topological order — a major advantage over general graphs where longest path is NP-hard.
- The transitive reduction of a DAG is **unique**; for cyclic graphs it is not.
- Converting a cyclic directed graph to a DAG: either remove a feedback vertex/arc set (minimum is NP-hard) or compute the **condensation** by contracting strongly connected components.
- DAGs model dependency graphs; a circular dependency corresponds to a cycle and prevents valid scheduling.
- The number of acyclic orientations of an undirected graph equals |χ(−1)| where χ is the chromatic polynomial.
- A DAG has a **unique** topological ordering iff it contains a directed Hamiltonian path.
- Every DAG defines a partial order via its reachability relation; every finite partial order can be represented as a DAG.
