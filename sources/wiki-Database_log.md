---
source: https://en.wikipedia.org/wiki/Database_log
fetched: 2026-06-19
---

History of actions executed by a database management system "Binary log" redirects here. For the logarithm to base 2, see [Binary logarithm](./Binary_logarithm). "Journal (computing)" redirects here. For other uses, see [Journal (disambiguation)](./Journal_(disambiguation)). 
|  | This articleis inlistformat but may read better asprose.You can help byconverting this article, if appropriate.Editing helpis available.(June 2015) |
| --- | --- |

 

In the field of [databases](./Database) in [computer science](./Computer_science), a **transaction log** (also **transaction journal**, **database log**, **binary log** or **audit trail**) is a history of actions executed by a [database management system](./Database_management_system) used to guarantee [ACID](./ACID) properties over [crashes](./Crash_(computing)) or hardware failures. Physically, a log is a [file](./Computer_file) listing changes to the database, stored in a stable storage format.

 

If, after a start, the database is found in an [inconsistent](./Consistency_(database_systems)) state or not been shut down properly, the database management system reviews the database logs for [uncommitted](./Commit_(data_management)) transactions and [rolls back](./Rollback_(data_management)) the changes made by these [transactions](./Database_transaction). Additionally, all transactions that are already committed but whose changes were not yet materialized in the database are re-applied. Both are done to ensure [atomicity](./Atomicity_(database_systems)) and [durability](./Durability_(computer_science)) of transactions.

 

This term is not to be confused with other, human-readable [logs](./Log_file) that a database management system usually provides.

  WP:PROVEIT In [[computer storage]], a '''journal''' is a [[Chronology|chronological]] record of [[data processing]] operations that may be used to construct or reinstate an historical or alternative version of a [[computer system]] or [[computer file]].  

In [database management systems](./Database_management_system), a journal is the record of data altered by a given process.[[1]](./Transaction_log#cite_note-1)[[2]](./Transaction_log#cite_note-2)[[3]](./Transaction_log#cite_note-3)[[4]](./Transaction_log#cite_note-4)

 

## Anatomy of a general database log

 

A database log record is made up of: 

 (FIXME: resource managers, xid not universal)   
- *Log Sequence Number* (LSN): A unique ID for a log record. With LSNs, logs can be recovered in constant time. Most LSNs are assigned in monotonically increasing order, which is useful in recovery [algorithms](./Algorithm), like [ARIES](./Algorithms_for_Recovery_and_Isolation_Exploiting_Semantics).
- *Prev LSN*: A link to their last log record. This implies database logs are constructed in [linked list](./Linked_list) form.
- *Transaction ID number*: A reference to the database transaction generating the log record.
- *Type*: Describes the type of database log record.
- Information about the actual changes that triggered the log record to be written.

 

## Types of database log records

 
|  | This sectionneeds additional citations forverification.Please helpimprove this articlebyadding citations to reliable sourcesin this section. Unsourced material may be challenged and removed.(July 2016)(Learn how and when to remove this message) |
| --- | --- |

 

All log records include the general log attributes above, and also other attributes depending on their type (which is recorded in the *Type* attribute, as above).

 
- **Update Log Record** notes an update (change) to the database. It includes this extra information:

- *PageID*: A reference to the Page ID of the modified page.
- *Length and Offset*: Length in bytes and offset of the page are usually included.
- *Before and After Images*: Includes the value of the bytes of page before and after the page change. Some databases may have logs which include one or both images.

- **Compensation Log Record** (CLR) notes the rollback of a particular change to the database. Each corresponds with exactly one other Update Log Record (although the corresponding update log record is not typically stored in the Compensation Log Record). It includes this extra information:

- *undoNextLSN*: This field contains the LSN of the next log record that is to be undone for transaction that wrote the last Update Log.

- **Commit Record** notes a decision to commit a transaction.
- **Abort Record** notes a decision to abort and hence roll back a transaction.
- **Checkpoint Record** notes that a checkpoint has been made. These are used to speed up recovery. They record information that eliminates the need to read a long way into the log's past. This varies according to checkpoint algorithm. If all dirty pages are flushed while creating the checkpoint (as in [PostgreSQL](./PostgreSQL)), it might contain:

- *redoLSN*: This is a reference to the first log record that corresponds to a dirty page. i.e. the first update that wasn't flushed at checkpoint time. This is where redo must begin on recovery.
- *undoLSN*: This is a reference to the oldest log record of the oldest in-progress transaction. This is the oldest log record needed to undo all in-progress transactions.

- **Completion Record** notes that all work has been done for this particular transaction. (It has been fully committed or aborted)

 

## See also

 
- [Data logging](./Data_logging)
- [Error correction and detection](./Error_correction_and_detection)
- [Hash function](./Hash_function)
- [Journaling file system](./Journaling_file_system)
- [Log-structured file system](./Log-structured_file_system)
- [Write-ahead logging](./Write-ahead_logging)
- [Redo log](./Redo_log)

 

## Sources

 
- [Federal Standard 1037C](./Federal_Standard_1037C)

 

## References

  
1. [↑](./Transaction_log#cite_ref-1) [Microsoft, The Transaction Log (SQL Server)](https://msdn.microsoft.com/en-us/library/ms190925.aspx)
2. [↑](./Transaction_log#cite_ref-2) [sqlshack.com, A beginner’s guide to SQL Server transaction logs, February 11, 2014 by Ivan Stankovic](http://www.sqlshack.com/beginners-guide-sql-server-transaction-logs/)
3. [↑](./Transaction_log#cite_ref-3) [techrepublic.com, Understanding the importance of transaction logs in SQL Server, SQL Server transaction log maintenance, By Crowe, Chizek, November 11, 2004](https://www.techrepublic.com/article/understanding-the-importance-of-transaction-logs-in-sql-server/)
4. [↑](./Transaction_log#cite_ref-4) [neurobs.com, Logfiles](https://www.neurobs.com/pres_docs/html/03_presentation/07_data_reporting/01_logfiles/index.html)

 
| vteDatabase management systems |
| --- |
| Types | Object-orientedcomparisonRelationallistcomparisonKey–valueColumn-orientedlistDocument-orientedWide-column storeGraphNoSQLNewSQLIn-memorylistMulti-modelcomparisonCloudBlockchain-based database |
| Concepts | DatabaseACIDArmstrong's axiomsCodd's 12 rulesCAP theoremCRUDNullCandidate keyForeign keyPACELC design principleSuperkeySurrogate keyUnique key |
| Objects | RelationtablecolumnrowViewTransactionTransaction logTriggerIndexStored procedureCursorPartition |
| Components | Concurrency controlData dictionaryJDBCXQJODBCQuery languageQuery optimizerQuery rewriting systemQuery plan |
| Functions | AdministrationQuery optimizationReplicationSharding |
| Related topics | Database modelsDatabase normalizationDatabase storageDistributed databaseFederated database systemReferential integrityRelational algebraRelational calculusRelational modelObject–relational databaseTransaction processingList of SQL software and tools |
| CategoryOutline |