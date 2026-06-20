---
source: sources/wiki-Journaling_file_system.md
source_url: https://en.wikipedia.org/wiki/Journaling_file_system
---

## Journaling File Systems: Crash Recovery Through Write-Ahead Logging

Journaling file systems use a dedicated log (the journal) to record pending changes before committing them to the main file system. This write-ahead strategy ensures that after a crash or power failure, the file system can be recovered quickly by replaying the journal, rather than requiring a full consistency check (e.g., `fsck`) across all data structures.

## Key Concepts

- **Journal (write-ahead log):** A dedicated area, usually a circular log, where intended changes are recorded before being applied to the main file system.
- **Atomicity of changes:** Journal entries either complete fully (replayed on recovery) or are discarded entirely (incomplete writes detected via missing/mismatched checksums). No partial state survives.
- **Crash consistency problem:** Multi-step file system operations (e.g., deleting a file requires removing the directory entry, freeing the inode, and freeing disk blocks) can leave data structures in an invalid intermediate state if interrupted — no ordering of steps eliminates all failure modes.
- **Physical journal:** Logs advance copies of every block that will be written. Provides absolute fault protection but imposes a write-twice penalty (every changed block written to journal then to main storage).
- **Logical (metadata-only) journal:** Logs only metadata changes, not file data. Substantially better write performance but allows data corruption if file data and metadata fall out of sync after a crash.
- **Write hazards:** Write caches (OS-level and device-level) can reorder writes, potentially committing metadata before data. Journaling file systems use barriers or cache flushes to enforce correct ordering, trading performance for correctness.
- **Checksum bracketing:** Journal implementations (e.g., JBD2 in ext4) wrap each logged change with a checksum so that partially written entries are detected and skipped during replay.
- **Recovery process:** On mount after crash, read the journal and replay all complete entries — far faster than walking all data structures with fsck.

## Commands and Syntax

- **`fsck`** — File system consistency checker; walks all data structures to detect and repair corruption. Journaling makes this largely unnecessary at mount time.
- **`tune2fs`** — Can configure journaling behavior on ext file systems (e.g., selecting journal mode: `data=journal`, `data=ordered`, `data=writeback`).
- **Barrier support in ext3/ext4** — Forces device cache flushes at critical journal points to prevent write reordering from violating consistency guarantees.

## Relationships

- **ACID properties:** Journaling provides the atomicity and durability guarantees analogous to database transaction logs.
- **Log-structured file systems:** The journal *is* the entire file system — eliminates the write-twice penalty but requires garbage collection.
- **Copy-on-write file systems (ZFS, Btrfs):** Achieve crash consistency without journaling by never modifying data in place — new data is written to fresh blocks, then metadata pointers are updated bottom-up to the superblock.
- **Soft updates (UFS):** An alternative to journaling that carefully orders writes so on-disk state is never inconsistent (except for storage leaks recovered by background garbage collection).
- **Intent log / Transaction processing:** The journal is functionally an intent log; the same concept underpins database write-ahead logs (WAL).
- **inode structure:** Journaling protects inode metadata updates; understanding inodes is prerequisite to understanding what metadata journaling covers.

## Exam-Relevant Points

- **Physical vs. logical journaling trade-off:** Physical journals guarantee both data and metadata consistency but double write I/O; logical journals protect only metadata, improving performance but risking data corruption after crashes.
- **The three-step delete problem:** Deleting a file requires removing the directory entry, freeing the inode, and freeing disk blocks — no ordering of these three steps prevents all possible corruption scenarios without journaling.
- **Recovery speed:** Journaling replays only the journal (bounded size); fsck walks the entire file system (proportional to total size). This is the primary operational motivation for journaling.
- **History:** IBM JFS in AIX 3.1 (1990) was among the first commercial UNIX journaling file systems. NTFS (1993), HFS+ (1998), and ext3 (2001) followed.
- **Alternatives comparison:** Log-structured FS eliminates write-twice penalty; copy-on-write FS (ZFS, Btrfs) avoids in-place updates entirely; soft updates enforce write ordering without a journal but require background garbage collection.
- **Write barriers:** ext3/ext4 use barriers to force device cache flushes, preventing hardware write reordering from breaking journal consistency — a critical detail often tested.
- **External journals:** Can be placed on a separate device (e.g., SSD or battery-backed NVRAM) for improved performance.
