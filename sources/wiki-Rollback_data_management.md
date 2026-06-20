---
source: https://en.wikipedia.org/wiki/Rollback_(data_management)
fetched: 2026-06-19
---

Database operation that restores a previous state 

In [database](./Database) technologies, a **rollback** is an operation which returns the database to some previous state. Rollbacks are important for database [integrity](./Data_integrity), because they mean that the database can be restored to a clean copy even after erroneous operations are performed.[[1]](./Rollback_(data_management)#cite_note-1) They are crucial for recovering from database server crashes; by rolling back any [transaction](./Database_transaction) which was active at the time of the crash, the database is restored to a consistent state.

 

The rollback feature is usually implemented with a [transaction log](./Database_log), but can also be implemented via [multiversion concurrency control](./Multiversion_concurrency_control).

 

## Cascading rollback

 

A cascading rollback occurs in database systems when a transaction (T1) causes a failure and a rollback must be performed. Other transactions dependent on T1's actions must also be rollbacked due to T1's failure, thus causing a cascading effect. That is, one transaction's failure causes many to fail.

 

Practical database recovery techniques guarantee cascadeless rollback, therefore a cascading rollback is not a desirable result. Cascading rollback is scheduled by dba.

 

## SQL

 

SQL refers to Structured Query Language, a kind of language used to access, update and manipulate database.
In [SQL](./SQL), `ROLLBACK` is a command that causes all data changes since the last `START TRANSACTION` or `BEGIN` to be discarded by the [relational database management systems](./Relational_database_management_systems) (RDBMS), so that the state of the data is "rolled back" to the way it was before those changes were made.[[2]](./Rollback_(data_management)#cite_note-2)

 

A `ROLLBACK` statement will also release any existing [savepoints](./Savepoint) that may be in use.

 

In most SQL dialects, `ROLLBACK`s are connection specific.  This means that if two connections are made to the same database, a `ROLLBACK` made in one connection will not affect any other connections.  This is vital for proper [concurrency](./Concurrent_programming).

 

## Usage outside databases

 

Rollbacks are not exclusive to databases: any [stateful](./Stateful) [distributed system](./Distributed_system) may use rollback operations to maintain [consistency](./Consistency_(database_systems)). Examples of distributed systems that can support rollbacks include [message queues](./Message_queue) and [workflow management systems](./Workflow_management_system). More generally, any operation that resets a system to its previous state before another operation or series of operations can be viewed as a rollback.

 

## See also

 
- [Savepoint](./Savepoint)
- [Commit](./Commit_(data_management))
- [Undo](./Undo)
- [Schema migration](./Schema_migration)

 

## Notes

  
1. [↑](./Rollback_(data_management)#cite_ref-1) ["Database Rollback – What and Why"](https://soaringeagle.biz/what-is-a-database-rollback/). 3 November 2019. Retrieved 16 April 2022.
2. [↑](./Rollback_(data_management)#cite_ref-2) Ben Richardson (26 December 2019). ["Rollback SQL: Rolling back transactions via the ROLLBACK SQL query"](https://www.sqlshack.com/rollback-sql-rolling-back-transactions-via-the-rollback-sql-query/). Retrieved 16 April 2022.

 

## References

 
- [Ramez Elmasri](./Ramez_Elmasri) (2007). *Fundamentals of Database Systems*. [Pearson Addison Wesley](./Pearson_Addison_Wesley?action=edit&redlink=1). [ISBN](./ISBN_(identifier)) [978-0-321-36957-4](./Special:BookSources/978-0-321-36957-4).
- ["ROLLBACK Transaction"](https://msdn2.microsoft.com/en-us/library/ms181299.aspx), Microsoft SQL Server.
- ["Sql Commands"](https://www.pantz.org/software/mysql/mysqlcommands.html), MySQL.

 
| vteDatabase management systems |
| --- |
| Types | Object-orientedcomparisonRelationallistcomparisonKey–valueColumn-orientedlistDocument-orientedWide-column storeGraphNoSQLNewSQLIn-memorylistMulti-modelcomparisonCloudBlockchain-based database |
| Concepts | DatabaseACIDArmstrong's axiomsCodd's 12 rulesCAP theoremCRUDNullCandidate keyForeign keyPACELC design principleSuperkeySurrogate keyUnique key |
| Objects | RelationtablecolumnrowViewTransactionTransaction logTriggerIndexStored procedureCursorPartition |
| Components | Concurrency controlData dictionaryJDBCXQJODBCQuery languageQuery optimizerQuery rewriting systemQuery plan |
| Functions | AdministrationQuery optimizationReplicationSharding |
| Related topics | Database modelsDatabase normalizationDatabase storageDistributed databaseFederated database systemReferential integrityRelational algebraRelational calculusRelational modelObject–relational databaseTransaction processingList of SQL software and tools |
| CategoryOutline |

 
| vteWeb syndication |
| --- |
| HistoryBloggingPodcastingVloggingWeb syndication technology |
| Types | ArtBloggernacleClassical musicCorporateDream diaryEdublogElectronic journalFakeFamilyFashionFoodHealthLawLifelogMP3NewsPhotoblogPolicePoliticalProjectReverseTravelWarblog | ArtBloggernacleClassical musicCorporateDream diaryEdublogElectronic journalFakeFamilyFashionFoodHealthLawLifelogMP3NewsPhotoblogPolicePoliticalProjectReverseTravelWarblog |
| ArtBloggernacleClassical musicCorporateDream diaryEdublogElectronic journalFakeFamilyFashionFoodHealthLawLifelogMP3NewsPhotoblogPolicePoliticalProjectReverseTravelWarblog |
| Technology | GeneralBitTorrentFeed URI schemeFeaturesLinkbackPermalinkPingPingbackRebloggingRefbackRollbackTrackbackMechanismThreadGeotaggingRSS enclosureSynchronizationMemeticsAtom feedData feedPhotofeedProduct feedRDF feedWeb feedRSSGeoRSSMRSSRSS TVSocialInter-process communicationMashupReferencingRSS editorRSS trackingStreaming mediaStandardOPMLRSS Advisory BoardUsenetWorld Wide WebXBELXOXO | General | BitTorrentFeed URI scheme | Features | LinkbackPermalinkPingPingbackRebloggingRefbackRollbackTrackback | Mechanism | ThreadGeotaggingRSS enclosureSynchronization | Memetics | Atom feedData feedPhotofeedProduct feedRDF feedWeb feed | RSS | GeoRSSMRSSRSS TV | Social | Inter-process communicationMashupReferencingRSS editorRSS trackingStreaming media | Standard | OPMLRSS Advisory BoardUsenetWorld Wide WebXBELXOXO |
| General | BitTorrentFeed URI scheme |
| Features | LinkbackPermalinkPingPingbackRebloggingRefbackRollbackTrackback |
| Mechanism | ThreadGeotaggingRSS enclosureSynchronization |
| Memetics | Atom feedData feedPhotofeedProduct feedRDF feedWeb feed |
| RSS | GeoRSSMRSSRSS TV |
| Social | Inter-process communicationMashupReferencingRSS editorRSS trackingStreaming media |
| Standard | OPMLRSS Advisory BoardUsenetWorld Wide WebXBELXOXO |
| Form | Audio podcastEnhanced podcastMobilecastNarrowcastingPeercastingScreencastSlidecastingVideocastWebcomicWebtoonWeb seriesAnonymous bloggingCollaborative blogColumnistInstant messagingLivebloggingMicroblogMobile bloggingSpam blogVideo bloggingMotovlogging | Audio podcastEnhanced podcastMobilecastNarrowcastingPeercastingScreencastSlidecastingVideocastWebcomicWebtoonWeb series | Anonymous bloggingCollaborative blogColumnistInstant messagingLivebloggingMicroblogMobile bloggingSpam blogVideo bloggingMotovlogging |
| Audio podcastEnhanced podcastMobilecastNarrowcastingPeercastingScreencastSlidecastingVideocastWebcomicWebtoonWeb series |
| Anonymous bloggingCollaborative blogColumnistInstant messagingLivebloggingMicroblogMobile bloggingSpam blogVideo bloggingMotovlogging |
| Media | Alternative mediaCarnivalsFictionJournalismCitizenDatabaseOnline diarySearch enginesSideblogSoftwareWeb directoryMicromediaAggregationNewsPollReviewSearchVideoAtomAtomPubBroadcatchingHashtagNewsML1G2Social communicationSocial softwareWeb SliceRelatedBlogosphereEscribitionistGlossary of bloggingPay per clickPosting styleSlashdot effectSpam in blogsUses of podcasting | Alternative media | CarnivalsFictionJournalismCitizenDatabaseOnline diarySearch enginesSideblogSoftwareWeb directory | Micromedia | AggregationNewsPollReviewSearchVideoAtomAtomPubBroadcatchingHashtagNewsML1G2Social communicationSocial softwareWeb Slice | Related | BlogosphereEscribitionistGlossary of bloggingPay per clickPosting styleSlashdot effectSpam in blogsUses of podcasting |
| Alternative media | CarnivalsFictionJournalismCitizenDatabaseOnline diarySearch enginesSideblogSoftwareWeb directory |
| Micromedia | AggregationNewsPollReviewSearchVideoAtomAtomPubBroadcatchingHashtagNewsML1G2Social communicationSocial softwareWeb Slice |
| Related | BlogosphereEscribitionistGlossary of bloggingPay per clickPosting styleSlashdot effectSpam in blogsUses of podcasting |

 
| Authority control databases: National | United StatesIsrael |
| --- | --- |