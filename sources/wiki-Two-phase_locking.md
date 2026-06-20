---
source: https://en.wikipedia.org/wiki/Two-phase_locking
fetched: 2026-06-19
---

Concurrency control method This article is about [concurrency control](./Concurrency_control). For commit consensus within a distributed transaction, see [Two-phase commit protocol](./Two-phase_commit_protocol). 

In [databases](./Database) and [transaction processing](./Transaction_processing), **two-phase locking** (**2PL**) is a pessimistic [concurrency control](./Concurrency_control) method that guarantees [conflict-serializability](./Database_transaction_schedule#Conflict-serializable).[[1]](./Two-phase_locking#cite_note-Bern1987-1)[[2]](./Two-phase_locking#cite_note-Weikum2001-2) It is also the name of the resulting set of [database transaction](./Database_transaction) [schedules](./Database_transaction_schedule) (histories). The protocol uses [locks](./Lock_(computer_science)), applied by a transaction to data, which may block (interpreted as signals to stop) other transactions from accessing the same data during the transaction's life.

 

By the 2PL protocol, locks are applied and removed in two phases:

 
1. Expanding phase: locks are acquired and no locks are released.
2. Shrinking phase: locks are released and no locks are acquired.

 

Two types of locks are used by the basic protocol: *Shared* and *Exclusive* locks. Refinements of the basic protocol may use more lock types. Using locks that block processes, 2PL, S2PL, and SS2PL may be subject to [deadlocks](./Deadlock_(computer_science)) that result from the mutual blocking of two or more transactions.

 

## Read and write locks

 

Locks are used to guarantee [serializability](./Serializability). A transaction is *holding* a [lock](./Lock_(computer_science)) on an object if that transaction has acquired a lock on that object which has not yet been released.

 

For 2PL, the only used data-access locks are **read-locks** (**shared locks**) and **write-locks** (**exclusive locks**). Below are the rules for *read-locks* and *write-locks*:

 
- A transaction is allowed to read an object [if and only if](./If_and_only_if) it is holding a *read-lock* or *write-lock* on that object.
- A transaction is allowed to write an object if and only if it is holding a *write-lock* on that object.
- A [schedule](./Database_transaction_schedule) (i.e., a set of transactions) is allowed to hold multiple locks on the same object simultaneously if and only if none of those locks are write-locks. If a disallowed lock attempts on being held simultaneously, it will be blocked.

 
| Lock type | read-lock | write-lock |
| --- | --- | --- |
| read-lock | ✔ | X |
| write-lock | X | X |

 

## Variants

 
|  | guarantees conflict-serializability | eliminates deadlocks | guarantees recoverability | guarantees strictness | preventsphantom reads | preventsdirty reads |
| --- | --- | --- | --- | --- | --- | --- |
| 2PL | Yes | No | No | No | No | No |
| C2PL | Yes | Yes | yes?[citation needed] | yes?[citation needed] | No[citation needed] | Yes[citation needed] |
| S2PL | Yes | No | Yes | Yes | Yes | Yes |
| SS2PL | Yes | No | Yes | Yes | Yes | Yes |

 

Note that all conflict serializable schedules are also view serializable (but not vice-versa).

 

### Two-phase locking

 

According to the **two-phase locking** protocol, each transaction handles its locks in two distinct, consecutive phases during the transaction's execution:

 
1. **Expanding phase** (aka Growing phase): locks are acquired and no locks are released (the number of locks can only increase).
2. **Shrinking phase** (aka Contracting phase): locks are released and no locks are acquired.

 

The two phase locking rules can be summarized as: each transaction must never acquire a lock after it has released a lock. The [serializability](./Serializability) property is guaranteed for a schedule with transactions that obey this rule.

 

Typically, without explicit knowledge in a transaction on end of phase 1, the rule is safely determined only when a transaction has completed processing and requested commit. In this case, all the locks can be released at once (phase 2).

 

### Conservative two-phase locking

 
|  | This sectiondoes notciteanysources.Please helpimprove this sectionbyadding citations to reliable sources. Unsourced material may be challenged andremoved.(November 2024)(Learn how and when to remove this message) |
| --- | --- |

 

Conservative two-phase locking (C2PL) differs from 2PL in that transactions obtain all the locks they need before the actual execution begins. This is to ensure that a transaction that already holds some locks will not block waiting for other locks. C2PL *prevents* [deadlocks](./Deadlock_(computer_science)). 

 

In cases of heavy lock [contention](./Resource_contention), C2PL reduces the time locks are held on average, relative to 2PL and Strict 2PL, because transactions that hold locks are never blocked. In light lock contention, C2PL holds more locks than is necessary, because it is difficult to predict which locks will be needed in the future, thus leading to higher overhead. 

 

A C2PL transaction will not obtain any locks if it cannot obtain all the locks it needs in its initial request. Furthermore, each transaction needs to declare its read and write set (the data items that will be read/written), which is not always possible. Because of these limitations, C2PL is not used very frequently.

 

### Strict two-phase locking

 

To comply with the strict two-phase locking (S2PL) protocol, a transaction needs to comply with 2PL, and release its *write (exclusive)* locks only after the transaction has ended (i.e., either *committed* or *aborted*). On the other hand, *read (shared)* locks are released regularly during the shrinking phase. 

 

Unlike 2PL, S2PL provides [strictness](./Database_transaction_schedule#Strict) (a special case of cascade-less recoverability). This protocol is not appropriate in [B-trees](./B-tree) because it causes Bottleneck (while B-trees always starts searching from the parent root). [*[citation needed](./Wikipedia:Citation_needed)*]

 

### Strong strict two-phase locking

 

or **Rigorousness**, or **Rigorous scheduling**, or **Rigorous two-phase locking**

 

To comply with **strong strict two-phase locking** (SS2PL), a transaction's read and write locks are released only after that transaction has ended (i.e., either committed or aborted). A transaction obeying SS2PL has only a phase 1 and lacks a phase 2 until the transaction has completed. Every SS2PL schedule is also an S2PL schedule, but not vice versa.

 

## See also

 
- [Serializability](./Serializability)
- [Lock (computer science)](./Lock_(computer_science))
- [Deadlock  (computer science)](./Deadlock_(computer_science))

 

## References

  
1. [↑](./Two-phase_locking#cite_ref-Bern1987_1-0) [Philip A. Bernstein](./Phil_Bernstein), Vassos Hadzilacos, Nathan Goodman (1987): [*Concurrency Control and Recovery in Database Systems*](http://research.microsoft.com/en-us/people/philbe/ccontrol.aspx), Addison Wesley Publishing Company, [ISBN](./ISBN_(identifier)) [0-201-10715-5](./Special:BookSources/0-201-10715-5)
2. [↑](./Two-phase_locking#cite_ref-Weikum2001_2-0) [Gerhard Weikum](./Gerhard_Weikum), Gottfried Vossen (2001): [*Transactional Information Systems*](http://www.elsevier.com/wps/find/bookdescription.cws_home/677937/description#description), Elsevier, [ISBN](./ISBN_(identifier)) [1-55860-508-8](./Special:BookSources/1-55860-508-8)