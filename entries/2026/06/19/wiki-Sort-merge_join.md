---
source: sources/wiki-Sort-merge_join.md
source_url: https://en.wikipedia.org/wiki/Sort-merge_join
---

## Sort-Merge Join Algorithm in Relational Databases

The sort-merge join is a join algorithm used in relational database management systems to combine tuples from two relations based on a common join attribute. The core idea is to sort both relations on the join attribute first, then perform interleaved linear scans to find matching tuples efficiently. The most expensive part is ensuring both inputs are in sorted order, which may require explicit external sorting or can leverage pre-existing "interesting orders" from upstream operations like index scans.

## Key Concepts

- **Join problem**: For each distinct value of the join attribute, find the set of tuples in each relation that share that value
- **Two-phase approach**: (1) Sort both relations on the join key, (2) Merge the sorted relations with linear scans
- **Interesting order**: A pre-existing sort order in the input that eliminates the need for explicit sorting — can come from index scans, prior merge joins, or other plan operators
- **Optimizer exploitation**: Query optimizers may deliberately choose a suboptimal plan for one operation if it produces an interesting order that benefits downstream joins
- **Mark/restore mechanism**: During the merge phase, the algorithm marks positions in the left relation to handle duplicate join keys, restoring to the mark when the right relation advances to a new matching value
- **Cartesian product on duplicates**: When both relations have multiple tuples with the same join key, the output contains all combinations (cross product of the matching groups)

## Commands and Syntax

**Pseudocode structure** (inner join of two relations):
1. Sort both relations using the comparator
2. Advance pointers through both relations:
   - Skip non-matching rows by advancing the smaller side
   - On match: mark position in left relation, emit all left×right combinations for that key group
   - Use `mark()` / `restoreMark()` to replay the left relation's matching group for each new matching right row
3. Terminate when either relation is exhausted

**Relation interface requirements**: `hasNext()`, `next()`, `sort()`, `mark()`, `restoreMark()`

**Comparator contract**: Returns -1 (less), 0 (equal), or 1 (greater)

## Relationships

- **vs. Hash Join**: Hash join builds a hash table on one relation and probes with the other; sort-merge is preferred when inputs are already sorted or when the result must be ordered
- **vs. Nested Loop Join**: Nested loop is simpler (O(n×m) worst case) but sort-merge is more efficient for large, unsorted relations
- **External Sort**: Sort-merge often relies on external sorting when relations don't fit in memory
- **Query Optimizer**: The optimizer's cost model considers interesting orders — it may choose sort-merge over hash join specifically to propagate sort order to downstream operators
- **Index Scans**: B-tree index scans produce sorted output, making them natural inputs to merge joins without additional sorting

## Exam-Relevant Points

- **I/O complexity (pre-sorted)**: O(P_r + P_s) — linear in the number of pages for both relations
- **I/O complexity (unsorted)**: O(P_r·log(P_r) + P_s·log(P_s)) — dominated by the sorting cost (linearithmic)
- **Best use case**: When one or both inputs are already sorted on the join key, or when downstream operators need sorted output
- **Interesting order optimization**: The query optimizer may choose a globally better plan by selecting a locally suboptimal operator that produces a useful sort order
- **Duplicate handling**: The mark/restore mechanism is essential for correctly producing the Cartesian product of matching groups — the simplified (unique-key) version omits this
- **Sort-merge join is symmetric**: Unlike nested loop join, neither relation is designated as "inner" or "outer" in terms of access pattern — both are scanned linearly
