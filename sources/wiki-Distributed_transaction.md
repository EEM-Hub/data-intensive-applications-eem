---
source: https://en.wikipedia.org/wiki/Distributed_transaction
fetched: 2026-06-19
---

Database transaction between two or more networks 

A **distributed transaction** operates within a [distributed environment](./Distributed_computing), typically involving multiple nodes across a network depending on the location of the data. A key aspect of distributed transactions is [atomicity](./Atomicity_(programming)), which ensures that the transaction is completed in its entirety or not executed at all. It's essential to note that distributed transactions are not limited to [databases](./Database). [[1]](./Distributed_transaction#cite_note-1)

 

[The Open Group](./The_Open_Group), a vendor consortium, proposed the [X/Open Distributed Transaction Processing Model](./X/Open_XA) (X/Open XA), which became a de facto standard for the behavior of transaction model components.

 

Databases are common transactional resources and, often, transactions span a couple of such databases. In this case, a distributed transaction can be seen as a [database transaction](./Database_transaction) that must be [synchronized](./Synchronization) (or provide [ACID](./ACID) properties) among multiple participating [databases](./Database) which are [distributed](./Distributed_computing) among different physical locations. The [isolation](./Isolation_(computer_science)) property (the I of ACID) poses a special challenge for multi database transactions, since the (global) [serializability](./Serializability) property could be violated, even if each database provides it (see also [global serializability](./Global_serializability)). In practice most commercial database systems use [strong strict two-phase locking (SS2PL)](./Two-phase_locking#Strong_strict_two-phase_locking) for [concurrency control](./Concurrency_control), which ensures global serializability, if all the participating databases employ it.

 

A common [algorithm](./Algorithm) for ensuring [correct](./Correctness_(computer_science)) completion of a distributed transaction is the [two-phase commit](./Two-phase_commit) (2PC). This algorithm is usually applied for updates able to [commit](./Commit_(data_management)) in a short period of time, ranging from couple of milliseconds to couple of minutes.

 

There are also long-lived distributed transactions, for example a transaction to book a trip, which consists of booking a flight, a rental car and a hotel. Since booking the flight might take up to a day to get a confirmation, two-phase commit is not applicable here, it will lock the resources for this long. In this case more sophisticated techniques that involve multiple undo levels are used. The way you can undo the hotel booking by calling a desk and cancelling the reservation, a system can be designed to undo certain operations (unless they are irreversibly finished).

 

In practice, long-lived distributed transactions are implemented in systems based on [web services](./Web_Services). Usually these transactions utilize principles of [compensating transactions](./Compensating_transaction), Optimism and Isolation Without Locking. The X/Open standard does not cover long-lived distributed transactions.[*[citation needed](./Wikipedia:Citation_needed)*]

 

Several technologies, including [Jakarta Enterprise Beans](./Enterprise_Java_Beans) and [Microsoft Transaction Server](./Microsoft_Transaction_Server) fully support distributed transaction standards.

 

## Synchronization

 

In [event-driven architectures](./Event-driven_architecture), distributed transactions can be [synchronized](./Synchronization_(computer_science)) through using [request–response](./Request–response) paradigm and it can be implemented in two ways: [[2]](./Distributed_transaction#cite_note-:02-2)

 
- Creating two separate [queues](./Message_queue): one for requests and the other for replies. The event producer must wait until it receives the response.
- Creating one dedicated ephemeral [queue](./Message_queue) for each request.

 

## See also

 
- [Java Transaction API](./Java_Transaction_API)

 

## References

  
1. [↑](./Distributed_transaction#cite_ref-1) Gray, Jim. *Transaction Processing Concepts and Techniques*. Morgan Kaufmann. [ISBN](./ISBN_(identifier)) [9780080519555](./Special:BookSources/9780080519555).
2. [↑](./Distributed_transaction#cite_ref-:02_2-0) Richards, Mark. *Fundamentals of Software Architecture: An Engineering Approach*. O'Reilly Media. [ISBN](./ISBN_(identifier)) [978-1492043454](./Special:BookSources/978-1492043454).

 
- ["Web-Services Transactions"](https://web.archive.org/web/20080511221610/http://xml.sys-con.com/read/43755.htm). Archived from [the original](http://xml.sys-con.com/read/43755.htm) on May 11, 2008. Retrieved May 2, 2005.
- ["Nuts And Bolts Of Transaction Processing"](https://web.archive.org/web/20180713045114/http://comet.lehman.cuny.edu/cocchi/CIS256/StudentReading/TransactionProcessing.doc). *Article about Transaction Management*. Archived from [the original](http://comet.lehman.cuny.edu/cocchi/CIS256/StudentReading/TransactionProcessing.doc) on July 13, 2018. Retrieved May 3, 2005.
- ["A Detailed Comparison of Enterprise JavaBeans (EJB) & The Microsoft Transaction Server (MTS) Models"](http://gsraj.tripod.com/misc/ejbmtscomp.html).

 

## Further reading

 
- Gerhard Weikum, Gottfried Vossen, *Transactional information systems: theory, algorithms, and the practice of concurrency control and recovery*, Morgan Kaufmann, 2002, [ISBN](./ISBN_(identifier)) [1-55860-508-8](./Special:BookSources/1-55860-508-8)