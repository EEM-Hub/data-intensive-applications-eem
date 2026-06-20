---
source: sources/wiki-Bloom_filter.md
source_url: https://en.wikipedia.org/wiki/Bloom_filter
---

## Bloom Filters: Probabilistic Set Membership

A Bloom filter is a space-efficient probabilistic data structure (conceived by Burton Howard Bloom in 1970) used to test whether an element is a member of a set. It guarantees no false negatives — queries return either "possibly in set" or "definitely not in set" — but allows false positives whose probability grows as more elements are added. Elements can be added but not removed from a standard Bloom filter.

## Key Concepts

- **Core structure**: A bit array of *m* bits (all initially 0) paired with *k* independent hash functions that map elements to array positions.
- **Add operation**: Hash the element with all *k* functions; set the resulting *k* bit positions to 1.
- **Query operation**: Hash the element with all *k* functions; if any resulting bit is 0, the element is definitely absent. If all are 1, the element is *possibly* present (could be a false positive).
- **No removal**: Clearing a bit for one element could invalidate other elements that share that bit position, introducing false negatives.
- **False positive probability**: Approximately `(1 - e^(-kn/m))^k`, where *n* is the number of inserted elements, *m* is the bit array size, and *k* is the number of hash functions.
- **Space efficiency**: Requires only ~9.6 bits per element for a 1% false positive rate, regardless of element size. Adding ~4.8 bits per element reduces the FP rate by a factor of 10.
- **Time complexity**: O(k) for both insertions and lookups — constant time independent of the number of elements in the set.
- **Counting Bloom filter**: A variant that replaces single bits with counters, enabling element removal at the cost of additional space.
- **Union and intersection**: Two Bloom filters with the same size and hash functions can be merged via bitwise OR (union, lossless) or AND (intersection, may overestimate false positive rate).
- **Cardinality estimation**: The number of items in a filter can be approximated as `n* = -(m/k) * ln(1 - X/m)`, where *X* is the number of bits set to 1.

## Commands and Syntax

**Optimal number of hash functions:**
```
k = (m/n) * ln(2)
```

**Required bits given desired false positive rate ε:**
```
m = -(n * ln(ε)) / (ln(2))^2
```

**Optimal bits per element:**
```
m/n ≈ -2.08 * ln(ε)
```

**Optimal number of hash functions from target FP rate:**
```
k = -ln(ε) / ln(2)
```

**Approximate item count from bit array state:**
```
n* = -(m/k) * ln(1 - X/m)
```

**Set union estimate:** Compute `|A ∪ B|` using bitwise OR of both filters, then apply the cardinality formula.

**Set intersection estimate:** `n(A ∩ B) = n(A) + n(B) - n(A ∪ B)` (inclusion-exclusion).

**Practical hash function design:** Rather than *k* independent hash functions, use enhanced double hashing or triple hashing — seed a simple RNG with two or three hash values to derive all *k* indices.

## Relationships

- **Hash functions**: Bloom filters depend on uniformly distributed, independent hash functions; enhanced double hashing and triple hashing are practical alternatives to truly independent functions.
- **Hash tables**: A hash table that ignores collisions and only tracks bucket occupancy is effectively a Bloom filter with k=1.
- **Bit arrays**: When the universe of possible elements is small, a deterministic bit array (1 bit per possible element) outperforms Bloom filters.
- **Probabilistic data structures family**: Related to Count-Min Sketch, Quotient filters, HyperLogLog, and Skip Lists.
- **Key-value stores / databases**: Used in Bigtable, HBase, Cassandra, ScyllaDB, and PostgreSQL to avoid unnecessary disk lookups for non-existent rows.
- **Content delivery / caching**: Akamai uses Bloom filters to prevent "one-hit-wonder" objects from polluting disk caches — only cache on the second request.
- **LSM-tree storage engines**: Bloom filters sit in front of SSTables to short-circuit reads for keys that don't exist in a given level.

## Exam-Relevant Points

- **Fundamental guarantee**: False positives are possible; false negatives are not. This is the defining property.
- **Cannot delete** from a standard Bloom filter without risking false negatives. Counting Bloom filters address this.
- **~9.6 bits per element** for 1% FP rate; each additional ~4.8 bits per element reduces FP rate by 10x.
- **Optimal k = (m/n) * ln(2)**: At the optimum, approximately half the bits in the array are set to 1.
- **m scales linearly with n** for a fixed FP rate; k depends only on the target FP rate, not on n.
- **O(k) time** for add and lookup — constant regardless of set size; k lookups are independent and can be parallelized in hardware.
- **Union via bitwise OR** is lossless (identical to building from scratch on the union set). Intersection via bitwise AND may have a higher FP rate than a from-scratch filter on the intersection set.
- **Real-world uses**: database read optimization (Bigtable, Cassandra, HBase), CDN cache admission (Akamai), malicious URL detection (Chrome historically), biological systems (fruit fly olfactory novelty detection).
- **Goel-Gupta upper bound**: `ε ≤ (1 - e^(-k(n+0.5)/(m-1)))^k` — a rigorous bound requiring no independence assumptions, equivalent to the approximation with a penalty of at most half an extra element and one fewer bit.
- **Filter regeneration**: When the FP rate becomes too high, the filter can be rebuilt from the original keys (assuming they are available), rather than trying to shrink or remove elements.
