---
source: https://en.wikipedia.org/wiki/ACID
fetched: 2026-06-19
---

Robustness properties for database transactions For other uses, see [Acid (disambiguation)](./Acid_(disambiguation)). 
|  | This articleneeds additional citations forverification.Please helpimprove this articlebyadding citations to reliable sources. Unsourced material may be challenged and removed.Find sources:"ACID"–news·newspapers·books·scholar·JSTOR(May 2018)(Learn how and when to remove this message) |
| --- | --- |

 

In [computer science](./Computer_science), **ACID** ([atomicity](./Atomicity_(database_systems)), [consistency](./Consistency_(database_systems)), [isolation](./Isolation_(database_systems)), [durability](./Durability_(database_systems))) is a set of properties of [database transactions](./Database_transaction) intended to guarantee data validity despite errors, power failures, and other mishaps. For example, a transfer of funds from one bank account to another, involving multiple changes such as debiting one account and crediting another, is a single transaction.

 

In 1983,[[1]](./ACID#cite_note-1) [Andreas Reuter](./Andreas_Reuter) and [Theo Härder](./Theo_Härder) coined the acronym *ACID*, building on earlier work by [Jim Gray](./Jim_Gray_(computer_scientist))[[2]](./ACID#cite_note-2) who named atomicity, consistency, and durability, but not isolation, when characterizing the transaction concept. These four properties are the major guarantees of the transaction paradigm, which has influenced many aspects of development in [database systems](./Database_management_system).

 

According to Gray and Reuter, the [IBM Information Management System](./IBM_Information_Management_System) supported ACID transactions as early as 1973 (although the acronym was created later).[[3]](./ACID#cite_note-3)

 

BASE stands for **b**asically **a**vailable, **s**oft state, and [**e**ventually consistent](./Eventual_consistency): the acronym highlights that [BASE](./BASE_(disambiguation)) is opposite of [ACID](./Acid), like their chemical equivalents. ACID databases prioritize [consistency](./Consistency_(database_systems)) over *availability* — the whole [transaction](./Database_transaction) fails if an error occurs in any step within the transaction; in contrast, BASE databases prioritize *availability* over *consistency*: instead of failing the transaction, users can access inconsistent data *temporarily*: data consistency is achieved, but *not immediately*. A database either leans towards ACID or BASE, but it cannot be both (according to [CAP theorem](./CAP_theorem)). For example, [SQL](./SQL) databases (like [MySQL](./MySQL), [PostgreSQL](./PostgreSQL), [AWS RedShift](./Amazon_Redshift)) are structured over the ACID model, while [NoSQL](./NoSQL) databases (like [DynamoDB](./Amazon_DynamoDB)[[4]](./ACID#cite_note-4) or [MongoDB](./MongoDB)) use the BASE architecture. However, some NoSQL databases might exhibit certain ACID traits.[[5]](./ACID#cite_note-5)

 

## Characteristics

 

The characteristics of these four properties as defined by Reuter and Härder are as follows:

 

### Atomicity

 Main article: [Atomicity (database systems)](./Atomicity_(database_systems)) 

[Transactions](./Database_transaction) are often composed of multiple [statements](./SQL_syntax). Atomicity guarantees that each transaction is treated as a single "unit", which either succeeds completely or fails completely: if any of the statements constituting a transaction fails to complete, the entire transaction fails and the database is left unchanged. An atomic system must guarantee atomicity in each and every situation, including power failures, errors, and crashes.[[6]](./ACID#cite_note-6) A guarantee of atomicity prevents updates to the database from occurring only partially, which can cause greater problems than rejecting the whole series outright. As a consequence, the transaction cannot be observed to be in progress by another database client. At one moment in time, it has not yet happened, and at the next, it has already occurred in whole (or nothing happened if the transaction was cancelled in progress).

 

### Consistency

 Main article: [Consistency (database systems)](./Consistency_(database_systems)) 

Consistency ensures that a transaction can only bring the database from one consistent state to another, preserving database [invariants](./Invariant_(computer_science)): any data written to the database must be valid according to all defined rules, including [constraints](./Integrity_constraints), [cascades](./Cascading_rollback), [triggers](./Database_trigger), and any combination thereof. This prevents database corruption by an illegal transaction. An example of a database invariant is [referential integrity](./Referential_integrity), which guarantees the [primary key](./Unique_key)–[foreign key](./Foreign_key) relationship.[[7]](./ACID#cite_note-Date2012-7)

 

### Isolation

 Main article: [Isolation (database systems)](./Isolation_(database_systems)) 

Transactions are often executed [concurrently](./Concurrent_computing) (e.g., multiple transactions reading and writing to a table at the same time). Isolation ensures that concurrent execution of transactions leaves the database in the same state that would have been obtained if the transactions were executed sequentially. Isolation is the main goal of [concurrency control](./Concurrency_control); depending on the isolation level used, the effects of an incomplete transaction might not be visible to other transactions.[[8]](./ACID#cite_note-8)

 

### Durability

 Main article: [Durability (database systems)](./Durability_(database_systems)) 

Durability guarantees that once a transaction has been committed, it will remain committed even in the case of a system failure (e.g., power outage or [crash](./Crash_(computing))). This usually means that completed transactions (or their effects) are recorded in [non-volatile memory](./Non-volatile_memory).[[9]](./ACID#cite_note-9)

 

## Examples

 
|  | This sectiondoes notciteanysources.Please helpimprove this sectionbyadding citations to reliable sources. Unsourced material may be challenged andremoved.(May 2018)(Learn how and when to remove this message) |
| --- | --- |

The following examples further illustrate the ACID properties. In these examples, the database table has two columns, A and B. An [integrity constraint](./Integrity_constraints) requires that the value in A and the value in B must sum to 100. The following [SQL](./SQL) code creates a table as described above:

```
CREATE TABLE acidtest (A INTEGER, B INTEGER, CHECK (A + B = 100));

```
 

### Atomicity

 

Atomicity is the guarantee that series of database operations in an atomic transaction will either all occur (a successful operation), or none will occur (an unsuccessful operation). The series of operations cannot be separated with only some of them being executed, which makes the series of operations "indivisible". A guarantee of atomicity prevents updates to the database from occurring only partially, which can cause greater problems than rejecting the whole series outright. In other words, atomicity means indivisibility and irreducibility.[[10]](./ACID#cite_note-10) Alternatively, we may say that a logical transaction may be composed of several physical transactions. Unless and until all component physical transactions are executed, the logical transaction will not have occurred. 

 

An example of an atomic transaction is a monetary transfer from bank account A to account B. It consists of two operations, withdrawing the money from account A and depositing it to account B. We would not want to see the amount removed from account A before we are sure it has also been transferred into account B. Performing these operations in an atomic transaction ensures that the database remains in a [consistent state](./Data_consistency), that is, money is neither debited nor credited if either of those two operations fails.[[11]](./ACID#cite_note-11)

 

### Consistency failure

 

Consistency is a very general term, which demands that the data must meet all validation rules. In the previous example, the validation is a requirement that A + B = 100. All validation rules must be checked to ensure consistency. Assume that a transaction attempts to subtract 10 from A without altering B. Because consistency is checked after each transaction, it is known that A + B = 100 before the transaction begins. If the transaction removes 10 from A successfully, atomicity will be achieved. However, a validation check will show that A + B = 90, which is inconsistent with the rules of the database. The entire transaction must be canceled and the affected rows rolled back to their pre-transaction state. If there had been other constraints, triggers, or cascades, every single change operation would have been checked in the same way as above before the transaction was committed. Similar issues may arise with other constraints. We may have required the data types of both A and B to be integers. If we were then to enter, say, the value 13.5 for A, the transaction will be canceled, or the system may give rise to an alert in the form of a trigger (if/when the trigger has been written to this effect). Another example would be integrity constraints, which would not allow us to delete a row in one table whose primary key is referred to by at least one [foreign key](./Foreign_key) in other tables.

 

### Isolation failure

 

To demonstrate isolation, we assume two transactions execute at the same time, each attempting to modify the same data. One of the two must wait until the other completes in order to maintain isolation.

 

Consider two transactions:

 
- T1 transfers 10 from A to B.
- T2 transfers 20 from B to A.

 

Combined, there are four actions:

 
1. T1 subtracts 10 from A.
2. T1 adds 10 to B.
3. T2 subtracts 20 from B.
4. T2 adds 20 to A.

 

If these operations are performed in order, isolation is maintained, although T2 must wait. Consider what happens if T1 fails halfway through. The database eliminates T1's effects, and T2 sees only valid data.

 

By interleaving the transactions, the actual order of actions might be:

 
1. T1 subtracts 10 from A.
2. T2 subtracts 20 from B.
3. T2 adds 20 to A.
4. T1 adds 10 to B.

 

Again, consider what happens if T1 fails while modifying B in Step 4. By the time T1 fails, T2 has already modified A; it cannot be restored to the value it had before T1 without leaving an invalid database. This is known as a [write-write contention](./Write–write_conflict),[[12]](./ACID#cite_note-12) because two transactions attempted to write to the same data field. In a typical system, the problem would be resolved by reverting to the last known good state, canceling the failed transaction T1, and restarting the interrupted transaction T2 from the good state.

 

### Durability failure

 

Consider a transaction that transfers 10 from A to B. First, it removes 10 from A, then it adds 10 to B. At this point, the user is told the transaction was a success. However, the changes are still queued in the [disk buffer](./Disk_buffer) waiting to be committed to disk. Power fails and the changes are lost, but the user assumes (understandably) that the changes persist.

 

## Implementation

 

Processing a transaction often requires a sequence of operations that is subject to failure for a number of reasons. For instance, the system may have no room left on its disk drives, or it may have used up its allocated CPU time. There are two popular families of techniques: [write-ahead logging](./Write-ahead_logging) and [shadow paging](./Shadow_paging). In both cases, [locks](./Lock_(computer_science)) must be acquired on all information to be updated, and depending on the level of isolation, possibly on all data that may be read as well. In write ahead logging, durability is guaranteed by writing the prospective change to a persistent log before changing the database. That allows the database to return to a consistent state in the event of a crash. In shadowing, updates are applied to a partial copy of the database, and the new copy is activated when the transaction commits.

 

### Locking vs. multiversioning

 

Many databases rely upon locking to provide ACID capabilities. Locking means that the transaction marks the data that it accesses so that the DBMS knows not to allow other transactions to modify it until the first transaction succeeds or fails. The lock must always be acquired before processing data, including data that is read but not modified. Non-trivial transactions typically require a large number of locks, resulting in substantial overhead as well as blocking other transactions. For example, if user A is running a transaction that has to read a row of data that user B wants to modify, user B must wait until user A's transaction completes. [Two-phase locking](./Two-phase_locking) is often applied to guarantee full isolation.

 

An alternative to locking is [multiversion concurrency control](./Multiversion_concurrency_control), in which the database provides each reading transaction the prior, unmodified version of data that is being modified by another active transaction. This allows readers to operate without acquiring locks, i.e., writing transactions do not block reading transactions, and readers do not block writers. Going back to the example, when user A's transaction requests data that user B is modifying, the database provides A with the version of that data that existed when user B started his transaction. User A gets a consistent view of the database even if other users are changing data. One implementation, namely [snapshot isolation](./Snapshot_isolation), relaxes the isolation property.

 

### Distributed transactions

 Main article: [Distributed transaction](./Distributed_transaction) 

Guaranteeing ACID properties in a [distributed transaction](./Distributed_transaction) across a [distributed database](./Distributed_database), where no single node is responsible for all data affecting a transaction, presents additional complications. Network connections might fail, or one node might successfully complete its part of the transaction and then be required to roll back its changes because of a failure on another node. The [two-phase commit protocol](./Two-phase_commit_protocol) (not to be confused with [two-phase locking](./Two-phase_locking)) provides atomicity for [distributed transactions](./Distributed_transaction) to ensure that each participant in the transaction agrees on whether the transaction should be committed or not.[[13]](./ACID#cite_note-Bern2009-13) Briefly, in the first phase, one node (the coordinator) interrogates the other nodes (the participants), and only when all reply that they are prepared does the coordinator, in the second phase, formalize the transaction.

 

## See also

 
- [Eventual consistency](./Eventual_consistency) (BASE: basically available)
- [CAP theorem](./CAP_theorem)
- [Concurrency control](./Concurrency_control)
- [Java Transaction API](./Java_Transaction_API)
- [Open Systems Interconnection](./Open_Systems_Interconnection)
- [Transactional NTFS](./Transactional_NTFS)
- [Two-phase commit protocol](./Two-phase_commit_protocol)
- [CRUD](./Create,_read,_update_and_delete)

 

## References

  
1. [↑](./ACID#cite_ref-1) [Haerder, T.](./Theo_Härder); [Reuter, A.](./Andreas_Reuter) (1983). "Principles of transaction-oriented database recovery". *ACM Computing Surveys*. **15** (4): 287. [doi](./Doi_(identifier)):[10.1145/289.291](https://doi.org/10.1145%2F289.291). [S2CID](./S2CID_(identifier)) [207235758](https://api.semanticscholar.org/CorpusID:207235758).
2. [↑](./ACID#cite_ref-2) [Gray, Jim](./Jim_Gray_(computer_scientist)) (September 1981). ["The Transaction Concept: Virtues and Limitations"](http://research.microsoft.com/~gray/papers/theTransactionConcept.pdf) (PDF). *Proceedings of the 7th International Conference on Very Large Databases*. Cupertino, California: [Tandem Computers](./Tandem_Computers). pp. 144–154. Retrieved March 27, 2015.
3. [↑](./ACID#cite_ref-3) [Gray, Jim](./Jim_Gray_(computer_scientist)); [Reuter, Andreas](./Andreas_Reuter) (1993). [*Distributed Transaction Processing: Concepts and Techniques*](https://archive.org/details/transactionproce0000gray). [Morgan Kaufmann](./Morgan_Kaufmann). [ISBN](./ISBN_(identifier)) [1-55860-190-2](./Special:BookSources/1-55860-190-2).
4. [↑](./ACID#cite_ref-4) ["DynamoDB read consistency - Amazon DynamoDB"](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/HowItWorks.ReadConsistency.html). *docs.aws.amazon.com*. Retrieved 2025-11-29. Read operations such as GetItem, Query, and Scan provide an optional ConsistentRead parameter. If you set ConsistentRead to true, DynamoDB returns a response with the most up-to-date data, reflecting the updates from all prior write operations that were successful
5. [↑](./ACID#cite_ref-5) ["ACID vs BASE Databases - Difference Between Databases - AWS"](https://aws.amazon.com/compare/the-difference-between-acid-and-base-database/). *Amazon Web Services, Inc*. Retrieved 2025-03-24.
6. [↑](./ACID#cite_ref-6) ["Atomic operation"](http://www.webopedia.com/TERM/A/atomic_operation.html). *webopedia.com*. Webopedia. 25 November 2003. Retrieved 2011-03-23. An operation during which a processor can simultaneously read a location and write it in the same bus operation. This prevents any other processor or I/O device from writing or reading memory until the operation is complete.
7. [↑](./ACID#cite_ref-Date2012_7-0) C. J. Date, "SQL and Relational Theory: How to Write Accurate SQL Code 2nd edition", *O'reilly Media, Inc.*, 2012, p. 180.
8. [↑](./ACID#cite_ref-8) Archiveddocs (2012-10-04). ["Isolation Levels in the Database Engine"](https://learn.microsoft.com/en-us/previous-versions/sql/sql-server-2008-r2/ms189122(v=sql.105)). *learn.microsoft.com*. Retrieved 2023-07-14.
9. [↑](./ACID#cite_ref-9) Silberschatz, Abraham; Korth, Henry F.; Sudarshan, S. (2011). "Transactions". [*Database system concepts*](https://www.worldcat.org/title/436031093) (6th ed.). New York: McGraw-Hill. p. 631. [ISBN](./ISBN_(identifier)) [978-0-07-352332-3](./Special:BookSources/978-0-07-352332-3). [OCLC](./OCLC_(identifier)) [436031093](https://search.worldcat.org/oclc/436031093).
10. [↑](./ACID#cite_ref-10) ["Atomicity"](https://docs.oracle.com/cd/E17276_01/html/programmer_reference/transapp_atomicity.html). *docs.oracle.com*. Retrieved 2016-12-13.
11. [↑](./ACID#cite_ref-11) Amsterdam, Jonathan. ["Atomic File Transactions, Part 1"](https://web.archive.org/web/20160303090517/http://archive.oreilly.com/pub/a/onjava/2001/11/07/atomic.html). *O'Reilly*. Archived from [the original](http://archive.oreilly.com/pub/a/onjava/2001/11/07/atomic.html) on 2016-03-03. Retrieved 2016-02-28.
12. [↑](./ACID#cite_ref-12) Silberschatz, Abraham; Korth, Henry F.; Sudarshan, S. (2011). "Advanced Application Development". [*Database system concepts*](https://www.worldcat.org/title/436031093) (6th ed.). New York: McGraw-Hill. p. 1042. [ISBN](./ISBN_(identifier)) [978-0-07-352332-3](./Special:BookSources/978-0-07-352332-3). [OCLC](./OCLC_(identifier)) [436031093](https://search.worldcat.org/oclc/436031093).
13. [↑](./ACID#cite_ref-Bern2009_13-0) [Bernstein, Philip A.](./Phil_Bernstein); Newcomer, Eric (2009). "Chapter 8". [*Principles of Transaction Processing*](https://web.archive.org/web/20100807151625/http://www.elsevierdirect.com/product.jsp?isbn=9781558606234) (2nd ed.). Morgan Kaufmann (Elsevier). [ISBN](./ISBN_(identifier)) [978-1-55860-623-4](./Special:BookSources/978-1-55860-623-4). Archived from [the original](http://www.elsevierdirect.com/product.jsp?isbn=9781558606234) on 2010-08-07.

  
| vteDatabase management systems |
| --- |
| Types | Object-orientedcomparisonRelationallistcomparisonKey–valueColumn-orientedlistDocument-orientedWide-column storeGraphNoSQLNewSQLIn-memorylistMulti-modelcomparisonCloudBlockchain-based database |
| Concepts | DatabaseACIDArmstrong's axiomsCodd's 12 rulesCAP theoremCRUDNullCandidate keyForeign keyPACELC design principleSuperkeySurrogate keyUnique key |
| Objects | RelationtablecolumnrowViewTransactionTransaction logTriggerIndexStored procedureCursorPartition |
| Components | Concurrency controlData dictionaryJDBCXQJODBCQuery languageQuery optimizerQuery rewriting systemQuery plan |
| Functions | AdministrationQuery optimizationReplicationSharding |
| Related topics | Database modelsDatabase normalizationDatabase storageDistributed databaseFederated database systemReferential integrityRelational algebraRelational calculusRelational modelObject–relational databaseTransaction processingList of SQL software and tools |
| CategoryOutline |