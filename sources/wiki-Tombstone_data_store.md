---
source: https://en.wikipedia.org/wiki/Tombstone_(data_store)
fetched: 2026-06-19
---

Sign in a replica of deleted information 

A **tombstone** is a deleted record in a replica of a [distributed data store](./Distributed_data_store).[[1]](./Tombstone_(data_store)#cite_note-deletion-1) The tombstone is necessary, as distributed data stores use [eventual consistency](./Eventual_consistency), where only a subset of nodes where the data is stored must respond before an operation is considered to be successful.

 

## Motivation

 

If information is deleted in an eventually-consistent distributed data store, the "eventual" part of the eventual consistency causes the information to ooze through the node structure, where some nodes may be unavailable at time of deletion. But a feature of eventual consistency causes a problem in case of deletion, as a node that was unavailable at that time will try to "update" the other nodes that no longer have the deleted entry, assuming that they have missed an insert of information. Therefore, instead of deleting the information, the distributed data store creates a (usually temporary) tombstone record, which is not returned in response to requests.[[1]](./Tombstone_(data_store)#cite_note-deletion-1)

 

## Removal of tombstones

 

In order not to fill the data store with useless information, there is a policy to remove tombstones completely. For this, the system checks the age of the tombstone and removes it after a prescribed time has elapsed. In [Apache Cassandra](./Apache_Cassandra), this elapsed time is set with the `GCGraceSeconds` parameter[[1]](./Tombstone_(data_store)#cite_note-deletion-1) and the process is named Compaction.[[2]](./Tombstone_(data_store)#cite_note-cassandratombstone-2) Compaction consumes system resources and also slows down computation capacity.[[2]](./Tombstone_(data_store)#cite_note-cassandratombstone-2)[[3]](./Tombstone_(data_store)#cite_note-3)

 

## Consequences

 

Because of the delayed removal, the deleted information will appear as empty, after the content of some columns of a number of records has been deleted. After a compaction, the unused columns will be removed from these records.[[4]](./Tombstone_(data_store)#cite_note-4)[*[self-published source](./Wikipedia:Verifiability#Self-published_sources)*]

 

## References

  
1. [1](./Tombstone_(data_store)#cite_ref-deletion_1-0) [2](./Tombstone_(data_store)#cite_ref-deletion_1-1) [3](./Tombstone_(data_store)#cite_ref-deletion_1-2) ["DistributedDeletes"](https://web.archive.org/web/20110511134910/http://wiki.apache.org/cassandra/DistributedDeletes). [Apache Software Foundation](./Apache_Software_Foundation). Archived from [the original](https://wiki.apache.org/cassandra/DistributedDeletes) on 2011-05-11. Retrieved 2011-04-13. Thus, the "eventual" in eventual consistency: if a client reads from a replica that did not get the update with a low enough ConsistencyLevel, it will potentially see old data. [...] There's one more piece to the problem: how do we know when it's safe to remove tombstones? [...] [It] defined a constant, GCGraceSeconds, and had each node track tombstone age locally. Once it has aged past the constant, it can be GC'd during compaction (see MemtableSSTable).
2. [1](./Tombstone_(data_store)#cite_ref-cassandratombstone_2-0) [2](./Tombstone_(data_store)#cite_ref-cassandratombstone_2-1) ["What are Tombstones"](https://docs.datastax.com/en/dse/5.1/dse-arch/datastax_enterprise/dbInternals/archTombstones.html). [Apache Cassandra](./Apache_Cassandra). Retrieved 18 June 2019.
3. [↑](./Tombstone_(data_store)#cite_ref-3) ["Removing tombstones in Cassandra"](https://www.ibm.com/support/knowledgecenter/en/SS3JSW_5.2.0/com.ibm.help.gdha_tuning.doc/com.ibm.help.gdha_tuning.doc/gdha_removing_tombstones.html). [IBM](./IBM). 21 May 2018. Retrieved 18 June 2019.
4. [↑](./Tombstone_(data_store)#cite_ref-4) ["User Guide: Dealing with Tombstones"](https://github.com/rantav/hector/wiki/User-Guide). *[GitHub](./GitHub)*. Retrieved 2011-04-13. To put this in the context of an example, say we have just created 10 rows of data with three columns each. If half the columns are later deleted, and a compaction has not yet occurred, these columns will show up in get_range_slices queries as empty. Using RangeSlicesQuery as described in the previous section, we would have 10 results returned, but only five of them will have values. More importantly, calls to get (via ColumnQuery) by design assume the Column you are retrieving exists in the store. Therefore if you call get on tombstoned data, null is returned (note: this is different than previous versions of Hector where the underlying NotFoundException was propagated up the stack).

 

## External links

 
- [Distributed deletes in Apache Cassandra](https://wiki.apache.org/cassandra/DistributedDeletes) [Archived](https://web.archive.org/web/20110511134910/http://wiki.apache.org/cassandra/DistributedDeletes) 2011-05-11 at the [Wayback Machine](./Wayback_Machine)

 

 Interwikies 

 Categories  

 

 
|  | Thisdatabase-related article is astub. You can help Wikipedia byadding missing information. |
| --- | --- |

- [v](./Template:Database-stub)
- [t](./Template_talk:Database-stub)
- [e](./Special:EditPage/Template:Database-stub)