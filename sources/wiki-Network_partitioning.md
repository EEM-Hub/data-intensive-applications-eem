---
source: https://en.wikipedia.org/wiki/Network_partitioning
fetched: 2026-06-19
---

Division of a computer network into subnets This article is about networking hardware and its optimization. For measurement in network science of graph structure, see [Modularity (networks)](./Modularity_(networks)). 

A **network partition** is a division of a computer network into relatively independent [subnets](./Subnetwork), either by design, to optimize them separately, or due to the failure of network devices. Distributed software must be designed to be partition-tolerant, that is, even after the network is partitioned, it still works correctly.

 

For example, in a network with multiple subnets where nodes A and B are located in one subnet and nodes C and D are in another, a partition occurs if the [network switch](./Network_switch) device between the two subnets fails. In that case nodes A and B can no longer communicate with nodes C and D, but all nodes A-D work the same as before.

 

## As a CAP trade-off

 

The [CAP theorem](./CAP_theorem) is based on three trade-offs: [consistency](./Consistency_(database_systems)), [availability](./Availability), and partition tolerance. Partition tolerance, in this context, means the ability of a data processing system to continue processing data even if a network partition causes communication errors between subsystems.[[1]](./Network_partition#cite_note-1)

 

## External links

 
- [Partition of the Large Network](https://www.slideshare.net/DmitryIgnatovPhD/network-optimization-82005426) [Archived](https://web.archive.org/web/20210922175855/https://www.slideshare.net/DmitryIgnatovPhD/network-optimization-82005426) 2021-09-22 at the [Wayback Machine](./Wayback_Machine) [doi:10.13140/RG.2.2.20183.06565/6](//doi.org/10.13140/RG.2.2.20183.06565/6)

 

## References

  
1. [↑](./Network_partition#cite_ref-1) Stonebraker, Michael (April 5, 2010). ["Errors in Database Systems, Eventual Consistency, and the CAP Theorem"](http://cacm.acm.org/blogs/blog-cacm/83396-errors-in-database-systems-eventual-consistency-and-the-cap-theorem/fulltext). Communications of the ACM. [Archived](https://web.archive.org/web/20150123191023/http://cacm.acm.org/blogs/blog-cacm/83396-errors-in-database-systems-eventual-consistency-and-the-cap-theorem/fulltext) from the original on January 23, 2015.