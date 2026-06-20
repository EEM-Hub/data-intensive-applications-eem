---
source: https://en.wikipedia.org/wiki/NoSQL
fetched: 2026-06-19
---

Database class for storage and retrieval of modeled data "Structured storage" redirects here. For the Microsoft technology, see [COM Structured Storage](./COM_Structured_Storage). 

 

**NoSQL** (a colloquial title that became formal, meaning "not only [SQL](./SQL)" or "non-relational")[[1]](./NoSQL#cite_note-1) refers to a type of [database](./Database) design that stores and retrieves data differently from the traditional table-based structure of [relational databases](./Relational_database). Unlike relational databases, which organize data into rows and columns like a spreadsheet, NoSQL databases use a single data structure—such as [key–value pairs](./Key-value_database), [wide columns](./Wide-column_store), [graphs](./Graph_database), or [documents](./Document-oriented_database)—to hold information. Since this non-relational design does not require a fixed [schema](./Database_schema), it scales easily to manage large, often [unstructured datasets](./Unstructured_data).[[2]](./NoSQL#cite_note-2) NoSQL systems are sometimes called *"Not only SQL"* because they can support [SQL](./SQL)-like query languages or work alongside SQL databases in [polyglot-persistent](./Polyglot_persistence) setups, where multiple database types are combined.[[3]](./NoSQL#cite_note-3)[[4]](./NoSQL#cite_note-4) Non-relational databases date back to the late 1960s, but the term "NoSQL" emerged in the early 2000s, spurred by the needs of [Web 2.0](./Web_2.0) companies like social media platforms.[[5]](./NoSQL#cite_note-5)[[6]](./NoSQL#cite_note-6)

 

NoSQL databases are popular in [big data](./Big_data) and [real-time web](./Real-time_web) applications due to their simple design, ability to scale across [clusters of machines](./Cluster_computing) (called [horizontal scaling](./Horizontal_scaling#Horizontal_(scale_out)_and_vertical_scaling_(scale_up))), and precise control over data [availability](./Availability).[[7]](./NoSQL#cite_note-leavitt6-7)[[8]](./NoSQL#cite_note-8) These structures can speed up certain tasks and are often considered more adaptable than fixed database tables.[[9]](./NoSQL#cite_note-9) However, many NoSQL systems prioritize speed and availability over strict consistency (per the [CAP theorem](./CAP_theorem)), using [eventual consistency](./Eventual_consistency)—where updates reach all nodes eventually, typically within milliseconds, but may cause brief delays in accessing the latest data, known as [stale reads](https://en.wiktionary.org/wiki/stale%20read).[[10]](./NoSQL#cite_note-10) While most lack full [ACID](./ACID) transaction support, some, like [MongoDB](./MongoDB), include it as a key feature.[[11]](./NoSQL#cite_note-11)

 

## Barriers to adoption

 

Barriers to wider NoSQL adoption include their use of low-level [query languages](./Query_language) instead of SQL, inability to perform ad hoc [joins](./Join_(SQL)) across tables, lack of standardized interfaces, and significant investments already made in relational databases.[[12]](./NoSQL#cite_note-12) Some NoSQL systems risk [losing data](./Data_loss) through lost writes or other forms, though features like [write-ahead logging](./Write-ahead_logging)—a method to record changes before they’re applied—can help prevent this.[[13]](./NoSQL#cite_note-13)[[14]](./NoSQL#cite_note-14) For [distributed transaction processing](./Distributed_transaction_processing) across multiple databases, keeping data consistent is a challenge for both NoSQL and relational systems, as relational databases cannot enforce rules linking separate databases, and few systems support both [ACID](./ACID) transactions and [X/Open XA](./X/Open_XA) standards for managing distributed updates.[[15]](./NoSQL#cite_note-15)[[16]](./NoSQL#cite_note-16) Limitations within the interface environment are overcome using semantic virtualization protocols, such that NoSQL services are accessible to most [operating systems](./Operating_system).[[17]](./NoSQL#cite_note-17)

 

## History

 [![Last.fm Player](//upload.wikimedia.org/wikipedia/commons/thumb/b/b7/Last.fm_software_screenshot.png/250px-Last.fm_software_screenshot.png)](./File:Last.fm_software_screenshot.png)Last.fm Player 

The term *NoSQL* was used by [Carlo Strozzi](./Carlo_Strozzi) in 1998 to name his lightweight [Strozzi NoSQL open-source relational database](./Strozzi_NoSQL_(RDBMS)) that did not expose the standard [Structured Query Language](./SQL) (SQL) interface, but was still relational.[[18]](./NoSQL#cite_note-:0-18) His NoSQL [RDBMS](./Relational_database) is distinct from the around-2009 general concept of NoSQL databases.  Strozzi suggests that, because the current NoSQL movement "departs from the relational model altogether, it should therefore have been called more appropriately 'NoREL'",[[19]](./NoSQL#cite_note-19) referring to "not relational".

 

Johan Oskarsson, then a developer at [Last.fm](./Last.fm), reintroduced the term *NoSQL* in early 2009 when he organized an event to discuss "[open-source](./Open_source) [distributed, non-relational databases](./Distributed_database)".[[20]](./NoSQL#cite_note-20) The name attempted to label the emergence of an increasing number of non-relational, distributed data stores, including open source clones of Google's [Bigtable](./Bigtable)/[MapReduce](./MapReduce) and Amazon's [DynamoDB](./Amazon_DynamoDB).

 

## Types and examples

 

There are various ways to classify NoSQL databases, with different categories and subcategories, some of which overlap. What follows is a non-exhaustive classification by data model, with examples:[[21]](./NoSQL#cite_note-21)

 
| Type | Notable examples of this type |
| --- | --- |
| Key–value cache | Apache Ignite,Couchbase,Coherence,eXtreme Scale,Hazelcast,Infinispan,Memcached,Redis, Velocity |
| Key–value store | Azure Cosmos DB,ArangoDB,Amazon DynamoDB,Aerospike,Couchbase,ScyllaDB |
| Key–value store (eventually consistent) | Azure Cosmos DB,Oracle NoSQL Database,Riak,Voldemort |
| Key–value store (ordered) | FoundationDB,InfinityDB,LMDB,MemcacheDB |
| Tuple store | Apache River,GigaSpaces,Tarantool,TIBCOActiveSpaces,OpenLink Virtuoso |
| Triplestore | AllegroGraph,MarkLogic,Ontotext-OWLIM,Oracle NoSQL database, Profium Sense,Virtuoso Universal Server |
| Object database | Objectivity/DB,Perst,ZODB,db4o,GemStone/S,InterSystems Caché,JADE,ObjectDatabase++,ObjectDB,ObjectStore,ODABA,Realm,OpenLink Virtuoso,Versant Object Database,Indexed Database API |
| Document store | Azure Cosmos DB,ArangoDB,BaseX,Clusterpoint,Couchbase,CouchDB,DocumentDB,eXist-db,Google Cloud Firestore,IBM Domino,MarkLogic,MongoDB,RavenDB, Qizx,RethinkDB,Elasticsearch,OrientDB |
| Wide-column store | Azure Cosmos DB,Amazon DynamoDB,Bigtable,Cassandra,Google Cloud Datastore,HBase,Hypertable,ScyllaDB |
| Native multi-model database | ArangoDB,Azure Cosmos DB,OrientDB,MarkLogic,Apache Ignite,[22][23]Couchbase,FoundationDB,Oracle Database, AgensGraph |
| Graph database | Azure Cosmos DB,AllegroGraph,ArangoDB,Apache Giraph,GUN (Graph Universe Node),InfiniteGraph,MarkLogic,Neo4J,OrientDB,Virtuoso |
| Multivalue database | D3Pick database,Extensible Storage Engine(ESE/NT),InfinityDB,InterSystems Caché, jBASEPick database, mvBaseRocket Software, mvEnterpriseRocket Software,Northgate Information SolutionsReality (the original Pick/MV Database), OpenQM, Revelation Software's OpenInsight (Windows) and Advanced Revelation (DOS), UniDataRocket U2, UniVerseRocket U2 |

 

### Key–value store

 Main article: [Key–value database](./Key–value_database) 

Key–value (KV) stores use the [associative array](./Associative_array) (also called a map or dictionary) as their fundamental data model. In this model, data is represented as a collection of key–value pairs, such that each possible key appears at most once in the collection.[[24]](./NoSQL#cite_note-24)[[25]](./NoSQL#cite_note-25)

 

The key–value model is one of the simplest non-trivial data models, and richer data models are often implemented as an extension of it. The key–value model can be extended to a discretely ordered model that maintains keys in [lexicographic order](./Lexicographical_order). This extension is computationally powerful, in that it can efficiently retrieve selective key *ranges*.[[26]](./NoSQL#cite_note-26)

 

Key–value stores can use [consistency models](./Consistency_model) ranging from [eventual consistency](./Eventual_consistency) to [serializability](./Serializability). Some databases support ordering of keys. There are various hardware implementations, and some users store data in memory (RAM), while others on [solid-state drives](./Solid-state_drive) (SSD) or [rotating disks](./Hard_disk_drive) (aka hard disk drive (HDD)).

 

### Document store

 Main articles: [Document-oriented database](./Document-oriented_database) and [XML database](./XML_database) 

The central concept of a document store is that of a "document". While the details of this definition differ among document-oriented databases, they all assume that documents encapsulate and encode data (or information) in some standard formats or encodings. Encodings in use include [XML](./XML), [YAML](./YAML), and [JSON](./JSON) and [binary](./Binary_number) forms like [BSON](./BSON). Documents are addressed in the database via a unique *key* that represents that document. Another defining characteristic of a document-oriented database is an [API](./API) or query language to retrieve documents based on their contents.

 

Different implementations offer different ways of organizing and/or grouping documents:

 
- Collections
- Tags
- Non-visible [metadata](./Metadata)
- Directory hierarchies

 

Compared to relational databases, collections could be considered analogous to tables and documents analogous to records. But they are different – every record in a table has the same sequence of fields, while documents in a collection may have fields that are completely different.

 

### Graph

 Main article: [Graph database](./Graph_database) 

Graph databases are designed for data whose relations are well represented as a [graph](./Graph_(discrete_mathematics)) consisting of elements connected by a finite number of relations. Examples of data include [social relations](./Social_relation), public transport links, road maps, network topologies, etc.

 Graph databases and their query language 
| Name | Language(s) | Notes |
| --- | --- | --- |
| AgensGraph | Cypher | Multi-modelgraph database |
| AllegroGraph | SPARQL | RDFtriple store |
| Amazon Neptune | Gremlin,SPARQL | Graph database |
| ArangoDB | AQL,JavaScript,GraphQL | Multi-model DBMSDocument,Graph databaseandKey-value store |
| Azure Cosmos DB | Gremlin | Graph database |
| DEX/Sparksee | C++,Java,C#,Python | Graph database |
| FlockDB | Scala | Graph database |
| GUN (Graph Universe Node) | JavaScript | Graph database |
| IBM Db2 | SPARQL | RDFtriple store added in DB2 10 |
| InfiniteGraph | Java | Graph database |
| JanusGraph | Java | Graph database |
| MarkLogic | Java,JavaScript,SPARQL,XQuery | Multi-modeldocument databaseandRDFtriple store |
| Neo4j | Cypher | Graph database |
| OpenLink Virtuoso | C++,C#,Java,SPARQL | Middlewareanddatabase enginehybrid |
| Oracle | SPARQL 1.1 | RDFtriple store added in 11g |
| OrientDB | Java, SQL | Multi-modeldocumentandgraph database |
| OWLIM | Java,SPARQL 1.1 | RDFtriple store |
| Profium Sense | Java,SPARQL | RDFtriple store |
| RedisGraph | Cypher | Graph database |
| Sqrrl Enterprise | Java | Graph database |
| TerminusDB | JavaScript,Python,datalog | Open source RDF triple-store and document store[27] |

 

## Performance

 

The performance of NoSQL databases is usually evaluated using the metric of [throughput](./Throughput), which is measured as operations per second. Performance evaluation must pay attention to the right [benchmarks](./Benchmark_(computing)) such as production configurations, parameters of the databases, anticipated data volume, and concurrent user [workloads](./Workload).

 

Ben Scofield rated different categories of NoSQL databases as follows:[[28]](./NoSQL#cite_note-28)

 
| Data model | Performance | Scalability | Flexibility | Complexity | Data integrity | Functionality |
| --- | --- | --- | --- | --- | --- | --- |
| Key–value store | high | high | high | none | low | variable (none) |
| Column-oriented store | high | high | moderate | low | low | minimal |
| Document-oriented store | high | variable (high) | high | low | low | variable (low) |
| Graph database | variable | variable | high | high | low-med | graph theory |
| Relational database | variable | variable | low | moderate | high | relational algebra |

 

Performance and scalability comparisons are most commonly done using the [YCSB](./YCSB) benchmark.

 

## Handling relational data

 

Since most NoSQL databases lack ability for joins in queries, the [database schema](./Database_schema) generally needs to be designed differently. There are three main techniques for handling relational data in a NoSQL database. (See [table join and ACID support](./NoSQL#ACID_and_join_support) for NoSQL databases that support joins.)

 

### Multiple queries

 

Instead of retrieving all the data with one query, it is common to do several queries to get the desired data. NoSQL queries are often faster than traditional SQL queries, so the cost of additional queries may be acceptable. If an excessive number of queries would be necessary, one of the other two approaches is more appropriate.

 

### Caching, replication and non-normalized data

 

Instead of only storing foreign keys, it is common to store actual foreign values along with the model's data. For example, each blog comment might include the username in addition to a user id, thus providing easy access to the username without requiring another lookup. When a username changes, however, this will now need to be changed in many places in the database. Thus this approach works better when reads are much more common than writes.[[29]](./NoSQL#cite_note-DataModeling-Couchbase.com_November_11_2019c-29)

 

### Nesting data

 

With document databases like MongoDB it is common to put more data in a smaller number of collections. For example, in a blogging application, one might choose to store comments within the blog post document, so that with a single retrieval one gets all the comments. Thus in this approach a single document contains all the data needed for a specific task.

 

## ACID and join support

 

A database is marked as supporting [ACID](./ACID) properties (atomicity, consistency, isolation, durability) or [join](./Join_(SQL)) operations if the documentation for the database makes that claim. However, this doesn't necessarily mean that the capability is fully supported in a manner similar to most SQL databases.

 
| Database | ACID | Joins |
| --- | --- | --- |
| Aerospike | Yes | No |
| AgensGraph | Yes | Yes |
| Apache Ignite | Yes | Yes |
| ArangoDB | Yes | Yes |
| Amazon DynamoDB | Yes | No |
| Couchbase | Yes | Yes |
| CouchDB | Yes | Yes |
| IBM Db2 | Yes | Yes |
| InfinityDB | Yes | No |
| LMDB | Yes | No |
| MarkLogic | Yes | Yes[nb 1] |
| MongoDB | Yes | Yes[nb 2] |
| OrientDB | Yes | Yes[nb 3] |

  
1. [↑](./NoSQL#cite_ref-MarkLogicJoins_31-0) Joins do not necessarily apply to document databases, but MarkLogic can do joins using semantics.[[30]](./NoSQL#cite_note-30)
2. [↑](./NoSQL#cite_ref-MongoDBJoin_33-0) MongoDB did not support joining from a sharded collection until version 5.1.[[31]](./NoSQL#cite_note-32)
3. [↑](./NoSQL#cite_ref-OrientDBJoin_35-0) OrientDB can resolve 1:1 joins using links by storing direct links to foreign records.[[32]](./NoSQL#cite_note-34)

 

## Query optimization and indexing in NoSQL databases

 

Different NoSQL databases, such as [DynamoDB](./Amazon_DynamoDB), [MongoDB](./MongoDB), [Cassandra](./Apache_Cassandra), [Couchbase](./Couchbase_Server), HBase, and Redis, exhibit varying behaviors when querying non-indexed fields. Many perform full-table or collection scans for such queries, applying filtering operations after retrieving data. However, modern NoSQL databases often incorporate advanced features to optimize query performance. For example, MongoDB supports compound indexes and query-optimization strategies, Cassandra offers secondary indexes and materialized views, and Redis employs custom indexing mechanisms tailored to specific use cases. Systems like Elasticsearch use inverted indexes for efficient text-based searches, but they can still require full scans for non-indexed fields. This behavior reflects the design focus of many NoSQL systems on scalability and efficient key-based operations rather than optimized querying for arbitrary fields. Consequently, while these databases excel at basic [CRUD](./Create,_read,_update_and_delete) operations and key-based lookups, their suitability for complex queries involving joins or non-indexed filtering varies depending on the database type—document, key–value, wide-column, or graph—and the specific implementation.[[33]](./NoSQL#cite_note-36)

 

## See also

  please do not list specific implementations here  
- [CAP theorem](./CAP_theorem)
- [Comparison of object database management systems](./Comparison_of_object_database_management_systems)
- [Comparison of structured storage software](./Comparison_of_structured_storage_software)
- [Database scalability](./Database_scalability)
- [Distributed cache](./Distributed_cache)
- [Faceted search](./Faceted_search)
- [List of NoSQL software and tools](./List_of_NoSQL_software_and_tools)
- [MultiValue](./MultiValue) database
- [Multi-model database](./Multi-model_database)
- [Schema-agnostic databases](./Schema-agnostic_databases)
- [Triplestore](./Triplestore)
- [Vector database](./Vector_database)

 

## References

 
1. [↑](./NoSQL#cite_ref-1) [http://nosql-database.org/](http://nosql-database.org/) "NoSQL DEFINITION: Next Generation Databases mostly addressing some of the points : being non-relational, distributed, open-source and horizontally scalable".
2. [↑](./NoSQL#cite_ref-2) ["What Is a NoSQL Database? | IBM"](https://www.ibm.com/topics/nosql-databases). *www.ibm.com*. 12 December 2022. Retrieved 9 August 2024.
3. [↑](./NoSQL#cite_ref-3) ["NoSQL (Not Only SQL)"](http://searchdatamanagement.techtarget.com/definition/NoSQL-Not-Only-SQL). NoSQL database, also called Not Only SQL
4. [↑](./NoSQL#cite_ref-4) [Fowler, Martin](./Martin_Fowler_(software_engineer)). ["NosqlDefinition"](http://martinfowler.com/bliki/NosqlDefinition.html). many advocates of NoSQL say that it does not mean a "no" to SQL, rather it means Not Only SQL
5. [↑](./NoSQL#cite_ref-5) Mohan, C. (2013). [*History Repeats Itself: Sensible and NonsenSQL Aspects of the NoSQL Hoopla*](http://openproceedings.eu/2013/conf/edbt/Mohan13.pdf) (PDF). Proc. 16th Int'l Conf. on Extending Database Technology.
6. [↑](./NoSQL#cite_ref-6) ["Amazon Goes Back to the Future With 'NoSQL' Database"](https://www.wired.com/2012/01/amazon-dynamodb/). WIRED. 19 January 2012. Retrieved 6 March 2017.
7. [↑](./NoSQL#cite_ref-leavitt6_7-0) Leavitt, Neal (2010). ["Will NoSQL Databases Live Up to Their Promise?"](http://www.leavcom.com/pdf/NoSQL.pdf) (PDF). *[IEEE Computer](./IEEE_Computer)*. **43** (2): 12–14. [Bibcode](./Bibcode_(identifier)):[2010Compr..43b..12L](https://ui.adsabs.harvard.edu/abs/2010Compr..43b..12L). [doi](./Doi_(identifier)):[10.1109/MC.2010.58](https://doi.org/10.1109%2FMC.2010.58). [S2CID](./S2CID_(identifier)) [26876882](https://api.semanticscholar.org/CorpusID:26876882).
8. [↑](./NoSQL#cite_ref-8) ["RDBMS dominate the database market, but NoSQL systems are catching up"](https://web.archive.org/web/20131124095417/http://db-engines.com/en/blog_post/23). DB-Engines.com. 21 November 2013. Archived from [the original](http://db-engines.com/en/blog_post/23) on 24 November 2013. Retrieved 24 November 2013.
9. [↑](./NoSQL#cite_ref-9) Vogels, Werner (18 January 2012). ["Amazon DynamoDB – a Fast and Scalable NoSQL Database Service Designed for Internet Scale Applications"](http://www.allthingsdistributed.com/2012/01/amazon-dynamodb.html). All Things Distributed. Retrieved 6 March 2017.
10. [↑](./NoSQL#cite_ref-10) ["Jepsen: MongoDB stale reads"](https://aphyr.com/posts/322-call-me-maybe-mongodb-stale-reads). *Aphyr.com*. 20 April 2015. Retrieved 6 March 2017.
11. [↑](./NoSQL#cite_ref-11) ["MongoDB ACID Transactions"](https://www.geeksforgeeks.org/acid-transactions-in-mongodb/). *GeeksforGeeks*. 12 March 2024. Retrieved 25 October 2024.
12. [↑](./NoSQL#cite_ref-12) Grolinger, K.; Higashino, W. A.; Tiwari, A.; Capretz, M. A. M. (2013). ["Data management in cloud environments: NoSQL and NewSQL data stores"](http://www.journalofcloudcomputing.com/content/pdf/2192-113X-2-22.pdf) (PDF). Aira, Springer. Retrieved 8 January 2014.
13. [↑](./NoSQL#cite_ref-13) ["Large volume data analysis on the Typesafe Reactive Platform"](https://www.slideshare.net/MartinZapletal/zapletal-martinlargevolumedataanalytics). *Slideshare.net*. 11 June 2015. Retrieved 6 March 2017.
14. [↑](./NoSQL#cite_ref-14) Fowler, Adam. ["10 NoSQL Misconceptions"](http://www.dummies.com/how-to/content/10-nosql-misconceptions.html). *Dummies.com*. Retrieved 6 March 2017.
15. [↑](./NoSQL#cite_ref-15) ["No! to SQL and No! to NoSQL"](https://iggyfernandez.wordpress.com/2013/07/28/no-to-sql-and-no-to-nosql/). *Iggyfernandez.wordpress.com*. 29 July 2013. Retrieved 6 March 2017.
16. [↑](./NoSQL#cite_ref-16) Chapple, Mike. ["The ACID Model"](https://web.archive.org/web/20161229001436/http://databases.about.com/od/specificproducts/a/acid.htm). *about.com*. Archived from [the original](http://databases.about.com/od/specificproducts/a/acid.htm) on 29 December 2016. Retrieved 26 September 2012.
17. [↑](./NoSQL#cite_ref-17) Lawrence, Integration and virtualization of relational SQL and NoSQL systems including MySQL and MongoDB (2014). "Integration and virtualization of relational SQL and NoSQL systems including MySQL and MongoDB". *International Conference on Computational Science and Computational Intelligence 1*.
18. [↑](./NoSQL#cite_ref-:0_18-0) Lith, Adam; Mattson, Jakob (2010). ["Investigating storage solutions for large data: A comparison of well performing and scalable data storage solutions for real time extraction and batch insertion of data"](http://publications.lib.chalmers.se/records/fulltext/123839.pdf) (PDF). Department of Computer Science and Engineering, Chalmers University of Technology. p. 70. Retrieved 12 May 2011.
19. [↑](./NoSQL#cite_ref-19) ["NoSQL Relational Database Management System: Home Page"](http://www.strozzi.it/cgi-bin/CSA/tw7/I/en_US/nosql/Home%20Page). Strozzi.it. 2 October 2007. Retrieved 29 March 2010.
20. [↑](./NoSQL#cite_ref-20) ["NoSQL 2009"](https://web.archive.org/web/20110716174012/http://blog.sym-link.com/2009/05/12/nosql_2009.html). Blog.sym-link.com. 12 May 2009. Archived from [the original](http://blog.sym-link.com/2009/05/12/nosql_2009.html) on 16 July 2011. Retrieved 29 March 2010.
21. [↑](./NoSQL#cite_ref-21) Strauch, Christof. ["NoSQL Databases"](http://www.christof-strauch.de/nosqldbs.pdf) (PDF). pp. 23–24. Retrieved 27 August 2017.
22. [↑](./NoSQL#cite_ref-22) [https://apacheignite.readme.io/docs](https://apacheignite.readme.io/docs) Ignite Documentation
23. [↑](./NoSQL#cite_ref-23) [https://www.infoworld.com/article/3135070/data-center/fire-up-big-data-processing-with-apache-ignite.html](https://www.infoworld.com/article/3135070/data-center/fire-up-big-data-processing-with-apache-ignite.html) fire-up-big-data-processing-with-apache-ignite
24. [↑](./NoSQL#cite_ref-24) Sandy (14 January 2011). ["Key Value stores and the NoSQL movement"](http://dba.stackexchange.com/a/619). Stackexchange. Retrieved 1 January 2012. Key–value stores allow the application developer to store schema-less data. This data usually consists of a string that represents the key, and the actual data that is considered the value in the "key–value" relationship. The data itself is usually some kind of primitive of the programming language (a string, an integer, or an array) or an object that is being marshaled by the programming language's bindings to the key-value store. This structure replaces the need for a fixed data model and allows proper formatting.
25. [↑](./NoSQL#cite_ref-25) Seeger, Marc (21 September 2009). ["Key-Value Stores: a practical overview"](http://blog.marc-seeger.de/assets/papers/Ultra_Large_Sites_SS09-Seeger_Key_Value_Stores.pdf) (PDF). Marc Seeger. Retrieved 1 January 2012. Key–value stores provide a high-performance alternative to relational database systems with respect to storing and accessing data. This paper provides a short overview of some of the currently available key–value stores and their interface to the Ruby programming language.
26. [↑](./NoSQL#cite_ref-26) Katsov, Ilya (1 March 2012). ["NoSQL Data Modeling Techniques"](http://highlyscalable.wordpress.com/2012/03/01/nosql-data-modeling-techniques/). Ilya Katsov. Retrieved 8 May 2014.
27. [↑](./NoSQL#cite_ref-27) ["TerminusDB an open-source in-memory document graph database"](https://terminusdb.com/products/terminusdb/). *terminusdb.com*. Retrieved 16 December 2021.
28. [↑](./NoSQL#cite_ref-28) Scofield, Ben (14 January 2010). ["NoSQL - Death to Relational Databases(?)"](https://www.slideshare.net/bscofield/nosql-codemash-2010). Retrieved 26 June 2014.
29. [↑](./NoSQL#cite_ref-DataModeling-Couchbase.com_November_11_2019c_29-0)  ["Moving From Relational to NoSQL: How to Get Started"](https://resources.couchbase.com/c/relational-no-sql-wp?x=3-FqHm). *Couchbase.com*. Retrieved 11 November 2019. 
30. [↑](./NoSQL#cite_ref-30) ["Can't do joins with MarkLogic? It's just a matter of Semantics! - General Networks"](https://web.archive.org/web/20170303200231/http://gennet.com/big-data/cant-joins-marklogic-just-matter-semantics/). *Gennet.com*. Archived from [the original](https://www.gennet.com/big-data/cant-joins-marklogic-just-matter-semantics/) on 3 March 2017. Retrieved 6 March 2017.
31. [↑](./NoSQL#cite_ref-32) ["Sharded Collection Restrictions"](https://docs.mongodb.com/manual/reference/operator/aggregation/lookup/#sharded-collection-restrictions). *docs.mongodb.com*. Retrieved 24 January 2020.
32. [↑](./NoSQL#cite_ref-34) ["SQL Reference · OrientDB Manual"](http://orientdb.com/docs/2.2.x/SQL.html#joins). *OrientDB.com*. Retrieved 24 January 2020.
33. [↑](./NoSQL#cite_ref-36) Sullivan, Dan. *NoSQL for Mere Mortals*. [ISBN](./ISBN_(identifier)) [978-0134023212](./Special:BookSources/978-0134023212).

 

## Further reading

 
- Sadalage, Pramod; [Fowler, Martin](./Martin_Fowler_(software_engineer)) (2012). *NoSQL Distilled: A Brief Guide to the Emerging World of Polyglot Persistence*. Addison-Wesley. [ISBN](./ISBN_(identifier)) [978-0-321-82662-6](./Special:BookSources/978-0-321-82662-6).
- McCreary, Dan; Kelly, Ann (2013). *Making Sense of NoSQL: A guide for managers and the rest of us*. Manning. [ISBN](./ISBN_(identifier)) [9781617291074](./Special:BookSources/9781617291074).
- Wiese, Lena (2015). *Advanced Data Management for SQL, NoSQL, Cloud and Distributed Databases*. DeGruyter/Oldenbourg. [ISBN](./ISBN_(identifier)) [978-3-11-044140-6](./Special:BookSources/978-3-11-044140-6).
- Strauch, Christof (2012). ["NoSQL Databases"](http://www.christof-strauch.de/nosqldbs.pdf) (PDF).
- Moniruzzaman, A. B.; Hossain, S. A. (2013). "NoSQL Database: New Era of Databases for Big data Analytics - Classification, Characteristics and Comparison". [arXiv](./ArXiv_(identifier)):[1307.0191](https://arxiv.org/abs/1307.0191) [[cs.DB](https://arxiv.org/archive/cs.DB)].
- Orend, Kai (2013). "Analysis and Classification of NoSQL Databases and Evaluation of their Ability to Replace an Object-relational Persistence Layer". [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.184.483](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.184.483).
- Krishnan, Ganesh; Kulkarni, Sarang; Dadbhawala, Dharmesh Kirit. ["Method and system for versioned sharing, consolidating and reporting information"](https://patents.google.com/patent/US7383272?oq=ganesh+krishnan).

 

## External links

 
- Strauch, Christof. ["NoSQL whitepaper"](http://www.christof-strauch.de/nosqldbs.pdf) (PDF). Stuttgart: Hochschule der Medien.
- Edlich, Stefan. ["NoSQL database List"](http://nosql-database.org/).
- Neubauer, Peter (2010). ["Graph Databases, NOSQL and Neo4j"](http://www.infoq.com/articles/graph-nosql-neo4j).
- Bushik, Sergey (2012). ["A vendor-independent comparison of NoSQL databases: Cassandra, HBase, MongoDB, Riak"](https://www.networkworld.com/article/665327/tech-primers-a-vendor-independent-comparison-of-nosql-databases-cassandra-hbase-mongodb-riak.html). NetworkWorld.
- Zicari, Roberto V. (2014). ["NoSQL Data Stores – Articles, Papers, Presentations"](http://www.odbms.org/category/downloads/nosql-data-stores/nosql-data-stores-articles/). *odbms.org*.

 
| vteDatabase management systems |
| --- |
| Types | Object-orientedcomparisonRelationallistcomparisonKey–valueColumn-orientedlistDocument-orientedWide-column storeGraphNoSQLNewSQLIn-memorylistMulti-modelcomparisonCloudBlockchain-based database |
| Concepts | DatabaseACIDArmstrong's axiomsCodd's 12 rulesCAP theoremCRUDNullCandidate keyForeign keyPACELC design principleSuperkeySurrogate keyUnique key |
| Objects | RelationtablecolumnrowViewTransactionTransaction logTriggerIndexStored procedureCursorPartition |
| Components | Concurrency controlData dictionaryJDBCXQJODBCQuery languageQuery optimizerQuery rewriting systemQuery plan |
| Functions | AdministrationQuery optimizationReplicationSharding |
| Related topics | Database modelsDatabase normalizationDatabase storageDistributed databaseFederated database systemReferential integrityRelational algebraRelational calculusRelational modelObject–relational databaseTransaction processingList of SQL software and tools |
| CategoryOutline |