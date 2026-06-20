---
source: https://en.wikipedia.org/wiki/Commit_(data_management)
fetched: 2026-06-19
---

Making a set of tentative changes to a database permanent For the revision control concept, see [Commit (revision control)](./Commit_(revision_control)). 
|  | This articleneeds additional citations forverification.Please helpimprove this articlebyadding citations to reliable sources. Unsourced material may be challenged and removed.Find sources:"Commit"data management–news·newspapers·books·scholar·JSTOR(May 2014)(Learn how and when to remove this message) |
| --- | --- |

 
| Commit (data management) |
| --- |
| Developers | Computer science researchers (e.g., Jim Gray, IBM R* team) |
| Operating system | Cross-platform |
| Platform | Database systems, distributed systems, blockchain networks |
| Type | Transaction protocol / Data consistency mechanism |

  

In [computer science](./Computer_science) and [data management](./Data_management), a **commit** is a behavior that marks the end of a transaction and provides [Atomicity](./Atomicity_(database_systems)), [Consistency](./Consistency_(database_systems)), [Isolation](./Isolation_(database_systems)), and [Durability](./Durability_(database_systems)) (ACID) in transactions. The submission records are stored in the submission [log](./Log_file) for recovery and consistency in case of failure. In terms of transactions, the opposite of committing is giving up tentative changes to the transaction, which is rolled back.

 

Due to the rise of [distributed computing](./Distributed_computing) and the need to ensure [data consistency](./Data_consistency) across multiple systems, commit protocols have been evolving since their emergence in the 1970s. The main developments include the [Two-Phase Commit](./Two-phase_commit_protocol) (2PC) first proposed by [Jim Gray](./Jim_Gray_(computer_scientist)), which is the fundamental core of distributed transaction management. Subsequently, the [Three-phase Commit](./Three-phase_commit_protocol) (3PC), Hypothesis Commit (PC), Hypothesis Abort (PA), and Optimistic Commit protocols gradually emerged, solving the problems of blocking and [fault recovery](./Fault_recovery).

 

Today, new fields such as [e-commerce](./E-commerce) payment and [blockchain](./Blockchain) technology are emerging, and submission protocols play a significant role in various business areas. By effectively handling transactions, resolving faults and recovering problems, the commit protocol becomes crucial in ensuring the [reliability](./Reliability_(computer_networking)) and consistency of data management.

 

## History

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/7/76/Jim_Gray_Computing_in_the_21st_Century_2006.jpg/250px-Jim_Gray_Computing_in_the_21st_Century_2006.jpg)](./File:Jim_Gray_Computing_in_the_21st_Century_2006.jpg)**Jim Gray** 

The concept of Commit originated in the late 1960s and early 1970s, when computer technology was rapidly advancing and data management was becoming an important requirement in business and finance. Enterprises have gradually replaced the traditional paper records with computers, which has fully improved the work efficiency. The reliability and consistency of data have become a necessary requirement. [Transaction management](./Transaction_management) at this stage is relatively simple, limited to using a single computer for processing. It merely effectively records the changes in data to ensure that the data remains stable after the transaction is completed or terminated. In the late 1970s, as database systems moved from a single calculator operation to multiple distributed collaborations, ensuring data consistency and reliability became a new challenge. In 1978, computer scientist Jim Gray proposed the famous two-phase Commit Protocol (2PC), which became an effective solution for distributed transaction management, successfully managing data synchronization problems between multiple nodes.[[1]](./Commit_(data_management)#cite_note-:0-1) However, this commit protocol has some potential transaction blocking problems when nodes fail.

 

In the early 1980s, researchers discovered that although the two-step commit protocol was effective at synchronizing data, there could be long waits and even system crashes, with limitations. To improve this problem, people have begun to explore new and effective methods, including enhancing efficiency by reducing message communication during the protocol process. IBM's R* database introduced the Assumed Commit and Assumed abort protocols, which contributed significantly to transaction management efficiency.[[2]](./Commit_(data_management)#cite_note-:1-2) These two protocols have greatly improved the processing efficiency of distributed transactions by reducing [communication](./Communication) overhead and have become an important breakthrough in the technology of transaction commit protocols.

 

By the early 1990s, with the increase in business demands and the complexity of transactions, enterprises required higher efficiency in distributed transaction processing. In order to adapt to the needs of different environments, the scientific community has gradually developed various variants of commit protocols to provide more flexible transaction management options for different needs.[[3]](./Commit_(data_management)#cite_note-:2-3) For example, the three-phase commit protocol promotes the commit of transactions more effectively and reduces the occurrence of blocking problems by adding a pre-commit protocol and a timeout mechanism.

 

In the 21st century, with the popularization of mobile Internet and wireless technology, the commit protocol has been further developed, and researchers have begun to pay attention to how to reduce the blocking in the transaction process to solve the problem of broadband limitation, battery life and network instability in the mobile environment. The proposal of optimistic commit protocol marks the extension of commit technology from traditional database to the emerging mobile data field.[[4]](./Commit_(data_management)#cite_note-:3-4) This protocol allows transactions to temporarily use unconfirmed data, improving the user experience in cases of poor network conditions.

 

In recent years, with the rise of blockchain and decentralized technologies, submission protocols and consensus mechanisms have gradually merged.[[5]](./Commit_(data_management)#cite_note-5) These consensus algorithms play a role in tamper-proofing and preventing malicious attacks on node pairs in a decentralized environment. This enables commit to no longer be confined to the scope of traditional database management, but to become the core technology of trust computing and distributed ledgers, further expanding the application field of commit in the [digital age](./Digital_age). This integration has brought about extensive application impacts. Each transaction can achieve the effect of tracking global submissions through the verification of the consensus mechanism, becoming an important technical foundation for promoting the circulation of digital assets, the operation of cryptocurrencies and decentralized applications.

 

## Commit Protocol Types

 

In the world of data management, a transaction is a series of database operations, such as [bank transfers](./Bank_transfer) and order submission. In order to ensure the accuracy, consistency, and security of the data, transactions are usually completed completely, or cancelled completely, leaving no partially completed results.[[6]](./Commit_(data_management)#cite_note-:4-6) Commit protocol is the method used to coordinate this process. Different protocols are applicable to different submission scenarios and have their own advantages and disadvantages. There are four major commit protocols.

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/d/d2/Two-Phase_Commit_Protocol.png/250px-Two-Phase_Commit_Protocol.png)](./File:Two-Phase_Commit_Protocol.png)Two-Phase Commit Protocol 

### Two-Phase Commit (2PC)

 

The two-phase commit protocol is the most classic and broadest approach to distributed transactions, which includes both a preparation phase and a commit phase.[[1]](./Commit_(data_management)#cite_note-:0-1) This commit protocol is designed to allow the database coordinator to determine if all participating nodes agree. The preparation phase is the phase in which the coordination node sends a ready to commit request to all nodes participating in the transaction. The commit phase is a global commit after all participating nodes are ready, and if no agreement is reached, all nodes [roll back](./Rollback_(data_management)) the transaction and undo all previous operations.

 

Although the two-phase commit protocol is the easiest to operate and widely used, its obvious drawback is that it can cause transactions to be blocked for a long time when nodes fail, resulting in a decline in system performance and making it difficult to terminate or continue immediately.

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/f/fa/Three-Phase_Commit_Protoco.png/250px-Three-Phase_Commit_Protoco.png)](./File:Three-Phase_Commit_Protoco.png)Three-Phase Commit Protocol 

### Three-Phase Commit (3PC)

 

The three-phase commit protocol is an improved non-blocking protocol based on 2PC, which is divided into three stages: preparation, pre-commit and commit. Firstly, each node sends a "preparation" request. After confirmation, a "pre-submission" stage is added. At this point, each node has completed most of the preparatory work and is waiting for the final confirmation. Finally, in the formal commit stage, after all nodes send the "commit" request, the transaction is completed and committed. Compared with 2PC, it increases the timeout mechanism, avoids the [blocking](./Blocking_(computing)) problem caused by single point of failure, and improves the reliability of the system.[[3]](./Commit_(data_management)#cite_note-:2-3)

 

The three-phase commit protocol significantly optimizes transaction reliability, but adds additional [overhead](./Overhead_(computing)) for message transmission and state maintenance. It is more suitable for distributed application scenarios with high transaction sensitivity and no acceptance of long waiting times.

 

### Presumed Commit (PC) and Presumed Abort (PA)

 

Presumed Commit (PC) is the default that the transaction will be committed successfully and rollback will be notified unless an anomaly is encountered. This commit reduces the message overhead and logging costs of a normal commits. Presumed Abort (PA) is assumed that the [default state](./Default_state_network) of the transaction is a rollback and will only be committed when all nodes have explicitly agreed.[[2]](./Commit_(data_management)#cite_note-:1-2) This commit is applicable to transactions that are not updated frequently or have a low probability of successful commit. The IBM R* Distributed Database management System was the first to propose and practice the PC and PA protocols, handling distributed transaction management very efficiently and becoming a classic case in the field of database transaction management.[[2]](./Commit_(data_management)#cite_note-:1-2)

 

### Optimistic Commit Protocol

 

With the rise of the Internet, the previous commit protocols are facing new challenges, especially in mobile scenarios with unstable networks. Excessively long transaction waiting times can affect the user experience. The Optimistic Commit Protocol allows a transaction to temporarily access uncommitted data before committing to avoid wait times.[[7]](./Commit_(data_management)#cite_note-:5-7) This type of commit is suitable for high-contention environments, but if a transaction fails, additional compensatory transactions need to be executed to achieve semantic atomicity to ensure final data consistency.[[6]](./Commit_(data_management)#cite_note-:4-6) Once the compensation thing detects a transaction failure, it will promptly execute another special transaction and undo the previous temporary operation to restore the data to the consistent state before the transaction. The optimistic commit protocol developed by Levy et al. (1991) uses compensation transactions to solve the problem of indefinite waiting that traditional two-phase commit protocols may face, and improves the system performance.

 

## Failures and Recovery in Commit Protocols

 

Commit protocol is mainly used to ensure the consistency and integrity of data during transaction processing. However, in actual operation, node failure or abnormal shutdown is inevitable, which may cause data confusion and loss. Common failures include network outages, server failures or transaction operation conflicts.[[1]](./Commit_(data_management)#cite_note-:0-1) The following mechanisms can help the Commit protocol effectively deal with anomalies, maintain data consistency, and ensure that the transaction submission can be completed efficiently.

 

### Logging and Recovery

 

Logging is one of the important means of fault recovery. Each participating database node records every step of a transaction in real time, including transaction initiation, data update, commit, or transaction termination. These [records](./Record_(computer_science)) are called logs. When the system malfunctions or terminates abnormally, the data will become inconsistent and chaotic. At this time, logs play an important role. In this case, the database system can quickly recover to the consistent state before the fault by reading the logs recorded before the fault. This recovery method is divided into redo and undo. To make sure the updated material is saved correctly, the system uses a technique known as "redo" to re-execute the transaction steps that were documented in the log after a transaction has been verified as committed.[[2]](./Commit_(data_management)#cite_note-:1-2) The system uses a feature known as "undo" to make sure that all actions have been completely rolled back in the event that a transaction commit mistake occurs.[[2]](./Commit_(data_management)#cite_note-:1-2) Log recording is widely used in various mainstream database systems, including IBM's R* database, effectively ensuring the reliability of data.

 

### Compensating Transactions

 

In the Optimistic Commit Protocol, a transaction may use data before it is committed, which improves efficiency, but only if it is committed successfully. When a transaction eventually fails or aborts, the data that has been modified may be inconsistent. Therefore, the concept of compensating transactions is introduced.[[7]](./Commit_(data_management)#cite_note-:5-7)

 

The meaning of a compensated transaction is that when a transaction fails or terminates, the system does not cancel the transaction, but executes a special transaction to compensate or undo the operation done by the previous transaction, so that the data is restored consistently. For example, in e-commerce, if the original transaction is to create an order and deduct inventory, when this transaction fails, the compensation transaction will cancel the order and restore the inventory. Compensation transactions have independence and [persistence](./Persistence_(computer_science)), that is, they can be executed without relying on the original transaction and still maintain the final successful execution when the system crashes. This method effectively avoids the Cascading Aborts problem that may occur due to traditional transaction revocation. It is applicable to scenarios where instability frequently occurs in mobile networks and ensures the performance and stability of transaction processing.

 

### Timeout Mechanism

 

Commit protocols typically wait for confirmation from multiple nodes. If one of the nodes fails or the network fails, the entire transaction can stop for a long time, seriously affecting efficiency, a situation known as a blocking problem.

 

The timeout mechanism provides a solution to the blocking problem. A maximum timeout threshold will be set in this mechanism. When the transaction waiting time exceeds the preset time, the system automatically determines that the transaction fails, rolls back the transaction, and releases the occupied data resources, effectively preventing the entire system waiting time from being too long. The time-out mechanism is typically used by the three-phase Commit protocol (3PC), which effectively reduces the problem of long waiting time and blocking in distributed transactions and avoids the phenomenon of system resources being occupied for a long time.[[3]](./Commit_(data_management)#cite_note-:2-3) The timeout mechanism is usually carried out in combination with the status inquiry mechanism to detect whether the node is still active, increasing the fault tolerance of the system.

 

## Applications of Commit Protocols

 

Commit protocols are widely used in all areas of life and business. Although most users do not have direct contact with these technologies, they effectively ensure the accuracy and consistency of user data. Financial transaction payments, e-commerce transactions, flight and [hotel reservations](./Hotel_reservation_system), blockchain and currency transactions are some typical [application](./Application_software) scenarios of submission protocols.

 

### Banking and Financial Transactions

 

Transactions processed by the banking system typically need to generate money flows between multiple accounts, and each transaction must be very accurate, especially in cross-regional transfer and payment businesses. Any error in data or nodes will lead to a loss of funds. For example, when you transfer money to a friend via [mobile banking](./Mobile_banking), the bank's processing system is actually operating on multiple database servers at the same time to complete the transaction.

 

The commit protocol ensures that each [bank transfer](./Bank_transfer) will only be a complete success and a complete non-execution of the transfer. This mechanism maintains the rigor of banking operations and prevents the loss of funds or account data. The classic Two-phase Commit Protocol (2PC) is typically used in banking systems around the world and is recognized as a standard solution by banks and [financial systems](./Financial_system) to ensure the accuracy and reliability of transactions, especially in cross-border transfer transactions.[[1]](./Commit_(data_management)#cite_note-:0-1) Through this agreement, the bank can avoid differences in the [balance](./Balance_of_payments) of users' accounts and significantly reduce the risk of customers' property loss.

 

### E-commerce and Mobile Applications

 

With the rapid development of mobile Internet, commit protocols are widely used in [online shopping](./Online_shopping) and mobile payment scenarios. For example, when a user places an order to pay on the platform, the backend system needs to use a commit protocol to ensure that order information, inventory data, and payment amounts are always consistent and accurate.

 

However, [electronic devices](./Electronic_devices) often encounter network disconnections or instability, and optimistic commit protocols are widely used in this context. This protocol allows transactions to use short-term data first and then compensate for the changes made before the transaction is rolled back after verification fails. This method enables things to be successfully submitted even under poor network conditions, effectively reducing waiting time, ensuring the smooth progress of transactions, and significantly improving user experience and satisfaction.[[4]](./Commit_(data_management)#cite_note-:3-4)

 

### Airline and Hotel Reservations

 

Airlines and hotels need to ensure that the inventory data on multiple [servers](./Client–server_model) remains consistent when handling [reservations](./Computer_reservation_system). Once the data is not synchronized in [real time](./Real-time_computing), problems such as [overselling](./Overselling) and duplicate reservations will occur. For example, when passengers book flights, the system must ensure that the number of remaining seats is updated in real time on all platforms.

 

The thing submission protocol avoids the overselling problem caused by data desynchronization by simultaneously controlling the data information on multiple servers. IBM 's R* database management system uses the Presumed Commit protocol to handle such booking services efficiently, ensuring the accuracy and efficiency of customer booking.[[2]](./Commit_(data_management)#cite_note-:1-2)

 

### Blockchain and Cryptocurrencies

 

In recent years, the rise of blockchain technology has made the commit protocol have a new application scenario. Blockchain is essentially a decentralized data management system that allows transactions and data updates to achieve data consistency through consensus among multiple decentralized nodes.

 

Commit protocol, combined with the Consensus Mechanism in the blockchain, provides the necessary [data security](./Data_security) for decentralized applications such as [cryptocurrency](./Cryptocurrency) transactions and [Smart Contracts](./Smart_contract).[[8]](./Commit_(data_management)#cite_note-8) In addition, this combination ensures that the results of transaction execution in the blockchain network are consistent across all nodes, thus becoming an essential [infrastructure](./Infrastructure_as_code) for the [digital economy](./Digital_economy).[[6]](./Commit_(data_management)#cite_note-:4-6) For example, the special commit protocol adopted by the [Hyperledger Fabric](./Hyperledger) platform directly emphyses the consensus mechanism into the transaction verification process to enhance the robustness against malicious nodes and network partitions.[[6]](./Commit_(data_management)#cite_note-:4-6)

 

## See also

 
- [Atomic commit](./Atomic_commit)
- [Two-phase commit protocol](./Two-phase_commit_protocol)
- [Three-phase commit protocol](./Three-phase_commit_protocol)

 

## References

  
1. [1](./Commit_(data_management)#cite_ref-:0_1-0) [2](./Commit_(data_management)#cite_ref-:0_1-1) [3](./Commit_(data_management)#cite_ref-:0_1-2) [4](./Commit_(data_management)#cite_ref-:0_1-3) ["Transaction Management in Distributed Database Systems"](http://www.springerreference.com/index/doi/10.1007/springerreference_65982), *SpringerReference*, Berlin/Heidelberg: Springer-Verlag, 2011, [doi](./Doi_(identifier)):[10.1007/springerreference_65982](https://doi.org/10.1007%2Fspringerreference_65982) (inactive 1 July 2025), retrieved 2025-05-29`{{citation}}`:  CS1 maint: DOI inactive as of July 2025 ([link](./Category:CS1_maint:_DOI_inactive_as_of_July_2025))
2. [1](./Commit_(data_management)#cite_ref-:1_2-0) [2](./Commit_(data_management)#cite_ref-:1_2-1) [3](./Commit_(data_management)#cite_ref-:1_2-2) [4](./Commit_(data_management)#cite_ref-:1_2-3) [5](./Commit_(data_management)#cite_ref-:1_2-4) [6](./Commit_(data_management)#cite_ref-:1_2-5) Mohan, C.; Lindsay, B.; Obermarck, R. (December 1986). ["Transaction management in the R* distributed database management system"](https://doi.org/10.1145/7239.7266). *ACM Transactions on Database Systems*. **11** (4): 378–396. [doi](./Doi_(identifier)):[10.1145/7239.7266](https://doi.org/10.1145%2F7239.7266). [ISSN](./ISSN_(identifier)) [0362-5915](https://search.worldcat.org/issn/0362-5915).
3. [1](./Commit_(data_management)#cite_ref-:2_3-0) [2](./Commit_(data_management)#cite_ref-:2_3-1) [3](./Commit_(data_management)#cite_ref-:2_3-2) Gupta, Ramesh; Haritsa, Jayant; Ramamritham, Krithi (1997). ["Revisiting commit processing in distributed database systems"](https://doi.org/10.1145/253260.253366). *Proceedings of the 1997 ACM SIGMOD international conference on Management of data - SIGMOD '97*. New York, New York, USA: ACM Press. pp. 486–497. [doi](./Doi_(identifier)):[10.1145/253260.253366](https://doi.org/10.1145%2F253260.253366). [ISBN](./ISBN_(identifier)) [0-89791-911-4](./Special:BookSources/0-89791-911-4).
4. [1](./Commit_(data_management)#cite_ref-:3_4-0) [2](./Commit_(data_management)#cite_ref-:3_4-1) Abdul Moiz, Salman; Rajamani, Lakshmi; N.Pal, Supriya (2010-08-31). ["Commit Protocols in Mobile Environments: Design & Implementation"](https://doi.org/10.5121/ijdms.2010.2310). *International Journal of Database Management Systems*. **2** (3): 116–126. [doi](./Doi_(identifier)):[10.5121/ijdms.2010.2310](https://doi.org/10.5121%2Fijdms.2010.2310). [ISSN](./ISSN_(identifier)) [0975-5985](https://search.worldcat.org/issn/0975-5985).
5. [↑](./Commit_(data_management)#cite_ref-5) Veijalainen, J.; Wolski, A. (1992). ["Prepare and commit certification for decentralized transaction management in rigorous heterogeneous multidatabases"](https://doi.org/10.1109/icde.1992.213162). *[1992] Eighth International Conference on Data Engineering*. IEEE Comput. Soc. Press. pp. 470–479. [doi](./Doi_(identifier)):[10.1109/icde.1992.213162](https://doi.org/10.1109%2Ficde.1992.213162). [ISBN](./ISBN_(identifier)) [0-8186-2545-7](./Special:BookSources/0-8186-2545-7).
6. [1](./Commit_(data_management)#cite_ref-:4_6-0) [2](./Commit_(data_management)#cite_ref-:4_6-1) [3](./Commit_(data_management)#cite_ref-:4_6-2) [4](./Commit_(data_management)#cite_ref-:4_6-3) Gupta, Ramesh; Haritsa, Jayant; Ramamritham, Krithi (June 1997). ["Revisiting commit processing in distributed database systems"](https://doi.org/10.1145/253262.253366). *ACM SIGMOD Record*. **26** (2): 486–497. [doi](./Doi_(identifier)):[10.1145/253262.253366](https://doi.org/10.1145%2F253262.253366). [ISSN](./ISSN_(identifier)) [0163-5808](https://search.worldcat.org/issn/0163-5808).
7. [1](./Commit_(data_management)#cite_ref-:5_7-0) [2](./Commit_(data_management)#cite_ref-:5_7-1) Levy, Eliezer; Korth, Henry F.; Silberschatz, Abraham (April 1991). ["An optimistic commit protocol for distributed transaction management"](https://doi.org/10.1145/119995.115800). *ACM SIGMOD Record*. **20** (2): 88–97. [doi](./Doi_(identifier)):[10.1145/119995.115800](https://doi.org/10.1145%2F119995.115800). [ISSN](./ISSN_(identifier)) [0163-5808](https://search.worldcat.org/issn/0163-5808).
8. [↑](./Commit_(data_management)#cite_ref-8) Nawab, Faisal; Sadoghi, Mohammad (2023). ["Consensus in Data Management: From Distributed Commit to Blockchain"](https://doi.org/10.1561/1900000075). *Foundations and Trends in Databases*. **12** (4): 221–364. [doi](./Doi_(identifier)):[10.1561/1900000075](https://doi.org/10.1561%2F1900000075). [ISSN](./ISSN_(identifier)) [1931-7883](https://search.worldcat.org/issn/1931-7883).

 
| vteDatabase management systems |
| --- |
| Types | Object-orientedcomparisonRelationallistcomparisonKey–valueColumn-orientedlistDocument-orientedWide-column storeGraphNoSQLNewSQLIn-memorylistMulti-modelcomparisonCloudBlockchain-based database |
| Concepts | DatabaseACIDArmstrong's axiomsCodd's 12 rulesCAP theoremCRUDNullCandidate keyForeign keyPACELC design principleSuperkeySurrogate keyUnique key |
| Objects | RelationtablecolumnrowViewTransactionTransaction logTriggerIndexStored procedureCursorPartition |
| Components | Concurrency controlData dictionaryJDBCXQJODBCQuery languageQuery optimizerQuery rewriting systemQuery plan |
| Functions | AdministrationQuery optimizationReplicationSharding |
| Related topics | Database modelsDatabase normalizationDatabase storageDistributed databaseFederated database systemReferential integrityRelational algebraRelational calculusRelational modelObject–relational databaseTransaction processingList of SQL software and tools |
| CategoryOutline |