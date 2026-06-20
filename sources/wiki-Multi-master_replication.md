---
source: https://en.wikipedia.org/wiki/Multi-master_replication
fetched: 2026-06-19
---

Method of database replication 
|  | This article includes a list ofgeneral references, butit lacks sufficient correspondinginline citations.Please help toimprovethis article byintroducingmore precise citations.(May 2012)(Learn how and when to remove this message) |
| --- | --- |

 

**Multi-master replication** is a method of database [replication](./Replication_(computer_science)) which allows data to be stored by a group of computers, and updated by any member of the group. All members are responsive to client data queries. The multi-master replication system is responsible for propagating the data modifications made by each member to the rest of the group and resolving any conflicts that might arise between concurrent changes made by different members.

 

Multi-master replication can be contrasted with [master-slave](./Master-slave_(computers)) replication, in which a single member of the group is designated as the "master" for a given piece of data and is the only node allowed to modify that data item. Other members wishing to modify the data item must first contact the master node. Allowing only a single master makes it easier to achieve consistency among the members of the group, but is less flexible than multi-master replication.

 

Multi-master replication can also be contrasted with [failover clustering](./High-availability_cluster) where passive replica servers are replicating the master data in order to prepare for takeover in the event that the master stops functioning. The master is the only server active for client interaction.

 

Often, communication and replication in Multi-master systems are handled via a type of [Consensus algorithm](./Consensus_algorithm), but can also be implemented via custom or proprietary algorithms specific to the software.

 

The primary purposes of multi-master replication are increased availability and faster server response time.[[1]](./Multi-master_replication#cite_note-1)

 

## Advantages

 
- **Availability**: If one master fails, other masters continue to update the [database](./Database).
- **Distributed access:** Masters can be located in several physical sites, i.e. distributed across the network.

 

## Disadvantages

 
- **Consistency**: Most multi-master replication systems are only loosely consistent, i.e. lazy and asynchronous, violating [ACID](./ACID) properties.
- **Performance**: Eager replication systems are complex and increase communication [latency](./Latency_(engineering)).
- **Integrity**: Issues such as conflict resolution can become intractable as the number of nodes involved rises and latency increases.

 

## Implementations

 

### Directory services

 

Many [directory servers](./Directory_service) are based on [Lightweight Directory Access Protocol](./Lightweight_Directory_Access_Protocol) (LDAP) and implement multi-master replication.

 

#### Active Directory

 

One of the more prevalent multi-master replication implementations in directory servers is [Microsoft](./Microsoft)'s [Active Directory](./Active_Directory). Within Active Directory, objects that are updated on one [Domain Controller](./Domain_Controller) are then replicated to other domain controllers through multi-master replication. It is not required for all domain controllers to replicate with each other as this would cause excessive network traffic in large Active Directory deployments. Instead, domain controllers have a complex update pattern that ensures that all servers are updated in a timely fashion without excessive replication traffic. Some Active Directory needs are however better served by [Flexible single master operation](./Flexible_single_master_operation).

 

#### CA Directory

 

[CA Directory](./CA_Directory?action=edit&redlink=1) supports multi-master replication.

 

#### OpenDS/OpenDJ

 

[OpenDS](./OpenDS) (and its successor product [OpenDJ](./OpenDJ)) implemented multi-master since version 1.0.
The OpenDS/OpenDJ multi-master replication is asynchronous, it uses a log with a publish-subscribe mechanism that allows scaling to a large number of nodes. OpenDS/OpenDJ replication does conflict resolution at the entry and attribute level. OpenDS/OpenDJ replication can be used over a [wide area network](./Wide_area_network).

 

#### OpenLDAP

 

[OpenLDAP](./OpenLDAP), the widely used [open-source](./Open-source) LDAP server, implements multi-master replication since version 2.4 (October 2007) [](http://www.openldap.org/software/roadmap.html).

 

### Database management systems

 

#### Amazon Aurora

 

[Amazon Aurora](./Amazon_Aurora) is composed of writer nodes, which replicate redo records, and 6 storage nodes.  The writer node sends change to each storage node, each of which checks for conflicts then reports confirmation or rejection of the change.[[2]](./Multi-master_replication#cite_note-2)

 

#### Apache CouchDB

 

[Apache CouchDB](./CouchDB) uses a simple, HTTP-based multi-master replication system built from its use of an append-only data-store and use of [Multiversion Concurrency Control (MVCC)](./Multiversion_concurrency_control).

 

Each document contains a revision ID, so every record stores the evolutionary timeline of all previous revision IDs leading up to itself—which provides the foundation of CouchDB's [MVCC](./Multiversion_concurrency_control) system. Additionally, it keeps a by-sequence index for the entire database. "The replication process only copies the last revision of a document, so all previous revisions that were only on the source database are not copied to the destination database."[[3]](./Multi-master_replication#cite_note-3)

 

The CouchDB replicator acts as a simple HTTP client acting on both a source and target database. It compares current sequence IDs for the database, calculates revision differences, and makes the necessary changes to the target based on what it found in the history of the source database. Bi-directional replication is the result of merely doing another replication with the source and target values swapped.

 

#### ArangoDB

 

[ArangoDB](./ArangoDB) is a native multi-model database system using multi-master replication.  Clusters in ArangoDB use the CP master/master model with no single point of failure. When a cluster encounters a network partition, ArangoDB prefers to maintain its internal consistency over availability. Clients experience the same view of the database regardless of which node they connect to. And, the cluster continues to serve requests even when one machine fails.[[4]](./Multi-master_replication#cite_note-4)

 

#### Cloudant

 

[Cloudant](./Cloudant), a distributed database system, uses largely the same HTTP API as [Apache CouchDB](./CouchDB), and exposes the same ability to replicate using [Multiversion Concurrency Control (MVCC)](./Multiversion_concurrency_control). Cloudant databases can replicate between each other, but internally, nodes within Cloudant clusters use multi-master replication to stay in sync with each other and provide high availability to API consumers.

 

#### eXtremeDB Cluster

 

eXtremeDB Cluster is the clustering sub-system for McObject's [eXtremeDB](./EXtremeDB) embedded database product family. It maintains database consistency across multiple hardware nodes by replicating transactions in a synchronous manner (two-phase commit).  An important characteristic of eXtremeDB Cluster is [transaction](./Database_transaction) replication, in contrast to log file-based, SQL statement-based, or other replication schemes that may or may not guarantee the success or failure of entire transactions. Accordingly, eXtremeDB Cluster is an [ACID](./ACID) compliant system (not BASE or [eventual consistency](./Eventual_consistency)); a query executed on any cluster node will return the same result as if executed on any other cluster node.

 

#### Oracle

 

[Database](./Database) [clusters](./Computer_cluster) implement multi-master replication using one of two methods. [Asynchronous](https://en.wiktionary.org/wiki/asynchronous) multi-master replication commits data changes to a [deferred transaction queue](./Deferred_transaction_queue?action=edit&redlink=1) which is periodically processed on all databases in the cluster. [Synchronous](./Synchronization_(computer_science)) multi-master replication uses Oracle's two-phase commit functionality to ensure that all databases with the cluster have a consistent [dataset](./Dataset).

 

#### Microsoft SQL

 

[Microsoft SQL](./Microsoft_SQL_Server) provides multi-master replication through peer-to-peer replication. It provides a scale-out and high-availability solution by maintaining copies of data across multiple nodes. Built on the foundation of transactional replication, peer-to-peer replication propagates transactionally consistent changes in near real-time.[[5]](./Multi-master_replication#cite_note-5)

 

#### MySQL / MariaDB

 

At a basic level, it is possible to achieve a multi-master replication scheme beginning with MySQL version 3.23 with circular replication.  
Departing from that, [MariaDB](./MariaDB) and [MySQL](./MySQL) ship with some replication support, each of them with different nuances.

 

In terms of direct support we have:

 

MariaDB: natively supports multi-master replication since version 10.0, but conflict resolution is not supported, so each master must contain different databases. On MySQL, this is named multi-source available since version [5.7.6](https://dev.mysql.com/doc/refman/5.7/en/replication-multi-source.html).

 

MySQL: MySQL Group Replication, a plugin for virtual synchronous multi-master with conflict handling and distributed recovery was released with [5.7.17](http://dev.mysql.com/doc/refman/5.7/en/group-replication.html).

 

Cluster Projects:

 

[MySQL Cluster](./MySQL_Cluster) supports conflict detection and resolution between multiple masters since version 6.3 for true multi-master capability for the MySQL Server.

 

There is also an external project, [Galera Cluster](./Galera_Cluster?action=edit&redlink=1) created by [codership](http://www.codership.com/) [Archived](https://web.archive.org/web/20110927181022/http://codership.com/) 2011-09-27 at the [Wayback Machine](./Wayback_Machine), that provides true multi-master capability, based on a fork of the InnoDB storage engine and custom replication plug-ins. Replication is synchronous, so no conflict is possible.

 

[Percona](./Percona) XtraDB Cluster also is a combination of Galera replication library and MySQL supporting multi-master.

 

#### PostgreSQL

 

Various options for synchronous multi-master replication exist. [Postgres-XL](./Postgres-XL) which is available under the Mozilla Public License, and [PostgresXC](https://web.archive.org/web/20120701122448/http://postgres-xc.sourceforge.net/) (now known as [Postgres-X2](https://github.com/postgres-x2/postgres-x2/)) which is available under the same license as PostgreSQL itself are examples. Note that the [PgCluster](https://web.archive.org/web/20050407084204/http://pgcluster.projects.postgresql.org/) ([Archived](https://web.archive.org/web/20170705002742/http://pgcluster.projects.pgfoundry.org/) 2017-07-05 at the [Wayback Machine](./Wayback_Machine)) project was abandoned in 2007.

 

The replication documentation for [PostgreSQL](./PostgreSQL)[[6]](./Multi-master_replication#cite_note-6) categorises the different types of replication available. Various options exist for distributed multi-master, including [Bucardo](http://bucardo.org/wiki/Bucardo),  [rubyrep](http://www.rubyrep.org) and BDR [Bi-Directional Replication](http://www.2ndQuadrant.com/BDR/).

 

##### PostgreSQL BDR

 

BDR is aimed at eventual inclusion in PostgreSQL core and has been benchmarked as demonstrating significantly enhanced performance[[7]](./Multi-master_replication#cite_note-7) over earlier options. BDR includes replication of data writes (DML), as well as changes to data definition (DDL) and global sequences. BDR nodes may be upgraded online from version 0.9 onwards. 2ndQuadrant has developed BDR continuously since 2012, with the system used in production since 2014. The latest version BDR 3.6 provides column-level conflict detection, CRDTs, eager replication, multi-node query consistency, and many other features.

 

#### Ingres

 
|  | This sectiondoes notciteanysources.Please helpimprove this sectionbyadding citations to reliable sources. Unsourced material may be challenged andremoved.(February 2013)(Learn how and when to remove this message) |
| --- | --- |

 

Within [Ingres](./Ingres_(database))  Replicator, objects that are updated on one Ingres server can then be replicated to other servers whether local or remote through multi-master replication. If one server fails, client connections can be re-directed to another server.  It is not required for all Ingres servers in an environment to replicate with each other as this could cause excessive network traffic in large implementations. Instead, Ingres Replicator allows the appropriate data to be replicated to the appropriate servers without excessive replication traffic.  This means that some servers in the environment can serve as failover candidates while other servers can meet other requirements such as managing a subset of columns or tables for a departmental solution, a subset of rows for a geographical region or one-way replication for a reporting server. In the event of a source, target, or network failure, data integrity is enforced through this [two-phase commit protocol](./Two-phase_commit_protocol) by ensuring that either the whole transaction is replicated, or none of it is. In addition, Ingres Replicator can operate over RDBMS’s from multiple vendors[*[which?](./Wikipedia:Avoid_weasel_words)*] to connect them.

 

## See also

 
- [Flexible single master operation](./Flexible_single_master_operation)
- [Active Directory](./Active_Directory)
- [Distributed database management system](./Distributed_database_management_system)
- [DNS zone transfer](./DNS_zone_transfer)
- [Optimistic replication](./Optimistic_replication)

 

## References

  
1. [↑](./Multi-master_replication#cite_ref-1) [Postgres-XC](https://postgres-xc.sourceforge.net/) [Archived](https://web.archive.org/web/20120701122448/http://postgres-xc.sourceforge.net/) 2012-07-01 at the [Wayback Machine](./Wayback_Machine) under *What Is Postgres-XC?*:Write-scalable means Postgres-XC can be configured with as many database servers as you want and handle many more writes (updating SQL statements) compared to what a single database server can not do
2. [↑](./Multi-master_replication#cite_ref-2) ["Build highly available MySQL applications using Amazon Aurora Multi-Master"](https://aws.amazon.com/blogs/database/building-highly-available-mysql-applications-using-amazon-aurora-mmsr/). 8 August 2019.
3. [↑](./Multi-master_replication#cite_ref-3) ["Apache CouchDB Replication"](http://docs.couchdb.org/en/latest/replication/index.html). Apache Foundation - Apache CouchDB Project.
4. [↑](./Multi-master_replication#cite_ref-4) ["ArangoDB Cluster Architecture"](https://www.arangodb.com/why-arangodb/cluster/). ArangoDB - ArangoDB Architecture.
5. [↑](./Multi-master_replication#cite_ref-5) [Peer-to-Peer Transactional Replication](https://technet.microsoft.com/en-us/library/ms151196.aspx)
6. [↑](./Multi-master_replication#cite_ref-6) [Comparison of different replication solutions for PostgreSQL](http://www.postgresql.org/docs/current/static/different-replication-solutions.html) As found in PostgreSQL 9 documentation. Retrieved 2012-05-08
7. [↑](./Multi-master_replication#cite_ref-7) [BDR Performance](http://2ndquadrant.com/en/resources/bdr/bdr-performance/) Petr Jelinek, 2ndQuadrant. Retrieved 2014-07-10

 

## External links

 
- [Active Directory Replication Concepts](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/get-started/replication/active-directory-replication-concepts)
- [Terms and Definitions for Database Replication](https://web.archive.org/web/20110710093040/http://www.postgres-r.org/documentation/terms)
- [SymmetricDS](http://symmetricds.org/) is database independent, [data synchronization](./Data_synchronization) software. It uses web and database technologies to replicate tables between relational databases in near real time. The software was designed to scale for a large number of databases, work across low-bandwidth connections, and withstand periods of network outage. It supports [MySQL](./MySQL), [Oracle](./Oracle_database), [SQL Server](./Microsoft_SQL_Server), [PostgreSQL](./PostgreSQL), [IBM Db2](./IBM_Db2), [Firebird](./Firebird_(database_server)), [Interbase](./Interbase), [HSQLDB](./HSQLDB), [H2](./H2_(DBMS)), [Apache Derby](./Apache_Derby), [Informix](./Informix), [Greenplum](./Greenplum), [SQLite](./SQLite), [Sybase ASE](./Sybase_ASE), and [Sybase ASA](./Sybase_ASA). Licensed under both open source ([GPL](./GPL)) and commercial licenses.
- [Daffodil Replicator](https://web.archive.org/web/20110314142602/http://opensource.replicator.daffodilsw.com/) is a [Java](./Java_(programming_language)) tool for [data synchronization](./Data_synchronization), [data migration](./Data_migration), and data backup between various database servers. Daffodil Replicator works over standard [JDBC](./JDBC) driver and supports replication across heterogeneous databases. At present, it supports following databases: [Microsoft SQL Server](./Microsoft_SQL_Server), [Oracle](./Oracle_database), Daffodil database, [IBM Db2](./IBM_Db2), [Apache Derby](./Apache_Derby), [MySQL](./MySQL), and [PostgreSQL](./PostgreSQL). Daffodil Replicator is available in both enterprise (commercial) and [open source](./Open-source_license) ([GPL](./GPL)-licensed) versions.
- [DMOZ Open Directory Project - Database Replication Page](http://www.dmoz.org/Computers/Software/Databases/Replication/)