---
source: https://en.wikipedia.org/wiki/LevelDB
fetched: 2026-06-19
---

Open-source key-value store by Google 
| LevelDB |
| --- |
| Developers | Jeffrey Dean,Sanjay Ghemawat,Google Inc. |
|  |
| Stable release | 1.23[1]/ 23 February 2021;5 years ago(23 February 2021) |
|  |
| Written in | C++ |
| Size | 350 kB (binary size) |
| Type | Database library |
| License | New BSD License |
| Website | github.com/google/leveldb |
| Repository | github.com/google/leveldb |

  

**LevelDB** is an [open-source](./Open-source_software) [on-disk key-value](./NoSQL#Classification_based_on_data_model) store written by [Google](./Google) fellows [Jeffrey Dean](./Jeff_Dean_(computer_scientist)) and [Sanjay Ghemawat](./Sanjay_Ghemawat).[[2]](./LevelDB#cite_note-jeffdean-2)[[3]](./LevelDB#cite_note-3) Inspired by [Bigtable](./Bigtable),[[4]](./LevelDB#cite_note-4) LevelDB source code is hosted on [GitHub](./GitHub) under the [New BSD License](./Modified_BSD_License) and has been ported to a variety of [Unix](./Unix)-based systems, [macOS](./MacOS), [Windows](./Microsoft_Windows), and [Android](./Android_(operating_system)).[[5]](./LevelDB#cite_note-leveldb_ports-5)

 

## Features

 

LevelDB stores keys and values in arbitrary byte arrays, and data is sorted by key. It supports batching writes, forward and backward iteration, and compression of the data via Google's [Snappy](./Snappy_(compression)) compression library.

 

LevelDB is not an [SQL](./SQL) database. Like other [NoSQL](./NoSQL) and [dbm](./DBM_(computing)) stores, it does not have a [relational data model](./Relational_data_model) and it does not support SQL queries. Also, it has no support for [indexes](./Index_(database)). Applications use LevelDB as a library, as it does not provide a server or command-line interface.

 

[MariaDB](./MariaDB) 10.0 comes with a storage engine which allows users to query LevelDB tables from MariaDB.[[6]](./LevelDB#cite_note-6)

 

## History

 

LevelDB is based on concepts from Google's [Bigtable](./Bigtable) database system. The table implementation for the Bigtable system was developed starting in about 2004, and is based on a different Google internal code base than the LevelDB code. That code base relies on a number of Google code libraries that are not themselves open sourced, so directly open sourcing that code would have been difficult. Jeff Dean and Sanjay Ghemawat wanted to create a system resembling the Bigtable tablet stack that had minimal dependencies and would be suitable for open sourcing, and also would be suitable for use in Chrome for the [IndexedDB](./IndexedDB) implementation. They wrote LevelDB starting in early 2011, with the same general design as the Bigtable tablet stack, but not sharing any of the code.[[7]](./LevelDB#cite_note-history-7)

 

## Usage

 

LevelDB is used as the backend database for [Google Chrome](./Google_Chrome)'s [IndexedDB](./IndexedDB) and is one of the supported backends for [Riak](./Riak).[[8]](./LevelDB#cite_note-8) Additionally, [Bitcoin Core](./Bitcoin_Core) and go-ethereum store the [blockchain](./Blockchain_(database)) metadata using a LevelDB database.[[9]](./LevelDB#cite_note-9) *[Minecraft](./Minecraft) Bedrock Edition* uses a modified version for chunk and entity data storage.[[10]](./LevelDB#cite_note-10) Autodesk AutoCAD 2016 also uses LevelDB.

 

## Performance

 

Google has provided benchmarks comparing LevelDB's performance to [SQLite](./SQLite) and [Kyoto Cabinet](./Kyoto_Cabinet) in different scenarios.[[11]](./LevelDB#cite_note-11) LevelDB outperforms both SQLite and Kyoto Cabinet in write operations and sequential-order read operations. LevelDB also excels at batch writes, but is slower than SQLite when dealing with large values. The currently published benchmarks were updated after SQLite configuration mistakes were noted in an earlier version of the results.[[12]](./LevelDB#cite_note-12) Updated benchmarks[[13]](./LevelDB#cite_note-13) show that LevelDB also outperforms [Berkeley DB](./Berkeley_DB), but these tests also show that [OpenLDAP](./OpenLDAP) [LightningDB](./Lightning_Memory-Mapped_Database) is much faster (~10 times in some scenarios) in read operations and some write types (e.g. batch and synchronous writes, see the link above), and is almost equal in the rest of the test.

 

All the above benchmarks date back from 2011 to 2014, and may only be of historical significance as SQLite, for instance, became significantly more efficient.[[14]](./LevelDB#cite_note-14)

 

## Bugs and reliability

 

LevelDB has a history of database corruption bugs.[[15]](./LevelDB#cite_note-15)[[16]](./LevelDB#cite_note-16)[[17]](./LevelDB#cite_note-17)[[18]](./LevelDB#cite_note-18)[[19]](./LevelDB#cite_note-19)[[20]](./LevelDB#cite_note-20) A study from 2014 has found that, on non-checksummed file systems, the database could become corrupted after a crash or power failure.[[21]](./LevelDB#cite_note-21)

 

## See also

 
- [Ordered Key-Value Store](./Ordered_Key-Value_Store)

 
- ![](//upload.wikimedia.org/wikipedia/commons/thumb/3/31/Free_and_open-source_software_logo_%282009%29.svg/40px-Free_and_open-source_software_logo_%282009%29.svg.png)[Free and open-source software portal](./Portal:Free_and_open-source_software)

 

## References

  
1. [↑](./LevelDB#cite_ref-wikidata-025bfdac0221dc86bbbaae46d0bff3160d4821d3-v20_1-0) ["Release 1.23"](https://github.com/google/leveldb/releases/tag/1.23). 23 February 2021. Retrieved 13 March 2021.
2. [↑](./LevelDB#cite_ref-jeffdean_2-0) ["Google Research Scientists and Engineers: Jeffrey Dean"](https://web.archive.org/web/20161119105302/http://research.google.com/people/jeff/). Google, Inc. Archived from [the original](http://research.google.com/people/jeff/) on 2016-11-19. Retrieved 2011-07-27.
3. [↑](./LevelDB#cite_ref-3) ["Research Scientists and Engineers: Sanjay Ghemawat"](https://web.archive.org/web/20161119222236/http://research.google.com/people/sanjay/). Google, Inc. Archived from [the original](http://research.google.com/people/sanjay/) on 2016-11-19. Retrieved 2011-07-27.
4. [↑](./LevelDB#cite_ref-4) ["Google Open-Sources NoSQL Database Called LevelDB"](https://web.archive.org/web/20110816070240/http://www.readwriteweb.com/hack/2011/07/google-open-sources-nosql-data.php). *[ReadWriteWeb](./ReadWriteWeb)*. July 30, 2011. Archived from [the original](http://www.readwriteweb.com/hack/2011/07/google-open-sources-nosql-data.php) on August 16, 2011. Retrieved July 30, 2011.
5. [↑](./LevelDB#cite_ref-leveldb_ports_5-0) ["Google Open Source Blog: LevelDB: A Fast Persistent Key-Value Store"](http://google-opensource.blogspot.com/2011/07/leveldb-fast-persistent-key-value-store.html). Google, Inc.
6. [↑](./LevelDB#cite_ref-6) [LevelDB storage engine](https://mariadb.com/kb/en/mariadb/leveldb/)
7. [↑](./LevelDB#cite_ref-history_7-0) Jeff Dean. ["LevelDB mailing list: "Current Status of LevelDB""](https://groups.google.com/d/msg/leveldb/Dby98QYzJqw/s5elVIkpIAUJ).
8. [↑](./LevelDB#cite_ref-8) [LevelDB](http://docs.basho.com/riak/latest/ops/advanced/backends/leveldb/). Docs.basho.com. Retrieved on 2013-09-18.
9. [↑](./LevelDB#cite_ref-9) Andreas M. Antonopoulos. ["Chapter 7. The Blockchain"](http://chimera.labs.oreilly.com/books/1234000001802/ch07.html?intcmp=il-na-books-videos-lp-bc15_20141218_radar_mastering_bitcoin_excerpt_chapter_seven). Retrieved 8 January 2015.
10. [↑](./LevelDB#cite_ref-10) ["Bedrock Edition level format"](https://minecraft.wiki/w/Bedrock_Edition_level_format). *Minecraft Wiki*. Retrieved 24 September 2023.
11. [↑](./LevelDB#cite_ref-11) ["LevelDB Benchmarks"](https://web.archive.org/web/20110820001028/http://leveldb.googlecode.com/svn/trunk/doc/benchmark.html). Google, Inc. Archived from [the original](http://leveldb.googlecode.com/svn/trunk/doc/benchmark.html) on 2011-08-20.
12. [↑](./LevelDB#cite_ref-12) ["LevelDB Benchmark discussion"](https://web.archive.org/web/20200224064040/http://sqlite.1065341.n5.nabble.com/LevelDB-benchmark-td62054.html). Archived from [the original](http://sqlite.1065341.n5.nabble.com/LevelDB-benchmark-td62054.html) on 2020-02-24. Retrieved 2014-08-11.
13. [↑](./LevelDB#cite_ref-13) [Database Microbenchmarks](http://symas.com/mdb/microbench/) [Archived](https://web.archive.org/web/20140809204443/http://symas.com/mdb/microbench/) 2014-08-09 at the [Wayback Machine](./Wayback_Machine), Symas Corp., 2012-09. Retrieved 22 October 2016
14. [↑](./LevelDB#cite_ref-14) ["Measuring and Reducing CPU Usage in SQLite"](https://www.sqlite.org/cpu.html).
15. [↑](./LevelDB#cite_ref-15) ["Repairing LevelDB"](https://web.archive.org/web/20160406082813/http://docs.basho.com/riak/latest/ops/running/recovery/repairing-leveldb/). Archived from [the original](https://docs.basho.com/riak/latest/ops/running/recovery/repairing-leveldb/) on 2016-04-06. Retrieved 2016-04-06.
16. [↑](./LevelDB#cite_ref-16) [Issues · google/leveldb · GitHub](https://github.com/google/leveldb/issues?utf8=%E2%9C%93&q=corrupt+is%3Aissue)
17. [↑](./LevelDB#cite_ref-17) [Unrecoverable corruption in Chromium](https://bugs.chromium.org/p/chromium/issues/detail?id=261623)
18. [↑](./LevelDB#cite_ref-18) [Corruption in syncthing](https://forum.syncthing.net/t/panic-leveldb-table-corruption-on-data-block/2526/23)
19. [↑](./LevelDB#cite_ref-19) [Corruption after power loss](https://github.com/google/leveldb/issues/333)
20. [↑](./LevelDB#cite_ref-20) [Corruption in Ethereum](http://ethereum.stackexchange.com/questions/1159/corruption-on-data-block-while-synchronising)
21. [↑](./LevelDB#cite_ref-21) [*All File Systems Are Not Created Equal: On the Complexity of Crafting Crash-Consistent Applications*](https://www.usenix.org/conference/osdi14/technical-sessions/presentation/pillai). 2014. pp. 433–448. [ISBN](./ISBN_(identifier)) [9781931971164](./Special:BookSources/9781931971164).

 

## External links

 
- [Official website](https://github.com/google/leveldb)

 
| vteGooglefree and open-source software |
| --- |
| Software | ApplicationsChromiumGemmaOpenRefineTesseractProgramming languagesCarbonDartGoSawzallFrameworks anddevelopment toolsAMPAngularAngularJSBeamBazelBlocklyBrotliClosure ToolsCpplintFlatBuffersFlutterGanetiGearsGerritGLOPgRPCGsonGuavaGuetzliGuicegVisorKubernetesLevelDBlibvpxLighthouseNaClNamebenchNomulusOR-ToolsPolymerProtocol BuffersTensorFlowV8Operating systemsAndroidChromiumOSFuchsiagLinuxGoobuntu | Applications | ChromiumGemmaOpenRefineTesseract | Programming languages | CarbonDartGoSawzall | Frameworks anddevelopment tools | AMPAngularAngularJSBeamBazelBlocklyBrotliClosure ToolsCpplintFlatBuffersFlutterGanetiGearsGerritGLOPgRPCGsonGuavaGuetzliGuicegVisorKubernetesLevelDBlibvpxLighthouseNaClNamebenchNomulusOR-ToolsPolymerProtocol BuffersTensorFlowV8 | Operating systems | AndroidChromiumOSFuchsiagLinuxGoobuntu |
| Applications | ChromiumGemmaOpenRefineTesseract |
| Programming languages | CarbonDartGoSawzall |
| Frameworks anddevelopment tools | AMPAngularAngularJSBeamBazelBlocklyBrotliClosure ToolsCpplintFlatBuffersFlutterGanetiGearsGerritGLOPgRPCGsonGuavaGuetzliGuicegVisorKubernetesLevelDBlibvpxLighthouseNaClNamebenchNomulusOR-ToolsPolymerProtocol BuffersTensorFlowV8 |
| Operating systems | AndroidChromiumOSFuchsiagLinuxGoobuntu |
| Related | Code-inGoogle LLC v. Oracle America, Inc.Open Source Security FoundationSummer of Code |