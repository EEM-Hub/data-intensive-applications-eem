---
source: sources/wiki-Hash_join.md
source_url: https://en.wikipedia.org/wiki/Hash_join
---

## Hash Join Algorithms in Relational Databases

Hash joins are a family of join algorithms used by relational database management systems to efficiently combine rows from two relations. All variants build hash tables from one or both relations, then probe those tables so only tuples with matching hash codes are compared. They require an equijoin predicate and are typically more efficient than nested loop joins except when the probe side is very small.

## Key Concepts

- **Build phase**: Construct a hash table from the smaller relation (the "build input"), mapping composite join attribute values to remaining row attributes
- **Probe phase**: Scan the larger relation (the "probe input"), looking up each row's join key in the hash table to find matches
- **Classic hash join**: Simple two-phase algorithm; requires the build relation to fit in memory. When it doesn't, degenerates into a block nested loop pattern that rescans the probe input multiple times
- **Grace hash join**: Partitions both relations to disk using a hash function on the join key, then loads partition pairs into memory for joining. Avoids full rescans. Named after the GRACE database machine. Applies recursively with an orthogonal hash function if a partition still exceeds memory
- **Hybrid hash join**: Combines classic and Grace approaches — keeps "partition 0" of the build relation in memory during the partitioning phase, reducing I/O. Memory-sensitive due to competing demands between the in-memory hash table and output buffers for remaining partitions
- **Hash anti-join**: Evaluates NOT IN predicates. Left anti-join hashes the NOT IN side and selects probe rows with no hash match. Right anti-join hashes the FROM side and removes entries on each hit, returning what remains
- **Hash semi-join**: Returns each matching record from the leading table only once. Left semi-join hashes the IN side; right semi-join hashes the FROM side and removes entries after returning them to enforce uniqueness

## Commands and Syntax

No specific SQL commands — hash joins are chosen internally by the query optimizer. The key algorithmic procedures are:

**Classic hash join (pseudocode):**
1. For each tuple r in build input R, add to hash table
2. If hash table fills memory: scan probe input S, emit matches, reset hash table, continue
3. Final scan of S to emit remaining matches

**Grace hash join:**
1. Partition R and S to disk using hash function h on join key
2. For each partition pair: load smaller side, build hash table, probe with other side
3. If a partition exceeds memory, recursively repartition with a different hash function

## Relationships

- **Nested loop join**: Hash joins outperform nested loops except on very small probe inputs; the classic hash join's memory-overflow fallback is essentially a block nested loop
- **Sort-merge join**: Alternative join algorithm; hash joins are generally preferred for equijoins while sort-merge handles inequality predicates and pre-sorted data
- **Symmetric hash join**: A variant that allows pipelining by building hash tables on both sides simultaneously
- **Hash tables**: The core data structure underlying all hash join variants
- **Query optimizer**: Chooses between join algorithms based on table statistics, available memory, and predicate types
- **Disk I/O**: The primary cost differentiator between Grace and hybrid approaches — hybrid saves I/O by keeping partition 0 in memory

## Exam-Relevant Points

- Hash joins **require equijoin predicates** — they cannot be used for inequality joins
- The **smaller relation** should be the build side to minimize memory usage
- Classic hash join requires the build relation to **fit in memory**; Grace and hybrid variants handle the case when it does not
- Grace hash join partitions **both** relations to disk before joining partition pairs
- Hybrid hash join keeps **partition 0 in memory** during partitioning, saving disk I/O compared to Grace
- When the build relation nearly fits in memory, hybrid hash join behaves like classic hash join; otherwise it behaves like Grace
- For anti-joins: use **left anti-join when NOT IN table is smaller**, right anti-join when it is larger
- For semi-joins: use **left semi-join when IN table is smaller**, right semi-join when it is larger
- Right semi-join removes hash table entries after returning them to guarantee **at-most-once** semantics
- Grace hash join uses **recursive repartitioning** with orthogonal hash functions when partitions exceed memory
- The hybrid hash join was first described by DeWitt et al. (1984) in the context of main memory database systems
