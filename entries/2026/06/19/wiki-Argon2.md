---
source: sources/wiki-Argon2.md
source_url: https://en.wikipedia.org/wiki/Argon2
---

## Argon2: Memory-Hard Password Hashing and Key Derivation

Argon2 is a key derivation function that won the 2015 Password Hashing Competition. Designed by Biryukov, Dinu, and Khovratovich at the University of Luxembourg, it uses a large fixed-size memory region to make brute-force and GPU-based cracking attacks computationally expensive. Standardized in RFC 9106 (September 2021), it is the current recommended algorithm for password hashing.

## Key Concepts

- **Memory-hard function**: Argon2 deliberately requires a large amount of memory, making attacks on custom hardware (GPUs, ASICs) expensive because they must provision that memory per parallel guess.
- **Three variants**:
  - **Argon2d**: Password-dependent memory access order; maximizes GPU cracking resistance but vulnerable to side-channel attacks.
  - **Argon2i**: Password-independent memory access order; resists side-channel attacks but weaker against time-memory trade-off (TMTO) attacks.
  - **Argon2id**: Hybrid — uses Argon2i for the first half-pass over memory, then Argon2d for subsequent passes. **RFC 9106 recommends Argon2id as the default choice.**
- **Three tunable parameters**: execution time (iterations), memory required (memorySizeKB), degree of parallelism (threads).
- **Internal hash**: Built on **BLAKE2b** for all internal hashing, including the variable-length hash function that produces digests up to 2^32 bytes.
- **Memory array structure**: A two-dimensional array of 1 KiB blocks, organized as `parallelism` rows by `columnCount` columns, where `columnCount = Floor(memorySizeKB, 4*parallelism) / parallelism`.
- **Licensing**: Reference implementation is public domain (CC0) or Apache License 2.0.

## Commands and Syntax

**Algorithm inputs:**
```
password (P):       0..2^32-1 bytes
salt (S):           8..2^32-1 bytes (16 bytes recommended)
parallelism (p):    1..2^24-1 (number of threads)
tagLength (T):      4..2^32-1 bytes (output length)
memorySizeKB (m):   8p..2^32-1 KiB
iterations (t):     1..2^32-1
version (v):        0x13 (decimal 19)
key (K):            0..2^32-1 bytes (optional)
associatedData (X): 0..2^32-1 bytes (optional)
hashType (y):       0=Argon2d, 1=Argon2i, 2=Argon2id
```

**Algorithm outline:**
1. Concatenate all inputs with their lengths into a buffer; hash with `Blake2b(buffer, 64)` to produce H0 (64 bytes).
2. Compute `blockCount = Floor(memorySizeKB, 4*parallelism)` and `columnCount = blockCount / parallelism`.
3. Initialize columns 0 and 1 for each lane using `Hash(H0 || columnIndex || laneIndex, 1024)`.
4. Fill remaining columns using the compression function G, with block index selection varying by variant (Argon2d/i/id).
5. For additional iterations, XOR new G outputs with existing blocks.
6. XOR the last column of every row to produce final block C.
7. Output `Hash(C, tagLength)`.

## Relationships

- **Key derivation function (KDF)**: Argon2 belongs to the family of password-based KDFs alongside bcrypt, scrypt, and PBKDF2.
- **BLAKE2b**: The internal hash primitive; all Argon2 hashing (initial hash, block generation, variable-length output) is built on BLAKE2b.
- **Password Hashing Competition**: Argon2 was selected as the winner over competitors including Catena, Lyra2, Makwa, and yescrypt.
- **RFC 9106**: The IETF standard defining Argon2 for password hashing and proof-of-work applications.
- **Time-memory trade-off (TMTO)**: Argon2d's data-dependent access pattern specifically resists TMTO attacks.
- **Side-channel attacks**: Argon2i's data-independent access pattern specifically resists these; Argon2id provides a balance.
- **Compared to scrypt**: Both are memory-hard, but Argon2 offers tunable parallelism and was designed to address known weaknesses in scrypt's design.

## Exam-Relevant Points

- **Argon2id is the recommended variant** per RFC 9106 when you don't know which to choose or when side-channel attacks are a concern.
- **RFC 9106 recommended minimums**:
  - Default: **2 GiB memory, 1 iteration, parallelism 4**
  - Memory-constrained: **64 MiB memory, 3 iterations, parallelism 4**
- **Salt should be at least 16 bytes** for password hashing.
- **Argon2i cryptanalysis**: Attacks show Argon2i v1.3 needs **more than 10 passes** over memory to resist known space-reduction attacks. This is why Argon2id is preferred.
- **No public cryptanalysis exists for Argon2d** — known attacks target only Argon2i.
- **Version 1.3** (0x13) fixed a space-reduction attack on single-pass Argon2i that allowed computation with 1/4 to 1/5 of the desired memory.
- The memory array size must be a multiple of `4 * parallelism` KiB.
- Argon2 supports optional **key** and **associated data** inputs beyond password and salt.
- Argon2 is both a **password hashing function** and applicable to **proof-of-work** scenarios.
