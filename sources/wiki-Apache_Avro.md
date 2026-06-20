---
source: https://en.wikipedia.org/wiki/Apache_Avro
fetched: 2026-06-19
---

Open-source remote procedure call framework 

 
| Apache Avro |
| --- |
|  |
| Developer | Apache Software Foundation |
| Release | 2November 2009;16 years ago(2009-11-02)[1] |
|  |
| Stable release | 1.12.1
   / October16, 2025;8 months ago(2025-10-16)[2] |
|  |
| Written in | Java,C,C++,C#,Perl,Python,PHP,Ruby |
| Type | Remote procedure callframework |
| License | Apache License 2.0 |
| Website | avro.apache.org |
| Repository | Avro Repository |

  

**Avro** is a [row-oriented](./Column-oriented_DBMS#Row-oriented_systems) [remote procedure call](./Remote_procedure_call) and data [serialization](./Serialization) [framework](./Software_framework) developed within [Apache's Hadoop](./Apache_Hadoop) project. It uses [JSON](./JSON) for defining [data types](./Data_type) and [protocols](./Communications_protocol), and serializes data in a compact binary format. Its primary use is in [Apache Hadoop](./Apache_Hadoop), where it can provide both a serialization format for [persistent data](./Persistent_data), and a [wire format](./Wire_format) for communication between Hadoop [nodes](./Node_(networking)), and from client programs to the Hadoop [services](./Service_(systems_architecture)).
Avro uses a schema to structure the data that is being encoded. It has two different types of schema languages: one for human editing (Avro IDL) and another which is more [machine-readable](./Machine-readable_data) based on JSON.[[3]](./Apache_Avro#cite_note-3)

 

It is similar to [Thrift](./Thrift_(protocol)) and [Protocol Buffers](./Protocol_Buffers), but does not require running a code-generation program when a [schema](./Database_schema) changes (unless desired for [statically-typed](./Statically-typed) languages).

 

[Apache Spark SQL](./Apache_Spark#Spark_SQL) can access Avro as a data source.[[4]](./Apache_Avro#cite_note-4)

 

## Avro Object Container File

 

An Avro [Object Container File](./Container_(abstract_data_type)) consists of:[[5]](./Apache_Avro#cite_note-5)

 
- A [file header](./File_header), followed by
- one or more file [data blocks](./Block_(data_storage)).

 

A file header consists of:

 
- Four bytes, [ASCII](./ASCII) 'O', 'b', 'j', followed by the Avro version number which is 1 (0x01) (Binary values 0x4F 0x62 0x6A 0x01).
- File metadata, including the schema definition.
- The 16-byte, randomly-generated sync marker for this file.

 

For data blocks Avro specifies two serialization encodings:[[6]](./Apache_Avro#cite_note-6) binary and JSON. Most applications will use the binary encoding, as it is smaller and faster.  For debugging and web-based applications, the JSON encoding may sometimes be appropriate.

 

## Schema definition

 

Avro schemas are defined using JSON.  Schemas are composed of primitive types (null, boolean, int, long, float, double, bytes, and string) and complex types (record, enum, array, map, union, and fixed).[[7]](./Apache_Avro#cite_note-7)

 

Simple schema example:

 
```
 {
   "namespace": "example.avro",
   "type": "record",
   "name": "User",
   "fields": [
      {"name": "name", "type": "string"},
      {"name": "favorite_number",  "type": ["null", "int"]},
      {"name": "favorite_color", "type": ["null", "string"]}
   ] 
 }

```
 

## Serializing and deserializing

 

Data in Avro might be stored with its corresponding schema, meaning a serialized item can be read without knowing the schema ahead of time.

 

### Example serialization and deserialization code in Python

 

Serialization:[[8]](./Apache_Avro#cite_note-8)

 
```
import avro.schema
from avro.datafile import DataFileReader, DataFileWriter
from avro.io import DatumReader, DatumWriter

# Need to know the schema to write. According to 1.8.2 of Apache Avro
schema = avro.schema.parse(open("user.avsc", "rb").read())

writer = DataFileWriter(open("users.avro", "wb"), DatumWriter(), schema)
writer.append({"name": "Alyssa", "favorite_number": 256})
writer.append({"name": "Ben", "favorite_number": 8, "favorite_color": "red"})
writer.close()

```
 

File "users.avro" will contain the schema in JSON and a compact binary representation[[9]](./Apache_Avro#cite_note-9) of the data:

 
```
$ od -v -t x1z users.avro 
0000000 4f 62 6a 01 04 14 61 76 72 6f 2e 63 6f 64 65 63  >Obj...avro.codec<
0000020 08 6e 75 6c 6c 16 61 76 72 6f 2e 73 63 68 65 6d  >.null.avro.schem<
0000040 61 ba 03 7b 22 74 79 70 65 22 3a 20 22 72 65 63  >a..{"type": "rec<
0000060 6f 72 64 22 2c 20 22 6e 61 6d 65 22 3a 20 22 55  >ord", "name": "U<
0000100 73 65 72 22 2c 20 22 6e 61 6d 65 73 70 61 63 65  >ser", "namespace<
0000120 22 3a 20 22 65 78 61 6d 70 6c 65 2e 61 76 72 6f  >": "example.avro<
0000140 22 2c 20 22 66 69 65 6c 64 73 22 3a 20 5b 7b 22  >", "fields": [{"<
0000160 74 79 70 65 22 3a 20 22 73 74 72 69 6e 67 22 2c  >type": "string",<
0000200 20 22 6e 61 6d 65 22 3a 20 22 6e 61 6d 65 22 7d  > "name": "name"}<
0000220 2c 20 7b 22 74 79 70 65 22 3a 20 5b 22 69 6e 74  >, {"type": ["int<
0000240 22 2c 20 22 6e 75 6c 6c 22 5d 2c 20 22 6e 61 6d  >", "null"], "nam<
0000260 65 22 3a 20 22 66 61 76 6f 72 69 74 65 5f 6e 75  >e": "favorite_nu<
0000300 6d 62 65 72 22 7d 2c 20 7b 22 74 79 70 65 22 3a  >mber"}, {"type":<
0000320 20 5b 22 73 74 72 69 6e 67 22 2c 20 22 6e 75 6c  > ["string", "nul<
0000340 6c 22 5d 2c 20 22 6e 61 6d 65 22 3a 20 22 66 61  >l"], "name": "fa<
0000360 76 6f 72 69 74 65 5f 63 6f 6c 6f 72 22 7d 5d 7d  >vorite_color"}]}<
0000400 00 05 f9 a3 80 98 47 54 62 bf 68 95 a2 ab 42 ef  >......GTb.h...B.<
0000420 24 04 2c 0c 41 6c 79 73 73 61 00 80 04 02 06 42  >$.,.Alyssa.....B<
0000440 65 6e 00 10 00 06 72 65 64 05 f9 a3 80 98 47 54  >en....red.....GT<
0000460 62 bf 68 95 a2 ab 42 ef 24                       >b.h...B.$<
0000471

```
 

Deserialization:

 
```
# The schema is embedded in the data file
reader = DataFileReader(open("users.avro", "rb"), DatumReader())
for user in reader:
    print(user)
reader.close()

```
 

This outputs:

 
```
{'name': 'Alyssa', 'favorite_number': 256, 'favorite_color': None}
{'name': 'Ben', 'favorite_number': 8, 'favorite_color': 'red'}

```
 

## Languages with APIs

 

Though theoretically any language could use Avro, the following languages have APIs written for them:[[10]](./Apache_Avro#cite_note-10)[[11]](./Apache_Avro#cite_note-11)

 
- [C](./C_(programming_language))
- [C++](./C++)
- [C#](./C_Sharp_(programming_language))[[12]](./Apache_Avro#cite_note-12)[[13]](./Apache_Avro#cite_note-13)[[14]](./Apache_Avro#cite_note-14)
- [Elixir](./Elixir_(programming_language))[[15]](./Apache_Avro#cite_note-15)[[16]](./Apache_Avro#cite_note-16)
- [Go](./Go_(programming_language))[[17]](./Apache_Avro#cite_note-17)[[18]](./Apache_Avro#cite_note-18)
- [Haskell](./Haskell)[[19]](./Apache_Avro#cite_note-19)
- [Java](./Java_(programming_language))
- [JavaScript](./JavaScript)[[20]](./Apache_Avro#cite_note-20)
- [Perl](./Perl)
- [PHP](./PHP)
- [Python](./Python_(programming_language))[[21]](./Apache_Avro#cite_note-21)[[22]](./Apache_Avro#cite_note-22)
- [Ruby](./Ruby_(programming_language))
- [Rust](./Rust_(programming_language))[[23]](./Apache_Avro#cite_note-23)
- [Scala](./Scala_(programming_language))

 

## Avro IDL

 

In addition to supporting JSON for type and protocol definitions, Avro includes experimental[[24]](./Apache_Avro#cite_note-24) support for an alternative [interface description language](./Interface_description_language) (IDL) syntax known as Avro IDL.  Previously known as GenAvro, this format is designed to ease adoption by users familiar with more traditional IDLs and programming languages, with a syntax similar to C/C++, [Protocol Buffers](./Protocol_Buffers) and others.

 

## Logo

 

The original Apache Avro logo was from the defunct British aircraft manufacturer [Avro](./Avro) (originally A.V. Roe and Company).[[25]](./Apache_Avro#cite_note-25)

 

The Apache Avro logo was updated to an original design in late 2023.[[26]](./Apache_Avro#cite_note-26)

 

## See also

 
- ![](//upload.wikimedia.org/wikipedia/commons/thumb/3/31/Free_and_open-source_software_logo_%282009%29.svg/40px-Free_and_open-source_software_logo_%282009%29.svg.png)[Free and open-source software portal](./Portal:Free_and_open-source_software)

 
- [Comparison of data serialization formats](./Comparison_of_data_serialization_formats)
- [Apache Thrift](./Apache_Thrift)
- [Protocol Buffers](./Protocol_Buffers)
- [Etch (protocol)](./Etch_(protocol))
- [Internet Communications Engine](./Internet_Communications_Engine)
- [MessagePack](./MessagePack)
- [CBOR](./CBOR)

 

## References

  
1. [↑](./Apache_Avro#cite_ref-1) ["Apache Avro: a New Format for Data Interchange"](https://blog.cloudera.com/blog/2009/11/avro-a-new-format-for-data-interchange/). *blog.cloudera.com*. Retrieved March 10, 2019.
2. [↑](./Apache_Avro#cite_ref-2) ["Apache Avro Releases"](https://avro.apache.org/releases.html). *avro.apache.org*. Retrieved October 27, 2025.
3. [↑](./Apache_Avro#cite_ref-3) Kleppmann, Martin (2017). *Designing Data-Intensive Applications* (First ed.). O'Reilly. p. 122.
4. [↑](./Apache_Avro#cite_ref-4) ["3 Reasons Why In-Hadoop Analytics are a Big Deal - Dataconomy"](http://dataconomy.com/3-reasons-hadoop-analytics-big-deal/). *dataconomy.com*. April 21, 2016.
5. [↑](./Apache_Avro#cite_ref-5) ["Apache Avro Specification: Object Container Files"](https://avro.apache.org/docs/++version++/specification/#object-container-files). *avro.apache.org*. Retrieved September 8, 2024.
6. [↑](./Apache_Avro#cite_ref-6) ["Apache Avro Specification: Encodings"](https://avro.apache.org/docs/++version++/specification/#encodings). *avro.apache.org*. Retrieved September 8, 2024.
7. [↑](./Apache_Avro#cite_ref-7) ["Apache Avro Getting Started (Python)"](https://web.archive.org/web/20160605204052/http://avro.apache.org/docs/current/gettingstartedpython.html#Defining+a+schema). *avro.apache.org*. Archived from [the original](https://avro.apache.org/docs/current/gettingstartedpython.html#Defining+a+schema) on June 5, 2016. Retrieved March 11, 2019.
8. [↑](./Apache_Avro#cite_ref-8) ["Apache Avro Getting Started (Python)"](https://web.archive.org/web/20160605204052/http://avro.apache.org/docs/current/gettingstartedpython.html). *avro.apache.org*. Archived from [the original](https://avro.apache.org/docs/current/gettingstartedpython.html) on June 5, 2016. Retrieved March 11, 2019.
9. [↑](./Apache_Avro#cite_ref-9) ["Apache Avro Specification: Data Serialization"](https://avro.apache.org/docs/++version++/specification/#data-serialization-and-deserialization). *avro.apache.org*. Retrieved September 8, 2024.
10. [↑](./Apache_Avro#cite_ref-10) phunt. ["GitHub - phunt/avro-rpc-quickstart: Apache Avro RPC Quick Start. Avro is a subproject of Apache Hadoop"](https://github.com/phunt/avro-rpc-quickstart). *GitHub*. Retrieved April 13, 2016.
11. [↑](./Apache_Avro#cite_ref-11) ["Supported Languages - Apache Avro - Apache Software Foundation"](https://cwiki.apache.org/confluence/display/AVRO/Supported+Languages). Retrieved April 21, 2016.
12. [↑](./Apache_Avro#cite_ref-12) ["Avro: 1.5.1 - ASF JIRA"](https://issues.apache.org/jira/browse/AVRO/fixforversion/12316197). Retrieved April 13, 2016.
13. [↑](./Apache_Avro#cite_ref-13) ["[AVRO-533] .NET implementation of Avro - ASF JIRA"](https://issues.apache.org/jira/browse/AVRO-533). Retrieved April 13, 2016.
14. [↑](./Apache_Avro#cite_ref-14) ["Supported Languages"](https://cwiki.apache.org/confluence/display/AVRO/Supported+Languages). Retrieved April 13, 2016.
15. [↑](./Apache_Avro#cite_ref-15) ["AvroEx"](https://hexdocs.pm/avro_ex/api-reference.html). *hexdocs.pm*. Retrieved October 18, 2017.
16. [↑](./Apache_Avro#cite_ref-16) ["Avrora — avrora v0.21.1"](https://hexdocs.pm/avrora/readme.html). *hexdocs.pm*. Retrieved June 11, 2021.
17. [↑](./Apache_Avro#cite_ref-17) ["avro package - github.com/hamba/avro - Go Packages"](https://pkg.go.dev/github.com/hamba/avro). *pkg.go.dev*. Retrieved July 4, 2023.
18. [↑](./Apache_Avro#cite_ref-18) [*goavro*](https://github.com/linkedin/goavro), LinkedIn, June 30, 2023, retrieved July 4, 2023
19. [↑](./Apache_Avro#cite_ref-19) ["Native Haskell implementation of Avro"](https://github.com/GaloisInc/avro). Thomas M. DuBuisson, Galois, Inc. Retrieved August 8, 2016.
20. [↑](./Apache_Avro#cite_ref-20) ["Pure JavaScript implementation of the Avro specification"](https://github.com/mtth/avsc). *[GitHub](./GitHub)*. Retrieved May 4, 2020.
21. [↑](./Apache_Avro#cite_ref-21) ["Getting Started (Python)"](https://avro.apache.org/docs/1.11.1/getting-started-python/). *Apache Avro*. Retrieved July 4, 2023.
22. [↑](./Apache_Avro#cite_ref-22) Avro, Apache, [*avro: Avro is a serialization and RPC framework.*](https://avro.apache.org/), retrieved July 4, 2023
23. [↑](./Apache_Avro#cite_ref-23) ["Apache Avro client library implementation in Rust"](https://crates.io/crates/apache-avro). Retrieved December 17, 2018.
24. [↑](./Apache_Avro#cite_ref-24) ["Apache Avro 1.8.2 IDL"](https://web.archive.org/web/20100920001652/http://avro.apache.org/docs/current/idl.html). Archived from [the original](https://avro.apache.org/docs/current/idl.html) on September 20, 2010. Retrieved March 11, 2019.
25. [↑](./Apache_Avro#cite_ref-25) ["The Avro Logo"](http://avroheritagemuseum.co.uk/the-avro-logo/). *avroheritagemuseum.co.uk*. Retrieved December 31, 2018.
26. [↑](./Apache_Avro#cite_ref-26) ["[AVRO-3908] Update project logo everywhere - ASF JIRA"](https://issues.apache.org/jira/browse/AVRO-3908). *apache.org*. Retrieved February 6, 2024.

 

## Further reading

 
- White, Tom (November 2010). [*Hadoop: The Definitive Guide*](https://archive.org/details/hadoopdefinitive0000whit). [ISBN](./ISBN_(identifier)) [978-1-4493-8973-4](./Special:BookSources/978-1-4493-8973-4).

 
| vteThe Apache Software Foundation |
| --- |
| Top-levelprojects | AccumuloActiveMQAiravataAirflowAlluraAmbariAntAriesArrowApache HTTP ServerAPRAvroAxisAxis2BeamBloodhoundBrooklynCalciteCamelCarbonDataCassandraCayenneCloudStackCordovaCouchDBcTAKESCXFDerbyDirectoryDrillDruidEmpire-dbFelixFlexFlinkFlumeFreeMarkerGeronimoGroovyGuacamoleGumpHadoopHBaseHelixHiveIcebergIgniteImpalaJackrabbitJamesJenaJMeterKafkaKuduKylinLuceneMahoutMavenMINAmod_perlMyFacesMynewtNiFiNetBeansNutchNuttXOFBizOozieOpenEJBOpenJPAOpenNLPOрenOfficeORCPDFBoxParquetPhoenixPOIPigPinotPivotQpidRollerRocketMQSamzaShiroSINGASlingSolrSparkStormSpamAssassinStruts1SubversionSupersetSystemDSTapestryThriftTikaTinkerPopTomcatTrafodionTraffic ServerUIMAVelocityWicketXalanXercesXMLBeansYetusZooKeeper |
| Commons | BCELBSFDaemonJellyLogging |
| Incubator | Taverna |
| Other projects | BatikFOPIvyLog4j |
| Attic | ApexAxKitBeehiveiBATISClickCocoonContinuumDeltacloudEtchGiraphHamaHarmonyJakartaMarmottaMXNetODERiverShaleSlideSqoopStanbolTuscanyWaveXML |
| Licenses | Apache License |
| Category |

 
| vteData exchangeformats |
| --- |
| Humanreadable | AtomCSVEDIFACTJSONWeb EncryptionWeb TokenWeb SignatureMarkdownProperty listRDFRebolTOMLTOONXMLYAML |
| Binary | AMFAscii85ASN.1SMIAvroBase32Base64BencodeBSONUBJSONCap'n ProtoCBORFlatBuffersMessagePackProperty listProtocol BuffersThriftCyphalDSDLXDRuuencodeyEnc |
| Comparison of data-serialization formats |