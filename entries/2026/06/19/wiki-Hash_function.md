---
source: sources/wiki-Hash_function.md
source_url: https://en.wikipedia.org/wiki/Hash_function
---

## Hash Functions: Principles, Properties, and Implementation

Hash functions map data of arbitrary size to fixed-size values (hash codes), enabling near-constant-time data storage and retrieval. They are foundational to hash tables, caches, Bloom filters, distributed systems, and cryptographic applications. This page covers the mathematical properties a good hash function must satisfy, common algorithms for hashing integers and variable-length data, collision resolution strategies, and the distinction between non-cryptographic and cryptographic hash functions.

## Key Concepts

- **Hash function**: A deterministic function mapping arbitrary-size input to fixed-size output (hash value/hash code/digest)
- **Hash table**: A fixed-size table indexed by hash codes; the primary data structure that consumes hash function output
- **Collision**: When two distinct keys produce the same hash value — unavoidable in general (birthday problem), but should be minimized
- **Chained hashing**: Collision resolution where each bucket holds a linked list of colliding entries
- **Open addressing**: Collision resolution by probing other slots — linear probing, quadratic probing, or double hashing
- **Uniformity**: A good hash function distributes outputs evenly across the output range for any typical subset of inputs
- **Strict avalanche criterion**: Flipping any single input bit should change each output bit with 50% probability
- **Perfect hash function**: One that maps a known, static key set with zero collisions — computationally infeasible for large key sets
- **Universal hashing**: A randomized scheme selecting from a family of functions such that collision probability for any two keys is 1/m
- **Determinism**: A hash function must always produce the same output for the same input within its usage context (Python's SipHash uses per-process random seed — valid within one run but not across runs)
- **Data normalization**: Inputs must be normalized before hashing if equivalence classes exist (e.g., case-insensitive comparison requires uppercasing before hashing)

## Commands and Syntax

No CLI commands per se, but key algorithmic patterns:

- **Division hashing**: `h(K) = K mod M` where M is a prime near table size. Simple but slow (division is ~10x slower than multiplication on x86). Vulnerable to clustered keys sharing a common factor.
- **Multiplicative hashing**: `h(K) = floor(M * frac(K * A))` where A is an irrational constant (often golden ratio). Faster than division, better distribution.
- **Mid-squares**: Square the key, extract middle digits. E.g., key 123456789 squared = 15241578750190521, extract middle 4 digits → 8750.
- **Identity hash**: Use the data itself as the hash when small enough (e.g., 32-bit integers as Java hash codes).
- **Bit masking for power-of-2 tables**: `h(K) = K & (n-1)` — fast but requires uniform input distribution.
- **Variable range without division**: `h = n * P(key) >> b` where P is a PRNG uniform on [0, 2^b - 1].
- **Chi-squared test for uniformity**: Ratio near 1.0 (within 0.95–1.05) indicates good distribution.
- **Fibonacci hashing** (multiplicative): Multiply key by golden-ratio constant, take upper bits. Good avalanche properties.

## Relationships

- **Hash tables**: Primary consumer of hash functions; collision resolution (chaining vs. open addressing) is a co-design concern
- **Bloom filters**: Use multiple hash functions to test set membership probabilistically
- **Distributed hash tables (DHTs)**: Require dynamic hash functions with minimal movement property — consistent hashing
- **Cryptographic hash functions**: Stricter requirements (preimage resistance, collision resistance) vs. non-cryptographic hash functions optimized for speed
- **Checksums/fingerprints**: Related but distinct — hash functions optimize for distribution, checksums for error detection
- **Caches**: Simplified hash tables where collisions are resolved by eviction
- **Geometric hashing**: Partitions metric spaces into grid cells for proximity searches in graphics/computational geometry
- **Linear hashing / extendible hashing / spiral hashing**: Dynamic hash functions that minimize record relocation when table resizes

## Exam-Relevant Points

- A hash function must be **deterministic** — same input always yields same output (within its usage scope)
- **Uniformity** is the most important statistical property — uneven distribution degrades performance from O(1) toward O(n)
- **Birthday problem** makes some collisions inevitable even when table is much larger than the dataset
- **Division hashing** uses prime divisor; drawback is CPU cost of division and vulnerability to clustered keys
- **Multiplicative hashing** is faster and generally better distributed than division hashing
- Perfect hash functions exist only for **static, known key sets** and are computationally expensive to find
- **Universal hashing** guarantees collision probability of 1/m for any two keys, independent of input distribution
- The **strict avalanche criterion** means each output bit changes with 50% probability when any single input bit flips
- **Chi-squared test** is the standard method for measuring hash function uniformity (target ratio: 0.95–1.05)
- Python's hash randomization (SipHash with per-process seed) means hash values are **not stable across runs** — cannot be persisted
- **Open addressing** methods: linear probing (cache-friendly but clustering), quadratic probing (less clustering), double hashing (best distribution but cache-unfriendly)
- Hash function design is a **tradeoff**: search time vs. storage space; computation cost vs. collision rate
- Prefer faster hash functions over slower ones that save marginal collisions — collisions are rare and only cause marginal delay
- **Dynamic hash functions** (consistent hashing) minimize key relocation on resize — critical for distributed systems
