---
source: https://en.wikipedia.org/wiki/Quorum_(distributed_computing)
fetched: 2026-06-19
---

Minimum number of votes that a distributed transaction has to obtain 

A **quorum** is the minimum number of votes that a [distributed transaction](./Distributed_transaction) has to obtain in order to be allowed to perform an operation in a [distributed system](./Distributed_system). A **quorum**-based technique is implemented to enforce consistent operation in a distributed system.

 

## Quorum-based techniques in distributed database systems

 

Quorum-based voting can be used as a [replica](./Replication_(computer_science)#Database_replication) control method,[[1]](./Quorum_(distributed_computing)#cite_note-ozsu-1)
as well as a commit method to ensure [transaction](./Database_transaction) [atomicity](./Atomicity_(database_systems)) in the presence of [network partitioning](./Network_partitioning).[[1]](./Quorum_(distributed_computing)#cite_note-ozsu-1)

 

### Quorum-based voting in commit protocols

 

In a [distributed database](./Distributed_database) system, a transaction could execute its operations at multiple sites. Since atomicity requires every distributed transaction to be atomic, the transaction must have the same fate ([commit](./Commit_(data_management)) or [abort](./Rollback_(data_management))) at every site. In case of [network partitioning](./Network_partitioning), sites are partitioned and the partitions may not be able to communicate with each other. This is where a quorum-based technique comes in. The fundamental idea is that a transaction is executed if the majority of sites vote to execute it.

 

Every site in the system is assigned a vote Vi. Let us assume that the total number of votes in the system is V and the abort and commit quorums are Va and Vc, respectively. Then the following rules must be obeyed in the implementation of the commit protocol:

 
1. Va + Vc > V, where 0 < Vc, Va     ≤ ≤    {\displaystyle \leq }  ![{\displaystyle \leq }](https://wikimedia.org/api/rest_v1/media/math/render/svg/440568a09c3bfdf0e1278bfa79eb137c04e94035) V.
2. Before a transaction commits, it must obtain a commit quorum Vc.
The total of at least one site that is prepared to commit and zero or more sites waiting     ≥ ≥    {\displaystyle \geq }  ![{\displaystyle \geq }](https://wikimedia.org/api/rest_v1/media/math/render/svg/bcef7c0e95bb77a35fd1a874ca91f425215f3c26) Vc.[[2]](./Quorum_(distributed_computing)#cite_note-2)
3. Before a transaction aborts, it must obtain an abort quorum Va
The total of zero or more sites that are prepared to abort or any sites waiting     ≥ ≥    {\displaystyle \geq }  ![{\displaystyle \geq }](https://wikimedia.org/api/rest_v1/media/math/render/svg/bcef7c0e95bb77a35fd1a874ca91f425215f3c26) Va.

 

The first rule ensures that a transaction cannot be committed and aborted at the same time. The next two rules indicate the votes that a transaction has to obtain before it can terminate one way or the other.

 

### Quorum-based voting for replica control

 

In replicated databases, a data object has copies present at several sites. To ensure [serializability](./Serializability), no two transactions should be allowed to read or write a data item concurrently. In case of replicated databases, a quorum-based replica control protocol can be used to ensure that no two copies of a data item are read or written by two transactions concurrently.

 

The quorum-based voting for replica control is due to [Gifford, 1979].[[3]](./Quorum_(distributed_computing)#cite_note-3)
Each copy of a replicated data item is assigned a vote. Each operation then has to obtain a *read quorum* (Vr) or a *write quorum* (Vw) to read or write a data item, respectively. If a given data item has a total of V votes, the quorums have to obey the following rules:

 
1. Vr + Vw > V
2. Vw > V/2

 

The first rule ensures that a data item is not read and written by two transactions concurrently. Additionally, it ensures that a read quorum contains at least one site with the newest version of the data item. The second rule ensures that two write operations from two transactions cannot occur concurrently on the same data item. The two rules ensure that one-copy serializability is maintained.

 

## See also

 
- [CAP theorem](./CAP_theorem)
- [Database transaction](./Database_transaction)
- [Replication (computer science)](./Replication_(computer_science))
- [Atomicity (database systems)](./Atomicity_(database_systems))

 

## References

 
1. [1](./Quorum_(distributed_computing)#cite_ref-ozsu_1-0) [2](./Quorum_(distributed_computing)#cite_ref-ozsu_1-1)  Ozsu, Tamer M; Valduriez, Patrick (1991). "12". *Principles of distributed database systems* (2nd ed.). Upper Saddle River, NJ: Prentice-Hall, Inc. [ISBN](./ISBN_(identifier)) [978-0-13-691643-7](./Special:BookSources/978-0-13-691643-7).
2. [↑](./Quorum_(distributed_computing)#cite_ref-2) Skeen, Dale. ["A Quorum-based Commit Protocol"](https://ecommons.cornell.edu/bitstream/handle/1813/6323/82-483.pdf?sequence=1) (PDF). Cornell University ECommons Library. Retrieved 10 February 2013.
3. [↑](./Quorum_(distributed_computing)#cite_ref-3)  Gifford, David K. (1979). *Weighted voting for replicated data*. SOSP '79: Proceedings of the seventh ACM symposium on Operating systems principles. Pacific Grove, California, United States: ACM. pp. 150–162. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.12.6256](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.12.6256). [doi](./Doi_(identifier)):[10.1145/800215.806583](https://doi.org/10.1145%2F800215.806583).

  categories