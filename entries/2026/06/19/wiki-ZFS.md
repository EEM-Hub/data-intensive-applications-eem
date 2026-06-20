---
source: sources/wiki-ZFS.md
source_url: https://en.wikipedia.org/wiki/ZFS
---

## ZFS: Copy-on-Write File System with Integrated Volume Management

ZFS is a combined file system and volume manager originally developed at Sun Microsystems (2001–2010), now maintained as OpenZFS (since 2013). Its defining architectural choice is unifying volume management and file system into a single layer, giving it end-to-end knowledge of both physical disks and logical data. This enables features impossible when these layers are separate: self-healing data, Merkle-tree checksumming, copy-on-write transactions, and efficient RAID rebuilds that skip unused blocks.

## Key Concepts

- **Copy-on-write (COW)**: ZFS never overwrites data in place; it writes new data to a new location, then atomically updates pointers. This eliminates the RAID write hole and enables cheap snapshots.
- **Unified volume manager + file system**: ZFS manages raw disks directly, combining what would typically be separate RAID/LVM and filesystem layers. This integration is fundamental to its data integrity guarantees.
- **Merkle tree checksumming**: Every block's checksum is stored in its *parent* block pointer, not alongside the data. This creates a self-validating tree from leaves to root, detecting corruption that co-located checksums would miss.
- **Self-healing**: When a checksum mismatch is detected on read, ZFS automatically reconstructs correct data from redundant copies or parity, repairs the damaged copy, and returns good data — transparently.
- **RAID-Z**: Software RAID with dynamic stripe width — every block is its own stripe, eliminating the read-modify-write penalty and write hole. Variants: RAID-Z1 (1 parity disk), RAID-Z2 (2), RAID-Z3 (3).
- **Snapshots and clones**: Zero-cost point-in-time snapshots via COW; clones create writable forks from snapshots. Checkpoints provide pool-level rollback.
- **Scrub vs fsck**: ZFS replaces offline fsck with online scrub that traverses *all* data and metadata, verifying checksums and repairing corruption on a live filesystem.
- **128-bit addressing**: Theoretical max pool size of 2^128 bytes (256 trillion yobibytes); max file size 16 EiB (2^64 bytes).
- **ARC (Adaptive Replacement Cache)**: ZFS's caching layer tracks evicted blocks to reassess caching decisions, achieving 80%+ hit rates.
- **Transparent compression, encryption, deduplication**: Applied in the I/O pipeline in order: compress → encrypt → checksum → dedup.
- **Deduplication caveat**: Dedup tables are held primarily in RAM and are memory-hungry; not practical for all workloads.
- **ECC RAM strongly recommended**: ZFS does not checksum in-memory (ARC) data by default, assuming enterprise hardware with ECC.

## Commands and Syntax

- **Scrub**: Regularly examines all data for silent corruption; recommended weekly for commodity disks, monthly for enterprise disks.
- **Copies property**: `copies=2` or `copies=3` stores multiple copies of data on disk for additional redundancy beyond RAID.
- **Encryption**: Policy set at dataset creation time; wrapping keys changeable without taking filesystem offline; child datasets inherit encryption policy by default.
- **Snapshots**: Can be taken at very high frequency (multiple per hour) without performance degradation; can be rolled back live or cloned into independent filesystems.
- **Checkpoint**: Pool-level snapshot enabling rollback of structural pool operations.

## Relationships

- **vs. traditional RAID**: ZFS should *not* be used behind hardware RAID controllers — they interfere with ZFS's algorithms, reduce reliability, and prevent ZFS from detecting disk conditions. Use HBA/JBOD passthrough instead.
- **vs. fsck/journaling filesystems**: ZFS's scrub replaces fsck; works online, validates data (not just metadata), and uses redundancy for repair rather than partial-data heuristics.
- **vs. Btrfs**: Both are COW filesystems with checksumming; ZFS is 128-bit vs Btrfs's 64-bit addressing. ZFS has more mature RAID-Z; Btrfs is GPL-licensed (kernel-native on Linux).
- **vs. UFS/ext/XFS/NTFS**: A 1999 study showed none of these provided sufficient protection against silent data corruption — ZFS was designed to address this gap.
- **OpenZFS vs Oracle ZFS**: Forked in 2010 after Oracle closed the source. OpenZFS coordinates open-source development across FreeBSD, Linux, and illumos.
- **SLOG/ZIL**: Separate intent log device converts synchronous writes to asynchronous for performance; related to ZFS's transactional write model.
- **Tiered storage**: ZFS natively handles caching tiers (L2ARC, SLOG) because it understands file-level access patterns, unlike standalone volume managers.

## Exam-Relevant Points

- ZFS stores checksums in the **parent block pointer**, not with the data itself — this is the key design difference enabling its Merkle tree integrity model.
- RAID-Z uses **dynamic stripe width** (each block = one stripe), eliminating the write hole without requiring NVRAM or write buffering.
- **Hardware RAID controllers should be avoided** with ZFS; use HBA in JBOD mode for direct disk access.
- RAID-Z3 exists because multi-TB drive rebuild times can take weeks, during which additional failures are likely — triple parity mitigates this.
- Scrub runs on **mounted, live** filesystems (unlike fsck which requires offline/unmounted).
- The I/O pipeline order is: **compress → encrypt → checksum → dedup**.
- Max file size: **16 EiB** (2^64 bytes); max pool size: **2^128 bytes**.
- ZFS encryption wrapping keys can be changed **without taking the filesystem offline**; data encryption keys are generated at dataset creation and shared only with descendant snapshots/clones.
- ZFS **does not check in-memory data integrity by default** — it assumes ECC RAM. This is a known operational requirement.
- Copy-on-write semantics combined with RAID-Z eliminate the **RAID write hole** — a classic failure mode where a crash during read-modify-write leaves parity inconsistent.
