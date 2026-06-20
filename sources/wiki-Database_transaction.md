---
source: https://en.wikipedia.org/wiki/Database_transaction
fetched: 2026-06-19
---

Unit of work performed within a database management system 
|  | This articleneeds additional citations forverification.Please helpimprove this articlebyadding citations to reliable sources. Unsourced material may be challenged and removed.Find sources:"Database transaction"–news·newspapers·books·scholar·JSTOR(August 2010)(Learn how and when to remove this message) |
| --- | --- |

 

A **database transaction** symbolizes a [unit of work](./Unit_of_work), performed within a [database management system](./Database_management_system) (or similar system) against a [database](./Database), that is treated in a coherent and reliable way independent of other transactions[[1]](./Database_transaction#cite_note-1). A transaction generally represents any change in a database. Transactions in a database environment have two main purposes:

 
1. To provide reliable units of work that allow correct recovery from failures and keep a database consistent even in cases of system failure. For example: when execution prematurely and unexpectedly stops (completely or partially) in which case many operations upon a database remain uncompleted, with unclear status.
2. To provide isolation between programs accessing a database concurrently. If this isolation is not provided, the programs' outcomes are possibly erroneous.

 

In a database management system, a transaction is a single unit of logic or work, sometimes made up of multiple operations. Any logical calculation done in a consistent mode in a database is known as a transaction. One example is a transfer from one bank account to another: the complete transaction requires subtracting the amount to be transferred from one account and adding that same amount to the other.

 

A database transaction, by definition, must be [atomic](./Atomicity_(database_systems)) (it must either be complete in its entirety or have no effect whatsoever), [consistent](./Consistency_(database_systems)) (it must conform to existing constraints in the database), [isolated](./Isolation_(database_systems)) (it must not affect other transactions) and [durable](./Durability_(database_systems)) (it must get written to persistent storage).[[2]](./Database_transaction#cite_note-2) Database practitioners often refer to these properties of database transactions using the acronym [ACID](./ACID).

 

## Purpose

 

[Databases](./Database) and other data stores which treat the [integrity](./Data_integrity) of data as paramount often include the ability to handle transactions to maintain the integrity of data. A single transaction consists of one or more independent units of work, each reading and/or writing information to a database or other data store. When this happens it is often important to ensure that all such processing leaves the database or data store in a consistent state.

 

Examples from [double-entry accounting systems](./Double-entry_bookkeeping_system) often illustrate the concept of transactions. In double-entry accounting every debit requires the recording of an associated credit. If one writes a check for $100 to buy groceries, a transactional double-entry accounting system must record the following two entries to cover the single transaction:

 
1. Debit $100 to Groceries Expense Account
2. Credit $100 to Checking Account

 

A transactional system would make both entries pass or both entries would fail. By treating the recording of multiple entries as an atomic transactional unit of work the system maintains the integrity of the data recorded. In other words, nobody ends up with a situation in which a debit is recorded but no associated credit is recorded, or vice versa.

 

## Transactional databases

 

A **transactional database** is a [DBMS](./DBMS) that provides the [ACID properties](./ACID_properties) for a bracketed set of database operations (begin-commit). Transactions ensure that the database is always in a consistent state, even in the event of concurrent updates and failures.[[3]](./Database_transaction#cite_note-3) All the write operations within a transaction have an all-or-nothing effect, that is, either the transaction succeeds and all writes take effect, or otherwise, the database is brought to a state that does not include any of the writes of the transaction. Transactions also ensure that the effect of concurrent transactions satisfies certain guarantees, known as [isolation level](./Isolation_level). The highest isolation level is [serializability](./Serializability), which guarantees that the effect of concurrent transactions is equivalent to their serial (i.e. sequential) execution.

 

Most modern[[update]](https://en.wikipedia.org/w/index.php?title=Database_transaction&action=edit) [relational database management systems](./Relational_database_management_system) support transactions. [NoSQL](./NoSQL) databases prioritize scalability along with supporting transactions in order to guarantee data consistency in the event of concurrent updates and accesses.

 

In a database system, a transaction might consist of one or more data-manipulation statements and queries, each reading and/or writing information in the database. Users of [database systems](./Database_system) consider [consistency](./Data_consistency) and [integrity](./Data_integrity) of data as highly important. A simple transaction is usually issued to the database system in a language like [SQL](./SQL) wrapped in a transaction, using a pattern similar to the following:

 
1. Begin the transaction.
2. Execute a set of data manipulations and/or queries.
3. If no error occurs, then commit the transaction.
4. If an error occurs, then roll back the transaction.

 

A transaction commit operation persists all the results of data manipulations within the scope of the transaction to the database. A transaction rollback operation does not persist the partial results of data manipulations within the scope of the transaction to the database. In no case can a partial transaction be committed to the database since that would leave the database in an inconsistent state.

 

Internally, multi-user databases store and process transactions, often by using a transaction [ID](./Identifier) or XID.

 

There are multiple varying ways for transactions to be implemented other than the simple way documented above. [Nested transactions](./Nested_transaction), for example, are transactions which contain statements within them that start new transactions (i.e. sub-transactions). *Multi-level transactions* are a variant of nested transactions where the sub-transactions take place at different levels of a layered system architecture (e.g., with one operation at the database-engine level, one operation at the operating-system level).[[4]](./Database_transaction#cite_note-4) Another type of transaction is the [compensating transaction](./Compensating_transaction).

 

### In SQL

 

Transactions are available in most SQL database implementations, though with varying levels of robustness. For example, [MySQL](./MySQL) began supporting transactions from early version 3.23, but the [InnoDB](./InnoDB) storage engine was not default before version 5.5. The earlier available storage engine, [MyISAM](./MyISAM) does not support transactions.

 

A transaction is typically started using the command `BEGIN` (although the SQL standard specifies `START TRANSACTION`). When the system processes a `COMMIT` statement, the transaction ends with successful completion.  A `ROLLBACK` statement can also end the transaction, undoing any work performed since `BEGIN`. If [autocommit](./Autocommit) was disabled with the start of a transaction, autocommit will also be re-enabled with the end of the transaction.

 

One can set the [isolation level](./Isolation_(database_systems)) for individual transactional operations as well as globally. At the highest level (`READ COMMITTED`), the result of any operation performed after a transaction has started will remain invisible to other database users until the transaction has ended. At the lowest level (`READ UNCOMMITTED`), which may occasionally be used to ensure high concurrency, such changes will be immediately visible.

 

## Object databases

 

Relational databases are traditionally composed of tables with fixed-size fields and records. Object databases comprise variable-sized [blobs](./Binary_large_object), possibly [serializable](./Serialization) or incorporating a [mime-type](./Mime-type). The fundamental similarities between Relational and Object databases are the start and the [commit](./Commit_(data_management)) or [rollback](./Rollback_(data_management)).

 

After starting a transaction, database records or objects are locked, either read-only or read-write. Reads and writes can then occur. Once the transaction is fully defined, changes are committed or rolled back [atomically](./Atomicity_(database_systems)), such that at the end of the transaction there is no [inconsistency](./Consistency_(database_systems)).

 

## Distributed transactions

 

Database systems implement [distributed transactions](./Distributed_transaction)[[5]](./Database_transaction#cite_note-5) as transactions accessing data over multiple nodes. A distributed transaction enforces the ACID properties over multiple nodes, and might include systems such as databases, storage managers, file systems, messaging systems, and other data managers. In a distributed transaction there is typically an entity coordinating all the process to ensure that all parts of the transaction are applied to all relevant systems. Moreover, the integration of Storage as a Service (StaaS) within these environments is crucial, as it offers a virtually infinite pool of storage resources, accommodating a range of cloud-based data store classes with varying availability, scalability, and ACID properties. This integration is essential for achieving higher availability, lower response time, and cost efficiency in data-intensive applications deployed across cloud-based data stores.[[6]](./Database_transaction#cite_note-6)

 

## Transactional filesystems

 

The [Namesys](./Namesys) [Reiser4](./Reiser4) filesystem for [Linux](./Linux)[[7]](./Database_transaction#cite_note-7) supports transactions, and as of [Microsoft](./Microsoft) [Windows Vista](./Windows_Vista), the Microsoft [NTFS](./NTFS) filesystem[[8]](./Database_transaction#cite_note-8) supports [distributed transactions](./Distributed_transaction) across networks. There is occurring research into more data coherent filesystems, such as the [Warp Transactional Filesystem](./Warp_Transactional_Filesystem?action=edit&redlink=1) (WTF).[[9]](./Database_transaction#cite_note-9)

 

## See also

 
- [ACID](./ACID)
- [Concurrency control](./Concurrency_control)
- [Critical section](./Critical_section)
- [Post void](./Post_void)
- [Database transaction schedule](./Database_transaction_schedule)

 

## References

  
1. [↑](./Database_transaction#cite_ref-1) ["ACID vs BASE Databases - Difference Between Databases - AWS"](https://aws.amazon.com/compare/the-difference-between-acid-and-base-database/). *Amazon Web Services, Inc*. Retrieved 2025-11-28. a transaction is any operation that the database considers a single unit of work. A transaction must complete fully for the database to remain consistent. For example, when you transfer money from one bank account to another, the money must leave your account and must be added to the third-party account. You cannot call the transaction complete without both steps occurring
2. [↑](./Database_transaction#cite_ref-2) ["What is a Transaction? (Windows)"](http://msdn.microsoft.com/en-us/library/aa366402(VS.85).aspx). *msdn.microsoft.com*. 7 January 2021.
3. [↑](./Database_transaction#cite_ref-3) DINCĂ, Ana-Maria; AXINTE, Sabina-Daniela; BACIVAROV, Ioan (2022-12-29). ["Performance Enhancements for Database Transactions"](https://dx.doi.org/10.19107/ijisc.2022.02.02). *International Journal of Information Security and Cybercrime*. **11** (2): 29–34. [doi](./Doi_(identifier)):[10.19107/ijisc.2022.02.02](https://doi.org/10.19107%2Fijisc.2022.02.02). [ISSN](./ISSN_(identifier)) [2285-9225](https://search.worldcat.org/issn/2285-9225). [S2CID](./S2CID_(identifier)) [259653728](https://api.semanticscholar.org/CorpusID:259653728).
4. [↑](./Database_transaction#cite_ref-4) Beeri, C.; Bernstein, P. A.; Goodman, N. (1989). ["A model for concurrency in nested transactions systems"](https://doi.org/10.1145%2F62044.62046). *Journal of the ACM*. **36** (1): 230–269. [doi](./Doi_(identifier)):[10.1145/62044.62046](https://doi.org/10.1145%2F62044.62046). [S2CID](./S2CID_(identifier)) [12956480](https://api.semanticscholar.org/CorpusID:12956480).
5. [↑](./Database_transaction#cite_ref-5) Özsu, M. Tamer; Valduriez, Patrick (2011). *Principles of Distributed Database Systems, Third Edition*. Springer. [Bibcode](./Bibcode_(identifier)):[2011podd.book.....O](https://ui.adsabs.harvard.edu/abs/2011podd.book.....O). [doi](./Doi_(identifier)):[10.1007/978-1-4419-8834-8](https://doi.org/10.1007%2F978-1-4419-8834-8). [ISBN](./ISBN_(identifier)) [978-1-4419-8833-1](./Special:BookSources/978-1-4419-8833-1).
6. [↑](./Database_transaction#cite_ref-6) Mansouri, Yaser; Toosi, Adel Nadjaran; Buyya, Rajkumar (2017-12-11). ["Data Storage Management in Cloud Environments: Taxonomy, Survey, and Future Directions"](https://doi.org/10.1145/3136623). *ACM Computing Surveys*. **50** (6): 91:1–91:51. [doi](./Doi_(identifier)):[10.1145/3136623](https://doi.org/10.1145%2F3136623). [ISSN](./ISSN_(identifier)) [0360-0300](https://search.worldcat.org/issn/0360-0300).
7. [↑](./Database_transaction#cite_ref-7) ["Linux.org"](https://www.linux.org/). *Linux.org*.
8. [↑](./Database_transaction#cite_ref-8) ["MSDN Library"](https://msdn.microsoft.com/en-us/library/ff361664(v=vs.110).aspx). 4 February 2013. Retrieved 16 October 2014.
9. [↑](./Database_transaction#cite_ref-9) ["The Design and Implementation of the Warp Transactional Filesystem"](https://www.usenix.org/system/files/conference/nsdi16/nsdi16-paper-escriva.pdf) (PDF). *usenix.org*. March 18, 2016. Retrieved 16 Oct 2025.

 

## Further reading

 
- [Philip A. Bernstein](./Philip_A._Bernstein), Eric Newcomer (2009): [*Principles of Transaction Processing*, 2nd Edition](https://web.archive.org/web/20100807151625/http://www.elsevierdirect.com/product.jsp?isbn=9781558606234),  Morgan Kaufmann (Elsevier), [ISBN](./ISBN_(identifier)) [978-1-55860-623-4](./Special:BookSources/978-1-55860-623-4) 
- Gerhard Weikum, Gottfried Vossen (2001), *Transactional information systems: theory, algorithms, and the practice of concurrency control and recovery*, Morgan Kaufmann, [ISBN](./ISBN_(identifier)) [1-55860-508-8](./Special:BookSources/1-55860-508-8)

 

## External links

 
- [c2:TransactionProcessing](https://wiki.c2.com/?TransactionProcessing)
- [https://docs.oracle.com/database/121/CNCPT/transact.htm#CNCPT016](https://docs.oracle.com/database/121/CNCPT/transact.htm#CNCPT016)
- [https://docs.oracle.com/cd/B28359_01/server.111/b28318/transact.htm](https://docs.oracle.com/cd/B28359_01/server.111/b28318/transact.htm)

 
| vteDatabase management systems |
| --- |
| Types | Object-orientedcomparisonRelationallistcomparisonKey–valueColumn-orientedlistDocument-orientedWide-column storeGraphNoSQLNewSQLIn-memorylistMulti-modelcomparisonCloudBlockchain-based database |
| Concepts | DatabaseACIDArmstrong's axiomsCodd's 12 rulesCAP theoremCRUDNullCandidate keyForeign keyPACELC design principleSuperkeySurrogate keyUnique key |
| Objects | RelationtablecolumnrowViewTransactionTransaction logTriggerIndexStored procedureCursorPartition |
| Components | Concurrency controlData dictionaryJDBCXQJODBCQuery languageQuery optimizerQuery rewriting systemQuery plan |
| Functions | AdministrationQuery optimizationReplicationSharding |
| Related topics | Database modelsDatabase normalizationDatabase storageDistributed databaseFederated database systemReferential integrityRelational algebraRelational calculusRelational modelObject–relational databaseTransaction processingList of SQL software and tools |
| CategoryOutline |