---
source: sources/wiki-Log-structured_merge-tree.md
source_url: https://en.wikipedia.org/wiki/Log-structured_merge-tree
---

## Log-Structured Merge-Tree (LSM Tree)

The LSM tree is a data structure invented in 1996 by Patrick O'Neil, Edward Cheng, Dieter Gawlick, and Elizabeth O'Neil. It is designed to provide high-performance indexed access for workloads with high insert volume (e.g., transactional log data). It achieves this by maintaining data across two or more structures optimized for their respective storage media (memory vs. disk), synchronizing them efficiently in batches using a merge-sort-like process.

## Key Concepts

- **Two-level structure (C0/C1)**: C0 is a small, memory-resident sorted structure; C1 is a larger, disk-resident structure. New records go into C0 first.
- **Flush threshold**: When C0 exceeds a size threshold, a contiguous segment is removed and merged into C1 on disk.
- **Sequential writes**: Data is written sequentially rather than via random access, reducing seek time on HDDs and latency on SSDs.
- **Multi-level LSM trees**: Most practical implementations use multiple levels. Level 0 is in memory; on-disk data is organized into sorted *runs* (single files or collections of files with non-overlapping key ranges).
- **Sorted runs**: Each run contains data sorted by index key. A key may appear in multiple runs; the application determines how to resolve duplicates (newest wins, or aggregate).
- **Tombstones**: Deletes are recorded as tombstone entries (placeholders indicating deletion), removed during compaction/merging.
- **Write-ahead log (WAL)**: Used to ensure durability — all writes are logged before being added to the memory buffer, surviving crashes.
- **Bloom filters**: Probabilistic structures attached to each on-disk component to quickly determine if a key is absent, dramatically reducing unnecessary disk reads.
- **Leveling vs. Tiering**: Two compaction strategies with different trade-offs:
  - **Leveling**: One component per level, frequent merges — fewer components to search (better reads) but higher write amplification.
  - **Tiering**: Multiple components per level, less frequent merges — lower write amplification but higher read cost.
- **Stepped-Merge variant**: Supports multiple levels with multiple tree structures at each level.
- **LSbM-tree**: A variant (Log-Structured buffered-Merged tree) designed to re-enable effective buffer caching for mixed read/write workloads, where compaction operations would otherwise invalidate cached data.

## Commands and Syntax

No CLI commands or configuration syntax — this is a data structure specification. Key operations are:

- **Write**: Buffer in memory (skip list or B+ tree) -> flush sequentially to disk when full -> merge across levels using merge-sort-like process.
- **Point lookup**: Search C0 (memory) first, then C1, C2, C3... (disk levels, newest first). Check Bloom filters before accessing each disk component. Stop on first match.
- **Range query**: Scan each component from start to end of range, merge results via priority queue, reconcile duplicates/tombstones. Short-range scans touch all levels; long-range scans are dominated by the largest level.

## Relationships

- **B+ trees**: Extensions like bLSM and Diff-Index incorporate B+ tree structures into LSM trees. LSM trees are often compared against B+ trees as the two dominant indexing approaches for databases.
- **Write-ahead logging (WAL)**: Used alongside LSM trees for crash recovery and durability.
- **Merge sort**: The core compaction algorithm is reminiscent of merge sort.
- **Bloom filters**: Essential optimization for read performance in LSM trees; without them, point lookups degrade to O(L).
- **Skip lists**: Commonly used as the in-memory component (C0) implementation.
- **Apache Cassandra**: Real-world system using LSM trees with leveled compaction, where values represent database rows with different column sets across versions.
- **Storage media (HDD/SSD)**: LSM trees are specifically designed to exploit sequential I/O patterns that benefit both spinning disks and flash storage.

## Exam-Relevant Points

- **Write complexity**: O(T * L / B) for leveling merge policy, where T = size ratio between levels, L = number of levels, B = entries per page.
- **Point lookup complexity**: O(L) without Bloom filters; O(L * e^(-M/N)) for zero-result lookups with Bloom filters (M = total Bloom filter size, N = number of keys); O(1) for existing key lookups with Bloom filters.
- **Range query complexity**: O(L) for short-range queries (fewer keys than 2L); O(s/B) for long-range queries (s = number of keys in range).
- **Space complexity**: O((T+1)/T).
- **Leveling vs. Tiering trade-off**: Leveling reduces read cost at the expense of higher write amplification; tiering reduces write amplification at the expense of higher read cost. This is a fundamental design knob.
- **Tombstones are necessary** because disk components are immutable — deletes cannot modify existing sorted runs in place.
- **Updates are treated as new writes** (not in-place modifications), with older versions resolved during compaction.
- **Bloom filters are critical** for practical LSM tree performance — they convert O(L) lookups to near-O(1) for existing keys.
- **Sequential I/O is the key insight**: LSM trees convert random writes into sequential writes by batching and merging, which is why they outperform B-trees for write-heavy workloads.
