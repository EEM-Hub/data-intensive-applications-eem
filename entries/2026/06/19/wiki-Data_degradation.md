---
source: sources/wiki-Data_degradation.md
source_url: https://en.wikipedia.org/wiki/Data_degradation
---

## Data Degradation (Bit Rot)

Data degradation is the gradual corruption of computer data due to an accumulation of non-critical failures in a data storage device. Also known as data decay, data rot, digital decay, or bit rot, it results in a decline in data quality over time even when data is not being actively used. This is a fundamental challenge for long-term data storage and digital preservation.

## Key Concepts

- **Soft errors in DRAM**: Cosmic rays and high-energy particles can flip bits in dynamic RAM, altering program code or stored data. ECC memory mitigates this.
- **Charge leakage in solid-state media**: EPROMs, flash memory, and SSDs store data as electrical charges that slowly leak through imperfect insulation. Multi-level cells (MLC) are especially vulnerable due to narrower voltage margins.
- **Magnetic decay**: Hard drives, floppy disks, and tapes lose magnetic orientation over time. Higher temperatures accelerate loss. Modern HDDs use Giant Magnetoresistance for longer magnetic lifespan (decades).
- **Optical media breakdown**: CD-R, DVD-R, and BD-R suffer from dye degradation and backing layer deterioration. Early cyanine dyes lacked UV stability; later discs use inorganic mixtures.
- **Paper media degradation**: Driven by acid hydrolysis and oxidation of cellulose; accelerated by humidity, temperature, acids, oxygen, light, and pollutants.
- **Latent faults**: Silent data corruption that goes undetected until the affected data is actually accessed and audited — the most dangerous form because no error is raised at write time.
- **JPEG sensitivity**: Because JPEG stores encoding parameters rather than raw pixel data, a single bit flip can cause visually significant corruption across a region of the image.
- **No complete solution exists**: Data degradation cannot be fully eliminated, only mitigated through layered strategies.

## Commands and Syntax

- **Detecting bit-level differences on Linux**:
  ```bash
  cmp -b original.jpg possibly-corrupted.jpg
  ```
  Reveals the binary difference between two files, useful for identifying bit rot.

- **Solid-state refresh cycle**: Reprogramming flash media approximately once per decade (or every 6 months for SD/USB) prevents charge-leak decay, provided an undamaged master copy exists.

- **Checksum verification**: Use checksums to verify on-chip data integrity before reprogramming or to detect latent corruption proactively.

## Relationships

- **Error Correction Codes (ECC)**: Used at both the DRAM level (ECC memory) and disk controller level to detect and correct errors before they become visible data corruption.
- **File systems (ZFS, Btrfs, ReFS)**: Next-generation file systems designed specifically to address bit rot through checksumming, copy-on-write semantics, and self-healing with redundant copies.
- **RAID**: Provides internal redundancy and error detection/correction mechanisms at the storage array level.
- **Digital preservation**: Data degradation is a core challenge; mitigation requires replication, auditing, and geographically distributed autonomous storage sites.
- **Data scrubbing**: The proactive process of reading and verifying data to detect latent faults before they cause data loss.
- **Data corruption**: Data degradation is the gradual accumulation path to data corruption; distinct from sudden failures like head crashes.
- **Backup and replication**: Primary mitigation strategy — checksumming against replicas is the only way to detect latent faults proactively.

## Exam-Relevant Points

- **Bit rot affects all storage media types** — DRAM, solid-state, magnetic, optical, and paper — through different physical mechanisms.
- **ECC memory mitigates soft errors in DRAM** caused by cosmic rays and high-energy particles.
- **Flash storage decay** is caused by charge leakage through imperfect insulation; modern controllers compensate by trying lower threshold voltages until ECC passes.
- **Latent faults** are silent corruptions detected only when data is accessed and audited — not at write time.
- **ZFS, Btrfs, and ReFS** are file systems specifically designed to combat data degradation through integrity checking and self-repair.
- **Checksumming and replication** are the only proactive way to detect latent faults; without auditing, corruption remains hidden until access.
- **Mitigation best practice**: Distribute replicas across multiple autonomous administrative sites with diverse hardware/software to resist failures, human error, and cyberattacks.
- **No technology fully eliminates data degradation** — all strategies are mitigation, not prevention.
- **Increasing disk capacity increases bit rot risk**: Larger disks and files mean more bits exposed to potential corruption, raising the statistical likelihood of undetected errors.
