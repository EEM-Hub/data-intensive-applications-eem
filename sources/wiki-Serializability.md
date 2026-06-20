---
source: https://en.wikipedia.org/wiki/Serializability
fetched: 2026-06-19
---

Order of execution of transactions in transaction processing This article is about databases and transaction processing. For other uses, see [Scheduling (computing)](./Scheduling_(computing)). 
|  | This articleneeds additional citations forverification.Please helpimprove this articlebyadding citations to reliable sources. Unsourced material may be challenged and removed.Find sources:"Database transaction schedule"–news·newspapers·books·scholar·JSTOR(November 2012)(Learn how and when to remove this message) |
| --- | --- |

 

In the fields of [databases](./Database) and [transaction processing](./Transaction_processing) (transaction management), a **schedule** (or **history**) of a system is an abstract model to describe the order of [executions](./Execution_(computing)) in a set of transactions running in the system. Often it is a *list* of operations (actions) ordered by time, performed by a set of [transactions](./Database_transaction) that are executed together in the system. If the order in time between certain operations is not determined by the system, then a *[partial order](./Partial_order)* is used. Examples of such operations are requesting a read operation, reading, writing, aborting, [committing](./Commit_(data_management)), requesting a [lock](./Lock_(computer_science)), locking, etc. Often, only a subset of the transaction operation types are included in a schedule. 

 

Schedules are fundamental concepts in database [concurrency control](./Concurrency_control) theory. In practice, most general purpose database systems employ conflict-serializable and strict recoverable schedules.

 

## Notation

 

Grid notation:

 
- **Columns:** The different transactions in the schedule.
- **Rows:** The time [order of operations](./Order_of_operations) (a.k.a., actions).

 

Operations (a.k.a., actions):

 
- **R(X):** The corresponding transaction "reads" object X (i.e., it retrieves the data stored at X). This is done so that it can modify the data (e.g., X=X+4) during a "write" operation rather than merely overwrite it. When the schedule is represented as a list rather than a grid, the action is represented as     R i ( X )   {\displaystyle Ri(X)}  ![{\displaystyle Ri(X)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e17d26b9c6746d7e84f2da1b0244f20cebb00033) where     i   {\displaystyle i}  ![{\displaystyle i}](https://wikimedia.org/api/rest_v1/media/math/render/svg/add78d8608ad86e54951b8c8bd6c8d8416533d20) is a number corresponding to a specific transaction.
- **W(X):** The corresponding transaction "writes" to object X (i.e., it modifies the data stored at X). When the schedule is represented as a list rather than a grid, the action is represented as     W i ( X )   {\displaystyle Wi(X)}  ![{\displaystyle Wi(X)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0f8ce0cfa1fd54127a0967af1b2bee035571aadf) where     i   {\displaystyle i}  ![{\displaystyle i}](https://wikimedia.org/api/rest_v1/media/math/render/svg/add78d8608ad86e54951b8c8bd6c8d8416533d20) is a number corresponding to a specific transaction.
- **Com.:** This represents a "commit" operation in which the corresponding transaction has successfully completed its preceding actions, and has made all its changes permanent in the database.

 

Alternatively, a schedule can be represented with a *[directed acyclic graph](./Acyclic_directed_graph)* (or DAG) in which there is an arc (i.e., [directed edge](./Directed_edge)) between each *[ordered pair](./Ordered_pair)* of operations.

 

### Example

 

The following is an example of a schedule:

 
| T1 | T2 | T3 |
| --- | --- | --- |
| R(X) |  |  |
| W(X) |  |  |
| Com. |  |  |
|  | R(Y) |  |
|  | W(Y) |  |
|  | Com. |  |
|  |  | R(Z) |
|  |  | W(Z) |
|  |  | Com. |

 

In this example, the columns represent the different transactions in the schedule D. Schedule D consists of three transactions T1, T2, T3. First T1 Reads and Writes to object X, and then Commits. Then T2 Reads and Writes to object Y and Commits, and finally, T3 Reads and Writes to object Z and Commits.

 

The schedule D above can be represented as list in the following way:

 

D = R1(X) W1(X) Com1 R2(Y) W2(Y) Com2 R3(Z) W3(Z) Com3

 

## Duration and order of actions

 

Usually, for the purpose of reasoning about concurrency control in databases, an operation is modelled as *[atomic](./Atomicity_(database_systems))*, occurring at a point in time, without duration. Real executed operations always have some duration.

 

Operations of transactions in a schedule can interleave (i.e., transactions can be executed [concurrently](./Concurrency_(computer_science))), but time orders between operations in each transaction must remain unchanged. The schedule is in *[partial order](./Partial_order)* when the operations of transactions in a schedule interleave (i.e., when the schedule is conflict-serializable but not serial). The schedule is in *[total order](./Partial_order)* when the operations of transactions in a schedule do not interleave (i.e., when the schedule is serial). 

 

## Types of schedule

 

A **complete schedule** is one that contains either an abort (a.k.a. **[rollback](./Rollback_(data_management)))** or commit action for each of its transactions. A transaction's last action is either to commit or abort. To maintain [atomicity](./Atomicity_(database_systems)), a transaction must undo all its actions if it is aborted.

 

### Serial

 

A schedule is **serial** if the executed transactions are non-interleaved (i.e., a serial schedule is one in which no transaction starts until a running transaction has ended).

 

Schedule D is an example of a serial schedule:

 
| T1 | T2 | T3 |
| --- | --- | --- |
| R(X) |  |  |
| W(X) |  |  |
| Com. |  |  |
|  | R(Y) |  |
|  | W(Y) |  |
|  | Com. |  |
|  |  | R(Z) |
|  |  | W(Z) |
|  |  | Com. |

 

### Serializable

 This section is linked from [[Concurrency control]]  

A schedule is **serializable** if it is equivalent (in its outcome) to a serial schedule. 

 

In schedule E, the order in which the actions of the transactions are executed is not the same as in D, but in the end, E gives the same result as D.

 
| T1 | T2 | T3 |
| --- | --- | --- |
| R(X) |  |  |
|  | R(Y) |  |
|  |  | R(Z) |
| W(X) |  |  |
|  | W(Y) |  |
|  |  | W(Z) |
| Com. | Com. | Com. |

 

Serializability is used to keep the data in the data item in a consistent state. It is the major criterion for the correctness of concurrent transactions' schedule, and thus supported in all general purpose database systems. Schedules that are not serializable are likely to generate erroneous outcomes; which can be extremely harmful (e.g., when dealing with money within banks).[[1]](./Database_transaction_schedule#cite_note-Bernstein872-1)[[2]](./Database_transaction_schedule#cite_note-Weikum012-2)[[3]](./Database_transaction_schedule#cite_note-Herlihy1993-3)

 

If any specific order between some transactions is requested by an application, then it is enforced independently of the underlying serializability mechanisms. These mechanisms are typically indifferent to any specific order, and generate some unpredictable [partial order](./Partial_order) that is typically compatible with multiple serial orders of these transactions.

 

#### Conflicting actions

 

Two actions are said to be in conflict (conflicting pair) [if and only if](./If_and_only_if) all of the 3 following conditions are satisfied:

 
1. The actions belong to different transactions.
2. At least one of the actions is a write operation.
3. The actions access the same object (read or write).[[4]](./Database_transaction_schedule#cite_note-:0-4)[[5]](./Database_transaction_schedule#cite_note-5)

 

Equivalently, two actions are considered conflicting if and only if they are [noncommutative](./Commutative_property). Equivalently, two actions are considered conflicting if and only if they are a [read-write](./Read–write_conflict), [write-read](./Write–read_conflict), or [write-write](./Write–write_conflict) conflict.

 

The following set of actions is conflicting:

 
- R1(X), W2(X), W3(X) (3 conflicting pairs)

 

While the following sets of actions are not conflicting: 

 
- R1(X), R2(X), R3(X)
- R1(X), W2(Y), R3(X)

 

Reducing conflicts, such as through commutativity, enhances performance because conflicts are the fundamental cause of delays and aborts.

 

The conflict is **materialized** if the requested conflicting operation is actually executed: in many cases a requested/issued conflicting operation by a transaction is delayed and even never executed, typically by a [lock](./Lock_(computer_science)) on the operation's object, held by another transaction, or when writing to a transaction's temporary private workspace and materializing, copying to the database itself, upon commit; as long as a requested/issued conflicting operation is not executed upon the database itself, the conflict is **non-materialized**; non-materialized conflicts are not represented by an edge in the precedence graph.

 

#### Conflict equivalence

 

The schedules S1 and S2 are said to be conflict-equivalent if and only if both of the following two conditions are satisfied:

 
1. Both schedules S1 and S2 involve the same set of transactions such that each transaction has the same actions in the same order.
2. Both schedules have the same set of conflicting pairs (such that the actions in each conflicting pair are in the same order).[[6]](./Database_transaction_schedule#cite_note-6) This is equivalent to requiring that all conflicting operations (i.e., operations in any conflicting pair) are in the same order in both schedules.

 

Equivalently, two schedules are said to be conflict equivalent if and only if one can be transformed to another by swapping pairs of non-conflicting operations (whether adjacent or not) while maintaining the order of actions for each transaction.[[4]](./Database_transaction_schedule#cite_note-:0-4)

 

Equivalently, two schedules are said to be conflict equivalent if and only if one can be transformed to another by swapping pairs of non-conflicting adjacent operations with different transactions.[[7]](./Database_transaction_schedule#cite_note-7)

 

#### Conflict-serializable

 

A schedule is said to be **conflict-serializable** when the schedule is conflict-equivalent to one or more serial schedules.

 

Equivalently, a schedule is conflict-serializable if and only if its [precedence graph](./Precedence_graph) is acyclic when only committed transactions are considered. Note that if the graph is defined to also include uncommitted transactions, then cycles involving uncommitted transactions may occur without conflict serializability violation.

 

The schedule K is conflict-equivalent to the serial schedule <T1,T2>, but not <T2,T1>.

 
| T1 | T2 |
| --- | --- |
| R(A) |  |
|  | R(A) |
| W(B) |  |
| Com. |  |
|  | W(A) |
|  | Com. |

 

Conflict serializability can be enforced by restarting any transaction within the cycle in the precedence graph, or by implementing [two-phase locking](./Two-phase_locking), [timestamp ordering](./Timestamp-based_concurrency_control), or [serializable snapshot isolation](./Snapshot_isolation#Workarounds).[[8]](./Database_transaction_schedule#cite_note-Cahill082-8)

 

#### View equivalence

 

Two schedules S1 and S2 are said to be view-equivalent when the following conditions are satisfied:

 
1. If the transaction      T  i     {\displaystyle T_{i}}  ![{\displaystyle T_{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a8dd1c50cb9436474f83624c3f679ccf3eebbfef) in S1 reads an initial value for object X, so does the same transaction      T  i     {\displaystyle T_{i}}  ![{\displaystyle T_{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a8dd1c50cb9436474f83624c3f679ccf3eebbfef) in S2.
2. If the transaction      T  i     {\displaystyle T_{i}}  ![{\displaystyle T_{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a8dd1c50cb9436474f83624c3f679ccf3eebbfef) reads a value (for an object X) written by the transaction      T  j     {\displaystyle T_{j}}  ![{\displaystyle T_{j}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/27cdb9041c8aa769beb9153a48f41002297faacc) in S1, it must do so in S2.
3. If the transaction      T  i     {\displaystyle T_{i}}  ![{\displaystyle T_{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a8dd1c50cb9436474f83624c3f679ccf3eebbfef) in S1 does the final write for object X, so does the same transaction      T  i     {\displaystyle T_{i}}  ![{\displaystyle T_{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a8dd1c50cb9436474f83624c3f679ccf3eebbfef) in S2.

 

Additionally, two view-equivalent schedules must involve the same set of transactions such that each transaction has the same actions in the same order.

 

In the example below, the schedules S1 and S2 are view-equivalent, but neither S1 nor S2 are view-equivalent to the schedule S3.

 
| S1 | S2 | S3 |
| --- | --- | --- |
| T1 | T2 | T1 | T2 | T1 | T2 |
| R(A) |  | R(A) |  | R(A) |  |
| W(A) |  | W(A) |  | W(A) |  |
| R(B)(1) |  |  | R(A) |  | R(A) |
| W(B) |  |  | W(A) |  | W(A) |
| Com. |  | R(B)(1) |  |  | R(B)(1) |
|  | R(A) | W(B) |  |  | W(B) |
|  | W(A) | Com. |  | R(B)(2) |  |
|  | R(B)(2) |  | R(B)(2) | W(B)(3) |  |
|  | W(B)(3) |  | W(B)(3) | Com. |  |
|  | Com. |  | Com. |  | Com. |

 

The conditions for S3 to be view-equivalent to S1 and S2 were not satisfied at the corresponding superscripts for the following reasons:

 
1. Failed the first condition of view equivalence because T1 read the initial value for B in S1 and S2, but T2 read the initial value for B in S3.
2. Failed the second condition of view equivalence because T2 read the value written by T1 for B in S1 and S2, but T1 read the value written by T2 for B in S3.
3. Failed the third condition of view equivalence because T2 did the final write for B in S1 and S2, but T1 did the final write for B in S3.

 

To quickly analyze whether two schedules are view-equivalent, write both schedules as a list with each action's subscript representing which view-equivalence condition they match. The schedules are view equivalent if and only if all the actions have the same subscript (or lack thereof) in both schedules:

 
- S1: R1(A)initial read, W1(A), R1(B)initial read, W1(B), Com1, R2(A)written by T1, W2(A)final write, R2(B)written by T1, W2(B)final write, Com2
- S2: R1(A)initial read, W1(A), R2(A)written by T1, W2(A)final write, R1(B)initial read, W1(B), Com1, R2(B)written by T1, W2(B)final write, Com2
- S3: R1(A)initial read, W1(A), R2(A)written by T1, W2(A)final write, **R2(B)initial read, W2(B), R1(B)written by T2, W1(B)final write,** Com1, Com2

 

#### View-serializable

 

A schedule is **view-serializable** if it is view-equivalent to some serial schedule. Note that by definition, all conflict-serializable schedules are view-serializable.

 
| T1 | T2 |
| --- | --- |
| R(A) |  |
|  | R(A) |
| W(B) |  |

 

Notice that the above example (which is the same as the example in the discussion of conflict-serializable) is both view-serializable and conflict-serializable at the same time. There are however view-serializable schedules that are not conflict-serializable: those schedules with a transaction performing a [blind write](./Blind_write):

 
| T1 | T2 | T3 |
| --- | --- | --- |
| R(A) |  |  |
|  | W(A) |  |
|  | Com. |  |
| W(A) |  |  |
| Com. |  |  |
|  |  | W(A) |
|  |  | Com. |

 

The above example is not conflict-serializable, but it is view-serializable since it has a view-equivalent serial schedule <T1,| T2,| T3>.

 

Since determining whether a schedule is view-serializable is [NP-complete](./NP-complete), view-serializability has little practical interest.[*[citation needed](./Wikipedia:Citation_needed)*]

 

### Recoverable

 This section is linked from [[Concurrency control]]  

In a **recoverable schedule**, transactions only commit after all transactions whose changes they read have committed. A schedule becomes **unrecoverable** if a transaction      T  i     {\displaystyle T_{i}}  ![{\displaystyle T_{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a8dd1c50cb9436474f83624c3f679ccf3eebbfef) reads and relies on changes from another transaction      T  j     {\displaystyle T_{j}}  ![{\displaystyle T_{j}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/27cdb9041c8aa769beb9153a48f41002297faacc), and then      T  i     {\displaystyle T_{i}}  ![{\displaystyle T_{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a8dd1c50cb9436474f83624c3f679ccf3eebbfef) commits and      T  j     {\displaystyle T_{j}}  ![{\displaystyle T_{j}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/27cdb9041c8aa769beb9153a48f41002297faacc) aborts.

 
| F | F2 | J |
| --- | --- | --- |
| T1 | T2 | T1 | T2 | T1 | T2 |
| R(A) |  | R(A) |  | R(A) |  |
| W(A) |  | W(A) |  | W(A) |  |
|  | R(A) |  | R(A) |  | R(A) |
|  | W(A) |  | W(A) |  | W(A) |
| Com. |  | Abort |  |  | Com. |
|  | Com. |  | Abort | Abort |  |

 

These schedules are recoverable. The schedule F is recoverable because T1 commits before T2, that makes the value read by T2 correct. Then T2 can commit itself. In the F2 schedule, if T1 aborted, T2 has to abort because the value of A it read is incorrect. In both cases, the database is left in a consistent state.

 

Schedule J is unrecoverable because T2 committed before T1 despite previously reading the value written by T1. Because T1 aborted after T2 committed, the value read by T2 is wrong. Because a transaction cannot be rolled-back after it commits, the schedule is unrecoverable.

 

#### Cascadeless

 

**Cascadeless schedules** (a.k.a. "Avoiding Cascading Aborts (ACA) schedules") are schedules which avoid cascading aborts by disallowing [dirty reads](./Write–read_conflict). **Cascading aborts** occur when one transaction's abort causes another transaction to abort because it read and relied on the first transaction's changes to an object. A **dirty read** occurs when a transaction reads data from uncommitted write in another transaction.[[9]](./Database_transaction_schedule#cite_note-9)

 

The following examples are the same as the ones in the discussion on recoverable:

 
| F | F2 |
| --- | --- |
| T1 | T2 | T1 | T2 |
| R(A) |  | R(A) |  |
| W(A) |  | W(A) |  |
|  | R(A) |  | R(A) |
|  | W(A) |  | W(A) |
| Com. |  | Abort |  |
|  | Com. |  | Abort |

 

In this example, although F2 is recoverable, it does not avoid 
cascading aborts. It can be seen that if T1 aborts, T2 will have to 
be aborted too in order to maintain the correctness of the schedule 
as T2 has already read the uncommitted value written by T1.

 

The following is a recoverable schedule which avoids cascading abort. Note, however, that the update of A by T1 is always lost (since T1 is aborted).

 
| T1 | T2 |
| --- | --- |
|  | R(A) |
| R(A) |  |
| W(A) |  |
|  | W(A) |
| Abort |  |
|  | Commit |

 

Note that this Schedule would not be serializable if T1 would be committed.
Cascading aborts avoidance is sufficient but not necessary for a schedule to be recoverable.

 

#### Strict

 

A schedule is **strict** if for any two transactions T1, T2, if a write operation of T1 precedes a *conflicting* operation of T2 (either read or write), then the commit or abort event of T1 also precedes that conflicting operation of T2. For example, the schedule F3 above is strict.

 

Any strict schedule is cascade-less, but not the converse. Strictness allows efficient recovery of databases from failure.

 

## Serializability class relationships

 

The following expressions illustrate the hierarchical (containment) relationships between [serializability](./Serializability) and [recoverability](./Serializability#Correctness_-_recoverability) classes:

 
- Serial ⊂ conflict-serializable ⊂ view-serializable ⊂ all schedules
- Serial ⊂ strict ⊂ cascadeless (ACA) ⊂ recoverable ⊂ all schedules

 

The [Venn diagram](./Venn_diagram) (below) illustrates the above clauses graphically.

 [![](//upload.wikimedia.org/wikipedia/commons/f/f1/Schedule-serializability.png)](./File:Schedule-serializability.png)Venn diagram for serializability and recoverability classes 

## See also

 
- [Schedule (project management)](./Schedule_(project_management))
- [Strong strict two-phase locking](./Two-phase_locking) (SS2PL or Rigorousness).
- [Making snapshot isolation serializable](./Snapshot_isolation#Making_Snapshot_Isolation_Serializable)[[8]](./Database_transaction_schedule#cite_note-Cahill082-8) in [Snapshot isolation](./Snapshot_isolation).
- [Global serializability](./Global_serializability), where the *Global serializability problem* and its proposed solutions are described.
- [Linearizability](./Linearizability), a more general concept in [concurrent computing](./Concurrent_computing).

 

## References

  
1. [↑](./Database_transaction_schedule#cite_ref-Bernstein872_1-0) [Philip A. Bernstein](./Phil_Bernstein), Vassos Hadzilacos, Nathan Goodman (1987): [*Concurrency Control and Recovery in Database Systems*](http://research.microsoft.com/en-us/people/philbe/ccontrol.aspx) (free PDF download), Addison Wesley Publishing Company, [ISBN](./ISBN_(identifier)) [0-201-10715-5](./Special:BookSources/0-201-10715-5)
2. [↑](./Database_transaction_schedule#cite_ref-Weikum012_2-0) [Gerhard Weikum](./Gerhard_Weikum), Gottfried Vossen (2001): [*Transactional Information Systems*](http://www.elsevier.com/wps/find/bookdescription.cws_home/677937/description#description), Elsevier, [ISBN](./ISBN_(identifier)) [1-55860-508-8](./Special:BookSources/1-55860-508-8)
3. [↑](./Database_transaction_schedule#cite_ref-Herlihy1993_3-0) [Maurice Herlihy](./Maurice_Herlihy) and J. Eliot B. Moss. *Transactional memory: architectural support for lock-free data structures.* Proceedings of the 20th annual international symposium on Computer architecture (ISCA '93). Volume 21, Issue 2, May 1993.
4. [1](./Database_transaction_schedule#cite_ref-:0_4-0) [2](./Database_transaction_schedule#cite_ref-:0_4-1) ["Conflict Serializability in DBMS"](https://www.geeksforgeeks.org/conflict-serializability-in-dbms/). *GeeksforGeeks*. 2015-12-29. Retrieved 2023-11-27.
5. [↑](./Database_transaction_schedule#cite_ref-5) Silberschatz, Abraham; Korth, Henry F.; Sudarshan, S. (2020). *Database system concepts* (Seventh ed.). New York, NY: McGraw-Hill Education. p. 814. [ISBN](./ISBN_(identifier)) [978-1-260-08450-4](./Special:BookSources/978-1-260-08450-4).
6. [↑](./Database_transaction_schedule#cite_ref-6) Ramakrishnan, Raghu; Gehrke, Johannes (2000). *Database management systems*. Computer science series (2nd ed.). Boston: McGraw-Hill. p. 540. [ISBN](./ISBN_(identifier)) [978-0-07-232206-4](./Special:BookSources/978-0-07-232206-4).
7. [↑](./Database_transaction_schedule#cite_ref-7) Garcia-Molina, Hector; Ullman, Jeffrey D.; Widom, Jennifer (2009). *Database systems: the complete book*. Pearson international edition (2nd ed.). Upper Saddle River, NJ: Pearson/Prentice Hall. pp. 891–892. [ISBN](./ISBN_(identifier)) [978-0-13-187325-4](./Special:BookSources/978-0-13-187325-4).
8. [1](./Database_transaction_schedule#cite_ref-Cahill082_8-0) [2](./Database_transaction_schedule#cite_ref-Cahill082_8-1) Michael J. Cahill, Uwe Röhm, Alan D. Fekete (2008): ["Serializable isolation for snapshot databases"](http://portal.acm.org/citation.cfm?id=1376690), *Proceedings of the 2008 ACM SIGMOD international conference on Management of data*, pp. 729-738, Vancouver, Canada, June 2008, [ISBN](./ISBN_(identifier)) [978-1-60558-102-6](./Special:BookSources/978-1-60558-102-6) (SIGMOD 2008 best paper award)
9. [↑](./Database_transaction_schedule#cite_ref-9) ["Cascadeless in DBMS"](https://www.geeksforgeeks.org/cascadeless-in-dbms/). *GeeksforGeeks*. 2019-08-06. Retrieved 2023-11-29.