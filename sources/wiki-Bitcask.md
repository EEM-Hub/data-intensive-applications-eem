---
source: https://en.wikipedia.org/wiki/Bitcask
fetched: 2026-06-19
---

|  | This article includes alist of references,related reading, orexternal links,but its sources remain unclear because it lacksinline citations.Please helpimprovethis article byintroducingmore precise citations.(December 2013)(Learn how and when to remove this message) |
| --- | --- |

 
| Bitcask |
| --- |
| Developer | Basho Technologies |
|  |
| Stable release | 2.1.0[1]/ 7 May 2020;6 years ago(7 May 2020) |
|  |
| Written in | Erlang |
| Operating system | Linux,BSD,Mac OS X,Solaris |
| Platform | IA-32,x86-64 |
| License | Apache License 2.0 |
| Website | docs.basho.com/riak/latest/ops/advanced/backends/bitcask/ |
| Repository | github.com/basho/bitcask |

  

**Bitcask** is an [Erlang](./Erlang_(programming_language)) application that provides an API for storing and retrieving key/value data into a log-structured [hash table](./Hash_table). The design owes a lot to the principles found in [log-structured file systems](./Log-structured_file_system) and draws inspiration from a number of designs that involve log file merging.

 

## Strengths

 

Bitcask has a number of advantages owing to its write-once, append-only on-disk data-format and its use of an in-memory hash-table of keys for lookups:

 
- Low latency for read and write operations.
- High throughput, especially when writing an incoming stream of random items: Because the data being written doesn't need to be ordered on disk and because the log-structured design allows for minimal disk-head movement during writes, these operations generally saturate the I/O and disk bandwidth.
- Single seek to retrieve any value: Bitcask's in-memory hash-table of keys points directly to the locations on disk where the data resides. Bitcask never needs more than one disk-seek to read a value, and the operating system's file-system caching can obviate the need for disk-seeks entirely for some lookups.
- Predictable lookup and insert performance: Read operations as well as write operations have fixed, predictable behavior. Write operations require only a seek to the end of the current file that is open for writing and an append to that file.
- Fast, bounded crash recovery: Bitcask's disk format makes recovery straightforward. The only items that might be lost are partially written records at the tail of the file last opened for writes. Recovery need only review the last record or two written and verify [checksums](./Checksum) to ensure that the data is consistent.
- Easy backup: Bitcask's disk format means that any utility that archives or copies files in disk-block order will properly backup or copy a Bitcask database.

 

## Weakness

 

Because Bitcask keeps all keys in memory at all times, the system must have enough memory to contain the entire keyspace in addition to other operational components and the operating system's file-system [buffers](./Buffer_(computer_science)).

 

## References

  
1. [↑](./Bitcask#cite_ref-wikidata-2cb53250703607ad7fb0550e9740c4e7c4ff366a-v20_1-0) ["Release 2.1.0"](https://github.com/basho/bitcask/releases/tag/2.1.0). 7 May 2020. Retrieved 28 October 2020.

 

## External links

 
- [Official Bitcask Design Paper](https://riak.com/assets/bitcask-intro.pdf)
- [Bitcask Capacity Calculator](http://docs.basho.com/riak/latest/ops/building/planning/bitcask/)
- [Bitcask: A Log-structured Hash Table for Fast Key-Value](http://highscalability.com/blog/2011/1/10/riaks-bitcask-a-log-structured-hash-table-for-fast-keyvalue.html/)