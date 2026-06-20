---
source: https://en.wikipedia.org/wiki/SQLite
fetched: 2026-06-19
---

Serverless relational database management system 
| SQLite |
| --- |
|  |
| Screenshot ofsqlite3command-line shell program |
| Developer | D. Richard Hipp |
| Release | 17August 2000;25 years ago(2000-08-17) |
|  |
| Stable release | 3.53.2[1](3 June 2026;17 days ago(3 June 2026)) |
|  |
| Written in | C |
| Operating system | Cross-platform |
| Size | 699KiB |
| Type | RDBMS(embedded) |
| License | Public domain[2] |
| Website | sqlite.org |
| Repository | sqlite.org/src |

  
| SQLite Database File Format |
| --- |
| Filename extension | .sqlite, .sqlite3, .db, .db3, .s3db, .sl3 |
| Internet mediatype | application/vnd.sqlite3[3] |
| Magic number | 53 51 4c 69 74 65 20 66 6f 72 6d 61 74 20 33 00(zero-terminatedASCII"SQLite format 3") |
| Initial release | 2004-06-18 |
| Open format? | yes (Public Domain) |
| Website | sqlite.org/fileformat.html |

 
| This article is part ofa serieson theStructured Query Language |
| --- |
| List of RDBMSs4th DimensionAccess Database EngineActian ZenAdabas DSAP Advantage Database ServerAirtableAltibaseAmazon AuroraAmazon RedshiftApache DerbyApache IgniteAster Data SystemsCA DatacomClarionClickHouseClustrixCockroachDBCUBRIDDataEaseDataFlexDataphordBaseDuckDBEmpress Embedded DatabaseEnterpriseDBeXtremeDBExasolExtensible Storage EngineFileMaker ProFirebirdFoundationDBFrontBaseGoogle BigQueryGreenplumH2HelixHSQLDBIBM Db2IBM Lotus ApproachCA IDMSInfobrightInformixIngresInterBaseInterSystems CachéInterSystems IRISLinter SQL RDBMSMariaDBMaxDBMicrosoft Azure SQL DatabaseMicrosoft SQL ServerMicrosoft SQL Server ExpressMicrosoft Visual FoxProMimer SQLMonetDBmSQLMySQLNetezzaNexusDBNonStop SQLNuoDBOmnis StudioVirtuoso Universal ServerOracle databaseOracle RdbPanoramaParadoxPercona Server for MySQLPercona XtraDBPolyhedraPostgreSQLPostgres Plus Advanced ServerProgress SoftwareR:BaseRethinkDBSAND CDBMSSAP Adaptive Server EnterpriseSAP HANASAP IQSingleStoreSnowflake Cloud Data WarehousesolidDBGoogle Cloud SpannerSQL AnywhereSQL AzureSQLBaseSQLiteSQream DBTeradataTiDBTimescaleDBTimesTenTrafodionTransbaseUnisys OS 2200 databasesUniDataUniVerseVectorwiseVerticaVoltDBYDBYugabyteDB |
| Database administration toolsAdminerApache OpenOffice BaseDatabase WorkbenchDatabaseSpyDbVisualizerDBeaverHeidiSQLLibreOffice BaseMicrosoft AccessMySQL WorkbenchNavicatOracle Enterprise ManagerpgAdminphpLiteAdminPhpSQLiteAdminphpMyAdminSQL Database StudioSQL Server Management StudiosqshToad Data ModelerTOra |
| IDEsApplication Development System OnlineDataGripdbForge StudioOracle SQL DeveloperPL/SQL DeveloperSQLyogSQuirreL SQL ClientToad |
| Database drivers andORMsActiveRecordDoctrineEntity FrameworkHibernateJDBCODBCSQLAlchemy |
| See alsoComparison of RDBMSsComparison of object–RDBMSsDB-Engine Ranking listList of data science softwareList of SQL software and toolsList of NoSQL software and tools |
| Computer programmingportalSQL (Wikibooks) |
| vte |

 

**SQLite** ([/ˌɛsˌkjuːˌɛlˈaɪt/](./Help:IPA/English) "S-Q-L-ite",[[4]](./SQLite#cite_note-4)[[5]](./SQLite#cite_note-5) [/ˈsiːkwəˌlaɪt/](./Help:IPA/English) "sequel-ite"[[6]](./SQLite#cite_note-6)) is a [free and open-source](./Free_and_open-source_software) [relational](./Relational_database) [database engine](./Database_engine) written in the [C programming language](./C_Language). It is not a standalone application; rather, it is a [library](./Library_(computing)) that [software developers](./Programmer) embed in their [applications](./Application_software). As such, it belongs to the family of [embedded databases](./Embedded_database). According to its developers, SQLite is the most widely deployed database engine, as it is used by several of the top [web browsers](./Web_browser), [operating systems](./Operating_system), [mobile phones](./Mobile_phone), and other [embedded systems](./Embedded_system).[[7]](./SQLite#cite_note-7)

 

Many [programming languages](./Programming_language) have [bindings](./Language_binding) to the SQLite library. It generally follows [PostgreSQL](./PostgreSQL) syntax, but does not enforce [type checking](./Type_checking) by default.[[8]](./SQLite#cite_note-Owens_2006-8)[[9]](./SQLite#cite_note-9) This means that one can, for example, insert a string into a [column](./Column_(database)) defined as an integer. Although it is a lightweight embedded database, SQLite implements most of the [SQL](./SQL) standard and the [relational model](./Relational_model), including [transactions](./Transaction_processing) and [ACID](./ACID) guarantees.[[10]](./SQLite#cite_note-10) However, it omits many features implemented by other databases, such as [materialized views](./Materialized_view) and complete support for [triggers](./Database_trigger) and [ALTER TABLE statements](./SQL_syntax).[[11]](./SQLite#cite_note-11)

 

## History

 

[D. Richard Hipp](./D._Richard_Hipp) designed SQLite in the spring of 2000 while working for [General Dynamics](./General_Dynamics) on contract with the [United States Navy](./United_States_Navy).[[12]](./SQLite#cite_note-Owens06-12) Hipp was designing software used for a [damage-control](./Damage_control_(maritime)) system aboard [guided-missile destroyers](./Guided-missile_destroyer); the damage-control system originally used [HP-UX](./HP-UX) with an [Informix](./IBM_Informix) [database](./Database) back-end. SQLite began as a [Tcl](./Tcl_(programming_language)) extension.[[13]](./SQLite#cite_note-:0-13)

 

In August 2000, version 1.0 of SQLite was released, with storage based on [gdbm](./Gdbm) (GNU Database Manager). In September 2001, SQLite 2.0 replaced gdbm with a custom [B-tree](./B-tree) implementation,[[a]](./SQLite#cite_note-15) adding [transaction](./Database_transaction) capability. In June 2004, SQLite 3.0 added [internationalization](./Internationalization_and_localization), [manifest typing](./Manifest_typing), and other major improvements, partially funded by [America Online](./America_Online). In 2011, Hipp announced his plans to add a [NoSQL](./NoSQL) interface to SQLite, as well as announcing UnQL, a functional superset of [SQL](./SQL) designed for [document-oriented databases](./Document-oriented_databases).[[15]](./SQLite#cite_note-unql-interview-16)

 

SQLite is one of four formats recommended for long-term storage of [datasets](./Data_set) approved for use by the [Library of Congress](./Library_of_Congress).[[16]](./SQLite#cite_note-17)[[17]](./SQLite#cite_note-18)[[18]](./SQLite#cite_note-19)

 

## Design

 

SQLite was designed to allow the program to be operated without installing a database management system or requiring a [database administrator](./Database_administrator). Unlike [client–server](./Client–server_model) database management systems, the SQLite engine has no standalone [processes](./Process_(computing)) with which the application program communicates. Instead, a [linker](./Linker_(computing)) integrates the SQLite library—[statically](./Static_library) or [dynamically](./Dynamic_linker)—into an application program which uses SQLite's functionality through simple [function calls](./Subroutine), reducing [latency](./Latency_(engineering)) in database operations; for simple queries with little concurrency, SQLite [performance](./Computer_performance) profits from avoiding the overhead of [inter-process communication](./Inter-process_communication).

 

Due to the serverless design, SQLite applications require less configuration than client–server databases. SQLite is called *zero-configuration*[[19]](./SQLite#cite_note-20) because configuration tasks such as service management, startup scripts, and password- or [GRANT](./Data_control_language)-based access control are unnecessary. [Access control](./Access-control_list) is handled through the [file-system permissions](./File-system_permissions) of the database file.[[20]](./SQLite#cite_note-:2-21) Databases in client–server systems use [file-system](./File_system) permissions that give access to the database files only to the [daemon](./Daemon_(computing)) process, which handles its locks internally, allowing [concurrent](./Concurrency_(computer_science)) writes from several processes.

 

SQLite stores the entire database, consisting of definitions, [tables](./Table_(database)), indices, and data, as a single [cross-platform](./Cross-platform_software) file, allowing several processes or [threads](./Thread_(computer_science)) to access the same database concurrently. It implements this simple design by [locking](./Lock_(computer_science)) the database file during writing.[[20]](./SQLite#cite_note-:2-21) Write access may fail with an [error code](./Error_code), or it can be retried until a configurable timeout expires. SQLite read operations can be [multitasked](./Computer_multitasking), though due to the serverless design, writes can only be performed sequentially. This concurrent access restriction does not apply to temporary tables, and it is relaxed in version 3.7 as [write-ahead logging](./Write-ahead_logging) (WAL) enables concurrent reads and writes.[[21]](./SQLite#cite_note-22) Since SQLite has to rely on file-system locks, it is not the preferred choice for write-intensive deployments.[[22]](./SQLite#cite_note-23)

 

SQLite uses [PostgreSQL](./PostgreSQL) as a reference platform. "What would PostgreSQL do" is used to make sense of the SQL standard.[[23]](./SQLite#cite_note-24)[[24]](./SQLite#cite_note-25) One major deviation is that, with the exception of [primary keys](./Primary_key), SQLite does not enforce [type checking](./Type_checking); the type of a value is dynamic and not strictly constrained by the [schema](./Database_schema) (although the schema will trigger a conversion when storing, if such a conversion is potentially reversible). SQLite strives to follow [Postel's rule](./Robustness_principle).[[25]](./SQLite#cite_note-:1-26)

 

## Features

 

SQLite implements most of the [SQL-92](./SQL-92) standard for SQL, but lacks some features. For example, it only partially provides [triggers](./Database_trigger) and cannot write to [views](./View_(database)) (however, it provides INSTEAD OF triggers that provide this functionality). Its support of [ALTER TABLE](./Data_definition_language#ALTER_statement) statements is limited.[[26]](./SQLite#cite_note-27)

 

SQLite uses an unusual [type system](./Type_system) for an SQL-compatible DBMS: instead of assigning a [type](./SQL_data_types) to a column as in most SQL database systems, types are assigned to individual values; in language terms it is *dynamically typed*. Moreover, it is *weakly typed* in some of the same ways that [Perl](./Perl) is: one can insert a [string](./String_(computer_science)) into an [integer](./Integer_(computer_science)) column (although SQLite will try to convert the string to an integer first, if the column's preferred type is integer). This adds flexibility to columns, especially when bound to a dynamically typed scripting language. However, the technique is not portable to other SQL products. A common criticism is that SQLite's type system lacks the [data integrity](./Data_integrity) mechanism provided by statically typed columns, although it can be emulated with constraints like `CHECK(typeof(x)='integer')`.[[12]](./SQLite#cite_note-Owens06-12) In 2021, support for static typing was added through STRICT tables, which enforce datatype constraints for columns.[[27]](./SQLite#cite_note-28)

 

Tables normally include a hidden *rowid* index column, which provides faster access.[[28]](./SQLite#cite_note-29) If a table includes an INTEGER PRIMARY KEY column, SQLite will typically optimize it by treating it as an alias for the *rowid*, causing the contents to be stored as a [strictly typed](./Strictly_typed) 64-bit signed integer and changing its behavior to be somewhat like an auto-incrementing column. SQLite includes an option to create a table without a rowid column, which can save disk space and improve lookup speed. WITHOUT ROWID tables are required to have a primary key.[[29]](./SQLite#cite_note-30)

 

SQLite supports foreign key constraints,[[30]](./SQLite#cite_note-31)[[31]](./SQLite#cite_note-32) although they are disabled by default and must be manually enabled with a PRAGMA statement.[[32]](./SQLite#cite_note-33)

 

[Stored procedures](./Stored_procedure) are not supported; this is an explicit choice by the developers to favor simplicity, as the typical use case of SQLite is to be embedded inside a host application that can define its own procedures around the database.[[33]](./SQLite#cite_note-34)

 

SQLite does not have full [Unicode](./Unicode) support by default for backwards compatibility and due to the size of the Unicode tables, which are larger than the SQLite library.[[34]](./SQLite#cite_note-35) Full support for [Unicode](./Unicode) case-conversions can be enabled through an optional extension.[[35]](./SQLite#cite_note-36)

 

SQLite supports [full-text search](./Full-text_search) through its FTS5 loadable extension, which allows users to efficiently search for a keyword in a large number of documents similar to how [search engines](./Search_engine) search webpages.[[36]](./SQLite#cite_note-37)

 

SQLite includes support for working with [JSON](./JSON) through its *json1* extension, which is enabled by default since 2021. SQLite's JSON functions can handle JSON5 syntax since 2023. In 2024, SQLite added support for JSONB, a binary serialization of SQLite's internal representation of JSON. Using JSONB allows applications to avoid having to parse the JSON text each time it is processed and saves a small amount of disk space.[[37]](./SQLite#cite_note-38)

 

In May 2025, the 25th‑anniversary release SQLite 3.50.0 introduced additional features, including new Unicode functions (`unistr()` and `unistr_quote()`), a new API (`sqlite3_setlk_timeout()`) for setting lock timeouts, improved command‑line tools and rsync utility enhancements, and optimized JSONB.[[38]](./SQLite#cite_note-39)

 

The maximum supported size for an SQLite database file is 281 terabytes.[[39]](./SQLite#cite_note-40)

 

SQLite normally stores every table and index in a SQLite database in a single ordinary disk file. Alternatively, SQLite can be told to keep a SQL database entirely in memory as an [in-memory database](./In-memory_database) with the `:memory:` connection string.[[40]](./SQLite#cite_note-41)

 

## Development and distribution

 

SQLite's code is hosted with [Fossil](./Fossil_(software)), a [distributed version control system](./Distributed_version_control_system) that uses SQLite as a local cache for its non-relational database format, and SQLite's SQL as an implementation language.[[41]](./SQLite#cite_note-42)[[42]](./SQLite#cite_note-43)

 

SQLite is [public domain](./Public-domain_software), but not "open-contribution", with the website stating "the project does not accept patches from people who have not submitted an [affidavit](./Affidavit) dedicating their contribution into the public domain."[[43]](./SQLite#cite_note-44) Instead of a [code of conduct](./Code_of_conduct), the founders have adopted a [code of ethics](./Ethical_code) based on chapter 4 of the [Rule of St. Benedict](./Rule_of_Saint_Benedict).[[44]](./SQLite#cite_note-45)

 

A standalone [command-line](./Console_application) [shell](./Shell_(computing)) program called *sqlite3*[[45]](./SQLite#cite_note-46) is provided in SQLite's distribution. It can be used to create a database, define tables, insert and change rows, run queries and manage an SQLite database file. It also serves as an example for writing applications that use the SQLite library.

 

SQLite uses automated [regression testing](./Regression_testing) prior to each release. Over 2 million tests are run as part of a release's verification. The SQLite library has 156,000 lines of source code, while all the test suites combined add up to 92 million lines of test code. SQLite's tests simulate a number of exceptional scenarios, such as power loss and I/O errors, in addition to testing the library's functionality. Starting with the August 10, 2009 release of SQLite 3.6.17, SQLite releases have 100% branch test coverage, one of the components of [code coverage](./Code_coverage). SQLite has four different [test harnesses](./Test_harness): the original public-domain TCL tests, the proprietary C-language TH3 test suite, the SQL Logic Tests, which check SQLite against other SQL databases, and the dbsqlfuzz proprietary [fuzzing](./Fuzzing) engine.[[46]](./SQLite#cite_note-tests-47)

 

## Notable uses

 

### Operating systems

 

SQLite is included by default in:

 
- [Android](./Android_(operating_system))[[14]](./SQLite#cite_note-CoRecursive-interview-14)[[47]](./SQLite#cite_note-48)
- [BlackBerry Tablet OS](./BlackBerry_Tablet_OS)[[48]](./SQLite#cite_note-Blackberry,_GitHub-49)
- [iOS](./IOS)[[13]](./SQLite#cite_note-:0-13)
- [Mac OS X 10.4](./Mac_OS_X_10.4) onwards (Apple adopted it as an option in [macOS](./MacOS)'s [Core Data](./Core_Data) API from the original implementation)[[13]](./SQLite#cite_note-:0-13)
- [NetBSD](./NetBSD)[[49]](./SQLite#cite_note-50)
- [NixOS](./NixOS) where it is used by the [Nix](./Nix_(package_manager)) core package management system[[50]](./SQLite#cite_note-51)
- [OpenBSD](./OpenBSD), which supports exporting [ports tree](./Ports_collection) metadata as an SQLite database[[51]](./SQLite#cite_note-52)
- [RPM](./RPM_Package_Manager) based [Linux distributions](./Linux_distribution) (including [Red Hat Enterprise Linux](./Red_Hat_Enterprise_Linux) and its derivative [Fedora Linux](./Fedora_Linux)), where it is used by the core package management system[[52]](./SQLite#cite_note-53)
- [Windows 10](./Windows_10) onwards[[53]](./SQLite#cite_note-54)

 

### Middleware

 
- [ADO.NET](./ADO.NET) adapter, initially developed by Robert Simpson, is maintained jointly with the SQLite developers since April 2010.[[54]](./SQLite#cite_note-55)
- [ODBC](./ODBC) driver has been developed and is maintained separately by Christian Werner.[[55]](./SQLite#cite_note-56) Werner's ODBC driver is the recommended connection method for accessing SQLite from [OpenOffice.org](./OpenOffice.org).[[56]](./SQLite#cite_note-57)
- [COM](./Component_Object_Model) ([ActiveX](./ActiveX)) wrapper making SQLite accessible on Windows to scripted languages such as [JScript](./JScript) and [VBScript](./VBScript). This adds SQLite database capabilities to [HTML Applications](./HTML_Application) (HTA).[[57]](./SQLite#cite_note-58)

 

### Web browsers

 
- The browsers [Google Chrome](./Google_Chrome), [Opera](./Opera_(web_browser)), [Safari](./Safari_(web_browser)) and the [Android Browser](./Android_Browser) all allow for storing information in, and retrieving it from, an SQLite database within the browser, using the official SQLite Wasm ([WebAssembly](./WebAssembly)) build,[[58]](./SQLite#cite_note-59) or using the [Web SQL Database](./Web_SQL_Database) technology, although the latter is becoming deprecated (namely superseded by SQLite Wasm or by [IndexedDB](./IndexedDB)). Internally, [Chromium](./Chromium_(web_browser)) based browsers use SQLite databases for storing configuration data like site visit history, cookies, download history etc.[[59]](./SQLite#cite_note-60)
- [Mozilla Firefox](./Mozilla_Firefox) and [Mozilla Thunderbird](./Mozilla_Thunderbird) store a variety of configuration data (bookmarks, cookies, contacts etc.) in internally managed SQLite databases. Until Firefox version 57 (["Firefox Quantum"](./History_of_Firefox#Firefox_57)), there was a third-party add-on that used the API supporting this functionality to provide a user interface for managing arbitrary SQLite databases.[[60]](./SQLite#cite_note-61)
- Several third-party add-ons can make use of [JavaScript](./JavaScript) APIs to manage SQLite databases.[[61]](./SQLite#cite_note-62)[[62]](./SQLite#cite_note-63)

 

### Web application frameworks

 
- [Symfony](./Symfony)
- [Laravel](./Laravel)
- [Bugzilla](./Bugzilla)
- [Django](./Django_(web_framework))'s default database management system
- [Drupal](./Drupal)
- [Trac](./Trac)
- [Ruby on Rails](./Ruby_on_Rails)'s default database management system
- [web2py](./Web2py)

 

### Others

 
- [Adobe Systems](./Adobe_Systems) uses SQLite as its file format in [Adobe Lightroom](./Adobe_Lightroom), a standard database in [Adobe AIR](./Adobe_AIR), and internally within [Adobe Acrobat Reader](./Adobe_Acrobat_Reader).[[13]](./SQLite#cite_note-:0-13)
- [Apple Photos](./Photos_(Apple)) uses SQLite internally.[[63]](./SQLite#cite_note-apple-photos-64)
- [Audacity](./Audacity_(audio_editor)) uses SQLite as its file format, as of version 3.0.0.[[64]](./SQLite#cite_note-audacity-65)
- [Evernote](./Evernote) uses SQLite to store its local database repository in Windows.
- [Skype](./Skype)[[65]](./SQLite#cite_note-skype-66)
- [WhatsApp](./WhatsApp)[[66]](./SQLite#cite_note-WhatsApp-67)
- The Service Management Facility, used for service management within the [Solaris](./Solaris_(operating_system)) and [OpenSolaris](./OpenSolaris) operating systems
- [Dropbox](./Dropbox) client software[[13]](./SQLite#cite_note-:0-13)
- [Intuit](./Intuit) uses SQLite in [QuickBooks](./QuickBooks) and [TurboTax](./TurboTax)[[13]](./SQLite#cite_note-:0-13)
- [McAfee Antivirus](./McAfee_Antivirus)[[13]](./SQLite#cite_note-:0-13)
- [Flame (malware)](./Flame_(malware))
- [BMW iDrive](./BMW_iDrive) [satellite navigation](./Satellite_navigation) system
- [TomTom](./TomTom) GPS systems, for the [NDS](./Navigation_Data_Standard) map data
- [Proxmox VE](./Proxmox_Virtual_Environment) - *Proxmox Cluster File System* ([pmxcfs](https://pve.proxmox.com/wiki/Proxmox_Cluster_File_System_(pmxcfs)))
- [Bentley Systems](./Bentley_Systems) [MicroStation](./MicroStation)[[13]](./SQLite#cite_note-:0-13)
- [Bosch](./Bosch_(company)) car multimedia systems[[13]](./SQLite#cite_note-:0-13)
- [Airbus A350](./Airbus_A350) flight system[[13]](./SQLite#cite_note-:0-13)
- [Quicken Essentials](./Quicken#History_of_Quicken_on_Mac) and later versions of Quicken for Mac[[67]](./SQLite#cite_note-68)
- [Python](./Python_(programming_language)) standard library[[68]](./SQLite#cite_note-69)
- [Xojo](./Xojo) IDE[[13]](./SQLite#cite_note-:0-13)
- [Wine](./Wine_(software))[[69]](./SQLite#cite_note-70)

 

## See also

 
- ![](//upload.wikimedia.org/wikipedia/commons/thumb/3/31/Free_and_open-source_software_logo_%282009%29.svg/40px-Free_and_open-source_software_logo_%282009%29.svg.png)[Free and open-source software portal](./Portal:Free_and_open-source_software)

 
- [Ordered key–value store](./Ordered_key–value_store)
- [Comparison of relational database management systems](./Comparison_of_relational_database_management_systems)
- [List of relational database management systems](./List_of_relational_database_management_systems)
- [MySQL](./MySQL)
- [SpatiaLite](./SpatiaLite)

 

## Notes

  
1. [↑](./SQLite#cite_ref-15) SQLite's B-tree implementation was originally adapted from [The Art of Computer Programming](./The_Art_of_Computer_Programming).[[14]](./SQLite#cite_note-CoRecursive-interview-14)

 

## References

 

### Citations

 
1. [↑](./SQLite#cite_ref-wikidata-1e9a4cc2e95d3d83e98a97ab5c740f03e028ebb7-v20_1-0) ["SQLite Release 3.53.2 On 2026-06-03"](https://sqlite.org/releaselog/3_53_2.html). 3 June 2026. Retrieved 4 June 2026.
2. [↑](./SQLite#cite_ref-license_2-0) ["SQLite Copyright"](https://sqlite.org/copyright.html). sqlite.org. Retrieved May 17, 2010.
3. [↑](./SQLite#cite_ref-3) ["SQLite database file format media type at IANA"](https://www.iana.org/assignments/media-types/application/vnd.sqlite3). *[Internet Assigned Numbers Authority](./Internet_Assigned_Numbers_Authority)*. [IANA](./Internet_Assigned_Numbers_Authority). Retrieved 2019-03-08.
4. [↑](./SQLite#cite_ref-4) ["Why SQLite succeeded as a database — Richard Hipp, creator of SQLite"](https://changelog.com/podcast/201). *The Changelog*. Episode 201.  Event occurs at 00:16:00. [Archived](https://web.archive.org/web/20220707033506/https://changelog.com/podcast/201) from the original on 2022-07-07. Retrieved 2025-04-11. How do I pronounce the name of the product? I say S-Q-L-ite, like a mineral.
5. [↑](./SQLite#cite_ref-5) [D. Richard Hipp](./D._Richard_Hipp) (presenter) (May 31, 2006). [*An Introduction to SQLite*](https://www.youtube.com/watch?v=f428dSRkTs4#t=1m14s) (video). Google Inc.  Event occurs at 00:01:14. Retrieved March 23, 2010. [ˌɛsˌkjuˌwəlˈaɪt̚]
6. [↑](./SQLite#cite_ref-6) [D. Richard Hipp](./D._Richard_Hipp) (presenter) (May 31, 2006). [*An Introduction to SQLite*](https://www.youtube.com/watch?v=f428dSRkTs4#t=48m15s). Google Inc.  Event occurs at 00:48:15. Retrieved March 23, 2010. [ˈsikwəˌlaɪt̚]
7. [↑](./SQLite#cite_ref-7) ["Most Widely Deployed SQL Database Estimates"](https://sqlite.org/mostdeployed.html). SQLite.org. Retrieved May 11, 2011.
8. [↑](./SQLite#cite_ref-Owens_2006_8-0) Owens, Michael (2006). ["Chapter 4: SQL"](https://books.google.com/books?id=VsZ5bUh0XAkC&pg=PA133). In Gilmore, Jason; [Thomas, Keir](./Keir_Thomas) (eds.). *The Definitive Guide to SQLite*. [D. Richard Hipp](./D._Richard_Hipp) (foreword), Preston Hagar (technical reviewer). [Apress](./Apress). p. 133. [ISBN](./ISBN_(identifier)) [978-1-59059-673-9](./Special:BookSources/978-1-59059-673-9). [Archived](https://web.archive.org/web/20201124002058/https://books.google.com/books?id=VsZ5bUh0XAkC&pg=PA133) from the original on 24 November 2020. Retrieved 30 December 2014.
9. [↑](./SQLite#cite_ref-9) ["STRICT Tables"](https://sqlite.org/stricttables.html). [Archived](https://web.archive.org/web/20220807204905/https://sqlite.org/stricttables.html) from the original on 2022-08-07. Retrieved 2022-08-11.
10. [↑](./SQLite#cite_ref-10) ["Full-Featured SQL"](https://www.sqlite.org/fullsql.html). *SQLite*. Retrieved January 24, 2025.
11. [↑](./SQLite#cite_ref-11) ["SQL Features That SQLite Does Not Implement"](https://www.sqlite.org/omitted.html). *SQLite*. Retrieved January 24, 2025.
12. [1](./SQLite#cite_ref-Owens06_12-0) [2](./SQLite#cite_ref-Owens06_12-1) Owens, Michael (2006). "Introducing SQLite". *The Definitive Guide to SQLite*. [Apress](./Apress). pp. 1–16. [doi](./Doi_(identifier)):[10.1007/978-1-4302-0172-4_1](https://doi.org/10.1007%2F978-1-4302-0172-4_1). [ISBN](./ISBN_(identifier)) [978-1-59059-673-9](./Special:BookSources/978-1-59059-673-9).
13. [1](./SQLite#cite_ref-:0_13-0) [2](./SQLite#cite_ref-:0_13-1) [3](./SQLite#cite_ref-:0_13-2) [4](./SQLite#cite_ref-:0_13-3) [5](./SQLite#cite_ref-:0_13-4) [6](./SQLite#cite_ref-:0_13-5) [7](./SQLite#cite_ref-:0_13-6) [8](./SQLite#cite_ref-:0_13-7) [9](./SQLite#cite_ref-:0_13-8) [10](./SQLite#cite_ref-:0_13-9) [11](./SQLite#cite_ref-:0_13-10) ["Well-Known Users Of SQLite"](https://sqlite.org/famous.html). SQLite. [Archived](https://web.archive.org/web/20150711135311/https://sqlite.org/famous.html) from the original on July 11, 2015. Retrieved August 5, 2015.
14. [1](./SQLite#cite_ref-CoRecursive-interview_14-0) [2](./SQLite#cite_ref-CoRecursive-interview_14-1) Bell, Adam. ["The Untold Story of SQLite"](https://corecursive.com/066-sqlite-with-richard-hipp/). *Corecursive*. Retrieved 16 November 2025.
15. [↑](./SQLite#cite_ref-unql-interview_16-0) ["Interview: Richard Hipp on UnQL, a New Query Language for Document Databases"](http://www.infoq.com/news/2011/08/UnQL). InfoQ. August 4, 2011. [Archived](https://web.archive.org/web/20140408215240/http://www.infoq.com/news/2011/08/UnQL) from the original on April 8, 2014. Retrieved October 5, 2011.
16. [↑](./SQLite#cite_ref-17) ["LoC Recommended Storage Format"](https://sqlite.org/locrsf.html). *sqlite.org*. [Archived](https://web.archive.org/web/20200423212849/https://sqlite.org/locrsf.html) from the original on 2020-04-23. Retrieved 2020-04-09.
17. [↑](./SQLite#cite_ref-18) ["SQLite, Version 3"](https://www.loc.gov/preservation/digital/formats/fdd/fdd000461.shtml). *www.loc.gov*. 2017-03-28. [Archived](https://web.archive.org/web/20200511194518/https://www.loc.gov/preservation/digital/formats/fdd/fdd000461.shtml) from the original on 2020-05-11. Retrieved 2020-04-09.
18. [↑](./SQLite#cite_ref-19) ["Recommended Formats Statement – datasets/databases"](https://www.loc.gov/preservation/resources/rfs/data.html). Library of Congress. [Archived](https://web.archive.org/web/20180822113435/https://www.loc.gov/preservation/resources/rfs/data.html) from the original on 2018-08-22. Retrieved 2020-04-09.
19. [↑](./SQLite#cite_ref-20) ["SQLite Is A Zero-Configuration Database"](https://sqlite.org/zeroconf.html). SQLite.org. [Archived](https://web.archive.org/web/20240502210736/https://sqlite.org/zeroconf.html) from the original on May 2, 2024. Retrieved August 3, 2015.
20. [1](./SQLite#cite_ref-:2_21-0) [2](./SQLite#cite_ref-:2_21-1) ["SQLite"](https://clickhouse.com/docs/en/engines/database-engines/sqlite). *ClickHouse Docs*. Retrieved January 25, 2025.
21. [↑](./SQLite#cite_ref-22) ["Write Ahead Logging in SQLite 3.7"](https://sqlite.org/wal.html). SQLite.org. [Archived](https://web.archive.org/web/20240502210711/https://sqlite.org/wal.html) from the original on May 2, 2024. Retrieved September 3, 2011. WAL provides more concurrency as readers do not block writers and a writer does not block readers. Reading and writing can proceed concurrently.
22. [↑](./SQLite#cite_ref-23) ["Appropriate Uses For SQLite"](https://sqlite.org/whentouse.html). SQLite.org. [Archived](https://web.archive.org/web/20240502210713/https://sqlite.org/whentouse.html) from the original on 2024-05-02. Retrieved 2015-09-03.
23. [↑](./SQLite#cite_ref-24) Berkus, Josh (4 June 2014). ["PGCon 2014: Clustering and VODKA"](https://lwn.net/Articles/601144/). *Lwn.net*. [Archived](https://web.archive.org/web/20150629195442/https://lwn.net/Articles/601144/) from the original on 2015-06-29. Retrieved 2017-01-06.
24. [↑](./SQLite#cite_ref-25) ["PGCon2014: SQLite: Protégé of PostgreSQL"](https://www.pgcon.org/2014/schedule/events/736.en.html). *Pgcon.org*. 20 September 2015. [Archived](https://web.archive.org/web/20141230193958/http://www.pgcon.org/2014/schedule/events/736.en.html) from the original on 2014-12-30. Retrieved 2017-01-06.
25. [↑](./SQLite#cite_ref-:1_26-0) ["SQLite: StrictMode"](https://sqlite.org/src/wiki?name=StrictMode). *Sqlite.org*. [Archived](https://web.archive.org/web/20160304115940/https://sqlite.org/src/wiki?name=StrictMode) from the original on March 4, 2016. Retrieved September 3, 2015.
26. [↑](./SQLite#cite_ref-27) ["Release History of SQLite"](https://sqlite.org/changes.html). [Archived](https://web.archive.org/web/20210316043517/https://sqlite.org/changes.html) from the original on 2021-03-16. Retrieved 2021-03-22.
27. [↑](./SQLite#cite_ref-28) ["STRICT Tables"](https://sqlite.org/stricttables.html). *SQLite*. Retrieved January 24, 2025.
28. [↑](./SQLite#cite_ref-29) ["SQL As Understood By SQLite"](https://sqlite.org/lang_createtable.html#rowid). *SQLite*. [Archived](https://web.archive.org/web/20180521104530/https://sqlite.org/lang_createtable.html#rowid) from the original on 21 May 2018. Retrieved 21 May 2018. Searching for a record with a specific rowid, or for all records with rowids within a specified range is around twice as fast as a similar search made by specifying any other PRIMARY KEY or indexed value.
29. [↑](./SQLite#cite_ref-30) ["Clustered Indexes and the WITHOUT ROWID Optimization"](https://sqlite.org/withoutrowid.html). *SQLite*. Retrieved January 24, 2025.
30. [↑](./SQLite#cite_ref-31) Karwin, Bill (May 2010). Carter, Jacquelyn (ed.). *SQL Antipatterns: Avoiding the Pitfalls of Database Programming*. The Pragmatic Bookshelf. p. 70. [ISBN](./ISBN_(identifier)) [978-1-934356-55-5](./Special:BookSources/978-1-934356-55-5). Sometimes you're forced to use a database brand that doesn't support foreign key constraints (for example MySQL's MyISAM storage engine or SQLite prior to version 3.6.19).
31. [↑](./SQLite#cite_ref-32) ["SQLite Release 3.6.19 On 2009-10-14"](https://sqlite.org/releaselog/3_6_19.html). *sqlite.org*. [Archived](https://web.archive.org/web/20201029060401/http://sqlite.org/releaselog/3_6_19.html) from the original on 2020-10-29. Retrieved 2020-10-15.
32. [↑](./SQLite#cite_ref-33) ["SQLite Foreign Key Support"](https://sqlite.org/foreignkeys.html). *SQLite*. Retrieved January 24, 2025.
33. [↑](./SQLite#cite_ref-34) Source: developers' comments on [SQLite forum](https://sqlite.org/forum/info/78a60bdeec7c1ee9) [Archived](https://web.archive.org/web/20230401220416/https://sqlite.org/forum/info/78a60bdeec7c1ee9) 2023-04-01 at the [Wayback Machine](./Wayback_Machine)
34. [↑](./SQLite#cite_ref-35) ["Quirks, Caveats, and Gotchas In SQLite"](https://sqlite.org/quirks.html). *SQLite*. Retrieved January 24, 2025.
35. [↑](./SQLite#cite_ref-36) ["Case-insensitive matching of Unicode characters does not work"](https://sqlite.org/faq.html#q18). *SQLite Frequently Asked Questions*. [Archived](https://web.archive.org/web/20150905054749/https://sqlite.org/faq.html#q18) from the original on 2015-09-05. Retrieved 2015-09-03.
36. [↑](./SQLite#cite_ref-37) ["SQLite FTS5 Extension"](https://sqlite.org/fts5.html). *SQLite*. Retrieved January 24, 2025.
37. [↑](./SQLite#cite_ref-38) ["JSON Functions And Operators"](https://sqlite.org/json1.html). *SQLite*. Retrieved January 24, 2025.
38. [↑](./SQLite#cite_ref-39) ["SQLite Release 3.50.0 On 2025-05-29"](https://sqlite.org/releaselog/3_50_0.html). *SQLite*. Retrieved November 3, 2025.
39. [↑](./SQLite#cite_ref-40) ["Limits In SQLite"](https://sqlite.org/limits.html). *SQLite.org*. [Archived](https://web.archive.org/web/20211107064937/https://sqlite.org/limits.html) from the original on 2021-11-07. Retrieved 2022-09-19.
40. [↑](./SQLite#cite_ref-41)  ["In-Memory Databases"](http://www.sqlite.org/inmemorydb.html). *www.sqlite.org*. 
41. [↑](./SQLite#cite_ref-42) ["Thoughts On The Design Of The Fossil DVCS"](https://www.fossil-scm.org/home/doc/trunk/www/theory1.wiki). Fossil-scm.org. July 12, 2017. [Archived](https://web.archive.org/web/20221013234319/https://www.fossil-scm.org/home/doc/trunk/www/theory1.wiki) from the original on October 13, 2022. Retrieved October 14, 2022.
42. [↑](./SQLite#cite_ref-43) ["Fossil: Fossil Performance"](https://www.fossil-scm.org/index.html/doc/tip/www/stats.wiki). Fossil-scm.org. August 23, 2009. [Archived](https://web.archive.org/web/20091009054952/http://www.fossil-scm.org/index.html/doc/tip/www/stats.wiki) from the original on October 9, 2009. Retrieved September 12, 2009.
43. [↑](./SQLite#cite_ref-44) ["SQLite Copyright"](https://sqlite.org/copyright.html). *sqlite.org*. [Archived](https://web.archive.org/web/20240315172355/https://sqlite.org/copyright.html) from the original on 2024-03-15. Retrieved 2024-03-06.
44. [↑](./SQLite#cite_ref-45) ["Code Of Ethics"](https://sqlite.org/codeofethics.html). *sqlite.org*. [Archived](https://web.archive.org/web/20240219225117/https://sqlite.org/codeofethics.html) from the original on 2024-02-19. Retrieved 2024-03-06.
45. [↑](./SQLite#cite_ref-46) ["Command Line Shell For SQLite"](https://sqlite.org/cli.html). Sqlite.org. [Archived](https://web.archive.org/web/20221006104551/https://sqlite.org/cli.html) from the original on October 6, 2022. Retrieved October 14, 2022.
46. [↑](./SQLite#cite_ref-tests_47-0) ["How SQLite Is Tested"](https://sqlite.org/testing.html). SQLite.org. [Archived](https://web.archive.org/web/20091006224147/https://sqlite.org/testing.html) from the original on October 6, 2009. Retrieved September 12, 2009.
47. [↑](./SQLite#cite_ref-48) ["android.database.sqlite"](https://developer.android.com/reference/android/database/sqlite/package-summary). *Android Developers*. Retrieved 23 April 2026.
48. [↑](./SQLite#cite_ref-Blackberry,_GitHub_49-0) ["Open Source Components for the Native SDK for BlackBerry Tablet OS"](https://web.archive.org/web/20130127102233/http://blackberry.github.com/ndk/components.html). Archived from [the original](https://blackberry.github.com/ndk/components.html) on 2013-01-27. Retrieved 2017-09-19.
49. [↑](./SQLite#cite_ref-50) ["sqlite3(1) - NetBSD Manual Pages"](https://man.netbsd.org/sqlite3.1). *man.netbsd.org*. NetBSD. Retrieved 23 April 2026.
50. [↑](./SQLite#cite_ref-51) ["Prerequisites"](https://nix.dev/manual/nix/2.28/installation/prerequisites-source.html). *nix.dev*. NixOS. Retrieved 23 April 2026.
51. [↑](./SQLite#cite_ref-52) ["ports(7) - OpenBSD manual pages"](https://man.openbsd.org/ports). *man.openbsd.org*. OpenBSD. Retrieved 23 April 2026.
52. [↑](./SQLite#cite_ref-53) ["RPM Database Recovery"](https://rpm.org/user_doc/db_recovery.html). *rpm.org*. Retrieved 23 April 2026.
53. [↑](./SQLite#cite_ref-54) ["To use the version of SQLite that is installed with Windows"](https://docs.microsoft.com/en-us/windows/uwp/data-access/sqlite-databases#to-use-the-version-of-sqlite-that-is-installed-with-windows). 20 October 2022. [Archived](https://web.archive.org/web/20220331170828/https://docs.microsoft.com/en-us/windows/uwp/data-access/sqlite-databases#to-use-the-version-of-sqlite-that-is-installed-with-windows) from the original on 31 March 2022. Retrieved 31 March 2022.
54. [↑](./SQLite#cite_ref-55) ["Home"](http://system.data.sqlite.org/index.html/doc/trunk/www/index.wiki). *System.Data.SQLite*. 2016-12-30. [Archived](https://web.archive.org/web/20140713080835/http://system.data.sqlite.org/index.html/doc/trunk/www/index.wiki) from the original on 2014-07-13. Retrieved 2017-01-06.
55. [↑](./SQLite#cite_ref-56) ["SQLite ODBC Driver"](http://www.ch-werner.de/sqliteodbc/). *Ch-werner.de*. 2016-12-01. [Archived](https://web.archive.org/web/20140626165719/http://www.ch-werner.de/sqliteodbc/) from the original on 2014-06-26. Retrieved 2017-01-06.
56. [↑](./SQLite#cite_ref-57) ["Using SQLite Database with OpenOffice.org : Version 2.0"](http://documentation.openoffice.org/HOW_TO/data_source/SQLite.pdf) (PDF). *Documentation.openoffice.org*. [Archived](https://web.archive.org/web/20110928073029/http://documentation.openoffice.org/HOW_TO/data_source/SQLite.pdf) (PDF) from the original on 2011-09-28. Retrieved 2017-01-06.
57. [↑](./SQLite#cite_ref-58) ["sqlite — Sqlite Wrappers"](https://sqlite.org/cvstrac/wiki?p=SqliteWrappers). SQLite.org. February 7, 2009. [Archived](https://web.archive.org/web/20090205225756/http://sqlite.org/cvstrac/wiki?p=SqliteWrappers) from the original on February 5, 2009. Retrieved February 7, 2009.
58. [↑](./SQLite#cite_ref-59) ["sqlite3 WebAssembly & JavaScript Documentation Index"](https://sqlite.org/wasm). *SQLite*. [Archived](https://web.archive.org/web/20240502210710/https://sqlite.org/wasm/doc/trunk/index.md) from the original on 2024-05-02. Retrieved 2023-05-08.
59. [↑](./SQLite#cite_ref-60) ["Location of Google Chrome history"](https://www.foxtonforensics.com/browser-history-examiner/chrome-history-location). *www.foxtonforensics.com*. 2020-10-06. [Archived](https://web.archive.org/web/20230228184524/https://www.foxtonforensics.com/browser-history-examiner/chrome-history-location) from the original on 2023-02-28. Retrieved 2020-10-06.
60. [↑](./SQLite#cite_ref-61) ["SQLite Manager :: Add-ons for Firefox"](https://web.archive.org/web/20170102010658/https://addons.mozilla.org/en-US/firefox/addon/sqlite-manager/). *Addons.mozilla.org*. 2015-02-28. Archived from [the original](https://addons.mozilla.org/en-US/firefox/addon/sqlite-manager/) on 2017-01-02. Retrieved 2017-01-06.
61. [↑](./SQLite#cite_ref-62) ["SQLite Manager – Get this Extension for 🦊 Firefox (en-US)"](https://addons.mozilla.org/en-US/firefox/addon/sqlite-manager-webext/). *Addons.mozilla.org*. 2018-07-24. [Archived](https://web.archive.org/web/20181005112443/https://addons.mozilla.org/en-US/firefox/addon/sqlite-manager-webext/) from the original on 2018-10-05. Retrieved 2018-10-05.
62. [↑](./SQLite#cite_ref-63) ["SQLite Reader – Get this Extension for 🦊 Firefox (en-US)"](https://addons.mozilla.org/en-US/firefox/addon/sql-reader/). *Addons.mozilla.org*. 2018-09-01. [Archived](https://web.archive.org/web/20181005112536/https://addons.mozilla.org/en-US/firefox/addon/sql-reader/) from the original on 2018-10-05. Retrieved 2018-10-05.
63. [↑](./SQLite#cite_ref-apple-photos_64-0) ["Using SQL to find my best photo of a pelican according to Apple Photo"](https://simonwillison.net/2020/May/21/dogsheep-photos/). *Simon Willison’s Weblog*. [Archived](https://web.archive.org/web/20200522181550/https://simonwillison.net/2020/May/21/dogsheep-photos/) from the original on May 22, 2020. Retrieved May 23, 2020.
64. [↑](./SQLite#cite_ref-audacity_65-0) ["Audacity 3.0.0 Released"](https://web.archive.org/web/20230814021313/https://www.audacityteam.org/audacity-3-0-0-released/). 17 March 2021. Archived from [the original](https://www.audacityteam.org/audacity-3-0-0-released/) on 14 August 2023. Retrieved March 17, 2021.
65. [↑](./SQLite#cite_ref-skype_66-0) Hinegardner, Jeremy (August 28, 2007). ["Skype client using SQLite?"](https://web.archive.org/web/20071117061133/https://www.mail-archive.com/sqlite-users%40sqlite.org/msg27326.html). *sqlite-users* (Mailing list). Archived from [the original](https://www.mail-archive.com/sqlite-users%40sqlite.org/msg27326.html) on 2007-11-17. Retrieved June 14, 2010.
66. [↑](./SQLite#cite_ref-WhatsApp_67-0) ["WhatsApp in Plain Sight: Where and How You Can Collect Forensic Artifacts"](https://www.group-ib.com/blog/whatsapp-forensic-artifacts/). *www.group-ib.com*. 7 November 2019. Retrieved 29 September 2025.
67. [↑](./SQLite#cite_ref-68) ["Addendum: Project Years of Expenses With Quicken for Mac"](https://frugalvagabond.com/addendum-project-years-of-expenses-with-quicken-for-mac/). *The Frugal Vagabond*.
68. [↑](./SQLite#cite_ref-69) ["sqlite3 — DB-API 2.0 interface for SQLite databases"](https://docs.python.org/library/sqlite3). *The Python Standard Library Documentation*.
69. [↑](./SQLite#cite_ref-70) ["Wine 11.9 Released"](https://www.winehq.org/news/2026051501). *WineHQ*. 15 May 2026. Retrieved 19 May 2026.

 

### Sources

  
- Allen, Grant; Owens, Mike (November 5, 2010). [*The Definitive Guide to SQLite*](https://web.archive.org/web/20101230035043/http://apress.com/book/view/1430232250) (2nd ed.). [Apress](./Apress). p. 368. [ISBN](./ISBN_(identifier)) [978-1-4302-3225-4](./Special:BookSources/978-1-4302-3225-4). Archived from [the original](http://apress.com/book/view/1430232250) on December 30, 2010. Retrieved December 23, 2010.
- Kreibich, Jay A. (August 17, 2010). [*Using SQLite*](http://oreilly.com/catalog/9780596521196) (1st ed.). [O'Reilly Media](./O'Reilly_Media). p. 528. [ISBN](./ISBN_(identifier)) [978-0-596-52118-9](./Special:BookSources/978-0-596-52118-9). [Archived](https://web.archive.org/web/20101225102001/http://oreilly.com/catalog/9780596521196) from the original on December 25, 2010. Retrieved December 23, 2010.
- Newman, Chris (November 9, 2004). [*SQLite (Developer's Library)*](http://www.informit.com/store/product.aspx?isbn=067232685X) (1st ed.). [Sams](./Sams). p. 336. [ISBN](./ISBN_(identifier)) [0-672-32685-X](./Special:BookSources/0-672-32685-X). [Archived](https://web.archive.org/web/20120114075902/http://www.informit.com/store/product.aspx?isbn=067232685X) from the original on January 14, 2012. Retrieved May 12, 2010.

  

## Further reading

 
- Gaffney, Kevin P; Prammer, Martin; Brasfield, Larry; Hipp, D Richard; Kennedy, Dan; Patel, Jignesh M (2022-08-01). ["SQLite: past, present, and future"](https://dl.acm.org/doi/10.14778/3554821.3554842). *Proceedings of the VLDB Endowment*. **15** (12): 3535–3547. [doi](./Doi_(identifier)):[10.14778/3554821.3554842](https://doi.org/10.14778%2F3554821.3554842).

 

## External links

   [![Wikimedia Commons logo](//upload.wikimedia.org/wikipedia/en/thumb/4/4a/Commons-logo.svg/40px-Commons-logo.svg.png)](./File:Commons-logo.svg) Wikimedia Commons has media related to [SQLite](https://commons.wikimedia.org/wiki/Category:SQLite).  
- [Official website](https://sqlite.org) [![Edit this at Wikidata](//upload.wikimedia.org/wikipedia/en/thumb/8/8a/OOjs_UI_icon_edit-ltr-progressive.svg/20px-OOjs_UI_icon_edit-ltr-progressive.svg.png)](https://www.wikidata.org/wiki/Q319417#P856)
- ["The Untold Story of SQLite"](https://corecursive.com/066-sqlite-with-richard-hipp/). CoRecursive.

 
| Authority control databases | GND |
| --- | --- |