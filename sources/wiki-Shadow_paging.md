---
source: https://en.wikipedia.org/wiki/Shadow_paging
fetched: 2026-06-19
---

|  | This article includes alist of references,related reading, orexternal links,but its sources remain unclear because it lacksinline citations.Please helpimprovethis article byintroducingmore precise citations.(January 2014)(Learn how and when to remove this message) |
| --- | --- |

 

In [computer science](./Computer_science), **shadow paging** is a technique for providing [atomicity](./Atomic_(computer_science)) and [durability](./Durability_(computer_science)) (two of the [ACID](./ACID) properties) in [database systems](./Database_system). A *page* in this context refers to a unit of physical storage (probably on a [hard disk](./Hard_disk)), typically of the order of 1 to 64 [KiB](./KiB).

 

Shadow paging is a [copy-on-write](./Copy-on-write) technique for avoiding [in-place](./In-place) updates of pages. Instead, when a page is to be modified, a *shadow page* is allocated. Since the shadow page has no references (from other pages on disk), it can be modified without concern for consistency constraints, etc. When the page is ready to become durable, all pages that referred to the original are updated to refer to the new replacement page instead. Since the page is "activated" only when it is ready, it is [atomic](./Atomic_(computer_science)).

 

If the referring pages must also be updated via shadow paging, this procedure may [recurse](./Recursion) many times, becoming costly. One solution, employed by the [Write Anywhere File Layout](./Write_Anywhere_File_Layout) (WAFL) file system, is to be lazy about making pages durable (i.e., write-behind caching). This increases performance significantly by avoiding many writes on hotspots high in the referential hierarchy (e.g., a file system superblock) at the cost of high commit latency.[[1]](./Shadow_paging#cite_note-1)

 

[Write-ahead logging](./Write-ahead_logging) is a more popular solution that uses in-place updates.[*[citation needed](./Wikipedia:Citation_needed)*]

 

Shadow paging is similar to the **old master–new master** batch processing technique used in mainframe database systems. In these systems, the output of each batch run (possibly a day's work) was written to two separate [disks](./Hard_disk) or other form of storage medium. One was kept for backup, and the other was used as the starting point for the next day's work.

 

Shadow paging is also similar to [purely functional data structures](./Purely_functional_data_structure), in that in-place updates are avoided.

 

## References

  
1. [↑](./Shadow_paging#cite_ref-1) ["File System Design for an NFS File Server Appliance"](https://www.cs.princeton.edu/courses/archive/fall09/cos318/reading/netapp.pdf) (PDF). 1994. Retrieved 1 November 2019. `{{cite journal}}`: Cite journal requires `|journal=` ([help](./Help:CS1_errors#missing_periodical))