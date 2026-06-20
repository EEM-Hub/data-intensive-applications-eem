---
source: https://en.wikipedia.org/wiki/Write-ahead_logging
fetched: 2026-06-19
---

Family of computer science techniques 
|  | This articleneeds additional citations forverification.Please helpimprove this articlebyadding citations to reliable sources. Unsourced material may be challenged and removed.Find sources:"Write-ahead logging"–news·newspapers·books·scholar·JSTOR(June 2022)(Learn how and when to remove this message) |
| --- | --- |

 

In [computer science](./Computer_science), **write-ahead logging** (**WAL**) is a family of techniques for providing [atomicity](./Atomicity_(database_systems)) and [durability](./Durability_(database_systems)) (two of the [ACID](./ACID) properties) in [database systems](./Database_system).[[1]](./Write-ahead_logging#cite_note-Hellerstein_Stonebraker_Hamilton_p.-1)

 

A write ahead log is an append-only auxiliary disk-resident structure used for crash and transaction recovery. The changes are first recorded in the log, which must be written to [stable storage](./Stable_storage), before the changes are written to the database.[[2]](./Write-ahead_logging#cite_note-2)

 

## Functionality

 

The main functionality of a write-ahead log can be summarized as:[[3]](./Write-ahead_logging#cite_note-3)

 
- Allow the page cache to buffer updates to disk-resident pages while ensuring durability semantics in the larger context of a database system.
- Persist all operations on disk until the cached copies of pages affected by these operations are synchronized on disk. Every operation that modifies the database state has to be logged on disk before the contents on the associated pages can be modified
- Allow lost in-memory changes to be reconstructed from the operation log in case of a crash.

 

In a system using WAL, all modifications are written to a [log](./Database_log) before they are applied. Usually both redo and undo information is stored in the log.

 

The purpose of this can be illustrated by an example. Imagine a program that is in the middle of performing some operation when the machine it is running on loses power. Upon restart, that program might need to know whether the operation it was performing succeeded, succeeded partially, or failed. If a write-ahead log is used, the program can check this log and compare what it was supposed to be doing when it unexpectedly lost power to what was actually done. On the basis of this comparison, the program could decide to undo what it had started, complete what it had started, or keep things as they are.

 

After a certain number of operations, the program should perform a [checkpoint](./Application_checkpointing), writing all the changes specified in the WAL to the database and clearing the log.

 

WAL allows updates of a database to be done [in-place](./In-place_algorithm). Another way to implement atomic updates is with [shadow paging](./Shadow_paging), which is not in-place. The main advantage of doing updates in-place is that it reduces the need to modify indexes and block lists.

 

Modern [file systems](./File_system) typically use a variant of WAL for at least file system [metadata](./Metadata); this is called [journaling](./Journaling_file_system).

 

## See also

 
- [ARIES](./Algorithms_for_Recovery_and_Isolation_Exploiting_Semantics), a popular algorithm in the WAL family.

 

## References

  
1. [↑](./Write-ahead_logging#cite_ref-Hellerstein_Stonebraker_Hamilton_p._1-0) Hellerstein, Joseph M.; Stonebraker, Michael; Hamilton, James (2007). *Architecture of a database system*. Boston: Now. [ISBN](./ISBN_(identifier)) [978-1-60198-079-3](./Special:BookSources/978-1-60198-079-3). [OCLC](./OCLC_(identifier)) [191079239](https://search.worldcat.org/oclc/191079239).
2. [↑](./Write-ahead_logging#cite_ref-2) ["30.3. Write-Ahead Logging (WAL)"](https://www.postgresql.org/docs/15/wal-intro.html). *PostgreSQL Documentation*. 2023-05-11. [Archived](https://web.archive.org/web/20250408194005/https://www.postgresql.org/docs/15/wal-intro.html) from the original on 2025-04-08. Retrieved 2023-06-05.
3. [↑](./Write-ahead_logging#cite_ref-3) Petrov, Alex (2019). [*Database Internals: A Deep Dive into How Distributed Data Systems Work*](http://worldcat.org/oclc/1103591515). O'Reilly Media. [ISBN](./ISBN_(identifier)) [978-1492040347](./Special:BookSources/978-1492040347). [OCLC](./OCLC_(identifier)) [1103591515](https://search.worldcat.org/oclc/1103591515). [Archived](https://web.archive.org/web/20250408215629/https://search.worldcat.org/title/1103591515) from the original on 2025-04-08.

  
|  | Thisdatabase-related article is astub. You can help Wikipedia byadding missing information. |
| --- | --- |

- [v](./Template:Database-stub)
- [t](./Template_talk:Database-stub)
- [e](./Special:EditPage/Template:Database-stub)