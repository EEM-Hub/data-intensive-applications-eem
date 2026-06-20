---
source: https://en.wikipedia.org/wiki/Stable_storage
fetched: 2026-06-19
---

|  | This articleneeds additional citations forverification.Please helpimprove this articlebyadding citations to reliable sources. Unsourced material may be challenged and removed.Find sources:"Stable storage"–news·newspapers·books·scholar·JSTOR(March 2026)(Learn how and when to remove this message) |
| --- | --- |

 

**Stable storage** is a classification of [computer data storage](./Computer_data_storage) technology that guarantees [atomicity](./Atomicity_(database_systems))[[1]](./Stable_storage#cite_note-1) for any given write operation and allows software to be written that is [robust](./Robustness_(computer_science)) against some hardware and power failures. To be considered atomic, upon reading back a just written-to portion of the disk, the storage subsystem must return either the write data or the data that was on that portion of the disk before the write operations.

 

Most computer [disk drives](./Hard_disk_drive) are not considered stable storage because they do not guarantee atomic write; an error could be returned upon subsequent read of the disk where it was just written to in lieu of either the new or prior data.

 

## Implementation

 

Multiple techniques have been developed to achieve the atomic property from weakly atomic devices such as disks. Writing data to a disk in two places in a specific way is one technique and can be done by [application software](./Application_software).

 

Most often though, stable storage functionality is achieved by [mirroring](./Disk_mirroring) data on separate disks via [RAID](./RAID) technology (level 1 or greater). The RAID controller implements the disk writing [algorithms](./Computer_algorithm) that enable separate disks to act as stable storage.
The RAID technique is robust against some single [disk failure](./Hard_disk_failure) in an array of disks whereas the software technique of writing to separate areas of the same disk only protects against some kinds of internal disk media failures such as bad [sectors](./Disk_sector) in single disk arrangements.

 

## References

  
1. [↑](./Stable_storage#cite_ref-1) Casavant, Thomas L.; Singhal, Mukesh (1994). [*Readings in Distributed Computing Systems*](https://www.google.com/books/edition/Readings_in_Distributed_Computing_System/hlkZAQAAIAAJ?hl=en&gbpv=1&bsq=Stable+storage+guarantees+atomicity&dq=Stable+storage+guarantees+atomicity&printsec=frontcover). IEEE Computer Society Press. p. 555. [ISBN](./ISBN_(identifier)) [978-0-8186-3032-3](./Special:BookSources/978-0-8186-3032-3).

  

 

 
|  | Thiscomputer sciencearticle is astub. You can help Wikipedia byadding missing information. |
| --- | --- |

- [v](./Template:Comp-sci-stub)
- [t](./Template_talk:Comp-sci-stub)
- [e](./Special:EditPage/Template:Comp-sci-stub)

 
|  | Thiscomputer-storage-related article is astub. You can help Wikipedia byadding missing information. |
| --- | --- |

- [v](./Template:Compu-storage-stub)
- [t](./Template_talk:Compu-storage-stub)
- [e](./Special:EditPage/Template:Compu-storage-stub)