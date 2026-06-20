---
source: https://en.wikipedia.org/wiki/Dynamo_(storage_system)
fetched: 2026-06-19
---

Cloud-based service 
|  | This articleneeds additional citations forverification.Please helpimprove this articlebyadding citations to reliable sources. Unsourced material may be challenged and removed.Find sources:"Dynamo"storage system–news·newspapers·books·scholar·JSTOR(February 2017)(Learn how and when to remove this message) |
| --- | --- |

 

**Dynamo** is a set of techniques that together can form a [highly available](./High_availability) key-value [structured storage](./Structured_storage) system[[1]](./Dynamo_(storage_system)#cite_note-decandia-2007-1) or a [distributed data store](./Distributed_data_store).[[1]](./Dynamo_(storage_system)#cite_note-decandia-2007-1) It has properties of both [databases](./Database) and [distributed hash tables](./Distributed_hash_table) (DHTs). It was created to help address some scalability issues that [Amazon](./Amazon_(company)) experienced during the holiday season of 2004.[[2]](./Dynamo_(storage_system)#cite_note-readwrite-2012-2)  By 2007, it was used in [Amazon Web Services](./Amazon_Web_Services), such as its [Simple Storage Service](./Amazon_S3) (S3).[[1]](./Dynamo_(storage_system)#cite_note-decandia-2007-1)

 

## Relationship to DynamoDB

 

[Amazon DynamoDB](./Amazon_DynamoDB) is "built on the principles of Dynamo"[[3]](./Dynamo_(storage_system)#cite_note-3) and is a hosted service within the AWS infrastructure. However, while Dynamo is based on leaderless replication, DynamoDB uses single-leader replication.[[4]](./Dynamo_(storage_system)#cite_note-4)

 

## Principles

 
- Incremental scalability: Dynamo should be able to scale out one storage host (or “node”) at a time, with minimal impact on both operators of the system and the system itself.
- Symmetry: Every node in Dynamo should have the same set of responsibilities as its peers; there should be no distinguished node or nodes that take special roles or extra set of responsibilities.
- Decentralization: An extension of symmetry, the design should favor decentralized peer-to-peer techniques over centralized control.
- Heterogeneity: The system should be able to exploit heterogeneity in the infrastructure it runs on. For example, the work distribution must be proportional to the capabilities of the individual servers. This is essential in adding new nodes with higher capacity without having to upgrade all hosts at once.

 

## Techniques

 
| Problem | Technique | Advantage |
| --- | --- | --- |
| Dataset partitioning | Consistent Hashing | Incremental, possibly linear scalability in proportion to the number of collaborating nodes. |
| Highly available writes | Vector ClockorDotted-Version-Vector Sets, reconciliation during reads | Version size is decoupled from update rates. |
| Handling temporary failures | Sloppy QuorumandHinted Handoff | Provides high availability and durability guarantee when some of the replicas are not available. |
| Recovering from permanent failures | Anti-entropy usingMerkle tree | Can be used to identify differences between replica owners and synchronize divergent replicas pro-actively. |
| Membership and failure detection | Gossip-based membership protocoland failure detection | Avoids having a centralized registry for storing membership and node liveness information, preserving symmetry. |

 

## Implementations

 

Amazon published the paper on Dynamo, but never released its implementation.  The index layer of [Amazon S3](./Amazon_S3) implements and extends many core features of Dynamo.  Since then, several implementations have been created based on the paper. The paper also inspired many other [NoSQL](./NoSQL) database implementations, such as [Apache Cassandra](./Apache_Cassandra), [Project Voldemort](./Project_Voldemort) and [Riak](./Riak).[[2]](./Dynamo_(storage_system)#cite_note-readwrite-2012-2)

 

## See also

 
- [Distributed data store](./Distributed_data_store)
- [NoSQL](./NoSQL)
- [Structured storage](./Structured_storage)

 

## References

 
1. [1](./Dynamo_(storage_system)#cite_ref-decandia-2007_1-0) [2](./Dynamo_(storage_system)#cite_ref-decandia-2007_1-1) [3](./Dynamo_(storage_system)#cite_ref-decandia-2007_1-2) Decandia, G.; Hastorun, D.; Jampani, M.; Kakulapati, G.; Lakshman, A.; Pilchin, A.; Sivasubramanian, S.; Vosshall, P.; Vogels, W. (2007). "Dynamo: Amazon's Highly Available Key-value Store". *Proceedings of twenty-first ACM SIGOPS symposium on Operating systems principles - SOSP '07*. p. 205. [doi](./Doi_(identifier)):[10.1145/1294261.1294281](https://doi.org/10.1145%2F1294261.1294281). [ISBN](./ISBN_(identifier)) [9781595935915](./Special:BookSources/9781595935915). [S2CID](./S2CID_(identifier)) [221033483](https://api.semanticscholar.org/CorpusID:221033483).
2. [1](./Dynamo_(storage_system)#cite_ref-readwrite-2012_2-0) [2](./Dynamo_(storage_system)#cite_ref-readwrite-2012_2-1) [Amazon Takes Another Pass at NoSQL with DynamoDB](https://web.archive.org/web/20130413061708/http://readwrite.com/2012/01/18/amazon-enters-the-nosql-market)
3. [↑](./Dynamo_(storage_system)#cite_ref-3) [Amazon DynamoDB – a Fast and Scalable NoSQL Database Service Designed for Internet Scale Applications](http://www.allthingsdistributed.com/2012/01/amazon-dynamodb.html)
4. [↑](./Dynamo_(storage_system)#cite_ref-4) Kleppmann, Martin (April 2, 2017). *Designing Data-Intensive Applications* (1 ed.). O'Reilly Media. p. 177. [ISBN](./ISBN_(identifier)) [978-1449373320](./Special:BookSources/978-1449373320). Dynamo is not available to users outside of Amazon. Confusingly, AWS offers a hosted database product called DynamoDB, which uses a completely different architecture: it is based on single-leader replication.

 

## External links

 
- [Amazon's Dynamo](http://www.allthingsdistributed.com/2007/10/amazons_dynamo.html) (2007)
- [Amazon reveals its distributed storage: Dynamo](https://arstechnica.com/old/content/2007/10/amazon-reveals-its-distributed-storage-dynamo.ars) (2007)

 
| vteAmazon |
| --- |
| People | CurrentJeff Bezos(Founder and Executive Chairman)Andy Jassy(President and CEO)Werner Vogels(CTO)FormerRick DalzellPaul DavisTony HsiehChristopher NorthRam ShriramTom SzkutakBrian Valentine | Current | Jeff Bezos(Founder and Executive Chairman)Andy Jassy(President and CEO)Werner Vogels(CTO) | Former | Rick DalzellPaul DavisTony HsiehChristopher NorthRam ShriramTom SzkutakBrian Valentine |
| Current | Jeff Bezos(Founder and Executive Chairman)Andy Jassy(President and CEO)Werner Vogels(CTO) |
| Former | Rick DalzellPaul DavisTony HsiehChristopher NorthRam ShriramTom SzkutakBrian Valentine |
| Facilities | DopplerDay 1HQ2Principal PlaceSpheresBellevue 600 |
| Products andservices | SubsidiariesAbeBooksAmazon Game StudiosAmazon Lab126Amazon LeoAmazon PharmacyPillPackAmazon RoboticsAmazon University EsportsAnnapurna LabsAudibleBlink HomeBody LabsBookFinderFreshGoodreadsGoodreads Choice AwardsGraphiqIMDbBox Office MojoIMDbProOne MedicalRingNeighborsShopbopTwitchIGDBWoot.comZapposZooxCloudcomputingWeb ServicesAMIAmazon AuroraBeanstalkCloudFrontDynamoDBEBSEC2EFSElastiCacheEMRGlacierGlueLambdaLightsailMTurkNeptuneProduct Advertising APIRDSRedshiftRekognitionRoute 53S3SageMakerSESSNSSimpleDBSQSVPCServicesAmazon.comChinaAlexaAppstoreDigital Game StoreFire OSKindle StoreLunaPaymentsPrimeAmazon miniTVMX PlayerKeyPrime MusicPrime NowPrime PantryPrime VideoSportsMarketplaceMusic(Wondery)SilkWirelessDevicesAstroEchoShowEcho BudsFireFire HDFire HDXFire TVStickKindleTechnology1-ClickAmazon OneDynamoObidosLumberyardMediaAmazon GamesAmazon PublishingBreakthrough Novel AwardBest Books of the YearAmazon MGM StudiosMetro-Goldwyn-MayerUnited ArtistsOrion PicturesAmerican International PicturesMGM+Kindle Direct PublishingYES Network(15%)RetailWhole Foods MarketLogisticsAmazon FreightAmazon AirAmazon Prime AirFormer43 ThingsA9.comAskvilleAlexa InternetAmapediaAmazon BooksAmazon ClinicAmazon FreshAmazon GoAmie Street(Songza)Book DepositoryCDNowComiXologyDash buttonsDash wandDiapers.comDigital Photography ReviewDouble Helix GamesDriveEndless.comFire PhoneFreeveeLexcycleLiquavistaLivingSocialLoveFilmMGM HoldingsMobipocketPlanetAllReflexive EntertainmentSellabandShelfariSouq.comTenMarksTreasure TruckWithoutabox | Subsidiaries | AbeBooksAmazon Game StudiosAmazon Lab126Amazon LeoAmazon PharmacyPillPackAmazon RoboticsAmazon University EsportsAnnapurna LabsAudibleBlink HomeBody LabsBookFinderFreshGoodreadsGoodreads Choice AwardsGraphiqIMDbBox Office MojoIMDbProOne MedicalRingNeighborsShopbopTwitchIGDBWoot.comZapposZoox | Cloudcomputing | Web ServicesAMIAmazon AuroraBeanstalkCloudFrontDynamoDBEBSEC2EFSElastiCacheEMRGlacierGlueLambdaLightsailMTurkNeptuneProduct Advertising APIRDSRedshiftRekognitionRoute 53S3SageMakerSESSNSSimpleDBSQSVPC | Services | Amazon.comChinaAlexaAppstoreDigital Game StoreFire OSKindle StoreLunaPaymentsPrimeAmazon miniTVMX PlayerKeyPrime MusicPrime NowPrime PantryPrime VideoSportsMarketplaceMusic(Wondery)SilkWireless | Devices | AstroEchoShowEcho BudsFireFire HDFire HDXFire TVStickKindle | Technology | 1-ClickAmazon OneDynamoObidosLumberyard | Media | Amazon GamesAmazon PublishingBreakthrough Novel AwardBest Books of the YearAmazon MGM StudiosMetro-Goldwyn-MayerUnited ArtistsOrion PicturesAmerican International PicturesMGM+Kindle Direct PublishingYES Network(15%) | Retail | Whole Foods Market | Logistics | Amazon FreightAmazon AirAmazon Prime Air | Former | 43 ThingsA9.comAskvilleAlexa InternetAmapediaAmazon BooksAmazon ClinicAmazon FreshAmazon GoAmie Street(Songza)Book DepositoryCDNowComiXologyDash buttonsDash wandDiapers.comDigital Photography ReviewDouble Helix GamesDriveEndless.comFire PhoneFreeveeLexcycleLiquavistaLivingSocialLoveFilmMGM HoldingsMobipocketPlanetAllReflexive EntertainmentSellabandShelfariSouq.comTenMarksTreasure TruckWithoutabox |
| Subsidiaries | AbeBooksAmazon Game StudiosAmazon Lab126Amazon LeoAmazon PharmacyPillPackAmazon RoboticsAmazon University EsportsAnnapurna LabsAudibleBlink HomeBody LabsBookFinderFreshGoodreadsGoodreads Choice AwardsGraphiqIMDbBox Office MojoIMDbProOne MedicalRingNeighborsShopbopTwitchIGDBWoot.comZapposZoox |
| Cloudcomputing | Web ServicesAMIAmazon AuroraBeanstalkCloudFrontDynamoDBEBSEC2EFSElastiCacheEMRGlacierGlueLambdaLightsailMTurkNeptuneProduct Advertising APIRDSRedshiftRekognitionRoute 53S3SageMakerSESSNSSimpleDBSQSVPC |
| Services | Amazon.comChinaAlexaAppstoreDigital Game StoreFire OSKindle StoreLunaPaymentsPrimeAmazon miniTVMX PlayerKeyPrime MusicPrime NowPrime PantryPrime VideoSportsMarketplaceMusic(Wondery)SilkWireless |
| Devices | AstroEchoShowEcho BudsFireFire HDFire HDXFire TVStickKindle |
| Technology | 1-ClickAmazon OneDynamoObidosLumberyard |
| Media | Amazon GamesAmazon PublishingBreakthrough Novel AwardBest Books of the YearAmazon MGM StudiosMetro-Goldwyn-MayerUnited ArtistsOrion PicturesAmerican International PicturesMGM+Kindle Direct PublishingYES Network(15%) |
| Retail | Whole Foods Market |
| Logistics | Amazon FreightAmazon AirAmazon Prime Air |
| Former | 43 ThingsA9.comAskvilleAlexa InternetAmapediaAmazon BooksAmazon ClinicAmazon FreshAmazon GoAmie Street(Songza)Book DepositoryCDNowComiXologyDash buttonsDash wandDiapers.comDigital Photography ReviewDouble Helix GamesDriveEndless.comFire PhoneFreeveeLexcycleLiquavistaLivingSocialLoveFilmMGM HoldingsMobipocketPlanetAllReflexive EntertainmentSellabandShelfariSouq.comTenMarksTreasure TruckWithoutabox |
| Litigation | Perfect 10, Inc. v. Amazon.com, Inc.Amazon.com, Inc. v. Barnesandnoble.com, Inc.Amazon.com Inc v Canada (Commissioner of Patents)FTC v. Amazon |
| Other | Amazon LightASINCommunity Banana StandCriticism(tax)FishbowlHistory of AmazonLibraryThingList of Amazon brandsList of Amazon products and servicesList of mergers and acquisitions by AmazonLockerMacKenzie ScottStatistically improbable phraseVineWorker organizationList of fatalitiesEdwardsville Amazon warehouse collapse |
| Unions | Congress of Essential WorkersAmazon Labor UnionAmazon worker organization2024 strike |
| Category |