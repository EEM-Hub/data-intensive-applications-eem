---
source: https://en.wikipedia.org/wiki/Isolation_(database_systems)
fetched: 2026-06-19
---

Database transaction integrity concept 
|  | This articleneeds additional citations forverification.Please helpimprove this articlebyadding citations to reliable sources. Unsourced material may be challenged and removed.Find sources:"Isolation"database systems–news·newspapers·books·scholar·JSTOR(January 2009)(Learn how and when to remove this message) |
| --- | --- |

 

In [database](./Database) systems, **isolation** is one of the [ACID](./ACID) (*[Atomicity](./Atomicity_(database_systems)), [Consistency](./Consistency_(database_systems)), Isolation, [Durability](./Durability_(database_systems))*) [transaction](./Database_transaction) properties. It determines how [transaction](./Database_transaction) integrity is visible to other users and systems. A lower isolation level increases the ability of many users to access the same data at the same time, but also increases the number of [concurrency](./Concurrency_(computer_science)) effects (such as [ dirty reads](./Write–read_conflict) or [lost updates](./Lost_update)) users might encounter. Conversely, a higher isolation level reduces the types of concurrency effects that users may encounter, but requires more system resources and increases the chances that one transaction will block another.[[1]](./Isolation_(database_systems)#cite_note-1)

 

## DBMS concurrency control

 

[Concurrency control](./Concurrency_control) comprises the underlying mechanisms in a [DBMS](./DBMS) which handle isolation and guarantee related correctness. It is heavily used by the database and storage engines both to guarantee the correct execution of concurrent transactions, and (via different mechanisms) the correctness of other DBMS processes. The transaction-related mechanisms typically constrain the database data access operations' timing ([transaction schedules](./Database_transaction_schedule)) to certain orders characterized as the [serializability](./Serializability) and [recoverability](./Recoverability) schedule properties. Constraining database access operation execution typically means reduced performance (measured by rates of execution), and thus concurrency control mechanisms are typically designed to provide the best performance possible under the constraints. Often, when possible without harming correctness, the serializability property is compromised for better performance. However, recoverability cannot be compromised, since such typically results in a [database integrity violation](./Data_integrity).

 

[Two-phase locking](./Two-phase_locking) is the most common transaction concurrency control method in DBMSs, used to provide both serializability and recoverability for correctness. In order to access a database object a transaction first needs to acquire a [lock](./Lock_(database)) for this object. Depending on the access operation type (e.g., reading or writing an object) and on the lock type, acquiring the lock may be blocked and postponed, if another transaction is holding a lock for that object.

 

## Client-side isolation

 

Isolation is typically enforced at the database level. However, various client-side systems can also be used. It can be controlled in application frameworks or runtime containers such as [J2EE](./J2EE) [Entity Beans](./Entity_Bean)[[2]](./Isolation_(database_systems)#cite_note-Stony_Brook-2) On older systems, it may be implemented systemically (by the application developers), for example through the use of temporary tables.[*[failed verification](./Wikipedia:Verifiability)*] In two-tier, three-tier, or [n-tier](./Multitier_architecture) web applications a [transaction manager](./Transaction_manager) can be used to maintain isolation. A transaction manager is [middleware](./Middleware_(distributed_applications)) which sits between an app service (back-end application service) and the [operating system](./Operating_system). A transaction manager can provide global isolation and atomicity. It tracks when new servers join a transaction and coordinates an [atomic commit](./Atomic_commit) protocol among the servers. The details are abstracted from the app, making transactions simpler and easier to code. A [transaction processing monitor](./Transaction_processing_system) (TPM) is a collection of middle-ware including a transaction manager. A TPM might provide local isolation to an app with a lock manager.[[2]](./Isolation_(database_systems)#cite_note-Stony_Brook-2)

 

## Read phenomena

 

The ANSI/ISO standard SQL 92 refers to three different *read phenomena* when a transaction retrieves data that another transaction might have updated.

 

In the following examples, two transactions take place. In transaction 1, a query is performed, then in transaction 2, an update is performed, and finally in transaction 1, the same query is performed again.

 

The examples use the following relation:

 
| id | name | age |
| --- | --- | --- |
| 1 | Alice | 20 |
| 2 | Bob | 25 |

 

### Dirty reads

 Main article: [Write-read conflict](./Write-read_conflict) 

A *dirty read* (aka *uncommitted dependency*) occurs when a transaction retrieves a row that has been updated by another transaction that is not yet committed.

 

In this example, transaction 1 retrieves the row with id 1, then transaction 2 updates the row with id 1, and finally transaction 1 retrieves the row with id 1 again. Now if transaction 2 rolls back its update (already retrieved by transaction 1) or performs other updates, then the view of the row may be wrong in transaction 1. At the READ UNCOMMITTED isolation level, the second SELECT in transaction 1 retrieves the updated row: this is a dirty read. At the READ COMMITTED, REPEATABLE READ, and SERIALIZABLE isolation levels, the second SELECT in transaction 1 retrieves the initial row.

 
| Transaction 1 | Transaction 2 |
| --- | --- |
| BEGIN;SELECTageFROMusersWHEREid=1;-- retrieves 20 |  |
|  | BEGIN;UPDATEusersSETage=21WHEREid=1;-- no commit here |
| SELECTageFROMusersWHEREid=1;-- READ UNCOMMITTED retrieves 21 (dirty read)-- READ COMMITTED retrieves 20 (dirty read has been avoided)-- REPEATABLE READ retrieves 20 (dirty read has been avoided)-- SERIALIZABLE retrieves 20 (dirty read has been avoided)COMMIT; |  |
|  | ROLLBACK; |

 

### Non-repeatable reads

 

A *non-repeatable read* occurs when a transaction retrieves a row twice and that row is updated by another transaction that is committed in between.

 

In this example, transaction 1 retrieves the row with id 1, then transaction 2 updates the row with id 1 and is committed, and finally transaction 1 retrieves the row with id 1 again. At the READ UNCOMMITTED and READ COMMITTED isolation levels, the second SELECT in transaction 1 retrieves the updated row: this is a non-repeatable read. At the REPEATABLE READ and SERIALIZABLE isolation levels, the second SELECT in transaction 1 retrieves the initial row.

 
| Transaction 1 | Transaction 2 |
| --- | --- |
| BEGIN;SELECTageFROMusersWHEREid=1;-- retrieves 20 |  |
|  | BEGIN;UPDATEusersSETage=21WHEREid=1;COMMIT; |
| SELECTageFROMusersWHEREid=1;-- READ UNCOMMITTED retrieves 21 (non-repeatable read)-- READ COMMITTED retrieves 21 (non-repeatable read)-- REPEATABLE READ retrieves 20 (non-repeatable read has been avoided)-- SERIALIZABLE retrieves 20 (non-repeatable read has been avoided)COMMIT; |

 

### Phantom reads

 

A *phantom read* occurs when a transaction retrieves a set of rows twice and new rows are inserted into or removed from that set by another transaction that is committed in between.

 

In this example, transaction 1 retrieves the set of rows with age greater than 17, then transaction 2 inserts a row with age 26 and is committed, and finally transaction 1 retrieves the set of rows with age greater than 17 again. At the READ UNCOMMITTED, READ COMMITTED, and REPEATABLE READ isolation levels, the second SELECT in transaction 1 retrieves the new set of rows that includes the inserted row: this is a phantom read. At the SERIALIZABLE isolation level, the second SELECT in transaction 1 retrieves the initial set of rows.

 
| Transaction 1 | Transaction 2 |
| --- | --- |
| BEGIN;SELECTnameFROMusersWHEREage>17;-- retrieves Alice and Bob |  |
|  | BEGIN;INSERTINTOusersVALUES(3,'Carol',26);COMMIT; |
| SELECTnameFROMusersWHEREage>17;-- READ UNCOMMITTED retrieves Alice, Bob and Carol (phantom read)-- READ COMMITTED retrieves Alice, Bob and Carol (phantom read)-- REPEATABLE READ retrieves Alice, Bob and Carol (phantom read)-- SERIALIZABLE retrieves Alice and Bob (phantom read has been avoided)COMMIT; |

 

There are two basic strategies used to prevent non-repeatable reads and phantom reads. In the first strategy, *lock-based concurrency control*, transaction 2 is committed after transaction 1 is committed or rolled back. It produces the serial [schedule](./Database_transaction_schedule) *T1, T2*. In the other strategy, *[multiversion concurrency control](./Multiversion_concurrency_control)*, transaction 2 is committed immediately while transaction 1, which started before transaction 2, continues to operate on an old snapshot of the database taken at the start of transaction 1, and when transaction 1 eventually tries to commit, if the result of committing would be equivalent to the serial schedule *T1, T2*, then transaction 1 is committed; otherwise, there is a commit conflict and transaction 1 is rolled back with a serialization failure.

 

Under lock-based concurrency control, non-repeatable reads and phantom reads may occur when read locks are not acquired when performing a SELECT, or when the acquired locks on affected rows are released as soon as the SELECT is performed. Under multiversion concurrency control, non-repeatable reads and phantom reads may occur when the requirement that a transaction affected by a commit conflict must be rolled back is relaxed.

 

## Isolation levels

 

Of the four [ACID](./ACID) properties in a [DBMS](./Database_management_system) (Database Management System), the isolation property is the one most often relaxed.  When attempting to maintain the highest level of isolation, a DBMS usually acquires [locks](./Lock_(database)) on data which may result in a loss of [concurrency](./Concurrency_(computer_science)), or implements [multiversion concurrency control](./Multiversion_concurrency_control). This requires adding logic for the [application](./Software_application) to function correctly.

 

Most DBMSs offer a number of *transaction isolation levels*, which control the degree of locking that occurs when selecting data. For many database applications, the majority of database transactions can be constructed to avoid requiring high isolation levels (e.g. SERIALIZABLE level), thus reducing the locking overhead for the system.  The programmer must carefully analyze database access code to ensure that any relaxation of isolation does not cause software bugs that are difficult to find. Conversely, if higher isolation levels are used, the possibility of [deadlock](./Deadlock_(computer_science)) is increased, which also requires careful analysis and programming techniques to avoid.

 

Since each isolation level is stronger than those below, in that no higher isolation level allows an action forbidden by a lower one, the standard permits a DBMS to run a transaction at an isolation level stronger than that requested (e.g., a "Read committed" transaction may actually be performed at a "Repeatable read" isolation level).

 

The isolation levels defined by the [ANSI](./American_National_Standards_Institute)/[ISO](./International_Organization_for_Standardization) [SQL](./SQL) standard are listed as follows.

 

### Serializable

 

This is the *highest* isolation level.

 

With a lock-based [concurrency control](./Concurrency_control) DBMS implementation, [serializability](./Serializability) requires read and write locks (acquired on selected data) to be released at the end of the transaction.  Also *range-locks* must be acquired when a [SELECT](./Select_(SQL)) query uses a ranged *WHERE* clause, especially to avoid the ***[phantom reads](./Isolation_(database_systems)#Phantom_reads)*** phenomenon.

 

When using non-lock based concurrency control, no locks are acquired; however, if the system detects a *write collision* among several concurrent transactions, only one of them is allowed to commit.  See *[snapshot isolation](./Snapshot_isolation)* for more details on this topic.

 

From : (Second Informal Review Draft) ISO/IEC 9075:1992, Database Language SQL- July 30, 1992:
*The execution of concurrent SQL-transactions at isolation level SERIALIZABLE is guaranteed to be serializable. A serializable execution is defined to be an execution of the operations of concurrently executing SQL-transactions that produces the same effect as some serial execution of those same SQL-transactions. A serial execution is one in which each SQL-transaction executes to completion before the next SQL-transaction begins.*

 

### Repeatable reads

 

In this isolation level, a lock-based [concurrency control](./Concurrency_control) DBMS implementation keeps read and write locks (acquired on selected data) until the end of the transaction.  However, *range-locks* are not managed, so ***[phantom reads](./Isolation_(database_systems)#Phantom_reads)*** can occur.

 

Write skew is possible at this isolation level in some systems. Write skew is a phenomenon where two writes are allowed to the same column(s) in a table by two different writers (who have previously read the columns they are updating), resulting in the column having data that is a mix of the two transactions.[[3]](./Isolation_(database_systems)#cite_note-3)[[4]](./Isolation_(database_systems)#cite_note-4)

 

### Read committed

 

In this isolation level, a lock-based [concurrency control](./Concurrency_control) DBMS implementation keeps write locks (acquired on selected data) until the end of the transaction, but read locks are released as soon as the [SELECT](./Select_(SQL)) operation is performed (so the ***[non-repeatable reads phenomenon](./Isolation_(database_systems)#Non-repeatable_reads)*** can occur in this isolation level). As in the previous level, *range-locks* are not managed.

 

Putting it in simpler words, read committed is an isolation level that guarantees that any data read is committed at the moment it is read. It simply restricts the reader from seeing any intermediate, uncommitted, 'dirty' read. It makes no promise whatsoever that if the transaction re-issues the read, it will find the same data; data is free to change after it is read.

 

### Read uncommitted

 

This is the *lowest* isolation level. In this level, ***[dirty reads](./Isolation_(database_systems)#Dirty_reads)*** are allowed, so one transaction may see *not-yet-committed* changes made by other transactions.

 

## Default isolation level

 

The *default isolation level* of different [DBMS](./Database_management_system)'s varies quite widely. Most databases that feature transactions allow the user to set any isolation level. Some DBMS's also require additional syntax when performing a SELECT statement to acquire locks (e.g. *SELECT ... FOR UPDATE* to acquire exclusive write locks on accessed rows).

 

However, the definitions above have been criticized as being ambiguous, and as not accurately reflecting the isolation provided by many databases:

 This paper shows a number of weaknesses in the anomaly approach to defining isolation levels. The three ANSI phenomena are ambiguous, and even in their loosest interpretations do not exclude some anomalous behavior ... This leads to some counter-intuitive results. In particular, lock-based isolation levels have different characteristics than their ANSI equivalents. This is disconcerting because commercial database systems typically use locking implementations. Additionally, the ANSI phenomena do not distinguish between a number of types of isolation level behavior that are popular in commercial systems.[[5]](./Isolation_(database_systems)#cite_note-sql-isolation-5) 

There are also other criticisms concerning ANSI SQL's isolation definition, in that it encourages implementors to do "bad things":

 ... it relies in subtle ways on an assumption that a locking schema is used for concurrency control, as opposed to an optimistic or multi-version concurrency scheme. This implies that the proposed semantics are *ill-defined*.[[6]](./Isolation_(database_systems)#cite_note-6) 

## Isolation levels vs read phenomena

 
| Read phenomenonIsolation level | Dirty read | Non-repeatable read | Phantom read |
| --- | --- | --- | --- |
| Serializable | no | no | no |
| Repeatable read | no | no | yes |
| Read committed | no | yes | yes |
| Read uncommitted | yes | yes | yes |

 

Anomaly serializable is not the same as serializable. That is, it is necessary, but not sufficient that a serializable schedule should be free of all three phenomena types.[[5]](./Isolation_(database_systems)#cite_note-sql-isolation-5)

 

## See also

 
- [Atomicity](./Atomicity_(database_systems))
- [Consistency](./Consistency_(database_systems))
- [Durability](./Durability_(database_systems))
- [Lock (database)](./Lock_(database))
- [Optimistic concurrency control](./Optimistic_concurrency_control)
- [Relational Database Management System](./Relational_Database_Management_System)
- [Snapshot isolation](./Snapshot_isolation)

 

## References

  
1. [↑](./Isolation_(database_systems)#cite_ref-1) "Isolation Levels in the Database Engine", TechNet, Microsoft, [https://technet.microsoft.com/en-us/library/ms189122(v=SQL.105).aspx](https://technet.microsoft.com/en-us/library/ms189122(v=SQL.105).aspx)
2. [1](./Isolation_(database_systems)#cite_ref-Stony_Brook_2-0) [2](./Isolation_(database_systems)#cite_ref-Stony_Brook_2-1) "The Architecture of Transaction Processing Systems", Chapter 23, Evolution of Processing Systems, Department of Computer Science, Stony Brook University, retrieved 20 March 2014, [http://www.cs.sunysb.edu/~liu/cse315/23.pdf](http://www.cs.sunysb.edu/~liu/cse315/23.pdf)
3. [↑](./Isolation_(database_systems)#cite_ref-3) Vlad Mihalcea (2015-10-20). ["A beginner's guide to read and write skew phenomena"](https://vladmihalcea.com/2015/10/20/a-beginners-guide-to-read-and-write-skew-phenomena/).
4. [↑](./Isolation_(database_systems)#cite_ref-4) ["Postgresql wiki - SSI"](https://wiki.postgresql.org/wiki/SSI#Simple_Write_Skew).
5. [1](./Isolation_(database_systems)#cite_ref-sql-isolation_5-0) [2](./Isolation_(database_systems)#cite_ref-sql-isolation_5-1)  ["A Critique of ANSI SQL Isolation Levels"](http://www.cs.umb.edu/~poneil/iso.pdf) (PDF). Retrieved 29 July 2012. 
6. [↑](./Isolation_(database_systems)#cite_ref-6) salesforce (2010-12-06). ["Customer testimonials (SimpleGeo, CLOUDSTOCK 2010)"](https://www.youtube.com/v/7J61pPG9j90?version=3). www.DataStax.com: DataStax. Retrieved 2010-03-09. (see above at about 13:30 minutes of the webcast!)

 

## External links

 
- [Oracle® Database Concepts](http://docs.oracle.com/cd/B12037_01/server.101/b10743/toc.htm), [chapter 13 Data Concurrency and Consistency, Preventable Phenomena and Transaction Isolation Levels](http://docs.oracle.com/cd/B12037_01/server.101/b10743/consist.htm#sthref1919)
- [Oracle® Database SQL Reference](http://docs.oracle.com/cd/B19306_01/server.102/b14200/toc.htm), [chapter 19 SQL Statements: SAVEPOINT to UPDATE](http://docs.oracle.com/cd/B19306_01/server.102/b14200/statements_10.htm#i2068385), [SET TRANSACTION](http://docs.oracle.com/cd/B19306_01/server.102/b14200/statements_10005.htm#i2067247)
- in [JDBC](./Java_Database_Connectivity): [Connection constant fields](http://docs.oracle.com/javase/7/docs/api/java/sql/Connection.html#field_summary), [Connection.getTransactionIsolation()](http://docs.oracle.com/javase/7/docs/api/java/sql/Connection.html#getTransactionIsolation()), [Connection.setTransactionIsolation(int)](http://docs.oracle.com/javase/7/docs/api/java/sql/Connection.html#setTransactionIsolation(int))
- in [Spring Framework](./Spring_Framework): [@Transactional](http://static.springsource.org/spring/docs/current/javadoc-api/org/springframework/transaction/annotation/Transactional.html)[*[dead link](./Wikipedia:Link_rot)*], [Isolation](http://static.springsource.org/spring/docs/current/javadoc-api/org/springframework/transaction/annotation/Isolation.html)[*[dead link](./Wikipedia:Link_rot)*]
- [P.Bailis. When is "ACID" ACID? Rarely](http://www.bailis.org/blog/when-is-acid-acid-rarely/)

 
| Authority control databases | GND |
| --- | --- |