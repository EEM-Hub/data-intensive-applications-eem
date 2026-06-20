---
source: sources/wiki-Shadow_paging.md
source_url: https://en.wikipedia.org/wiki/Shadow_paging
---

## Shadow Paging: Copy-on-Write Technique for Database Atomicity and Durability

Shadow paging is a database technique that provides atomicity and durability (two ACID properties) by avoiding in-place updates to storage pages. Instead of modifying pages directly, it allocates a new "shadow" copy, modifies that copy freely, then atomically swaps references from the old page to the new one. This is a foundational alternative to write-ahead logging (WAL) for crash recovery in database systems.

## Key Concepts

- **Page**: A unit of physical storage (typically 1–64 KiB on disk) — the granularity at which shadow paging operates.
- **Shadow page**: A newly allocated copy of a page that can be modified without consistency concerns because no other on-disk pages reference it yet.
- **Copy-on-write semantics**: Pages are never modified in place; a new copy is written, then activated by updating references.
- **Atomic activation**: The page becomes visible (durable) only when all references are switched to point to the new version — this is what provides atomicity.
- **Recursive cost problem**: If referring pages must also be updated via shadow paging, the update can recurse up the reference hierarchy (e.g., to a superblock), becoming expensive.
- **Write-behind caching**: A mitigation for recursive cost — delay making pages durable to batch updates to frequently-modified high-level pages (used by WAFL).
- **Old master–new master**: A historical mainframe batch processing analogue where each day's output was written to two disks (one backup, one working copy for the next run).

## Commands and Syntax

No specific commands or configuration syntax — shadow paging is a conceptual technique implemented internally by storage engines and file systems.

## Relationships

- **ACID properties**: Shadow paging directly provides **atomicity** (all-or-nothing page activation) and **durability** (once references are swapped, the change persists).
- **Write-ahead logging (WAL)**: The primary alternative approach; WAL uses in-place updates with a sequential log for recovery, and is more widely adopted in modern systems.
- **Copy-on-write (COW)**: Shadow paging is a specific application of the general COW pattern to database storage pages.
- **WAFL (Write Anywhere File Layout)**: NetApp's file system that uses shadow paging with write-behind caching to amortize the recursive update cost.
- **Purely functional data structures**: Shadow paging shares the property of avoiding in-place mutation — structurally similar to persistent/immutable data structures.
- **B-tree storage**: Shadow paging's recursive cost is most visible in tree-structured storage where updating a leaf forces updates up to the root.

## Exam-Relevant Points

- Shadow paging provides **atomicity and durability**, not isolation or consistency — know which two ACID properties it addresses.
- The key distinction from WAL: shadow paging avoids in-place updates entirely; WAL uses in-place updates with a log for undo/redo.
- The recursive update problem is the main **performance weakness** — updating a leaf page can cascade through all ancestor pages up to the root/superblock.
- WAFL's solution to recursive cost is **write-behind caching** (lazy durability), which trades **higher commit latency** for better throughput.
- Shadow paging is conceptually a **copy-on-write** technique applied at the page level.
- WAL is described as the **more popular** solution in practice compared to shadow paging.
