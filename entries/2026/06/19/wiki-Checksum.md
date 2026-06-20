---
source: sources/wiki-Checksum.md
source_url: https://en.wikipedia.org/wiki/Checksum
---

## Checksums: Error Detection in Data Transmission and Storage

A checksum is a small block of data derived from a larger data block, used to detect errors introduced during transmission or storage. Checksums verify data integrity but not data authenticity. The checksum function (algorithm) produces significantly different output values even for small input changes, especially when using cryptographic hash functions. Checksums are related to but distinct from hash functions, fingerprints, and cryptographic hash functions — each serves different design goals.

## Key Concepts

- **Checksum** — a fixed-size value computed from arbitrary-size data for error detection purposes
- **Data integrity vs. data authenticity** — checksums verify integrity (data unchanged) but do NOT verify authenticity (data from trusted source)
- **Check digits and parity bits** are special cases of checksums for small data blocks (SSNs, bank accounts, single bytes)
- **Error-correcting codes** extend checksums to not only detect errors but recover original data in certain cases
- **Hypercube model** — an m-bit message with n-bit checksum maps to a corner of an (m+n)-dimensional hypercube; good algorithms spread valid corners far apart to maximize detection of typical errors
- **Fuzzy checksums** — reduce content to a characteristic minimum before checksumming, allowing detection of near-duplicate content (used in spam detection)

## Commands and Syntax

- **`cksum`** — Unix utility that computes a CRC checksum for files
- **`md5sum`** — computes MD5 hash digest
- **`sha1sum`** — computes SHA-1 hash digest
- No configuration syntax per se; checksums are computed algorithmically and appended to or stored alongside data

## Algorithms (simplest to most robust)

| Algorithm | Method | Weakness |
|-----------|--------|----------|
| **Parity byte (LRC)** | XOR all fixed-width words; append result | Misses two-bit errors at same position in different words; misses word reordering |
| **Sum complement** | Sum all words as unsigned integers, append two's complement of total | Same class of weaknesses; used in SAE J1708 |
| **Position-dependent** (Fletcher, Adler-32, CRC) | Considers both value AND position of each word | Higher computation cost but detects reordering, insertion, and deletion of zero-words |
| **Fuzzy checksum** | Reduces body to characteristic minimum, then checksums normally | Designed for near-duplicate detection (spam), not bit-level integrity |

## Relationships

- **Hash functions** — checksums are a subset; hash functions serve broader purposes (indexing, deduplication)
- **Cryptographic hash functions (HMAC)** — when both integrity and authenticity are needed, checksums become primitives within larger authentication schemes
- **CRC (Cyclic Redundancy Check)** — the most widely used position-dependent checksum in practice (Ethernet, ZIP, PNG)
- **Error-correcting codes** (Hamming, Reed-Solomon) — build on checksum concepts but add recovery capability
- **File systems** — Bcachefs, Btrfs, ReFS, and ZFS use checksums for automatic file integrity checking
- **IPv4 header checksum** — protocol-level application of checksums for network reliability
- **Parity bits** — simplest single-bit checksum; foundation concept

## Exam-Relevant Points

- Checksums verify **integrity**, not **authenticity** — this distinction is frequently tested
- **Parity (XOR) checksum** detects all odd-number-of-bit errors but misses even-number errors at corresponding positions across words; probability of undetected two-bit error is **1/n**
- **Position-dependent checksums** (Fletcher, Adler-32, CRC) overcome weaknesses of simple parity/sum by incorporating word position — they detect reordering, insertion, and deletion of zero-words
- **Two's complement sum** — the receiver adds all words including checksum; result must be all zeros or an error occurred
- The **hypercube model** formalizes checksum quality: a k-bit error moves a message k steps from its valid corner; good algorithms maximize distance between valid corners
- **CRC** is the dominant checksum in practice for data-intensive systems (networking, storage, file formats)
- File systems that perform **automatic integrity checking via checksums**: Bcachefs, Btrfs, ReFS, ZFS
- Checksums serve as **cryptographic primitives** in larger authentication algorithms — not standalone authentication
