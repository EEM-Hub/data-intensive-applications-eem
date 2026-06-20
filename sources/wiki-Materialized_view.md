---
source: https://en.wikipedia.org/wiki/Materialized_view
fetched: 2026-06-19
---

In databases, cached query results 

In [computing](./Computing), a **materialized view** is a [database](./Database) object that contains the results of a [query](./Query_(databases)). For example, it may be a local copy of data located remotely, or may be a subset of the rows and/or columns of a table or [join](./Join_(SQL)) result, or may be a summary using an [aggregate function](./Aggregate_function).

 

The process of setting up a materialized view is sometimes called **materialization**.[[1]](./Materialized_view#cite_note-Date2006-1) This is a form of [caching](./Cache_(computing)) the results of a query, similar to [memoization](./Memoization) of the value of a function in functional languages, and it is sometimes described as a form of [precomputation](./Precomputation).[[2]](./Materialized_view#cite_note-MortonOsborne2013-2)[[3]](./Materialized_view#cite_note-AufaureZimányi2012-3) As with other forms of precomputation, database users typically use materialized views for performance reasons, i.e. as a form of optimization.[[4]](./Materialized_view#cite_note-Gonzales2003-4)

 

Materialized views that store data based on remote tables were also known as [snapshots](./Snapshot_(computer_storage)#In_databases)[[5]](./Materialized_view#cite_note-5) (deprecated [Oracle](./Oracle_Database) terminology).

 

In any [database management system](./Database_management_system) following the [relational model](./Relational_model), a [view](./View_(database)) is a virtual [table](./Table_(database)) representing the result of a [database](./Database) [query](./Information_retrieval). Whenever a query or an update addresses an ordinary view's virtual table, the DBMS converts these into queries or updates against the underlying base tables. A materialized view takes a different approach: the query result is [cached](./Database_cache) as a concrete ("materialized") table (rather than a view as such) that may be updated from the original base tables from time to time. This enables much more efficient access, at the cost of extra storage and of some data being potentially out-of-date. Materialized views find use especially in [data warehousing](./Data_warehousing) scenarios, where frequent queries of the actual base tables can be expensive.[*[citation needed](./Wikipedia:Citation_needed)*]

 

In a materialized view, [indexes](./Index_(database)) can be built on any column. In contrast, in a normal view, it's typically only possible to exploit indexes on columns that come directly from (or have a mapping to) indexed columns in the base tables; often this functionality is not offered at all.

 

## Implementations

 

### Oracle

 

Materialized views were implemented first by the [Oracle Database](./Oracle_Database): the Query rewrite feature was added from version 8i.[[6]](./Materialized_view#cite_note-6)

 

Example syntax to create a materialized view in Oracle:

 
```
 CREATE MATERIALIZED VIEW MV_MY_VIEW
REFRESH FAST START WITH SYSDATE
   NEXT SYSDATE + 1
     AS SELECT * FROM <table_name>;

```
 

### PostgreSQL

 

In [PostgreSQL](./PostgreSQL), version 9.3 and newer natively support materialized views.[[7]](./Materialized_view#cite_note-7) In version 9.3, a materialized view is not auto-refreshed, and is populated only at time of creation (unless `WITH NO DATA` is used). It may be refreshed later manually using `REFRESH MATERIALIZED VIEW`.[[8]](./Materialized_view#cite_note-8) In version 9.4, the refresh may be concurrent with selects on the materialized view if `CONCURRENTLY` is used.[[9]](./Materialized_view#cite_note-9)

 

Example syntax to create a materialized view in PostgreSQL:

 
```
 CREATE MATERIALIZED VIEW MV_MY_VIEW
 [ WITH (storage_parameter [= value] [, ... ]) ]
    [ TABLESPACE tablespace_name ]
     AS SELECT * FROM <table_name>;

```
 

### SQL Server

 

Microsoft SQL Server differs from other RDBMS by the way of implementing materialized view via a concept known as "Indexed Views". The main difference is that such views do not require a refresh because they are in fact always synchronized to the original data of the tables that compound the view. To achieve this, it is necessary that the lines of origin and destination are "deterministic" in their mapping, which limits the types of possible queries to do this. This mechanism has been realised since the 2000 version of SQL Server.

 

Example syntax to create a materialized view in SQL Server:

 
```
CREATE VIEW MV_MY_VIEW
WITH SCHEMABINDING
AS 
SELECT COL1, SUM(COL2) AS TOTAL
FROM <table_name>
GROUP BY COL1;
GO
CREATE UNIQUE CLUSTERED INDEX XV 
   ON MV_MY_VIEW (COL1);

```
 

### Stream processing frameworks

 

[Apache Kafka](./Apache_Kafka) (since v0.10.2), [Apache Spark](./Apache_Spark) (since v2.0), Apache Flink, [Kinetica DB](./Kinetica_(software)),[[10]](./Materialized_view#cite_note-10) Materialize,[[11]](./Materialized_view#cite_note-11) RisingWave,[[12]](./Materialized_view#cite_note-12) and Epsio[[13]](./Materialized_view#cite_note-13) all support materialized views on streams of data.

 

### Others

 

Materialized views are also supported in [Sybase](./Sybase) [SQL Anywhere](./SQL_Anywhere).[[14]](./Materialized_view#cite_note-14) In [IBM Db2](./IBM_Db2), they are called "materialized query tables".[[15]](./Materialized_view#cite_note-15) [ClickHouse](./ClickHouse) supports materialized views that automatically refresh on merges. [[16]](./Materialized_view#cite_note-16) [MySQL](./MySQL) doesn't support materialized views natively, but workarounds can be implemented by using triggers or stored procedures [[17]](./Materialized_view#cite_note-17) or by using the open-source application [Flexviews](./Flexviews?action=edit&redlink=1).[[18]](./Materialized_view#cite_note-18) Materialized views can be implemented in [Amazon DynamoDB](./Amazon_DynamoDB) using data modification events captured by DynamoDB Streams.
Google announced in 8 April 2020[[19]](./Materialized_view#cite_note-19) the availability of materialized views for BigQuery[[20]](./Materialized_view#cite_note-20) as a beta release.

 

## References

  
1. [↑](./Materialized_view#cite_ref-Date2006_1-0) Compare: C.J. Date (28 August 2006). [*The Relational Database Dictionary: A Comprehensive Glossary of Relational Terms and Concepts, with Illustrative Examples*](https://books.google.com/books?id=vWKClUCN2HYC&pg=PA59). O'Reilly Media, Inc. p. 59. [ISBN](./ISBN_(identifier)) [978-1-4493-9115-7](./Special:BookSources/978-1-4493-9115-7). Retrieved 26 October 2016. materialization[:] A somewhat unsophisticated technique for implementing operations on views according to which (a) the relational expression that defines the view is evaluated at the time the operation is invoked, (b) the view is thereby materialized, and (c) the operation in question is then executed against the relation so materialized.
2. [↑](./Materialized_view#cite_ref-MortonOsborne2013_2-0) Karen Morton; Kerry Osborne; Robyn Sands; Riyaj Shamsudeen; Jared Still (28 October 2013). [*Pro Oracle SQL*](https://books.google.com/books?id=XUPXAQAAQBAJ&pg=PA48). Apress. p. 48. [ISBN](./ISBN_(identifier)) [978-1-4302-6220-6](./Special:BookSources/978-1-4302-6220-6).
3. [↑](./Materialized_view#cite_ref-AufaureZimányi2012_3-0) Marie-Aude Aufaure; Esteban Zimányi (16 January 2012). [*Business Intelligence: First European Summer School, EBISS 2011, Paris, France, July 3-8, 2011, Tutorial Lectures*](https://books.google.com/books?id=UWtes499ZaUC&pg=PA43). Springer Science & Business Media. p. 43. [ISBN](./ISBN_(identifier)) [978-3-642-27357-5](./Special:BookSources/978-3-642-27357-5).
4. [↑](./Materialized_view#cite_ref-Gonzales2003_4-0) Michael L. Gonzales (25 February 2003). [*IBM Data Warehousing: with IBM Business Intelligence Tools*](https://books.google.com/books?id=7ZepRMDSsf8C&pg=PA214). John Wiley & Sons. p. 214. [ISBN](./ISBN_(identifier)) [978-0-471-45736-7](./Special:BookSources/978-0-471-45736-7).
5. [↑](./Materialized_view#cite_ref-5)  C.J. Date (28 August 2006). [*The Relational Database Dictionary: A Comprehensive Glossary of Relational Terms and Concepts, with Illustrative Examples*](https://books.google.com/books?id=vWKClUCN2HYC&pg=PA59). O'Reilly Media, Inc. p. 59. [ISBN](./ISBN_(identifier)) [978-1-4493-9115-7](./Special:BookSources/978-1-4493-9115-7). Retrieved 26 October 2016. materialized view[:] Deprecated term for a snapshot. [...] The problem is [...] that (as the definition indicates) snapshots have come to be known, at least in some circles, not as snapshots at all but as materialized views. But snapshots aren't views; views are virtual and snapshots aren't, and 'materialized view' is a contradiction in terms (at least as far as the model is concerned). Worse yet, the unqualified term *view* is often taken to mean a materialized view specifically, and thus we're in danger of no longer having a good term for a view in the original sense.
6. [↑](./Materialized_view#cite_ref-6) [Oracle8i Tuning Release 8.1.5](http://www.ecst.csuchico.edu/~melody/courses/Fall2001CSCI379/DOC/server.815/a67775/ch2.htm). Ecst.csuchico.edu. Retrieved on 2012-02-09.
7. [↑](./Materialized_view#cite_ref-7) ["Materialized Views - PostgreSQL wiki"](https://wiki.postgresql.org/wiki/Materialized_Views). *wiki.postgresql.org*. Retrieved 29 November 2022.
8. [↑](./Materialized_view#cite_ref-8) ["CREATE MATERIALIZED VIEW"](https://www.postgresql.org/docs/15/sql-creatematerializedview.html). *PostgreSQL Documentation*. 10 November 2022. Retrieved 29 November 2022.
9. [↑](./Materialized_view#cite_ref-9) ["REFRESH MATERIALIZED VIEW"](https://www.postgresql.org/docs/current/sql-refreshmaterializedview.html). *PostgreSQL Documentation*. 13 February 2020. Retrieved 29 November 2022.
10. [↑](./Materialized_view#cite_ref-10) ["Materialized Views"](https://docs.kinetica.com/7.1/concepts/materialized_views/). Retrieved 28 December 2022.
11. [↑](./Materialized_view#cite_ref-11) ["CMU DB Talk: Building Materialize"](https://materialize.com/blog-cmudb/). Retrieved 30 March 2022.
12. [↑](./Materialized_view#cite_ref-12) ["Is RisingWave the Next Apache Flink?"](https://www.singularity-data.com/blog/is-risingwave-the-next-apache-flink). *www.singularity-data.com*. 28 April 2022. Retrieved 30 June 2022.
13. [↑](./Materialized_view#cite_ref-13) ["How we built a Streaming SQL Engine"](https://www.epsio.io/blog/how-to-create-a-streaming-sql-engine). Retrieved 21 May 2025.
14. [↑](./Materialized_view#cite_ref-14) [Materialized Views – Sybase SQL Anywhere](http://www.ianywhere.com/developer/product_manuals/sqlanywhere/1000/en/html/dbugen10/ug-workingwdb-s-3142433.html) [Archived](https://web.archive.org/web/20091214083022/http://www.ianywhere.com/developer/product_manuals/sqlanywhere/1000/en/html/dbugen10/ug-workingwdb-s-3142433.html) 2009-12-14 at the [Wayback Machine](./Wayback_Machine). Ianywhere.com. Retrieved on 2012-02-09.
15. [↑](./Materialized_view#cite_ref-15) [Improving Performance with SQL Server 2005 Indexed Views](http://www.microsoft.com/technet/prodtechnol/sql/2005/impprfiv.mspx). Microsoft.com. Retrieved on 2012-02-09.
16. [↑](./Materialized_view#cite_ref-16) [ClickHouse Documentation MaterializedView](https://clickhouse.yandex/docs/en/operations/table_engines/materializedview/). Clickhouse.yandex. Retrieved on 2019-09-05.
17. [↑](./Materialized_view#cite_ref-17) [Implementing materialized views in MySQL](http://www.shinguz.ch/MySQL/mysql_mv.html). Shinguz.ch (2006-11-06). Retrieved on 2012-02-09.
18. [↑](./Materialized_view#cite_ref-18) [Flexviews for MySQL – incrementally refreshable materialized views w/ MySQL](https://flexviews.sourceforge.net/index.html). Flexviews.sourceforge.net. Retrieved on 2012-02-09.
19. [↑](./Materialized_view#cite_ref-19) ["Release notes"](https://cloud.google.com/bigquery/docs/release-notes#April_08_2020). Google.com. 8 April 2020. Retrieved 21 July 2021.
20. [↑](./Materialized_view#cite_ref-20) [Google BigQuery Materialized Views documentation](https://cloud.google.com/bigquery/docs/materialized-views-intro#monitoring_materialized_views) Google.com Retrieved on 2020-05-20.

 

## External links

 
- [Materialized View Concepts and Architecture – Oracle](http://download.oracle.com/docs/cd/B10501_01/server.920/a96567/repmview.htm)
- [SQL Snippets: SQL Features Tutorials – Materialized Views – Oracle](http://www.sqlsnippets.com/en/topic-12868.html)
- [Oracle9i Replication Management API Reference Release 2 (9.2)](http://download.oracle.com/docs/cd/B10501_01/server.920/a96568/rarmviea.htm#94135)
- [Materialized Views in Oracle 11.2](https://web.archive.org/web/20110303073052/http://download.oracle.com/docs/cd/E11882_01/server.112/e17118/statements_6002.htm#SQLRF01302)
- [Materialized query tables in Db2](https://archive.today/20130103084125/http://publib.boulder.ibm.com/infocenter/dzichelp/v2r2/index.jsp?topic=/com.ibm.db2z10.doc.intro/src/tpc/db2z_typesoftables.htm)
- [Creating Materialized Views In MySQL](http://www.coding-dude.com/wp/databases/creating-mysql-materialized-views/)

 
- [Optimizing Data with Materialized Views: An E-Commerce Story](https://datamaster.cloud/the-journey-of-data-optimization-a-story-of-materialized-views-in-e-commerce/)

 
| vteDatabase management systems |
| --- |
| Types | Object-orientedcomparisonRelationallistcomparisonKey–valueColumn-orientedlistDocument-orientedWide-column storeGraphNoSQLNewSQLIn-memorylistMulti-modelcomparisonCloudBlockchain-based database |
| Concepts | DatabaseACIDArmstrong's axiomsCodd's 12 rulesCAP theoremCRUDNullCandidate keyForeign keyPACELC design principleSuperkeySurrogate keyUnique key |
| Objects | RelationtablecolumnrowViewTransactionTransaction logTriggerIndexStored procedureCursorPartition |
| Components | Concurrency controlData dictionaryJDBCXQJODBCQuery languageQuery optimizerQuery rewriting systemQuery plan |
| Functions | AdministrationQuery optimizationReplicationSharding |
| Related topics | Database modelsDatabase normalizationDatabase storageDistributed databaseFederated database systemReferential integrityRelational algebraRelational calculusRelational modelObject–relational databaseTransaction processingList of SQL software and tools |
| CategoryOutline |