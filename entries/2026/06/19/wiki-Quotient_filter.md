---
source: sources/wiki-Quotient_filter.md
source_url: https://en.wikipedia.org/wiki/Quotient_filter
---

## Quotient Filter: Space-Efficient Probabilistic Set Membership

A quotient filter is a space-efficient probabilistic data structure for approximate membership queries (AMQ). It tests whether an element belongs to a set, returning either "definitely not present" (no false negatives) or "probably present" (with false positive probability ε). Unlike Bloom filters, quotient filters support efficient merging and resizing without rehashing original keys, making them particularly valuable in log-structured merge-tree (LSM-tree) storage systems.

## Key Concepts

- **AMQ filter**: Supports insert, query, and optionally delete. False positive rate increases as more elements are added.
- **Fingerprint partitioning**: A hash function produces a *p*-bit fingerprint, split into a *q*-bit **quotient** (most significant) and an *r*-bit **remainder** (least significant). The table has 2^q slots.
- **Canonical slot**: Slot dQ is the "home" slot for a key with quotient dQ. If occupied, the remainder is stored in a slot to the right.
- **Run**: A contiguous set of slots holding remainders that share the same quotient. Runs are kept in sorted order.
- **Cluster**: A contiguous sequence of runs, starting where a run's first fingerprint occupies its canonical slot, ending at an empty slot or another cluster's start.
- **Three metadata bits per slot**:
  - `is_occupied` — this slot is the canonical slot for some key in the filter
  - `is_continuation` — this slot holds a non-first remainder in a run
  - `is_shifted` — the remainder here has been displaced from its canonical slot
- **Hard collision**: Two keys hash to the same fingerprint (causes false positives)
- **Soft collision**: Two keys have different fingerprints but the same quotient (handled by runs)
- **Cluster length**: With uniform hashing, most runs are O(1) length; all runs are highly likely O(log m) where m is the number of slots
- **False positive rate**: Approximately 2^(-r), where r is the remainder size. Controlled by adjusting r independently of table size.

## Commands and Syntax

No CLI commands — this is a data structure specification. Key algorithmic procedures:

**Lookup procedure**:
1. Hash key d to fingerprint dH; extract quotient dQ and remainder dR
2. Check canonical slot dQ — if all three metadata bits are false, element is definitely absent
3. If occupied, scan left from dQ to find the cluster start (first slot with `is_shifted` = false)
4. Scan right, maintaining a running count: increment for each `is_occupied` slot left of canonical, decrement for each `is_continuation` = false slot (run boundary)
5. When count reaches zero, scan the run comparing remainders to dR

**Insert procedure**:
1. Follow lookup path until element is confirmed absent
2. Insert remainder in sorted position within the run
3. Shift all subsequent remainders in the cluster rightward
4. Update metadata: `is_shifted` on displaced remainders, `is_continuation` on non-first run entries
5. `is_occupied` is a property of the slot position, not the remainder — it does not shift

**Merge procedure**:
1. Walk each filter left-to-right reconstructing full fingerprints from quotients + remainders (output is sorted)
2. Merge the two sorted lists
3. Populate a new filter from the merged list — no access to original keys required

## Relationships

- **Bloom filter**: The most well-known AMQ alternative. Quotient filters use comparable space but support merging and resizing without rehashing. Quotient filters use less space than Bloom filters when target false-positive rate < 1/64 (Pandey 2017).
- **Cuckoo filter**: Another AMQ alternative (see-also relationship).
- **Log-structured merge-tree (LSM-tree)**: Primary application context. Quotient filters attached to sub-trees (e.g., Wanna-B-trees in SAMT) can be merged during compaction without re-reading keys from disk.
- **Hash tables**: Quotient filters are built on compact hash tables (Cleary 1984) where entries store only partial keys plus metadata bits, avoiding pointer-based overflow chains.
- **Bigtable / Webtable**: Example of large databases using per-sub-table AMQ filters to avoid unnecessary I/O on queries.

## Exam-Relevant Points

- Quotient filters produce **no false negatives** but have a tunable false positive rate ε ≈ 2^(-r)
- The fingerprint is split into **quotient** (q bits, selects slot) and **remainder** (r bits, stored in slot) — this is the "quotienting" technique attributed to Knuth
- Three metadata bits per slot (`is_occupied`, `is_continuation`, `is_shifted`) enable reconstructing which quotient each remainder belongs to
- **Key advantage over Bloom filters**: quotient filters can be merged and resized without access to original keys, because fingerprints can be fully reconstructed from stored quotients and remainders
- Fingerprints are stored in **sorted order** by construction (runs ordered by quotient, remainders sorted within runs), enabling merge via simple sorted-list merge
- Load factor α = n/m; false positive probability ≈ 1 - e^(-α/2^r) ≤ 2^(-r)
- Quotient filters are especially beneficial for **LSM-tree compaction** where merging sub-tree filters without disk I/O for original keys is critical
- History: compact hash table by Cleary (1984), named "quotient filter" by Bender et al. (2011), hardware-optimized counting version by Pandey et al. (2017)
- Space advantage over Bloom filters specifically when false-positive rate target is **less than 1/64**
