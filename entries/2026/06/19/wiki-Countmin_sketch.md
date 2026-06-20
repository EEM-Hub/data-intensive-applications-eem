---
source: sources/wiki-Countmin_sketch.md
source_url: https://en.wikipedia.org/wiki/Count–min_sketch
---

## Count–Min Sketch: Probabilistic Frequency Estimation

The count–min sketch (CM sketch) is a probabilistic data structure that estimates the frequency of events in a data stream. Invented by Cormode and Muthukrishnan (2003), it uses hash functions to map events to a compact two-dimensional array, trading exact accuracy for sub-linear space. It only overcounts (never undercounts) due to hash collisions, making it a one-sided error structure.

## Key Concepts

- **Structure**: A 2D array with *w* columns and *d* rows, where each row has an independent pairwise-independent hash function.
- **Parameter sizing**: *w* = ceil(*e*/epsilon), *d* = ceil(ln(1/delta)), where epsilon controls error magnitude and delta controls failure probability.
- **Update operation**: For each event of type *i*, hash *i* with each of the *d* hash functions to get a column index per row, then increment each of those *d* cells by one.
- **Point query**: Estimate frequency of event *i* by taking the **minimum** across all *d* rows: `a_hat_i = min_j count[j, h_j(i)]`.
- **One-sided error guarantee**: The estimate is always >= the true count. With probability 1 - delta, the estimate is at most `a_i + epsilon * N`, where N is total stream size.
- **Inner product query**: Two CM sketches (same hash functions) can estimate the inner product of their frequency vectors by summing element-wise products per row and taking the minimum across rows.
- **Linearity / mergeability**: CM sketches are linear — summing two sketches element-wise is equivalent to sketching the concatenated streams. This makes them suitable for distributed and parallel settings.
- **Bias**: The standard min estimator is biased (always overestimates). This works well for skewed distributions but is less accurate for uniform distributions.

## Commands and Syntax

No CLI commands — this is an algorithmic data structure. Pseudocode for core operations:

```
# Initialization
count[d][w] = all zeros
# d hash functions h_1..h_d, each mapping universe -> {0..w-1}

# Update(event i, count c=1):
for j in 1..d:
    count[j][h_j(i)] += c

# PointQuery(event i):
return min over j in 1..d of count[j][h_j(i)]

# Conservative Update(event i, count c=1):
est = PointQuery(i)
for j in 1..d:
    count[j][h_j(i)] = max(count[j][h_j(i)], est + c)

# Merge(sketch_A, sketch_B):  (same hash functions required)
for j, k: result[j][k] = sketch_A[j][k] + sketch_B[j][k]
```

## Relationships

- **Counting Bloom filter**: CM sketch can be viewed as an implementation of a counting Bloom filter, but sized relative to desired approximation quality rather than set cardinality.
- **Count sketch**: An alternative that uses mean-based estimation (better for non-skewed distributions) rather than min-based estimation.
- **Bloom filter**: Shares the hash-based, sub-linear space paradigm but answers membership queries rather than frequency queries.
- **Streaming algorithms**: CM sketch is a core primitive for processing data streams in a single pass with bounded memory.
- **Feature hashing / locality-sensitive hashing / MinHash**: Related probabilistic techniques using hashing for dimensionality reduction or similarity estimation.
- **Distributed systems**: Mergeability makes CM sketches composable across nodes — each node maintains a local sketch, and sketches are summed at aggregation points.

## Exam-Relevant Points

- The estimate **never undercounts** — error is strictly one-sided (overestimation only).
- Space is **sub-linear** in the universe size — O(w * d) = O((e/epsilon) * ln(1/delta)).
- Parameter formulas: **w = ceil(e/epsilon)**, **d = ceil(ln(1/delta))** — know how epsilon and delta map to width and depth.
- **Point query guarantee**: With probability >= 1 - delta, the overcount is at most epsilon * N (total stream size).
- The sketch is **linear/mergeable**: addition of sketches = sketch of concatenated streams. This is critical for distributed streaming.
- **Conservative update** reduces overestimation by only incrementing cells to `max(current, estimate + c)` — improves accuracy but **breaks linearity** (though still mergeable).
- **Maximum likelihood estimation** (Ting, 2018) always matches or beats the min estimator regardless of distribution skew.
- Hash functions must be **pairwise independent** (not fully independent).
- Unlike count sketch (which can underestimate), CM sketch's min-based approach guarantees a lower bound equal to the true frequency.
