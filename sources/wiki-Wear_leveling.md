---
source: https://en.wikipedia.org/wiki/Wear_leveling
fetched: 2026-06-19
---

Operating principle for certain storage media [![A fragment of a road surface, heavily rutted by car wheels following the same path.](//upload.wikimedia.org/wikipedia/commons/thumb/7/76/DK1_koleiny.jpg/250px-DK1_koleiny.jpg)](./File:DK1_koleiny.jpg)Deep ruts from car wheels following the same path. Repetitive use of memory cells leads to a similar effect. Wear leveling attempts to distribute "traffic" more evenly. 

**Wear leveling** (also written as **wear levelling**) is a technique[[1]](./Wear_leveling#cite_note-Fundamental_Patent-1) for prolonging the [service life](./Service_life) of some kinds of erasable [computer storage](./Computer_storage) media, such as [flash memory](./Flash_memory), which is used in [solid-state drives](./Solid-state_drive) (SSDs) and [USB flash drives](./USB_flash_drive), and [phase-change memory](./Phase-change_memory).

 [![A view on stairs, where the central part deteriorated from people using mostly the middle section of each step.](//upload.wikimedia.org/wikipedia/commons/thumb/d/d5/Battery_Stairs_%28geograph_2739813%29.jpg/250px-Battery_Stairs_%28geograph_2739813%29.jpg)](./File:Battery_Stairs_(geograph_2739813).jpg)Uneven wear on the central section of stairs, from pedestrians following a single path. Another everyday-life example of a similar issue. 

The idea underpinning wear leveling is similar to [changing position of car tires](./Tire#Maintenance), avoiding repetitive load from being used on the same wheel. Wear leveling algorithms distribute writes more evenly across the entire device, so no block is used more often than others.

 

The term *preemptive wear leveling* (PWL) has been used by [Western Digital](./Western_Digital) to describe their preservation technique used on [hard disk drives](./Hard_disk_drive) (HDDs) designed for storing audio and video data.[[2]](./Wear_leveling#cite_note-2) However, HDDs generally are not wear-leveled devices in the context of this article.

 

## Rationale

 

[EEPROM](./EEPROM) and flash memory media have individually erasable segments, each of which can be put through a [limited number of erase cycles](./Flash_memory#Memory_wear) before becoming unreliable. This is usually around 3,000/5,000 cycles[[3]](./Wear_leveling#cite_note-3)[[4]](./Wear_leveling#cite_note-4) but many flash devices have one block with a specially extended life of 100,000+ cycles that can be used by the [flash memory controller](./Flash_memory_controller) to track wear and movement of data across segments.[*[citation needed](./Wikipedia:Citation_needed)*] Erasable [optical media](./Optical_disc) such as [CD-RW](./CD-RW) and [DVD-RW](./DVD-RW) are rated at up to 1,000 cycles (100,000 cycles for [DVD-RAM](./DVD-RAM) media).

 

Wear leveling attempts to work around these limitations by arranging data so that erasures and re-writes are distributed evenly across the medium. In this way, no single erase block prematurely fails due to a high concentration of write cycles.[[5]](./Wear_leveling#cite_note-5) In flash memory, a single block on the chip is designed for longer life than the others so that the memory controller can store operational data with less chance of its corruption.[[6]](./Wear_leveling#cite_note-Corsair-6)[[7]](./Wear_leveling#cite_note-7)

 

Conventional [file systems](./File_system) such as [FAT](./File_Allocation_Table), [UFS](./Unix_File_System), [HFS](./Hierarchical_File_System_(Apple))/[HFS+](./HFS_Plus), [EXT](./Extended_file_system), and [NTFS](./NTFS) were originally designed for magnetic disks and as such rewrite many of their data structures (such as their directories) repeatedly to the same area. When these systems are used on flash memory media, this becomes a problem. The problem is aggravated by the fact that some file systems track last-access times, which can lead to file [metadata](./Metadata) being constantly rewritten in-place.[[8]](./Wear_leveling#cite_note-8)

 

## Types

 

There are several wear leveling mechanisms that provide varying levels of longevity enhancement in such memory systems.[[9]](./Wear_leveling#cite_note-Spansion-9)[[6]](./Wear_leveling#cite_note-Corsair-6)

 

### No wear leveling

 

A flash memory storage system with *no wear leveling* will not last very long if data is written to the flash. Without wear leveling, the underlying flash controller must permanently assign the logical addresses from the [operating system](./Operating_system) (OS) to the physical addresses of the flash memory. This means that every write to a previously written block must first be read, erased, modified, and re-written to the same location. This approach is very time-consuming and frequently written locations will wear out quickly, while other locations will not be used at all. Once a few blocks reach their end of life, such a device becomes inoperable.[[9]](./Wear_leveling#cite_note-Spansion-9)

 

### Dynamic wear leveling

 

The first type of wear leveling is called *dynamic wear leveling* and it uses a map to link [logical block addresses](./Logical_block_address) (LBAs) from the OS to the physical flash memory. Each time the OS writes replacement data, the map is updated so the original physical block is marked as *invalid* data, and a new block is linked to that map entry. Each time a block of data is re-written to the flash memory, it is written to a new location. However, flash memory blocks that never get replacement data would sustain no additional wear, thus the name comes only from the dynamic data being recycled. Such a device may last longer than one with no wear leveling, but there are blocks still remaining as active even though the device is no longer operable.[[9]](./Wear_leveling#cite_note-Spansion-9)[[6]](./Wear_leveling#cite_note-Corsair-6)

 

### Static wear leveling

 

The other type of wear leveling is called *static wear leveling* which also uses a map to link the LBA to physical memory addresses. Static wear leveling works the same as dynamic wear leveling except the static blocks that do not change are periodically moved so that these low usage cells are able to be used by other data. This rotational effect enables an SSD to continue to operate until most of the blocks are near their end of life.[[9]](./Wear_leveling#cite_note-Spansion-9)[[6]](./Wear_leveling#cite_note-Corsair-6)

 

### Global wear leveling

 

Both dynamic and static wear leveling are implemented at the local level. This simply means that in a multi-chip product, every chip is managed as a single resource. The number of defective blocks in different chips within a NAND flash memory varies: a given chip could have all its data blocks worn out while another chip in the same device could have all its blocks still active. Global wear leveling addresses this problem by managing all blocks from all chips in the flash memory together―in a single pool. It ensures that all the cells in all the chips within the product are worn out evenly.[[10]](./Wear_leveling#cite_note-10)[[11]](./Wear_leveling#cite_note-11)

 

### Comparison

 

The following table compares static and dynamic wear leveling:[[6]](./Wear_leveling#cite_note-Corsair-6)

 
| Item | Static | Dynamic |
| --- | --- | --- |
| Endurance | Longer life expectancy | Shorter life expectancy |
| Performance | Slower | Faster |
| Design complexity | More complex | Less complex |
| Typical use | SSDs,[9]industrial-grade flash drives[12] | Consumer-grade flash drives |

 

## Techniques

 

There are several techniques for extending the media life:

 
- A checksum or [error-correcting](./Error_detection_and_correction) code can be kept for each block or sector in order to detect errors or correct errors.
- A pool of [overprovisioned](./Overprovisioning) reserve space can also be kept. When a block or sector does fail, future reads and writes to it can be redirected to a replacement in that pool.
- Blocks or sectors on the media can be tracked in a [least frequently used](./Least_frequently_used) (LFU) queue. The data structures for the queue itself must either be stored off-device or in such a way that the space it uses is itself wear-leveled or, in the case of flash memory, in a block with a specially extended life. However, usual [cache algorithms](./Cache_algorithms) are designed to manage the data flow into and out of [RAM](./Random-access_memory)-based caches, making them not directly suitable for [flash-based](./Flash_memory) storage devices as they have an asymmetrical nature –  reads are usually much faster than writes, and erase operations can be performed only one "block" at a time.[[13]](./Wear_leveling#cite_note-13)
- [Garbage collection](./Garbage_collection_(SSD))

 

On [Secure Digital cards](./Secure_Digital_card) and [USB flash drives](./USB_flash_drive),[[12]](./Wear_leveling#cite_note-:0-12) techniques are implemented in hardware by a built-in [microcontroller](./Microcontroller). On such devices, wear leveling is [transparent](./Transparency_(human-computer_interaction)), and conventional file system such as [FAT](./File_Allocation_Table) can be used on them as-is.

 

Wear leveling can also be implemented in software by special-purpose file systems such as [JFFS2](./JFFS2) and [YAFFS](./YAFFS) on flash media or [UDF](./Universal_Disk_Format) on optical media. All three are [log-structured file systems](./Log-structured_file_system) in that they treat their media as circular logs and write to them in sequential passes. File systems which implement [copy-on-write](./Copy-on-write) strategies, such as [ZFS](./ZFS), also implement a form of wear leveling.

 

## See also

 
- [Flash file system](./Flash_file_system)
- [Battery balancing](./Battery_balancing)

 

## References

 
1. [↑](./Wear_leveling#cite_ref-Fundamental_Patent_1-0) [U.S. patent 6,850,443](https://patents.google.com/patent/US6850443) Wear leveling techniques for flash memory systems.
2. [↑](./Wear_leveling#cite_ref-2) ["Western Digital AV Hard Drive Product Information"](https://web.archive.org/web/20100102045638/http://wdc.com/en/products/products.asp?driveid=285). Western Digital. Archived from [the original](http://wdc.com/en/products/products.asp?driveid=285) on 2010-01-02. Retrieved 2010-06-01.
3. [↑](./Wear_leveling#cite_ref-3) ["So you wanna buy a SSD? Read this first"](https://hardwarecanucks.com/forum/threads/so-you-wanna-buy-a-ssd-read-this-first.39762/). *Hardware Canucks*. 10 January 2011.
4. [↑](./Wear_leveling#cite_ref-4) ["SSDs Shifting to 25nm NAND - What You Need to Know | StorageReview.com - Storage Reviews"](https://web.archive.org/web/20191205222622/https://www.storagereview.com/ssds_shifting_to_25nm_nand_what_you_need_to_know). *www.storagereview.com*. February 12, 2011. Archived from [the original](https://www.storagereview.com/ssds_shifting_to_25nm_nand_what_you_need_to_know) on December 5, 2019. Retrieved December 5, 2019.
5. [↑](./Wear_leveling#cite_ref-5) "Algorithms and data structures for flash memories", E. Gal,  and S. Toledo, ACM Computing Surveys, 2005
6. [1](./Wear_leveling#cite_ref-Corsair_6-0) [2](./Wear_leveling#cite_ref-Corsair_6-1) [3](./Wear_leveling#cite_ref-Corsair_6-2) [4](./Wear_leveling#cite_ref-Corsair_6-3) [5](./Wear_leveling#cite_ref-Corsair_6-4) ["USB Flash Wear-Leveling and Life Span"](https://web.archive.org/web/20071013150729/http://www.corsair.com/_faq/FAQ_flash_drive_wear_leveling.pdf) (PDF). [Corsair](./Corsair_Gaming). June 2007. Archived from [the original](http://www.corsair.com/_faq/FAQ_flash_drive_wear_leveling.pdf) (PDF) on 13 October 2007. Retrieved 27 July 2013.
7. [↑](./Wear_leveling#cite_ref-7) Arnd Bergmann (2011-02-18). ["Optimizing Linux with cheap flash drives"](https://lwn.net/Articles/428584/). [LWN.net](./LWN.net). Retrieved 2013-10-03.
8. [↑](./Wear_leveling#cite_ref-8) Jonathan Corbet (2007-08-08). ["Once upon atime"](https://lwn.net/Articles/244829/). [LWN.net](./LWN.net). Retrieved 2014-01-21.
9. [1](./Wear_leveling#cite_ref-Spansion_9-0) [2](./Wear_leveling#cite_ref-Spansion_9-1) [3](./Wear_leveling#cite_ref-Spansion_9-2) [4](./Wear_leveling#cite_ref-Spansion_9-3) [5](./Wear_leveling#cite_ref-Spansion_9-4) Perdue, Ken (2010-04-30). ["Wear Leveling Application Note"](https://web.archive.org/web/20110607212139/http://www.eettaiwan.com/STATIC/PDF/200808/EETOL_2008IIC_Spansion_AN_13.pdf) (PDF). [Spansion](./Spansion). Archived from [the original](http://www.eettaiwan.com/STATIC/PDF/200808/EETOL_2008IIC_Spansion_AN_13.pdf) (PDF) on 2011-06-07. Retrieved 12 August 2010.
10. [↑](./Wear_leveling#cite_ref-10) ["Wear Leveling"](https://www.transcend-info.com/Embedded/Essay-22). *Transcend*. Retrieved 20 November 2019.
11. [↑](./Wear_leveling#cite_ref-11) ["Wear Leveling – Static, Dynamic and Global"](https://www.cactus-tech.com/wp-content/uploads/2019/03/Wear-Leveling-Static-Dynamic-Global.pdf) (PDF). *Cactus*: 5. Retrieved 20 November 2019.
12. [1](./Wear_leveling#cite_ref-:0_12-0) [2](./Wear_leveling#cite_ref-:0_12-1) ["Swissbit Industrial SD Memory Cards"](http://eu.mouser.com/new/Swissbit/swissbit-industrial-SD-memory/). [Mouser Electronics](./Mouser_Electronics). Retrieved 21 April 2017.
13. [↑](./Wear_leveling#cite_ref-13) Qing Yang (2012-02-25). ["Why Standard Cache Algorithms Won't Work For SSDs"](https://web.archive.org/web/20131202230046/http://www.velobit.com/storage-performance-blog/bid/118134/Why-Standard-Cache-Algorithms-Won-t-Work-For-SSDs). velobit.com. Archived from [the original](http://www.velobit.com/storage-performance-blog/bid/118134/Why-Standard-Cache-Algorithms-Won-t-Work-For-SSDs) on 2013-12-02. Retrieved 2013-11-26.

 

## External links

 
- [Flash SSDs –  Inferior Technology or Closet Superstar?](https://web.archive.org/web/20070202230957/http://www.bitmicro.com/press_resources_flash_ssd.php), bitmicro.com, archived from the original on February 2, 2007

 
| vteSolid-state drives |
| --- |
| Key terminology | EncryptionECCFlash file systemFlash memorySLC/MLCFlash memory controllerGarbage collectionIOPSMB/sMemory wearOpen-channel SSDOver-provisioningRead disturbSecure eraseSolid-state storageTrim commandWear levelingWrite amplification |
| Flash manufacturers | MicronSamsungSK HynixBoughtIntel's NAND flash chips and NAND flash SSD businesses and renamed the SSD business as SolidigmFlash Forward (joint venture betweenSandiskandKioxia)YMTCXMC |
| Controllers | CaptiveSandiskWestern DigitalFusion-ioHGSTsTecKioxiaOCZ(bankrupt, assets sold to Toshiba, which later spun off its SSD and flash business to Kioxia)Indilinx(bought by OCZ)MicronSamsungSeagateSandForceSK HynixBoughtIntel's NAND flash chips and NAND flash SSD businesses including controllers and renamed the SSD business SolidigmFADUIndependentGreenliant SystemsGokeMaxiotekMarvellPhisonPMC-SierraSMI | Captive | SandiskWestern DigitalFusion-ioHGSTsTecKioxiaOCZ(bankrupt, assets sold to Toshiba, which later spun off its SSD and flash business to Kioxia)Indilinx(bought by OCZ)MicronSamsungSeagateSandForceSK HynixBoughtIntel's NAND flash chips and NAND flash SSD businesses including controllers and renamed the SSD business SolidigmFADU | Independent | Greenliant SystemsGokeMaxiotekMarvellPhisonPMC-SierraSMI |
| Captive | SandiskWestern DigitalFusion-ioHGSTsTecKioxiaOCZ(bankrupt, assets sold to Toshiba, which later spun off its SSD and flash business to Kioxia)Indilinx(bought by OCZ)MicronSamsungSeagateSandForceSK HynixBoughtIntel's NAND flash chips and NAND flash SSD businesses including controllers and renamed the SSD business SolidigmFADU |
| Independent | Greenliant SystemsGokeMaxiotekMarvellPhisonPMC-SierraSMI |
| SSD manufacturers | List of solid-state drive manufacturers |
| Interfaces | Advanced Host Controller Interface(AHCI)Fibre Channel(FC)NVM Express(NVMe)PCI Express(PCIe)SATA ExpressSerial ATA(SATA)Serial attached SCSI(SAS)Universal Serial Bus(USB) |
| Configurations | HDD form factorsmSATAM.2PCI Expressexpansion cardThunderboltUSB Type-CU.2U.3EDSFF |
| Related organizations | INCITSJEDEC / JC-42, JC-64.8ONFINVMHCI Work GroupUSB-IFSATA-IOSFF CommitteeSNIASSSIT10/SCSIT11/FCT13/ATA |
| Category |