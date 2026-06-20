---
source: sources/wiki-B-tree.md
source_url: https://en.wikipedia.org/wiki/B-tree
---

## B-Tree Data Structure

The B-tree is a self-balancing tree data structure invented in 1970 by Rudolf Bayer and Edward McCreight at Boeing Research Labs. It maintains sorted data and supports search, insertion, deletion, and sequential access all in O(log n) time. The B-tree generalizes the binary search tree by allowing nodes to have more than two children, which reduces tree height and minimizes expensive disk reads — making it the dominant index structure in both relational and non-relational databases.

## Key Concepts

- **Self-balancing**: all leaf nodes are always at the same depth; depth changes only when the root splits or merges
- **Order *m* (Knuth's definition)**: the maximum number of children any node may have; terminology varies across literature (some authors define order as minimum keys instead)
- **Node occupancy invariant**: every non-root internal node has at least ⌈m/2⌉ children and at most *m* children; a node with *k* children holds *k*−1 keys
- **Keys as separators**: keys in an internal node partition the key space among its child subtrees — left subtree < key < right subtree
- **Space complexity**: O(n); all operations (search, insert, delete) are O(log n) both amortized and worst case
- **Why fewer disk reads**: by packing hundreds of keys per node (matched to a disk block or cache line), tree height drops from log₂ N to log_b N, where *b* is the blocking factor
- **Blocking factor example**: 1M records, 100 records/block → binary search needs ~20 disk reads; B-tree index needs ~3 disk reads
- **Nodes are at least half full**, which bounds wasted space while allowing room for insertions without immediate splits

## Commands and Syntax

No CLI commands — this is a data structure definition. Key algorithmic procedures:

- **Search**: start at root, binary-search within node for the correct child pointer, recurse downward — O(log n)
- **Insertion**: always begins at a leaf. If the leaf is full (2d keys), split into two d-key nodes and promote the median key to the parent. Splits can cascade to the root; a root split is the only event that increases tree height
- **Deletion**: remove key from leaf (or swap with in-order predecessor/successor first). If the node underflows (< d keys), redistribute keys from a sibling or merge with a sibling and pull a key down from the parent. Merges can cascade; merging the root's last two children is the only event that decreases tree height
- **Lazy deletion** (in database context): mark records as deleted without restructuring; periodically compact

## Relationships

- **Binary search tree**: B-tree generalizes it; a B-tree of order 2 is essentially a 2-3 tree
- **B+ tree**: variant where all record pointers live in leaf nodes only; internal nodes hold only keys and child pointers, enabling higher fan-out and faster search; leaf nodes are often linked for sequential scan
- **B\* tree**: variant requiring nodes to be at least 2/3 full (vs. 1/2); uses sibling redistribution (spill) to delay splits
- **B\*+ tree**: combines B+ leaf-only records with B\* density guarantees
- **Order statistic trees**: B-trees can be augmented to support rank queries (find Nth key, count keys in a range)
- **Database indexes**: B-tree is the standard index implementation in virtually all relational databases (PostgreSQL, MySQL/InnoDB, SQLite, Oracle, SQL Server) and many non-relational ones
- **LSM trees**: an alternative write-optimized structure; B-trees favor read-heavy workloads with in-place updates
- **Disk/block storage**: B-tree node size is typically matched to the storage block size (e.g., 4 KB or 16 KB pages)

## Exam-Relevant Points

- All B-tree operations are **O(log n)** — both amortized and worst case
- **Knuth's definition of order *m***: maximum number of children (not keys); maximum keys per node = m−1; minimum children for non-root internal nodes = ⌈m/2⌉
- **Best-case height**: h_min = ⌈log_m(n+1)⌉ − 1 (fully packed tree)
- **Worst-case height**: h_max = ⌊log_d((n+1)/2)⌋ where d = ⌈m/2⌉
- **Insertion splits** propagate upward; **deletion merges** propagate upward — tree height changes only at the root
- **B+ trees store all data pointers at leaves**; B-trees store data pointers at every level — this is a frequently tested distinction
- **B\* trees guarantee 2/3 occupancy** instead of 1/2, using sibling redistribution before splitting
- The key advantage of B-trees over binary search trees for disk-based storage is **reduced tree height → fewer disk I/Os**: log_b N reads vs. log₂ N reads
- **Blocking factor** transforms the search from binary (log₂ N comparisons, each potentially a disk seek) to B-tree (log_b N block reads)
- B-tree remains the **standard index in almost all relational databases** — this is stated directly by Kleppmann (DDIA) and is a core exam fact
