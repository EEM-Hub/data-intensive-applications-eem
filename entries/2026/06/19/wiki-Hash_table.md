---
source: sources/wiki-Hash_table.md
source_url: https://en.wikipedia.org/wiki/Hash_table
---

## Hash Tables: Associative Array Data Structure

Hash tables are a foundational data structure that implements an associative array (also called a dictionary or map) by using a hash function to compute an index into an array of buckets. Invented in 1953, they provide average-case O(1) time complexity for search, insert, and delete operations, making them one of the most widely used data structures in computer science. They represent a classic space-time tradeoff and are the backbone of built-in types like Python's `dict`, Java's `HashMap`, C++'s `unordered_map`, and Go's `map`.

## Key Concepts

- **Hash function**: Maps keys from a universe U to indices in range {0, ..., m-1}. The function `h(x)` computes the bucket index for key x.
- **Load factor (α = n/m)**: Ratio of stored elements (n) to total buckets (m). The single most important metric for hash table performance.
  - Separate chaining: optimal α_max typically between 1 and 3; performance degrades gradually.
  - Open addressing: α must stay below 1 (physically impossible to exceed); recommended α_max is 0.6–0.75; performance degrades catastrophically as α approaches 1.
- **Collision**: When two distinct keys hash to the same index. Inevitable with imperfect hash functions; must be resolved.
- **Separate chaining**: Each bucket stores a linked list (or other structure) of collided entries. Simpler but potentially cache-unfriendly due to pointer chasing.
- **Open addressing**: All entries stored directly in the bucket array. On collision, a probe sequence finds the next open slot. Probe strategies include:
  - **Linear probing** — fixed interval (usually 1); susceptible to primary clustering.
  - **Quadratic probing** — interval grows quadratically.
  - **Double hashing** — second hash function determines interval.
- **Rehashing**: Resizing the table when α exceeds α_max (or shrinking when α drops below α_max/4). All entries must be re-hashed into the new array.
- **Perfect hash function**: Injective on a given set S — no collisions. Only possible when all keys are known in advance.
- **Dynamic perfect hashing**: Two-level hash tables that guarantee O(1) worst-case lookup using k^2 slots per bucket of k entries.
- **Space-time tradeoff**: Hash tables trade memory (the bucket array) for speed (constant-time access). With infinite memory, direct indexing suffices; with infinite time, linear search suffices.
- **Cache locality**: Linked-list chaining scatters nodes in memory, causing cache misses. Array-based chaining exploits contiguous allocation and hardware prefetchers (e.g., TLB), yielding up to 97% better performance under heavy load.
- **Uniform distribution requirement**: A hash function must distribute keys uniformly to minimize collisions. Can be verified empirically with chi-squared tests.

## Commands and Syntax

**Chained hash table pseudocode:**
```
Chained-Hash-Insert(T, k)
  insert x at the head of linked list T[h(k)]

Chained-Hash-Search(T, k)
  search for an element with key k in linked list T[h(k)]

Chained-Hash-Delete(T, k)
  delete x from the linked list T[h(k)]
```

**Hash function schemes:**
```
Division method:    h(x) = x mod m
Multiplication:     h(x) = floor(m * ((x * A) mod 1))
                    where A is a non-integer constant (Knuth suggests golden ratio)
```

**String hashing (C++ style):**
- Initialize unsigned integer to zero
- For each character: left-shift one bit, XOR with character's integer value
- Take result modulo table size

## Relationships

- **Associative arrays / dictionaries**: Hash tables are the dominant implementation of this abstract data type.
- **Self-balancing BSTs** (red-black trees, AVL trees): The main alternative. O(log n) guaranteed worst case vs. hash table's O(1) average / O(n) worst case. Hash tables win on average but BSTs provide ordered iteration and worst-case guarantees.
- **Database indexing**: Hash indexes provide O(1) point lookups but cannot support range queries (where B-trees excel).
- **Caches and sets**: Hash tables are the standard backing structure for both.
- **Consistent hashing**: Extension used in distributed systems (e.g., partitioning in data-intensive applications) to minimize rehashing when nodes join/leave.
- **Bloom filters**: Probabilistic cousin — uses multiple hash functions for set membership testing without storing values.
- **LSM trees / SSTables**: In write-optimized storage engines, hash indexes (like Bitcask) offer fast point lookups but are eventually superseded by LSM approaches for range queries.

## Exam-Relevant Points

- **Time complexity**: Average O(1) for search/insert/delete; worst case O(n) when all keys collide into one bucket.
- **Space complexity**: Θ(n) average and O(n) worst case.
- **Load factor formula**: α = n/m. This is the key performance predictor.
- **Open addressing cannot have α > 1** (each slot holds exactly one item). Separate chaining can exceed α = 1.
- **Rehashing trigger**: When α exceeds α_max. For open addressing, α_max should be 0.6–0.75. For chaining, 1–3.
- **Shrinking trigger**: When α drops below α_max/4.
- **Worst case with chaining can be reduced to O(log n)** by using self-balancing BSTs instead of linked lists per bucket (as Java's HashMap does when bucket size exceeds 8).
- **Dynamic perfect hashing guarantees O(1) worst case** using two-level tables with k^2 slots per k-entry bucket.
- **Hash function must produce uniform distribution**; for open addressing, it must also avoid clustering (runs of consecutive occupied slots).
- **Division method uses prime table sizes** for better distribution; multiplication method is less sensitive to table size choice.
- **K-independent hashing** provides provable guarantees for specific collision resolution schemes.
- **Poisson distribution**: In the limit, bucket occupancy follows Poisson with λ = α for an ideal hash function.
