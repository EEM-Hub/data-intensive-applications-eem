---
source: sources/wiki-Fsync.md
source_url: https://en.wikipedia.org/wiki/Fsync
---

## Unix sync: Flushing Kernel Buffers to Non-Volatile Storage

The `sync` system call and command-line utility commits all data from kernel filesystem buffers to non-volatile storage. It is a critical primitive for ensuring data durability, particularly in database systems, and sits at the intersection of operating system I/O, storage hardware semantics, and application reliability.

## Key Concepts

- **`sync()`** flushes *all* kernel filesystem buffers to non-volatile storage. Declared as `void sync(void)` in `<unistd.h>`.
- **`fsync(fd)`** flushes only buffered data for a specific file descriptor — more targeted than `sync()`.
- **`fdatasync(fd)`** writes only the file's data changes, not necessarily metadata — lighter than `fsync()`.
- Higher-level I/O layers (e.g., stdio) maintain their own buffers separate from the kernel's; `sync` only affects kernel buffers.
- Historically, Unix systems ran flush/update daemons (e.g., Linux's `pdflush`, removed 2012) to call `sync` periodically.
- Buffers are also flushed on filesystem unmount or remount read-only (e.g., before shutdown).
- **Write errors may not surface at `write()` time** — they are often reported only at `fsync()`, `msync()`, or `close()`. Callers must check `fsync()` return values to detect data loss.
- Prior to 2018, Linux's `fsync()` had a bug where it could fail to report error status under certain conditions.

## Commands and Syntax

- **Command-line**: `sync` (flushes all filesystem buffers)
- **C API**:
  ```c
  #include <unistd.h>
  void sync(void);          // flush everything
  int fsync(int fd);        // flush specific file descriptor
  int fdatasync(int fd);    // flush data only, skip metadata
  ```
- **`hdparm -F`**: Instructs the HDD controller to flush the on-drive write cache buffer (hardware-level).
- **`eatmydata`**: Wrapper that transparently disables `fsync()` and related calls for a program — used in throwaway tasks (e.g., speeding up package installs in temporary environments).

## Relationships

- **Durability (ACID)**: `fsync` is the mechanism databases use to implement the "D" in ACID. PostgreSQL uses `fsync()` and `fdatasync()` for durable commits.
- **Write-Ahead Log (WAL)**: Databases sync WAL files frequently but sync main data files less often, amortizing the cost of `fsync`.
- **Page cache**: `sync` flushes the kernel page cache to disk. Without `sync`, data exists only in volatile memory.
- **Storage hardware**: Hard drives may have their own volatile write caches. Force Unit Access (FUA) in SCSI/SATA-NCQ allows bypassing the drive cache for specific writes without flushing the entire cache — more efficient than full cache flush.
- **Filesystem semantics**: On ext3 `data=ordered`, calling `fsync` on one file can flush the entire filesystem's write cache, causing performance problems for unrelated I/O.
- **Transaction logs**: Complement `fsync` by recording recent changes so that crash recovery can redo lost writes without syncing main data files on every commit.

## Exam-Relevant Points

- **`sync()` vs `fsync()` vs `fdatasync()`**: `sync` = all buffers; `fsync` = one file descriptor (data + metadata); `fdatasync` = one file descriptor (data only, skipping metadata).
- **Rotating disk commit rate**: A rotating hard drive can only commit once per rotation, limiting single-client durable commits to a few hundred per second.
- **Disabling fsync improves performance but risks corruption**: Turning off fsync dramatically improves database commit throughput but introduces risk of data loss or corruption after a crash.
- **Error reporting**: Write errors are often deferred to `fsync()`/`close()` rather than `write()` — applications must check `fsync()` return values.
- **FUA (Force Unit Access)**: Allows the host to ensure data reaches disk platters without flushing the entire drive cache. Available in SCSI and SATA with NCQ. Linux enabled SATA/NCQ FUA support in 2012.
- **Drive write caches can "lie"**: Hardware may report writes as complete when data is only in volatile drive cache, creating a durability gap even when software calls `fsync`.
- **WAL pattern**: Databases use transaction logs (synced frequently) to allow less frequent syncing of main data files — a key durability/performance tradeoff.
- **The Firefox/ext3 incident (2008)**: Illustrates how `fsync` on ext3 `data=ordered` flushed the *entire* filesystem cache, not just the target file — a cross-file performance penalty.
