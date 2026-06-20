---
source: sources/wiki-OpenZFS.md
source_url: https://en.wikipedia.org/wiki/OpenZFS
---

## OpenZFS: Open-Source ZFS File System and Volume Manager

OpenZFS is the open-source continuation of the ZFS file system originally developed by Sun Microsystems for Solaris. It provides a combined file system and volume manager with advanced data integrity features including self-healing, copy-on-write, snapshots, compression, deduplication, and RAID-Z. After Oracle acquired Sun and closed ZFS development in 2010, the community forked the codebase via illumos. In 2020, the ZFS-on-Linux and broader OpenZFS codebases were merged into OpenZFS 2.0, unifying Linux and FreeBSD support under a single project. It is licensed under CDDL and primarily used in enterprise, data center, and NAS environments.

## Key Concepts

- **Self-healing**: OpenZFS detects and corrects data errors during normal operation without requiring a dedicated fsck-style checker — a key differentiator for mission-critical/high-availability workloads.
- **Copy-on-write (COW)**: Data is never overwritten in place; new data is written to a new location, then metadata is updated atomically. This underpins snapshots, clones, and crash consistency.
- **Feature flags (pool version 5000)**: Replaced legacy sequential pool version numbers (1–28) to enable distributed, independent development. Each on-disk format change is tagged with a unique name (`feature@<org>:<name>`), and pools are portable between implementations as long as both support the active feature flags.
- **Feature flag states**: *Disabled* (not used, backward-compatible), *Enabled* (may be used, no format changes yet, still backward-compatible), *Active* (backward-incompatible on-disk changes made).
- **Features for read vs. features for write**: Some features only need support for write access; a pool can still be opened read-only without them. Features for read must be supported even to open the pool.
- **CDDL vs. GPL incompatibility**: The FSF considers CDDL and GPL legally incompatible, preventing ZFS from being merged into the mainline Linux kernel. Workarounds include FUSE (userspace, performance penalty) and distributing as a loadable kernel module (Ubuntu's approach since 16.04).
- **RAID-Z**: ZFS's integrated software RAID, eliminating the need for a separate volume manager or hardware RAID controller.
- **Data deduplication and compression**: Built-in storage efficiency features (LZ4 compression commonly used).
- **ARC / L2ARC / SLOG**: Adaptive Replacement Cache (in-memory), Level 2 ARC (SSD-based read cache), and Separate Log (write intent log on fast device) — ZFS's tiered caching architecture.

## Commands and Syntax

- **Feature flag property naming**: `feature@<org-name>:<feature-name>` where `<org-name>` is reverse DNS (e.g., `feature@com.foocompany:async_destroy`). Can be shortened to `feature@async_destroy` when unambiguous.
- **Pool version**: OpenZFS permanently uses pool version `5000` — this number never changes. New features are indicated by feature flags, not version increments.
- **Legacy pool versions**: Versions 1–28 are implied by pool version 5000 and remain for backward compatibility with older Oracle ZFS implementations.
- New pools are created with all supported features enabled by default. Feature states can generally be reverted from *active* back to *enabled* (though not always possible).

## Relationships

- **Oracle ZFS**: The proprietary fork that diverged when Oracle acquired Sun in 2010. Uses sequential version numbering; pool version 5000 was chosen to never conflict with Oracle's numbering.
- **illumos**: The open-source fork of OpenSolaris that initially served as upstream for OpenZFS. Over time, feature development shifted to Linux, and in 2020 the Linux codebase became the canonical upstream.
- **FreeBSD**: Long-standing ZFS support since FreeBSD 7.0 (2008). FreeBSD 13.0 switched from illumos-based ZFS to the unified OpenZFS 2.0 codebase.
- **Linux kernel**: ZFS cannot be merged into mainline due to CDDL/GPL license conflict. Distributed as a loadable kernel module; Ubuntu ships precompiled binaries since 16.04.
- **TrueNAS (formerly FreeNAS)**: Major consumer of OpenZFS — both FreeBSD-based (Core) and Linux-based (Scale/current) editions use OpenZFS as their storage layer. As of TrueNAS 25.04, only the Linux version remains.
- **NAS appliances**: OpenZFS is the dominant filesystem for open-source NAS platforms (TrueNAS, XigmaNAS).
- **FUSE**: Early workaround for Linux licensing issues; now defunct in favor of the native kernel module.
- **Lustre**: The LLNL native ZFS port included early Lustre filesystem support, connecting ZFS to HPC storage.

## Exam-Relevant Points

- OpenZFS pool version is permanently **5000** — new features use feature flags, not version increments.
- Feature flag states: **disabled → enabled → active**. Disabled and enabled are backward-compatible; active is not.
- The **CDDL/GPL license incompatibility** prevents ZFS from being merged into the mainline Linux kernel. Ubuntu resolved this by distributing ZFS as a binary kernel module (since 16.04), a position disputed by the FSF.
- **Self-healing** allows OpenZFS to detect and correct errors during operation without a dedicated filesystem checker.
- ZFS was originally developed at **Sun Microsystems** (2001), open-sourced in **2005** via OpenSolaris, and forked as OpenZFS after **Oracle's 2010 acquisition** of Sun.
- **OpenZFS 2.0 (2020)** merged the ZFS-on-Linux and OpenZFS codebases, making the Linux implementation the canonical upstream for all platforms including FreeBSD.
- Feature flags use the naming convention `feature@<reverse-dns>:<feature-name>` to ensure uniqueness across independent development efforts.
- **Features for read** must be supported to open a pool at all; **features for write** are only required for write access (read-only access is still possible without them).
- FreeBSD has supported ZFS since version **7.0 (2008)**; switched to unified OpenZFS 2.0 in **FreeBSD 13.0**.
- The **Lawrence Livermore National Laboratory (LLNL)** produced the native Linux port that became ZFS-on-Linux (GA release 2013), which ultimately became the basis for OpenZFS 2.0.
