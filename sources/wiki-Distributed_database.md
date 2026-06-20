---
source: https://en.wikipedia.org/wiki/Distributed_database
fetched: 2026-06-19
---

Database whose data is stored in different physical locations 
|  | This article has multiple issues.Please helpimprove itor discuss these issues on thetalk page.(Learn how and when to remove these messages)This articleneeds additional citations forverification.Please helpimprove this articlebyadding citations to reliable sources. Unsourced material may be challenged and removed.Find sources:"Distributed database"–news·newspapers·books·scholar·JSTOR(August 2010)(Learn how and when to remove this message)This article includes a list ofgeneral references, butit lacks sufficient correspondinginline citations.Please help toimprovethis article byintroducingmore precise citations.(April 2013)(Learn how and when to remove this message)(Learn how and when to remove this message) |  | This articleneeds additional citations forverification.Please helpimprove this articlebyadding citations to reliable sources. Unsourced material may be challenged and removed.Find sources:"Distributed database"–news·newspapers·books·scholar·JSTOR(August 2010)(Learn how and when to remove this message) |  | This article includes a list ofgeneral references, butit lacks sufficient correspondinginline citations.Please help toimprovethis article byintroducingmore precise citations.(April 2013)(Learn how and when to remove this message) |
| --- | --- | --- | --- | --- | --- |
|  | This articleneeds additional citations forverification.Please helpimprove this articlebyadding citations to reliable sources. Unsourced material may be challenged and removed.Find sources:"Distributed database"–news·newspapers·books·scholar·JSTOR(August 2010)(Learn how and when to remove this message) |
|  | This article includes a list ofgeneral references, butit lacks sufficient correspondinginline citations.Please help toimprovethis article byintroducingmore precise citations.(April 2013)(Learn how and when to remove this message) |

 

A **distributed database** is a [database](./Database) in which data is stored across different physical locations.[[1]](./Distributed_database#cite_note-1) It may be stored in multiple [computers](./Computers) located in the same physical location (e.g. a data centre); or maybe dispersed over a [network](./Computer_network) of interconnected computers. Unlike [parallel systems](./Parallel_computing), in which the processors are tightly coupled and constitute a single database system, a distributed database system consists of loosely coupled sites that share no physical components.

 

System administrators can distribute collections of data (e.g. in a database) across multiple physical locations. A distributed database can reside on organised [network servers](./Network_servers) or [decentralised independent computers](./Blockchain_(database)) on the [Internet](./Internet), on corporate [intranets](./Intranets) or [extranets](./Extranets), or on other organisation [networks](./Computer_network). Because distributed databases store data across multiple computers, distributed databases may improve performance at [end-user](./End-user) worksites by allowing transactions to be processed on many machines, instead of being limited to one.[[2]](./Distributed_database#cite_note-O'Brien-2)

 

Two processes ensure that the distributed databases remain up-to-date and current: [replication](./Replication_(computing))[[3]](./Distributed_database#cite_note-3) and [duplication](./Data_transmission).

 
1. Replication involves using specialized software that looks for changes in the distributive database. Once the changes have been identified, the replication process makes all the databases look the same. The replication process can be complex and time-consuming, depending on the size and number of the distributed databases. This process can also require much time and computer resources.
2. Duplication, on the other hand, has less complexity. It identifies one database as a [master](./Master/slave_(technology)) and then duplicates that database. The duplication process is normally done at a set time after hours. This is to ensure that each distributed location has the same data.  In the duplication process, users may change only the master database. This ensures that local data will not be overwritten.

 

Both replication and duplication can keep the data current in all distributive locations.[[2]](./Distributed_database#cite_note-O'Brien-2)

 

Besides distributed database replication and [fragmentation](./Fragmentation_(computing)), there are many other distributed database design technologies. For example, local autonomy, synchronous, and asynchronous distributed database technologies. The implementation of these technologies can and do depend on the needs of the business and the sensitivity/[confidentiality](./Confidentiality) of the data stored in the database and the price the business is willing to spend on ensuring [data security](./Data_security), [consistency](./Data_consistency) and [integrity](./Data_integrity).

 

When discussing access to distributed databases, [Microsoft](./Microsoft) favors the term **distributed query**, which it defines in protocol-specific manner as "[a]ny SELECT, INSERT, UPDATE, or DELETE statement that references tables and rowsets from one or more external OLE DB data sources."[[4]](./Distributed_database#cite_note-4) [Oracle](./Oracle_Database) provides a more language-centric view in which distributed queries and [distributed transactions](./Distributed_transaction) form part of **distributed SQL**.[[5]](./Distributed_database#cite_note-5)

 

## Architecture

 

There are 3 main architecture types for distributed databases:

 
- [Shared-memory](./Shared-memory_architecture): very rarely used[[6]](./Distributed_database#cite_note-:0-6)
- [Shared-disk](./Shared-disk_architecture)
- [Shared-nothing](./Shared-nothing_architecture)

 

In the shared-memory and shared-disk architectures, the data is not [partitioned](./Partition_(database)), but it has to be in a shared-nothing architecture.

 

Shared-disk architecture is more common for [cloud databases](./Cloud_database) than for on-premise.[[6]](./Distributed_database#cite_note-:0-6)

 

Historically, shared-nothing was the first architecture to be implemented on the cloud, before the advent of shared cloud storage made shared-disk possible.

 

In practice, different layers of the database can have different architectures. It is now common to have a compute layer with a shared nothing architecture, and a storage layer with a shared disk architecture. This is for instance the case of [Snowflake](./Snowflake_Inc.)[[7]](./Distributed_database#cite_note-7) and [AWS Aurora](./Amazon_Aurora).[[8]](./Distributed_database#cite_note-8)

 

### List of shared-nothing databases

 
- [IBM Db2](./IBM_Db2)
- [Greenplum](./Greenplum)
- [MongoDB](./MongoDB)
- [Netezza](./Netezza)
- [Teradata](./Teradata)
- [TiDB](./TiDB)
- [OceanBase](https://en.oceanbase.com/)
- [Vertica](./Vertica)

 

### List of shared-disk databases

 
- [AWS Aurora](./Amazon_Aurora)
- Neon
- [Snowflake](./Snowflake_Inc.)

 

## See also

 
- [Centralized database](./Centralized_database)
- [Data grid](./Data_grid)
- [Distributed cache](./Distributed_cache)
- [Distributed data store](./Distributed_data_store)
- [Distributed hash table](./Distributed_hash_table)
- [Routing protocol](./Routing_protocol)
- [Distributed SQL](./Distributed_SQL)

 

## References

 
1. [↑](./Distributed_database#cite_ref-1) ["Definition: distributed database"](http://www.its.bldrdoc.gov/fs-1037/dir-012/_1750.htm). *www.its.bldrdoc.gov*.
2. [1](./Distributed_database#cite_ref-O'Brien_2-0) [2](./Distributed_database#cite_ref-O'Brien_2-1) 
O'Brien, J. & Marakas, G.M.(2008) Management Information Systems (pp. 185-189). New York, NY: McGraw-Hill Irwin
3. [↑](./Distributed_database#cite_ref-3) Ozsu, M.T.; Valduriez, P. (1991). "Distributed database systems: where are we now?". *Computer*. **24** (8): 68–78. [doi](./Doi_(identifier)):[10.1109/2.84879](https://doi.org/10.1109%2F2.84879). [ISSN](./ISSN_(identifier)) [1558-0814](https://search.worldcat.org/issn/1558-0814). [S2CID](./S2CID_(identifier)) [5898169](https://api.semanticscholar.org/CorpusID:5898169).
4. [↑](./Distributed_database#cite_ref-4)  ["TechNet Glossary"](https://technet.microsoft.com/en-us/library/cc966484.aspx). Microsoft. 28 January 2010. Retrieved 2013-07-16. distributed query[:] Any SELECT, INSERT, UPDATE, or DELETE statement that references tables and rowsets from one or more external OLE DB data sources. 
5. [↑](./Distributed_database#cite_ref-5)  Ashdown, Lance; Kyte, Tom (September 2011). ["Oracle Database Concepts, 11g Release 2 (11.2)"](https://web.archive.org/web/20130715001716/http://docs.oracle.com/cd/E11882_01/server.112/e25789/toc.htm). Oracle Corporation. Archived from [the original](http://docs.oracle.com/cd/E11882_01/server.112/e25789/toc.htm) on 2013-07-15. Retrieved 2013-07-17. Distributed SQL synchronously accesses and updates data distributed among multiple databases. [...] Distributed SQL includes distributed queries and distributed transactions. 
6. [1](./Distributed_database#cite_ref-:0_6-0) [2](./Distributed_database#cite_ref-:0_6-1) Garrod, Charlie (2023). ["Lecture #21: Introduction to Distributed Databases"](https://15445.courses.cs.cmu.edu/spring2023/notes/21-distributed.pdf) (PDF). *Carnegie Mellon University - School of Computer Science*. Retrieved 2023-03-12.
7. [↑](./Distributed_database#cite_ref-7) Kaushik, Arun (2020-02-14). ["What Makes Snowflake So Powerful — It's the Hybrid of Shared Disk and Shared Nothing Architecture"](https://medium.com/@a.kaushik5587/what-makes-snowflake-so-powerful-its-the-hybrid-of-shared-disk-and-shared-nothing-architecture-5b4fa8f039fa). *Medium*. Retrieved 2024-03-12.
8. [↑](./Distributed_database#cite_ref-8) Brahmadesam, Murali; Ternstrom, Tobias (2019). ["Amazon Aurora storage demystified: How it all works"](https://d1.awsstatic.com/events/reinvent/2019/REPEAT_Amazon_Aurora_storage_demystified_How_it_all_works_DAT309-R.pdf) (PDF). Retrieved 2024-03-12.

 

## Further reading

 
- M. T. Özsu and P. Valduriez, *Principles of Distributed Databases* (3rd edition) (2011), Springer, [ISBN](./ISBN_(identifier)) [978-1-4419-8833-1](./Special:BookSources/978-1-4419-8833-1)
- Elmasri and Navathe, *Fundamentals of database systems* (3rd edition), Addison-Wesley Longman, [ISBN](./ISBN_(identifier)) [0-201-54263-3](./Special:BookSources/0-201-54263-3)
- *Oracle Database Administrator's Guide 10g* (Release 1), [http://docs.oracle.com/cd/B14117_01/server.101/b10739/ds_concepts.htm](http://docs.oracle.com/cd/B14117_01/server.101/b10739/ds_concepts.htm)

 
| vteDatabase management systems |
| --- |
| Types | Object-orientedcomparisonRelationallistcomparisonKey–valueColumn-orientedlistDocument-orientedWide-column storeGraphNoSQLNewSQLIn-memorylistMulti-modelcomparisonCloudBlockchain-based database |
| Concepts | DatabaseACIDArmstrong's axiomsCodd's 12 rulesCAP theoremCRUDNullCandidate keyForeign keyPACELC design principleSuperkeySurrogate keyUnique key |
| Objects | RelationtablecolumnrowViewTransactionTransaction logTriggerIndexStored procedureCursorPartition |
| Components | Concurrency controlData dictionaryJDBCXQJODBCQuery languageQuery optimizerQuery rewriting systemQuery plan |
| Functions | AdministrationQuery optimizationReplicationSharding |
| Related topics | Database modelsDatabase normalizationDatabase storageDistributed databaseFederated database systemReferential integrityRelational algebraRelational calculusRelational modelObject–relational databaseTransaction processingList of SQL software and tools |
| CategoryOutline |

 
| Authority control databases |
| --- |
| National | United StatesFranceBnF dataIsrael |
| Other | Yale LUX |