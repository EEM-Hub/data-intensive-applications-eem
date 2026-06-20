---
source: sources/wiki-Count_sketch.md
source_url: https://en.wikipedia.org/wiki/Count_sketch
---

## Count Sketch: A Dimensionality Reduction Method for Stream Frequency Estimation

Count sketch is a probabilistic data structure for dimensionality reduction, designed to approximate the frequency of elements in a data stream using sublinear space. Invented by Charikar, Chen, and Farach-Colton (2004) as an improvement to the AMS Sketch, it uses randomized hashing with sign functions and the median trick to provide robust frequency estimates. It is closely related to feature hashing but uses hash functions with lower dependence, making it more practical for large-scale applications in statistics, machine learning, and numerical linear algebra.

## Key Concepts

- **Core problem**: Approximating frequency moments of streams — counting occurrences of distinct elements without storing the entire stream.
- **Two families of hash functions**: `h_i: [n] → [w]` maps elements to buckets; `s_i: [n] → {+1, -1}` assigns random signs. Both must be drawn from pairwise independent families.
- **Data structure**: A `d × w` matrix of counters `C_{i,j}`, where `d = 2t + 1` rows (one per hash pair) and `w` columns (buckets per row).
- **Update rule**: For each stream element `q`, add `s_j(q)` to counter `C_{j, h_j(q)}` for each row `j`.
- **Query/estimation**: The frequency estimate for element `q` is `r_q = median over i of s_i(q) · C_{i, h_i(q)}`.
- **Median trick**: Uses the median (not mean) across rows to aggregate estimates, providing robustness against hash collisions with high-frequency elements. This is what distinguishes count sketch from simpler averaging approaches.
- **Unbiased estimator**: Each `s_i(q) · C_{i, h_i(q)}` is an unbiased estimate of the true frequency `n(q)`.
- **Variance bound**: `O(min{m_1² / w², m_2² / w})`, where `m_1` is stream length and `m_2²` is the second frequency moment.
- **Error guarantee**: The estimate is within `2·m_2 / √w` of the true value with probability `1 - e^{-O(t)}`.
- **Relation to feature hashing**: Nearly identical to Moody's feature hashing (1989), but count sketch's use of low-dependence hash functions gives it stronger theoretical guarantees.

## Commands and Syntax

**Intuitive construction (iterative):**
1. Start with a single hash `s` mapping elements to `{+1, -1}`, feeding one counter `C`. Estimate `n(q) ≈ E[C · s(q)]` — very noisy.
2. Use `d` independent sign hashes `s_i`, each with its own counter `C_i`. Average across `i` to reduce variance.
3. Replace each `C_i` with an array of `w` counters, indexed by bucket hash `h_i(q)`. This reduces collision frequency between distinct elements.

**Vector formulation:**
- Define sparse matrices `M^{(i)} ∈ {-1, 0, 1}^{w×n}` where `M_{h_i(j), j}^{(i)} = s_i(j)`.
- Sketch: `C^{(i)} = M^{(i)} · v` (linear projection from R^n to R^w).
- Reconstruct: `v_j* = median_i C_j^{(i)} · s_i(j)` (non-linear reconstruction).
- Guarantees hold with `m_1 = ||v||_1` and `m_2 = ||v||_2`.

## Relationships

- **AMS Sketch**: Count sketch was designed to speed up AMS Sketch (Alon, Matias, Szegedy 1999) for frequency moment approximation.
- **Count-Min Sketch**: A related structure with smaller memory requirements but weaker error guarantees (one-sided error vs. count sketch's two-sided).
- **Feature hashing**: Nearly identical algorithm; count sketch adds low-dependence hash guarantees.
- **Tensor sketch**: The count sketch of an outer product `x ⊗ x^T` equals the convolution of two independent count sketches `C^{(1)}x * C^{(2)}x^T` (Pham & Pagh 2013). This enables fast polynomial kernel approximation.
- **FFT**: Fast Fourier transform accelerates the convolution step in tensor sketch applications.
- **Kernel methods**: Count sketch enables explicit kernel approximations, replacing expensive implicit kernel computations.
- **Neural networks**: Used for bilinear pooling (compact bilinear pooling) in deep learning architectures.
- **Numerical linear algebra**: A cornerstone technique for randomized matrix algorithms (Woodruff 2014).
- **Khatri-Rao / face-splitting product**: Enables faster computation of tensor sketch structures than standard matrix operations.

## Exam-Relevant Points

- Count sketch uses **two** hash function families: bucket hashes `h_i` and sign hashes `s_i`, both requiring **pairwise independence**.
- The aggregation uses **median** (not mean) — this is the "median trick" that provides exponentially decreasing failure probability.
- The number of rows `d = 2t + 1` (odd, for well-defined median); increasing `t` improves success probability as `1 - e^{-O(t)}`.
- Error bound is `2·m_2 / √w` — increasing `w` (number of buckets per row) improves accuracy.
- Space complexity is `O(w · d)` counters — sublinear in stream length.
- Count sketch vs. Count-Min sketch tradeoff: Count-Min uses less space but only provides one-sided error (overestimates); count sketch provides two-sided error bounds.
- The vector formulation shows count sketch is a **linear** mapping (sketch step) followed by a **non-linear** reconstruction (median step).
- Tensor sketch connection: convolution of two count sketches equals the count sketch of the outer product — this is the foundation for fast explicit polynomial kernel approximation.
- The data structure supports **single-pass** streaming — each element is processed once and discarded.
