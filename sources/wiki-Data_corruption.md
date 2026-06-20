---
source: https://en.wikipedia.org/wiki/Data_corruption
fetched: 2026-06-19
---

Errors in computer data that introduce unintended changes to the original data "Corrupted" redirects here. For the Japanese metal band, see [Corrupted (band)](./Corrupted_(band)). [![](//upload.wikimedia.org/wikipedia/commons/thumb/6/63/Data_loss_of_image_file.JPG/250px-Data_loss_of_image_file.JPG)](./File:Data_loss_of_image_file.JPG)Photo data corruption; in this case, a result of a failed data recovery from a hard disk drive 

**Data corruption** is the undesired alteration in [computer data](./Computer_data) that occurs during writing, reading, storage, transmission, or processing. Computer systems use a number of measures to provide end-to-end [data integrity](./Data_integrity), or lack of errors.

 

In general, when data corruption occurs, a [file](./Computer_file) containing that data will produce unexpected results when accessed by the system or the related application. Results could range from a minor loss of data to a system crash. For example, if a [document file](./Document_file_format) is corrupted, when a person tries to open that file with a document editor they may get an [error message](./Error_message), thus the file might not be opened or might open with some of the data corrupted (or in some cases, completely corrupted, leaving the document unintelligible). The adjacent image is a corrupted image file in which most of the information has been lost.

 

Some types of [malware](./Malware) may intentionally corrupt files as part of their [payloads](./Payload_(computing)), usually by overwriting them with inoperative or garbage code, while a non-malicious virus may also unintentionally corrupt files when it accesses them. If a virus or [trojan](./Trojan_horse_(computing)) with this payload method manages to alter files critical to the running of the computer's operating system software or physical hardware, the entire system may be rendered unusable.

 

Some programs can give a suggestion to repair the file automatically (after the error), and some programs cannot repair it. It depends on the level of corruption, and the built-in functionality of the application to handle the error. There are various causes of the corruption.

 

## Overview

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/9/99/Atari_2600_with_corrupted_ram.jpg/250px-Atari_2600_with_corrupted_ram.jpg)](./File:Atari_2600_with_corrupted_ram.jpg)Screen output of an Atari 2600 with corrupted RAM. A video that has been corrupted, displaying bright flashing light and color 

There are two types of data corruption associated with computer systems: undetected and detected.  Undetected data corruption, also known as *silent data corruption*, results in the most dangerous errors as there is no indication that the data is incorrect.  Detected
data corruption may be permanent with the loss of data, or may be temporary when some part of the system is able to detect and correct the error; there is no data corruption in the latter case.

 

Data corruption can occur at any level in a system, from the host to the storage medium.  Modern systems attempt to detect corruption at many layers and then recover or correct the corruption; this is almost always successful but very rarely the information arriving in the systems memory is corrupted and can cause unpredictable results.

 &#x2D; Add Data corruption at the system level  

Data corruption during transmission has a variety of causes. Interruption of data transmission causes [information loss](./Data_loss). Environmental conditions can interfere with data transmission, especially when dealing with wireless transmission methods. Heavy clouds can block satellite transmissions. Wireless networks are susceptible to interference from devices such as microwave ovens.

 &#x2D; Add Data corruption at the storage level  

Hardware and software failure are the two main causes for [data loss](./Data_loss).  [Background radiation](./Background_radiation), [head crashes](./Head_crash), and [aging](./Mean_time_between_failures) or wear of the storage device fall into the former category, while software failure typically occurs due to [bugs](./Software_bug) in the code.
[Cosmic rays](./Cosmic_ray) cause most [soft errors](./Soft_error) in DRAM.[[1]](./Data_corruption#cite_note-1)

 

## Silent

 See also: [Hard disk drive error rates and handling](./Hard_disk_drive_error_rates_and_handling) 

Some errors go unnoticed, without being detected by the disk firmware or the host operating system; these errors are known as *silent data corruption*.[[2]](./Data_corruption#cite_note-2)

 

There are many error sources beyond the disk storage subsystem itself. For instance, cables might be slightly loose, the power supply might be unreliable,[[3]](./Data_corruption#cite_note-3) external vibrations such as a loud sound,[[4]](./Data_corruption#cite_note-4) the network might introduce undetected corruption,[[5]](./Data_corruption#cite_note-5) [cosmic radiation](./Cosmic_ray#Effect_on_electronics) and many other causes of [soft memory errors](./Soft_error), etc. In 39,000 storage systems that were analyzed, firmware bugs accounted for 5–10% of storage failures.[[6]](./Data_corruption#cite_note-6) The error rates as observed by a [CERN](./CERN) study on silent corruption are far higher than one in every 1016 bits.[[7]](./Data_corruption#cite_note-CERN2007-7) [Amazon Web Services](./Amazon_Web_Services) acknowledged that data corruption was the cause of a widespread outage of their [Amazon S3](./Amazon_S3) storage network in 2008.[[8]](./Data_corruption#cite_note-8) In 2021, faulty processor cores were identified as an additional cause in publications by Google and Facebook; cores were found to be faulty at a rate of several in thousands of cores.[[9]](./Data_corruption#cite_note-9)[[10]](./Data_corruption#cite_note-10)

 

One problem is that hard disk drive capacities have increased substantially, but their error rates remain unchanged. The data corruption rate has always been roughly constant in time, meaning that modern disks are not much safer than old disks. In old disks the probability of data corruption was very small because they stored tiny amounts of data. In modern disks the probability is much larger because they store much more data, whilst not being safer. That way, silent data corruption has not been a serious concern while storage devices remained relatively small and slow. In modern times and with the advent of larger drives and very fast RAID setups, users are capable of transferring 1016 bits in a reasonably short time, thus easily reaching the data corruption thresholds.[[11]](./Data_corruption#cite_note-11)

 

As an example, [ZFS](./ZFS) creator Jeff Bonwick stated that the fast database at [Greenplum](./Greenplum), which is a database software company specializing in large-scale data warehousing and analytics, faces silent corruption every 15 minutes.[[12]](./Data_corruption#cite_note-12)  As another example, a real-life study performed by [NetApp](./NetApp) on more than 1.5 million HDDs over 41 months found more than 400,000 silent data corruptions, out of which more than 30,000 were not detected by the hardware RAID controller (only detected during [scrubbing](./Data_scrubbing)).[[13]](./Data_corruption#cite_note-13)  Another study, performed by [CERN](./CERN) over six months and involving about 97 [petabytes](./Petabytes) of data, found that about 128 [megabytes](./Megabytes) of data became permanently corrupted silently somewhere in the pathway from network to disk.[[14]](./Data_corruption#cite_note-14)

 

Silent data corruption may result in [cascading failures](./Cascading_failure), in which the system may run for a period of time with undetected initial error causing increasingly more problems until it is ultimately detected.[[15]](./Data_corruption#cite_note-15)  For example, a failure affecting file system [metadata](./Metadata) can result in multiple files being partially damaged or made completely inaccessible as the file system is used in its corrupted state.

 

## Countermeasures

 See also: [Error detection and correction](./Error_detection_and_correction) 

When data corruption behaves as a [Poisson process](./Poisson_process), where each [bit](./Bit) of data has an independently low probability of being changed, data corruption can generally be detected by the use of [checksums](./Checksum), and can often be [corrected](./Error_detection_and_correction) by the use of [error correcting codes](./Error_correcting_code) (ECC).

 

If an uncorrectable data corruption is detected, procedures such as automatic retransmission or restoration from [backups](./Backup) can be applied. Certain levels of [RAID](./Redundant_array_of_independent_disks) disk arrays have the ability to store and evaluate [parity bits](./Parity_bit) for data across a set of hard disks and can reconstruct corrupted data upon the failure of a single or multiple disks, depending on the level of RAID implemented.  Some [CPU](./CPU) architectures employ various transparent checks to detect and mitigate data corruption in [CPU caches](./CPU_cache), [CPU buffers](./Data_buffer) and [instruction pipelines](./Instruction_pipeline); an example is *Intel Instruction Replay* technology, which is available on [Intel Itanium](./Intel_Itanium) processors.[[16]](./Data_corruption#cite_note-16)

 

Many errors are detected and corrected by the hard disk drives using the ECC codes[[17]](./Data_corruption#cite_note-17) which are stored on disk for each sector.  If the disk drive detects multiple read errors on a sector it may make a copy of the failing sector on another part of the disk, by remapping the failed sector of the disk to a spare sector without the involvement of the operating system (though this may be delayed until the next write to the sector).  This "silent correction" can be monitored using [S.M.A.R.T.](./Self-Monitoring,_Analysis_and_Reporting_Technology) and tools available for most operating systems to automatically check the disk drive for impending failures by watching for deteriorating SMART parameters.

 

Some [file systems](./File_systems), such as [Btrfs](./Btrfs), [HAMMER](./HAMMER_(file_system)), [ReFS](./ReFS), and [ZFS](./ZFS), use internal data and [metadata](./Metadata) checksumming to detect silent data corruption.  In addition, if a corruption is detected and the file system uses integrated RAID mechanisms that provide [data redundancy](./Data_redundancy), such file systems can also reconstruct corrupted data in a transparent way.[[18]](./Data_corruption#cite_note-18)  This approach allows improved data integrity protection covering the entire data paths, which is usually known as *end-to-end data protection*, compared with other data integrity approaches that do not span different layers in the storage stack and allow data corruption to occur while the data passes boundaries between the different layers.[[19]](./Data_corruption#cite_note-Zhang2010-19)

 

*[Data scrubbing](./Data_scrubbing)* is another method to reduce the likelihood of data corruption, as disk errors are caught and recovered from before multiple errors accumulate and overwhelm the number of parity bits.  Instead of parity being checked on each read, the parity is checked during a regular scan of the disk, often done as a low priority background process. The "data scrubbing" operation activates a parity check.  If a user simply runs a normal program that reads data from the disk, then the parity would not be checked unless parity-check-on-read was both supported and enabled on the disk subsystem.

 

If appropriate mechanisms are employed to detect and remedy data corruption, data integrity can be maintained. This is particularly important in commercial applications (e.g. [banking](./Banking)), where an undetected error could either corrupt a database index or change data to drastically affect an account balance, and in the use of [encrypted](./Encryption) or [compressed](./Data_compression) data, where a small error can make an extensive dataset unusable.[[7]](./Data_corruption#cite_note-CERN2007-7)

 

## See also

  
- Various resources:

- [Data degradation](./Data_degradation), also called data rot
- [Computer science](./Computer_science)
- [Data integrity](./Data_integrity)
- [Database integrity](./Database_integrity)
- [Radiation hardening](./Radiation_hardening)
- [Software rot](./Software_rot)

- Countermeasures:

- [Data Integrity Field](./Data_Integrity_Field)
- [ECC memory](./ECC_memory)
- [Forward error correction](./Forward_error_correction)
- [List of data recovery software](./List_of_data_recovery_software)
- [Parchive](./Parchive)
- [RAID](./RAID)
- [Reed–Solomon error correction](./Reed–Solomon_error_correction)

  

## References

 
1. [↑](./Data_corruption#cite_ref-1) [Scientific American](./Scientific_American) (2008-07-21). ["Solar Storms: Fast Facts"](http://www.scientificamerican.com/article.cfm?id=solar-storms-fast-facts). [Nature Publishing Group](./Nature_Publishing_Group). [Archived](https://web.archive.org/web/20101226165751/http://www.scientificamerican.com/article.cfm?id=solar-storms-fast-facts) from the original on 2010-12-26. Retrieved 2009-12-08.
2. [↑](./Data_corruption#cite_ref-2) ["Silent Data Corruption"](https://support.google.com/cloud/answer/10759085?hl=en#:~:text=Silent%20Data%20Corruption%20(SDC)%2C,to%20data%20loss%20and%20corruption.). Google Inc. 2023. Retrieved January 30, 2023. Silent Data Corruption (SDC), sometimes referred to as Silent Data Error (SDE), is an industry-wide issue impacting not only long-protected memory, storage, and networking, but also computer CPUs.
3. [↑](./Data_corruption#cite_ref-3) Eric Lowe (16 November 2005). ["ZFS saves the day(-ta)!"](https://web.archive.org/web/20120205040345/http://blogs.oracle.com/elowe/entry/zfs_saves_the_day_ta). *Oracle – Core Dumps of a Kernel Hacker's Brain – Eric Lowe's Blog*. Oracle. Archived from [the original](http://blogs.oracle.com/elowe/entry/zfs_saves_the_day_ta) (Blog) on 5 February 2012. Retrieved 9 June 2012.
4. [↑](./Data_corruption#cite_ref-4) bcantrill (31 December 2008). ["Shouting in the Datacenter"](https://www.youtube.com/watch?v=tDacjrSCeq4) (Video file). *YouTube*. [Archived](https://web.archive.org/web/20120703132341/http://www.youtube.com/watch?v=tDacjrSCeq4) from the original on 3 July 2012. Retrieved 9 June 2012.
5. [↑](./Data_corruption#cite_ref-5) jforonda (31 January 2007). ["Faulty FC port meets ZFS"](http://jforonda.blogspot.com/2007/01/faulty-fc-port-meets-zfs.html) (Blog). *Blogger – Outside the Box*. [Archived](https://web.archive.org/web/20120426055112/http://jforonda.blogspot.com/2007/01/faulty-fc-port-meets-zfs.html) from the original on 26 April 2012. Retrieved 9 June 2012.
6. [↑](./Data_corruption#cite_ref-6) ["Are Disks the Dominant Contributor for Storage Failures? A Comprehensive Study of Storage Subsystem Failure Characteristics"](http://www.usenix.org/event/fast08/tech/full_papers/jiang/jiang.pdf) (PDF). USENIX. [Archived](https://web.archive.org/web/20220125061938/https://www.usenix.org/legacy/event/fast08/tech/full_papers/jiang/jiang.pdf) (PDF) from the original on 2022-01-25. Retrieved 2014-01-18.
7. [1](./Data_corruption#cite_ref-CERN2007_7-0) [2](./Data_corruption#cite_ref-CERN2007_7-1) Bernd Panzer-Steindel (8 April 2007). ["Draft 1.3"](http://indico.cern.ch/getFile.py/access?contribId=3&sessionId=0&resId=1&materialId=paper&confId=13797). *Data integrity*. CERN. [Archived](https://web.archive.org/web/20121027083405/http://indico.cern.ch/getFile.py/access?contribId=3&sessionId=0&resId=1&materialId=paper&confId=13797) from the original on 27 October 2012. Retrieved 9 June 2012.
8. [↑](./Data_corruption#cite_ref-8) ["AWS Service Availability"](https://web.archive.org/web/20081225062644/https://status.aws.amazon.com/s3-20080720.html). *status.aws.amazon.com*. Archived from [the original](https://status.aws.amazon.com/s3-20080720.html) on December 25, 2008. Retrieved 11 July 2025.
9. [↑](./Data_corruption#cite_ref-9) Hochschild, Peter H.; Turner, Paul Jack; Mogul, Jeffrey C.; Govindaraju, Rama Krishna; Ranganathan, Parthasarathy; Culler, David E.; Vahdat, Amin (2021). ["Cores that don't count"](https://sigops.org/s/conferences/hotos/2021/papers/hotos21-s01-hochschild.pdf) (PDF). *Proceedings of the Workshop on Hot Topics in Operating Systems*. pp. 9–16. [doi](./Doi_(identifier)):[10.1145/3458336.3465297](https://doi.org/10.1145%2F3458336.3465297). [ISBN](./ISBN_(identifier)) [9781450384384](./Special:BookSources/9781450384384). [S2CID](./S2CID_(identifier)) [235311320](https://api.semanticscholar.org/CorpusID:235311320). [Archived](https://web.archive.org/web/20210603055415/https://sigops.org/s/conferences/hotos/2021/papers/hotos21-s01-hochschild.pdf) (PDF) from the original on 2021-06-03. Retrieved 2021-06-02.
10. [↑](./Data_corruption#cite_ref-10) [*HotOS 2021: Cores That Don't Count (Fun Hardware)*](https://www.youtube.com/watch?v=QMF3rqhjYuM), 27 May 2021, [archived](https://ghostarchive.org/varchive/youtube/20211222/QMF3rqhjYuM) from the original on 2021-12-22, retrieved 2021-06-02
11. [↑](./Data_corruption#cite_ref-11) ["Silent data corruption in disk arrays: A solution"](https://web.archive.org/web/20131029210013/http://www.necam.com/docs/?id=54157ff5-5de8-4966-a99d-341cf2cb27d3). NEC. 2009. Archived from [the original](http://www.necam.com/docs/?id=54157ff5-5de8-4966-a99d-341cf2cb27d3) (PDF) on 29 October 2013. Retrieved 14 December 2020.
12. [↑](./Data_corruption#cite_ref-12) ["A Conversation with Jeff Bonwick and Bill Moore"](http://queue.acm.org/detail.cfm?id=1317400). Association for Computing Machinery. November 15, 2007. [Archived](https://web.archive.org/web/20110716221142/http://queue.acm.org/detail.cfm?id=1317400) from the original on 16 July 2011. Retrieved 14 December 2020.
13. [↑](./Data_corruption#cite_ref-13) [David S. H. Rosenthal](./David_S._H._Rosenthal) (October 1, 2010). ["Keeping Bits Safe: How Hard Can It Be?"](http://queue.acm.org/detail.cfm?id=1866298). *ACM Queue*. [Archived](https://web.archive.org/web/20131217020947/http://queue.acm.org/detail.cfm?id=1866298) from the original on December 17, 2013. Retrieved 2014-01-02.;  Bairavasundaram, L., Goodson, G., Schroeder, B., Arpaci-Dusseau, A. C., Arpaci-Dusseau, R. H. 2008. An analysis of data corruption in the storage stack. In Proceedings of 6th Usenix Conference on File and Storage Technologies.
14. [↑](./Data_corruption#cite_ref-14) Kelemen, P. [*Silent corruptions*](https://indico.desy.de/event/257/contributions/58082/attachments/37574/46878/kelemen-2007-HEPiX-Silent_Corruptions.pdf) (PDF). 8th Annual Workshop on Linux Clusters for Super Computing.
15. [↑](./Data_corruption#cite_ref-15) David Fiala; Frank Mueller; Christian Engelmann; Rolf Riesen; Kurt Ferreira; Ron Brightwell (November 2012). ["Detection and Correction of Silent Data Corruption for Large-Scale High-Performance Computing"](http://www.fiala.me/pubs/papers/sc12-redmpi.pdf) (PDF). *fiala.me*. [IEEE](./IEEE). [Archived](https://web.archive.org/web/20141107074511/http://www.fiala.me/pubs/papers/sc12-redmpi.pdf) (PDF) from the original on 2014-11-07. Retrieved 2015-01-26.
16. [↑](./Data_corruption#cite_ref-16) Steve Bostian (2012). ["Rachet Up Reliability for Mission-Critical Applications: Intel Instruction Replay Technology"](http://www.intel.com/content/dam/www/public/us/en/documents/white-papers/itanium-9500-reliability-mission-critical-applications-paper.pdf) (PDF). [Intel](./Intel). [Archived](https://web.archive.org/web/20160202125833/http://www.intel.com/content/dam/www/public/us/en/documents/white-papers/itanium-9500-reliability-mission-critical-applications-paper.pdf) (PDF) from the original on 2016-02-02. Retrieved 2016-01-27.
17. [↑](./Data_corruption#cite_ref-17) ["Read Error Severities and Error Management Logic"](http://pcguide.com/ref/hdd/geom/errorRead-c.html). [Archived](https://web.archive.org/web/20120407181624/http://www.pcguide.com/ref/hdd/geom/errorRead-c.html) from the original on 7 April 2012. Retrieved 4 April 2012.
18. [↑](./Data_corruption#cite_ref-18) Margaret Bierman; Lenz Grimmer (August 2012). ["How I Use the Advanced Capabilities of Btrfs"](http://www.oracle.com/technetwork/articles/servers-storage-admin/advanced-btrfs-1734952.html). [Oracle Corporation](./Oracle_Corporation). [Archived](https://web.archive.org/web/20140102193726/http://www.oracle.com/technetwork/articles/servers-storage-admin/advanced-btrfs-1734952.html) from the original on 2014-01-02. Retrieved 2014-01-02.
19. [↑](./Data_corruption#cite_ref-Zhang2010_19-0) Yupu Zhang; Abhishek Rajimwale; [Andrea Arpaci-Dusseau](./Andrea_Arpaci-Dusseau); Remzi H. Arpaci-Dusseau (2010). ["End-to-end data integrity for file systems: a ZFS case study"](https://www.usenix.org/legacy/events/fast10/tech/full_papers/zhang.pdf) (PDF). *USENIX Conference on File and Storage Technologies*. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.154.3979](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.154.3979). [S2CID](./S2CID_(identifier)) [5722163](https://api.semanticscholar.org/CorpusID:5722163). [Wikidata](./WDQ_(identifier)) [Q111972797](https://www.wikidata.org/wiki/Q111972797). Retrieved 2014-08-12.

 

## External links

 
- [SoftECC: A System for Software Memory Integrity Checking](http://pdos.csail.mit.edu/papers/softecc:ddopson-meng/softecc_ddopson-meng.pdf)
- [A Tunable, Software-based DRAM Error Detection and Correction Library for HPC](http://www.fiala.me/pubs/papers/libsdc11.pdf)
- [Detection and Correction of Silent Data Corruption for Large-Scale High-Performance Computing](http://www.fiala.me/pubs/papers/sc12-redmpi.pdf)
- [End-to-end Data Integrity for File Systems: A ZFS Case Study](https://www.usenix.org/legacy/events/fast10/tech/full_papers/zhang.pdf)
- [DRAM Errors in the Wild: A Large-Scale Field Study](http://www.cs.toronto.edu/~bianca/papers/sigmetrics09.pdf)
- [A study on silent corruptions](https://www.nsc.liu.se/lcsc2007/presentations/LCSC_2007-kelemen.pdf), and an associated paper on [data integrity](https://web.archive.org/web/20141220141819/http://indico.cern.ch/event/13797/session/0/material/paper/1?contribId=3) (CERN, 2007)
- [End-to-end Data Protection in SAS and Fibre Channel Hard Disk Drives](http://www.hgst.com/tech/techlib.nsf/techdocs/328DB53FC65C4DF18625742C00562B92/$file/End-to-end_Data_Protection.pdf) (HGST)

 
| vteData |
| --- |
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