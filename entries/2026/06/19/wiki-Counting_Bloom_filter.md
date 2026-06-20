---
source: sources/wiki-Counting_Bloom_filter.md
source_url: https://en.wikipedia.org/wiki/Counting_Bloom_filter
---

## Counting Bloom Filters and Invertible Variants

A **counting Bloom filter** (CBF), also called a **spectral Bloom filter**, is a probabilistic data structure that tests whether the number of occurrences of an element exceeds a given threshold. It generalizes the standard Bloom filter by replacing single bits with counters, enabling frequency-based queries. Like standard Bloom filters, false positives are possible but false negatives are not — queries return either "possibly >= threshold" or "definitely < threshold."

## Key Concepts

- **Counter array instead of bit array**: A CBF uses *m* counters (all initialized to 0) instead of *m* bits, allowing it to track element frequency, not just membership.
- **Add operation**: Hash the element with *k* hash functions to get *k* positions, then **increment** each counter (vs. setting bits to 1 in a standard Bloom filter).
- **Threshold query (θ)**: Hash the element to *k* positions. If **any** counter < θ, the element's count is definitely < θ. If **all** counters >= θ, the count is possibly >= θ (may be a false positive).
- **Deletion introduces false negatives**: Decrementing counters to delete elements that were never inserted can produce false negatives — a key difference from standard Bloom filters.
- **Relationship to count-min sketch**: A CBF is essentially the same data structure as a count-min sketch, but used differently (threshold testing vs. frequency estimation).
- **False positive probability**: Follows a binomial distribution model — the probability a single counter reaches value *l* is b(l, kn, 1/m). The overall false positive rate is p_fp(θ, k, n, m) = (1 - Σ_{l<θ} b(l, kn, 1/m))^k. When θ=1, this reduces to the standard Bloom filter FP rate.
- **Optimal k**: For fixed n and m, there exists a k_opt that minimizes false positives. For θ > 30, the approximation k_opt ≈ (m/n)(0.2037θ + 0.9176) can be used.

## Commands and Syntax

**Invertible Bloom Filter (IBF) operations:**

Insert element x:
```
increment n
for each 1 ≤ i ≤ k do
    increment B[hi(x)].count
    add x to B[hi(x)].idSum
    add g(x) to B[hi(x)].hashSum
for each i in {1, 2} do
    increment C[fi(x)].count
    add x to C[fi(x)].idSum
    add g(x) to C[fi(x)].hashSum
```

Remove element x: same structure but decrement/subtract.

List remaining elements ("stragglers"): find pure cells where `g(idSum/count) = hashSum/count`, recover element as `idSum/count`, then remove or re-insert depending on sign of count. Falls back to secondary table C on conflicts.

## Relationships

- **Bloom filter**: CBF is a direct generalization — replace bits with counters, set-to-1 with increment. All Bloom filter hash function analysis applies.
- **Count-min sketch**: Structurally identical data structure, but CBF tests threshold membership while CMS estimates frequency.
- **Invertible Bloom filter (IBF)**: Extends CBF with `idSum` and `hashSum` fields per cell, enabling enumeration of remaining elements when the set is small. Uses a secondary hash table for conflict recovery.
- **Invertible Bloom lookup table (IBLT)**: Extends IBF to store key-value pairs by adding a `valueSum` field. Used in databases, networking, and data compression.
- **Hash tables**: IBFs and IBLTs are built on hash table structures with multiple hash functions.
- **Binomial distribution**: The mathematical foundation for analyzing false positive probability.

## Exam-Relevant Points

- A counting Bloom filter replaces bits with counters and increments on insert — this is the core generalization from standard Bloom filters.
- Query semantics: "any counter < θ" means definitely below threshold; "all counters >= θ" means possibly at or above threshold.
- **Deletion is dangerous**: decrementing counters for never-inserted elements introduces false negatives, breaking the standard Bloom filter guarantee.
- When θ = 1, the CBF false positive formula reduces exactly to the standard Bloom filter false positive formula.
- A CBF and a count-min sketch are the same data structure used for different purposes.
- The optimal number of hash functions k_opt depends on the threshold θ, not just on m and n as in a standard Bloom filter. For θ > 30, use k_opt ≈ floor/ceil of (m/n)(0.2037θ + 0.9176).
- An IBF can list remaining elements only if there are few enough — it is not guaranteed to recover all elements if too many hash collisions occur.
- An IBLT extends an IBF with associated values, making it applicable to database synchronization and data compression.
- Pure cell detection in IBFs uses the invariant: `g(idSum/count) = hashSum/count`.
