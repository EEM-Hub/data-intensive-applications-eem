---
source: https://en.wikipedia.org/wiki/Data_degradation
fetched: 2026-06-19
---

Accumulation of data corruption on a storage device over time 

 Not to be confused with [Software rot](./Software_rot). 
|  | This articlemay containoriginal research.Pleaseimprove itbyverifyingthe claims made and addinginline citations. Statements consisting only of original research should be removed.(April 2015)(Learn how and when to remove this message) |
| --- | --- |

 

**Data degradation** is the gradual [corruption](./Data_corruption) of [computer data](./Data_(computing)) due to an accumulation of non-critical failures in a [data storage device](./Data_storage_device). It is also referred to as **data decay**, **data rot**, **digital decay**, or **bit rot**.[[1]](./Data_degradation#cite_note-Rouse_2020-1) This results in a decline in data quality over time, even when the data is not being utilized. 

 

## Manifestations

 

### Primary storages

 

Data degradation in [dynamic random-access memory](./Dynamic_random-access_memory) (DRAM) can occur when the [electric charge](./Electric_charge) of a [bit](./Bit) in DRAM disperses, possibly altering program code or stored data. DRAM may be altered by [cosmic rays](./Cosmic_ray)[[2]](./Data_degradation#cite_note-2) or other high-energy particles. Such data degradation is known as a [soft error](./Soft_error).[[3]](./Data_degradation#cite_note-O'Gorman_1996-3) [ECC memory](./ECC_memory) can be used to mitigate this type of data degradation.[[4]](./Data_degradation#cite_note-Normand_1996-4)

 

### Secondary storages

 

Data degradation results from the gradual decay of [storage media](./Storage_media) over the course of years or longer. Causes vary by medium.

 

#### Solid-state media

 

[EPROMs](./EPROM), [flash memory](./Flash_memory) and other [solid-state drive](./Solid-state_drive) store data using electrical charges, which can slowly leak away due to imperfect [insulation](./Insulator_(electricity)). Modern flash controller chips account for this leak by trying several lower threshold voltages (until [ECC](./Error_correction_code) passes), prolonging the age of data. [Multi-level cells](./Multi-level_cell) with much lower distance between voltage levels cannot be considered stable without this functionality.[[5]](./Data_degradation#cite_note-Li_2022-5)

 

The chip itself is not affected by this, so reprogramming it approximately once per decade prevents decay. An undamaged copy of the master data is required for the reprogramming. A [checksum](./Checksum) can be used to assure that the on-chip data is not yet damaged and ready for reprogramming.

 

The typical SD card, USB stick and M.2 NVMe all have a limited endurance. Power on can usually recover data[*[citation needed](./Wikipedia:Citation_needed)*] but error rates will eventually degrade the media to illegibility. Writing zeros to a degraded NAND device can revive the storage to close to new condition for further use.[*[citation needed](./Wikipedia:Citation_needed)*] Refresh cycles should be no longer than 6 months to  be sure the device is legible.

 

#### Magnetic media

 

[Magnetic media](./Magnetic_storage), such as [hard disk drives](./Hard_disk_drive), [floppy disks](./Floppy_disk) and [magnetic tapes](./Magnetic_tape), may experience data decay as bits lose their magnetic orientation. Higher temperature speeds up the rate of magnetic loss. As with solid-state media, re-writing is useful as long as the medium itself is not damaged (see below).[[6]](./Data_degradation#cite_note-NAA-6) Modern hard drives use [Giant magnetoresistance](./Giant_magnetoresistance) and have a higher magnetic lifespan on the order of decades. They also automatically correct any errors detected by ECC through rewriting. The reliance on a [servowriter](./Servowriter) can complicate data recovery if it becomes unrecoverable, however.

 

Floppy disks and tapes are poorly protected against ambient air. In warm/humid conditions, they are prone to the physical [decomposition](./Decomposition) of the storage medium.[[7]](./Data_degradation#cite_note-Riss_1993-7)[[6]](./Data_degradation#cite_note-NAA-6)

 

#### Optical media

 

[Optical media](./Optical_storage) such as [CD-R](./CD-R), [DVD-R](./DVD-R) and [BD-R](./BD-R), may experience data decay from the [breakdown](./Disc_rot) of the storage medium. This can be mitigated by storing discs in a dark, cool, low humidity location. "Archival quality" discs are available with an extended lifetime, but are still not permanent. However, [data integrity scanning](./Optical_disc#Surface_error_scanning) that measures the rates of various types of errors is able to predict data decay on optical media well ahead of uncorrectable data loss occurring.[[8]](./Data_degradation#cite_note-qpx-g-8)

 

Both the disc dye and the disc backing layer are potentially susceptible to breakdown. Early cyanine-based dyes used in CD-R were notorious for their lack of UV stability. Early CDs also suffered from [CD bronzing](./CD_bronzing), and is related to a combination of bad lacquer material and failure of the aluminum reflection layer.[[9]](./Data_degradation#cite_note-IASA_1997-9) Later discs use more stable dyes or forgo them for an inorganic mixture. The aluminum layer is also commonly swapped out for gold or silver alloy.

 

#### Paper media

 

[Paper media](./Paper_data_storage), such as [punched cards](./Punched_cards) and [punched tape](./Punched_tape), may literally [rot](./Decomposition). [Mylar](./Mylar) punched tape is another approach that does not rely on electromagnetic stability. Degradation of [books](./Books) and [printing paper](./Printing_and_writing_paper) is primarily driven by [acid hydrolysis](./Acid_hydrolysis) of [glycosidic bonds](./Glycosidic_bonds) within the [cellulose](./Cellulose) molecule as well as by [oxidation](./Oxidation);[[10]](./Data_degradation#cite_note-Malachowska_2021-10) degradation of paper is accelerated by high [relative humidity](./Relative_humidity), high temperature, as well as by exposure to acids, oxygen, light, and various pollutants, including various [volatile organic compounds](./Volatile_organic_compounds) and [nitrogen dioxide](./Nitrogen_dioxide).[[11]](./Data_degradation#cite_note-Menart_2011-11)

 

#### Streaming media

 

Data degradation occurs in [streaming media](./Streaming_media) transmission, causing data quality issues.[[12]](./Data_degradation#cite_note-Yu_2022-12)

 

### Example

 

One manifestation of data degradation is when one or a few bits are randomly flipped over a long period.[[13]](./Data_degradation#cite_note-FOOTNOTERosenthal201050-13) This is illustrated by several digital images below, all consisting of 326,272 bits. The original photo is displayed first. In the next image, a single bit was changed from 0 to 1. In the next two images, two and three bits were flipped. On [Linux](./Linux) systems, the binary difference between files can be revealed using the `cmp` command (e.g. `cmp -b bitrot-original.jpg bitrot-1bit-changed.jpg`).

 
- [![0 bits flipped](//upload.wikimedia.org/wikipedia/commons/thumb/2/2f/Bitrot_in_JPEG_files%2C_0_bits_flipped.jpg/120px-Bitrot_in_JPEG_files%2C_0_bits_flipped.jpg)](./File:Bitrot_in_JPEG_files,_0_bits_flipped.jpg)0 bits flipped
- [![1 bit flipped](//upload.wikimedia.org/wikipedia/commons/thumb/1/1a/Bitrot_in_JPEG_files%2C_1_bit_flipped.jpg/120px-Bitrot_in_JPEG_files%2C_1_bit_flipped.jpg)](./File:Bitrot_in_JPEG_files,_1_bit_flipped.jpg)1 bit flipped
- [![2 bits flipped](//upload.wikimedia.org/wikipedia/commons/thumb/3/37/Bitrot_in_JPEG_files%2C_2_bits_flipped.jpg/120px-Bitrot_in_JPEG_files%2C_2_bits_flipped.jpg)](./File:Bitrot_in_JPEG_files,_2_bits_flipped.jpg)2 bits flipped
- [![3 bits flipped](//upload.wikimedia.org/wikipedia/commons/thumb/d/dd/Bitrot_in_JPEG_files%2C_3_bits_flipped.jpg/120px-Bitrot_in_JPEG_files%2C_3_bits_flipped.jpg)](./File:Bitrot_in_JPEG_files,_3_bits_flipped.jpg)3 bits flipped

 

The JPEG format does not store a bitwise image, but the parameters for decoding. Therefore, changing just one bit leads to noticeable changes. The coefficient of the encoding function changed, for example, several times if the bit was in one of the higher digits.[*[citation needed](./Wikipedia:Citation_needed)*]

 

## Causes

 

This deterioration can be caused by a variety of factors that impact the reliability and integrity of digital information, including physical factors, [software errors](./Software_error), security breaches, [human error](./Human_error), obsolete technology, and unauthorized access incidents.[[14]](./Data_degradation#cite_note-ShengLance_2015-14)[[15]](./Data_degradation#cite_note-PCMag-15)[[16]](./Data_degradation#cite_note-Hakob_2023-16)[[17]](./Data_degradation#cite_note-Triches_2006-17)

 

Most disk, [disk controller](./Disk_controller) and higher-level systems are subject to a slight chance of unrecoverable failure. With ever-growing disk capacities, file sizes, and increases in the amount of data stored on a disk, the likelihood of the occurrence of data decay and other forms of uncorrected and undetected [data corruption](./Data_corruption) increases.[[18]](./Data_degradation#cite_note-18)

 

Low-level disk controllers typically employ [error correction codes](./Error_correction_code) (ECC) to correct erroneous data.[[19]](./Data_degradation#cite_note-19)

 

Higher-level software systems may be employed to mitigate the risk of such underlying failures by increasing redundancy and implementing integrity checking, error correction codes and self-repairing algorithms.[[20]](./Data_degradation#cite_note-Salter_2014-20) The [ZFS](./ZFS) [file system](./File_system) was designed to address many of these data corruption issues.[[21]](./Data_degradation#cite_note-Bonwick_2009-21) The [Btrfs](./Btrfs) file system also includes data protection and recovery mechanisms,[[22]](./Data_degradation#cite_note-22)[*[better source needed](./Wikipedia:Verifiability#Questionable_sources)*] as does [ReFS](./ReFS).[[23]](./Data_degradation#cite_note-Wlodarz_2014-23)

 

## Mitigation

 

There is no solution that completely eliminates the threat of data degradation,[[24]](./Data_degradation#cite_note-FOOTNOTERosenthal201047-24) but various measures exist that can stave it off. One of these is to [replicate the data](./Replication_(computing)) as [backups](./Backup). Both the original and backed data are then [audited](./Data_auditing) for any faults due to storage media errors by [checksumming](./Checksum) the data or comparing it with that of other copies. This is the only way to detect *latent* faults proactively,[[25]](./Data_degradation#cite_note-FOOTNOTEBaker_et_al.2006229-25) which might otherwise go unnoticed until the data is actually accessed.[[26]](./Data_degradation#cite_note-Baker_2006-p224-26) Current storage systems such as those based on [RAID](./RAID) already employ such measures internally.[[27]](./Data_degradation#cite_note-FOOTNOTERosenthal201051-27) Ideally, and especially for data that must be [preserved digitally](./Digital_preservation), the replicas should be distributed across multiple administrative sites that function autonomously and deploy various hardware and software, increasing resistance to failure, as well as human error and cyberattacks.[[28]](./Data_degradation#cite_note-FOOTNOTEBakerKeetonMartin20055-28)

 

## See also

  
- [Cliff effect](./Cliff_effect)
- [Database integrity](./Database_integrity)
- [Data curation](./Data_curation)
- [Data preservation](./Data_preservation)
- [Data scrubbing](./Data_scrubbing)
- [Digital permanence](./Digital_permanence)
- [Disc rot](./Disc_rot)
- [Error detection and correction](./Error_detection_and_correction)
- [Link rot](./Link_rot)
- [Media preservation](./Media_preservation)
- [RAR](./RAR_(file_format)) archive file format has optional recovery
- [PAR2](./Parchive) recovery file format

  

## References

  
1. [↑](./Data_degradation#cite_ref-Rouse_2020_1-0) Rouse, Margaret (25 March 2020). ["What is Bit Rot?"](https://www.techopedia.com/definition/33108/bit-rot). *Techopedia Dictionary*. Retrieved 10 April 2024.
2. [↑](./Data_degradation#cite_ref-2) ["The Invisible Neutron Threat | National Security Science Magazine"](https://www.lanl.gov/science/NSS/issue1_2012/story4full.shtml). *Los Alamos National Laboratory*. Retrieved 13 March 2020.
3. [↑](./Data_degradation#cite_ref-O'Gorman_1996_3-0) O'Gorman, T. J.; Ross, J. M.; Taber, A. H.; Ziegler, J. F.; Muhlfeld, H. P.; Montrose, C. J.; Curtis, H. W.; Walsh, J. L. (January 1996). "Field testing for cosmic ray soft errors in semiconductor memories". *IBM Journal of Research and Development*. **40** (1): 41–50. [doi](./Doi_(identifier)):[10.1147/rd.401.0041](https://doi.org/10.1147%2Frd.401.0041).
4. [↑](./Data_degradation#cite_ref-Normand_1996_4-0) Normand, Eugene (December 1996). ["Single Event Upset at Ground Level"](https://web.archive.org/web/20131021190327/http://pdf.yuri.se/files/art/2.pdf) (PDF). *[IEEE Transactions on Nuclear Science](./IEEE_Transactions_on_Nuclear_Science)*. **43** (6): 2742–2750. [Bibcode](./Bibcode_(identifier)):[1996ITNS...43.2742N](https://ui.adsabs.harvard.edu/abs/1996ITNS...43.2742N). [doi](./Doi_(identifier)):[10.1109/23.556861](https://doi.org/10.1109%2F23.556861). Archived from [the original](http://pdf.yuri.se/files/art/2.pdf) (PDF) on 21 October 2013.
5. [↑](./Data_degradation#cite_ref-Li_2022_5-0) Li, Qianhui; Wang, Qi; Yang, Liu; Yu, Xiaolei; Jiang, Yiyang; He, Jing; Huo, Zongliang (April 2022). "Optimal read voltages decision scheme eliminating read retry operations for 3D NAND flash memories". *Microelectronics Reliability*. **131** 114509. [Bibcode](./Bibcode_(identifier)):[2022MiRe..13114509L](https://ui.adsabs.harvard.edu/abs/2022MiRe..13114509L). [doi](./Doi_(identifier)):[10.1016/j.microrel.2022.114509](https://doi.org/10.1016%2Fj.microrel.2022.114509).[*[page needed](./Wikipedia:Citing_sources)*]
6. [1](./Data_degradation#cite_ref-NAA_6-0) [2](./Data_degradation#cite_ref-NAA_6-1) ["Preserving magnetic media"](https://www.naa.gov.au/information-management/storing-and-preserving-information/preserving-information/preserving-magnetic-media). *National Archives of Australia*. Retrieved 3 November 2020. High temperature and humidity and fluctuations may cause the magnetic and base layers in a reel of tape to separate, or cause adjacent loops to block together. High temperatures may also weaken the magnetic signal, and ultimately de-magnetise the magnetic layer.
7. [↑](./Data_degradation#cite_ref-Riss_1993_7-0) Riss, Dan (July 1993). ["Conserve O Gram (number 19/8) Preservation Of Magnetic Media"](https://www.nps.gov/museum/publications/conserveogram/19-08.pdf) (PDF). *nps.gov*. Harpers Ferry, West Virginia: National Park Service / Department of the Interior (US). p. 2. The longevity of magnetic media is most seriously affected by processes that attack the binder resin. Moisture from the air is absorbed by the binder and reacts with the resin. The result is a gummy residue that can deposit on tape heads and cause tape layers to stick together. Reaction with moisture also can result in breaks in the long molecular chains of the binder. This weakens the physical properties of the binder and can result in a lack of adhesion to the backing. These reactions are greatly accelerated by the presence of acids. Typical sources would be the usual pollutant gases in the air, such as sulphur dioxide (SO2) and nitrous oxides (NOx), which react with moist air to form acids. Though acid inhibitors are usually built into the binder layer, over time they can lose their effectiveness.
8. [↑](./Data_degradation#cite_ref-qpx-g_8-0) ["QPxTool glossary"](https://qpxtool.sourceforge.io/glossar.html). *qpxtool.sourceforge.io*. QPxTool. 1 August 2008. Retrieved 22 July 2020.[*[better source needed](./Wikipedia:Verifiability#Questionable_sources)*]
9. [↑](./Data_degradation#cite_ref-IASA_1997_9-0) ["Bronzed CD alert!"](https://web.archive.org/web/20110722224026/http://www.iasa-web.org/content/information-bulletin-no-22-july-1997). *IASA Information Bulletin no. 22*. July 1997. Archived from [the original](http://www.iasa-web.org/content/information-bulletin-no-22-july-1997) on 22 July 2011. Retrieved 3 August 2007.
10. [↑](./Data_degradation#cite_ref-Malachowska_2021_10-0) Małachowska, Edyta; Pawcenis, Dominika; Dańczak, Jacek; Paczkowska, Joanna; Przybysz, Kamila (26 March 2021). ["Paper Ageing: The Effect of Paper Chemical Composition on Hydrolysis and Oxidation"](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8036582). *[Polymers](./Polymers_(journal))*. **13** (7): 1029. [doi](./Doi_(identifier)):[10.3390/polym13071029](https://doi.org/10.3390%2Fpolym13071029). [PMC](./PMC_(identifier)) [8036582](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8036582). [PMID](./PMID_(identifier)) [33810293](https://pubmed.ncbi.nlm.nih.gov/33810293).
11. [↑](./Data_degradation#cite_ref-Menart_2011_11-0) Menart, Eva; De Bruin, Gerrit; Strlič, Matija (9 September 2011). ["Dose–response functions for historic paper"](https://discovery.ucl.ac.uk/1335848/1/Menart_PDSt_2011_EPS.pdf) (PDF). *Polymer Degradation and Stability*. **96** (12): 2029–2039. [doi](./Doi_(identifier)):[10.1016/j.polymdegradstab.2011.09.002](https://doi.org/10.1016%2Fj.polymdegradstab.2011.09.002). Retrieved 5 June 2023.
12. [↑](./Data_degradation#cite_ref-Yu_2022_12-0) Yu, Wenwu; Jiang, Jingjing; Zhai, Yue; Xu, Peng (20 May 2022). Rajakani, Kalidoss (ed.). ["Perceived Integrity of Distributed Streaming Media Based on AWTC-TT Algorithm Optimization"](https://doi.org/10.1155%2F2022%2F7522174). *[Wireless Communications and Mobile Computing](./Wireless_Communications_and_Mobile_Computing)*: 1–17. [doi](./Doi_(identifier)):[10.1155/2022/7522174](https://doi.org/10.1155%2F2022%2F7522174). [ISSN](./ISSN_(identifier)) [1530-8677](https://search.worldcat.org/issn/1530-8677).
13. [↑](./Data_degradation#cite_ref-FOOTNOTERosenthal201050_13-0) [Rosenthal 2010](./Data_degradation#CITEREFRosenthal2010), p. 50.
14. [↑](./Data_degradation#cite_ref-ShengLance_2015_14-0) Sheng Lance, Li (22 July 2015). ["What is data decay?"](https://www.techinasia.com/talk/data-decay-affect-business). *[Tech in Asia](./Tech_in_Asia)*. Retrieved 10 April 2024.
15. [↑](./Data_degradation#cite_ref-PCMag_15-0) ["Definition of data degradation"](https://www.pcmag.com/encyclopedia/term/data-fade). *[PC Magazine](./PC_Magazine)*. Retrieved 10 April 2024.
16. [↑](./Data_degradation#cite_ref-Hakob_2023_16-0) Hakob, Mike (27 December 2023). ["Data Decay: What are the Causes?"](https://formstory.io/learn/data-decay/). *FormStory*. Retrieved 10 April 2024.[*[better source needed](./Wikipedia:Verifiability#Questionable_sources)*]
17. [↑](./Data_degradation#cite_ref-Triches_2006_17-0) Triches, Robert (16 March 2006). ["Forskare: Billiga cd-skivor håller bara i två år"](https://www.aftonbladet.se/nyheter/a/ddR9kw/forskare-billiga-cd-skivor-haller-bara-i-tva-ar). *[Aftonbladet](./Aftonbladet)*. Retrieved 10 April 2024.
18. [↑](./Data_degradation#cite_ref-18) Gray, Jim; van Ingen, Catharine (December 2005). ["Empirical Measurements of Disk Failure Rates and Error Rates"](http://research.microsoft.com/pubs/64599/tr-2005-166.pdf) (PDF). *Microsoft Research Technical Report MSR-TR-2005-166*. Retrieved 4 March 2013.
19. [↑](./Data_degradation#cite_ref-19) ["ECC and Spare Blocks help to keep Kingston SSD data protected from errors"](https://www.kingston.com/en/ssd/data-protection). *Kingston Technology Company*. Retrieved 30 March 2021.
20. [↑](./Data_degradation#cite_ref-Salter_2014_20-0) Salter, Jim (15 January 2014). ["Bitrot and atomic COWs: Inside "next-gen" filesystems"](https://web.archive.org/web/20150306225935/http://arstechnica.com/information-technology/2014/01/bitrot-and-atomic-cows-inside-next-gen-filesystems/). [Ars Technica](./Ars_Technica). Archived from [the original](https://arstechnica.com/information-technology/2014/01/bitrot-and-atomic-cows-inside-next-gen-filesystems/) on 6 March 2015. Retrieved 15 January 2014.
21. [↑](./Data_degradation#cite_ref-Bonwick_2009_21-0) Bonwick, Jeff (2009). ["ZFS: The Last Word in File Systems"](https://web.archive.org/web/20130921055345/http://www.snia.org/sites/default/files2/sdc_archives/2009_presentations/monday/JeffBonwickzfs-Basic_and_Advanced.pdf) (PDF). Storage Networking Industry Association (SNIA). Archived from [the original](http://www.snia.org/sites/default/files2/sdc_archives/2009_presentations/monday/JeffBonwickzfs-Basic_and_Advanced.pdf) (PDF) on 21 September 2013. Retrieved 4 March 2013.
22. [↑](./Data_degradation#cite_ref-22) ["btrfs Wiki: Features"](https://btrfs.wiki.kernel.org/index.php/Main_Page#Features). The btrfs Project. Retrieved 19 September 2013.
23. [↑](./Data_degradation#cite_ref-Wlodarz_2014_23-0) Wlodarz, Derrick (15 January 2014). ["Windows Storage Spaces and ReFS: is it time to ditch RAID for good?"](http://betanews.com/2014/01/15/windows-storage-spaces-and-refs-is-it-time-to-ditch-raid-for-good/). Betanews. Retrieved 9 February 2014.
24. [↑](./Data_degradation#cite_ref-FOOTNOTERosenthal201047_24-0) [Rosenthal 2010](./Data_degradation#CITEREFRosenthal2010), p. 47.
25. [↑](./Data_degradation#cite_ref-FOOTNOTEBaker_et_al.2006229_25-0) [Baker et al. 2006](./Data_degradation#CITEREFBaker_et_al.2006), p. 229.
26. [↑](./Data_degradation#cite_ref-Baker_2006-p224_26-0) [Baker et al. 2006](./Data_degradation#CITEREFBaker_et_al.2006), p. 224: "While many faults are detected at the time an error causes them, some occur silently. These are called 'latent faults.' There are many sources of latent faults, but media errors are the best known. While a [head crash](./Head_crash) would be detectable, bit rot might not be uncovered until the affected faulty data are actually accessed and audited. As another example, a sector on a disk might become unreadable; this would not be detected until the next read of that sector. Further, a sector might be readable but contain incorrect information due to a previous misplaced sector write."
27. [↑](./Data_degradation#cite_ref-FOOTNOTERosenthal201051_27-0) [Rosenthal 2010](./Data_degradation#CITEREFRosenthal2010), p. 51.
28. [↑](./Data_degradation#cite_ref-FOOTNOTEBakerKeetonMartin20055_28-0) [Baker, Keeton & Martin 2005](./Data_degradation#CITEREFBakerKeetonMartin2005), p. 5.

 

## Sources

 
- Baker, Mary; [Keeton, Kimberly](./Kimberly_Keeton); Martin, Sean (30 June 2005). [*Why Traditional Storage Systems Don't Help Us Save Stuff Forever*](https://web.archive.org/web/20060907054345/http://www.hpl.hp.com/techreports/2005/HPL-2005-120.pdf) (PDF). HotDep'05: Proceedings of the First conference on Hot topics in system dependability. [USENIX](./USENIX). Archived from [the original](http://www.hpl.hp.com/techreports/2005/HPL-2005-120.pdf) (PDF) on 7 September 2006. Retrieved 15 February 2025.
- Baker, Mary; Shah, Mehul; [Rosenthal, David S. H.](./David_S._H._Rosenthal); Roussopoulos, Mema; Maniatis, Petros; Giuli, TJ; Bungale, Prashanth (18 April 2006). *A fresh look at the reliability of long-term digital storage*. EuroSys '06: Proceedings of the 1st ACM SIGOPS/EuroSys European Conference on Computer Systems 2006. [Association for Computing Machinery](./Association_for_Computing_Machinery). pp. 221–234. [doi](./Doi_(identifier)):[10.1145/1217935.1217957](https://doi.org/10.1145%2F1217935.1217957).
- [Rosenthal, David S. H.](./David_S._H._Rosenthal) (November 2010). ["Keeping Bits safe: how hard can it Be?"](https://doi.org/10.1145%2F1839676.1839692). *[Communications of the ACM](./Communications_of_the_ACM)*. **53** (11): 47–55. [doi](./Doi_(identifier)):[10.1145/1839676.1839692](https://doi.org/10.1145%2F1839676.1839692).

 
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