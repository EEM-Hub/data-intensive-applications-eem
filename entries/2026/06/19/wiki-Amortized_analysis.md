---
source: sources/wiki-Amortized_analysis.md
source_url: https://en.wikipedia.org/wiki/Amortized_analysis
---

## Amortized Analysis of Algorithm Complexity

Amortized analysis is a method for analyzing an algorithm's time or space complexity by averaging the cost of operations over an entire sequence, rather than focusing on the worst-case cost of any single operation. Introduced by Robert Tarjan in 1985, it is especially useful for data structures whose state persists between operations, where an expensive operation may restructure the state so that subsequent operations are cheap. It is a worst-case technique (not probabilistic) — it makes no assumptions about input distribution, unlike average-case analysis.

## Key Concepts

- **Core idea**: A worst-case operation can alter state such that the worst case cannot recur for a long time, effectively spreading ("amortizing") its cost across many operations.
- **Differs from average-case analysis**: Amortized analysis assumes nothing about input distribution; it guarantees worst-case bounds over sequences of operations, not individual operations.
- **Three methods** (all yield correct answers; choice is convenience):
  - **Aggregate method**: Compute total cost T(n) for n operations, then amortized cost = T(n)/n.
  - **Accounting method**: Assign each operation an amortized cost that may differ from actual cost. Cheap operations "save credit"; expensive operations "spend" it. Credit must remain non-negative, ensuring amortized cost upper-bounds actual cost.
  - **Potential method**: A formalization of the accounting method where credit is expressed as a potential function of data structure state. Amortized cost = immediate cost + change in potential.
- **Requires knowledge of possible operation sequences** — most naturally applied to data structures with persistent state.

## Commands and Syntax

No CLI commands. Key analytical patterns:

**Dynamic array push (e.g., ArrayList, std::vector)**:
- Pushes are O(1) until capacity is reached, then O(n) to copy into a doubled array.
- Resize costs form a geometric series summing to O(n) over n pushes.
- Amortized cost per push: O(n)/n = **O(1)**.

**Two-stack queue implementation** (Python):
```python
class Queue:
    def __init__(self):
        self.input = []
        self.output = []

    def enqueue(self, element):
        self.input.append(element)        # Always O(1)

    def dequeue(self):
        if not self.output:
            while self.input:
                self.output.append(self.input.pop())  # O(n) transfer
        return self.output.pop()          # O(1)
```
- Each element is moved from input to output exactly once. Charging the copy cost to enqueue gives both operations **amortized O(1)**.

## Relationships

- **Worst-case analysis**: Amortized analysis complements it — worst-case per-operation can be overly pessimistic for sequences.
- **Average-case analysis**: Unlike amortized, average-case assumes a distribution over inputs; amortized makes no such assumption.
- **Dynamic arrays**: The canonical example — ArrayList/vector resizing is amortized O(1) per insertion.
- **Binary trees and union-find**: Original motivation for Tarjan's work; union-find's inverse-Ackermann bound relies on amortized reasoning.
- **Online algorithms**: Commonly analyzed using amortized techniques.
- **Data structures with state**: Amortized analysis is most naturally applicable when operations mutate persistent state (hash tables, splay trees, Fibonacci heaps).

## Exam-Relevant Points

- Amortized O(1) for dynamic array append — despite individual resizes being O(n), the geometric series argument yields O(1) per operation.
- The three methods (aggregate, accounting, potential) are equivalent in power — know when each is most convenient.
- Amortized analysis is **not** average-case analysis: no probabilistic assumptions, it is a worst-case bound over operation sequences.
- The accounting method requires accumulated credit to remain non-negative at all times — this invariant is what makes it an upper bound.
- In the potential method: amortized cost = actual cost + ΔΦ (change in potential function).
- Two-stack queue achieves amortized O(1) for both enqueue and dequeue despite worst-case O(n) dequeue.
- Know that amortized analysis requires understanding which operation sequences are possible — it applies to data structures with persistent state, not arbitrary algorithms.
