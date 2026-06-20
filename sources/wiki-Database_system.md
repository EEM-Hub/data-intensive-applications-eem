---
source: https://en.wikipedia.org/wiki/Database_system
fetched: 2026-06-19
---

Organized collection of data in computing This article is about the computing concept. For instances of the general concept, see [Lists of databases](./Lists_of_databases). 

  

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/f/f2/DVD_Rental_Query.png/500px-DVD_Rental_Query.png)](./File:DVD_Rental_Query.png)An [SQL](./SQL) select statement and its result 

In [computing](./Computing), a **database** is an organized collection of [data](./Data_(computing)) or a type of [data store](./Data_store) based on the use of a **database management system** (**DBMS**), the [software](./Software) that interacts with [end users](./End_user), [applications](./Application_software), and the database itself to capture and analyze the data. The DBMS additionally encompasses the core facilities provided to administer the database. The sum total of the database, the DBMS and the associated applications can be referred to as a **database system**. Often the term "database" is also used loosely to refer to any of the DBMS, the database system or an application associated with the database.

 

Before digital storage and retrieval of data became widespread, [index cards](./Index_cards) were used for [data storage](./Data_storage) in a wide range of applications and environments: in the home to record and store recipes, shopping lists, contact information and other organizational data; in business to record presentation notes, project research and notes, and contact information; in schools as flash cards or other visual aids; and in academic research to hold data such as bibliographical citations or notes in a [card file](./Card_file). Professional book indexers used index cards in the creation of book indexes until they were replaced by [indexing software](./Indexing_software) in the 1980s and 1990s.

 

Small databases can be stored on a [file system](./File_system), while large databases are hosted on [computer clusters](./Computer_clusters) or [cloud storage](./Cloud_storage). The [design of databases](./Database_design) spans formal techniques and practical considerations, including [data modeling](./Data_modeling), efficient data representation and storage, [query languages](./Query_language), [security](./Database_security) and [privacy](./Information_privacy) of sensitive data, and [distributed computing](./Distributed_computing) issues, including supporting [concurrent](./Concurrent_computing) access and [fault tolerance](./Fault_tolerance).

 

[Computer scientists](./Computer_scientists) may classify database management systems according to the [database models](./Database_model) that they support. [Relational databases](./Relational_database) became dominant in the 1980s. These model data as [rows](./Row_(database)) and [columns](./Column_(database)) in a series of [tables](./Table_(database)), and the vast majority use [SQL](./SQL) for writing and querying data. In the 2000s, non-relational databases became popular, collectively referred to as [NoSQL](./NoSQL), because they use different [query languages](./Query_language).

 

## Terminology and overview

 

Formally, a "database" refers to a set of related data accessed through the use of a "database management system" (DBMS), which is an integrated set of [computer software](./Computer_software) that allows [users](./User_(computing)) to interact with one or more databases and provides access to all of the data contained in the database (although restrictions may exist that limit access to particular data). The DBMS provides various functions that allow entry, storage and retrieval of large quantities of information and provides ways to manage how that information is organized.

 

Because of the close relationship between them, the term "database" is often used casually to refer to both a database and the DBMS used to manipulate it.

 

Outside the world of professional [information technology](./Information_technology), the term *database* is often used to refer to any collection of related data (such as a [spreadsheet](./Spreadsheet) or a card index) as size and usage requirements typically necessitate use of a database management system.[[1]](./Database#cite_note-FOOTNOTEUllmanWidom19971-1)

 

Existing DBMSs provide various functions that allow management of a database and its data which can be classified into four main functional groups:

 
- **Data definition** – Creation, modification and removal of definitions that detail how the data is to be organized.
- **Update** – Insertion, modification, and deletion of the data itself.[[2]](./Database#cite_note-2)
- **Retrieval** – Selecting data according to specified criteria (e.g., a query, a position in a hierarchy, or a position in relation to other data) and providing that data either directly to the user, or making it available for further processing by the database itself or by other applications. The retrieved data may be made available in a more or less direct form without modification, as it is stored in the database, or in a new form obtained by altering it or combining it with existing data from the database.[[3]](./Database#cite_note-3)
- **Administration** – Registering and monitoring users, enforcing data security, monitoring performance, maintaining data integrity, dealing with concurrency control, and recovering information that has been corrupted by some event such as an unexpected system failure.[[4]](./Database#cite_note-4)

 

Both a database and its DBMS conform to the principles of a particular [database model](./Database_model).[[5]](./Database#cite_note-FOOTNOTETsitchizrisLochovsky1982-5) "Database system" refers collectively to the database model, database management system, and database.[[6]](./Database#cite_note-FOOTNOTEBeynon-Davies2003-6)

 

Physically, database [servers](./Server_(computing)) are dedicated computers that hold the actual databases and run only the DBMS and related software. Database servers are usually [multiprocessor](./Multiprocessor) computers, with generous memory and [RAID](./RAID) disk arrays used for stable storage. Hardware database accelerators, connected to one or more servers via a high-speed channel, are also used in large-volume [transaction processing environments](./Transaction_processing_system). DBMSs are found at the heart of most [database applications](./Database_application). DBMSs may be built around a custom [multitasking](./Computer_multitasking) [kernel](./Kernel_(operating_system)) with built-in [networking](./Computer_network) support, but modern DBMSs typically rely on a standard [operating system](./Operating_system) to provide these functions.[*[citation needed](./Wikipedia:Citation_needed)*]

 

Since DBMSs comprise a significant [market](./Market_(economics)), computer and storage vendors often take into account DBMS requirements in their own development plans.[[7]](./Database#cite_note-FOOTNOTENelsonNelson2001-7)

 

Databases and DBMSs can be categorized according to the database model(s) that they support (such as [relational](./Relational_database) or [XML](./XML)), the type(s) of computer they run on (from a [server cluster](./Server_cluster) to a [mobile phone](./Mobile_phone)), the [query language](./Query_language)(s) used to access the database (such as SQL or [XQuery](./XQuery)), and their internal engineering, which affects performance, [scalability](./Scalability), resilience, and security.

 

## History

 

The sizes, capabilities, and performance of databases and their respective DBMSs have grown in orders of magnitude. These performance increases were enabled by the technology progress in the areas of [processors](./Central_processing_unit), [computer memory](./Computer_memory), [computer storage](./Computer_storage), and [computer networks](./Computer_network). The concept of a database was made possible by the emergence of direct access [storage media](./Storage_media) such as [magnetic disks](./Hard_disk_drive), which became widely available in the mid-1960s; earlier systems relied on sequential storage of data on [magnetic tape](./Magnetic_tape). The subsequent development of database technology can be divided into three eras based on data model or structure: [navigational](./Navigational_database),[[8]](./Database#cite_note-FOOTNOTEBachman1973-8) SQL/[relational](./Relational_database), and post-relational.

 

The two main early navigational [data models](./Data_model) were the [hierarchical model](./Hierarchical_model) and the [CODASYL](./CODASYL) model ([network model](./Network_model)). These were characterized by the use of [pointers](./Pointer_(computer_programming)) (often physical disk addresses) to follow relationships from one record to another.

 

The [relational model](./Relational_model), first proposed in 1970 by [Edgar F. Codd](./Edgar_F._Codd), departed from this tradition by insisting that [applications](./Application_software) should search for data by content, rather than by following links. The relational model employs sets of ledger-style tables, each used for a different type of [entity](./Entity). Only in the mid-1980s did computing hardware become powerful enough to allow the wide deployment of relational systems (DBMSs plus applications). By the early 1990s, however, relational systems dominated in all large-scale [data processing](./Data_processing) applications, and as of 2018[[update]](https://en.wikipedia.org/w/index.php?title=Database&action=edit) they remain dominant: [IBM Db2](./IBM_Db2), [Oracle](./Oracle_database), [MySQL](./MySQL), and [Microsoft SQL Server](./Microsoft_SQL_Server) are the most searched [DBMS](./DBMS).[[9]](./Database#cite_note-9) The dominant database language, standardized SQL for the relational model, has influenced database languages for other data models.[*[citation needed](./Wikipedia:Citation_needed)*]

 

[Object databases](./Object_database) were developed in the 1980s to overcome the inconvenience of [object–relational impedance mismatch](./Object–relational_impedance_mismatch), which led to the coining of the term "post-relational" and also the development of hybrid [object–relational databases](./Object–relational_database).

 

The next generation of post-relational databases in the late 2000s became known as [NoSQL](./NoSQL) databases, introducing fast [key–value stores](./Key–value_store) and [document-oriented databases](./Document-oriented_database). A competing "next generation" known as [NewSQL](./NewSQL) databases attempted new implementations that retained the relational/SQL model while aiming to match the high performance of NoSQL compared to commercially available relational DBMSs.

 

### 1960s, navigational DBMS

 Further information: [Navigational database](./Navigational_database) [![](//upload.wikimedia.org/wikipedia/commons/thumb/d/d6/CodasylB.png/330px-CodasylB.png)](./File:CodasylB.png)Basic structure of navigational [CODASYL](./CODASYL) database model 

The introduction of the term *database* coincided with the availability of direct-access storage (disks and drums) from the mid-1960s onwards. The term represented a contrast with the tape-based systems of the past, allowing shared interactive use rather than daily [batch processing](./Batch_processing). The [Oxford English Dictionary](./Oxford_English_Dictionary) cites a 1962 report by the [System Development Corporation](./System_Development_Corporation) of California as the first to use the term "data-base" in a specific technical sense.[[10]](./Database#cite_note-10)

 

As computers grew in speed and capability, a number of general-purpose database systems emerged; by the mid-1960s a number of such systems had come into commercial use. Interest in a standard began to grow, and [Charles Bachman](./Charles_Bachman), author of one such product, the [Integrated Data Store](./Integrated_Data_Store) (IDS), founded the [Database Task Group](./Data_Base_Task_Group) within [CODASYL](./CODASYL), the group responsible for the creation and standardization of [COBOL](./COBOL). In 1971, the Database Task Group delivered their standard, which generally became known as the *CODASYL approach*, and soon a number of commercial products based on this approach entered the market.

 

The CODASYL approach offered applications the ability to navigate around a linked data set which was formed into a large network. Applications could find records by one of three methods:

 
1. Use of a primary key (known as a CALC key, typically implemented by [hashing](./Hash_function))
2. Navigating relationships (called *sets*) from one record to another
3. Scanning all the records in a sequential order

 

Later systems added [B-trees](./B-tree) to provide alternate access paths. Many CODASYL databases also added a declarative query language for end users (as distinct from the navigational [API](./API)). However, CODASYL databases were complex and required significant training and effort to produce useful applications.

 

[IBM](./IBM) also had its own DBMS in 1966, known as [Information Management System](./Information_Management_System) (IMS). IMS was a development of software written for the [Apollo program](./Apollo_program) on the [System/360](./System/360). IMS was generally similar in concept to CODASYL, but used a strict hierarchy for its model of data navigation instead of CODASYL's network model. Both concepts later became known as navigational databases due to the way data was accessed: the term was popularized by Bachman's 1973 [Turing Award](./Turing_Award) presentation *The Programmer as Navigator*. IMS is classified by IBM as a [hierarchical database](./Hierarchical_database). IDMS and [Cincom Systems](./Cincom_Systems)' [TOTAL](./Cincom_Systems#1970s_and_1980s) databases are classified as network databases. IMS remains in use as of 2014[[update]](https://en.wikipedia.org/w/index.php?title=Database&action=edit).[[11]](./Database#cite_note-11)

 

### 1970s, relational DBMS

 

[Edgar F. Codd](./Edgar_F._Codd) worked at IBM in [San Jose, California](./San_Jose,_California), in an office primarily involved in the development of [hard disk](./Hard_disk) systems.[[12]](./Database#cite_note-rdbmsearlyyearsoh20070612-12) He was unhappy with the navigational model of the CODASYL approach, notably the lack of a "search" facility. In 1970, he wrote a number of papers that outlined a new approach to database construction that eventually culminated in the groundbreaking *A Relational Model of Data for Large Shared Data Banks*.[[13]](./Database#cite_note-FOOTNOTECodd1970-13)

 

The paper described a new system for storing and working with large databases. Instead of records being stored in some sort of [linked list](./Linked_list) of free-form records as in CODASYL, Codd's idea was to organize the data as a number of "[tables](./Table_(database))", each table being used for a different type of entity. Each table would contain a fixed number of columns containing the attributes of the entity. One or more columns of each table were designated as a  [primary key](./Primary_key) by which the rows of the table could be uniquely identified; cross-references between tables always used these primary keys, rather than disk addresses, and queries would join tables based on these key relationships, using a set of operations based on the mathematical system of [relational calculus](./Relational_calculus) (from which the model takes its name). Splitting the data into a set of normalized tables (or *relations*) aimed to ensure that each "fact" was only stored once, thus simplifying update operations. Virtual tables called *views* could present the data in different ways for different users, but views could not be directly updated.

 

Codd used mathematical terms to define the model: relations, tuples, and domains rather than tables, rows, and columns. The terminology that is now familiar came from early implementations. Codd would later criticize the tendency for practical implementations to depart from the mathematical foundations on which the model was based.

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/4/4c/Relational_key_SVG.svg/250px-Relational_key_SVG.svg.png)](./File:Relational_key_SVG.svg)In the [relational model](./Relational_model), records are "linked" using virtual keys not stored in the database but defined as needed between the data contained in the records. 

The use of primary keys (user-oriented identifiers) to represent cross-table relationships, rather than disk addresses, had two primary motivations. From an engineering perspective, it enabled tables to be relocated and resized without expensive database reorganization. But Codd was more interested in the difference in semantics: the use of explicit identifiers made it easier to define update operations with clean mathematical definitions, and it also enabled query operations to be defined in terms of the established discipline of [first-order predicate calculus](./First-order_predicate_calculus); because these operations have clean mathematical properties, it becomes possible to rewrite queries in provably correct ways, which is the basis of query optimization. There is no loss of expressiveness compared with the hierarchic or network models, though the connections between tables are no longer so explicit.

 

In the hierarchic and network models, records were allowed to have a complex internal structure. For example, the salary history of an employee might be represented as a "repeating group" within the employee record. In the relational model, the process of normalization led to such internal structures being replaced by data held in multiple tables, connected only by logical keys.

 

For instance, a common use of a database system is to track information about users, their name, login information, various addresses and phone numbers. In the navigational approach, all of this data would be placed in a single variable-length record. In the relational approach, the data would be *normalized* into a user table, an address table and a phone number table (for instance). Records would be created in these optional tables only if the address or phone numbers were actually provided.

 

As well as identifying rows/records using logical identifiers rather than disk addresses, Codd changed the way in which applications assembled data from multiple records. Rather than requiring applications to gather data one record at a time by navigating the links, they would use a declarative query language that expressed what data was required, rather than the access path by which it should be found. Finding an efficient access path to the data became the responsibility of the database management system, rather than the application programmer. This process, called query optimization, depended on the fact that queries were expressed in terms of mathematical logic.

 

Codd's paper inspired teams at various universities to research the subject, including one at [University of California, Berkeley](./University_of_California,_Berkeley)[[12]](./Database#cite_note-rdbmsearlyyearsoh20070612-12) led by [Eugene Wong](./Eugene_Wong) and [Michael Stonebraker](./Michael_Stonebraker), who started [INGRES](./INGRES) using funding that had already been allocated for a geographical database project and student programmers to produce code. Beginning in 1973, INGRES delivered its first test products which were generally ready for widespread use in 1979. INGRES was similar to [System R](./IBM_System_R) in a number of ways, including the use of a "language" for [data access](./Data_access), known as [QUEL](./QUEL_query_languages). Over time, INGRES moved to the emerging SQL standard.

 

IBM itself did one test implementation of the relational model, [PRTV](./PRTV), and a production one, [Business System 12](./Business_System_12), both now discontinued. [Honeywell](./Honeywell) wrote [MRDS](./Multics_Relational_Data_Store) for [Multics](./Multics), and now there are two new implementations: [Alphora Dataphor](./Dataphor) and Rel. Most other DBMS implementations usually called *relational* are actually SQL DBMSs.

 

In 1970, the University of Michigan began development of the [MICRO Information Management System](./MICRO_Information_Management_System)[[14]](./Database#cite_note-FOOTNOTEHersheyEasthope1972-14) based on [D.L. Childs](./David_L._Childs)' Set-Theoretic Data model.[[15]](./Database#cite_note-FOOTNOTENorth2010-15)[[16]](./Database#cite_note-FOOTNOTEChilds1968a-16)[[17]](./Database#cite_note-FOOTNOTEChilds1968b-17) The university in 1974 hosted a debate between Codd and Bachman which Bruce Lindsay of IBM later described as "throwing lightning bolts at each other!".[[12]](./Database#cite_note-rdbmsearlyyearsoh20070612-12) MICRO was used to manage very large data sets by the [US Department of Labor](./US_Department_of_Labor), the [U.S. Environmental Protection Agency](./U.S._Environmental_Protection_Agency), and researchers from the [University of Alberta](./University_of_Alberta), the [University of Michigan](./University_of_Michigan), and [Wayne State University](./Wayne_State_University). It ran on IBM mainframe computers using the [Michigan Terminal System](./Michigan_Terminal_System).[[18]](./Database#cite_note-MICROManual1977-18) The system remained in production until 1998.

 

### Integrated approach

 Main article: [Database machine](./Database_machine) 

In the 1970s and 1980s, attempts were made to build database systems with integrated hardware and software. The underlying philosophy was that such integration would provide higher performance at a lower cost. Examples were [IBM System/38](./IBM_System/38), the early offering of [Teradata](./Teradata), and the [Britton Lee, Inc.](./Britton_Lee,_Inc.) database machine.

 

Another approach to hardware support for database management was [ICL](./International_Computers_Limited)'s [CAFS](./Content_Addressable_File_Store) accelerator, a hardware disk controller with programmable search capabilities. In the long term, these efforts were generally unsuccessful because specialized database machines could not keep pace with the rapid development and progress of general-purpose computers. Thus most database systems nowadays are software systems running on general-purpose hardware, using general-purpose computer data storage. However, this idea is still pursued in certain applications by some companies like [Netezza](./Netezza) and Oracle ([Exadata](./Exadata)).

 

### Late 1970s, SQL DBMS

 

IBM formed a team led by Codd that started working on a prototype system, *[System R](./IBM_System_R)* despite opposition from others at the company.[[12]](./Database#cite_note-rdbmsearlyyearsoh20070612-12) The first version was ready in 1974/5, and work then started on multi-table systems in which the data could be split so that all of the data for a record (some of which is optional) did not have to be stored in a single large "chunk". Subsequent multi-user versions were tested by customers in 1978 and 1979, by which time a standardized [query language](./Query_language) – SQL[[19]](./Database#cite_note-19)[*[citation needed](./Wikipedia:Citation_needed)*] – had been added. Codd's ideas were establishing themselves as both workable and superior to CODASYL, pushing IBM to develop a true production version of System R, known as *SQL/DS*, and, later, *Database 2* ([IBM Db2](./IBM_Db2)).

 

[Larry Ellison](./Larry_Ellison)'s Oracle Database (or more simply, [Oracle](./Oracle_Database)) started from a different chain, based on IBM's papers on System R. Though Oracle V1 implementations were completed in 1978, it was not until Oracle Version 2 when Ellison beat IBM to market in 1979.[[20]](./Database#cite_note-20)

 

Stonebraker went on to apply the lessons from INGRES to develop a new database, Postgres, which is now known as [PostgreSQL](./PostgreSQL). PostgreSQL is often used for global mission-critical applications (the .org and .info domain name registries use it as their primary [data store](./Data_store), as do many large companies and financial institutions).

 

In Sweden, Codd's paper was also read and [Mimer SQL](./Mimer_SQL) was developed in the mid-1970s at [Uppsala University](./Uppsala_University). In 1984, this project was consolidated into an independent enterprise.

 

Another data model, the [entity–relationship model](./Entity–relationship_model), emerged in 1976 and gained popularity for [database design](./Database_design) as it emphasized a more familiar description than the earlier relational model. Later on, entity–relationship constructs were retrofitted as a [data modeling](./Data_modeling) construct for the relational model, and the difference between the two has become irrelevant.[*[citation needed](./Wikipedia:Citation_needed)*]

 

### 1980s, on the desktop

 

Besides IBM and various software companies such as [Sybase](./Sybase) and [Informix Corporation](./Informix_Corporation), most large computer hardware vendors by the 1980s had their own database systems such as [DEC](./DEC_(company))'s [VAX Rdb/VMS](./VAX_Rdb/VMS).[[21]](./Database#cite_note-rdbmslateryears20070612-21) The decade ushered in the age of [desktop computing](./Desktop_computing). The new computers empowered their users with spreadsheets like [Lotus 1-2-3](./Lotus_1-2-3) and database software like [dBASE](./DBASE). The dBASE product was lightweight and easy for any computer user to understand out of the box. [C. Wayne Ratliff](./C._Wayne_Ratliff), the creator of dBASE, stated: "dBASE was different from programs like BASIC, C, FORTRAN, and COBOL in that a lot of the dirty work had already been done. The data manipulation is done by dBASE instead of by the user, so the user can concentrate on what he is doing, rather than having to mess with the dirty details of opening, reading, and closing files, and managing space allocation."[[22]](./Database#cite_note-22) dBASE was one of the top selling software titles in the 1980s and early 1990s.

 

### 1990s, object-oriented

 

By the start of the decade databases had become a billion-dollar industry in about ten years.[[21]](./Database#cite_note-rdbmslateryears20070612-21) The 1990s, along with a rise in [object-oriented programming](./Object-oriented_programming), saw a growth in how data in various databases were handled. Programmers and designers began to treat the data in their databases as [objects](./Object_(computer_science)). That is to say that if a person's data were in a database, that person's attributes, such as their address, phone number, and age, were now considered to belong to that person instead of being extraneous data. This allows for relations between data to be related to objects and their [attributes](./Property_(programming)) and not to individual fields.[[23]](./Database#cite_note-23) The term "[object–relational impedance mismatch](./Object–relational_impedance_mismatch)" described the inconvenience of translating between programmed objects and database tables. [Object databases](./Object_database) and [object–relational databases](./Object–relational_database) attempt to solve this problem by providing an object-oriented language (sometimes as extensions to SQL) that programmers can use as alternative to purely relational SQL. On the programming side, libraries known as [object–relational mappings](./Object–relational_mapping) (ORMs) attempt to solve the same problem.

 

### 2000s, NoSQL and NewSQL

 Main articles: [NoSQL](./NoSQL) and [NewSQL](./NewSQL) 

Database sales grew rapidly during the [dotcom bubble](./Dotcom_bubble) and, after its end, the rise of [ecommerce](./Ecommerce). The popularity of [open source](./Open_source) databases such as [MySQL](./MySQL) has grown since 2000, to the extent that Ken Jacobs of Oracle said in 2005 that perhaps "these guys are doing to us what we did to IBM".[[21]](./Database#cite_note-rdbmslateryears20070612-21)

 

[XML databases](./XML_database) are a type of structured document-oriented database that allows querying based on [XML](./XML) document attributes. XML databases are mostly used in applications where the data is conveniently viewed as a collection of documents, with a structure that can vary from the very flexible to the highly rigid: examples include scientific articles, patents, tax filings, and personnel records.

 

[NoSQL](./NoSQL) databases are often very fast,[[24]](./Database#cite_note-24)[[25]](./Database#cite_note-25) do not require fixed table schemas, avoid join operations by storing [denormalized](./Denormalization) data, and are designed to [scale horizontally](./Horizontal_scaling).

 

In recent years, there has been a strong demand for massively distributed databases with high partition tolerance, but according to the [CAP theorem](./CAP_theorem), it is impossible for a [distributed system](./Distributed_system) to simultaneously provide [consistency](./Consistency_model), availability, and partition tolerance guarantees. A distributed system can satisfy any two of these guarantees at the same time, but not all three. For that reason, many NoSQL databases are using what is called [eventual consistency](./Eventual_consistency) to provide both availability and partition tolerance guarantees with a reduced level of data consistency.

 

[NewSQL](./NewSQL) is a class of modern relational databases that aims to provide the same scalable performance of NoSQL systems for online transaction processing (read-write) workloads while still using SQL and maintaining the [ACID](./ACID) guarantees of a traditional database system.

 

## Use cases

 
|  | This sectiondoes notciteanysources.Please helpimprove this sectionbyadding citations to reliable sources. Unsourced material may be challenged andremoved.(March 2013)(Learn how and when to remove this message) |
| --- | --- |

 

Databases are used to support internal operations of organizations and to underpin online interactions with customers and suppliers (see [Enterprise software](./Enterprise_software)).

 

Databases are used to hold administrative information and more specialized data, such as engineering data or economic models. Examples include computerized [library](./Library) systems, [flight reservation systems](./Flight_reservation_system), computerized [parts inventory systems](./Parts_inventory_system), and many [content management systems](./Content_management_system) that store [websites](./Website) as collections of webpages in a database.

 

## Classification terms

 

One way to classify databases involves the type of their contents, for example: [bibliographic](./Bibliographic_database), document-text, statistical, or multimedia objects. Another way is by their application area, for example: accounting, music compositions, movies, banking, manufacturing, or insurance. A third way is by some technical aspect, such as the database structure or interface type. This section lists a few of the adjectives used to characterize different kinds of databases.

 
- An [in-memory database](./In-memory_database) is a database that primarily resides in [main memory](./Main_memory), but is typically backed-up by non-volatile computer data storage. Main memory databases are faster than disk databases, and so are often used where response time is critical, such as in telecommunications network equipment.
- An [active database](./Active_database) includes an event-driven architecture which can respond to conditions both inside and outside the database. Possible uses include security monitoring, alerting, statistics gathering and authorization. Many databases provide active database features in the form of [database triggers](./Database_trigger).
- A [cloud database](./Cloud_database) relies on [cloud technology](./Cloud_technology). Both the database and most of its DBMS reside remotely, "in the cloud", while its applications are both developed by programmers and later maintained and used by end-users through a [web browser](./Web_browser) and [Open APIs](./Open_API).
- [Data warehouses](./Data_warehouse)[*[citation needed](./Wikipedia:Citation_needed)*] archive data from operational databases and often from external sources such as market research firms. The warehouse becomes the central source of data for use by managers and other end-users who may not have access to operational data. For example, sales data might be aggregated to weekly totals and converted from internal product codes to use [UPCs](./Universal_Product_Code) so that they can be compared with [ACNielsen](./ACNielsen) data. Some basic and essential components of data warehousing include extracting, analyzing, and [mining](./Data_mining) data, transforming, loading, and managing data so as to make them available for further use.
- A [deductive database](./Deductive_database) combines [logic programming](./Logic_programming) with a relational database.
- A [distributed database](./Distributed_database) is one in which both the data and the DBMS span multiple computers.
- A [document-oriented database](./Document-oriented_database) is designed for storing, retrieving, and managing document-oriented, or semi structured, information. Document-oriented databases are one of the main categories of NoSQL databases.
- An [embedded database](./Embedded_database) system is a DBMS which is tightly integrated with an application software that requires access to stored data in such a way that the DBMS is hidden from the application's end-users and requires little or no ongoing maintenance.[[26]](./Database#cite_note-26)
- End-user databases consist of data developed by individual end-users. Examples of these are collections of documents, spreadsheets, presentations, multimedia, and other files. Several products[*[which?](./Wikipedia:Avoid_weasel_words)*] exist to support such databases.
- A [federated database system](./Federated_database_system) comprises several distinct databases, each with its own DBMS. It is handled as a single database by a federated database management system (FDBMS), which transparently integrates multiple autonomous DBMSs, possibly of different types (in which case it would also be a [heterogeneous database system](./Heterogeneous_database_system)), and provides them with an integrated conceptual view.
- Sometimes the term *multi-database* is used as a synonym for federated database, though it may refer to a less integrated (e.g., without an FDBMS and a managed integrated schema) group of databases that cooperate in a single application. In this case, typically [middleware](./Middleware_(distributed_applications)) is used for distribution, which typically includes an atomic commit protocol (ACP), e.g., the [two-phase commit protocol](./Two-phase_commit_protocol), to allow [distributed (global) transactions](./Distributed_transaction) across the participating databases.
- A [graph database](./Graph_database) is a kind of NoSQL database that uses [graph structures](./Graph_(data_structure)) with nodes, edges, and properties to represent and store information. General graph databases that can store any graph are distinct from specialized graph databases such as [triplestores](./Triplestore) and [network databases](./Network_database_model).
- An [array DBMS](./Array_DBMS) is a kind of NoSQL DBMS that allows modeling, storage, and retrieval of (usually large) multi-dimensional [arrays](./Array_data_structure) such as satellite images and climate simulation output.
- In a [hypertext](./Hypertext) or [hypermedia](./Hypermedia) database, any word or a piece of text representing an object, e.g., another piece of text, an article, a picture, or a film, can be [hyperlinked](./Hyperlink) to that object. Hypertext databases are particularly useful for organizing large amounts of disparate information. For example, they are useful for organizing [online encyclopedias](./Online_encyclopedia), where users can conveniently jump around the text. The [World Wide Web](./World_Wide_Web) is thus a large distributed hypertext database.
- A [knowledge base](./Knowledge_base) (abbreviated **KB**, **kb** or Δ[[27]](./Database#cite_note-27)[[28]](./Database#cite_note-28)) is a special kind of database for [knowledge management](./Knowledge_management), providing the means for the computerized collection, organization, and [retrieval](./Information_retrieval) of [knowledge](./Knowledge). Also a collection of data representing problems with their solutions and related experiences.

 
- A [mobile database](./Mobile_database) can be carried on or synchronized from a mobile computing device.
- [Operational databases](./Operational_database) store detailed data about the operations of an organization. They typically process relatively high volumes of updates using [transactions](./Transaction_(database)). Examples include [customer databases](./Customer_relationship_management) that record contact, credit, and demographic information about a business's customers, personnel databases that hold information such as salary, benefits, skills data about employees, [enterprise resource planning](./Enterprise_resource_planning) systems that record details about product components, parts inventory, and financial databases that keep track of the organization's money, accounting and financial dealings.
- A [parallel database](./Parallel_database) seeks to improve performance through [parallelization](./Parallelization) for tasks such as loading data, building indexes and evaluating queries.

 The major parallel DBMS architectures which are induced by the underlying [hardware](./Computer_hardware) architecture are:

- **[Shared memory architecture](./Shared_memory_architecture)**, where multiple processors share the main memory space, as well as other data storage.
- **Shared disk architecture**, where each processing unit (typically consisting of multiple processors) has its own main memory, but all units share the other storage.
- **[Shared-nothing architecture](./Shared-nothing_architecture)**, where each processing unit has its own main memory and other storage.

 
- [Probabilistic databases](./Probabilistic_database) employ [fuzzy logic](./Fuzzy_logic) to draw inferences from imprecise data.
- [Real-time databases](./Real-time_database) process transactions fast enough for the result to come back and be acted on right away.
- A [spatial database](./Spatial_database) can store the data with multidimensional features. The queries on such data include location-based queries, like "Where is the closest hotel in my area?".
- A [temporal database](./Temporal_database) has built-in time aspects, for example a temporal data model and a temporal version of [SQL](./SQL). More specifically the temporal aspects usually include valid-time and transaction-time.
- A [terminology-oriented database](./Terminology-oriented_database) builds upon an [object-oriented database](./Object-oriented_database), often customized for a specific field.
- An [unstructured data](./Unstructured_data) database is intended to store in a manageable and protected way diverse objects that do not fit naturally and conveniently in common databases. It may include email messages, documents, journals, multimedia objects, etc. The name may be misleading since some objects can be highly structured. However, the entire possible object collection does not fit into a predefined structured framework. Most established DBMSs now support unstructured data in various ways, and new dedicated DBMSs are emerging. Isn't this a document&#x2D;oriented database? If not, clearly distinguish. 

 

## Database management system

 

Connolly and Begg define database management system (DBMS) as a "software system that enables users to define, create, maintain and control access to the database."[[29]](./Database#cite_note-FOOTNOTEConnollyBegg201464-29) Examples of DBMS's include [MySQL](./MySQL), [MariaDB](./MariaDB), [PostgreSQL](./PostgreSQL), [Microsoft SQL Server](./Microsoft_SQL_Server), [Oracle Database](./Oracle_Database), and [Microsoft Access](./Microsoft_Access).

 

The DBMS acronym is sometimes extended to indicate the underlying [database model](./Database_model), with RDBMS for the [relational](./Relational_model), OODBMS for the [object (oriented)](./Object_model) and ORDBMS for the [object–relational model](./Object–relational_model). Other extensions can indicate some other characteristics, such as DDBMS for a distributed database management systems.

 

The functionality provided by a DBMS can vary enormously. The core functionality is the storage, retrieval and update of data. [Codd](./Edgar_F._Codd) proposed the following functions and services a fully-fledged general purpose DBMS should provide:[[30]](./Database#cite_note-FOOTNOTEConnollyBegg201497–102-30)

 
- Data storage, retrieval and update
- User accessible catalog or [data dictionary](./Data_dictionary) describing the metadata
- Support for transactions and concurrency
- Facilities for recovering the database should it become damaged
- Support for authorization of access and update of data
- Access support from remote locations
- Enforcing constraints to ensure data in the database abides by certain rules

 

It is also generally to be expected the DBMS will provide a set of utilities for such purposes as may be necessary to administer the database effectively, including import, export, monitoring, defragmentation and analysis utilities.[[31]](./Database#cite_note-FOOTNOTEConnollyBegg2014102-31) The core part of the DBMS interacting between the database and the application interface sometimes referred to as the [database engine](./Database_engine).

 

Often DBMSs will have configuration parameters that can be statically and dynamically tuned, for example the maximum amount of main memory on a server the database can use. The trend is to minimize the amount of manual configuration, and for cases such as [embedded databases](./Embedded_database) the need to target zero-administration is paramount.

 

The large major enterprise DBMSs have tended to increase in size and functionality and have involved up to thousands of human years of development effort throughout their lifetime.[[a]](./Database#cite_note-33)

 

Early multi-user DBMS typically only allowed for the application to reside on the same computer with access via [terminals](./Computer_terminal) or terminal emulation software. The [client–server architecture](./Client–server_architecture) was a development where the application resided on a client desktop and the database on a server allowing the processing to be distributed. This evolved into a [multitier architecture](./Multitier_architecture) incorporating [application servers](./Application_server) and [web servers](./Web_server) with the end user interface via a [web browser](./Web_browser) with the database only directly connected to the adjacent tier.[[33]](./Database#cite_note-FOOTNOTEConnollyBegg2014106–113-34)

 

A general-purpose DBMS will provide public [application programming interfaces](./Application_programming_interface) (API) and optionally a processor for [database languages](./Database_language) such as [SQL](./SQL) to allow applications to be written to interact with and manipulate the database. A special purpose DBMS may use a private API and be specifically customized and linked to a single application. For example, an [email](./Email) system performs many of the functions of a general-purpose DBMS such as message insertion, message deletion, attachment handling, blocklist lookup, associating messages an email address and so forth however these functions are limited to what is required to handle email.

 

## Application

 Main article: [Database application](./Database_application) 

External interaction with the database will be via an application program that interfaces with the DBMS.[[34]](./Database#cite_note-FOOTNOTEConnollyBegg201465-35) This can range from a [database tool](./Comparison_of_database_tools) that allows users to execute SQL queries textually or graphically, to a website that happens to use a database to store and search information.

 

### Application program interface

 

A [programmer](./Programmer) will [code](./Computer_programming) interactions to the database (sometimes referred to as a [datasource](./Datasource)) via an [application program interface](./Application_program_interface) (API) or via a [database language](./Database#database_language). The particular API or language chosen will need to be supported by DBMS, possibly indirectly via a [preprocessor](./Preprocessor) or a bridging API. Some API's aim to be database independent, [ODBC](./ODBC) being a commonly known example. Other common API's include [JDBC](./JDBC) and [ADO.NET](./ADO.NET).

 

## Database languages

 

Database languages are special-purpose languages, which allow one or more of the following tasks, sometimes distinguished as [sublanguages](./Sublanguage):

 
- [Data control language](./Data_control_language) (DCL) – controls access to data;
- [Data definition language](./Data_definition_language) (DDL) – defines data types such as creating, altering, or dropping tables and the relationships among them;
- [Data manipulation language](./Data_manipulation_language) (DML) – performs tasks such as inserting, updating, or deleting data occurrences;
- [Data query language](./Data_query_language) (DQL) – allows searching for information and computing derived information.

 

Database languages are specific to a particular data model. Notable examples include:

 
- SQL combines the roles of data definition, data manipulation, and query in a single language. It was one of the first commercial languages for the relational model, although it departs in some respects from [the relational model as described by Codd](./Codd's_12_rules) (for example, the rows and columns of a table can be ordered). SQL became a standard of the [American National Standards Institute](./American_National_Standards_Institute) (ANSI) in 1986, and of the [International Organization for Standardization](./International_Organization_for_Standardization) (ISO) in 1987. The standards have been regularly enhanced since and are supported (with varying degrees of conformance) by all mainstream commercial relational DBMSs.[[35]](./Database#cite_note-FOOTNOTEChapple2005-36)[[36]](./Database#cite_note-IBM-sql-37)
- [OQL](./OQL) is an object model language standard (from the [Object Data Management Group](./Object_Data_Management_Group)). It has influenced the design of some of the newer query languages like [JDOQL](./JDOQL?action=edit&redlink=1) and [EJB QL](./EJB_QL).
- [XQuery](./XQuery) is a standard XML query language implemented by XML database systems such as [MarkLogic](./MarkLogic) and [eXist](./EXist), by relational databases with XML capability such as Oracle and Db2, and also by in-memory XML processors such as [Saxon](./Saxon_XSLT).
- [SQL/XML](./SQL/XML) combines [XQuery](./XQuery) with SQL.[[37]](./Database#cite_note-FOOTNOTEWagner2010-38)

 

A database language may also incorporate features like:

 
- DBMS-specific configuration and storage engine management
- Computations to modify query results, like counting, summing, averaging, sorting, grouping, and cross-referencing
- Constraint enforcement (e.g. in an automotive database, only allowing one engine type per car)
- Application programming interface version of the query language, for programmer convenience

 

## Storage

 Main articles: [Computer data storage](./Computer_data_storage) and [Database engine](./Database_engine) 

Database storage is the container of the physical materialization of a database. It comprises the *internal* (physical) *level* in the database architecture. It also contains all the information needed (e.g., [metadata](./Metadata), "data about the data", and internal [data structures](./Data_structure)) to reconstruct the *conceptual level* and *external level* from the internal level when needed. Databases as digital objects contain three layers of information which must be stored: the data, the structure, and the semantics. Proper storage of all three layers is needed for future [preservation](./Database_preservation) and longevity of the database.[[38]](./Database#cite_note-39) Putting data into permanent storage is generally the responsibility of the [database engine](./Database_engine) a.k.a. "storage engine". Though typically accessed by a DBMS through the underlying operating system (and often using the operating systems' [file systems](./File_system) as intermediates for storage layout), storage properties and configuration settings are extremely important for the efficient operation of the DBMS, and thus are closely maintained by database administrators. A DBMS, while in operation, always has its database residing in several types of storage (e.g., memory and external storage). The database data and the additional needed information, possibly in very large amounts, are coded into bits. Data typically reside in the storage in structures that look completely different from the way the data look at the conceptual and external levels, but in ways that attempt to optimize (the best possible) these levels' reconstruction when needed by users and programs, as well as for computing additional types of needed information from the data (e.g., when querying the database).

 

Some DBMSs support specifying which [character encoding](./Character_encoding) was used to store data, so multiple encodings can be used in the same database.

 

Various low-level database storage structures are used by the storage engine to serialize the data model so it can be written to the medium of choice. Techniques such as indexing may be used to improve performance. Conventional storage is row-oriented, but there are also [column-oriented](./Column-oriented_DBMS) and [correlation databases](./Correlation_database?action=edit&redlink=1).

 

### Materialized views

 Main article: [Materialized view](./Materialized_view) 

Often storage redundancy is employed to increase performance. A common example is storing *materialized views*, which consist of frequently needed *external views* or query results. Storing such views saves the expensive computing them each time they are needed. The downsides of materialized views are the overhead incurred when updating them to keep them synchronized with their original updated database data, and the cost of storage redundancy.

 

### Replication

 See also: [Replication (computing) § Database replication](./Replication_(computing)#Database_replication) 

Occasionally a database employs storage redundancy by [database objects](./Database_object) replication (with one or more copies) to increase data availability (both to improve performance of simultaneous multiple end-user accesses to the same database object, and to provide resiliency in a case of partial failure of a distributed database). Updates of a replicated object need to be synchronized across the object copies. In many cases, the entire database is replicated.

 

### Virtualization

 

With [data virtualization](./Data_virtualization), the data used remains in its original locations and real-time access is established to allow analytics across multiple sources. This can aid in resolving some technical difficulties such as compatibility problems when combining data from various platforms, lowering the risk of error caused by faulty data, and guaranteeing that the newest data is used. Furthermore, avoiding the creation of a new database containing personal information can make it easier to comply with privacy regulations. However, with data virtualization, the connection to all necessary data sources must be operational as there is no local copy of the data, which is one of the main drawbacks of the approach.[[39]](./Database#cite_note-Paiho-40)

 

## Security

 Main article: [Database security](./Database_security) 
|  | This articleappears to contradict the articleDatabase security.Please discuss at thetalk pageand do not remove this message until the contradictions are resolved.(March 2013) |
| --- | --- |

 

[Database security](./Database_security) deals with all various aspects of protecting the database content, its owners, and its users. It ranges from protection from intentional unauthorized database uses to unintentional database accesses by unauthorized entities (e.g., a person or a computer program).

 

Database access control deals with controlling who (a person or a certain computer program) are allowed to access what information in the database. The information may comprise specific database objects (e.g., record types, specific records, data structures), certain computations over certain objects (e.g., query types, or specific queries), or using specific access paths to the former (e.g., using specific indexes or other data structures to access information). Database access controls are set by special authorized (by the database owner) personnel that uses dedicated protected security DBMS interfaces.

 

This may be managed directly on an individual basis, or by the assignment of individuals and [privileges](./Privilege_(Computing)) to groups, or (in the most elaborate models) through the assignment of individuals and groups to roles which are then granted entitlements. Data security prevents unauthorized users from viewing or updating the database. Using passwords, users are allowed access to the entire database or subsets of it called "subschemas". For example, an employee database can contain all the data about an individual employee, but one group of users may be authorized to view only payroll data, while others are allowed access to only work history and medical data. If the DBMS provides a way to interactively enter and update the database, as well as interrogate it, this capability allows for managing personal databases.

 

[Data security](./Data_security) in general deals with protecting specific chunks of data, both physically (i.e., from corruption, or destruction, or removal; e.g., see [physical security](./Physical_security)), or the interpretation of them, or parts of them to meaningful information (e.g., by looking at the strings of bits that they comprise, concluding specific valid credit-card numbers; e.g., see [data encryption](./Data_encryption)).

 

Change and access logging records who accessed which attributes, what was changed, and when it was changed. Logging services allow for a forensic [database audit](./Database_audit) later by keeping a record of access occurrences and changes. Sometimes application-level code is used to record changes rather than leaving this in the database. Monitoring can be set up to attempt to detect security breaches. Therefore, organizations must take database security seriously because of the many benefits it provides. Organizations will be safeguarded from security breaches and hacking activities like firewall intrusion, virus spread, and ransom ware. This helps in protecting the company's essential information, which cannot be shared with outsiders at any cause.[[40]](./Database#cite_note-41)

 

## Transactions and concurrency

 Further information: [Concurrency control](./Concurrency_control) 

[Database transactions](./Database_transactions) can be used to introduce some level of [fault tolerance](./Fault_tolerance) and [data integrity](./Data_integrity) after recovery from a [crash](./Crash_(computing)). A database transaction is a unit of work, typically encapsulating a number of operations over a database (e.g., reading a database object, writing, acquiring or releasing a [lock](./Lock_(database)), etc.), an abstraction supported in database and also other systems. Each transaction has well defined boundaries in terms of which program/code executions are included in that transaction (determined by the transaction's programmer via special transaction commands).

 

The acronym [ACID](./ACID) describes some ideal properties of a database transaction: [atomicity](./Atomicity_(database_systems)), [consistency](./Consistency_(database_systems)), [isolation](./Isolation_(database_systems)), and [durability](./Durability_(database_systems)).

 

## Migration

 See also: [Data migration § Database migration](./Data_migration#Database_migration) 

A database built with one DBMS is not portable to another DBMS (i.e., the other DBMS cannot run it). However, in some situations, it is desirable to migrate a database from one DBMS to another. The reasons are primarily economical (different DBMSs may have different [total costs of ownership](./Total_cost_of_ownership) or TCOs), functional, and operational (different DBMSs may have different capabilities). The migration involves the database's transformation from one DBMS type to another. The transformation should maintain (if possible) the database related application (i.e., all related application programs) intact. Thus, the database's conceptual and external architectural levels should be maintained in the transformation. It may be desired that also some aspects of the architecture internal level are maintained. A complex or large database migration may be a complicated and costly (one-time) project by itself, which should be factored into the decision to migrate. This is in spite of the fact that tools may exist to help migration between specific DBMSs. Typically, a DBMS vendor provides tools to help import databases from other popular DBMSs.

 

## Building, maintaining, and tuning

 Main article: [Database tuning](./Database_tuning) 

After designing a database for an application, the next stage is building the database. Typically, an appropriate general-purpose DBMS can be selected to be used for this purpose. A DBMS provides the needed [user interfaces](./User_interface) to be used by database administrators to define the needed application's data structures within the DBMS's respective data model. Other user interfaces are used to select needed DBMS parameters (like security related, storage allocation parameters, etc.).

 

When the database is ready (all its data structures and other needed components are defined), it is typically populated with initial application's data (database initialization, which is typically a distinct project; in many cases using specialized DBMS interfaces that support bulk insertion) before making it operational. In some cases, the database becomes operational while empty of application data, and data are accumulated during its operation.

 

After the database is created, initialized and populated it needs to be maintained. Various database parameters may need changing and the database may need to be tuned ([tuning](./Database_tuning)) for better performance; application's data structures may be changed or added, new related application programs may be written to add to the application's functionality, etc.

 

## Backup and restore

 Main article: [Backup](./Backup) 

Sometimes it is desired to bring a database back to a previous state (for many reasons, e.g., cases when the database is found corrupted due to a software error, or if it has been updated with erroneous data). To achieve this, a backup operation is done occasionally or continuously, where each desired database state (i.e., the values of its data and their embedding in database's data structures) is kept within dedicated backup files (many techniques exist to do this effectively). When it is decided by a database administrator to bring the database back to this state (e.g., by specifying this state by a desired point in time when the database was in this state), these files are used to restore that state.

 

## Static analysis

 

Static analysis techniques for software verification can be applied also in the scenario of query languages. In particular, the *[Abstract interpretation](./Abstract_interpretation) framework has been extended to the field of query languages for relational databases as a way to support sound approximation techniques.[[41]](./Database#cite_note-FOOTNOTEHalderCortesi2011-42) The semantics of query languages can be tuned according to suitable abstractions of the concrete domain of data. The abstraction of relational database systems has many interesting applications, in particular, for security purposes, such as fine-grained access control, watermarking, etc.

 

## Miscellaneous features

 

Other DBMS features might include:

 
- [Database logs](./Database_log) – This helps in keeping a history of the executed functions.
- Graphics component for producing graphs and charts, especially in a data warehouse system.
- [Query optimizer](./Query_optimizer) – Performs query optimization on every query to choose an efficient *[query plan](./Query_plan)* (a partial order (tree) of operations) to be executed to compute the query result. May be specific to a particular storage engine.
- Tools or hooks for database design, application programming, application program maintenance, database performance analysis and monitoring, database configuration monitoring, DBMS hardware configuration (a DBMS and related database may span computers, networks, and storage units) and related database mapping (especially for a distributed DBMS), storage allocation and database layout monitoring, storage migration, etc.

 

Increasingly, there are calls for a single system that incorporates all of these core functionalities into the same build, test, and deployment framework for database management and source control. Borrowing from other developments in the software industry, some market such offerings as "[DevOps](./DevOps) for database".[[42]](./Database#cite_note-43)

 

## Design and modeling

 Main article: [Database design](./Database_design) [![](//upload.wikimedia.org/wikipedia/commons/thumb/0/09/Process_of_database_design_v2.png/500px-Process_of_database_design_v2.png)](./File:Process_of_database_design_v2.png) 

The first task of a database designer is to produce a [conceptual data model](./Conceptual_data_model) that reflects the structure of the information to be held in the database. A common approach to this is to develop an [entity–relationship model](./Entity–relationship_model), often with the aid of drawing tools. Another popular approach is the [Unified Modeling Language](./Unified_Modeling_Language). A successful data model will accurately reflect the possible state of the external world being modeled: for example, if people can have more than one phone number, it will allow this information to be captured. Designing a good conceptual data model requires a good understanding of the application domain; it typically involves asking deep questions about the things of interest to an organization, like "can a customer also be a supplier?", or "if a product is sold with two different forms of packaging, are those the same product or different products?", or "if a plane flies from New York to Dubai via Frankfurt, is that one flight or two (or maybe even three)?". The answers to these questions establish definitions of the terminology used for entities (customers, products, flights, flight segments) and their relationships and attributes.

 

Producing the conceptual data model sometimes involves input from [business processes](./Business_process_modeling), or the analysis of [workflow](./Workflow) in the organization. This can help to establish what information is needed in the database, and what can be left out. For example, it can help when deciding whether the database needs to hold historic data as well as current data.

 

Having produced a conceptual data model that users are happy with, the next stage is to translate this into a [schema](./Database_schema) that implements the relevant data structures within the database. This process is often called logical database design, and the output is a [logical data model](./Logical_data_model) expressed in the form of a schema. Whereas the conceptual data model is (in theory at least) independent of the choice of database technology, the logical data model will be expressed in terms of a particular database model supported by the chosen DBMS. (The terms *data model* and *database model* are often used interchangeably, but in this article we use *data model* for the design of a specific database, and *database model* for the modeling notation used to express that design).

 

The most popular database model for general-purpose databases is the relational model, or more precisely, the relational model as represented by the SQL language. The process of creating a logical database design using this model uses a methodical approach known as [normalization](./Database_normalization). The goal of normalization is to ensure that each elementary "fact" is only recorded in one place, so that insertions, updates, and deletions automatically maintain consistency.

 

The final stage of database design is to make the decisions that affect performance, scalability, recovery, security, and the like, which depend on the particular DBMS. This is often called *physical database design*, and the output is the [physical data model](./Physical_data_model). A key goal during this stage is [data independence](./Data_independence), meaning that the decisions made for performance optimization purposes should be invisible to end-users and applications. There are two types of data independence: Physical data independence and logical data independence. Physical design is driven mainly by performance requirements, and requires a good knowledge of the expected workload and access patterns, and a deep understanding of the features offered by the chosen DBMS.

 

Another aspect of physical database design is security. It involves both defining [access control](./Access_control) to database objects as well as defining security levels and methods for the data itself.

 

### Models

 Main article: [Database model](./Database_model) [![](//upload.wikimedia.org/wikipedia/commons/thumb/3/3b/Database_models.jpg/500px-Database_models.jpg)](./File:Database_models.jpg)Collage of five types of database models 

A database model is a type of data model that determines the logical structure of a database and fundamentally determines in which manner [data](./Data) can be stored, organized, and manipulated. The most popular example of a database model is the relational model (or the SQL approximation of relational), which uses a table-based format.

 

Common logical data models for databases include:

 
- [Navigational databases](./Navigational_database) 
- [Hierarchical database model](./Hierarchical_database_model)
- [Network model](./Network_model)
- [Graph database](./Graph_database)

- [Relational model](./Relational_model)
- [Entity–relationship model](./Entity–relationship_model) 
- [Enhanced entity–relationship model](./Enhanced_entity–relationship_model)

- [Object model](./Object_database)
- [Document model](./Document-oriented_database)
- [Entity–attribute–value model](./Entity–attribute–value_model)
- [Star schema](./Star_schema)

 

An object–relational database combines the two related structures.

 

[Physical data models](./Physical_data_model) include:

 
- [Inverted index](./Inverted_index)
- [Flat file](./Flat_file)

 

Other models include:

 
- [Multidimensional model](./Multidimensional_database)
- [Array model](./Array_DBMS)
- [Multivalue model](./Multivalue_model)

 

Specialized models are optimized for particular types of data:

 
- [XML database](./XML_database)
- [Semantic model](./Semantic_data_model)
- [Content store](./Content_store)
- [Event store](./Event_store)
- [Time series model](./Time_series_database)

 

### External, conceptual, and internal views

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/4/4d/Traditional_View_of_Data_SVG.svg/330px-Traditional_View_of_Data_SVG.svg.png)](./File:Traditional_View_of_Data_SVG.svg)Traditional view of data[[43]](./Database#cite_note-ITL93-44) 

A database management system provides three views of the database data:

 
- The **external level** defines how each group of end-users sees the organization of data in the database. A single database can have any number of views at the external level.
- The **conceptual level** (or *logical level*) unifies the various external views into a compatible global view.[[44]](./Database#cite_note-FOOTNOTEDate200331–32-45) It provides the synthesis of all the external views. It is out of the scope of the various database end-users, and is rather of interest to database application developers and database administrators.
- The **internal level** (or *physical level*) is the internal organization of data inside a DBMS. It is concerned with cost, performance, scalability and other operational matters. It deals with storage layout of the data, using storage structures such as [indexes](./Index_(database)) to enhance performance. Occasionally it stores data of individual views ([materialized views](./Materialized_view)), computed from generic data, if performance justification exists for such redundancy. It balances all the external views' performance requirements, possibly conflicting, in an attempt to optimize overall performance across all activities.

 

While there is typically only one conceptual and internal view of the data, there can be any number of different external views. This allows users to see database information in a more business-related way rather than from a technical, processing viewpoint. For example, a financial department of a company needs the payment details of all employees as part of the company's expenses, but does not need details about employees that are in the interest of the [human resources](./Human_resources) department. Thus different departments need different *views* of the company's database.

 

The three-level database architecture relates to the concept of *data independence* which was one of the major initial driving forces of the relational model.[[44]](./Database#cite_note-FOOTNOTEDate200331–32-45) The idea is that changes made at a certain level do not affect the view at a higher level. For example, changes in the internal level do not affect application programs written using conceptual level interfaces, which reduces the impact of making physical changes to improve performance.

 

The conceptual view provides a level of indirection between internal and external. On the one hand it provides a common view of the database, independent of different external view structures, and on the other hand it abstracts away details of how the data are stored or managed (internal level). In principle every level, and even every external view, can be presented by a different data model. In practice usually a given DBMS uses the same data model for both the external and the conceptual levels (e.g., relational model). The internal level, which is hidden inside the DBMS and depends on its implementation, requires a different level of detail and uses its own types of data structure types.

 

## Research

 

Database technology has been an active research topic since the 1960s, both in academia and in the research and development groups of companies (for example [IBM Research](./IBM_Research)). Research activity includes [theory](./Database_theory) and development of [prototypes](./Prototype). Notable research topics have included [models](./Data_model), the atomic transaction concept, related [concurrency control](./Concurrency_control) techniques, query languages and [query optimization](./Query_optimization) methods, [RAID](./RAID), and more.

 

The database research area has several dedicated [academic journals](./Academic_journal) (for example, *[ACM Transactions on Database Systems](./ACM_Transactions_on_Database_Systems)*-TODS, *[Data and Knowledge Engineering](./Data_and_Knowledge_Engineering)*-DKE) and annual [conferences](./Academic_conference) (e.g., [ACM](./Association_for_Computing_Machinery) [SIGMOD](./SIGMOD), ACM [PODS](./Symposium_on_Principles_of_Database_Systems), VLDB, [IEEE](./IEEE) ICDE).

 

## See also

 For a topical guide, see [Outline of databases](./Outline_of_databases).  
- [Comparison of database tools](./Comparison_of_database_tools)
- [Comparison of object database management systems](./Comparison_of_object_database_management_systems)
- [Comparison of object–relational database management systems](./Comparison_of_object–relational_database_management_systems)
- [Comparison of relational database management systems](./Comparison_of_relational_database_management_systems)
- [Data bank](./Data_bank) – Organized collection of data in computingPages displaying short descriptions of redirect targets
- [Data hierarchy](./Data_hierarchy) – Systematic organization of data
- [Data store](./Data_store) – Repository for data collection storage and management
- [Database testing](./Database_testing) – Testing of database software systems
- [Database theory](./Database_theory) – Study of database design and use
- [Database-as-IPC](./Database-as-IPC) – Misusing databases for temporary messages
- [Database-centric architecture](./Database-centric_architecture) – Software architecture
- [Datalog](./Datalog) – Declarative logic programming language
- [DBOS](./DBOS) – Open source software library
- [Flat-file database](./Flat-file_database) – Database stored as flat data
- [INP (database)](./INP_(database)) – Early database management system
- [Journal of Database Management](./Journal_of_Database_Management)
- [Casio Databank](./Casio_Databank) – Brand of watch
- [Conformational dynamics data bank](./Conformational_dynamics_data_bank) – Database of protein conformations
- [Data repository](./Data_repository) – Long-term storage of research dataPages displaying short descriptions of redirect targets
- [Databank Systems](./Databank_Systems) – Financial computing shared service
- [Dortmund Data Bank](./Dortmund_Data_Bank)
- [Electron Microscopy Data Bank](./Electron_Microscopy_Data_Bank) – European biological databasePages displaying short descriptions of redirect targets
- [Hazardous Substances Data Bank](./Hazardous_Substances_Data_Bank) – Database of toxic compounds
- [List of databases](./List_of_databases)
- [Memory bank](./Memory_bank) – Logical unit of storage in computer architecture
- [National Trauma Data Bank](./National_Trauma_Data_Bank) – Compilation of U.S. traumatic injury data from participating institutions
- [Protein Data Bank](./Protein_Data_Bank) – International open access database of large biological molecules
- [Star Wars Databank](./Star_Wars_Databank)

  

## Notes

  
1. [↑](./Database#cite_ref-33) This article quotes a development time of five years involving 750 people for DB2 release 9 alone.[[32]](./Database#cite_note-FOOTNOTEChongWangDangSnow2007-32)

 

## References

 
1. [↑](./Database#cite_ref-FOOTNOTEUllmanWidom19971_1-0) [Ullman & Widom 1997](./Database#CITEREFUllmanWidom1997), p. 1.
2. [↑](./Database#cite_ref-2) ["Update Definition & Meaning"](http://www.merriam-webster.com/dictionary/update). *Merriam-Webster*. [Archived](https://web.archive.org/web/20240225065959/https://www.merriam-webster.com/dictionary/update) from the original on 25 February 2024.
3. [↑](./Database#cite_ref-3) ["Retrieval Definition & Meaning"](http://www.merriam-webster.com/dictionary/retrieval). *Merriam-Webster*. [Archived](https://web.archive.org/web/20230627174611/https://www.merriam-webster.com/dictionary/retrieval) from the original on 27 June 2023.
4. [↑](./Database#cite_ref-4) ["Administration Definition & Meaning"](http://www.merriam-webster.com/dictionary/administration). *Merriam-Webster*. [Archived](https://web.archive.org/web/20231206055116/https://www.merriam-webster.com/dictionary/administration) from the original on 6 December 2023.
5. [↑](./Database#cite_ref-FOOTNOTETsitchizrisLochovsky1982_5-0) [Tsitchizris & Lochovsky 1982](./Database#CITEREFTsitchizrisLochovsky1982).
6. [↑](./Database#cite_ref-FOOTNOTEBeynon-Davies2003_6-0) [Beynon-Davies 2003](./Database#CITEREFBeynon-Davies2003).
7. [↑](./Database#cite_ref-FOOTNOTENelsonNelson2001_7-0) [Nelson & Nelson 2001](./Database#CITEREFNelsonNelson2001).
8. [↑](./Database#cite_ref-FOOTNOTEBachman1973_8-0) [Bachman 1973](./Database#CITEREFBachman1973).
9. [↑](./Database#cite_ref-9) ["TOPDB Top Database index"](https://pypl.github.io/DB.html). *pypl.github.io*.
10. [↑](./Database#cite_ref-10) ["database, n"](http://www.oed.com/view/Entry/47411). *OED Online*. Oxford University Press. June 2013. Retrieved 12 July 2013. (Subscription required.)
11. [↑](./Database#cite_ref-11) IBM Corporation (October 2013). ["IBM Information Management System (IMS) 13 Transaction and Database Servers delivers high performance and low total cost of ownership"](http://www-01.ibm.com/common/ssi/cgi-bin/ssialias?subtype=ca&infotype=an&appname=iSource&supplier=897&letternum=ENUS213-381). Retrieved 20 February 2014.
12. [1](./Database#cite_ref-rdbmsearlyyearsoh20070612_12-0) [2](./Database#cite_ref-rdbmsearlyyearsoh20070612_12-1) [3](./Database#cite_ref-rdbmsearlyyearsoh20070612_12-2) [4](./Database#cite_ref-rdbmsearlyyearsoh20070612_12-3) ["RDBMS Plenary 1: Early Years"](https://archive.computerhistory.org/resources/access/text/2013/05/102702562-05-01-acc.pdf) (PDF) (Interview). Interviewed by Burton Grad. Computer History Museum. 12 June 2007. Retrieved 30 May 2025.
13. [↑](./Database#cite_ref-FOOTNOTECodd1970_13-0) [Codd 1970](./Database#CITEREFCodd1970).
14. [↑](./Database#cite_ref-FOOTNOTEHersheyEasthope1972_14-0) [Hershey & Easthope 1972](./Database#CITEREFHersheyEasthope1972).
15. [↑](./Database#cite_ref-FOOTNOTENorth2010_15-0) [North 2010](./Database#CITEREFNorth2010).
16. [↑](./Database#cite_ref-FOOTNOTEChilds1968a_16-0) [Childs 1968a](./Database#CITEREFChilds1968a).
17. [↑](./Database#cite_ref-FOOTNOTEChilds1968b_17-0) [Childs 1968b](./Database#CITEREFChilds1968b).
18. [↑](./Database#cite_ref-MICROManual1977_18-0) M.A. Kahn; D.L. Rumelhart; B.L. Bronson (October 1977). [*MICRO Information Management System (Version 5.0) Reference Manual*](https://docs.google.com/viewer?a=v&pid=explorer&chrome=true&srcid=0B4t_NX-QeWDYZGMwOTRmOTItZTg2Zi00YmJkLTg4MTktN2E4MWU0YmZlMjE3). Institute of Labor and Industrial Relations (ILIR), University of Michigan and Wayne State University.
19. [↑](./Database#cite_ref-19) ["What Is Structured Query Language (SQL)?"](https://www.ibm.com/think/topics/structured-query-language). *IBM*. Retrieved 18 March 2026. In the 1970s, IBM scientists Donald Chamberlin and Raymond Boyce developed and introduced SQL. It originated from the concept of relational models and was initially called structured English query language (SEQUEL) before being shortened to SQL.
20. [↑](./Database#cite_ref-20) ["Oracle 30th Anniversary Timeline"](https://www.oracle.com/us/corporate/profit/p27anniv-timeline-151918.pdf) (PDF). [Archived](https://web.archive.org/web/20110320220813/http://www.oracle.com/us/corporate/profit/p27anniv-timeline-151918.pdf) (PDF) from the original on 20 March 2011. Retrieved 23 August 2017.
21. [1](./Database#cite_ref-rdbmslateryears20070612_21-0) [2](./Database#cite_ref-rdbmslateryears20070612_21-1) [3](./Database#cite_ref-rdbmslateryears20070612_21-2) ["RDBMS Plenary Session: The Later Years"](https://archive.computerhistory.org/resources/access/text/2013/05/102701921-05-01-acc.pdf) (PDF) (Interview). Interviewed by Burton Grad. Computer History Museum. 12 June 2007. Retrieved 30 May 2025.
22. [↑](./Database#cite_ref-22) [Interview with Wayne Ratliff](http://www.foxprohistory.org/interview_wayne_ratliff.htm). The FoxPro History. Retrieved on 12 July 2013.
23. [↑](./Database#cite_ref-23) Development of an object-oriented DBMS; Portland, Oregon, United States; Pages: 472–482; 1986; [ISBN](./ISBN_(identifier)) [0-89791-204-7](./Special:BookSources/0-89791-204-7)
24. [↑](./Database#cite_ref-24) Jordan, Meghan. ["NoSQL Latency"](https://www.scylladb.com/glossary/nosql-latency/). *ScyllaDB*. Retrieved 9 June 2025.
25. [↑](./Database#cite_ref-25) ["SQL vs. NoSQL: Full comparison of features, differences, and more"](https://www.testgorilla.com/blog/sql-vs-nosql/). *www.testgorilla.com*. Retrieved 9 June 2025.
26. [↑](./Database#cite_ref-26) Graves, Steve. ["COTS Databases For Embedded Systems"](http://www.embedded-computing.com/articles/id/?2020) [Archived](https://web.archive.org/web/20071114050734/http://www.embedded-computing.com/articles/id/?2020) 14 November 2007 at the [Wayback Machine](./Wayback_Machine), *Embedded Computing Design* magazine, January 2007. Retrieved on 13 August 2008.
27. [↑](./Database#cite_ref-27) Argumentation in Artificial Intelligence by Iyad Rahwan, Guillermo R. Simari
28. [↑](./Database#cite_ref-28) ["OWL DL Semantics"](http://www.obitko.com/tutorials/ontologies-semantic-web/owl-dl-semantics.html). Retrieved 10 December 2010.
29. [↑](./Database#cite_ref-FOOTNOTEConnollyBegg201464_29-0) [Connolly & Begg 2014](./Database#CITEREFConnollyBegg2014), p. 64.
30. [↑](./Database#cite_ref-FOOTNOTEConnollyBegg201497–102_30-0) [Connolly & Begg 2014](./Database#CITEREFConnollyBegg2014), pp. 97–102.
31. [↑](./Database#cite_ref-FOOTNOTEConnollyBegg2014102_31-0) [Connolly & Begg 2014](./Database#CITEREFConnollyBegg2014), p. 102.
32. [↑](./Database#cite_ref-FOOTNOTEChongWangDangSnow2007_32-0) [Chong et al. 2007](./Database#CITEREFChongWangDangSnow2007).
33. [↑](./Database#cite_ref-FOOTNOTEConnollyBegg2014106–113_34-0) [Connolly & Begg 2014](./Database#CITEREFConnollyBegg2014), pp. 106–113.
34. [↑](./Database#cite_ref-FOOTNOTEConnollyBegg201465_35-0) [Connolly & Begg 2014](./Database#CITEREFConnollyBegg2014), p. 65.
35. [↑](./Database#cite_ref-FOOTNOTEChapple2005_36-0) [Chapple 2005](./Database#CITEREFChapple2005).
36. [↑](./Database#cite_ref-IBM-sql_37-0) ["Structured Query Language (SQL)"](http://publib.boulder.ibm.com/infocenter/db2luw/v9/index.jsp?topic=com.ibm.db2.udb.admin.doc/doc/c0004100.htm). International Business Machines. 27 October 2006. Retrieved 10 June 2007.
37. [↑](./Database#cite_ref-FOOTNOTEWagner2010_38-0) [Wagner 2010](./Database#CITEREFWagner2010).
38. [↑](./Database#cite_ref-39) Ramalho, J.C.; Faria, L.; Helder, S.; Coutada, M. (31 December 2013). ["Database Preservation Toolkit: A flexible tool to normalize and give access to databases"](https://core.ac.uk/display/55635702?algorithmId=15&similarToDoc=55614406&similarToDocKey=CORE&recSetID=f3ffea4d-1504-45e9-bfd6-a0495f5c8f9c&position=2&recommendation_type=same_repo&otherRecs=55614407,55635702,55607961,55613627,2255664). *Biblioteca Nacional de Portugal*. University of Minho.
39. [↑](./Database#cite_ref-Paiho_40-0) Paiho, Satu; Tuominen, Pekka; Rökman, Jyri; Ylikerälä, Markus; Pajula, Juha; Siikavirta, Hanne (2022). ["Opportunities of collected city data for smart cities"](https://doi.org/10.1049%2Fsmc2.12044). *IET Smart Cities*. **4** (4): 275–291. [doi](./Doi_(identifier)):[10.1049/smc2.12044](https://doi.org/10.1049%2Fsmc2.12044). [ISSN](./ISSN_(identifier)) [2631-7680](https://search.worldcat.org/issn/2631-7680). [S2CID](./S2CID_(identifier)) [253467923](https://api.semanticscholar.org/CorpusID:253467923).
40. [↑](./Database#cite_ref-41) David Y. Chan; Victoria Chiu; Miklos A. Vasarhelyi (2018). *Continuous auditing : theory and application* (1st ed.). Bingley, UK: Emerald Publishing. [ISBN](./ISBN_(identifier)) [978-1-78743-413-4](./Special:BookSources/978-1-78743-413-4). [OCLC](./OCLC_(identifier)) [1029759767](https://search.worldcat.org/oclc/1029759767).
41. [↑](./Database#cite_ref-FOOTNOTEHalderCortesi2011_42-0) [Halder & Cortesi 2011](./Database#CITEREFHalderCortesi2011).
42. [↑](./Database#cite_ref-43) Ben Linders (28 January 2016). ["How Database Administration Fits into DevOps"](https://www.infoq.com/news/2016/01/database-administration-devops). Retrieved 15 April 2017.
43. [↑](./Database#cite_ref-ITL93_44-0) itl.nist.gov (1993) [*Integration Definition for Information Modeling (IDEFIX)*](http://www.itl.nist.gov/fipspubs/idef1x.doc) [Archived](https://web.archive.org/web/20131203223034/http://www.itl.nist.gov/fipspubs/idef1x.doc) 3 December 2013 at the [Wayback Machine](./Wayback_Machine). 21 December 1993.
44. [1](./Database#cite_ref-FOOTNOTEDate200331–32_45-0) [2](./Database#cite_ref-FOOTNOTEDate200331–32_45-1) [Date 2003](./Database#CITEREFDate2003), pp. 31–32.

 

## Sources

  
- [Bachman, Charles W.](./Charles_Bachman) (1973). ["The Programmer as Navigator"](https://doi.org/10.1145%2F355611.362534). *Communications of the ACM*. **16** (11): 653–658. [doi](./Doi_(identifier)):[10.1145/355611.362534](https://doi.org/10.1145%2F355611.362534).
- Beynon-Davies, Paul (2003). *Database Systems* (3rd ed.). Palgrave Macmillan. [ISBN](./ISBN_(identifier)) [978-1403916013](./Special:BookSources/978-1403916013).
- Chapple, Mike (2005). ["SQL Fundamentals"](http://databases.about.com/od/sql/a/sqlfundamentals.htm). *Databases*. About.com. [Archived](https://web.archive.org/web/20090222225300/http://databases.about.com/od/sql/a/sqlfundamentals.htm) from the original on 22 February 2009. Retrieved 28 January 2009.
- [Childs, David L.](./David_L._Childs) (1968a). [*Description of a set-theoretic data structure*](https://deepblue.lib.umich.edu/bitstream/handle/2027.42/4163/bac0294.0001.001.pdf?sequence=5&isAllowed=y) (PDF) (Technical report). CONCOMP (Research in Conversational Use of Computers) Project. University of Michigan. Technical Report 3.
- [Childs, David L.](./David_L._Childs) (1968b). [*Feasibility of a set-theoretic data structure: a general structure based on a reconstituted definition*](https://deepblue.lib.umich.edu/bitstream/handle/2027.42/4164/bac0293.0001.001.pdf?sequence=5&isAllowed=y) (PDF) (Technical report). CONCOMP (Research in Conversational Use of Computers) Project. University of Michigan. Technical Report 6.
- Chong, Raul F.; Wang, Xiaomei; Dang, Michael; Snow, Dwaine R. (2007). ["Introduction to DB2"](http://www.ibmpressbooks.com/articles/article.asp?p=1163083). *Understanding DB2: Learning Visually with Examples* (2nd ed.). IBM Press Pearson plc. [ISBN](./ISBN_(identifier)) [978-0131580183](./Special:BookSources/978-0131580183). Retrieved 17 March 2013.
- [Codd, Edgar F.](./Edgar_F._Codd) (1970). ["A Relational Model of Data for Large Shared Data Banks"](http://www.seas.upenn.edu/~zives/03f/cis550/codd.pdf) (PDF). *Communications of the ACM*. **13** (6): 377–387. [doi](./Doi_(identifier)):[10.1145/362384.362685](https://doi.org/10.1145%2F362384.362685). [S2CID](./S2CID_(identifier)) [207549016](https://api.semanticscholar.org/CorpusID:207549016).
- Connolly, Thomas M.; Begg, Carolyn E. (2014). *Database Systems – A Practical Approach to Design Implementation and Management* (6th ed.). Pearson. [ISBN](./ISBN_(identifier)) [978-1292061184](./Special:BookSources/978-1292061184).
- [Date, C. J.](./Christopher_J._Date) (2003). [*An Introduction to Database Systems*](https://archive.org/details/introductiontoda0000date) (8th ed.). Pearson. [ISBN](./ISBN_(identifier)) [978-0321197849](./Special:BookSources/978-0321197849).
- Halder, Raju; Cortesi, Agostino (2011). ["Abstract Interpretation of Database Query Languages"](https://web.archive.org/web/20241123005344/https://www.dsi.unive.it/~cortesi/paperi/CL2012.pdf) (PDF). *Computer Languages, Systems & Structures*. **38** (2): 123–157. [doi](./Doi_(identifier)):[10.1016/j.cl.2011.10.004](https://doi.org/10.1016%2Fj.cl.2011.10.004). [ISSN](./ISSN_(identifier)) [1477-8424](https://search.worldcat.org/issn/1477-8424). Archived from [the original](http://www.dsi.unive.it/~cortesi/paperi/CL2012.pdf) (PDF) on 23 November 2024. Retrieved 18 June 2015.
- Hershey, William; Easthope, Carol (1972). [*A set theoretic data structure and retrieval language*](https://docs.google.com/open?id=0B4t_NX-QeWDYNmVhYjAwMWMtYzc3ZS00YjI0LWJhMjgtZTYyODZmNmFkNThh). Spring Joint Computer Conference, May 1972. *ACM SIGIR Forum*. Vol. 7, no. 4. pp. 45–55. [doi](./Doi_(identifier)):[10.1145/1095495.1095500](https://doi.org/10.1145%2F1095495.1095500).
- Nelson, Anne Fulcher; Nelson, William Harris Morehead (2001). *Building Electronic Commerce: With Web Database Constructions*. Prentice Hall. [ISBN](./ISBN_(identifier)) [978-0201741308](./Special:BookSources/978-0201741308).
- North, Ken (10 March 2010). ["Sets, Data Models and Data Independence"](http://drdobbs.com/blogs/database/228700616). *Dr. Dobb's*. [Archived](https://web.archive.org/web/20121024064523/http://www.drdobbs.com/database/sets-data-models-and-data-independence/228700616) from the original on 24 October 2012.
- Tsitchizris, Dionysios C.; Lochovsky, Fred H. (1982). [*Data Models*](https://archive.org/details/datamodels00tsic). Prentice–Hall. [ISBN](./ISBN_(identifier)) [978-0131964280](./Special:BookSources/978-0131964280).
- Ullman, Jeffrey; Widom, Jennifer (1997). [*A First Course in Database Systems*](https://archive.org/details/firstcourseindat00ullm). Prentice–Hall. [ISBN](./ISBN_(identifier)) [978-0138613372](./Special:BookSources/978-0138613372).
- Wagner, Michael (2010), *SQL/XML:2006 – Evaluierung der Standardkonformität ausgewählter Datenbanksysteme*, Diplomica Verlag, [ISBN](./ISBN_(identifier)) [978-3836696098](./Special:BookSources/978-3836696098)

  

## Further reading

 
- [Ling Liu](./Ling_Liu_(computer_scientist)) and Tamer M. Özsu (Eds.) (2009).  "[Encyclopedia of Database Systems](https://www.springer.com/computer/database+management+&+information+retrieval/book/978-0-387-49616-0), 4100 p. 60 illus. [ISBN](./ISBN_(identifier)) [978-0-387-49616-0](./Special:BookSources/978-0-387-49616-0).
- Gray, J. and Reuter, A. *Transaction Processing: Concepts and Techniques*, 1st edition,  Morgan Kaufmann Publishers, 1992.
- Kroenke, David M. and David J. Auer. *Database Concepts.* 3rd ed. New York: Prentice, 2007.
- [Raghu Ramakrishnan](./Raghu_Ramakrishnan) and [Johannes Gehrke](./Johannes_Gehrke), *[Database Management Systems](http://pages.cs.wisc.edu/~dbbook/)*.
- [Abraham Silberschatz](./Abraham_Silberschatz), [Henry F. Korth](./Henry_F._Korth), S. Sudarshan, *[Database System Concepts](http://www.db-book.com/)*.
- Lightstone, S.; Teorey, T.; Nadeau, T. (2007). *Physical Database Design: the database professional's guide to exploiting indexes, views, storage, and more*. Morgan Kaufmann Press. [ISBN](./ISBN_(identifier)) [978-0-12-369389-1](./Special:BookSources/978-0-12-369389-1).
- Teorey, T.; Lightstone, S. and Nadeau, T. *Database Modeling & Design: Logical Design*, 4th edition, Morgan Kaufmann Press, 2005. [ISBN](./ISBN_(identifier)) [0-12-685352-5](./Special:BookSources/0-12-685352-5).
- *[CMU Database courses playlist](https://www.youtube.com/@CMUDatabaseGroup/playlists)*
- *[MIT OCW 6.830 | Fall 2010 | Database Systems](https://ocw.mit.edu/courses/6-830-database-systems-fall-2010/)*
- *[Berkeley CS W186](https://cs186berkeley.net)*

 

## External links

 
- [DB File extension](http://www.fileextension.org/DB) – information about files with the DB extension

 **Database** at Wikipedia's [sister projects](./Wikipedia:Wikimedia_sister_projects):
- [![Wiktionary logo](//upload.wikimedia.org/wikipedia/commons/thumb/9/99/Wiktionary-logo-en-v2.svg/20px-Wiktionary-logo-en-v2.svg.png)](./File:Wiktionary-logo-en-v2.svg)[**Definitions**](https://en.wiktionary.org/wiki/database) from Wiktionary
- [![Wikimedia Commons logo](//upload.wikimedia.org/wikipedia/en/thumb/4/4a/Commons-logo.svg/20px-Commons-logo.svg.png)](./File:Commons-logo.svg)[**Media**](https://commons.wikimedia.org/wiki/Category:Database) from Commons
- ![](//upload.wikimedia.org/wikipedia/commons/thumb/f/fa/Wikiquote-logo.svg/20px-Wikiquote-logo.svg.png)[**Quotations**](https://en.wikiquote.org/wiki/Special:Search/Database) from Wikiquote
- [![Wikisource logo](//upload.wikimedia.org/wikipedia/commons/thumb/4/4c/Wikisource-logo.svg/20px-Wikisource-logo.svg.png)](./File:Wikisource-logo.svg)[**Texts**](https://en.wikisource.org/wiki/Special:Search/Database) from Wikisource
- [![Wikibooks logo](//upload.wikimedia.org/wikipedia/commons/thumb/f/fa/Wikibooks-logo.svg/20px-Wikibooks-logo.svg.png)](./File:Wikibooks-logo.svg)[**Textbooks**](https://en.wikibooks.org/wiki/Special:Search/Database) from Wikibooks
- [![Wikiversity logo](//upload.wikimedia.org/wikipedia/commons/thumb/0/0b/Wikiversity_logo_2017.svg/40px-Wikiversity_logo_2017.svg.png)](./File:Wikiversity_logo_2017.svg)[**Resources**](https://en.wikiversity.org/wiki/Topic:Databases) from Wikiversity

 
| Links to related articles |
| --- |
| vteComputer scienceThis template follows roughly the 2012ACM Computing Classification SystemHardwarePrinted circuit boardPeripheralIntegrated circuitVery-large-scale integrationSystem on a chip(SoC)Energy consumption(green computing)Electronic design automationHardware accelerationProcessorSize–FormSystemsorganizationComputer architectureComputational complexityDependabilityEmbedded systemReal-time computingCyber-physical systemFault toleranceWireless sensor networkNetworksNetwork architectureNetwork protocolNetwork componentsNetwork schedulerNetwork performance evaluationNetwork serviceSoftwareorganizationInterpreterMiddlewareVirtual machineOperating systemSoftware qualitySoftwarenotations,toolsProgramming paradigmProgramming languageCompilerDomain-specific languageModeling languageSoftware frameworkIntegrated development environmentSoftware configuration managementSoftware librarySoftware repositorySoftwaredevelopmentControl flowSoftware development processRequirements analysisSoftware designSoftware constructionSoftware deploymentSoftware engineeringSoftware maintenanceProgramming teamOpen sourcemodelTheory ofcomputingModel of computationStochasticFormal languageAutomata theoryComputability theoryComputational complexity theoryLogicSemanticsAlgorithmsAlgorithm designAnalysis of algorithmsAlgorithmic efficiencyRandomized algorithmComputational geometryMathematicsofcomputingDiscrete mathematicsProbabilityStatisticsMathematical softwareInformation theoryMathematical analysisNumerical analysisTheoretical computer scienceComputational problemInformationsystemsDatabasemanagementInformation storageEnterprise informationSocial informationGeographic informationDecision supportProcess controlMultimedia informationData miningDigital libraryComputing platformDigital marketingWorld Wide WebInformation retrievalSecurityCryptographyFormal methodsSecurity hackerSecurityservicesIntrusion detection systemHardware securityNetwork securityInformation securityApplication securityHuman-centeredcomputingAccessibilityExtended realityaugmentedvirtualHuman–computer interactionInteraction designMobile computingSocial computingUbiquitous computingVisualizationConcurrencyConcurrent computingParallel computingDistributed computingMultithreadingMultiprocessingArtificialintelligenceComputational intelligenceNatural language processingKnowledge representation and reasoningComputer visionAutomated planning and schedulingSearch methodologyControl methodPhilosophy ofDistributedMachinelearningSupervisedUnsupervisedReinforcementMulti-taskCross-validationGraphicsAnimationRenderingPhotograph manipulationGraphics processing unitImage compressionSolid modelingAppliedcomputingQuantum computingE-commerceEnterprise softwareComputational mathematicsComputational physicsComputational chemistryComputational biologyComputational social scienceComputational engineeringDifferentiable computingComputational healthcareDigital artElectronic publishingCyberwarfareElectronic votingVideo gamesWord processingOperations researchEducational technologyDocument managementOutlineGlossariesCategoryvteDatabaseMainRequirementsTheoryDatabase objectModelsDatabase management systemMachineEngineServerApplicationConnectiondatasourceDSNAdministratorSynonymLockTypesToolsLanguagesData definitionData manipulationQueryinformation retrievalSecurityActivity monitoringAuditForensicsNegative databaseDesignEntities and relationships(andEnhancednotation)NormalizationSchemaRefactoringCardinalityProgrammingAbstraction layerObject–relational mappingManagementVirtualizationTuningcachingMigrationPreservationIntegrityLists ofAcademicBiologicalBiodiversityFacial expressionOnlineOnline musicOnline real estateSee alsoDatabase-centric architectureIntelligent databaseTwo-phase lockingLocks with ordered sharingLoad filePublishingHalloween ProblemLog shippingWikiProjectCategoryvteDatabase management systemsTypesObject-orientedcomparisonRelationallistcomparisonKey–valueColumn-orientedlistDocument-orientedWide-column storeGraphNoSQLNewSQLIn-memorylistMulti-modelcomparisonCloudBlockchain-based databaseConceptsDatabaseACIDArmstrong's axiomsCodd's 12 rulesCAP theoremCRUDNullCandidate keyForeign keyPACELC design principleSuperkeySurrogate keyUnique keyObjectsRelationtablecolumnrowViewTransactionTransaction logTriggerIndexStored procedureCursorPartitionComponentsConcurrency controlData dictionaryJDBCXQJODBCQuery languageQuery optimizerQuery rewriting systemQuery planFunctionsAdministrationQuery optimizationReplicationShardingRelated topicsDatabase modelsDatabase normalizationDatabase storageDistributed databaseFederated database systemReferential integrityRelational algebraRelational calculusRelational modelObject–relational databaseTransaction processingList of SQL software and toolsCategoryOutlinevteData warehousesCreating a data warehouseConceptsDatabaseDimensionDimensional modelingFactOLAPStar schemaSnowflake schemaReverse star schemaAggregateSingle version of the truthVariantsColumn-oriented DBMSData hubData meshEnsemble modeling patternsAnchor modelingData vault modelingFocal point modelingHOLAPMOLAPROLAPOperational data storeElementsData dictionary/MetadataData martSixth normal formSurrogate keyFactFact tableEarly-arriving factMeasureDimensionDimension tableDegenerateSlowly changingFillingExtract, transform, load (ETL)Extract, load, transform (ELT)ExtractTransformLoadUsing a data warehouseConceptsBusiness intelligenceDashboardData miningDecision support system (DSS)OLAP cubeData warehouse automationLanguagesData Mining Extensions (DMX)MultiDimensional eXpressions (MDX)XML for Analysis (XMLA)ToolsBusiness intelligence softwareReporting softwareSpreadsheetRelatedPeopleBill InmonInformation factoryRalph KimballEnterprise busDan LinstedtProductsComparison of OLAP serversData warehousing products and their producersvteDataInformation, data, and valueInformationMetaTypeStructureEcosystemLibraryInfrastructureValueData categories and semantic structureData categoriesMaster dataMaster data managementReference dataTransaction dataAnalytical dataMetadataCode tablesControlled vocabularyCrosswalksHierarchiesObservation dataDark dataTrade and market dataData management and governanceManagementGovernanceCooperativesEthicsStewardshipLineageCurationLocalizationPreservationRetentionPublishingOpen dataMaster data managementReference dataData quality, trust, and protectionQualityInformation qualityValidationCleansingScrubbingIntegrityProtection (privacy)SecurityAnonymizationDe-identificationRe-identificationMinimizationErasureRemanenceCorruptionDegradationLossRecoveryQuality dimensionsAccuracyCompletenessConsistencyTimelinessValidityUniquenessIntegrityConformityRelevanceData engineering and movementEngineeringIntegrationStorageETL/ELTExtractTransformLoadMigrationSynchronizationCompressionFusionFormat managementData preparation and operationsAcquisitionAugmentationCollectionAnnotationEditingDeduplicationPre-processingPreparationProcessingReductionRedundancyWrangling/mungingScrapingRescueAnalysis, science, and interpretationBigAnalysisExplorationMiningScienceTopological data analysisWarehouseBusiness intelligenceData economy and exchangeData economySharingOpen dataPhilanthropyData as a serviceData brokerResponsible reuseExchange, use, and public contextExhaustFarmingArchaeologyDistributed data, domains, and digital twinsData meshData productData domainsData categoriesData digital twinsDigital threadOperational twinsAnalytical twinsVendors and actorsData vendorsData technology vendorsData service providersData brokersChief data officersInformation professionalsCollibraInformaticaIBMSAPOracleSASQlikExperianAlationAtaccamaPreciselyCategoryvteSemantic WebBackgroundDatabasesHypertextInternetOntologiesSemanticsSemantic networksWorld Wide WebSub-topicsDataspacesHyperdataLinked dataRule-based systemsApplicationsSemantic analyticsSemantic computingSemantic mapperSemantic matchingSemantic publishingSemantic reasonerSemantic searchSemantic service-oriented architectureSemantic wikiSolidRelated topicsCollective intelligenceDescription logicFolksonomyGeotaggingInformation architectureiXBRLKnowledge extractionKnowledge managementKnowledge representation and reasoningLibrary 2.0Digital libraryDigital humanitiesMetadataReferencesTopic mapWeb 2.0Web engineeringWeb Science TrustStandardsSyntax and supporting technologiesHTTPIRIURIRDFtriplesRDF/XMLJSON-LDTurtleTriGNotation3N-TriplesTriX(no W3C standard)RRIDSPARQLXMLSemantic HTMLSchemas, ontologies and rulesCommon LogicOWLRDFSRule Interchange FormatSemantic Web Rule LanguageSHACLSemantic annotationCOinSGRDDLMicrodataMicroformatsRDFaSAWSDLFacebook PlatformCommon vocabulariesBIBFRAMEBIBODOAPDublin CoreMODS/MADSFOAFSchema.orgSIOCSKOSMicroformat vocabularieshAtomhCalendarhCardh-feedhProducthRecipehReview | vteComputer science | This template follows roughly the 2012ACM Computing Classification System | Hardware | Printed circuit boardPeripheralIntegrated circuitVery-large-scale integrationSystem on a chip(SoC)Energy consumption(green computing)Electronic design automationHardware accelerationProcessorSize–Form | Systemsorganization | Computer architectureComputational complexityDependabilityEmbedded systemReal-time computingCyber-physical systemFault toleranceWireless sensor network | Networks | Network architectureNetwork protocolNetwork componentsNetwork schedulerNetwork performance evaluationNetwork service | Softwareorganization | InterpreterMiddlewareVirtual machineOperating systemSoftware quality | Softwarenotations,tools | Programming paradigmProgramming languageCompilerDomain-specific languageModeling languageSoftware frameworkIntegrated development environmentSoftware configuration managementSoftware librarySoftware repository | Softwaredevelopment | Control flowSoftware development processRequirements analysisSoftware designSoftware constructionSoftware deploymentSoftware engineeringSoftware maintenanceProgramming teamOpen sourcemodel | Theory ofcomputing | Model of computationStochasticFormal languageAutomata theoryComputability theoryComputational complexity theoryLogicSemantics | Algorithms | Algorithm designAnalysis of algorithmsAlgorithmic efficiencyRandomized algorithmComputational geometry | Mathematicsofcomputing | Discrete mathematicsProbabilityStatisticsMathematical softwareInformation theoryMathematical analysisNumerical analysisTheoretical computer scienceComputational problem | Informationsystems | DatabasemanagementInformation storageEnterprise informationSocial informationGeographic informationDecision supportProcess controlMultimedia informationData miningDigital libraryComputing platformDigital marketingWorld Wide WebInformation retrieval | Security | CryptographyFormal methodsSecurity hackerSecurityservicesIntrusion detection systemHardware securityNetwork securityInformation securityApplication security | Human-centeredcomputing | AccessibilityExtended realityaugmentedvirtualHuman–computer interactionInteraction designMobile computingSocial computingUbiquitous computingVisualization | Concurrency | Concurrent computingParallel computingDistributed computingMultithreadingMultiprocessing | Artificialintelligence | Computational intelligenceNatural language processingKnowledge representation and reasoningComputer visionAutomated planning and schedulingSearch methodologyControl methodPhilosophy ofDistributedMachinelearningSupervisedUnsupervisedReinforcementMulti-taskCross-validation | Computational intelligenceNatural language processingKnowledge representation and reasoningComputer visionAutomated planning and schedulingSearch methodologyControl methodPhilosophy ofDistributed | Machinelearning | SupervisedUnsupervisedReinforcementMulti-taskCross-validation | Graphics | AnimationRenderingPhotograph manipulationGraphics processing unitImage compressionSolid modeling | Appliedcomputing | Quantum computingE-commerceEnterprise softwareComputational mathematicsComputational physicsComputational chemistryComputational biologyComputational social scienceComputational engineeringDifferentiable computingComputational healthcareDigital artElectronic publishingCyberwarfareElectronic votingVideo gamesWord processingOperations researchEducational technologyDocument management | OutlineGlossariesCategory | vteDatabase | Main | RequirementsTheoryDatabase objectModelsDatabase management systemMachineEngineServerApplicationConnectiondatasourceDSNAdministratorSynonymLockTypesTools | Languages | Data definitionData manipulationQueryinformation retrieval | Security | Activity monitoringAuditForensicsNegative database | Design | Entities and relationships(andEnhancednotation)NormalizationSchemaRefactoringCardinality | Programming | Abstraction layerObject–relational mapping | Management | VirtualizationTuningcachingMigrationPreservationIntegrity | Lists of | AcademicBiologicalBiodiversityFacial expressionOnlineOnline musicOnline real estate | See also | Database-centric architectureIntelligent databaseTwo-phase lockingLocks with ordered sharingLoad filePublishingHalloween ProblemLog shipping | WikiProjectCategory | vteDatabase management systems | Types | Object-orientedcomparisonRelationallistcomparisonKey–valueColumn-orientedlistDocument-orientedWide-column storeGraphNoSQLNewSQLIn-memorylistMulti-modelcomparisonCloudBlockchain-based database | Concepts | DatabaseACIDArmstrong's axiomsCodd's 12 rulesCAP theoremCRUDNullCandidate keyForeign keyPACELC design principleSuperkeySurrogate keyUnique key | Objects | RelationtablecolumnrowViewTransactionTransaction logTriggerIndexStored procedureCursorPartition | Components | Concurrency controlData dictionaryJDBCXQJODBCQuery languageQuery optimizerQuery rewriting systemQuery plan | Functions | AdministrationQuery optimizationReplicationSharding | Related topics | Database modelsDatabase normalizationDatabase storageDistributed databaseFederated database systemReferential integrityRelational algebraRelational calculusRelational modelObject–relational databaseTransaction processingList of SQL software and tools | CategoryOutline | vteData warehouses | Creating a data warehouseConceptsDatabaseDimensionDimensional modelingFactOLAPStar schemaSnowflake schemaReverse star schemaAggregateSingle version of the truthVariantsColumn-oriented DBMSData hubData meshEnsemble modeling patternsAnchor modelingData vault modelingFocal point modelingHOLAPMOLAPROLAPOperational data storeElementsData dictionary/MetadataData martSixth normal formSurrogate keyFactFact tableEarly-arriving factMeasureDimensionDimension tableDegenerateSlowly changingFillingExtract, transform, load (ETL)Extract, load, transform (ELT)ExtractTransformLoad | Creating a data warehouse | ConceptsDatabaseDimensionDimensional modelingFactOLAPStar schemaSnowflake schemaReverse star schemaAggregateSingle version of the truthVariantsColumn-oriented DBMSData hubData meshEnsemble modeling patternsAnchor modelingData vault modelingFocal point modelingHOLAPMOLAPROLAPOperational data storeElementsData dictionary/MetadataData martSixth normal formSurrogate keyFactFact tableEarly-arriving factMeasureDimensionDimension tableDegenerateSlowly changingFillingExtract, transform, load (ETL)Extract, load, transform (ELT)ExtractTransformLoad | Concepts | DatabaseDimensionDimensional modelingFactOLAPStar schemaSnowflake schemaReverse star schemaAggregateSingle version of the truth | Variants | Column-oriented DBMSData hubData meshEnsemble modeling patternsAnchor modelingData vault modelingFocal point modelingHOLAPMOLAPROLAPOperational data store | Elements | Data dictionary/MetadataData martSixth normal formSurrogate key | Fact | Fact tableEarly-arriving factMeasure | Dimension | Dimension tableDegenerateSlowly changing | Filling | Extract, transform, load (ETL)Extract, load, transform (ELT)ExtractTransformLoad | Using a data warehouseConceptsBusiness intelligenceDashboardData miningDecision support system (DSS)OLAP cubeData warehouse automationLanguagesData Mining Extensions (DMX)MultiDimensional eXpressions (MDX)XML for Analysis (XMLA)ToolsBusiness intelligence softwareReporting softwareSpreadsheet | Using a data warehouse | ConceptsBusiness intelligenceDashboardData miningDecision support system (DSS)OLAP cubeData warehouse automationLanguagesData Mining Extensions (DMX)MultiDimensional eXpressions (MDX)XML for Analysis (XMLA)ToolsBusiness intelligence softwareReporting softwareSpreadsheet | Concepts | Business intelligenceDashboardData miningDecision support system (DSS)OLAP cubeData warehouse automation | Languages | Data Mining Extensions (DMX)MultiDimensional eXpressions (MDX)XML for Analysis (XMLA) | Tools | Business intelligence softwareReporting softwareSpreadsheet | RelatedPeopleBill InmonInformation factoryRalph KimballEnterprise busDan LinstedtProductsComparison of OLAP serversData warehousing products and their producers | Related | PeopleBill InmonInformation factoryRalph KimballEnterprise busDan LinstedtProductsComparison of OLAP serversData warehousing products and their producers | People | Bill InmonInformation factoryRalph KimballEnterprise busDan Linstedt | Products | Comparison of OLAP serversData warehousing products and their producers | vteData | Information, data, and value | InformationMetaTypeStructureEcosystemLibraryInfrastructureValue | Data categories and semantic structure | Data categoriesMaster dataMaster data managementReference dataTransaction dataAnalytical dataMetadataCode tablesControlled vocabularyCrosswalksHierarchiesObservation dataDark dataTrade and market data | Data management and governance | ManagementGovernanceCooperativesEthicsStewardshipLineageCurationLocalizationPreservationRetentionPublishingOpen dataMaster data managementReference data | Data quality, trust, and protection | QualityInformation qualityValidationCleansingScrubbingIntegrityProtection (privacy)SecurityAnonymizationDe-identificationRe-identificationMinimizationErasureRemanenceCorruptionDegradationLossRecovery | Quality dimensions | AccuracyCompletenessConsistencyTimelinessValidityUniquenessIntegrityConformityRelevance | Data engineering and movement | EngineeringIntegrationStorageETL/ELTExtractTransformLoadMigrationSynchronizationCompressionFusionFormat management | Data preparation and operations | AcquisitionAugmentationCollectionAnnotationEditingDeduplicationPre-processingPreparationProcessingReductionRedundancyWrangling/mungingScrapingRescue | Analysis, science, and interpretation | BigAnalysisExplorationMiningScienceTopological data analysisWarehouseBusiness intelligence | Data economy and exchange | Data economySharingOpen dataPhilanthropyData as a serviceData brokerResponsible reuse | Exchange, use, and public context | ExhaustFarmingArchaeology | Distributed data, domains, and digital twins | Data meshData productData domainsData categoriesData digital twinsDigital threadOperational twinsAnalytical twins | Vendors and actors | Data vendorsData technology vendorsData service providersData brokersChief data officersInformation professionalsCollibraInformaticaIBMSAPOracleSASQlikExperianAlationAtaccamaPrecisely | Category | vteSemantic Web | Background | DatabasesHypertextInternetOntologiesSemanticsSemantic networksWorld Wide Web | Sub-topics | DataspacesHyperdataLinked dataRule-based systems | Applications | Semantic analyticsSemantic computingSemantic mapperSemantic matchingSemantic publishingSemantic reasonerSemantic searchSemantic service-oriented architectureSemantic wikiSolid | Related topics | Collective intelligenceDescription logicFolksonomyGeotaggingInformation architectureiXBRLKnowledge extractionKnowledge managementKnowledge representation and reasoningLibrary 2.0Digital libraryDigital humanitiesMetadataReferencesTopic mapWeb 2.0Web engineeringWeb Science Trust | Standards | Syntax and supporting technologiesHTTPIRIURIRDFtriplesRDF/XMLJSON-LDTurtleTriGNotation3N-TriplesTriX(no W3C standard)RRIDSPARQLXMLSemantic HTMLSchemas, ontologies and rulesCommon LogicOWLRDFSRule Interchange FormatSemantic Web Rule LanguageSHACLSemantic annotationCOinSGRDDLMicrodataMicroformatsRDFaSAWSDLFacebook PlatformCommon vocabulariesBIBFRAMEBIBODOAPDublin CoreMODS/MADSFOAFSchema.orgSIOCSKOSMicroformat vocabularieshAtomhCalendarhCardh-feedhProducthRecipehReview | Syntax and supporting technologies | HTTPIRIURIRDFtriplesRDF/XMLJSON-LDTurtleTriGNotation3N-TriplesTriX(no W3C standard)RRIDSPARQLXMLSemantic HTML | Schemas, ontologies and rules | Common LogicOWLRDFSRule Interchange FormatSemantic Web Rule LanguageSHACL | Semantic annotation | COinSGRDDLMicrodataMicroformatsRDFaSAWSDLFacebook Platform | Common vocabularies | BIBFRAMEBIBODOAPDublin CoreMODS/MADSFOAFSchema.orgSIOCSKOS | Microformat vocabularies | hAtomhCalendarhCardh-feedhProducthRecipehReview |
| vteComputer science |
| This template follows roughly the 2012ACM Computing Classification System |
| Hardware | Printed circuit boardPeripheralIntegrated circuitVery-large-scale integrationSystem on a chip(SoC)Energy consumption(green computing)Electronic design automationHardware accelerationProcessorSize–Form |
| Systemsorganization | Computer architectureComputational complexityDependabilityEmbedded systemReal-time computingCyber-physical systemFault toleranceWireless sensor network |
| Networks | Network architectureNetwork protocolNetwork componentsNetwork schedulerNetwork performance evaluationNetwork service |
| Softwareorganization | InterpreterMiddlewareVirtual machineOperating systemSoftware quality |
| Softwarenotations,tools | Programming paradigmProgramming languageCompilerDomain-specific languageModeling languageSoftware frameworkIntegrated development environmentSoftware configuration managementSoftware librarySoftware repository |
| Softwaredevelopment | Control flowSoftware development processRequirements analysisSoftware designSoftware constructionSoftware deploymentSoftware engineeringSoftware maintenanceProgramming teamOpen sourcemodel |
| Theory ofcomputing | Model of computationStochasticFormal languageAutomata theoryComputability theoryComputational complexity theoryLogicSemantics |
| Algorithms | Algorithm designAnalysis of algorithmsAlgorithmic efficiencyRandomized algorithmComputational geometry |
| Mathematicsofcomputing | Discrete mathematicsProbabilityStatisticsMathematical softwareInformation theoryMathematical analysisNumerical analysisTheoretical computer scienceComputational problem |
| Informationsystems | DatabasemanagementInformation storageEnterprise informationSocial informationGeographic informationDecision supportProcess controlMultimedia informationData miningDigital libraryComputing platformDigital marketingWorld Wide WebInformation retrieval |
| Security | CryptographyFormal methodsSecurity hackerSecurityservicesIntrusion detection systemHardware securityNetwork securityInformation securityApplication security |
| Human-centeredcomputing | AccessibilityExtended realityaugmentedvirtualHuman–computer interactionInteraction designMobile computingSocial computingUbiquitous computingVisualization |
| Concurrency | Concurrent computingParallel computingDistributed computingMultithreadingMultiprocessing |
| Artificialintelligence | Computational intelligenceNatural language processingKnowledge representation and reasoningComputer visionAutomated planning and schedulingSearch methodologyControl methodPhilosophy ofDistributedMachinelearningSupervisedUnsupervisedReinforcementMulti-taskCross-validation | Computational intelligenceNatural language processingKnowledge representation and reasoningComputer visionAutomated planning and schedulingSearch methodologyControl methodPhilosophy ofDistributed | Machinelearning | SupervisedUnsupervisedReinforcementMulti-taskCross-validation |
| Computational intelligenceNatural language processingKnowledge representation and reasoningComputer visionAutomated planning and schedulingSearch methodologyControl methodPhilosophy ofDistributed |
| Machinelearning | SupervisedUnsupervisedReinforcementMulti-taskCross-validation |
| Graphics | AnimationRenderingPhotograph manipulationGraphics processing unitImage compressionSolid modeling |
| Appliedcomputing | Quantum computingE-commerceEnterprise softwareComputational mathematicsComputational physicsComputational chemistryComputational biologyComputational social scienceComputational engineeringDifferentiable computingComputational healthcareDigital artElectronic publishingCyberwarfareElectronic votingVideo gamesWord processingOperations researchEducational technologyDocument management |
| OutlineGlossariesCategory |
| vteDatabase |
| Main | RequirementsTheoryDatabase objectModelsDatabase management systemMachineEngineServerApplicationConnectiondatasourceDSNAdministratorSynonymLockTypesTools |
| Languages | Data definitionData manipulationQueryinformation retrieval |
| Security | Activity monitoringAuditForensicsNegative database |
| Design | Entities and relationships(andEnhancednotation)NormalizationSchemaRefactoringCardinality |
| Programming | Abstraction layerObject–relational mapping |
| Management | VirtualizationTuningcachingMigrationPreservationIntegrity |
| Lists of | AcademicBiologicalBiodiversityFacial expressionOnlineOnline musicOnline real estate |
| See also | Database-centric architectureIntelligent databaseTwo-phase lockingLocks with ordered sharingLoad filePublishingHalloween ProblemLog shipping |
| WikiProjectCategory |
| vteDatabase management systems |
| Types | Object-orientedcomparisonRelationallistcomparisonKey–valueColumn-orientedlistDocument-orientedWide-column storeGraphNoSQLNewSQLIn-memorylistMulti-modelcomparisonCloudBlockchain-based database |
| Concepts | DatabaseACIDArmstrong's axiomsCodd's 12 rulesCAP theoremCRUDNullCandidate keyForeign keyPACELC design principleSuperkeySurrogate keyUnique key |
| Objects | RelationtablecolumnrowViewTransactionTransaction logTriggerIndexStored procedureCursorPartition |
| Components | Concurrency controlData dictionaryJDBCXQJODBCQuery languageQuery optimizerQuery rewriting systemQuery plan |
| Functions | AdministrationQuery optimizationReplicationSharding |
| Related topics | Database modelsDatabase normalizationDatabase storageDistributed databaseFederated database systemReferential integrityRelational algebraRelational calculusRelational modelObject–relational databaseTransaction processingList of SQL software and tools |
| CategoryOutline |
| vteData warehouses |
| Creating a data warehouseConceptsDatabaseDimensionDimensional modelingFactOLAPStar schemaSnowflake schemaReverse star schemaAggregateSingle version of the truthVariantsColumn-oriented DBMSData hubData meshEnsemble modeling patternsAnchor modelingData vault modelingFocal point modelingHOLAPMOLAPROLAPOperational data storeElementsData dictionary/MetadataData martSixth normal formSurrogate keyFactFact tableEarly-arriving factMeasureDimensionDimension tableDegenerateSlowly changingFillingExtract, transform, load (ETL)Extract, load, transform (ELT)ExtractTransformLoad | Creating a data warehouse | ConceptsDatabaseDimensionDimensional modelingFactOLAPStar schemaSnowflake schemaReverse star schemaAggregateSingle version of the truthVariantsColumn-oriented DBMSData hubData meshEnsemble modeling patternsAnchor modelingData vault modelingFocal point modelingHOLAPMOLAPROLAPOperational data storeElementsData dictionary/MetadataData martSixth normal formSurrogate keyFactFact tableEarly-arriving factMeasureDimensionDimension tableDegenerateSlowly changingFillingExtract, transform, load (ETL)Extract, load, transform (ELT)ExtractTransformLoad | Concepts | DatabaseDimensionDimensional modelingFactOLAPStar schemaSnowflake schemaReverse star schemaAggregateSingle version of the truth | Variants | Column-oriented DBMSData hubData meshEnsemble modeling patternsAnchor modelingData vault modelingFocal point modelingHOLAPMOLAPROLAPOperational data store | Elements | Data dictionary/MetadataData martSixth normal formSurrogate key | Fact | Fact tableEarly-arriving factMeasure | Dimension | Dimension tableDegenerateSlowly changing | Filling | Extract, transform, load (ETL)Extract, load, transform (ELT)ExtractTransformLoad |
| Creating a data warehouse |
| ConceptsDatabaseDimensionDimensional modelingFactOLAPStar schemaSnowflake schemaReverse star schemaAggregateSingle version of the truthVariantsColumn-oriented DBMSData hubData meshEnsemble modeling patternsAnchor modelingData vault modelingFocal point modelingHOLAPMOLAPROLAPOperational data storeElementsData dictionary/MetadataData martSixth normal formSurrogate keyFactFact tableEarly-arriving factMeasureDimensionDimension tableDegenerateSlowly changingFillingExtract, transform, load (ETL)Extract, load, transform (ELT)ExtractTransformLoad | Concepts | DatabaseDimensionDimensional modelingFactOLAPStar schemaSnowflake schemaReverse star schemaAggregateSingle version of the truth | Variants | Column-oriented DBMSData hubData meshEnsemble modeling patternsAnchor modelingData vault modelingFocal point modelingHOLAPMOLAPROLAPOperational data store | Elements | Data dictionary/MetadataData martSixth normal formSurrogate key | Fact | Fact tableEarly-arriving factMeasure | Dimension | Dimension tableDegenerateSlowly changing | Filling | Extract, transform, load (ETL)Extract, load, transform (ELT)ExtractTransformLoad |
| Concepts | DatabaseDimensionDimensional modelingFactOLAPStar schemaSnowflake schemaReverse star schemaAggregateSingle version of the truth |
| Variants | Column-oriented DBMSData hubData meshEnsemble modeling patternsAnchor modelingData vault modelingFocal point modelingHOLAPMOLAPROLAPOperational data store |
| Elements | Data dictionary/MetadataData martSixth normal formSurrogate key |
| Fact | Fact tableEarly-arriving factMeasure |
| Dimension | Dimension tableDegenerateSlowly changing |
| Filling | Extract, transform, load (ETL)Extract, load, transform (ELT)ExtractTransformLoad |
| Using a data warehouseConceptsBusiness intelligenceDashboardData miningDecision support system (DSS)OLAP cubeData warehouse automationLanguagesData Mining Extensions (DMX)MultiDimensional eXpressions (MDX)XML for Analysis (XMLA)ToolsBusiness intelligence softwareReporting softwareSpreadsheet | Using a data warehouse | ConceptsBusiness intelligenceDashboardData miningDecision support system (DSS)OLAP cubeData warehouse automationLanguagesData Mining Extensions (DMX)MultiDimensional eXpressions (MDX)XML for Analysis (XMLA)ToolsBusiness intelligence softwareReporting softwareSpreadsheet | Concepts | Business intelligenceDashboardData miningDecision support system (DSS)OLAP cubeData warehouse automation | Languages | Data Mining Extensions (DMX)MultiDimensional eXpressions (MDX)XML for Analysis (XMLA) | Tools | Business intelligence softwareReporting softwareSpreadsheet |
| Using a data warehouse |
| ConceptsBusiness intelligenceDashboardData miningDecision support system (DSS)OLAP cubeData warehouse automationLanguagesData Mining Extensions (DMX)MultiDimensional eXpressions (MDX)XML for Analysis (XMLA)ToolsBusiness intelligence softwareReporting softwareSpreadsheet | Concepts | Business intelligenceDashboardData miningDecision support system (DSS)OLAP cubeData warehouse automation | Languages | Data Mining Extensions (DMX)MultiDimensional eXpressions (MDX)XML for Analysis (XMLA) | Tools | Business intelligence softwareReporting softwareSpreadsheet |
| Concepts | Business intelligenceDashboardData miningDecision support system (DSS)OLAP cubeData warehouse automation |
| Languages | Data Mining Extensions (DMX)MultiDimensional eXpressions (MDX)XML for Analysis (XMLA) |
| Tools | Business intelligence softwareReporting softwareSpreadsheet |
| RelatedPeopleBill InmonInformation factoryRalph KimballEnterprise busDan LinstedtProductsComparison of OLAP serversData warehousing products and their producers | Related | PeopleBill InmonInformation factoryRalph KimballEnterprise busDan LinstedtProductsComparison of OLAP serversData warehousing products and their producers | People | Bill InmonInformation factoryRalph KimballEnterprise busDan Linstedt | Products | Comparison of OLAP serversData warehousing products and their producers |
| Related |
| PeopleBill InmonInformation factoryRalph KimballEnterprise busDan LinstedtProductsComparison of OLAP serversData warehousing products and their producers | People | Bill InmonInformation factoryRalph KimballEnterprise busDan Linstedt | Products | Comparison of OLAP serversData warehousing products and their producers |
| People | Bill InmonInformation factoryRalph KimballEnterprise busDan Linstedt |
| Products | Comparison of OLAP serversData warehousing products and their producers |
| vteData |
| Information, data, and value | InformationMetaTypeStructureEcosystemLibraryInfrastructureValue |
| Data categories and semantic structure | Data categoriesMaster dataMaster data managementReference dataTransaction dataAnalytical dataMetadataCode tablesControlled vocabularyCrosswalksHierarchiesObservation dataDark dataTrade and market data |
| Data management and governance | ManagementGovernanceCooperativesEthicsStewardshipLineageCurationLocalizationPreservationRetentionPublishingOpen dataMaster data managementReference data |
| Data quality, trust, and protection | QualityInformation qualityValidationCleansingScrubbingIntegrityProtection (privacy)SecurityAnonymizationDe-identificationRe-identificationMinimizationErasureRemanenceCorruptionDegradationLossRecovery |
| Quality dimensions | AccuracyCompletenessConsistencyTimelinessValidityUniquenessIntegrityConformityRelevance |
| Data engineering and movement | EngineeringIntegrationStorageETL/ELTExtractTransformLoadMigrationSynchronizationCompressionFusionFormat management |
| Data preparation and operations | AcquisitionAugmentationCollectionAnnotationEditingDeduplicationPre-processingPreparationProcessingReductionRedundancyWrangling/mungingScrapingRescue |
| Analysis, science, and interpretation | BigAnalysisExplorationMiningScienceTopological data analysisWarehouseBusiness intelligence |
| Data economy and exchange | Data economySharingOpen dataPhilanthropyData as a serviceData brokerResponsible reuse |
| Exchange, use, and public context | ExhaustFarmingArchaeology |
| Distributed data, domains, and digital twins | Data meshData productData domainsData categoriesData digital twinsDigital threadOperational twinsAnalytical twins |
| Vendors and actors | Data vendorsData technology vendorsData service providersData brokersChief data officersInformation professionalsCollibraInformaticaIBMSAPOracleSASQlikExperianAlationAtaccamaPrecisely |
| Category |
| vteSemantic Web |
| Background | DatabasesHypertextInternetOntologiesSemanticsSemantic networksWorld Wide Web |
| Sub-topics | DataspacesHyperdataLinked dataRule-based systems |
| Applications | Semantic analyticsSemantic computingSemantic mapperSemantic matchingSemantic publishingSemantic reasonerSemantic searchSemantic service-oriented architectureSemantic wikiSolid |
| Related topics | Collective intelligenceDescription logicFolksonomyGeotaggingInformation architectureiXBRLKnowledge extractionKnowledge managementKnowledge representation and reasoningLibrary 2.0Digital libraryDigital humanitiesMetadataReferencesTopic mapWeb 2.0Web engineeringWeb Science Trust |
| Standards | Syntax and supporting technologiesHTTPIRIURIRDFtriplesRDF/XMLJSON-LDTurtleTriGNotation3N-TriplesTriX(no W3C standard)RRIDSPARQLXMLSemantic HTMLSchemas, ontologies and rulesCommon LogicOWLRDFSRule Interchange FormatSemantic Web Rule LanguageSHACLSemantic annotationCOinSGRDDLMicrodataMicroformatsRDFaSAWSDLFacebook PlatformCommon vocabulariesBIBFRAMEBIBODOAPDublin CoreMODS/MADSFOAFSchema.orgSIOCSKOSMicroformat vocabularieshAtomhCalendarhCardh-feedhProducthRecipehReview | Syntax and supporting technologies | HTTPIRIURIRDFtriplesRDF/XMLJSON-LDTurtleTriGNotation3N-TriplesTriX(no W3C standard)RRIDSPARQLXMLSemantic HTML | Schemas, ontologies and rules | Common LogicOWLRDFSRule Interchange FormatSemantic Web Rule LanguageSHACL | Semantic annotation | COinSGRDDLMicrodataMicroformatsRDFaSAWSDLFacebook Platform | Common vocabularies | BIBFRAMEBIBODOAPDublin CoreMODS/MADSFOAFSchema.orgSIOCSKOS | Microformat vocabularies | hAtomhCalendarhCardh-feedhProducthRecipehReview |
| Syntax and supporting technologies | HTTPIRIURIRDFtriplesRDF/XMLJSON-LDTurtleTriGNotation3N-TriplesTriX(no W3C standard)RRIDSPARQLXMLSemantic HTML |
| Schemas, ontologies and rules | Common LogicOWLRDFSRule Interchange FormatSemantic Web Rule LanguageSHACL |
| Semantic annotation | COinSGRDDLMicrodataMicroformatsRDFaSAWSDLFacebook Platform |
| Common vocabularies | BIBFRAMEBIBODOAPDublin CoreMODS/MADSFOAFSchema.orgSIOCSKOS |
| Microformat vocabularies | hAtomhCalendarhCardh-feedhProducthRecipehReview |

 
| Authority control databases |
| --- |
| International | GNDFAST |
| National | United States23FranceBnF dataJapanCzech RepublicIsrael |
| Other | IdRefNARAEncyclopedia of Modern UkraineYale LUX |