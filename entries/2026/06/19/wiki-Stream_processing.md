---
source: sources/wiki-Stream_processing.md
source_url: https://en.wikipedia.org/wiki/Stream_processing
---

## Stream Processing: Paradigm, Architecture, and Parallel Computation

Stream processing is a programming paradigm that treats continuous sequences of data elements (streams) as the central objects of computation. It encompasses dataflow programming, reactive programming, and distributed data processing. The paradigm simplifies parallel execution by restricting computation to applying kernel functions to each element in a stream, enabling automatic optimization of memory access and parallelism by compilers and hardware.

## Key Concepts

- **Stream**: A sequence of data elements (events, records) flowing through a system over time
- **Kernel function (compute kernel)**: An operation applied to each element in a stream; kernels are typically pipelined for efficiency
- **Uniform streaming**: Applying the same kernel function to every element in a stream (the most common pattern)
- **Data-centric model**: Stream processing is a compromise — excellent for DSP/GPU workloads (image, video, signal processing) but less suited for random-access patterns like databases
- **Three characteristics that make applications suitable for stream processing**:
  - **Compute intensity**: High ratio of arithmetic operations to I/O (often >50:1 in signal processing)
  - **Data parallelism**: Same function applied to all records independently, with no inter-record dependencies
  - **Data locality**: Data produced once, read once or twice, then never again — intermediate streams capture this naturally
- **Write-only output constraint**: For each record, you can read input, perform operations, and write output — but never have memory that is both readable and writable simultaneously
- **AoS vs SoA**: Array-of-Structures layout is cache-unfriendly for SIMD; Structure-of-Arrays reorganizes data for contiguous, aligned access — a key concern in stream processor programming
- **Stream Register File (SRF)**: A large on-chip cache shared across ALU clusters where stream data is staged before bulk transfer to external memory; the compiler automates allocation
- **Three-tiered memory hierarchy**: External memory → SRF (shared cache) → Local Register Files (per-ALU) — keeps temporary data away from slow memory
- **Short stream effect**: Penalty incurred when streams are too small to amortize kernel-switching and setup costs
- **~90% of stream processor work is done on-chip**, requiring only ~1% of global data to be stored to external memory

## Commands and Syntax

**Continuous SQL query** — joining two event streams with a time window:
```sql
SELECT DataStream
   Orders.TimeStamp, Orders.orderId, Orders.ticker,
   Orders.amount, Trade.amount
FROM Orders
JOIN Trades OVER (RANGE INTERVAL '1' SECOND FOLLOWING)
ON Orders.orderId = Trades.orderId;
```

**Complex event processing (CEP) pattern detection**:
```
WHEN Person.Gender EQUALS "man" AND Person.Clothes EQUALS "tuxedo"
FOLLOWED-BY
  Person.Clothes EQUALS "gown" AND
  (Church_Bell OR Rice_Flying)
WITHIN 2 hours
ACTION Wedding
```

**RaftLib (C++ stream processing)**:
```cpp
// Link kernels as a dataflow graph using stream operators
m += hello >> p;
m.exe();
```

**Paradigm comparison for adding two arrays of 100 4-component vectors**:
- Sequential: `for` loop over 400 elements — one operation at a time
- SIMD/SWAR: `for` loop over 100 elements — vectorized 4-wide operations
- Stream: Define entire dataset + kernel; runtime unrolls across hundreds of ALUs

## Relationships

- **Dataflow programming**: Stream processing is a descendant; explored in the 1980s (e.g., SISAL language)
- **Reactive programming**: Stream processing encompasses reactive paradigms
- **SIMD/MIMD**: Stream processing is a branch of SIMD/MIMD but achieves far greater performance (>10x on dedicated hardware vs ~1.5x on generic CPUs) due to efficient memory access patterns
- **GPU computing**: GPUs are the most widespread consumer stream processors; evolved from fixed-function graphics pipelines to programmable stream architectures (R2xx/NV2x through R8xx generations)
- **Complex Event Processing (CEP)**: Stream processing enables pattern detection across event flows — composing simple events into complex/composite events
- **Hardware acceleration**: FPGAs, GPUs, and specialized processors (Imagine, Merrimac, Cell, Storm-1) implement stream processing in silicon
- **Batch processing**: Stream processing is its real-time counterpart — processing data as it arrives rather than in accumulated batches
- **PCI Express / communication latency**: The biggest bottleneck for stream processors; small datasets may not benefit due to setup overhead

## Exam-Relevant Points

- Stream processing applies **kernel functions** to **each element** in a stream — the fundamental abstraction
- The three suitability criteria are **compute intensity**, **data parallelism**, and **data locality**
- Stream processing memory is **write-only for output** — no memory region is both readable and writable
- **SoA (Structure of Arrays)** layout is preferred over AoS for SIMD/stream efficiency because it keeps like-typed data contiguous
- Dedicated stream processors achieve **>10x speedup** over sequential; generic CPUs see only **~1.5x** from stream techniques
- The **Stream Register File (SRF)** is the key architectural innovation — compiler-managed shared cache between ALU clusters and external memory
- **Short stream effect**: Small streams don't amortize kernel-switching costs — a key limitation
- **Pipeline depth** on GPUs can exceed **200 stages**; switching pipeline state is expensive (mitigated by techniques like über shaders and texture atlases)
- Stanford's **Imagine** (2002) and **Merrimac** (2004) were foundational research projects led by William Dally
- **Continuous SQL queries** with time windows (RANGE INTERVAL, OVER) are the primary query language mechanism for stream processing
- GPU evolution for stream processing: Pre-R2xx (no explicit support) → R2xx (vertex only) → R3xx (branching) → R8xx (append/consume buffers, atomic operations)
