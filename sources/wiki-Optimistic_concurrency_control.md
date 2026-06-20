---
source: https://en.wikipedia.org/wiki/Optimistic_concurrency_control
fetched: 2026-06-19
---

Concurrency control method 

**Optimistic concurrency control** (**OCC**), also known as **optimistic locking**, is a [non-locking concurrency control](./Non-lock_concurrency_control) method applied to transactional systems such as [relational database management systems](./Relational_database_management_systems) and [software transactional memory](./Software_transactional_memory). OCC assumes that multiple transactions can frequently complete without interfering with each other. While running, transactions use data resources without acquiring locks on those resources. Before committing, each transaction verifies that no other transaction has modified the data it has read. If the check reveals conflicting modifications, the committing transaction rolls back and can be restarted.[[1]](./Optimistic_concurrency_control#cite_note-1) Optimistic concurrency control was first proposed in 1979 by [H. T. Kung](./H._T._Kung) and John T. Robinson.[[2]](./Optimistic_concurrency_control#cite_note-KungRobinson1981-2)

 

OCC is generally used in environments with low [data contention](./Block_contention). When conflicts are rare, transactions can complete without the expense of managing locks and without having transactions wait for other transactions' locks to clear, leading to higher throughput than other concurrency control methods. However, if contention for data resources is frequent, the cost of repeatedly restarting transactions hurts performance significantly, in which case other [concurrency control](./Concurrency_control) methods may be better suited. However, locking-based ("pessimistic") methods also can deliver poor performance because locking can drastically limit effective concurrency even when deadlocks are avoided.

 

## Phases of optimistic concurrency control

 

Optimistic concurrency control transactions involve these phases:[[2]](./Optimistic_concurrency_control#cite_note-KungRobinson1981-2)

 
- **Begin**: Record a timestamp marking the transaction's beginning.
- **Modify**: Read database values, and tentatively write changes.
- **Validate**: Check whether other transactions have modified data that this transaction has used (read or written). This includes transactions that completed after this transaction's start time, and optionally, transactions that are still active at validation time.
- **Commit/Rollback**: If there is no conflict, make all changes take effect. If there is a conflict, resolve it, typically by aborting the transaction, although other resolution schemes are possible.  Care must be taken to avoid a [time-of-check to time-of-use](./Time-of-check_to_time-of-use) bug, particularly if this phase and the previous one are not performed as a single [atomic](./Linearizability) operation.

 

## Web usage

 

The [stateless](./Stateless_server) nature of [HTTP](./HTTP) makes locking infeasible for web user interfaces. It is common for a user to start editing a record, then leave without following a "cancel" or "logout" link. If locking is used, other users who attempt to edit the same record must wait until the first user's lock times out.

 

[HTTP](./HTTP) does provide a form of built-in OCC. The response to an initial GET request can include an [ETag](./HTTP_ETag) for subsequent PUT requests to use in the If-Match header. Any PUT requests with an out-of-date ETag in the If-Match header can then be rejected.[[3]](./Optimistic_concurrency_control#cite_note-3)

 

Some database management systems offer OCC natively, without requiring special application code. For others, the application can implement an OCC layer outside of the database, and avoid waiting or silently overwriting records. In such cases, the [form](./Form_(web)) may include a hidden field with the record's original content, a timestamp, a sequence number, or an opaque token. On submit, this is compared against the database. If it differs, the conflict resolution algorithm is invoked.

 

### Examples

 
- [MediaWiki](./MediaWiki)'s edit pages use OCC.[[4]](./Optimistic_concurrency_control#cite_note-4)
- [Bugzilla](./Bugzilla) uses OCC; [edit conflicts](./Edit_conflict) are called "mid-air collisions".[[5]](./Optimistic_concurrency_control#cite_note-5)
- The [Ruby on Rails](./Ruby_on_Rails) framework has an API for OCC.[[6]](./Optimistic_concurrency_control#cite_note-6)
- The [Grails](./Grails_(framework)) framework uses OCC in its default conventions.[[7]](./Optimistic_concurrency_control#cite_note-7)
- The [GT.M](./GT.M) database engine uses OCC for managing transactions[[8]](./Optimistic_concurrency_control#cite_note-8) (even single updates are treated as mini-transactions).
- [Microsoft](./Microsoft)'s [Entity Framework](./Entity_Framework) (including Code-First) has built-in support for OCC based on a binary timestamp value.[[9]](./Optimistic_concurrency_control#cite_note-9)
- Most [revision control](./Revision_control) systems support the "merge" model for concurrency, which is OCC.[*[citation needed](./Wikipedia:Citation_needed)*]
- [Mimer SQL](./Mimer_SQL) is a [DBMS](./DBMS) that only implements optimistic concurrency control.[[10]](./Optimistic_concurrency_control#cite_note-10)
- [Google App Engine](./Google_App_Engine) data store uses OCC.[[11]](./Optimistic_concurrency_control#cite_note-11)
- The [Apache Solr](./Apache_Solr) search engine supports OCC via the _version_ field.[[12]](./Optimistic_concurrency_control#cite_note-12)
- The [Elasticsearch](./Elasticsearch) search engine updates its documents via OCC. Each version of a document is assigned a sequence number, and newer versions receive higher sequence numbers. As changes to a document arrive asynchronously, the software can use the sequence number to avoid overriding a newer version with an old one.[[13]](./Optimistic_concurrency_control#cite_note-13)
- [CouchDB](./CouchDB) implements OCC through document revisions.[[14]](./Optimistic_concurrency_control#cite_note-14)
- The [MonetDB](./MonetDB) [column-oriented](./Column-oriented_DBMS) [database management system](./Database_management_system)'s transaction management scheme is based on OCC.[[15]](./Optimistic_concurrency_control#cite_note-15)
- Most implementations of [software transactional memory](./Software_transactional_memory) use OCC.[*[citation needed](./Wikipedia:Citation_needed)*]
- [Redis](./Redis) provides OCC through WATCH command.[[16]](./Optimistic_concurrency_control#cite_note-16)
- [Firebird](./Firebird_(database_server)) uses [Multi-generational architecture](./Multiversion_concurrency_control) as an implementation of OCC for data management.[*[citation needed](./Wikipedia:Citation_needed)*]
- [DynamoDB](./Amazon_DynamoDB) uses conditional update as an implementation of OCC.[[17]](./Optimistic_concurrency_control#cite_note-17)
- [Kubernetes](./Kubernetes) uses OCC when updating resources.[[18]](./Optimistic_concurrency_control#cite_note-18)
- [YugabyteDB](./YugabyteDB) is a cloud-native database that primarily uses OCC.[[19]](./Optimistic_concurrency_control#cite_note-19)
- [Firestore](./Firestore) is a NoSQL database by [Firebase](./Firebase) that uses OCC in its transactions.
- [Apache Iceberg](./Apache_Iceberg) uses OCC to update tables and run maintenance operations on them.

 

## See also

 
- [Server Message Block#Opportunistic locking](./Server_Message_Block#Opportunistic_locking)

 

## References

  
1. [↑](./Optimistic_concurrency_control#cite_ref-1) Johnson, Rohit (2003). ["Common Data Access Issues"](https://web.archive.org/web/20111008203709/http://learning.infocollections.com/ebook%202/Computer/Programming/Java/Expert_One-on-One_J2EE_Design_and_Development/6266final/LiB0080.html). *Expert One-on-One J2EE Design and Development*. Wrox Press. [ISBN](./ISBN_(identifier)) [978-0-7645-4385-2](./Special:BookSources/978-0-7645-4385-2). Archived from [the original](http://learning.infocollections.com/ebook%202/Computer/Programming/Java/Expert_One-on-One_J2EE_Design_and_Development/6266final/LiB0080.html) on 8 October 2011.
2. [1](./Optimistic_concurrency_control#cite_ref-KungRobinson1981_2-0) [2](./Optimistic_concurrency_control#cite_ref-KungRobinson1981_2-1) H. T. Kung, J. T. Robinson (1981). ["On Optimistic Methods for Concurrency Control"](https://apps.dtic.mil/dtic/tr/fulltext/u2/a081452.pdf) (PDF). ACM Transactions on Database Systems. [Archived](https://web.archive.org/web/20190831230313/https://apps.dtic.mil/dtic/tr/fulltext/u2/a081452.pdf) (PDF) from the original on August 31, 2019.
3. [↑](./Optimistic_concurrency_control#cite_ref-3) ["Editing the Web - Detecting the Lost Update Problem Using Unreserved Checkout"](http://www.w3.org/1999/04/Editing/). *W3C Note*. 10 May 1999.
4. [↑](./Optimistic_concurrency_control#cite_ref-4) [Help:Edit conflict](./Help:Edit_conflict) Use interwiki syntax so that mirrors can at least have a chance to pick it up 
5. [↑](./Optimistic_concurrency_control#cite_ref-5) ["Bugzilla: FAQ: Administrative Questions"](https://wiki.mozilla.org/Bugzilla:FAQ#Does_Bugzilla_provide_record_locking_when_there_is_simultaneous_access_to_the_same_bug.3F_Does_the_second_person_get_a_notice_that_the_bug_is_in_use_or_how_are_they_notified.3F). *MozillaWiki*. 11 April 2012.
6. [↑](./Optimistic_concurrency_control#cite_ref-6) ["Module ActiveRecord::Locking"](http://api.rubyonrails.org/classes/ActiveRecord/Locking/Optimistic.html). *Rails Framework Documentation*.
7. [↑](./Optimistic_concurrency_control#cite_ref-7) ["Object Relational Mapping (GORM)"](https://web.archive.org/web/20140815173309/http://grails.org/doc/1.0.x/guide/single.html#5.3.5%20Pessimistic%20and%20Optimistic%20Locking). *Grails Framework Documentation*. Archived from [the original](http://grails.org/doc/1.0.x/guide/single.html#5.3.5%20Pessimistic%20and%20Optimistic%20Locking) on 2014-08-15.
8. [↑](./Optimistic_concurrency_control#cite_ref-8) ["Transaction Processing"](http://tinco.pair.com/bhaskar/gtm/doc/books/pg/UNIX_manual/ch05s17.html). *GT.M Programmers Guide UNIX Edition*.
9. [↑](./Optimistic_concurrency_control#cite_ref-9) ["Handling Concurrency Conflicts"](https://learn.microsoft.com/en-us/ef/core/saving/concurrency?tabs=data-annotations#optimistic-concurrency). *Entity Framework documentation hub*. 5 July 2023.
10. [↑](./Optimistic_concurrency_control#cite_ref-10) ["Transaction Concurrency - Optimistic Concurrency Control"](https://developer.mimer.com/article/transaction-concurrency-optimistic-concurrency-control/). *Mimer Developers - Features*. Retrieved 22 Dec 2023.
11. [↑](./Optimistic_concurrency_control#cite_ref-11) ["The Datastore"](https://code.google.com/appengine/docs/whatisgoogleappengine.html). *What Is Google App Engine?*. 27 August 2010.
12. [↑](./Optimistic_concurrency_control#cite_ref-12) ["Updating Parts of Documents"](https://lucene.apache.org/solr/guide/6_6/updating-parts-of-documents.html). Retrieved 2018-06-28.
13. [↑](./Optimistic_concurrency_control#cite_ref-13) ["Optimistic concurrency control"](https://www.elastic.co/guide/en/elasticsearch/reference/current/optimistic-concurrency-control.html). *Elastic*. Retrieved 2024-02-05.
14. [↑](./Optimistic_concurrency_control#cite_ref-14) ["Technical Overview"](https://docs.couchdb.org/en/stable/intro/overview.html). *Apache CouchDB Documentation*. Retrieved 2024-02-06.
15. [↑](./Optimistic_concurrency_control#cite_ref-15) ["Transactions - MonetDB"](http://www.monetdb.org/Documentation/Manuals/SQLreference/Transactions). 16 January 2013.
16. [↑](./Optimistic_concurrency_control#cite_ref-16) ["Transactions in Redis"](http://redis.io/topics/transactions).
17. [↑](./Optimistic_concurrency_control#cite_ref-17) ["Working with Items and Attributes - Conditional Writes"](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/WorkingWithItems.html#WorkingWithItems.ConditionalUpdate). Retrieved 2 November 2020.
18. [↑](./Optimistic_concurrency_control#cite_ref-18) ["API Overview - Resource Operations"](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.18/#resource-operations-update). Retrieved 3 November 2020.
19. [↑](./Optimistic_concurrency_control#cite_ref-19) Yugabyte, Team. ["Explicit locking | YugabyteDB Docs"](https://web.archive.org/web/20220104081936/https://docs.yugabyte.com/latest/architecture/transactions/explicit-locking/). *docs.yugabyte.com*. Archived from [the original](https://docs.yugabyte.com/latest/architecture/transactions/explicit-locking/) on 2022-01-04. Retrieved 2022-01-04.

 

## External links

 
- Kung, H. T.; John T. Robinson (June 1981). "On optimistic methods for concurrency control". *ACM Transactions on Database Systems*. **6** (2): 213–226. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.101.8988](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.101.8988). [doi](./Doi_(identifier)):[10.1145/319566.319567](https://doi.org/10.1145%2F319566.319567). [S2CID](./S2CID_(identifier)) [61600099](https://api.semanticscholar.org/CorpusID:61600099).
- Enterprise JavaBeans, 3.0, By Bill Burke, Richard Monson-Haefel, Chapter 16. Transactions, Section 16.3.5. Optimistic Locking, Publisher: O'Reilly, Pub Date: May 16, 2006, Print [ISBN](./ISBN_(identifier)) [0-596-00978-X](./Special:BookSources/0-596-00978-X),
- Hollmann, Andreas (May 2009). ["Multi-Isolation: Virtues and Limitations"](http://www.andrej-hollmann.de/images/stories/informatik/multi-isolation-part-1.pdf) (PDF). *Multi-Isolation (what is between pessimistic and optimistic locking)*. 01069 Gutzkovstr. 30/F301.2, Dresden: Happy-Guys Software GbR. p. 8. Retrieved 2013-05-16.`{{cite conference}}`:  CS1 maint: location ([link](./Category:CS1_maint:_location))[*[permanent dead link](./Wikipedia:Link_rot)*]

   Categories