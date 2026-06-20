---
source: https://en.wikipedia.org/wiki/Journaling_file_system
fetched: 2026-06-19
---

File system for tracking pending changes For the IBM Journaled File System, see [JFS (file system)](./JFS_(file_system)). 

 

A **journaling file system** is a [file system](./File_system) that keeps track of changes not yet committed to the file system's main part by recording the goal of such changes in a data structure known as a "[journal](./Journal_(computing))", which is usually a [circular log](./Circular_log).  In the event of a system crash or power failure, such file systems can be brought back online more quickly with a lower likelihood of becoming [corrupted](./Data_corruption).[[1]](./Journaling_file_system#cite_note-developerworks-1-1)[[2]](./Journaling_file_system#cite_note-ostep-1-2)

 

Depending on the actual implementation, a journaling file system may only keep track of stored [metadata](./Metadata), resulting in improved performance at the expense of increased possibility for data corruption.  Alternatively, a journaling file system may track both stored data and related metadata, while some implementations allow selectable behavior in this regard.[[3]](./Journaling_file_system#cite_note-3)

 

## History

 

In 1990 IBM introduced [JFS](./JFS_(file_system)) in [AIX](./AIX) 3.1 as one of the first UNIX commercial filesystems that implemented journaling.[[4]](./Journaling_file_system#cite_note-4)  The next year the idea was popularized in a widely cited paper on log-structured file systems.[[5]](./Journaling_file_system#cite_note-5)
This was subsequently implemented in Microsoft's [Windows NT](./Windows_NT)'s [NTFS](./NTFS) filesystem in 1993, in Apple's [HFS Plus](./HFS_Plus) filesystem in 1998, and in [Linux](./Linux)'s [ext3](./Ext3) filesystem in 2001.[[6]](./Journaling_file_system#cite_note-6)

 

## Rationale

 

Updating file systems to reflect changes to files and directories usually requires many separate write operations.  This makes it possible for an interruption (like a power failure or system [crash](./Crash_(computing))) between writes to leave data structures in an invalid intermediate state.[[1]](./Journaling_file_system#cite_note-developerworks-1-1)

 

For example, deleting a file on a Unix file system involves three steps:[[7]](./Journaling_file_system#cite_note-7)

 
1. Removing its directory entry.
2. Releasing the [inode](./Inode) to the pool of free inodes.
3. Returning all disk blocks to the pool of free disk blocks.

 

If a crash occurs after step 1 and before step 2, there will be an orphaned inode and hence a [storage leak](./Storage_leak); if a crash occurs between steps 2 and 3, then the blocks previously used by the file cannot be used for new files, effectively decreasing the storage capacity of the file system. Re-arranging the steps does not help, either. If step 3 preceded step 1, a crash between them could allow the file's blocks to be reused for a new file, meaning the partially deleted file would contain part of the contents of another file, and modifications to either file would show up in both. On the other hand, if step 2 preceded step 1, a crash between them would cause the file to be inaccessible, despite appearing to exist.

 

Detecting and recovering from such inconsistencies normally requires a complete [walk](./Glossary_of_graph_theory_terms#walk) of its data structures, for example by a tool such as [fsck](./Fsck) (the file system checker).[[2]](./Journaling_file_system#cite_note-ostep-1-2)  This must typically be done before the file system is next mounted for read-write access.  If the file system is large and if there is relatively little I/O bandwidth, this can take a long time and result in longer downtimes if it blocks the rest of the system from coming back online.

 

To prevent this, a journaled file system allocates a special area—the journal—in which it records the changes it will make ahead of time.  After a crash, recovery simply involves reading the journal from the file system and replaying changes from this journal until the file system is consistent again.  The changes are thus said to be [atomic](./Atomicity_(database_systems)) (not divisible) in that they either succeed (succeeded originally or are replayed completely during recovery), or are not replayed at all (are skipped because they had not yet been completely written to the journal before the crash occurred).

 

## Techniques

 

Some file systems allow the journal to grow, shrink and be re-allocated just as a regular file, while others put the journal in a contiguous area or a hidden file that is guaranteed not to move or change size while the file system is mounted.  Some file systems may also allow *external journals* on a separate device, such as a [solid-state drive](./Solid-state_drive) or battery-backed non-volatile RAM.  Changes to the journal may themselves be journaled for additional redundancy, or the journal may be distributed across multiple physical volumes to protect against device failure.

 

The internal format of the journal must guard against crashes while the journal itself is being written to.  Many journal implementations (such as the JBD2 layer in [ext4](./Ext4)) bracket every change logged with a checksum, on the understanding that a crash would leave a partially written change with a missing (or mismatched) checksum that can simply be ignored when replaying the journal at next remount.

 

### Physical journals

 

A *physical journal* logs an advance copy of every block that will later be written to the main file system.  If there is a crash when the main file system is being written to, the write can simply be replayed to completion when the file system is next mounted.  If there is a crash when the write is being logged to the journal, the partial write will have a missing or mismatched checksum and can be ignored at next mount.

 

Physical journals impose a significant performance penalty because every changed block must be committed *twice* to storage, but may be acceptable when absolute fault protection is required.[[8]](./Journaling_file_system#cite_note-tweedie-1-8)

 

### Logical journals

 

A *logical journal* stores only changes to file [metadata](./Metadata) in the journal, and trades fault tolerance for substantially better write performance.[[9]](./Journaling_file_system#cite_note-9)  A file system with a logical journal still recovers quickly after a crash, but may allow unjournaled file data and journaled metadata to fall out of sync with each other, causing data corruption.

 

For example, appending to a file may involve three separate writes to:

 
1. The file's [inode](./Inode), to note in the file's metadata that its size has increased.
2. The free space map, to mark out an allocation of space for the to-be-appended data.
3. The newly allocated space, to actually write the appended data.

 

In a metadata-only journal, step 3 would not be logged.  If step 3 was not done, but steps 1 and 2 are replayed during recovery, the file will be appended with garbage.

 

### Write hazards

 

The write cache in most operating systems sorts its writes (using the [elevator algorithm](./Elevator_algorithm) or some similar scheme) to maximize throughput.  To avoid an out-of-order write hazard with a metadata-only journal, writes for file data must be sorted so that they are committed to storage before their associated metadata.  This can be tricky to implement because it requires coordination within the operating system kernel between the file system driver and write cache.  An out-of-order write hazard can also occur if a device cannot write blocks immediately to its underlying storage, that is, it cannot flush its write-cache to disk due to deferred write being enabled.

 

To complicate matters, many mass storage devices have their own write caches, in which they may aggressively reorder writes for better performance.  (This is particularly common on magnetic hard drives, which have large seek latencies that can be minimized with elevator sorting.)  Some journaling file systems conservatively assume such write-reordering always takes place, and sacrifice performance for correctness by forcing the device to flush its cache at certain points in the journal (called barriers in [ext3](./Ext3) and [ext4](./Ext4)).[[10]](./Journaling_file_system#cite_note-10)

 

## Alternatives

 

### Soft updates

 

Some [UFS](./Unix_File_System) implementations avoid journaling and instead implement [soft updates](./Soft_updates): they order their writes in such a way that the on-disk file system is never inconsistent, or that the only inconsistency that can be created in the event of a crash is a storage leak.  To recover from these leaks, the free space map is reconciled against a full walk of the file system at next mount.  This [garbage collection](./Garbage_collection_(computer_science)) is usually done in the background.[[11]](./Journaling_file_system#cite_note-11)

 

### Log-structured file systems

 

In [log-structured file systems](./Log-structured_file_system), the write-twice penalty does not apply because the journal itself *is* the file system:  it occupies the entire storage device and is structured so that it can be traversed as would a normal file system.

 

### Copy-on-write file systems

 

Full [copy-on-write](./Copy-on-write) file systems (such as [ZFS](./ZFS) and [Btrfs](./Btrfs)) avoid in-place changes to file data by writing out the data in newly allocated blocks, followed by updated metadata that would point to the new data and disown the old, followed by metadata pointing to that, and so on up to the superblock, or the root of the file system hierarchy.  This has the same correctness-preserving properties as a journal, without the write-twice overhead.

 

## See also

 
- [ACID](./ACID)
- [Comparison of file systems](./Comparison_of_file_systems)
- [Database](./Database)
- [Intent log](./Intent_log)
- [Journaled File System (JFS)](./JFS_(file_system)) –  a file system made by IBM
- [Transaction processing](./Transaction_processing)
- [Versioning file system](./Versioning_file_system)

 

## References

 
1. [1](./Journaling_file_system#cite_ref-developerworks-1_1-0) [2](./Journaling_file_system#cite_ref-developerworks-1_1-1) Jones, M Tim (June 4, 2008), [*Anatomy of Linux journaling file systems*](http://www.ibm.com/developerworks/library/l-journaling-filesystems/index.html), IBM DeveloperWorks, [archived](https://web.archive.org/web/20090221103211/http://www.ibm.com/developerworks/library/l-journaling-filesystems/index.html) from the original on February 21, 2009, retrieved April 13, 2009
2. [1](./Journaling_file_system#cite_ref-ostep-1_2-0) [2](./Journaling_file_system#cite_ref-ostep-1_2-1) Arpaci-Dusseau, Remzi H.; Arpaci-Dusseau, Andrea C. (January 21, 2014), [*Crash Consistency: FSCK and Journaling*](http://pages.cs.wisc.edu/~remzi/OSTEP/file-journaling.pdf) (PDF), Arpaci-Dusseau Books, [archived](https://web.archive.org/web/20140124115718/http://pages.cs.wisc.edu/~remzi/OSTEP/file-journaling.pdf) (PDF) from the original on January 24, 2014, retrieved January 22, 2014
3. [↑](./Journaling_file_system#cite_ref-3) ["tune2fs(8) – Linux man page"](http://linux.die.net/man/8/tune2fs). *linux.die.net*. [Archived](https://web.archive.org/web/20150225155348/http://linux.die.net/man/8/tune2fs) from the original on February 25, 2015. Retrieved February 20, 2015.
4. [↑](./Journaling_file_system#cite_ref-4) Chang, A.; Mergen, M.F.; Rader, R.K.; Roberts, J.A.; Porter, S.L. (January 1990), ["Evolution of storage facilities in AIX Version 3 for RISC System/6000 processors"](https://pdf.zlibcdn.com/dtoken/243353b0d047d2ef2a07fbf41a5fbd40/rd.341.0105.pdf) (PDF), *IBM Journal of Research and Development*, **34:1**: 105–109, [doi](./Doi_(identifier)):[10.1147/rd.341.0105](https://doi.org/10.1147%2Frd.341.0105)
5. [↑](./Journaling_file_system#cite_ref-5) Rosenblum, Mendel; Ousterhout, John (February 1991). [*The Design and Implementation of a Log-Structure File System*](https://people.eecs.berkeley.edu/~brewer/cs262/LFS.pdf) (PDF). ACM 13th Annual Symposium on Operating Systems Principles.
6. [↑](./Journaling_file_system#cite_ref-6) ["'2.4.15-final' - MARC"](https://marc.info/?l=linux-kernel&m=100650331813822&w=2). *marc.info*. Retrieved March 24, 2018.
7. [↑](./Journaling_file_system#cite_ref-7) File Systems from Tanenbaum, A.S. (2008). Modern operating systems (3rd ed., pp. 287). Upper Saddle River, NJ: Prentice Hall.
8. [↑](./Journaling_file_system#cite_ref-tweedie-1_8-0) Tweedie, Stephen (2000), "Ext3, journaling filesystem", *Proceedings of the Ottawa Linux Symposium*: 24–29
9. [↑](./Journaling_file_system#cite_ref-9) Prabhakaran, Vijayan; Arpaci-Dusseau, Andrea C; Arpaci-Dusseau, Remzi H, ["Analysis and Evolution of Journaling File Systems"](https://www.usenix.org/events/usenix05/tech/general/full_papers/prabhakaran/prabhakaran.pdf) (PDF), *2005 USENIX Annual Technical Conference*, USENIX Association, [archived](https://web.archive.org/web/20070926161625/https://www.usenix.org/events/usenix05/tech/general/full_papers/prabhakaran/prabhakaran.pdf) (PDF) from the original on September 26, 2007, retrieved July 27, 2007.
10. [↑](./Journaling_file_system#cite_ref-10) Corbet, Jonathan (May 21, 2008), [*Barriers and journaling filesystems*](https://lwn.net/Articles/283161/), [archived](https://web.archive.org/web/20100314050156/http://lwn.net/Articles/283161/) from the original on March 14, 2010, retrieved March 6, 2010
11. [↑](./Journaling_file_system#cite_ref-11) Seltzer, Margo I; Ganger, Gregory R; McKusick, M Kirk, ["Journaling Versus Soft Updates: Asynchronous Meta-data Protection in File Systems"](http://www.usenix.org/event/usenix2000/general/full_papers/seltzer/seltzer_html), *2000 USENIX Annual Technical Conference*, USENIX Association, [archived](https://web.archive.org/web/20071026004711/http://www.usenix.org/event/usenix2000/general/full_papers/seltzer/seltzer_html/) from the original on October 26, 2007, retrieved July 27, 2007.

 
| vteFile systems |
| --- |
| Comparison of file systemsdistributedUnix filesystem |
| Disk andnon-rotating | ADFSAdvFSAmiga FFSAmiga OFSAPFSAthFSbcachefsBFSBe File SystemBoot File SystemByte File System (z/VM)BtrfsCVFSCXFSDFSEFSEncrypting File SystemExtent File SystemEpisodeextext2ext3ext4FATexFATFiles-11FossilGPFSHAMMERHAMMER2HFS(Classic Mac OS)HFS(MVS)HFS+HPFSHTFSJFSLFSMFSMacintosh File SystemTiVo Media File SystemMINIXNetWare File SystemNext3NILFSNILFS2NSSNTFSOneFSOpenZFSPFSQFSQNX4FSReFSReiserFSReiser4RelianceReliance NitroRFSSFSShared File System (VM)Smart File SystemSNFSSoup (Apple)Tux3UBIFSUFS/UFS2soft updatesWAPBLVxFSWAFLXiafsXFSXsanzFS(z/OS)ZFS(Sun)Optical discHSFISO 9660ISO 13490UDFFlash memoryandSSDAPFSFATexFATTFATEROFSF2FSJFSNVFShost-sidewear levelingCHFSJFFSJFFS2LogFSNILFSNILFS2YAFFSUBIFSDistributed parallelBeeGFSCephCXFSGFS2Google File SystemOCFS2OrangeFSPVFSQFSXsanmore... | ADFSAdvFSAmiga FFSAmiga OFSAPFSAthFSbcachefsBFSBe File SystemBoot File SystemByte File System (z/VM)BtrfsCVFSCXFSDFSEFSEncrypting File SystemExtent File SystemEpisodeextext2ext3ext4FATexFATFiles-11FossilGPFSHAMMERHAMMER2HFS(Classic Mac OS)HFS(MVS)HFS+HPFSHTFSJFSLFSMFSMacintosh File SystemTiVo Media File SystemMINIXNetWare File SystemNext3NILFSNILFS2NSSNTFSOneFSOpenZFSPFSQFSQNX4FSReFSReiserFSReiser4RelianceReliance NitroRFSSFSShared File System (VM)Smart File SystemSNFSSoup (Apple)Tux3UBIFSUFS/UFS2soft updatesWAPBLVxFSWAFLXiafsXFSXsanzFS(z/OS)ZFS(Sun) | Optical disc | HSFISO 9660ISO 13490UDF | Flash memoryandSSD | APFSFATexFATTFATEROFSF2FSJFSNVFShost-sidewear levelingCHFSJFFSJFFS2LogFSNILFSNILFS2YAFFSUBIFS | host-sidewear leveling | CHFSJFFSJFFS2LogFSNILFSNILFS2YAFFSUBIFS | Distributed parallel | BeeGFSCephCXFSGFS2Google File SystemOCFS2OrangeFSPVFSQFSXsanmore... |
| ADFSAdvFSAmiga FFSAmiga OFSAPFSAthFSbcachefsBFSBe File SystemBoot File SystemByte File System (z/VM)BtrfsCVFSCXFSDFSEFSEncrypting File SystemExtent File SystemEpisodeextext2ext3ext4FATexFATFiles-11FossilGPFSHAMMERHAMMER2HFS(Classic Mac OS)HFS(MVS)HFS+HPFSHTFSJFSLFSMFSMacintosh File SystemTiVo Media File SystemMINIXNetWare File SystemNext3NILFSNILFS2NSSNTFSOneFSOpenZFSPFSQFSQNX4FSReFSReiserFSReiser4RelianceReliance NitroRFSSFSShared File System (VM)Smart File SystemSNFSSoup (Apple)Tux3UBIFSUFS/UFS2soft updatesWAPBLVxFSWAFLXiafsXFSXsanzFS(z/OS)ZFS(Sun) |
| Optical disc | HSFISO 9660ISO 13490UDF |
| Flash memoryandSSD | APFSFATexFATTFATEROFSF2FSJFSNVFShost-sidewear levelingCHFSJFFSJFFS2LogFSNILFSNILFS2YAFFSUBIFS | host-sidewear leveling | CHFSJFFSJFFS2LogFSNILFSNILFS2YAFFSUBIFS |
| host-sidewear leveling | CHFSJFFSJFFS2LogFSNILFSNILFS2YAFFSUBIFS |
| Distributed parallel | BeeGFSCephCXFSGFS2Google File SystemOCFS2OrangeFSPVFSQFSXsanmore... |
| NAS | 9PAFS(OpenAFS)AFPCodaDFSGoogle File SystemGPFSLustreNCPNFSPOHMELFSHadoopSMB (CIFS)SSHFSmore... |
| Specialized | AufsAXFSBoot File SystemCompact Disc File SystemcramfsDavfs2EROFSFTPFSFUSELnfsLTFSNOVAMVFSSquashFSUMSDOSOverlayFSUnionFSPseudoconfigfsdevfsdebugfskernfsprocfsspecfssysfstmpfsWinFSEncryptedeCryptfsEncFSEFSRubberhoseSSHFSZFS | AufsAXFSBoot File SystemCompact Disc File SystemcramfsDavfs2EROFSFTPFSFUSELnfsLTFSNOVAMVFSSquashFSUMSDOSOverlayFSUnionFS | Pseudo | configfsdevfsdebugfskernfsprocfsspecfssysfstmpfsWinFS | Encrypted | eCryptfsEncFSEFSRubberhoseSSHFSZFS |
| AufsAXFSBoot File SystemCompact Disc File SystemcramfsDavfs2EROFSFTPFSFUSELnfsLTFSNOVAMVFSSquashFSUMSDOSOverlayFSUnionFS |
| Pseudo | configfsdevfsdebugfskernfsprocfsspecfssysfstmpfsWinFS |
| Encrypted | eCryptfsEncFSEFSRubberhoseSSHFSZFS |
| Types | ClusteredGlobalGridSelf-certifyingFlashJournalingLog-structuredObjectRecord-orientedSemanticSteganographicSyntheticVersioning |
| Features | Case preservationCopy-on-writeData deduplicationData scrubbingExecute in placeExtentFile attributeExtended file attributesFile change logForkInodeLinksHardSymbolicAccess controlAccess-control listFilesystem-level encryptionPermissionsModesSticky bit | Case preservationCopy-on-writeData deduplicationData scrubbingExecute in placeExtentFile attributeExtended file attributesFile change logForkInodeLinksHardSymbolic | Access control | Access-control listFilesystem-level encryptionPermissionsModesSticky bit |
| Case preservationCopy-on-writeData deduplicationData scrubbingExecute in placeExtentFile attributeExtended file attributesFile change logForkInodeLinksHardSymbolic |
| Access control | Access-control listFilesystem-level encryptionPermissionsModesSticky bit |
| Interfaces | File managerFile system APIInstallable File SystemVirtual file system |
| Lists | CryptographicDefaultLog-structured |
| Layouts | Master Boot RecordGUID Partition TableApple Partition Map |

 
| vteOperating systems |
| --- |
| General | ComparisonForensic engineeringHistoryListTimelineUsage shareUser features comparison |
| Variants | Disk operating systemDistributed operating systemEmbedded operating systemHobbyist operating systemJust enough operating systemMobile operating systemNetwork operating systemObject-oriented operating systemReal-time operating systemSupercomputer operating system |
| Kernel | ArchitecturesExokernelHybridMicrokernelMonolithicMultikernelvkernelRump kernelUnikernelComponentsDevice driverLoadable kernel moduleUser space and kernel space | Architectures | ExokernelHybridMicrokernelMonolithicMultikernelvkernelRump kernelUnikernel | Components | Device driverLoadable kernel moduleUser space and kernel space |
| Architectures | ExokernelHybridMicrokernelMonolithicMultikernelvkernelRump kernelUnikernel |
| Components | Device driverLoadable kernel moduleUser space and kernel space |
| Process management | ConceptsComputer multitasking(Cooperative,Preemptive)Context switchInterruptIPCProcessProcess control blockReal-timeThreadTime-sharingSchedulingalgorithmsFixed-priority preemptiveMultilevel feedback queueRound-robinShortest job next | Concepts | Computer multitasking(Cooperative,Preemptive)Context switchInterruptIPCProcessProcess control blockReal-timeThreadTime-sharing | Schedulingalgorithms | Fixed-priority preemptiveMultilevel feedback queueRound-robinShortest job next |
| Concepts | Computer multitasking(Cooperative,Preemptive)Context switchInterruptIPCProcessProcess control blockReal-timeThreadTime-sharing |
| Schedulingalgorithms | Fixed-priority preemptiveMultilevel feedback queueRound-robinShortest job next |
| Memory management,resourceprotection | Bus errorGeneral protection faultMemory pagingMemory protectionProtection ringSegmentation faultVirtual memory |
| Storageaccess,file systems | Boot loaderDefragmentationDevice fileFile attributeInodeJournalPartitionVirtual file systemVirtual tape library |
| Supporting concepts | APIComputer networkHALLive CDLive USBShellCLIUser interfacePXE |