---
source: https://en.wikipedia.org/wiki/Fsync
fetched: 2026-06-19
---

Unix command to commit all data in the kernel filesystem to non-volatile storage buffers  

**sync** is a standard [system call](./System_call) in the [Unix](./Unix) operating system, which commits all data from the [kernel](./Kernel_(operating_system)) [filesystem](./Filesystem) [buffers](./Buffer_(computer_science)) to [non-volatile](./Non-volatile_memory) storage, i.e., data which has been scheduled for writing via low-level [I/O](./Input/output) system calls. Higher-level I/O layers such as [stdio](./C_file_input/output) may maintain separate buffers of their own.

 

As a function in [C](./C_(programming_language)), the `sync()` call is typically declared as `void sync(void)` in `<unistd.h>`. The system call is also available via a [command line](./Command-line_interface) utility also called *sync*, and similarly named functions in other languages such as [Perl](./Perl) and [Node.js](./Node.js) (in the fs module).

 

The related system call `fsync()` commits just the buffered data relating to a specified [file descriptor](./File_descriptor).[[1]](./Sync_(Unix)#cite_note-1) `fdatasync()` is also available to write out just the changes made to the data in the file, and not necessarily the file's related metadata.[[2]](./Sync_(Unix)#cite_note-2)

 

Some Unix systems run a kind of *flush* or *update* [daemon](./Daemon_(computing)), which calls the *sync* function on a regular basis. On some systems, the [cron](./Cron) daemon does this, and on [Linux](./Linux) it was handled by the [pdflush](./Pdflush?action=edit&redlink=1) daemon which was replaced by a new implementation and finally removed from the Linux kernel in 2012.[[3]](./Sync_(Unix)#cite_note-3) Buffers are also flushed when filesystems are [unmounted](./Mount_(computing)) or remounted [read-only](./File-system_permissions),[[4]](./Sync_(Unix)#cite_note-4) for example prior to system shutdown.

 

Some applications, such as [LibreOffice](./LibreOffice), also call the *sync* function to save recovery information in an interval.

 

## Database use

 

In order to provide proper [durability](./Durability_(database_systems)), databases need to use some form of sync in order to make sure the information written has made it to [non-volatile storage](./Non-volatile_storage) rather than just being stored in a memory-based write cache that would be lost if power failed. [PostgreSQL](./PostgreSQL) for example may use a variety of different sync calls, including `fsync()` and `fdatasync()`,[[5]](./Sync_(Unix)#cite_note-5) in order for commits to be durable.[[6]](./Sync_(Unix)#cite_note-6) Unfortunately, for any single client writing a series of records, a rotating hard drive can only commit once per rotation, which makes for at best a few hundred such commits per second.[[7]](./Sync_(Unix)#cite_note-7) Turning off the fsync requirement can therefore greatly improve commit performance, but at the expense of potentially introducing database corruption after a crash.

 

Databases also employ [transaction log](./Transaction_log) files (typically much smaller than the main data files) that have information about recent changes, such that changes can be reliably redone in case of crash; then the main data files can be synced less often.

 

## Error reporting and checking

 

To avoid any data loss return values of `fsync()` should be checked because when performing I/O operations that are buffered by the library or the kernel, errors may not be reported at the time of using the `write()` system call or the `fflush()` call, since the data may not be written to non-volatile storage but only be written to the memory [page cache](./Page_cache). Errors from writes are instead often reported during system calls to `fsync()`, `msync()` or `close()`.[[8]](./Sync_(Unix)#cite_note-8) Prior to 2018, Linux's `fsync()` behavior under certain circumstances failed to report error status,[[9]](./Sync_(Unix)#cite_note-9)[[10]](./Sync_(Unix)#cite_note-10) change behavior was proposed on 23 April 2018.[[11]](./Sync_(Unix)#cite_note-11)

 

## Performance controversies

 

### Hardware-level cache semantics

 

Hard disks may default to using their own volatile write cache to buffer writes, which greatly improves performance while introducing a potential for lost writes if they "lie" about when the data has finished writing.[[12]](./Sync_(Unix)#cite_note-12) Tools such as [hdparm](./Hdparm) -F will instruct the HDD controller to flush the on-drive write cache buffer. The performance impact of turning caching off is so large that even the normally conservative [FreeBSD](./FreeBSD) community rejected disabling write caching by default in FreeBSD 4.3.[[13]](./Sync_(Unix)#cite_note-13)

 

In [SCSI](./SCSI) and in [SATA](./SATA) with [Native Command Queuing](./Native_Command_Queuing) (but not in plain ATA, even with TCQ) the host can specify whether it wants to be notified of completion when the data hits the disk's platters or when it hits the disk's buffer (on-board cache). Assuming a correct hardware implementation, this feature allows the disk's on-board cache to be used while guaranteeing correct semantics for system calls like `fsync`.[[14]](./Sync_(Unix)#cite_note-14) This hardware feature is called [Force Unit Access](./Force_Unit_Access) (FUA) and it allows consistency with less overhead than flushing the entire cache as done for ATA (or SATA non-NCQ) disks.[[15]](./Sync_(Unix)#cite_note-Smith2010-15) Although Linux enabled NCQ around 2007, it did not enable SATA/NCQ FUA until 2012, citing lack of support in the early drives.[[16]](./Sync_(Unix)#cite_note-16)[[17]](./Sync_(Unix)#cite_note-17)

 

### Use in applications

 

Firefox 3.0, released in 2008, introduced `fsync` system calls that were found to degrade its performance; the call was introduced in order to guarantee the integrity of the embedded [SQLite](./SQLite) database.[[18]](./Sync_(Unix)#cite_note-18)
More specifically, the [user interface](./User_interface) thread calls SQLite for every new page visited and the library calls `fsync`. On ext3's `data=ordered` mode, which is a fairly common setup of the time, calling `fsync` means that the *entire* filesytem's write cache is flushed, which can take a long time if the cache contains a lot of other pending operations (e.g. in the middle of copying a large file).[[19]](./Sync_(Unix)#cite_note-19)

 

This event inspired a lot of finger-pointing against the use of `fsync`, claiming performance problems, unnecessary HDD spinups, and/or needing only atomicity and not durability.[[20]](./Sync_(Unix)#cite_note-tso-20) [Linux Foundation](./Linux_Foundation) [chief technical officer](./Chief_technical_officer) [Theodore Ts'o](./Theodore_Ts'o) provided an analysis of the problem:  He responds that there is no need to "fear `fsync`" when used properly, and emphasizes that `fsync` is the only POSIX way to request that a data is written to non-volatile storage. He retorts to the three criticisms of `fsync` stating that (1) the performance impact should be minimal in a typical use case (downloading a file while browsing the web), that `fsync` does not create extra I/O (it only waits for it), and that Firefox was wrong to make so much disk writes when browsing a webpage anyways; (2) that spinup could be avoided by a tweak of the existing `laptop_mode`; and (3) that "atomicity not durability" is a bad security comprise compared to spawning of an I/O thread to run `fsync`.[[20]](./Sync_(Unix)#cite_note-tso-20)

 

Stewart Smith happened to have made a presentation on the use, misuse, and underuse of `fsync` in applications just the year before (2007). Although his talk was mostly about practices detrimental to data integrity (and ways to take care of both speed and safety),[[21]](./Sync_(Unix)#cite_note-21) the "eatmydata" tool for disabling all sync-type calls for a program ended up seeing wider distribution.[[22]](./Sync_(Unix)#cite_note-22) It is mainly used in "throwaway" tasks where data loss is acceptable,[[23]](./Sync_(Unix)#cite_note-23) for example in a temporary environment to speed up package installs.[[24]](./Sync_(Unix)#cite_note-24)

 

## See also

 
- [Page cache](./Page_cache)
- [inode](./Inode)

 

## References

  
1. [↑](./Sync_(Unix)#cite_ref-1) [fsync specification](http://pubs.opengroup.org/onlinepubs/9699919799/functions/fsync.html)
2. [↑](./Sync_(Unix)#cite_ref-2) [fdatasync specification](http://pubs.opengroup.org/onlinepubs/9699919799/functions/fdatasync.html)
3. [↑](./Sync_(Unix)#cite_ref-3) ["R.I.P. Pdflush [LWN.net]"](http://lwn.net/Articles/508212/).
4. [↑](./Sync_(Unix)#cite_ref-4) ["mount - Does umount calls sync to complete any pending writes"](https://unix.stackexchange.com/questions/345917/does-umount-calls-sync-to-complete-any-pending-writes). *Unix & Linux Stack Exchange*. Retrieved 2021-05-02.
5. [↑](./Sync_(Unix)#cite_ref-5) Vondra, Tomas (2 February 2019). ["PostgreSQL vs. fsync"](https://web.archive.org/web/20190210111845/https://ftp.osuosl.org/pub/fosdem/2019/K.1.105/postgresql_fsync.mp4). *Osuosl Org*. Archived from [the original](https://ftp.osuosl.org/pub/fosdem/2019/K.1.105/postgresql_fsync.mp4) (mp4) on 10 February 2019. Retrieved 10 February 2019.
6. [↑](./Sync_(Unix)#cite_ref-6) [PostgreSQL Reliability and the Write-Ahead Log](http://www.postgresql.org/docs/current/static/wal.html)
7. [↑](./Sync_(Unix)#cite_ref-7) [Tuning PostgreSQL WAL Synchronization](http://www.westnet.com/~gsmith/content/postgresql/TuningPGWAL.htm) [Archived](https://web.archive.org/web/20091125043111/http://www.westnet.com/~gsmith/content/postgresql/TuningPGWAL.htm) 2009-11-25 at the [Wayback Machine](./Wayback_Machine)
8. [↑](./Sync_(Unix)#cite_ref-8) ["Ensuring data reaches disk [LWN.net]"](https://lwn.net/Articles/457667/).
9. [↑](./Sync_(Unix)#cite_ref-9) ["PostgreSQL's fsync() surprise [LWN.net]"](https://lwn.net/Articles/752063/).
10. [↑](./Sync_(Unix)#cite_ref-10) ["Improved block-layer error handling [LWN.net]"](https://lwn.net/Articles/724307/).
11. [↑](./Sync_(Unix)#cite_ref-11) ["Always report a writeback error once - Patchwork"](https://web.archive.org/web/20180504092257/https://patchwork.kernel.org/patch/10358111/). Archived from [the original](https://patchwork.kernel.org/patch/10358111/) on 2018-05-04. Retrieved 2018-05-03.
12. [↑](./Sync_(Unix)#cite_ref-12) [Write-Cache Enabled?](http://www.jasonbrome.com/blog/archives/2004/04/03/writecache_enabled.html)
13. [↑](./Sync_(Unix)#cite_ref-13) [FreeBSD Handbook — Tuning Disks](http://www.freebsd.org/doc/en_US.ISO8859-1/books/handbook/configtuning-disk.html#AEN16830)
14. [↑](./Sync_(Unix)#cite_ref-14) [Marshall Kirk McKusick](./Marshall_Kirk_McKusick). ["Disks from the Perspective of a File System - ACM Queue"](http://queue.acm.org/detail.cfm?id=2367378). Queue.acm.org. Retrieved 2014-01-11.
15. [↑](./Sync_(Unix)#cite_ref-Smith2010_15-0) Gregory Smith (2010). *PostgreSQL 9.0: High Performance*. Packt Publishing Ltd. p. 78. [ISBN](./ISBN_(identifier)) [978-1-84951-031-8](./Special:BookSources/978-1-84951-031-8).
16. [↑](./Sync_(Unix)#cite_ref-16) ["Enabling FUA for SATA drives (Was Re: [RFC][PATCH] libata: Enable SATA disk fua detection on default) (Linux SCSI)"](http://www.spinics.net/lists/linux-scsi/msg61241.html).
17. [↑](./Sync_(Unix)#cite_ref-17) ["Linux-Kernel Archive: [PATCH RFC] libata: FUA updates"](http://lkml.indiana.edu/hypermail/linux/kernel/0702.2/1358.html).
18. [↑](./Sync_(Unix)#cite_ref-18) ["Shaver » fsyncers and curveballs"](https://web.archive.org/web/20121209115158/http://shaver.off.net/diary/2008/05/25/fsyncers-and-curveballs/). Archived from [the original](http://shaver.off.net/diary/2008/05/25/fsyncers-and-curveballs/) on 2012-12-09. Retrieved 2009-10-15.
19. [↑](./Sync_(Unix)#cite_ref-19) [Mike Shaver](./Mike_Shaver):
On some rather common Linux configurations, especially using the [ext3](./Ext3) filesystem in the "data=ordered" mode, calling fsync doesn't just flush out the data for the file it's called on, but rather on all the buffered data for that filesystem.
in ["Delayed allocation and the zero-length file problem"](http://thunk.org/tytso/blog/2009/03/12/delayed-allocation-and-the-zero-length-file-problem/).
20. [1](./Sync_(Unix)#cite_ref-tso_20-0) [2](./Sync_(Unix)#cite_ref-tso_20-1) ["Don't fear the fsync!"](http://thunk.org/tytso/blog/2009/03/15/dont-fear-the-fsync/).
21. [↑](./Sync_(Unix)#cite_ref-21) Smith, Stewart (2007). [*eat my data: how everybody gets file IO wrong*](https://mirror.int.linux.conf.au/pub/linux.conf.au/2007/video/wednesday/278.pdf) (PDF). linux.conf.au.
22. [↑](./Sync_(Unix)#cite_ref-22) ["eatmydata (1)  transparently disable fsync() and other data-to-disk synchronization calls"](https://manpages.debian.org/testing/eatmydata/eatmydata.1.en.html).
23. [↑](./Sync_(Unix)#cite_ref-23) ["libeatmydata - disable fsync and SAVE!"](https://www.flamingspork.com/projects/libeatmydata/). *www.flamingspork.com*.
24. [↑](./Sync_(Unix)#cite_ref-24) ["Package: apt-eatmydata (1) - Disable fsync and friends for APT's dpkg calls"](https://packages.debian.org/sid/apt-eatmydata). *packages.debian.org*.

 

## External links

 
- [sync(8) - Linux man page](http://linux.die.net/man/8/sync)
- [http://austingroupbugs.net/view.php?id=672](http://austingroupbugs.net/view.php?id=672)

 
| vteGNU Core Utilitiescommand-line interfaceprograms |
| --- |
| File system | chconchmodchownchgrpcksumcpdddfdirdircolorsinstalllnlsmkdirmkfifomknodmktempmvrealpathrmrmdirshredsynctouchtruncatevdir |
| Text utilities | b2sumbase32base64catcksumcommcsplitcutexpandfmtfoldheadjoinmd5sumnlnumfmtodpasteptxprsha1sumshufsortsplitsumtactailtrtsortunexpanduniqwc |
| Shell utilities | archbasenamechrootdatedirnameduechoenvexprfactorfalsegroupshostididlinklognamenicenohupnprocpathchkpinkyprintenvprintfpwdreadlinkrunconseqsleepstatstdbufsttyteetesttimeouttruettyunameunlinkuptimeuserswhowhoamiyes |