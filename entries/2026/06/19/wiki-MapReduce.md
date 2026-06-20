---
source: sources/wiki-MapReduce.md
source_url: https://en.wikipedia.org/wiki/MapReduce
---

## MapReduce: Parallel Data Processing Framework

MapReduce is a programming model and framework for processing large datasets using parallel and distributed computation across clusters of machines. It decomposes work into a **map** phase (filtering/transformation applied independently to input partitions) and a **reduce** phase (aggregation of mapped outputs by key), with the framework handling distribution, shuffling, fault tolerance, and redundancy. Its key contribution is not the map/reduce primitives themselves but the scalability and fault tolerance achieved through parallelization. MapReduce is a specialization of the *split-apply-combine* strategy, inspired by functional programming's map and reduce, though semantically different.

## Key Concepts

- **Three core operations**: Map (apply function to local data), Shuffle (redistribute by output key), Reduce (aggregate per key in parallel)
- **Key/value pair model**: Map takes `(k1, v1)` and emits `list(k2, v2)`; Reduce takes `(k2, list(v2))` and emits `list(k3, v3)` — transforms one list of pairs into another
- **Data locality**: processing occurs near where data is stored to minimize communication overhead
- **Fault tolerance**: if a node fails, master reassigns its work to another node; atomic file-naming operations prevent conflicting parallel threads
- **Shuffle is often the bottleneck**: optimizing communication cost is essential; shuffle can take longer than computation depending on network bandwidth
- **Six extensible components** (hot spots): input reader, Map function, partition function, comparison function, Reduce function, output writer
- **Input splits**: typically 64–128 MB per split, one split per mapper
- **Partition function**: assigns map output to reducers, typically `hash(key) mod num_reducers`; poor partitioning causes skew and straggler reducers
- **Combiner function**: optional module that reduces data volume between map and reduce (local pre-aggregation)
- **Monoid requirement**: the reduce operation must be associative with a neutral element — this is the mathematical basis for correctness under arbitrary regrouping
- **Not always faster**: single-threaded MapReduce is usually slower than a traditional implementation; benefits only materialize with multi-threaded execution on multi-processor hardware and large datasets
- **Batch-oriented**: tasks are acyclic dataflow programs (stateless mapper → stateless reducer), making iterative algorithms and repeated queries difficult
- **Google deprecated MapReduce** as primary big data model by 2014 in favor of streaming systems (Percolator, FlumeJava, MillWheel)

## Commands and Syntax

**Canonical word count example:**
```
function map(String name, String document):
    for each word w in document:
        emit (w, 1)

function reduce(String word, Iterator partialCounts):
    sum = 0
    for each pc in partialCounts:
        sum += pc
    emit (word, sum)
```

**Average contacts by age (with counting for correctness):**
```
function Map:
    input: integer K1 (batch of 1M records)
    for each record:
        let Y = person's age
        let N = number of contacts
        produce (Y, (N, 1))

function Reduce:
    input: age Y
    for each (Y, (N, C)):
        S += N * C
        Cnew += C
    produce (Y, (S/Cnew, Cnew))
```

**SQL equivalent** of the MapReduce average example:
```sql
SELECT age, AVG(contacts)
  FROM social.person
GROUP BY age
ORDER BY age
```

**Logical signatures:**
- `Map(k1, v1) → list(k2, v2)`
- `Reduce(k2, list(v2)) → list(k3, v3)`

## Relationships

- **Apache Hadoop**: most popular open-source MapReduce implementation; older versions had NameNode as single point of failure
- **Distributed file systems** (e.g., HDFS, GFS): provide stable input/output storage; transient data stored on local disk
- **Higher-level abstractions**: Pig/PigLatin, Apache Hive, Sawzall address MapReduce's low-level interface by adding schema support and query languages
- **Successor systems**: Google moved to Percolator (incremental), FlumeJava (pipeline optimization), MillWheel (streaming) — all offer continuous processing vs. batch
- **Apache Mahout**: moved away from MapReduce to less disk-oriented mechanisms
- **Functional programming**: map and reduce originate from FP but MapReduce semantics differ (list-of-pairs → list-of-pairs vs. list → single value)
- **MPI (Message Passing Interface)**: MapReduce's reduce/scatter operations resemble MPI's 1995 standard operations
- **Parallel databases** (Teradata, RDBMS): critics argue these offer advantages for complex processing and enterprise use; MapReduce is better for simple or one-time processing
- **Graph processing and iterative algorithms**: MapReduce's acyclic dataflow is a poor fit; led to systems like Pregel and Spark

## Exam-Relevant Points

- MapReduce's value is **scalability and fault tolerance**, not the map/reduce primitives themselves
- The reduce operation **must be associative with a neutral element** (monoid); average is NOT directly reducible — you must carry counts (moments) to compute it correctly across multiple reduce stages
- **Partition function** defaults to `hash(key) % num_reducers`; skewed partitioning creates straggler reducers
- Input splits are typically **64–128 MB**
- The **shuffle phase** often dominates total cost; communication cost frequently exceeds computation cost
- MapReduce is **not effective for small datasets** that fit in memory — crash recovery overhead only pays off at scale
- MapReduce programs are **stateless and acyclic** — this limits iterative algorithms (graph processing, ML training loops)
- **Combiners** reduce intermediate data volume (local pre-aggregation on the mapper side before shuffle)
- Google **stopped using MapReduce as primary model by 2014**, replaced by streaming/incremental systems
- The **counting trick for averages**: when reducing in multiple stages, you must carry both sum and count; otherwise, re-reducing averages produces incorrect results (weighted average problem)
- **Fault recovery mechanism**: master node detects silent workers, reassigns their work; individual operations use atomic file renames to prevent conflicts
- Data locality optimization: assign mappers to nodes where data resides; schedule reducers close to their input data
