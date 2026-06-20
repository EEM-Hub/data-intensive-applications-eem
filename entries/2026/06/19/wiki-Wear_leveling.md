---
source: sources/wiki-Wear_leveling.md
source_url: https://en.wikipedia.org/wiki/Wear_leveling
---

## Wear Leveling in Flash Storage

Wear leveling is a technique for prolonging the service life of erasable storage media—primarily flash memory (SSDs, USB flash drives) and phase-change memory. It works by distributing write and erase operations evenly across all memory blocks, preventing any single block from wearing out prematurely while others remain underused.

## Key Concepts

- **Write endurance limit**: EEPROM and flash memory segments can only endure a limited number of erase cycles—typically 3,000–5,000 for standard NAND flash, with some special blocks rated for 100,000+ cycles
- **Optical media endurance**: CD-RW/DVD-RW rated ~1,000 cycles; DVD-RAM rated ~100,000 cycles
- **Logical-to-physical mapping**: Wear leveling uses an indirection map linking logical block addresses (LBAs) from the OS to physical flash addresses, allowing writes to be redirected to less-worn blocks
- **The fundamental problem**: Traditional file systems (FAT, NTFS, EXT, HFS+, UFS) were designed for magnetic disks and repeatedly rewrite metadata structures (directories, access times) to the same physical locations, which accelerates flash wear
- **Last-access time tracking** (atime) in file systems causes constant in-place metadata rewrites, aggravating wear on flash
- **Overprovisioning**: A pool of reserve blocks is kept so that when a block fails, reads/writes can be redirected to a replacement
- **Error detection**: Checksums or error-correcting codes (ECC) are maintained per block/sector to detect or correct errors
- **Garbage collection**: Works alongside wear leveling to reclaim invalidated blocks

## Types of Wear Leveling

- **No wear leveling**: Logical addresses permanently mapped to physical addresses. Every rewrite requires read-erase-modify-write to the same location. Device fails quickly as hot blocks exhaust their erase cycles while cold blocks remain unused.
- **Dynamic wear leveling**: Remaps only blocks that receive new writes. When data is rewritten, it goes to a fresh block and the old block is marked invalid. Limitation: static/cold data blocks never move and never share wear burden.
- **Static wear leveling**: Extends dynamic wear leveling by periodically relocating static (cold) data blocks so their low-usage cells can be repurposed for active data. Enables the device to operate until most blocks approach end of life.
- **Global wear leveling**: Manages all blocks across all chips in a multi-chip device as a single pool, preventing one chip from wearing out while another remains fresh.

| Property | Static | Dynamic |
|---|---|---|
| Endurance | Longer life | Shorter life |
| Performance | Slower | Faster |
| Complexity | More complex | Less complex |
| Typical use | SSDs, industrial flash | Consumer flash drives |

## Commands and Syntax

No direct user-facing commands—wear leveling is implemented transparently by:
- **Hardware controllers**: Built-in microcontrollers on SD cards and USB flash drives handle wear leveling automatically; conventional file systems (FAT) work as-is
- **Flash memory controllers**: Manage the LBA-to-physical mapping, block erasure tracking, and data relocation
- **Software file systems**: JFFS2, YAFFS (log-structured file systems for raw flash), UDF (for optical media), and copy-on-write file systems like ZFS all implement wear leveling in software by writing sequentially and treating media as circular logs

## Relationships

- **Flash Memory Controller (FTL)**: The firmware layer that implements wear leveling, garbage collection, and bad block management
- **Write Amplification**: Closely related—wear leveling can increase write amplification (more physical writes per logical write), creating a tradeoff between even wear distribution and write efficiency
- **TRIM Command**: Informs the SSD which blocks are no longer in use, enabling better garbage collection and wear leveling decisions
- **Over-provisioning**: Provides the spare blocks that wear leveling algorithms need to redistribute data
- **Garbage Collection (SSD)**: Works in conjunction with wear leveling to reclaim invalidated blocks
- **Log-structured File Systems**: JFFS2, YAFFS, and F2FS are designed specifically to provide software-level wear leveling on flash
- **Copy-on-Write (COW)**: File systems like ZFS and Btrfs inherently distribute writes, providing implicit wear leveling

## Exam-Relevant Points

- **Dynamic vs. static wear leveling**: Dynamic only remaps written blocks (cold data stays in place); static periodically moves cold data to share wear across all blocks—static provides longer device life but with higher complexity and lower performance
- **Typical erase cycle limits**: 3,000–5,000 cycles for standard NAND; 100,000+ for special controller blocks; 1,000 for CD-RW/DVD-RW; 100,000 for DVD-RAM
- **Why traditional file systems harm flash**: They repeatedly overwrite metadata (directories, timestamps) in the same physical locations, concentrating wear
- **Global wear leveling solves the multi-chip problem**: Without it, individual chips in a multi-chip device can fail while others remain healthy
- **Hardware vs. software implementation**: SD cards and USB drives implement wear leveling in hardware (transparent to OS); raw flash uses software file systems (JFFS2, YAFFS) or flash-aware file systems (F2FS, ZFS)
- **Without any wear leveling**: A flash device will fail when its hottest blocks exhaust their erase cycles, even though most blocks remain perfectly usable—the device becomes inoperable prematurely
- **LFU tracking caveat**: Standard cache algorithms designed for RAM are not directly suitable for flash because of flash's asymmetric read/write/erase characteristics
