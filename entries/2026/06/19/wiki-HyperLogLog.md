---
source: sources/wiki-HyperLogLog.md
source_url: https://en.wikipedia.org/wiki/HyperLogLog
---

## HyperLogLog: Probabilistic Distinct Count Estimation

HyperLogLog is a probabilistic algorithm for the count-distinct problem — estimating the number of unique elements in a multiset without storing them all. It achieves remarkable space efficiency: cardinalities exceeding 10^9 can be estimated with ~2% standard error using only 1.5 kB of memory. It extends the earlier LogLog algorithm (2003), which itself derives from the Flajolet-Martin algorithm (1984).

## Key Concepts

- **Core insight**: The cardinality of uniformly distributed random numbers can be estimated from the maximum number of leading zeros in their binary representations. If the max leading zeros observed is *n*, the estimated distinct count is 2^n.
- **Hash function role**: A hash function converts arbitrary input elements into uniformly distributed values, preserving cardinality while enabling the leading-zeros technique.
- **Stochastic averaging**: The single-estimate approach has high variance. HyperLogLog splits the hashed values into *m* subsets (registers), computes the max leading zeros per subset, then combines estimates using a **harmonic mean** to reduce variance.
- **Bias correction constant** (alpha_m): Corrects systematic multiplicative bias from hash collisions. Approximated as 0.7213/(1 + 1.079/m) for m >= 128.
- **Standard error**: sigma = 1.04 / sqrt(m), where m is the number of registers.
- **Space complexity**: O(epsilon^-2 * log log n + log n), where n is cardinality and epsilon is desired error.
- **Registers**: An array of m counters (typically sub-byte sized), each tracking the maximum rho(w) seen for its bucket.

## Commands and Syntax

**Three core operations:**

- **Add(v)**: Hash element v, use first b = log2(m) bits to select register j, compute rho(w) (position of leftmost 1) from remaining bits, set M[j] = max(M[j], rho(w)). Time: O(1).
- **Count**: Compute harmonic mean Z = (sum of 2^-M[j])^-1, then E = alpha_m * m^2 * Z. Time: O(m).
- **Merge(hll1, hll2)**: Element-wise max of register arrays: hll_union[j] = max(hll1[j], hll2[j]). Time: O(m).

**Small-range correction** (E < 5/2 * m): Use Linear Counting — E* = m * log(m/V) where V = count of zero registers. Skip if V = 0.

**Large-range correction** (E > 2^32/30 for 32-bit hashes): E* = -2^32 * log(1 - E/2^32).

**Intersection/difference**: Derivable via the inclusion-exclusion principle using merge + count.

## Relationships

- **Count-distinct problem**: HyperLogLog is the dominant practical solution for this class of problems in streaming/big-data contexts.
- **Flajolet-Martin algorithm** (1984): The foundational predecessor; HyperLogLog refines it through stochastic averaging.
- **Linear Counting**: Used as a fallback for small cardinalities where HyperLogLog is biased.
- **HLL++** (Google, 2013): Production improvement — uses 64-bit hashes (eliminating large-range correction), empirical bias correction for small cardinalities, and a sparse-to-dense register representation to save memory.
- **Streaming HLL / HIP estimator**: The Historic Inverse Probability estimator achieves 36% less memory for same error on single streams, provably optimal for single-stream scenarios.
- **HLL-TailCut+**: Trades 45% memory savings against loss of mergeability and order dependence.
- **Redis PFCOUNT/PFADD/PFMERGE**: Major production implementation with fixed register count, treating count/merge as O(1).
- **Harmonic mean**: Critical to variance reduction — chosen over arithmetic mean because it down-weights outlier registers.

## Exam-Relevant Points

- HyperLogLog estimates cardinalities > 10^9 with ~2% error using only **1.5 kB** of memory.
- Standard error formula: **1.04 / sqrt(m)** — doubling precision requires 4x the registers.
- Add is **O(1)**, count and merge are **O(m)**.
- The merge operation is a simple **element-wise max** of register arrays — this is what makes HyperLogLog composable across distributed systems (each node maintains a local sketch, merge produces the global sketch).
- Small cardinality bias: below **5/2 * m**, switch to **Linear Counting**; above **2^32/30**, apply large-range hash-collision correction.
- **HLL++ improvements**: 64-bit hash (no large-range correction needed), empirical small-range bias correction, sparse representation for low cardinalities.
- The algorithm lineage: Flajolet-Martin (1984) -> LogLog (2003) -> HyperLogLog (2007) -> HLL++ (2013).
- Space complexity is **O(epsilon^-2 * log log n + log n)** — the double-log of n is what gives the algorithm its name and its extreme space efficiency.
- Intersection and set difference cardinalities can be derived via **inclusion-exclusion** from merged sketches, but with compounding error.
- The "HyperLogLog sketch of S" refers to the register array M initialized from multiset S — this is the serializable data structure.
