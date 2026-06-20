---
source: https://en.wikipedia.org/wiki/Split-brain_(computing)
fetched: 2026-06-19
---

Concept in computing 
|  | This article has multiple issues.Please helpimprove itor discuss these issues on thetalk page.(Learn how and when to remove these messages)This article or sectionpossibly contains originalsynthesis.Source material shouldverifiably mentionandrelateto the main topic.Relevant discussion may be found on thetalk page.(December 2011)(Learn how and when to remove this message)This articleneeds additional citations forverification.Please helpimprove this articlebyadding citations to reliable sources. Unsourced material may be challenged and removed.Find sources:"Split-brain"computing–news·newspapers·books·scholar·JSTOR(December 2011)(Learn how and when to remove this message)(Learn how and when to remove this message) |  | This article or sectionpossibly contains originalsynthesis.Source material shouldverifiably mentionandrelateto the main topic.Relevant discussion may be found on thetalk page.(December 2011)(Learn how and when to remove this message) |  | This articleneeds additional citations forverification.Please helpimprove this articlebyadding citations to reliable sources. Unsourced material may be challenged and removed.Find sources:"Split-brain"computing–news·newspapers·books·scholar·JSTOR(December 2011)(Learn how and when to remove this message) |
| --- | --- | --- | --- | --- | --- |
|  | This article or sectionpossibly contains originalsynthesis.Source material shouldverifiably mentionandrelateto the main topic.Relevant discussion may be found on thetalk page.(December 2011)(Learn how and when to remove this message) |
|  | This articleneeds additional citations forverification.Please helpimprove this articlebyadding citations to reliable sources. Unsourced material may be challenged and removed.Find sources:"Split-brain"computing–news·newspapers·books·scholar·JSTOR(December 2011)(Learn how and when to remove this message) |

 

In [computing](./Computing), **split-brain** is a state indicating data or availability inconsistencies originating from the maintenance of two separate data sets with overlap in scope, either because of servers in a [network design](./Network_planning_and_design), or a failure condition based on servers not communicating and synchronizing their data to each other. This last case is also commonly referred to as a [network partition](./Network_partition).[*[citation needed](./Wikipedia:Citation_needed)*] The name is based on an analogy with the medical [split-brain](./Split-brain) syndrome.

 

## State

 

Although the term *split-brain* typically refers to an error state, *[split-brain DNS](./Split-horizon_DNS)* (or *split-horizon DNS*) is sometimes used to describe a deliberate situation where internal and external [Domain Name System](./Domain_Name_System) services (DNS services) for a corporate network are not communicating, so that separate DNS name spaces are to be administered for external computers and for internal ones. This requires a double administration, and if there is domain overlap in the computer names, there is a risk that the same [fully qualified domain name](./Fully_qualified_domain_name) (FQDN), may ambiguously occur in both name spaces referring to different computer IP addresses.[[1]](./Split-brain_(computing)#cite_note-1)

 

[High-availability clusters](./High-availability_cluster) (HA clusters) usually use a [heartbeat private network](./Heartbeat_private_network) connection which is used to monitor the health and status of each node in the cluster. For example, the split-brain syndrome may occur when all of the private links go down simultaneously, but the cluster nodes are still running, each one believing they are the only one running. The data sets of each cluster may then randomly serve clients by their own "idiosyncratic" data set updates, without any coordination with the other data sets. This may lead to [data corruption](./Data_corruption) or other data inconsistencies that might require operator intervention and cleanup.

 

## Approaches for dealing with split-brain

 

Davidson et al.,[[2]](./Split-brain_(computing)#cite_note-2) after surveying several approaches to handle the problem, classify them as either optimistic or pessimistic.

 

The optimistic approaches simply let the partitioned nodes work as usual; this provides a greater level of availability, at the cost of sacrificing correctness. Once the problem has ended, automatic or manual reconciliation might be required in order to have the cluster in a consistent state. One current implementation for this approach is [Hazelcast](./Hazelcast), which does automatic reconciliation of its key-value store.[[3]](./Split-brain_(computing)#cite_note-3)

 

The pessimistic approaches sacrifice availability in exchange for consistency. Once a network partitioning has been detected, access to the sub-partitions is limited in order to guarantee consistency. A typical approach, as described by Coulouris et al.,[[4]](./Split-brain_(computing)#cite_note-4) is to use a [quorum](./Quorum_(distributed_computing))-consensus approach. This allows the sub-partition with a majority of the votes to remain available, while the remaining sub-partitions should fall down to an auto-[fencing](./Fencing_(computing)) mode. One current implementation for this approach is the one used by [MongoDB](./MongoDB) replica sets.[[5]](./Split-brain_(computing)#cite_note-5) And another such implementation is Galera replication for [MariaDB](./MariaDB) and [MySQL](./MySQL).[[6]](./Split-brain_(computing)#cite_note-6)

 

Modern commercial general-purpose [HA clusters](./High-availability_cluster) typically use a combination of heartbeat network connections between cluster hosts, and [quorum](./Quorum_(distributed_computing)) witness storage.  The challenge with two-node clusters is that adding a witness device adds cost and complexity (even if implemented in the cloud), but without it, if heartbeat fails, cluster members cannot determine which should be active.  In such clusters (without quorum), if a member fails, even if the members normally assign primary and secondary statuses to the hosts, there is at least a 50% probability that a 2-node HA cluster will totally fail until human intervention is provided, to prevent multiple members becoming active independently and either directly conflicting or corrupting data.

 

## References

 
1. [↑](./Split-brain_(computing)#cite_ref-1) Windows Server 2008 Active Directory, Configuring (2nd Edition) [ISBN](./ISBN_(identifier)) [978-0-7356-5193-7](./Special:BookSources/978-0-7356-5193-7)
2. [↑](./Split-brain_(computing)#cite_ref-2) Davidson, Susan; Garcia-Molina, Hector; Skeen, Dale (1985). "Consistency In A Partitioned Network: A Survey". *ACM Computing Surveys*. **17** (3): 341–370. [doi](./Doi_(identifier)):[10.1145/5505.5508](https://doi.org/10.1145%2F5505.5508). [hdl](./Hdl_(identifier)):[1813/6456](https://hdl.handle.net/1813%2F6456). [S2CID](./S2CID_(identifier)) [8424228](https://api.semanticscholar.org/CorpusID:8424228).
3. [↑](./Split-brain_(computing)#cite_ref-3) ["Hazelcast Documentation"](http://docs.hazelcast.org/docs/3.4/manual/html/networkpartitioning.html). Retrieved 16 February 2015.
4. [↑](./Split-brain_(computing)#cite_ref-4) Coulouris, George; Dollimore, Jean; Kindberg, Tim (2001). *Distributed systems: concepts and design* (3. ed., 1st, 2nd and 3rd impression. ed.). Harlow [u.a.]: Addison-Wesley. [ISBN](./ISBN_(identifier)) [0201-61918-0](./Special:BookSources/0201-61918-0).
5. [↑](./Split-brain_(computing)#cite_ref-5) ["MongoDB Replication Fundamentals"](http://docs.mongodb.org/manual/core/replication/). Retrieved 12 December 2012.
6. [↑](./Split-brain_(computing)#cite_ref-6) ["Weighted Quorum in Galera Cluster"](http://galeracluster.com/documentation-webpages/weightedquorum.html). Retrieved 17 December 2015.