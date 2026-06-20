---
source: https://en.wikipedia.org/wiki/Atomicity_(database_systems)
fetched: 2026-06-19
---

Property of the ACID database system 
|  | This articleneeds additional citations forverification.Please helpimprove this articlebyadding citations to reliable sources. Unsourced material may be challenged and removed.Find sources:"Atomicity"database systems–news·newspapers·books·scholar·JSTOR(April 2020)(Learn how and when to remove this message) |
| --- | --- |

 

In [database systems](./Database_system), **atomicity** ([/ˌætəˈmɪsəti/](./Help:IPA/English); from [Ancient Greek](./Ancient_Greek_language): ἄτομος, [romanized](./Romanization_of_Ancient_Greek): *átomos*, [lit.](./Literal_translation) 'undividable') is the property of a [database transaction](./Database_transaction) consisting of an *indivisible* and *[irreducible](./Irreducibility)* series of database operations such that either *all* occur, or *none* occur.[[1]](./Atomicity_(database_systems)#cite_note-1) It is one of the [ACID](./ACID) transaction properties: Atomicity, [Consistency](./Consistency_(database_systems)), [Isolation](./Isolation_(database_systems)), [Durability](./Durability_(database_systems)). 
A guarantee of atomicity prevents partial database updates from occurring, because they can cause greater problems than rejecting the whole series outright. As a consequence, an **atomic transaction** cannot be observed to be in progress by another database client: at one moment in time, it has not yet happened, and at the next it has already occurred in whole (or nothing happened if the transaction was cancelled in progress).

 

An example of transaction atomicity could be a digital monetary transfer from bank account A to account B. It consists of two operations, debiting the money from account A and crediting it to account B. Performing both of these operations inside of an atomic transaction ensures that the database remains in a [consistent state](./Data_consistency), if either operation fails there will not be any unaccountable credits or debits affecting either account.[[2]](./Atomicity_(database_systems)#cite_note-2)

 

The same term is also used in the definition of [First normal form](./First_normal_form) in database systems, where it instead refers to the concept that the values for fields may not consist of multiple smaller values to be decomposed, such as a string into which multiple names, numbers, dates, or other types may be packed.

 

## Orthogonality

 

Atomicity does not behave completely [orthogonally](./Orthogonal_(computing)) with regard to the other [ACID](./ACID) properties of transactions. For example, [isolation](./Isolation_(database_systems)) relies on atomicity to roll back the enclosing transaction in the event of an isolation violation such as a [deadlock](./Deadlock_(computer_science)); [consistency](./Consistency_(database_systems)) also relies on atomicity to roll back the enclosing transaction in the event of a consistency violation by an illegal transaction.

 

As a result of this, a failure to detect a violation and roll back the enclosing transaction may cause an isolation or consistency failure.

 

## Implementation

 

Typically, systems implement Atomicity by providing some mechanism to indicate which transactions have started and which finished; or by keeping a copy of the data before any changes occurred ([Read-copy-update](./Read-copy-update)). Several filesystems have developed methods for avoiding the need to keep multiple copies of data, using journaling (see [journaling file system](./Journaling_file_system)). Databases usually implement this using some form of logging/journaling to track changes. The system synchronizes the logs (often the [metadata](./Metadata)) as necessary after changes have successfully taken place. Afterwards, crash recovery ignores incomplete entries. Although implementations vary depending on factors such as concurrency issues, the principle of atomicity – i.e. complete success or complete failure – remain.

 

Ultimately, any application-level implementation relies on [operating-system](./Operating_system) functionality. At the file-system level, [POSIX](./POSIX)-compliant systems provide [system calls](./System_call) such as `open(2)` and `flock(2)` that allow applications to atomically open or lock a file. At the process level, [POSIX Threads](./POSIX_Threads) provide adequate synchronization primitives.

 

The hardware level requires [atomic operations](./Linearizability) such as [Test-and-set](./Test-and-set), [Fetch-and-add](./Fetch-and-add), [Compare-and-swap](./Compare-and-swap), or [Load-Link/Store-Conditional](./Load-Link/Store-Conditional), together with [memory barriers](./Memory_barrier). Portable operating systems cannot simply block interrupts to implement synchronization, since hardware that lacks concurrent execution such as [hyper-threading](./Hyper-threading) or [multi-processing](./Multi-processing) is now extremely rare.[*[citation needed](./Wikipedia:Citation_needed)*]

 

In distributed and sharded databases, atomicity is complicated by network latency and the potential for partial failures. While traditional distributed systems often employ [locking protocols](./Two-phase_commit_protocol) (like [2PC](./Two-phase_commit_protocol)) to ensure cross-shard atomicity, these can introduce performance bottlenecks. Recent research into [distributed ledger](./Distributed_ledger_technology) consensus suggests alternative models, such as "braided synchronization". This technique, utilized in protocols like Cerberus, intertwines the consensus phases of multiple shards to enforce atomic guarantees without a global ordering of all transactions.[[3]](./Atomicity_(database_systems)#cite_note-3)

 

## See also

 
- [Atomic operation](./Atomic_operation)
- [Transaction processing](./Transaction_processing)
- [Long-running transaction](./Long-running_transaction)
- [Read-copy-update](./Read-copy-update)

 

## References

  
1. [↑](./Atomicity_(database_systems)#cite_ref-1) ["Atomic operation"](http://www.webopedia.com/TERM/A/atomic_operation.html). Webopedia. 25 November 2003. Retrieved 2011-03-23. An operation during which a processor can simultaneously read a location and write it in the same bus operation. This prevents any other processor or I/O device from writing or reading memory until the operation is complete.
2. [↑](./Atomicity_(database_systems)#cite_ref-2) Amsterdam, Jonathan. ["Atomic File Transactions, Part 1"](https://web.archive.org/web/20160303090517/http://archive.oreilly.com/pub/a/onjava/2001/11/07/atomic.html). *O'Reilly*. Archived from [the original](http://archive.oreilly.com/pub/a/onjava/2001/11/07/atomic.html) on 2016-03-03. Retrieved 2016-02-28.
3. [↑](./Atomicity_(database_systems)#cite_ref-3) Hellings, Jelle; Sadoghi, Mohammad (2021). ["Cerberus: Minimalistic Multi-shard Byzantine-resilient Transaction Processing"](http://www.vldb.org/pvldb/vol14/p2230-hellings.pdf) (PDF). *Proceedings of the VLDB Endowment*. **14** (11): 2230–2243. [doi](./Doi_(identifier)):[10.14778/3476249.3476274](https://doi.org/10.14778%2F3476249.3476274).