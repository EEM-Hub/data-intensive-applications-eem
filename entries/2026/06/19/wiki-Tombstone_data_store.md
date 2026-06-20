---
source: sources/wiki-Tombstone_data_store.md
source_url: https://en.wikipedia.org/wiki/Tombstone_(data_store)
---

## Tombstones in Distributed Data Stores

A tombstone is a marker record created when data is deleted in a distributed data store that uses eventual consistency. Rather than simply removing data, the system inserts a tombstone to prevent deleted records from being resurrected by nodes that were unavailable during the deletion. This is a fundamental mechanism for handling deletes correctly in eventually consistent systems.

## Key Concepts

- **Tombstone**: A special record that marks data as deleted without physically removing it; not returned in response to client requests
- **Resurrection problem**: Without tombstones, a node that missed a delete operation would interpret the absence of data on other nodes as a missed *insert* and re-propagate the deleted data
- **Eventual consistency interaction**: The "eventual" propagation of state means not all nodes see a delete immediately, making simple physical deletion unsafe
- **Tombstones are temporary**: They exist long enough for all nodes to learn about the deletion, then are garbage collected
- **Compaction**: The background process that physically removes tombstones after a grace period (term used in Apache Cassandra)

## Commands and Syntax

- **`GCGraceSeconds`** (Cassandra): Configuration parameter that controls how long tombstones are retained before being eligible for garbage collection during compaction
- Tombstoned columns return `null` on read (not an exception, in modern client libraries)
- Range queries (`get_range_slices`) will return rows with empty columns for tombstoned data until compaction runs

## Relationships

- **Eventual consistency**: Tombstones exist specifically because of the consistency model — they solve the delete-propagation problem inherent in systems where not all replicas are updated synchronously
- **Replication and anti-entropy**: Tombstones participate in replica synchronization protocols (read repair, anti-entropy) to propagate deletes
- **Storage engine / compaction**: Tombstone removal is tied to the LSM-tree compaction process in systems like Cassandra
- **Consistency levels**: A low `ConsistencyLevel` on reads may surface stale data before tombstones propagate
- **Distributed deletes vs. CRDTs**: Tombstones are one approach; conflict-free replicated data types offer alternatives for some data structures

## Exam-Relevant Points

- Tombstones prevent deleted data from being **resurrected** by out-of-date replicas — this is their core purpose
- Tombstones are **not returned to clients** but still consume storage and I/O until compacted
- **GCGraceSeconds** controls tombstone retention in Cassandra — setting it too low risks resurrection; too high wastes resources
- **Compaction** is resource-intensive — excessive tombstones degrade read performance because the system must skip over them
- After deletion but before compaction, queries may return **rows with empty columns** — applications must handle this
- The fundamental tension: tombstones must persist long enough for all replicas to see the delete, but not so long that they bloat storage and slow reads
