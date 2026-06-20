---
source: sources/wiki-Skip_list.md
source_url: https://en.wikipedia.org/wiki/Skip_list
---

## Skip Lists: Probabilistic Alternative to Balanced Trees

Skip lists are a probabilistic data structure invented by William Pugh in 1989 that provides O(log n) average-case complexity for search, insertion, and deletion within an ordered sequence. They achieve the search performance of sorted arrays while maintaining the insertion flexibility of linked lists by building a hierarchy of linked lists where each successive layer skips over more elements. Elements are promoted to higher layers based on random coin flips, making them simpler to implement than deterministic balanced trees.

## Key Concepts

- **Layered structure**: The bottom layer is an ordinary sorted linked list; each higher layer is an "express lane" that skips elements, enabling fast traversal
- **Probabilistic promotion**: Each element in layer *i* appears in layer *i+1* with fixed probability *p* (commonly 1/2 or 1/4)
- **Expected height**: A skip list with *n* elements contains log_{1/p}(n) layers
- **Average element participation**: Each element appears in 1/(1-p) lists on average
- **Search algorithm**: Start at the top-left, move right until overshooting the target, then drop down one level and repeat
- **Expected search cost**: (1/p) * log_{1/p}(n), which is O(log n) for constant *p*
- **Complexity tradeoffs**: Average O(log n) for search/insert/delete; worst case O(n) (extremely unlikely); space O(n) average, O(n log n) worst case
- **p=1/e minimizes average search time**; p=1/2 simplifies implementation
- **No absolute worst-case guarantees**: Unlike balanced trees (AVL, red-black), bad coin flips can theoretically produce a degenerate structure
- **Indexable skip lists**: By storing link widths (number of bottom-layer nodes spanned), O(log n) positional access is possible

## Commands and Syntax

**Quasi-random level construction** (used during O(n) traversals to optimize structure):
```
make all nodes level 1
j ← 1
while the number of nodes at level j > 1 do
    for each i'th node at level j do
        if i is odd and i is not the last node at level j
            randomly choose whether to promote it to level j+1
        else if i is even and node i-1 was not promoted
            promote it to level j+1
    j ← j + 1
```

**Indexed lookup by position** (with width-augmented links):
```
function lookupByPositionIndex(i)
    node ← head
    i ← i + 1
    for level from top to bottom do
        while i ≥ node.width[level] do
            i ← i - node.width[level]
            node ← node.next[level]
    return node.value
```

**Width invariant**: The width of a higher-level link equals the sum of the component link widths immediately below it. Total width is the same on every level.

## Relationships

- **vs. Balanced trees (AVL, red-black, B-trees)**: Skip lists offer similar O(log n) average performance but are simpler to implement; balanced trees provide stronger worst-case guarantees
- **Probabilistic data structures family**: Grouped with Bloom filters, count-min sketches, quotient filters, and HyperLogLog
- **Linked lists**: Skip lists extend the basic linked list with hierarchical express lanes
- **Parallel computing**: Skip lists naturally support concurrent insertions in different regions without global rebalancing — a key advantage over balanced trees
- **Lock-free/concurrent data structures**: Skip lists underpin lock-free priority queues and concurrent dictionaries

## Exam-Relevant Points

- **Time complexity**: O(log n) average for search, insert, delete; O(n) worst case for all three
- **Space complexity**: O(n) average, O(n log n) worst case
- **Promotion probability *p***: Each element promoted independently with probability *p*; choosing *p* trades search cost against storage
- **Not deterministically balanced**: Unlike AVL/red-black trees, worst-case O(n) is possible (though astronomically unlikely)
- **Real-world usage**: Redis (sorted sets), RocksDB (memtable), Java (ConcurrentSkipListMap/Set), Lucene (posting lists), MemSQL (primary index), Discord (member lists)
- **Concurrency advantage**: Lock-free implementations possible; parallel insertions without global rebalancing
- **Indexable variant**: Augmenting links with widths enables O(log n) positional access — described in Pugh's "Skip List Cookbook"
- **Derandomization and quasi-randomization**: Can be done during O(n) traversals to optimize level structure, but reveals structural information to adversaries
- **Inventor**: William Pugh, 1989; published formally in Communications of the ACM, 1990
