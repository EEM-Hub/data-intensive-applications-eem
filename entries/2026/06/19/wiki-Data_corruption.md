---
source: sources/wiki-Data_corruption.md
source_url: https://en.wikipedia.org/wiki/Data_corruption
---

## Data Corruption: Types, Causes, and Countermeasures

Data corruption is the unintended alteration of computer data during writing, reading, storage, transmission, or processing. It ranges from minor data loss to complete system crashes and can be caused by hardware failures, software bugs, environmental interference, malware, and even cosmic rays. This topic is fundamental to understanding why data-intensive systems must implement end-to-end data integrity mechanisms.

## Key Concepts

- **Two types of data corruption**: *detected* (system catches it, may recover) and *undetected/silent* (most dangerous — no indication data is wrong)
- **Silent data corruption (SDC)**: errors that go unnoticed by disk firmware or OS; can cause cascading failures as corrupted state compounds over time
- **Error sources span the entire stack**: disk media, cables, power supply, vibration, network, cosmic radiation, firmware bugs, and faulty CPU cores
- **Disk capacity growth has not been matched by error rate improvement** — larger drives store more data at the same per-bit error rate, making corruption statistically more likely
- **Firmware bugs account for 5–10% of storage failures** (per USENIX study of 39,000 storage systems)
- **Faulty CPU cores** identified by Google and Facebook (2021) as a corruption source, occurring at a rate of several per thousand cores
- **Real-world scale**: CERN found ~128 MB silently corrupted out of 97 PB over six months; Greenplum faced silent corruption every 15 minutes; NetApp found 400,000+ silent corruptions across 1.5M HDDs over 41 months
- **Cascading failures**: corrupted filesystem metadata can damage multiple files progressively as the filesystem continues to operate in a corrupted state

## Commands and Syntax

No specific commands are defined in this source, but the following tools and mechanisms are referenced:

- **S.M.A.R.T. monitoring**: tools available on most OSes to watch for deteriorating disk parameters and impending failures
- **Data scrubbing**: background parity-checking scans that catch and recover disk errors before they accumulate beyond recovery capacity
- **ECC (Error Correcting Codes)**: stored per-sector on disk; drives can silently remap failing sectors to spare sectors
- **Checksumming filesystems**: ZFS, Btrfs, HAMMER, ReFS checksum both data and metadata internally
- **RAID**: parity-based reconstruction of corrupted data across disk arrays (effectiveness depends on RAID level)

## Relationships

- **Data Integrity**: corruption is the primary threat to data integrity; countermeasures like checksums and ECC are integrity mechanisms
- **Replication and Redundancy**: RAID, integrated filesystem redundancy (ZFS mirrors/raidz), and backups are the recovery path when corruption is detected
- **End-to-End Data Protection**: checksumming at the filesystem level (e.g., ZFS) provides integrity across the full storage stack, unlike layer-specific approaches that leave gaps between layers
- **Data Scrubbing**: proactive background verification complements on-read detection by catching latent errors before they compound
- **Distributed Systems**: silent corruption is especially dangerous at scale — AWS S3 outage (2008) was caused by data corruption; large-scale systems must assume corruption will occur
- **Soft Errors and Hardware Reliability**: cosmic rays cause most soft errors in DRAM; this connects to ECC memory and radiation hardening in mission-critical systems

## Exam-Relevant Points

- **Silent data corruption is undetected by disk firmware or OS** and is the most dangerous form because there is no error indication
- **CERN study**: error rates for silent corruption are far higher than 1 in 10^16 bits
- **Disk error rates have remained roughly constant** even as capacity has grown — probability of encountering corruption increases with data volume
- **End-to-end data protection** (e.g., ZFS checksumming data and metadata) is superior to layer-specific integrity checks because corruption can occur at layer boundaries
- **Data scrubbing** catches errors proactively during background scans rather than waiting for read-time detection
- **Checksums detect corruption; ECC corrects it** — these are complementary mechanisms
- **Filesystems with built-in checksumming**: ZFS, Btrfs, HAMMER, ReFS
- **Cascading failure pattern**: undetected corruption in metadata can progressively damage an entire filesystem
- **Modern corruption sources include CPUs themselves** — Google and Facebook identified mercurial (faulty) cores at a rate of several per thousand (2021)
- **In encrypted or compressed data, even a small corruption can render an entire dataset unusable** — amplification effect
