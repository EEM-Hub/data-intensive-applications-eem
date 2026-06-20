---
source: sources/wiki-External_sorting.md
source_url: https://en.wikipedia.org/wiki/External_sorting
---

## External Sorting Algorithms

External sorting is a class of sorting algorithms designed for datasets too large to fit in main memory (RAM), requiring data to reside in slower external memory such as disk drives. These algorithms are analyzed under the external memory model of computation, where performance is measured by the number of memory transfers between internal memory (size M) and external storage organized in blocks of size B. Asymptotically optimal external sorts achieve O((N/B) · log_{M/B}(N/B)) I/O operations.

## Key Concepts

- **External sorting** is required when data exceeds available RAM and must be sorted using disk-based storage
- Two main types: **external merge sort** (resembles merge sort) and **external distribution sort** (resembles quicksort)
- External merge sort uses a **hybrid sort-merge strategy**: sort phase creates sorted chunks that fit in RAM; merge phase combines them
- External distribution sort finds ~M/B pivots to partition data into equally-sized subarrays, recursing until subarrays fit in a block
- The **external memory model** measures cost in block transfers between internal memory (size M) and external memory (block size B)
- There is a **duality** (fundamental similarity) between merge-based and distribution-based external sorting approaches
- **Replacement-selection algorithm**: historically used instead of sorting for initial distribution, producing on average half as many output chunks of double length
- **K-way merge**: merging K sorted runs simultaneously in one pass, rather than repeated 2-way merges, reduces total passes over data
- Disk seek time vs. data transfer rate is a critical tradeoff — each seek on a typical HDD costs ~10ms, equivalent to transferring ~1MB
- Doubling available RAM halves the number of chunks AND halves reads per chunk, reducing seeks by ~75%

## Commands and Syntax

**Two-pass external merge sort (900 MB data, 100 MB RAM):**
1. Read 100 MB chunks into RAM, sort with quicksort, write sorted chunk to disk
2. Repeat until all data is in sorted chunks (9 chunks of 100 MB)
3. Allocate input buffers: 100 MB / (9 + 1) = 10 MB per buffer (9 input + 1 output)
4. Perform 9-way merge: read 10 MB from each chunk into buffers, output minimum repeatedly
5. When output buffer fills, flush to final file; when input buffer empties, refill from its chunk

**Three-pass sort (50 GB data, 100 MB RAM):**
1. Sort phase: create 500 × 100 MB sorted chunks
2. First merge: combine 25 chunks at a time → 20 × 2.5 GB sorted chunks (reads are 4 MB each)
3. Second merge: merge 20 × 2.5 GB chunks → single 50 GB sorted output

**Buffer sizing rule:** Memory / (number of chunks + 1) = per-buffer size. Larger output buffers may improve performance in practice.

## Relationships

- **Merge sort** — external merge sort is the external-memory generalization of merge sort
- **Quicksort** — external distribution sort is the external-memory analog of quicksort
- **K-way merge algorithm** — core subroutine for the merge phase of external merge sort
- **External memory model** — the theoretical framework for analyzing I/O complexity of these algorithms
- **Cache-oblivious algorithms** — achieve the same asymptotic bounds without knowing M and B parameters
- **Funnelsort / cache-oblivious distribution sort** — related cache-oblivious sorting algorithms
- **Radix sort** — used by some high-performance implementations for the initial binning phase
- **Solid-state drives** — change the performance calculus by reducing seek penalties, allowing fewer passes
- **Distributed sorting** — cluster-based parallelism as an alternative to multi-pass single-machine sorts

## Exam-Relevant Points

- **Optimal I/O complexity**: O((N/B) · log_{M/B}(N/B)) block transfers — know the formula and what M, B, N represent
- **Why K-way merge instead of 2-way**: each merge pass reads and writes every value, so fewer passes (even with costlier K-way merge) wins overall
- **When to add merge passes**: when buffer size drops below ~1 MB per chunk, seek time dominates transfer time — add another pass to increase buffer sizes
- **Seek vs. transfer tradeoff**: 10ms seek ≈ 1 MB transfer at 100 MB/s; buffer sizes < 1 MB mean most time is spent seeking
- **500 GB with 1 GB RAM** can be sorted in two passes before a third pass becomes beneficial
- **RAM impact**: doubling RAM reduces seeks by ~75% (halves chunks × halves reads per chunk)
- **Replacement selection** produces runs averaging 2× memory size, halving the number of initial chunks
- **Performance optimizations**: parallel disks, multi-threading, asynchronous I/O, SSD as intermediate tier, key-value separation for large records
- **Distribution sort pivot selection**: uses median-of-medians recursively on sampled elements to find √(M/B) pivots efficiently
- **Overall time complexity**: O(n log n), same as in-memory sorts — dataset growth requires linearly more passes, each O(n)
