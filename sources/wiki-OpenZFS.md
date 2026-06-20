---
source: https://en.wikipedia.org/wiki/OpenZFS
fetched: 2026-06-19
---

Open-source implementation of ZFS file system 

 
| OpenZFS |
| --- |
|  |
| Original author | Sun Microsystems |
| Developer | OpenZFS Project |
| Release | Ported to various systems between 2006 and 2010.Forkedfrom OpenSolaris August2010;15years ago(2010-08) |
|  |
| Stable release | 2.4.3[1]/ 12 June 2026;8 days ago(12 June 2026) |
| Preview release | 2.4.0-rc5[2]/ December11, 2025;6 months ago(2025-12-11)[2] |
|  |
| Written in | C |
| Operating system | OpenSolaris,illumos,OpenIndiana,FreeBSD,NetBSD,macOS,Linux,OSv |
| License | Common Development and Distribution License |
| Website | openzfs.org |
| Repository | github.com/openzfs/zfs |

  

**OpenZFS** is an [open-source](./Open-source) implementation of the [ZFS](./ZFS) [file system](./File_system) and [volume manager](./Volume_manager) initially developed by [Sun Microsystems](./Sun_Microsystems) for the [Solaris](./Oracle_Solaris) operating system, and is now maintained by the OpenZFS Project. Similar to the original ZFS, the implementation supports features like [data compression](./Data_compression), [data deduplication](./Data_deduplication), [copy-on-write](./Copy-on-write) clones, [snapshots](./Snapshot_(computer_storage)), [RAID-Z](./RAID-Z), and [virtual devices](./Device_driver) that can create filesystems that span multiple disks.

 

One of the main capabilities of OpenZFS is self-healing. The file system can detect and correct errors while in use, without the need for a dedicated file system checker. This feature makes it suitable for mission-critical applications that require high availability.

 

OpenZFS is mainly used in enterprise and [data center](./Data_center) environments, as well as consumer devices like [network-attached storage](./Network-attached_storage) (NAS) devices, where data reliability and safety is essential. While initially designed for Solaris, development has since focused on [Linux](./Linux), while ports exist for various [BSD](./Berkeley_Software_Distribution) distributions and [macOS](./MacOS). Unlike [Oracle ZFS](./Oracle_ZFS), OpenZFS is licensed under the [Common Development and Distribution License](./Common_Development_and_Distribution_License) (CDDL), enabling both open-source and commercial use of the file system.

 

Founding members of OpenZFS include Matt Ahrens, one of the main architects of ZFS.[[3]](./OpenZFS#cite_note-freebsdnews2-3) In 2020, the codebases of OpenZFS and ZFS on Linux, a [kernel module](./Loadable_kernel_module) allowing ZFS to be used on Linux, were merged and released as OpenZFS 2.0, allowing other non-Linux operating systems to receive the various improvements that the Linux driver had incorporated over time.[[4]](./OpenZFS#cite_note-zfs2-ixsystems2-4)[[5]](./OpenZFS#cite_note-zfs2-github2-5)

 

## History

 See also: [History and implementations of ZFS](./History_and_implementations_of_ZFS) 

The [ZFS](./ZFS) file system was originally developed by [Sun Microsystems](./Sun_Microsystems) for the [Solaris](./Solaris_(operating_system)) operating system. The ZFS source code was released in 2005 under the [Common Development and Distribution License](./Common_Development_and_Distribution_License) as part of the [OpenSolaris](./OpenSolaris) [operating system](./Operating_system), and it was later ported to other operating systems and environments.[[6]](./OpenZFS#cite_note-openzfs-history-6)[[7]](./OpenZFS#cite_note-linuxjournal-7)

 

The following is a list of key events in the development of ZFS and its various implementations:[[6]](./OpenZFS#cite_note-openzfs-history-6)[[8]](./OpenZFS#cite_note-linuxcon-openzfs-8)

 
- 2001: Closed-source development of ZFS began with two engineers at Sun.
- 2005: ZFS source code was released as part of the OpenSolaris project.
- 2006: Development of a ZFS port to [FUSE](./Filesystem_in_Userspace) for Linux started.
- 2007: Apple began a project to port ZFS to [Mac OS X](./MacOS).
- 2008: A port to FreeBSD was released as part of FreeBSD 7.0.
- 2008: Development of a native ZFS Linux port started, known as ZFS on Linux.
- 2009: Apple's ZFS project closed, and the MacZFS project took over development of the driver. (It has since also been discontinued; it was current through [Mac OS X 10.9](./OS_X_Mavericks)).
- 2010: OpenSolaris was discontinued following the [acquisition of Sun Microsystems by Oracle](./Acquisition_of_Sun_Microsystems_by_Oracle_Corporation), resulting in the further development of ZFS on Solaris being no longer open-source.
- 2010: Following the discontinuation, a project named [illumos](./Illumos) was formed and [forked](./Fork_(software_development)) OpenSolaris to continue open-source development,[[9]](./OpenZFS#cite_note-9)[[10]](./OpenZFS#cite_note-10) ZFS included. Ports of ZFS to other platforms continued by pulling in upstream changes from [illumos](./Illumos).
- 2012: Feature flags were introduced to replace legacy on-disk version numbers, enabling easier development of the ZFS on-disk format to support new features.
- 2013: Coexisting with the stable version of MacZFS, its prototype generation (known as OpenZFS on OS X or O3X) uses ZFS on Linux as the new upstream codebase.[[11]](./OpenZFS#cite_note-11)[[12]](./OpenZFS#cite_note-12)
- 2013: The first stable release of ZFS on Linux.[[13]](./OpenZFS#cite_note-13)
- 2013: Official announcement of the OpenZFS Project as an organization for maintaining OpenZFS.[[14]](./OpenZFS#cite_note-lwn-567090-14)[[15]](./OpenZFS#cite_note-openzfs-announcement-15) New features and fixes are regularly pulled into OpenZFS from illumos and pushed into all ports to other platforms, and vice versa.[[6]](./OpenZFS#cite_note-openzfs-history-6)
- 2016: [Ubuntu 16.04](./Ubuntu_version_history#1604) includes the open-source ZFS file system variant by default.
- 2020: ZFS on Linux was merged into OpenZFS and added FreeBSD support, unifying the codebase for both platforms.[[16]](./OpenZFS#cite_note-16)

 

### Ports

 

As the [FSF](./Free_Software_Foundation) (Free Software Foundation) claimed that there was a [legal incompatibility between the CDDL and the GPL](./CDDL_and_GPL_legal_incompatibility) in 2005, Sun's implementation of the ZFS file system couldn't be used as a basis for the development of a [module](./Loadable_kernel_module) in the [Linux kernel](./Linux_kernel), couldn't be merged into the [mainline Linux kernel](./Linux_kernel_mainline), and [Linux distributions](./Linux_distribution) generally did not include it as a precompiled kernel module.[[17]](./OpenZFS#cite_note-17)[[18]](./OpenZFS#cite_note-18)[[19]](./OpenZFS#cite_note-19) As a workaround, [FUSE](./Filesystem_in_Userspace), a framework that allows file systems to run in [userspace](./User_space_and_kernel_space), was used on Linux as a separation layer for which the licensing issues did not apply, although with a set of its own issues that includes a performance penalty.[[7]](./OpenZFS#cite_note-linuxjournal-7)[[20]](./OpenZFS#cite_note-20) However, the April 2016 release of [Ubuntu](./Ubuntu) 16.04 [LTS](./Long-term_support) includes ZFS as a kernel module.[[21]](./OpenZFS#cite_note-:0-21)[[22]](./OpenZFS#cite_note-22)

 

### Apple and OS X

 

In the release version of [Mac OS X 10.5](./Mac_os_x_10.5), ZFS was available in read-only mode from the command line, which lacks the possibility to create z-pools or write to them.[[23]](./OpenZFS#cite_note-23) Before the 10.5 release, [Apple](./Apple_Inc.) released the "ZFS Beta Seed v1.1", which allowed read-write access and the creation of z-pools;[[24]](./OpenZFS#cite_note-24) however, the installer for the "ZFS Beta Seed v1.1" has been reported to only work on version 10.5.0, and has not been updated for version 10.5.1 and above.[[25]](./OpenZFS#cite_note-25) In August 2007, Apple opened a ZFS project on their Mac OS Forge web site. On that site, Apple provided the source code and binaries of their port of ZFS which includes read-write access,[[26]](./OpenZFS#cite_note-26) but without an installer.[[27]](./OpenZFS#cite_note-27) In October 2009, Apple discontinued development of the ZFS project on Mac OS Forge with no explanation. Apple removed everything but the CDDL-licensed portion of the source code for their final build of the ZFS project, code named "10a286". Complete ZFS support was originally advertised as a feature of [Snow Leopard Server](./Mac_OS_X_Snow_Leopard_Server) before launch,[[28]](./OpenZFS#cite_note-28) but by the time the operating system was released all references to this feature had been removed from its features page.[[29]](./OpenZFS#cite_note-29)

 

Apple's "10a286" source code release, and versions of the previously released source and binaries, have been preserved and new development had been adopted by the MacZFS project[[30]](./OpenZFS#cite_note-30)[[31]](./OpenZFS#cite_note-code.google.com-31)[[32]](./OpenZFS#cite_note-32) to continue development outside of Apple. As of July 2012, Mac ZFS implements z-pool version 8 and ZFS version 2, released with the October 2008 release of [Solaris](./Solaris_(operating_system)). Additional historical information and commentary can be found on the Mac ZFS web site and [FAQ](./FAQ).[[33]](./OpenZFS#cite_note-33) However, the project ceased development in mid 2013 with a message asking users to switch to *Open ZFS on OSX* (abbreviated to *O3X*).[[34]](./OpenZFS#cite_note-34)

 

## Implementations

 See also: [Oracle ZFS § Implementations](./Oracle_ZFS#Implementations) 

### OpenSolaris

 
- [OpenSolaris](./OpenSolaris) 2008.05, 2008.11 and 2009.06 use ZFS as their default filesystem.

 

#### OpenIndiana

 
- [OpenIndiana](./OpenIndiana) uses OpenZFS with feature flags as implemented in [Illumos](./Illumos). ZFS version 28 used up to version 151a3.[[35]](./OpenZFS#cite_note-OI-151a5_release_notes-35)
- By upgrading from OpenSolaris snv_134 to both OpenIndiana and Solaris 11 Express, one also has the ability to upgrade and separately boot Solaris 11 Express on the same ZFS pool.[[36]](./OpenZFS#cite_note-istgt-36)

 

### macOS

 
- *Open ZFS on OSX* (abbreviated to *O3X*) is an implementation of ZFS for [macOS](./MacOS).[[37]](./OpenZFS#cite_note-37) O3X is under active development, with close relation to ZFS on Linux and illumos' ZFS implementation, while maintaining feature flag compatibility with ZFS on Linux. O3X implements z-pool version 5000, and includes the Solaris Porting Layer (SPL) originally written for Mac ZFS, which has been further enhanced to include a memory management layer based on the illumos kmem and vmem allocators. O3X is fully featured, supporting LZ4 compression, deduplication, ARC, [L2ARC](./L2ARC), and SLOG.[*[citation needed](./Wikipedia:Citation_needed)*]
- [MacZFS](./MacZFS) is free software providing support for ZFS on macOS. The stable legacy branch provides up to ZFS pool version 8 and ZFS filesystem version 2. The development branch, based on ZFS on Linux and OpenZFS, provides updated ZFS functionality, such as up to ZFS zpool version 5000 and feature flags. This implementation is no longer supported, and developers have advised users to switch to O3X.[[38]](./OpenZFS#cite_note-zpool-features-38)[[39]](./OpenZFS#cite_note-39)
- A proprietary implementation of ZFS (Zevo) was available at no cost from [GreenBytes](./GreenBytes), Inc., implementing up to ZFS file system version 5 and ZFS pool version 28.[[40]](./OpenZFS#cite_note-40) Zevo offered a limited ZFS feature set, pending further commercial development; it was sold to [Oracle](./Oracle_Corporation) in 2014, with unknown future plans.[*[citation needed](./Wikipedia:Citation_needed)*]

 

### BSD

 

#### DragonFlyBSD

 
- Edward O'Callaghan started the initial port of ZFS to [DragonFlyBSD](./DragonFlyBSD).[[41]](./OpenZFS#cite_note-dfly-41)

 

#### NetBSD

 
- The NetBSD ZFS port was started as a part of the 2007 [Google Summer of Code](./Google_Summer_of_Code) and in August 2009, the code was merged into [NetBSD](./NetBSD)'s source tree.[[42]](./OpenZFS#cite_note-netbsd-42)

 

#### FreeBSD

 
- Paweł Jakub Dawidek ported ZFS to [FreeBSD](./FreeBSD), and it has been part of FreeBSD since version 7.0.[[43]](./OpenZFS#cite_note-fbsd-43) This includes zfsboot, which allows booting FreeBSD directly from a ZFS dataset.[[44]](./OpenZFS#cite_note-fbsd-zfs13-44)[[45]](./OpenZFS#cite_note-fbsd-zfs13voras-45)
- FreeBSD's ZFS implementation is fully functional; the only missing features are kernel [CIFS](./CIFS) server and [iSCSI](./ISCSI), but the latter can be added using externally available packages.[[46]](./OpenZFS#cite_note-autogenerated1-46) [Samba](./Samba_(software)) can be used to provide a userspace CIFS server.
- FreeBSD 13.0-RELEASE switches ZFS implementation from illumos-based code base to the unified OpenZFS 2 code base.[[47]](./OpenZFS#cite_note-47) This change allows FreeBSD to receive OpenZFS improvements much quicker.[[48]](./OpenZFS#cite_note-48)

 

#### MidnightBSD

 
- [MidnightBSD](./MidnightBSD), a desktop operating system derived from FreeBSD, supports ZFS storage pool version 6 as of 0.3-RELEASE. This was derived from code included in [FreeBSD](./FreeBSD) 7.0-RELEASE. An update to storage pool 28 is in progress in 0.4-CURRENT and based on 9-STABLE sources around FreeBSD 9.1-RELEASE code.[*[citation needed](./Wikipedia:Citation_needed)*]

 

#### TrueOS (formerly PC-BSD)

 
- [TrueOS](./TrueOS) (formerly known as PC-BSD, now defunct[[49]](./OpenZFS#cite_note-trueos-defunct-49)) was a desktop-oriented distribution of FreeBSD, which inherited its ZFS support.[*[citation needed](./Wikipedia:Citation_needed)*]

 

#### TrueNAS Core, (formerly FreeNAS)

 
- [TrueNAS](./TrueNAS) Core, an embedded open source [network-attached storage](./Network-attached_storage) (NAS) distribution based on [FreeBSD](./FreeBSD), has the same ZFS support as FreeBSD and [PC-BSD](./PC-BSD).[[50]](./OpenZFS#cite_note-50)

 

#### pfSense

 
- [pfSense](./PfSense), an open source BSD based [router](./Router_(computing)), supports ZFS, including installation and booting to ZFS pools, as of version 2.4.

 

#### OPNsense

 
- [OPNsense](./OPNsense), an open source [FreeBSD](./FreeBSD) based [firewall](./Firewall_(computing)) and [router](./Router_(computing)) distribution, supports ZFS, including installation and booting.

 

#### XigmaNAS

 
- [XigmaNAS](./XigmaNAS) (formerly NAS4Free), an embedded open source [network-attached storage](./Network-attached_storage) (NAS) distribution based on [FreeBSD](./FreeBSD), has the same ZFS support as FreeBSD, ZFS storage pool version 5000. This project is a continuation of FreeNAS 7 series project.[[51]](./OpenZFS#cite_note-51)

 

#### Debian GNU/kFreeBSD

 
- Being based on the FreeBSD kernel, [Debian GNU/kFreeBSD](./Debian_GNU/kFreeBSD) has ZFS support from the kernel. However, additional userland tools are required,[[52]](./OpenZFS#cite_note-52) while it is possible to have ZFS as root or /boot file system[[53]](./OpenZFS#cite_note-53) in which case required [GRUB](./GNU_GRUB) configuration is performed by the Debian installer since the *Wheezy* release.[[54]](./OpenZFS#cite_note-54)
- As of January 31, 2013, the ZPool version available is 14 for the *Squeeze* release, and 28 for the *Wheezy-9* release.[[55]](./OpenZFS#cite_note-55)

 

### Linux

 

Although the ZFS filesystem supports [Linux](./Linux)-based operating systems, difficulties arise for [Linux distribution](./Linux_distribution) maintainers wishing to provide native support for ZFS in their products due to [legal incompatibilities](./CDDL_and_GPL_legal_incompatibility) between the ZFS's CDDL license and the [GPL](./GPL) license used by the Linux kernel. To enable ZFS support within Linux, a [loadable kernel module](./Loadable_kernel_module) containing the CDDL-licensed ZFS code must be compiled and loaded into the kernel. According to the [Free Software Foundation](./Free_Software_Foundation), the wording of the GPL license legally prohibits redistribution of the resulting product as a [derivative work](./Derivative_work),[[56]](./OpenZFS#cite_note-56)[[57]](./OpenZFS#cite_note-57) though this viewpoint has caused some controversy.[[58]](./OpenZFS#cite_note-58)[[59]](./OpenZFS#cite_note-59)

 

#### ZFS on FUSE

 

One potential workaround to licensing incompatibility was trialed in 2006, with an experimental port of the ZFS code to Linux's [FUSE](./FUSE_(Linux)) system. The [filesystem](./Filesystem) ran entirely in [userspace](./Userspace) instead of being integrated into the Linux kernel, and was therefore not considered a derivative work of the kernel. This approach was functional, but suffered from significant performance penalties when compared with integrating the filesystem as a native kernel module running in [kernel space](./Kernel_space).[[60]](./OpenZFS#cite_note-FUSE-60) As of 2016, the ZFS on FUSE project appears to be defunct, as the ZFS on Linux kernel driver has prevailed over the userspace one.

 

#### Native ZFS on Linux

 

A native port of ZFS for Linux produced by the [Lawrence Livermore National Laboratory](./Lawrence_Livermore_National_Laboratory) (LLNL) was released in March 2013,[[61]](./OpenZFS#cite_note-61)[[62]](./OpenZFS#cite_note-62) following these key events:[[63]](./OpenZFS#cite_note-LinuxCon_2013:_OpenZFS-63)

 
- 2008: prototype to determine viability
- 2009: initial ZVOL and [Lustre](./Lustre_(file_system)) support
- 2010: development moved to [GitHub](./GitHub)
- 2011: [POSIX](./POSIX) layer added
- 2011: community of early adopters
- 2012: production usage of ZFS
- 2013: stable [GA](./General_availability) release

 

As of August 2014[[update]](https://en.wikipedia.org/w/index.php?title=OpenZFS&action=edit), ZFS on [Linux](./Linux) uses the OpenZFS pool version number 5000, which indicates that the features it supports are defined via [feature flags](./OpenZFS#Pool_versions_and_feature_flags). This pool version is an unchanging number that is expected to never conflict with version numbers given by Oracle.[[64]](./OpenZFS#cite_note-64)

 

#### KQ InfoTech

 

Another native port for Linux was developed by KQ InfoTech in 2010.[[65]](./OpenZFS#cite_note-linuxforums-65)[[66]](./OpenZFS#cite_note-66) This port used the *zvol* implementation from the Lawrence Livermore National Laboratory as a starting point. A release supporting *zpool* v28 was announced in January 2011.[[67]](./OpenZFS#cite_note-phoronixbenchmark-67) In April 2011, KQ Infotech was acquired by [sTec, Inc.](./STec,_Inc.), and their work on ZFS ceased.[[68]](./OpenZFS#cite_note-phoronix-68) Source code of this port can be found on [GitHub](./GitHub).[[69]](./OpenZFS#cite_note-69)

 

The work of KQ InfoTech was ultimately integrated into the LLNL's native port of ZFS for Linux.[[68]](./OpenZFS#cite_note-phoronix-68)

 

#### Source code distribution

 

While license incompatibilities may arise with the distribution of compiled binaries containing ZFS code, it is generally agreed that distribution of the source code itself is not affected by this. In [Gentoo Linux](./Gentoo_Linux), configuring a ZFS root filesystem is well documented and the required packages can be installed from its package repository.[[70]](./OpenZFS#cite_note-70) [Slackware](./Slackware) also provides documentation on supporting ZFS, both as a kernel module and built into the [kernel](./Kernel_(operating_system)).[[71]](./OpenZFS#cite_note-71)[[72]](./OpenZFS#cite_note-72)

 

#### Ubuntu integration

 

The question of the CDDL license's compatibility with the GPL license resurfaced in 2015, when the Linux distribution [Ubuntu](./Ubuntu_(operating_system)) announced that it intended to make precompiled OpenZFS binary kernel modules available to end-users directly from the distribution's official package repositories.[[73]](./OpenZFS#cite_note-73) In 2016, Ubuntu announced that a legal review resulted in the conclusion that providing support for ZFS via a binary [kernel module](./Kernel_module) was not in violation of the provisions of the GPL license.[[74]](./OpenZFS#cite_note-74) Other organizations such as the [Software Freedom Law Center](./Software_Freedom_Law_Center) followed Ubuntu's conclusion,[[75]](./OpenZFS#cite_note-75) while the FSF and SFC reiterated their opposing views.[[76]](./OpenZFS#cite_note-76)

 

[Ubuntu](./Ubuntu_(operating_system)) 16.04 LTS ("[Xenial Xerus](./Xenial_Xerus)"), released on April 21, 2016, allows the user to install the OpenZFS binary packages directly from the Ubuntu software repositories.[[21]](./OpenZFS#cite_note-:0-21)[[77]](./OpenZFS#cite_note-phoronix-Ubuntu16.04-ZFS-77) As of 2024[[update]](https://en.wikipedia.org/w/index.php?title=OpenZFS&action=edit), no legal challenge has been brought against [Canonical](./Canonical_(company)) regarding the distribution of these packages.

 

As of 2019, Ubuntu supports experimental installation of ZFS as a root filesystem, starting with the 19.10 release ("Eoan Ermine"), to support coexistence of a nearly pure ZFS OS with GRUB and other operating systems on the same disk.[[78]](./OpenZFS#cite_note-78)[[79]](./OpenZFS#cite_note-79)

 

#### TrueNAS (formerly TrueNAS Scale)

 

A version of [TrueNAS](./TrueNAS) by [iXsystems](./IXsystems), based on [Debian Linux](./Debian). As with TrueNAS Core (based on FreeBSD), it uses OpenZFS for storage and adds a variety of additional features. These include expanded device driver support, KVM virtual machines, PCIe passthrough and container support via Kubernetes and Docker. Furthermore, it allows clustered Docker and ZFS via [gluster](./Gluster). Information about the current release can be found at the iXsystems [Software Status](https://www.truenas.com/software-status/) page.[[80]](./OpenZFS#cite_note-80) The "Scale" branding was officially dropped from the name with the release of TrueNAS 25.04, Fangtooth, which only has a Linux release. [[81]](./OpenZFS#cite_note-81)

 

### Microsoft Windows

 

A port of open source ZFS was attempted in 2010 but after a hiatus of over one year development ceased in 2012.[[82]](./OpenZFS#cite_note-82) In October 2017, a new port of OpenZFS was announced by Jörgen Lundman at OpenZFS Developer Summit.[[83]](./OpenZFS#cite_note-83)[[84]](./OpenZFS#cite_note-84)

 

A newer open source port of ZFS which is considered a BETA release, can be found also on GitHub.[[85]](./OpenZFS#cite_note-85)

 

## Version history

 For earlier history, see [ZFS § Version history](./ZFS#Version_history). 
| LatestFOSSstable release |
| --- |

 
| ZFS Pool Version Number | Release date | Significant changes |
| --- | --- | --- |
| 5000 | OpenZFS | Unchanging pool version to signify that the pool indicates new features after pool version 28 usingZFS feature flagsrather than by incrementing the pool version |

 

### Pool versions and feature flags

 See also: [ZFS § Version history](./ZFS#Version_history) 

Originally, [version numbers](./Software_versioning) of the pool and file system were incremented as new features were introduced, in order to designate the on-disk file system format and available features. This worked well when a single entity controlled the development of ZFS, and this versioning scheme is still in use with the ZFS in [Oracle](./Oracle_Corporation) [Solaris](./Solaris_(operating_system)).[[86]](./OpenZFS#cite_note-86)[[87]](./OpenZFS#cite_note-87)

 

In a more [distributed development](./Distributed_development) model, having a single version number is far from ideal as all implementations of OpenZFS would need to agree on all changes to the on-disk file system format. The solution selected by OpenZFS was to introduce *feature flags* as a new [versioning system](./Software_versioning) that tags on-disk format changes with unique names, and supports both completely independent format changes and format changes that depend on each other. A pool can be moved and used between OpenZFS implementations as long as all feature flags in use by the pool are supported by both implementations.[[8]](./OpenZFS#cite_note-linuxcon-openzfs-8): 20, 26–27 [[88]](./OpenZFS#cite_note-openzfs-feature-flags-88): 2–3 [[89]](./OpenZFS#cite_note-89)

 

In OpenZFS, the pool version is permanently set to 5000, signifying that the pool indicates new features by setting or unsetting ZFS feature flags rather than by incrementing the pool version.[[38]](./OpenZFS#cite_note-zpool-features-38) The number 5000 was chosen because it is expected to never conflict with version numbers given by [Oracle](./Oracle_Corporation). Legacy version numbers still exist for pool versions 1–28.[[90]](./OpenZFS#cite_note-90)[[91]](./OpenZFS#cite_note-91)[[92]](./OpenZFS#cite_note-92) Future on-disk format changes are enabled / disabled independently via these feature flags.

 

Legacy version numbers still exist for pool versions 1–28, and are implied by the pool version 5000;[[93]](./OpenZFS#cite_note-openzfs-pools-portable-93) the initial proposal was to use 1000 as the pool version.[[88]](./OpenZFS#cite_note-openzfs-feature-flags-88): 4  Future on-disk format changes are enabled and disabled independently via feature flags.

 

Feature flags are exposed as pool properties, following these naming scheme rules:[[88]](./OpenZFS#cite_note-openzfs-feature-flags-88): 4 

 
- Format of the property name is feature@<org-name>:<feature-name>
- <org-name> is the reverse DNS name of the organization that developed the feature, ensuring unique property names.
- Property names can be shortened to feature@<feature-name> when they remain unambiguous.

 

For example, feature@com.foocompany:async_destroy is a valid property name, and it could be shortened to feature@async_destroy.[[88]](./OpenZFS#cite_note-openzfs-feature-flags-88): 4 

 

Each pool feature can be in either *disabled*, *enabled*, or *active* state. Disabled features are those that will not be used, and no on-disk format changes will be made; as a result, such features are [backward-compatible](./Backward_compatibility). Enabled features are those that will be used, no on-disk format changes have been made yet, but the software may make the changes at any time; such features are still backward-compatible. Active features are those that have made backward-incompatible on-disk format changes to the pool.[[88]](./OpenZFS#cite_note-openzfs-feature-flags-88): 5 

 

When any pool feature is enabled, legacy version of the pool is automatically upgraded to 5000 and any other prerequisite features are also enabled. By default, new pools are created with all supported features enabled. In general, state of a feature can be changed from *active* back to *enabled*, undoing that way performed on-disk format changes and making the pool compatible again with an older OpenZFS implementation; however, for some features that might not be possible.[[88]](./OpenZFS#cite_note-openzfs-feature-flags-88): 5, 9 [[93]](./OpenZFS#cite_note-openzfs-pools-portable-93)

 

On-disk format changes can be associated with either *features for write* or *features for read*. The former are the features that an OpenZFS implementation must support to be capable of writing to the pool, while supporting such features is not mandatory for opening the pool in read-only mode. The latter are the features that an OpenZFS implementation must support to be able to read from the pool or to just open it, because opening a pool is not possible without actually reading from it.[[88]](./OpenZFS#cite_note-openzfs-feature-flags-88): 7 

 

For example, async_destroy feature adds a new on-disk data structure to keep track of freed datasets, but an OpenZFS implementation does not need to know about this data structure to access the pool in read-only mode. Additionally, writing to a pool that has some features in *active* state is not possible by an OpenZFS implementation that does not support the same features.[[88]](./OpenZFS#cite_note-openzfs-feature-flags-88): 7–8 

 

A list of [feature flags](./Feature_flags) and which operating systems support them is available from the OpenZFS documentation Web site[[94]](./OpenZFS#cite_note-94) (here the old Open-ZFS.org Web site[[95]](./OpenZFS#cite_note-95))

 

#### OpenZFS 2.0

 

Historically, OpenZFS has been implemented as a core ZFS code, with each operating system's team adapting it to fit into their projects. This led in some cases to feature stagnation and divergence of features and command lines, as different operating systems developed divergent features and bug fixes, often for a single platform rather than across all platforms. Over time, new feature development shifted from [Illumos](./Illumos) to [Linux](./Linux).[[96]](./OpenZFS#cite_note-jude-BSDCAN2019-96) These new features and fixes then had to be backported to Illumos before they could be re-ported for [FreeBSD](./FreeBSD).[[96]](./OpenZFS#cite_note-jude-BSDCAN2019-96) But this was difficult because the Linux version also included many smaller changes, which were hard to disentangle.[[96]](./OpenZFS#cite_note-jude-BSDCAN2019-96)

 

In 2018, it was agreed that OpenZFS development would be overhauled to remedy these issues.[[96]](./OpenZFS#cite_note-jude-BSDCAN2019-96) Rather than try to import all the Linux changes to other platforms piecemeal, the entire Linux ZFS code would be 'pivoted' as a whole, with other platforms being based on the more actively developed Linux version.[[96]](./OpenZFS#cite_note-jude-BSDCAN2019-96) A wide range of ported and new features, including many long-desired enhancements, would also be rolled out or ported across platforms, and future changes would be discussed across platforms before being implemented.[[96]](./OpenZFS#cite_note-jude-BSDCAN2019-96) The plans included appropriate porting layers to prevent Linux, [GPL](./GPL) or Linux-KPI [shim](./Shim_(computing)) code from being introduced to other platform [kernels](./Kernel_(operating_system)).[[96]](./OpenZFS#cite_note-jude-BSDCAN2019-96)

 

The features in progress or ported for OpenZFS 2.0 is lengthy, and includes:

 
- Faster rollout of enhancements and new features across platforms[[96]](./OpenZFS#cite_note-jude-BSDCAN2019-96)
- Command line standardisation[[96]](./OpenZFS#cite_note-jude-BSDCAN2019-96)
- Improved pool portability (ZFS pools created on one system can be equally used by another)[[97]](./OpenZFS#cite_note-zfs2-github-97)
- Wider cross-platform feature parity and platform independence[[97]](./OpenZFS#cite_note-zfs2-github-97)
- Overlay (union) mounts accepted by default[[97]](./OpenZFS#cite_note-zfs2-github-97)
- Bug fixes and enhancements[[97]](./OpenZFS#cite_note-zfs2-github-97)
- ZTS and various other features working on FreeBSD[[97]](./OpenZFS#cite_note-zfs2-github-97)
- [TRIM](./Trim_(computing)) and [ACL](./Access_control_list)MODE enhancements[[97]](./OpenZFS#cite_note-zfs2-github-97)[[96]](./OpenZFS#cite_note-jude-BSDCAN2019-96)
- ZFS holds (from FreeBSD)[[97]](./OpenZFS#cite_note-zfs2-github-97)
- Enhanced native NFSv4 [ACLs](./Access_control_list) (FreeBSD)[[97]](./OpenZFS#cite_note-zfs2-github-97)
- Enhanced [AES-GCM](./AES-GCM) performance for encrypted pools[[97]](./OpenZFS#cite_note-zfs2-github-97)
- Redacted send/receive[[97]](./OpenZFS#cite_note-zfs2-github-97)
- Log spacemap and other metaslab management enhancements - a project to re-implement ZFS' management of free space and "metaslabs" for much greater efficiency[[97]](./OpenZFS#cite_note-zfs2-github-97)
- Fast clone deletion[[97]](./OpenZFS#cite_note-zfs2-github-97)
- Zstd data compression as a new option[[97]](./OpenZFS#cite_note-zfs2-github-97)
- Channel program property inheritance[[97]](./OpenZFS#cite_note-zfs2-github-97)
- AltiVec RAID-Z[[97]](./OpenZFS#cite_note-zfs2-github-97)
- Bookmark support and copying[[97]](./OpenZFS#cite_note-zfs2-github-97)
- Direct IO support[[97]](./OpenZFS#cite_note-zfs2-github-97)
- Persistent L2ARC (L2ARC retained across reboots)[[97]](./OpenZFS#cite_note-zfs2-github-97)
- Sequential (high speed) scrub and resilver[[96]](./OpenZFS#cite_note-jude-BSDCAN2019-96)
- Scrub pause/resume[[96]](./OpenZFS#cite_note-jude-BSDCAN2019-96)
- Resilver restart[[96]](./OpenZFS#cite_note-jude-BSDCAN2019-96)
- Device (VDEV) removal[[96]](./OpenZFS#cite_note-jude-BSDCAN2019-96)
- Zpool initialize and checkpoint[[96]](./OpenZFS#cite_note-jude-BSDCAN2019-96)
- Channel programs[[96]](./OpenZFS#cite_note-jude-BSDCAN2019-96)
- Large Dnode[[96]](./OpenZFS#cite_note-jude-BSDCAN2019-96)
- Allocation classes (allowing specific high speed storage to be designated for [metadata](./Metadata) and deduplication tables)[[96]](./OpenZFS#cite_note-jude-BSDCAN2019-96)
- Parallel pool mounting[[96]](./OpenZFS#cite_note-jude-BSDCAN2019-96)
- Per-vdev properties[[96]](./OpenZFS#cite_note-jude-BSDCAN2019-96)
- Deduplication enhancements – dedup-log (high speed deduplication), dedup table size limits, and deduplication table preloading (loaded fully at one time rather than piecemeal as needed), listed as "nice to have" in 2018, were all stated in April 2020 to be "coming along nicely" or largely complete[[98]](./OpenZFS#cite_note-openzfs_leadership_notes-98)

 

## See also

 
- ![](//upload.wikimedia.org/wikipedia/commons/thumb/3/31/Free_and_open-source_software_logo_%282009%29.svg/40px-Free_and_open-source_software_logo_%282009%29.svg.png)[Free and open-source software portal](./Portal:Free_and_open-source_software)

 
- [Comparison of file systems](./Comparison_of_file_systems)
- [Btrfs](./Btrfs)—a copy-on-write file system for Linux
- [HAMMER](./HAMMER_(file_system))—a high-availability file system for DragonFly BSD
- [Write Anywhere File Layout](./Write_Anywhere_File_Layout) (WAFL)—NetApp's proprietary file layout

 

## References

 
1. [↑](./OpenZFS#cite_ref-wikidata-12368bc94161b7a6336bcdd3e594c74ec26e1578-v20_1-0) ["Release 2.4.3"](https://github.com/openzfs/zfs/releases/tag/zfs-2.4.3). June 12, 2026. Retrieved June 13, 2026.
2. [1](./OpenZFS#cite_ref-openzfsReleases_2-0) [2](./OpenZFS#cite_ref-openzfsReleases_2-1) [Releases · openzfs/zfs](https://github.com/openzfs/zfs/releases) on [GitHub](./GitHub)
3. [↑](./OpenZFS#cite_ref-freebsdnews2_3-0) ["OpenZFS – Communities co-operating on ZFS code and features"](http://www.freebsdnews.net/2013/09/23/openzfs-communities-co-operating-on-zfs-code-and-features/). *freebsdnews.net*. September 23, 2013. [Archived](https://web.archive.org/web/20131014000145/http://www.freebsdnews.net/2013/09/23/openzfs-communities-co-operating-on-zfs-code-and-features/) from the original on October 14, 2013. Retrieved March 14, 2014.
4. [↑](./OpenZFS#cite_ref-zfs2-ixsystems2_4-0) ["FreeNAS and TrueNAS are Unifying"](https://www.ixsystems.com/blog/freenas-truenas-unification). March 5, 2020. [Archived](https://web.archive.org/web/20200604013042/https://www.ixsystems.com/blog/freenas-truenas-unification/) from the original on June 4, 2020. Retrieved June 7, 2020.
5. [↑](./OpenZFS#cite_ref-zfs2-github2_5-0) ["OpenZFS 2.0 · openzfs/ZFS"](https://github.com/openzfs/zfs/projects/25). *[GitHub](./GitHub)*. [Archived](https://web.archive.org/web/20200417085650/https://github.com/openzfs/zfs/projects/25) from the original on April 17, 2020. Retrieved June 7, 2020.
6. [1](./OpenZFS#cite_ref-openzfs-history_6-0) [2](./OpenZFS#cite_ref-openzfs-history_6-1) [3](./OpenZFS#cite_ref-openzfs-history_6-2) ["OpenZFS History"](http://open-zfs.org/wiki/History). *open-zfs.org*. [Archived](https://web.archive.org/web/20131224105247/http://open-zfs.org/wiki/History) from the original on December 24, 2013. Retrieved September 24, 2013.
7. [1](./OpenZFS#cite_ref-linuxjournal_7-0) [2](./OpenZFS#cite_ref-linuxjournal_7-1) Koutoupis, Petros (June 1, 2016). ["ZFS: Finding Its Way to a Linux Near You?"](http://www.linuxjournal.com/content/zfs-finding-its-way-linux-near-you). *[Linux Journal](./Linux_Journal)*. [Archived](https://web.archive.org/web/20160627221356/http://www.linuxjournal.com/content/zfs-finding-its-way-linux-near-you) from the original on June 27, 2016. Retrieved July 4, 2016.
8. [1](./OpenZFS#cite_ref-linuxcon-openzfs_8-0) [2](./OpenZFS#cite_ref-linuxcon-openzfs_8-1) Ahrens, Matt; Behlendorf, Brian (September 17, 2013). ["LinuxCon 2013: OpenZFS"](https://events.linuxfoundation.org/sites/events/files/slides/OpenZFS%20-%20LinuxCon_0.pdf) (PDF). [Linux Foundation](./Linux_Foundation). [Archived](https://web.archive.org/web/20131113204955/http://events.linuxfoundation.org/sites/events/files/slides/OpenZFS%20-%20LinuxCon_0.pdf) (PDF) from the original on November 13, 2013. Retrieved November 13, 2013.
9. [↑](./OpenZFS#cite_ref-9) Cantrill, Bryan (December 8, 2011). ["Fork Yeah! The Rise and Development of illumos"](https://www.slideshare.net/bcantrill/fork-yeah-the-rise-and-development-of-illumos). [SlideShare](./SlideShare). [Archived](https://web.archive.org/web/20130927190448/http://www.slideshare.net/bcantrill/fork-yeah-the-rise-and-development-of-illumos) from the original on September 27, 2013. Retrieved September 24, 2013.
10. [↑](./OpenZFS#cite_ref-10) ["illumos FAQs"](http://wiki.illumos.org/display/illumos/illumos+FAQs). *illumos.org*. [Archived](https://web.archive.org/web/20131224103149/http://wiki.illumos.org/display/illumos/illumos+FAQs) from the original on December 24, 2013. Retrieved September 24, 2013.
11. [↑](./OpenZFS#cite_ref-11) ["MacZFS: Official Site for the Free ZFS for Mac OS"](https://code.google.com/p/maczfs/). *code.google.com*. [Archived](https://web.archive.org/web/20140211021646/http://code.google.com/p/maczfs/) from the original on February 11, 2014. Retrieved March 2, 2014.
12. [↑](./OpenZFS#cite_ref-12) ["OpenZFS on OS X"](https://openzfsonosx.org/wiki/Main_Page). *openzfsonosx.org*. November 15, 2014. [Archived](https://web.archive.org/web/20141129042747/https://openzfsonosx.org/wiki/Main_Page) from the original on November 29, 2014. Retrieved November 23, 2014.
13. [↑](./OpenZFS#cite_ref-13) Corbet, Jonathan (March 29, 2013). ["ZFS on Linux 0.6.1"](https://lwn.net/Articles/545163/). [LWN.net](./LWN.net). [Archived](https://web.archive.org/web/20160730051437/http://lwn.net/Articles/545163/) from the original on July 30, 2016. Retrieved July 4, 2016.
14. [↑](./OpenZFS#cite_ref-lwn-567090_14-0) Corbet, Jonathan (September 17, 2013). ["The OpenZFS project launches"](https://lwn.net/Articles/567090/). [LWN.net](./LWN.net). [Archived](https://web.archive.org/web/20161011141200/https://lwn.net/Articles/567090/) from the original on October 11, 2016. Retrieved October 1, 2013.
15. [↑](./OpenZFS#cite_ref-openzfs-announcement_15-0) ["OpenZFS Announcement"](http://open-zfs.org/wiki/Announcement). *open-zfs.org*. September 17, 2013. [Archived](https://web.archive.org/web/20180402091425/http://open-zfs.org/wiki/Announcement) from the original on April 2, 2018. Retrieved September 19, 2013.
16. [↑](./OpenZFS#cite_ref-16) ["Release OpenZFS 2.0.0 · openzfs/zfs"](https://github.com/openzfs/zfs/releases/tag/zfs-2.0.0). *GitHub*. Retrieved March 11, 2024.
17. [↑](./OpenZFS#cite_ref-17) Moglen, Eben; Choudharyl, Mishi (February 26, 2016). ["The Linux Kernel, CDDL and Related Issues"](https://www.softwarefreedom.org/resources/2016/linux-kernel-cddl.html). *softwarefreedom.org*. [Archived](https://web.archive.org/web/20160401205722/http://softwarefreedom.org/resources/2016/linux-kernel-cddl.html) from the original on April 1, 2016. Retrieved March 30, 2016.
18. [↑](./OpenZFS#cite_ref-18) Kuhn, Bradley M.; Sandler, Karen M. (February 25, 2016). ["GPL Violations Related to Combining ZFS and Linux"](https://sfconservancy.org/blog/2016/feb/25/zfs-and-linux/). *sfconservancy.org*. [Archived](https://web.archive.org/web/20160403231244/http://sfconservancy.org/blog/2016/feb/25/zfs-and-linux/) from the original on April 3, 2016. Retrieved March 30, 2016.
19. [↑](./OpenZFS#cite_ref-19) Bottomley, James (February 23, 2016). ["Are GPLv2 and CDDL incompatible?"](http://blog.hansenpartnership.com/are-gplv2-and-cddl-incompatible/). *hansenpartnership.com*. [Archived](https://web.archive.org/web/20160301044941/http://blog.hansenpartnership.com/are-gplv2-and-cddl-incompatible/) from the original on March 1, 2016. Retrieved July 3, 2016.
20. [↑](./OpenZFS#cite_ref-20) Paul, Ryan (June 9, 2010). ["Uptake of native Linux ZFS port hampered by license conflict"](https://arstechnica.com/information-technology/2010/06/uptake-of-native-linux-zfs-port-hampered-by-license-conflict/). *[Ars Technica](./Ars_Technica)*. [Archived](https://web.archive.org/web/20140714170107/http://arstechnica.com/information-technology/2010/06/uptake-of-native-linux-zfs-port-hampered-by-license-conflict/) from the original on July 14, 2014. Retrieved July 1, 2014.
21. [1](./OpenZFS#cite_ref-:0_21-0) [2](./OpenZFS#cite_ref-:0_21-1) Sharwood, Simon (April 21, 2016). ["Ubuntu 16.04 LTS arrives today complete with forbidden ZFS"](https://www.theregister.co.uk/2016/04/21/ubuntu_16_04_lts_launched/). *[The Register](./The_Register)*. [Archived](https://web.archive.org/web/20160708231237/http://www.theregister.co.uk/2016/04/21/ubuntu_16_04_lts_launched) from the original on July 8, 2016. Retrieved July 3, 2016.
22. [↑](./OpenZFS#cite_ref-22) Larabel, Michael (October 6, 2015). ["Ubuntu is Planning to Make The ZFS Filesystem a "Standard" Offering"](https://www.phoronix.com/scan.php?page=news_item&px=Ubuntu-ZFS-Standard-Plans). [Phoronix](./Phoronix). [Archived](https://web.archive.org/web/20160630114359/https://www.phoronix.com/scan.php?page=news_item&px=Ubuntu-ZFS-Standard-Plans) from the original on June 30, 2016. Retrieved July 3, 2016.
23. [↑](./OpenZFS#cite_ref-23) ["Apple: Leopard offers limited ZFS read-only"](http://www.macnn.com/articles/07/06/12/leopard.uses.hfs.not.zfs/). *MacNN*. June 12, 2007. [Archived](https://web.archive.org/web/20070619171212/http://www.macnn.com/articles/07/06/12/leopard.uses.hfs.not.zfs/) from the original on June 19, 2007. Retrieved June 23, 2007.
24. [↑](./OpenZFS#cite_ref-24) ["Apple delivers ZFS Read/Write Developer Preview 1.1 for Leopard"](https://arstechnica.com/journals/apple.ars/2007/10/07/apple-delivers-zfs-readwrite-developer-preview-1-1-for-leopard). *Ars Technica*. October 7, 2007. [Archived](https://web.archive.org/web/20071010082428/http://arstechnica.com/journals/apple.ars/2007/10/07/apple-delivers-zfs-readwrite-developer-preview-1-1-for-leopard) from the original on October 10, 2007. Retrieved October 7, 2007.
25. [↑](./OpenZFS#cite_ref-25) Kristo, Ché (November 18, 2007). ["ZFS Beta Seed v1.1 will not install on Leopard.1 (10.5.1) " ideas are free"](https://web.archive.org/web/20071224112557/http://synesius.wordpress.com/2007/11/18/zfs-beta-seed-v11-will-not-install-on-leopard1-1051/). Archived from [the original](http://synesius.wordpress.com/2007/11/18/zfs-beta-seed-v11-will-not-install-on-leopard1-1051/) on December 24, 2007. Retrieved December 30, 2007.
26. [↑](./OpenZFS#cite_ref-26) ["ZFS"](https://web.archive.org/web/20091102050530/http://zfs.macosforge.org/). November 2, 2009. Archived from [the original](http://zfs.macosforge.org/) on November 2, 2009. Retrieved September 19, 2024.
27. [↑](./OpenZFS#cite_ref-27) [http://alblue.blogspot.com/2008/11/zfs-119-on-mac-os-x.html](http://alblue.blogspot.com/2008/11/zfs-119-on-mac-os-x.html) [Archived](https://web.archive.org/web/20120220074105/http://alblue.blogspot.com/2008/11/zfs-119-on-mac-os-x.html) February 20, 2012, at the [Wayback Machine](./Wayback_Machine) |title=Alblue.blogspot.com
28. [↑](./OpenZFS#cite_ref-28) ["Snow Leopard (archive.org cache)"](https://web.archive.org/web/20080721031014/http://www.apple.com/server/macosx/snowleopard/). July 21, 2008. Archived from [the original](https://www.apple.com/server/macosx/snowleopard/) on July 21, 2008.
29. [↑](./OpenZFS#cite_ref-29) ["Snow Leopard"](https://www.apple.com/server/macosx/snowleopard/). June 9, 2009. [Archived](https://web.archive.org/web/20080721031014/http://www.apple.com/server/macosx/snowleopard/) from the original on July 21, 2008. Retrieved June 10, 2008.
30. [↑](./OpenZFS#cite_ref-30) ["zfs-macos | Google Groups"](https://groups.google.com/group/zfs-macos/?pli=1). [Archived](https://web.archive.org/web/20121108014127/http://groups.google.com/group/zfs-macos/?pli=1) from the original on November 8, 2012. Retrieved November 4, 2011.
31. [↑](./OpenZFS#cite_ref-code.google.com_31-0) ["maczfs – Official Site for the Free ZFS for Mac OS – Google Project Hosting"](http://maczfs.org/). [Archived](https://web.archive.org/web/20160729211102/http://maczfs.org/) from the original on July 29, 2016. Retrieved July 30, 2012.
32. [↑](./OpenZFS#cite_ref-32) Sallings, Dustin (May 31, 2024), [*dustin/mac-zfs*](https://github.com/dustin/mac-zfs), retrieved September 19, 2024
33. [↑](./OpenZFS#cite_ref-33) [Frequently Asked Questions page](https://code.google.com/p/maczfs/wiki/FAQ) [Archived](https://web.archive.org/web/20150319135415/http://code.google.com/p/maczfs/wiki/FAQ) March 19, 2015, at the [Wayback Machine](./Wayback_Machine) on code.google.com/p/maczfs
34. [↑](./OpenZFS#cite_ref-34) ["Google Code Archive - Long-term storage for Google Code Project Hosting"](https://code.google.com/archive/p/maczfs/). *code.google.com*. Retrieved September 19, 2024.
35. [↑](./OpenZFS#cite_ref-OI-151a5_release_notes_35-0) ["oi_151a_prestable5 Release Notes"](http://wiki.openindiana.org/oi/oi_151a_prestable5+Release+Notes). [Archived](https://web.archive.org/web/20160517204530/http://wiki.openindiana.org/oi/oi_151a_prestable5+Release+Notes) from the original on May 17, 2016. Retrieved May 23, 2016.
36. [↑](./OpenZFS#cite_ref-istgt_36-0) ["Upgrading from OpenSolaris"](http://wiki.openindiana.org/oi/Upgrading+from+OpenSolaris). [Archived](https://web.archive.org/web/20110926154800/http://wiki.openindiana.org/oi/Upgrading+from+OpenSolaris) from the original on September 26, 2011. Retrieved September 24, 2011.
37. [↑](./OpenZFS#cite_ref-37) ["OpenZFS on OS X"](https://openzfsonosx.org/wiki/OpenZFS_on_OS_X). *openzfsonosx.org*. September 29, 2014. [Archived](https://web.archive.org/web/20141129042839/https://openzfsonosx.org/wiki/OpenZFS_on_OS_X) from the original on November 29, 2014. Retrieved November 23, 2014.
38. [1](./OpenZFS#cite_ref-zpool-features_38-0) [2](./OpenZFS#cite_ref-zpool-features_38-1) ["Features – OpenZFS – Feature flags"](http://open-zfs.org/wiki/Features#Feature_Flags). OpenZFS. [Archived](https://web.archive.org/web/20130922041052/http://www.open-zfs.org/wiki/Features#Feature_Flags) from the original on September 22, 2013. Retrieved September 22, 2013.
39. [↑](./OpenZFS#cite_ref-39) ["MacZFS: Official Site for the Free ZFS for Mac OS"](https://code.google.com/p/maczfs/). *code.google.com*. [MacZFS](./MacZFS). [Archived](https://web.archive.org/web/20150319165431/http://code.google.com/p/maczfs/) from the original on March 19, 2015. Retrieved March 2, 2014.
40. [↑](./OpenZFS#cite_ref-40) ["ZEVO Wiki Site/ZFS Pool And Filesystem Versions"](http://zevo.getgreenbytes.com/wiki/pmwiki.php?n=Site.ZFSPoolAndFilesystemVersions). GreenBytes, Inc. September 15, 2012. [Archived](https://web.archive.org/web/20140810064726/http://zevo.getgreenbytes.com/wiki/pmwiki.php?n=Site.ZFSPoolAndFilesystemVersions) from the original on August 10, 2014. Retrieved September 22, 2013.
41. [↑](./OpenZFS#cite_ref-dfly_41-0) ["Github zfs-port branch"](https://github.com/victoredwardocallaghan/DragonFlyBSD/tree/zfs-port). *[GitHub](./GitHub)*. September 23, 2014. [Archived](https://web.archive.org/web/20160109150222/https://github.com/victoredwardocallaghan/DragonFlyBSD/tree/zfs-port) from the original on January 9, 2016. Retrieved October 5, 2014.
42. [↑](./OpenZFS#cite_ref-netbsd_42-0) ["NetBSD Google Summer of Code projects: ZFS"](http://www.netbsd.org/contrib/soc-projects.html#zfs-port). [Archived](https://web.archive.org/web/20071011015826/http://netbsd.org/contrib/soc-projects.html#zfs-port) from the original on October 11, 2007. Retrieved September 5, 2007.
43. [↑](./OpenZFS#cite_ref-fbsd_43-0) Dawidek, Paweł (April 6, 2007). ["ZFS committed to the FreeBSD base"](http://lists.freebsd.org/pipermail/freebsd-current/2007-April/070544.html). [Archived](https://web.archive.org/web/20120622050730/http://lists.freebsd.org/pipermail/freebsd-current/2007-April/070544.html) from the original on June 22, 2012. Retrieved April 6, 2007.
44. [↑](./OpenZFS#cite_ref-fbsd-zfs13_44-0) ["Revision 192498"](http://svn.freebsd.org/viewvc/base?view=revision&revision=192498). May 20, 2009. Retrieved May 22, 2009.
45. [↑](./OpenZFS#cite_ref-fbsd-zfs13voras_45-0) ["ZFS v13 in 7-STABLE"](https://web.archive.org/web/20090527011500/http://ivoras.sharanet.org/blog/tree/2009-05-21.zfs-v13-in-7-stable.html). May 21, 2009. Archived from [the original](http://ivoras.sharanet.org/blog/tree/2009-05-21.zfs-v13-in-7-stable.html) on May 27, 2009. Retrieved May 22, 2009.
46. [↑](./OpenZFS#cite_ref-autogenerated1_46-0) ["iSCSI target for FreeBSD"](https://web.archive.org/web/20110714005700/http://shell.peach.ne.jp/aoyama/). Archived from [the original](http://shell.peach.ne.jp/aoyama/) on July 14, 2011. Retrieved August 6, 2011.
47. [↑](./OpenZFS#cite_ref-47) ["FreeBSD 13.0-RELEASE Release Notes"](https://www.freebsd.org/releases/13.0R/relnotes/). *FreeBSD*. The FreeBSD Project. Retrieved July 10, 2021.
48. [↑](./OpenZFS#cite_ref-48) Macy, Matt (August 25, 2020). ["commit 9e5787d2284e187abb5b654d924394a65772e004 Merge OpenZFS support in to HEAD"](https://cgit.freebsd.org/src/commit/?id=9e5787d2284e). *src - FreeBSD source tree*. Retrieved July 10, 2021.
49. [↑](./OpenZFS#cite_ref-trueos-defunct_49-0) ["TrueOS discontinuation"](https://www.truenas.com/trueos-discontinuation/). *trueos.com*. August 19, 2020. [Archived](https://web.archive.org/web/20210124125445/https://www.truenas.com/trueos-discontinuation/) from the original on January 24, 2021. Retrieved April 9, 2021.
50. [↑](./OpenZFS#cite_ref-50) ["TrueNAS 12.0 is Released!"](https://www.ixsystems.com/blog/truenas-12-0-is-released/). October 21, 2020. Retrieved April 9, 2021.
51. [↑](./OpenZFS#cite_ref-51) ["NAS4Free: Features"](http://www.nas4free.org/index.php?id=3). [Archived](https://web.archive.org/web/20150206032723/http://www.nas4free.org/index.php?id=3) from the original on February 6, 2015. Retrieved January 13, 2015.
52. [↑](./OpenZFS#cite_ref-52) ["Debian GNU/kFreeBSD FAQ"](http://wiki.debian.org/Debian_GNU/kFreeBSD_FAQ#Q._Is_there_ZFS_support.3F). *Is there ZFS support?*. [Archived](https://web.archive.org/web/20130927182446/https://wiki.debian.org/Debian_GNU/kFreeBSD_FAQ#Q._Is_there_ZFS_support.3F) from the original on September 27, 2013. Retrieved September 24, 2013.
53. [↑](./OpenZFS#cite_ref-53) ["Debian GNU/kFreeBSD FAQ"](https://wiki.debian.org/Debian_GNU/kFreeBSD_FAQ#Q._Can_I_use_ZFS_as_root_or_.2Fboot_file_system.3F). *Can I use ZFS as root or /boot file system?*. [Archived](https://web.archive.org/web/20190118051541/https://wiki.debian.org/Debian_GNU/kFreeBSD_FAQ#Q._Can_I_use_ZFS_as_root_or_.2Fboot_file_system.3F) from the original on January 18, 2019. Retrieved September 24, 2013.
54. [↑](./OpenZFS#cite_ref-54) ["Debian GNU/kFreeBSD FAQ"](https://wiki.debian.org/Debian_GNU/kFreeBSD_FAQ#Q._What_grub_commands_are_necessary_to_boot_Debian.2FkFreeBSD_from_a_zfs_root.3F). *What grub commands are necessary to boot Debian/kFreeBSD from a zfs root?*. [Archived](https://web.archive.org/web/20190118051541/https://wiki.debian.org/Debian_GNU/kFreeBSD_FAQ#Q._What_grub_commands_are_necessary_to_boot_Debian.2FkFreeBSD_from_a_zfs_root.3F) from the original on January 18, 2019. Retrieved September 24, 2013.
55. [↑](./OpenZFS#cite_ref-55) Larabel, Michael (September 10, 2010). ["Debian GNU/kFreeBSD Becomes More Interesting"](https://www.phoronix.com/scan.php?page=news_item&px=ODU4Ng). [Phoronix](./Phoronix). [Archived](https://web.archive.org/web/20161129111815/https://www.phoronix.com/scan.php?page=news_item&px=ODU4Ng) from the original on November 29, 2016. Retrieved September 24, 2013.
56. [↑](./OpenZFS#cite_ref-56) Moglen, Eben; Choudharyl, Mishi (February 26, 2016). ["The Linux Kernel, CDDL and Related Issues"](https://www.softwarefreedom.org/resources/2016/linux-kernel-cddl.html). *softwarefreedom.org*. [Archived](https://web.archive.org/web/20160401205722/http://softwarefreedom.org/resources/2016/linux-kernel-cddl.html) from the original on April 1, 2016. Retrieved March 30, 2016.
57. [↑](./OpenZFS#cite_ref-57) Kuhn, Bradley M.; Sandler, Karen M. (February 25, 2016). ["GPL Violations Related to Combining ZFS and Linux"](https://sfconservancy.org/blog/2016/feb/25/zfs-and-linux/). *sfconservancy.org*. [Archived](https://web.archive.org/web/20160403231244/http://sfconservancy.org/blog/2016/feb/25/zfs-and-linux/) from the original on April 3, 2016. Retrieved March 30, 2016.
58. [↑](./OpenZFS#cite_ref-58) Corbet, Jonathan (June 12, 2007). ["Linus on GPLv3 and ZFS"](https://lwn.net/Articles/237905/). Lwn.net. [Archived](https://web.archive.org/web/20110723194715/http://lwn.net/Articles/237905/) from the original on July 23, 2011. Retrieved November 4, 2011.
59. [↑](./OpenZFS#cite_ref-59) Paul, Ryan (June 9, 2010). ["Uptake of native Linux ZFS port hampered by license conflict"](https://arstechnica.com/information-technology/2010/06/uptake-of-native-linux-zfs-port-hampered-by-license-conflict/). Ars Technica. [Archived](https://web.archive.org/web/20140714170107/http://arstechnica.com/information-technology/2010/06/uptake-of-native-linux-zfs-port-hampered-by-license-conflict/) from the original on July 14, 2014. Retrieved July 1, 2014.
60. [↑](./OpenZFS#cite_ref-FUSE_60-0) Rajgarhia, Aditya & Gehani, Ashish (November 23, 2012). ["Performance and Extension of User Space File Systems"](http://www.csl.sri.com/users/gehani/papers/SAC-2010.FUSE.pdf) (PDF). [Archived](https://web.archive.org/web/20140907030210/http://www.csl.sri.com/users/gehani/papers/SAC-2010.FUSE.pdf) (PDF) from the original on September 7, 2014. Retrieved November 23, 2012.
61. [↑](./OpenZFS#cite_ref-61) Behlendorf, Brian (May 28, 2013). ["spl/zfs-0.6.1 released"](https://groups.google.com/a/zfsonlinux.org/forum/?fromgroups=#!topic/zfs-announce/ZXADhyOwFfA). *zfs-announce mailing list*. [Archived](https://web.archive.org/web/20130608034401/https://groups.google.com/a/zfsonlinux.org/forum/?fromgroups=#!topic/zfs-announce/ZXADhyOwFfA) from the original on June 8, 2013. Retrieved October 9, 2013.
62. [↑](./OpenZFS#cite_ref-62) ["ZFS on Linux"](http://zfsonlinux.org/). [Archived](https://web.archive.org/web/20190522092146/https://zfsonlinux.org/) from the original on May 22, 2019. Retrieved August 29, 2013.
63. [↑](./OpenZFS#cite_ref-LinuxCon_2013:_OpenZFS_63-0) Ahrens, Matt; Behlendorf, Brian (September 17, 2013). ["LinuxCon 2013: OpenZFS"](https://events.static.linuxfound.org/sites/events/files/slides/OpenZFS%20-%20LinuxCon_0.pdf) (PDF). *linuxfoundation.org*. [Archived](https://web.archive.org/web/20200607152335/https://events.static.linuxfound.org/sites/events/files/slides/OpenZFS%20-%20LinuxCon_0.pdf) (PDF) from the original on June 7, 2020. Retrieved November 13, 2013.
64. [↑](./OpenZFS#cite_ref-64) ["ZFS on Linux"](http://zfsonlinux.org). *zfsonlinux.org*. [Archived](https://web.archive.org/web/20190522092146/https://zfsonlinux.org/) from the original on May 22, 2019. Retrieved August 13, 2014.
65. [↑](./OpenZFS#cite_ref-linuxforums_65-0) Darshin (August 24, 2010). ["ZFS Port to Linux (all versions)"](https://web.archive.org/web/20120311011657/http://linuxforums.co.uk/viewtopic.php?f=16&t=3). Archived from [the original](http://www.linuxforums.co.uk/viewtopic.php?f=16&t=3) on March 11, 2012. Retrieved August 31, 2010.
66. [↑](./OpenZFS#cite_ref-66) ["Where can I get the ZFS for Linux source code?"](https://web.archive.org/web/20111008110651/http://www.stec-inc.com/press/kqi/supportfaq.php). Archived from [the original](http://www.stec-inc.com/press/kqi/supportfaq.php) on October 8, 2011. Retrieved August 29, 2013.
67. [↑](./OpenZFS#cite_ref-phoronixbenchmark_67-0) Phoronix (November 22, 2010). ["Running The Native ZFS Linux Kernel Module, Plus Benchmarks"](https://www.phoronix.com/scan.php?page=article&item=linux_kqzfs_benchmarks&num=1). [Archived](https://web.archive.org/web/20101211202554/http://www.phoronix.com/scan.php?page=article&item=linux_kqzfs_benchmarks&num=1) from the original on December 11, 2010. Retrieved December 7, 2010.
68. [1](./OpenZFS#cite_ref-phoronix_68-0) [2](./OpenZFS#cite_ref-phoronix_68-1) ["KQ ZFS Linux Is No Longer Actively Being Worked On"](https://www.phoronix.com/scan.php?page=news_item&px=OTU1NQ). June 10, 2011. [Archived](https://web.archive.org/web/20161129051936/https://www.phoronix.com/scan.php?page=news_item&px=OTU1NQ) from the original on November 29, 2016. Retrieved September 14, 2016.
69. [↑](./OpenZFS#cite_ref-69) ["zfs-linux / zfs"](https://github.com/zfs-linux/zfs). *[GitHub](./GitHub)*. [Archived](https://web.archive.org/web/20110516114938/https://github.com/zfs-linux/zfs) from the original on May 16, 2011. Retrieved September 15, 2011.
70. [↑](./OpenZFS#cite_ref-70) ["ZFS – Gentoo documentation"](http://wiki.gentoo.org/wiki/ZFS). *gentoo.org*. [Archived](https://web.archive.org/web/20131003040801/http://wiki.gentoo.org/wiki/ZFS) from the original on October 3, 2013. Retrieved October 9, 2013.
71. [↑](./OpenZFS#cite_ref-71) ["ZFS root"](http://slackwiki.com/ZFS_root). *Slackware ZFS root*. SlackWiki.com. [Archived](https://web.archive.org/web/20140814082700/http://slackwiki.com/ZFS_root) from the original on August 14, 2014. Retrieved August 13, 2014.
72. [↑](./OpenZFS#cite_ref-72) ["ZFS root (builtin)"](http://slackwiki.com/ZFS_root_%28builtin%29). *Slackware ZFS root (builtin)*. SlackWiki.com. [Archived](https://web.archive.org/web/20140814232836/http://slackwiki.com/ZFS_root_%28builtin%29) from the original on August 14, 2014. Retrieved August 13, 2014.
73. [↑](./OpenZFS#cite_ref-73) [Michael Larabel](./Michael_Larabel) (October 6, 2015). ["Ubuntu Is Planning To Make The ZFS File-System A "Standard" Offering"](https://www.phoronix.com/scan.php?page=news_item&px=Ubuntu-ZFS-Standard-Plans). [Phoronix](./Phoronix). [Archived](https://web.archive.org/web/20160630114359/https://www.phoronix.com/scan.php?page=news_item&px=Ubuntu-ZFS-Standard-Plans) from the original on June 30, 2016. Retrieved June 30, 2016.
74. [↑](./OpenZFS#cite_ref-74) Dustin Kirkland (February 18, 2016). ["ZFS Licensing and Linux"](https://insights.ubuntu.com/2016/02/18/zfs-licensing-and-linux/). *Ubuntu Insights*. Canonical. [Archived](https://web.archive.org/web/20160729004422/http://insights.ubuntu.com/2016/02/18/zfs-licensing-and-linux/) from the original on July 29, 2016. Retrieved June 30, 2016.
75. [↑](./OpenZFS#cite_ref-75) [Moglen, Eben](./Eben_Moglen); Choudhary, Mishi (February 26, 2016). ["The Linux Kernel, CDDL and Related Issues"](https://softwarefreedom.org/resources/2016/linux-kernel-cddl.html). [Archived](https://web.archive.org/web/20160714132240/http://softwarefreedom.org/resources/2016/linux-kernel-cddl.html) from the original on July 14, 2016. Retrieved June 30, 2016.
76. [↑](./OpenZFS#cite_ref-76) ["GPL Violations Related to Combining ZFS and Linux"](https://sfconservancy.org/blog/2016/feb/25/zfs-and-linux/). *Software Freedom Conservancy*. Retrieved September 19, 2024.
77. [↑](./OpenZFS#cite_ref-phoronix-Ubuntu16.04-ZFS_77-0) Larabel, Michael. ["Taking ZFS For A Test Drive On Ubuntu 16.04 LTS"](https://www.phoronix.com/scan.php?page=article&item=ubuntu-xenial-zfs&num=1). *phoronix*. Phoronix Media. [Archived](https://web.archive.org/web/20160919090252/http://www.phoronix.com/scan.php?page=article&item=ubuntu-xenial-zfs&num=1) from the original on September 19, 2016. Retrieved April 25, 2016.
78. [↑](./OpenZFS#cite_ref-78) ["Ubuntu ZFS support in 19.10: Introduction"](https://didrocks.fr/2019/08/06/ubuntu-zfs-support-in-19.10-introduction/). August 6, 2019. [Archived](https://web.archive.org/web/20191023090713/https://didrocks.fr/2019/08/06/ubuntu-zfs-support-in-19.10-introduction/) from the original on October 23, 2019. Retrieved October 23, 2019.
79. [↑](./OpenZFS#cite_ref-79) Salter, Jim (October 10, 2019). ["A detailed look at Ubuntu's new experimental ZFS installer"](https://arstechnica.com/information-technology/2019/10/a-detailed-look-at-ubuntus-new-experimental-zfs-installer/). *Ars Technica*. [Archived](https://web.archive.org/web/20191231181013/https://arstechnica.com/information-technology/2019/10/a-detailed-look-at-ubuntus-new-experimental-zfs-installer/) from the original on December 31, 2019. Retrieved January 14, 2020.
80. [↑](./OpenZFS#cite_ref-80) ["Software Status"](https://www.truenas.com/software-status/). *www.truenas.com*. August 8, 2022. Retrieved January 7, 2024.
81. [↑](./OpenZFS#cite_ref-81) ["25.04 (Fangtooth) Version Notes"](https://www.truenas.com/docs/scale/25.04/gettingstarted/scalereleasenotes/). *www.truenas.com*. May 31, 2025. Retrieved May 31, 2025.
82. [↑](./OpenZFS#cite_ref-82) ["zfs-win"](https://code.google.com/archive/p/zfs-win/source/default/commits). *[Google Search](./Google_Search)*. Google Code Archive. [Archived](https://web.archive.org/web/20161230213832/https://code.google.com/archive/p/zfs-win/source/default/commits) from the original on December 30, 2016. Retrieved December 11, 2017.
83. [↑](./OpenZFS#cite_ref-83) ["Open ZFS File-System Running On Windows"](https://www.phoronix.com/scan.php?page=news_item&px=OpenZFS-Windows). *[Phoronix](./Phoronix)*. [Archived](https://web.archive.org/web/20171211213532/https://www.phoronix.com/scan.php?page=news_item&px=OpenZFS-Windows) from the original on December 11, 2017. Retrieved December 11, 2017.
84. [↑](./OpenZFS#cite_ref-84) ["OpenZFS on Windows"](https://github.com/openzfsonwindows/ZFSin). *[GitHub](./GitHub)*. [Archived](https://web.archive.org/web/20171120033145/https://github.com/openzfsonwindows/ZFSin) from the original on November 20, 2017. Retrieved December 11, 2017.
85. [↑](./OpenZFS#cite_ref-85) [*openzfsonwindows/openzfs*](https://github.com/openzfsonwindows/openzfs), openzfsonwindows, October 13, 2024, retrieved October 15, 2024
86. [↑](./OpenZFS#cite_ref-86) ["Solaris ZFS Administration Guide, Appendix A ZFS Version Descriptions"](http://download.oracle.com/docs/cd/E19253-01/819-5461/appendixa-1/index.html). [Oracle Corporation](./Oracle_Corporation). 2010. [Archived](https://web.archive.org/web/20110406181614/http://download.oracle.com/docs/cd/E19253-01/819-5461/appendixa-1/index.html) from the original on April 6, 2011. Retrieved February 11, 2011.
87. [↑](./OpenZFS#cite_ref-87) ["Oracle Solaris ZFS Version Descriptions"](http://docs.oracle.com/cd/E26502_01/html/E29007/appendixa-1.html#scrolltoc). [Oracle Corporation](./Oracle_Corporation). [Archived](https://web.archive.org/web/20131007113906/http://docs.oracle.com/cd/E26502_01/html/E29007/appendixa-1.html#scrolltoc) from the original on October 7, 2013. Retrieved September 23, 2013.
88. [1](./OpenZFS#cite_ref-openzfs-feature-flags_88-0) [2](./OpenZFS#cite_ref-openzfs-feature-flags_88-1) [3](./OpenZFS#cite_ref-openzfs-feature-flags_88-2) [4](./OpenZFS#cite_ref-openzfs-feature-flags_88-3) [5](./OpenZFS#cite_ref-openzfs-feature-flags_88-4) [6](./OpenZFS#cite_ref-openzfs-feature-flags_88-5) [7](./OpenZFS#cite_ref-openzfs-feature-flags_88-6) [8](./OpenZFS#cite_ref-openzfs-feature-flags_88-7) Siden, Christopher (January 11, 2012). ["ZFS Feature Flags (Illumos Meetup)"](https://web.archive.org/web/20130403114800/http://blog.delphix.com/csiden/files/2012/01/ZFS_Feature_Flags.pdf) (PDF). *delphix.com*. Archived from [the original](http://blog.delphix.com/csiden/files/2012/01/ZFS_Feature_Flags.pdf) (PDF) on April 3, 2013. Retrieved July 4, 2016.
89. [↑](./OpenZFS#cite_ref-89) ["OpenZFS Features – Feature flags"](http://open-zfs.org/wiki/Features#Feature_Flags). *open-zfs.org*. [Archived](https://web.archive.org/web/20130922041052/http://www.open-zfs.org/wiki/Features#Feature_Flags) from the original on September 22, 2013. Retrieved September 23, 2013.
90. [↑](./OpenZFS#cite_ref-90) Siden, Christopher (January 2012). ["ZFS Feature Flags"](https://web.archive.org/web/20130403114800/http://blog.delphix.com/csiden/files/2012/01/ZFS_Feature_Flags.pdf) (PDF). [Illumos](./Illumos) Meetup. Delphix. p. 4. Archived from [the original](http://blog.delphix.com/csiden/files/2012/01/ZFS_Feature_Flags.pdf) (PDF) on April 3, 2013. Retrieved September 22, 2013.
91. [↑](./OpenZFS#cite_ref-91) ["/usr/src/uts/common/sys/fs/zfs.h (line 338)"](https://github.com/illumos/illumos-gate/blob/master/usr/src/uts/common/sys/fs/zfs.h#L338). illumos (GitHub). [Archived](https://web.archive.org/web/20160211205337/https://github.com/illumos/illumos-gate/blob/master/usr/src/uts/common/sys/fs/zfs.h#L338) from the original on February 11, 2016. Retrieved November 16, 2013.
92. [↑](./OpenZFS#cite_ref-92) ["/usr/src/uts/common/fs/zfs/zfeature.c (line 89)"](https://github.com/illumos/illumos-gate/blob/master/usr/src/uts/common/fs/zfs/zfeature.c#L89). illumos (GitHub). [Archived](https://web.archive.org/web/20160211205337/https://github.com/illumos/illumos-gate/blob/master/usr/src/uts/common/fs/zfs/zfeature.c#L89) from the original on February 11, 2016. Retrieved November 16, 2013.
93. [1](./OpenZFS#cite_ref-openzfs-pools-portable_93-0) [2](./OpenZFS#cite_ref-openzfs-pools-portable_93-1) ["OpenZFS FAQ: Are storage pools created by OpenZFS portable between operating systems?"](http://open-zfs.org/wiki/FAQ#Are_storage_pools_created_by_OpenZFS_portable_between_operating_systems.3F). *open-zfs.org*. September 26, 2013. [Archived](https://web.archive.org/web/20160103105216/http://open-zfs.org/wiki/FAQ#Are_storage_pools_created_by_OpenZFS_portable_between_operating_systems.3F) from the original on January 3, 2016. Retrieved October 30, 2015.
94. [↑](./OpenZFS#cite_ref-94) ["Feature Flags — OpenZFS documentation"](https://openzfs.github.io/openzfs-docs/Basic%20Concepts/Feature%20Flags.html). *openzfs.github.io*. Retrieved January 4, 2024.
95. [↑](./OpenZFS#cite_ref-95) ["Feature Flags – OpenZFS"](http://open-zfs.org/wiki/Feature_Flags#Feature_flags_implementation). *open-zfs.org*. [Archived](https://web.archive.org/web/20170829041828/http://open-zfs.org/wiki/Feature_Flags#Feature_flags_implementation) from the original on August 29, 2017. Retrieved August 28, 2017.
96. [1](./OpenZFS#cite_ref-jude-BSDCAN2019_96-0) [2](./OpenZFS#cite_ref-jude-BSDCAN2019_96-1) [3](./OpenZFS#cite_ref-jude-BSDCAN2019_96-2) [4](./OpenZFS#cite_ref-jude-BSDCAN2019_96-3) [5](./OpenZFS#cite_ref-jude-BSDCAN2019_96-4) [6](./OpenZFS#cite_ref-jude-BSDCAN2019_96-5) [7](./OpenZFS#cite_ref-jude-BSDCAN2019_96-6) [8](./OpenZFS#cite_ref-jude-BSDCAN2019_96-7) [9](./OpenZFS#cite_ref-jude-BSDCAN2019_96-8) [10](./OpenZFS#cite_ref-jude-BSDCAN2019_96-9) [11](./OpenZFS#cite_ref-jude-BSDCAN2019_96-10) [12](./OpenZFS#cite_ref-jude-BSDCAN2019_96-11) [13](./OpenZFS#cite_ref-jude-BSDCAN2019_96-12) [14](./OpenZFS#cite_ref-jude-BSDCAN2019_96-13) [15](./OpenZFS#cite_ref-jude-BSDCAN2019_96-14) [16](./OpenZFS#cite_ref-jude-BSDCAN2019_96-15) [17](./OpenZFS#cite_ref-jude-BSDCAN2019_96-16) [18](./OpenZFS#cite_ref-jude-BSDCAN2019_96-17) [19](./OpenZFS#cite_ref-jude-BSDCAN2019_96-18) [20](./OpenZFS#cite_ref-jude-BSDCAN2019_96-19) ["Archived copy"](https://papers.freebsd.org/2019/BSDCan/jude-The_Future_of_OpenZFS_and_FreeBSD.files/jude-The_Future_of_OpenZFS_and_FreeBSD.pdf) (PDF). [Archived](https://web.archive.org/web/20200806005715/https://papers.freebsd.org/2019/BSDCan/jude-The_Future_of_OpenZFS_and_FreeBSD.files/jude-The_Future_of_OpenZFS_and_FreeBSD.pdf) (PDF) from the original on August 6, 2020. Retrieved June 7, 2020.`{{cite web}}`:  CS1 maint: archived copy as title ([link](./Category:CS1_maint:_archived_copy_as_title))
97. [1](./OpenZFS#cite_ref-zfs2-github_97-0) [2](./OpenZFS#cite_ref-zfs2-github_97-1) [3](./OpenZFS#cite_ref-zfs2-github_97-2) [4](./OpenZFS#cite_ref-zfs2-github_97-3) [5](./OpenZFS#cite_ref-zfs2-github_97-4) [6](./OpenZFS#cite_ref-zfs2-github_97-5) [7](./OpenZFS#cite_ref-zfs2-github_97-6) [8](./OpenZFS#cite_ref-zfs2-github_97-7) [9](./OpenZFS#cite_ref-zfs2-github_97-8) [10](./OpenZFS#cite_ref-zfs2-github_97-9) [11](./OpenZFS#cite_ref-zfs2-github_97-10) [12](./OpenZFS#cite_ref-zfs2-github_97-11) [13](./OpenZFS#cite_ref-zfs2-github_97-12) [14](./OpenZFS#cite_ref-zfs2-github_97-13) [15](./OpenZFS#cite_ref-zfs2-github_97-14) [16](./OpenZFS#cite_ref-zfs2-github_97-15) [17](./OpenZFS#cite_ref-zfs2-github_97-16) [18](./OpenZFS#cite_ref-zfs2-github_97-17) ["OpenZFS 2.0 · openzfs/ZFS"](https://github.com/openzfs/zfs/projects/25). *[GitHub](./GitHub)*. [Archived](https://web.archive.org/web/20200417085650/https://github.com/openzfs/zfs/projects/25) from the original on April 17, 2020. Retrieved June 7, 2020.
98. [↑](./OpenZFS#cite_ref-openzfs_leadership_notes_98-0) ["OpenZFS Leadership Team - Meeting Agenda and Notes"](https://docs.google.com/document/d/1w2jv2XVYFmBVvG1EGf-9A5HBVsjAYoLIFZAnWHhV-BM/edit). [Archived](https://web.archive.org/web/20200607152333/https://docs.google.com/document/d/1w2jv2XVYFmBVvG1EGf-9A5HBVsjAYoLIFZAnWHhV-BM/edit) from the original on June 7, 2020. Retrieved June 7, 2020.

 

## External links

   [![Wikimedia Commons logo](//upload.wikimedia.org/wikipedia/en/thumb/4/4a/Commons-logo.svg/40px-Commons-logo.svg.png)](./File:Commons-logo.svg) Wikimedia Commons has media related to [OpenZFS](https://commons.wikimedia.org/wiki/Category:OpenZFS).  
- [The OpenZFS Project](http://www.open-zfs.org/): [website](http://open-zfs.org/wiki/Main_Page) and list of [OpenZFS distributions](http://open-zfs.org/wiki/Distributions)
- FreeBSD: [Webpage](https://zfsonfreebsd.github.io/ZoF/) [GitHub](https://github.com/zfsonfreebsd/ZoF) [wiki](https://wiki.freebsd.org/ZFS)
- illumos: [Webpage](https://illumos.org/docs/about/features/) [GitHub](https://github.com/illumos/illumos-gate/)
- Linux: [Webpage](http://zfsonlinux.org/) [GitHub](https://github.com/zfsonlinux/zfs/)
- macOS: [Webpage](https://openzfsonosx.org/) [GitHub](https://github.com/openzfsonosx/) [Google](https://code.google.com/p/maczfs/)
- Windows: [Webpage](https://openzfsonwindows.org/) [GitHub](https://github.com/openzfsonwindows/)
- [OpenZFS Office Hours](https://www.youtube.com/watch?v=G2vIdPmsnTI&list=PLaUVvul17xSegxJjny2Gz85IgIyq9wu8n) on [YouTube](./YouTube_video_(identifier)), October 11, 2013, by Matt Ahrens
- [OpenZFS Device Removal](http://blog.delphix.com/alex/2015/01/15/openzfs-device-removal/) [Archived](https://web.archive.org/web/20150512214041/http://blog.delphix.com/alex/2015/01/15/openzfs-device-removal/) May 12, 2015, at the [Wayback Machine](./Wayback_Machine), January 15, 2015, by Alex Reece

 
| vteFile systems |
| --- |
| Comparison of file systemsdistributedUnix filesystem |
| Disk andnon-rotating | ADFSAdvFSAmiga FFSAmiga OFSAPFSAthFSbcachefsBFSBe File SystemBoot File SystemByte File System (z/VM)BtrfsCVFSCXFSDFSEFSEncrypting File SystemExtent File SystemEpisodeextext2ext3ext4FATexFATFiles-11FossilGPFSHAMMERHAMMER2HFS(Classic Mac OS)HFS(MVS)HFS+HPFSHTFSJFSLFSMFSMacintosh File SystemTiVo Media File SystemMINIXNetWare File SystemNext3NILFSNILFS2NSSNTFSOneFSOpenZFSPFSQFSQNX4FSReFSReiserFSReiser4RelianceReliance NitroRFSSFSShared File System (VM)Smart File SystemSNFSSoup (Apple)Tux3UBIFSUFS/UFS2soft updatesWAPBLVxFSWAFLXiafsXFSXsanzFS(z/OS)ZFS(Sun)Optical discHSFISO 9660ISO 13490UDFFlash memoryandSSDAPFSFATexFATTFATEROFSF2FSJFSNVFShost-sidewear levelingCHFSJFFSJFFS2LogFSNILFSNILFS2YAFFSUBIFSDistributed parallelBeeGFSCephCXFSGFS2Google File SystemOCFS2OrangeFSPVFSQFSXsanmore... | ADFSAdvFSAmiga FFSAmiga OFSAPFSAthFSbcachefsBFSBe File SystemBoot File SystemByte File System (z/VM)BtrfsCVFSCXFSDFSEFSEncrypting File SystemExtent File SystemEpisodeextext2ext3ext4FATexFATFiles-11FossilGPFSHAMMERHAMMER2HFS(Classic Mac OS)HFS(MVS)HFS+HPFSHTFSJFSLFSMFSMacintosh File SystemTiVo Media File SystemMINIXNetWare File SystemNext3NILFSNILFS2NSSNTFSOneFSOpenZFSPFSQFSQNX4FSReFSReiserFSReiser4RelianceReliance NitroRFSSFSShared File System (VM)Smart File SystemSNFSSoup (Apple)Tux3UBIFSUFS/UFS2soft updatesWAPBLVxFSWAFLXiafsXFSXsanzFS(z/OS)ZFS(Sun) | Optical disc | HSFISO 9660ISO 13490UDF | Flash memoryandSSD | APFSFATexFATTFATEROFSF2FSJFSNVFShost-sidewear levelingCHFSJFFSJFFS2LogFSNILFSNILFS2YAFFSUBIFS | host-sidewear leveling | CHFSJFFSJFFS2LogFSNILFSNILFS2YAFFSUBIFS | Distributed parallel | BeeGFSCephCXFSGFS2Google File SystemOCFS2OrangeFSPVFSQFSXsanmore... |
| ADFSAdvFSAmiga FFSAmiga OFSAPFSAthFSbcachefsBFSBe File SystemBoot File SystemByte File System (z/VM)BtrfsCVFSCXFSDFSEFSEncrypting File SystemExtent File SystemEpisodeextext2ext3ext4FATexFATFiles-11FossilGPFSHAMMERHAMMER2HFS(Classic Mac OS)HFS(MVS)HFS+HPFSHTFSJFSLFSMFSMacintosh File SystemTiVo Media File SystemMINIXNetWare File SystemNext3NILFSNILFS2NSSNTFSOneFSOpenZFSPFSQFSQNX4FSReFSReiserFSReiser4RelianceReliance NitroRFSSFSShared File System (VM)Smart File SystemSNFSSoup (Apple)Tux3UBIFSUFS/UFS2soft updatesWAPBLVxFSWAFLXiafsXFSXsanzFS(z/OS)ZFS(Sun) |
| Optical disc | HSFISO 9660ISO 13490UDF |
| Flash memoryandSSD | APFSFATexFATTFATEROFSF2FSJFSNVFShost-sidewear levelingCHFSJFFSJFFS2LogFSNILFSNILFS2YAFFSUBIFS | host-sidewear leveling | CHFSJFFSJFFS2LogFSNILFSNILFS2YAFFSUBIFS |
| host-sidewear leveling | CHFSJFFSJFFS2LogFSNILFSNILFS2YAFFSUBIFS |
| Distributed parallel | BeeGFSCephCXFSGFS2Google File SystemOCFS2OrangeFSPVFSQFSXsanmore... |
| NAS | 9PAFS(OpenAFS)AFPCodaDFSGoogle File SystemGPFSLustreNCPNFSPOHMELFSHadoopSMB (CIFS)SSHFSmore... |
| Specialized | AufsAXFSBoot File SystemCompact Disc File SystemcramfsDavfs2EROFSFTPFSFUSELnfsLTFSNOVAMVFSSquashFSUMSDOSOverlayFSUnionFSPseudoconfigfsdevfsdebugfskernfsprocfsspecfssysfstmpfsWinFSEncryptedeCryptfsEncFSEFSRubberhoseSSHFSZFS | AufsAXFSBoot File SystemCompact Disc File SystemcramfsDavfs2EROFSFTPFSFUSELnfsLTFSNOVAMVFSSquashFSUMSDOSOverlayFSUnionFS | Pseudo | configfsdevfsdebugfskernfsprocfsspecfssysfstmpfsWinFS | Encrypted | eCryptfsEncFSEFSRubberhoseSSHFSZFS |
| AufsAXFSBoot File SystemCompact Disc File SystemcramfsDavfs2EROFSFTPFSFUSELnfsLTFSNOVAMVFSSquashFSUMSDOSOverlayFSUnionFS |
| Pseudo | configfsdevfsdebugfskernfsprocfsspecfssysfstmpfsWinFS |
| Encrypted | eCryptfsEncFSEFSRubberhoseSSHFSZFS |
| Types | ClusteredGlobalGridSelf-certifyingFlashJournalingLog-structuredObjectRecord-orientedSemanticSteganographicSyntheticVersioning |
| Features | Case preservationCopy-on-writeData deduplicationData scrubbingExecute in placeExtentFile attributeExtended file attributesFile change logForkInodeLinksHardSymbolicAccess controlAccess-control listFilesystem-level encryptionPermissionsModesSticky bit | Case preservationCopy-on-writeData deduplicationData scrubbingExecute in placeExtentFile attributeExtended file attributesFile change logForkInodeLinksHardSymbolic | Access control | Access-control listFilesystem-level encryptionPermissionsModesSticky bit |
| Case preservationCopy-on-writeData deduplicationData scrubbingExecute in placeExtentFile attributeExtended file attributesFile change logForkInodeLinksHardSymbolic |
| Access control | Access-control listFilesystem-level encryptionPermissionsModesSticky bit |
| Interfaces | File managerFile system APIInstallable File SystemVirtual file system |
| Lists | CryptographicDefaultLog-structured |
| Layouts | Master Boot RecordGUID Partition TableApple Partition Map |

 
| vteUnixandUnix-likeoperating systemsandcompatibility layers |
| --- |
| ArchitectureFilesystemHistoryPhilosophySecurityShell |
| Operatingsystems | BSD386BSDFreeBSDNetBSDOpenBSDDragonFly BSDDarwinmacOSiOSaudioOSiPadOStvOSwatchOSbridgeOSDYNIXNeXTSTEPSunOSUltrixLinuxAndroidArchChromeOSDebianFedoraGentooRed HatSlackwareSUSEUbuntuOther distributionsSystem VA/UXAIXHP-UXIRIXOpenServerSolarisOpenSolarisIllumosTru64 UNIXUnixWareOtherCoherentDomain/OSGNUHurdLynxOSMinixMOSOSF/1QNXBlackBerry 10Research UnixSerenityOSXenixmore... | BSD | 386BSDFreeBSDNetBSDOpenBSDDragonFly BSDDarwinmacOSiOSaudioOSiPadOStvOSwatchOSbridgeOSDYNIXNeXTSTEPSunOSUltrix | Linux | AndroidArchChromeOSDebianFedoraGentooRed HatSlackwareSUSEUbuntuOther distributions | System V | A/UXAIXHP-UXIRIXOpenServerSolarisOpenSolarisIllumosTru64 UNIXUnixWare | Other | CoherentDomain/OSGNUHurdLynxOSMinixMOSOSF/1QNXBlackBerry 10Research UnixSerenityOSXenixmore... |
| BSD | 386BSDFreeBSDNetBSDOpenBSDDragonFly BSDDarwinmacOSiOSaudioOSiPadOStvOSwatchOSbridgeOSDYNIXNeXTSTEPSunOSUltrix |
| Linux | AndroidArchChromeOSDebianFedoraGentooRed HatSlackwareSUSEUbuntuOther distributions |
| System V | A/UXAIXHP-UXIRIXOpenServerSolarisOpenSolarisIllumosTru64 UNIXUnixWare |
| Other | CoherentDomain/OSGNUHurdLynxOSMinixMOSOSF/1QNXBlackBerry 10Research UnixSerenityOSXenixmore... |
| Compatibilitylayers | CygwinDarlingEuniceGNVInterixMachTenMicrosoft POSIX subsystemMKS ToolkitPASEP.I.P.S.PWS/VSE-AFUNIX System ServicesUserLAnd TechnologiesWindows Services for UNIXWindows Subsystem for Linux |
| Italicsindicate discontinued systems.CategoryCommons |

 
| vteTheFreeBSDProject |
| --- |
| FreeBSD | FreeBSD Core TeamFreeBSD Documentation LicenseFreeBSD FoundationFreeBSD PortsVersion History |
| Subsystems | SchedulingALTQULE schedulerVirtualisationchrootjailbhyveStorageGEOMraid5GBDEgeliLVM2vinumdisklabelfdiskUFSSoft updatesVFSZFSHighly Available STorageNetworking802.11 driversALTQBluetoothBPFIPFilteripfwNetgraphNDISpfCARPpfsyncSCTPOtherbusdmaDTraceOpenPAMOpenBSMportsnapkqueueKLDmousedsystat | Scheduling | ALTQULE scheduler | Virtualisation | chrootjailbhyve | Storage | GEOMraid5GBDEgeliLVM2vinumdisklabelfdiskUFSSoft updatesVFSZFSHighly Available STorage | Networking | 802.11 driversALTQBluetoothBPFIPFilteripfwNetgraphNDISpfCARPpfsyncSCTP | Other | busdmaDTraceOpenPAMOpenBSMportsnapkqueueKLDmousedsystat |
| Scheduling | ALTQULE scheduler |
| Virtualisation | chrootjailbhyve |
| Storage | GEOMraid5GBDEgeliLVM2vinumdisklabelfdiskUFSSoft updatesVFSZFSHighly Available STorage |
| Networking | 802.11 driversALTQBluetoothBPFIPFilteripfwNetgraphNDISpfCARPpfsyncSCTP |
| Other | busdmaDTraceOpenPAMOpenBSMportsnapkqueueKLDmousedsystat |
| People | Matthew DillonJordan HubbardPoul-Henning KampMike KarelsBen LaurieSam LefflerMarshall Kirk McKusickDiomidis SpinellisRobert WatsonDru Lavigne |
| Derivatives | open-sourceChimera LinuxXNUDarwinDesktopBSDDragonFly BSDFreeNASFreeSBIEGhostBSDMidnightBSDm0n0wallOPNsensepfSenseTrueOSGNU/kFreeBSDGentoo/FreeBSDXigmaNASproprietaryJunosmacOS,iOS,tvOS, andwatchOSNintendo Switch OSOpenServer 10PlayStation 3 OSPlayStation 4 OSPlayStation Vita OS | open-source | Chimera LinuxXNUDarwinDesktopBSDDragonFly BSDFreeNASFreeSBIEGhostBSDMidnightBSDm0n0wallOPNsensepfSenseTrueOSGNU/kFreeBSDGentoo/FreeBSDXigmaNAS | proprietary | JunosmacOS,iOS,tvOS, andwatchOSNintendo Switch OSOpenServer 10PlayStation 3 OSPlayStation 4 OSPlayStation Vita OS |
| open-source | Chimera LinuxXNUDarwinDesktopBSDDragonFly BSDFreeNASFreeSBIEGhostBSDMidnightBSDm0n0wallOPNsensepfSenseTrueOSGNU/kFreeBSDGentoo/FreeBSDXigmaNAS |
| proprietary | JunosmacOS,iOS,tvOS, andwatchOSNintendo Switch OSOpenServer 10PlayStation 3 OSPlayStation 4 OSPlayStation Vita OS |

 
| vtemacOS |
| --- |
| HistoryArchitectureBuilt-in appsServerSoftware |
| Versions | Mac OS XServer 1.0Public Beta10.0 Cheetah10.1 Puma10.2 Jaguar10.3 Panther10.4 Tiger10.5 Leopard10.6 Snow LeopardOS X10.7 Lion10.8 Mountain Lion10.9 Mavericks10.10 Yosemite10.11 El CapitanmacOS10.12 Sierra10.13 High Sierra10.14 Mojave10.15 Catalina11 Big Sur12 Monterey13 Ventura14 Sonoma15 Sequoia26 Tahoe27 Golden GatePredecessorsClassic Mac OSNeXTSTEPRhapsody | Mac OS X | Server 1.0Public Beta10.0 Cheetah10.1 Puma10.2 Jaguar10.3 Panther10.4 Tiger10.5 Leopard10.6 Snow Leopard | OS X | 10.7 Lion10.8 Mountain Lion10.9 Mavericks10.10 Yosemite10.11 El Capitan | macOS | 10.12 Sierra10.13 High Sierra10.14 Mojave10.15 Catalina11 Big Sur12 Monterey13 Ventura14 Sonoma15 Sequoia26 Tahoe27 Golden Gate | Predecessors | Classic Mac OSNeXTSTEPRhapsody |
| Mac OS X | Server 1.0Public Beta10.0 Cheetah10.1 Puma10.2 Jaguar10.3 Panther10.4 Tiger10.5 Leopard10.6 Snow Leopard |
| OS X | 10.7 Lion10.8 Mountain Lion10.9 Mavericks10.10 Yosemite10.11 El Capitan |
| macOS | 10.12 Sierra10.13 High Sierra10.14 Mojave10.15 Catalina11 Big Sur12 Monterey13 Ventura14 Sonoma15 Sequoia26 Tahoe27 Golden Gate |
| Predecessors | Classic Mac OSNeXTSTEPRhapsody |
| Applications | CoreapplicationsApp StoreAutomatorCalculatorCalendarContactsControl CenterDictionaryFaceTimeFinderGame CenterGrapherHomeMailMessagesNewsMusicNotesNotification CenterPodcastsPhoto BoothPhotosPreviewQuickTime PlayerRemindersSafariShortcutsSiriStickiesTextEditTime MachineDeveloperToolsXcodeInstrumentsFormerInterface BuilderDashcodeQuartz ComposerUtilitiesBoot Camp(deprecated)ColorSyncConfiguratorDisk UtilityFont BookKeychain AccessScript EditorSystem SettingsTerminalVoiceOverFormerDashboardFront RowiChatiPhotoiSynciTuneshistorySherlock | Coreapplications | App StoreAutomatorCalculatorCalendarContactsControl CenterDictionaryFaceTimeFinderGame CenterGrapherHomeMailMessagesNewsMusicNotesNotification CenterPodcastsPhoto BoothPhotosPreviewQuickTime PlayerRemindersSafariShortcutsSiriStickiesTextEditTime Machine | DeveloperTools | XcodeInstrumentsFormerInterface BuilderDashcodeQuartz Composer | Xcode | Instruments | Former | Interface BuilderDashcodeQuartz Composer | Utilities | Boot Camp(deprecated)ColorSyncConfiguratorDisk UtilityFont BookKeychain AccessScript EditorSystem SettingsTerminalVoiceOver | Former | DashboardFront RowiChatiPhotoiSynciTuneshistorySherlock |
| Coreapplications | App StoreAutomatorCalculatorCalendarContactsControl CenterDictionaryFaceTimeFinderGame CenterGrapherHomeMailMessagesNewsMusicNotesNotification CenterPodcastsPhoto BoothPhotosPreviewQuickTime PlayerRemindersSafariShortcutsSiriStickiesTextEditTime Machine |
| DeveloperTools | XcodeInstrumentsFormerInterface BuilderDashcodeQuartz Composer | Xcode | Instruments | Former | Interface BuilderDashcodeQuartz Composer |
| Xcode | Instruments |
| Former | Interface BuilderDashcodeQuartz Composer |
| Utilities | Boot Camp(deprecated)ColorSyncConfiguratorDisk UtilityFont BookKeychain AccessScript EditorSystem SettingsTerminalVoiceOver |
| Former | DashboardFront RowiChatiPhotoiSynciTuneshistorySherlock |
| Technologies,user interface | AirDropAppKitApple File SystemApple menuApple Push Notification serviceAppleScriptAquaAudio UnitsAVFoundationBonjourBundleCloudKitCocoaColorSyncCommand keyCore AnimationCore AudioCore DataCore FoundationCore ImageCore OpenGLCore TextCore VideoCover FlowCUPSDarwinDockFileVaultFontsFoundationGatekeeperGrand Central DispatchicnsiCloudKernel panicKeychainlaunchdLiquid GlassMach-OMenu extraMetalMission ControlNight ShiftOpenCLOption keyPreference PaneProperty listQuartzQuick LookRosettaSmart FoldersSpeakable itemsSpotlightStacksSystem Integrity ProtectionUniform Type IdentifierUniversal binaryWebKitXNUXQuartzDeprecatedHFS+DiscontinuedATSUIBootXBrushed metalCarbonClassic EnvironmentInkwellQuickTimeSpacesXgrid | AirDropAppKitApple File SystemApple menuApple Push Notification serviceAppleScriptAquaAudio UnitsAVFoundationBonjourBundleCloudKitCocoaColorSyncCommand keyCore AnimationCore AudioCore DataCore FoundationCore ImageCore OpenGLCore TextCore VideoCover FlowCUPSDarwinDockFileVaultFontsFoundationGatekeeperGrand Central DispatchicnsiCloudKernel panicKeychainlaunchdLiquid GlassMach-OMenu extraMetalMission ControlNight ShiftOpenCLOption keyPreference PaneProperty listQuartzQuick LookRosettaSmart FoldersSpeakable itemsSpotlightStacksSystem Integrity ProtectionUniform Type IdentifierUniversal binaryWebKitXNUXQuartz | Deprecated | HFS+ | Discontinued | ATSUIBootXBrushed metalCarbonClassic EnvironmentInkwellQuickTimeSpacesXgrid |
| AirDropAppKitApple File SystemApple menuApple Push Notification serviceAppleScriptAquaAudio UnitsAVFoundationBonjourBundleCloudKitCocoaColorSyncCommand keyCore AnimationCore AudioCore DataCore FoundationCore ImageCore OpenGLCore TextCore VideoCover FlowCUPSDarwinDockFileVaultFontsFoundationGatekeeperGrand Central DispatchicnsiCloudKernel panicKeychainlaunchdLiquid GlassMach-OMenu extraMetalMission ControlNight ShiftOpenCLOption keyPreference PaneProperty listQuartzQuick LookRosettaSmart FoldersSpeakable itemsSpotlightStacksSystem Integrity ProtectionUniform Type IdentifierUniversal binaryWebKitXNUXQuartz |
| Deprecated | HFS+ |
| Discontinued | ATSUIBootXBrushed metalCarbonClassic EnvironmentInkwellQuickTimeSpacesXgrid |
| Category |