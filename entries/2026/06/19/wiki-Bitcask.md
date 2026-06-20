---
source: sources/wiki-Bitcask.md
source_url: https://en.wikipedia.org/wiki/Bitcask
---

## Bitcask: Log-Structured Hash Table for Key/Value Storage

Bitcask is a storage engine developed by Basho Technologies (the creators of Riak) that combines an append-only log-structured file format on disk with an in-memory hash table for key lookups. It provides a simple API for storing and retrieving key/value data, drawing its design from log-structured file systems and log-file merging techniques.

## Key Concepts

- **Append-only, write-once disk format**: All writes go to the end of the current active file; data is never modified in place.
- **In-memory hash table of all keys**: Every key in the dataset is held in memory, mapping directly to the on-disk byte offset where the value resides.
- **Single disk seek per read**: The hash table gives the exact location on disk, so at most one seek is needed (and OS filesystem caching may eliminate even that).
- **Log-structured merging**: Older log files are periodically compacted/merged to reclaim space from overwritten or deleted keys — similar to LSM-tree compaction but simpler since the index is a hash table, not a sorted structure.
- **Checksum-based integrity**: Records include checksums, enabling fast verification during crash recovery.
- **Critical constraint — keys must fit in RAM**: The entire keyspace must be held in memory. This is Bitcask's primary limitation and determines its capacity ceiling.

## Commands and Syntax

Bitcask is an Erlang library; its API is programmatic rather than CLI-based. The core operations are:

- `bitcask:open(Directory, Opts)` — open or create a Bitcask store
- `bitcask:put(Ref, Key, Value)` — write a key/value pair (append to log)
- `bitcask:get(Ref, Key)` — retrieve a value by key (single seek)
- `bitcask:delete(Ref, Key)` — mark a key as deleted (tombstone append)
- `bitcask:merge(Directory)` — compact old log files, reclaiming space

## Relationships

- **Riak KV**: Bitcask was designed as the default storage backend for Riak. Alternative Riak backends include LevelDB (sorted, disk-based index) which trades Bitcask's speed for the ability to handle keyspaces larger than RAM.
- **LSM-Trees**: Bitcask shares the append-only write path with LSM-tree engines (LevelDB, RocksDB) but differs fundamentally in its read path — hash table lookup vs. multi-level sorted search.
- **Log-structured file systems**: Bitcask's design is directly inspired by log-structured FS principles (sequential writes, background compaction).
- **Write-ahead logs (WAL)**: Bitcask's data file essentially *is* the WAL — there is no separate log and data store, which simplifies the architecture.

## Exam-Relevant Points

- **Read performance**: Exactly one disk seek per read (or zero with OS cache hit) — this is a defining characteristic.
- **Write performance**: Always sequential (append-only), so write throughput is bounded by disk bandwidth, not random I/O.
- **Memory requirement**: All keys must fit in memory. This is the key trade-off and the primary reason to choose an alternative engine.
- **Crash recovery**: Fast and bounded — only the tail of the last active file needs to be checked; partial writes are detected via checksums.
- **Compaction/merging**: Required to reclaim disk space from updated/deleted keys; without it, disk usage grows without bound.
- **Predictable latency**: Both reads and writes have fixed, predictable performance characteristics — no variance from tree rebalancing or multi-level lookups.
- **Use case fit**: Ideal for workloads where the number of distinct keys is bounded and fits in RAM, especially write-heavy or mixed read/write workloads requiring low, predictable latency.
