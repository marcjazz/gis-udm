# Linux Installation and Package Management

## Preamble

- **Purpose**: To provide the essential basics for installing, managing startup, and maintaining software on Linux systems, which are fundamental skills for working on servers and in cloud environments.
- **Target audience**: Students in Cloud Computing.
- **Type of access**: Open.
- **Teaching mode**: Synchronous and Asynchronous.
- **prerequisites**: None

## Summary

This course provides a comprehensive exploration of the Linux operating system, from initial installation to advanced system maintenance. Students will master storage preparation using modern partitioning and Logical Volume Management (LVM), configure robust boot sequences with GRUB2, and manage software ecosystems across Debian and Red Hat families. Beyond basic setup, the course emphasizes practical, high-stakes skills including system recovery using `chroot`, transaction rollbacks with `dnf history`, and server hardening through firewall configuration and secure remote access.

## Course Sessions

1. [Session 1: The Linux Ecosystem and Installation Media](session1_introduction_and_ecosystem.md)
2. [Session 2: Disk Design, Partitioning, and Filesystems](session2_disk_design_and_filesystems.md)
3. [Session 3: The Linux Boot Process and GRUB2 Configuration](session3_boot_process_and_grub2.md)
4. [Session 4: Managing Shared Libraries and Resolving Dependencies](session4_shared_libraries.md)
5. [Session 5: Mastering Debian Package Management (DPKG/APT)](session5_debian_package_management.md)
6. [Session 6: Enterprise Package Management with RPM and DNF](session6_redhat_package_management.md)
7. [Session 7: Flexible Storage with Logical Volume Management (LVM)](session7_lvm.md)
8. [Session 8: Server Hardening and Emergency Recovery](session8_hardening_and_recovery.md)

## Glossary

- **Linux distribution**: A coherent set consisting of the Linux kernel, a package manager, and a set of tools and applications (e.g., Ubuntu, Debian, Fedora).
- **Kernel**: The core of the operating system that manages hardware resources, processes, memory, and peripherals.
- **CLI (Command Line Interface)**: Command line interface, used to administer the system without a graphical interface.
- **ISO**: Installation image of an operating system containing the files necessary for installation.
- **Bootloader**: Program loaded when the PC starts up, allowing the operating system to be launched.
- **GRUB (GRand Unified Bootloader)**: Bootloader widely used on Linux systems, configurable and multi-OS.
- **UEFI (Unified Extensible Firmware Interface)**: Modern replacement for BIOS, enabling advanced boot management and GPT disk support.
- **BIOS (Basic Input/Output System)**: Legacy firmware that manages hardware initialization at startup.
- **MBR (Master Boot Record)**: Old partitioning scheme limited to 2 TB and 4 primary partitions.
- **GPT (GUID Partition Table)**: Modern partitioning scheme supporting large disks and an unlimited number of partitions.
- **Partition**: Logical division of a disk used to store systems or data.
- **Swap**: Disk space used as "virtual memory" when physical RAM is exhausted.
- **Mount point**: Directory in which a partition or external disk is integrated into the Linux tree structure.
- **fstab**: File containing the configuration of file systems to be mounted automatically.
- **UUID**: Universally Unique Identifier. A unique string tied to a filesystem that ensures reliable mounting even if device names change.
- **Journaling**: A filesystem feature that records changes in a log before applying them, ensuring data integrity and fast recovery after a crash.
- **Shared library (.so)**: File containing code that can be reused by several programs simultaneously, avoiding duplication.
- **soname**: Shared Object Name. A field inside a shared library that indicates compatibility, allowing multiple versions of a library to coexist.
- **ldconfig**: Command that updates the shared library cache.
- **Dependency**: A package or file required for another program to function properly.
- **Package**: File containing a program, its data, and metadata, managed via a manager.
- **dpkg**: Low-level package manager on Debian/Ubuntu that allows you to install or remove .deb files.
- **apt (Advanced Package Tool)**: High-level manager that automatically resolves dependencies and manages repositories.
- **RPM (Red Hat Package Manager)**: Package format and low-level manager used on RHEL, CentOS, Fedora.
- **DNF (Dandified Yum)**: A modern replacement for YUM, faster and more reliable, featuring transaction history.
- **LVM (Logical Volume Management)**: A storage abstraction layer that allows for flexible disk management, including resizing volumes and spanning across multiple disks.
- **PV / VG / LV**: Physical Volume, Volume Group, and Logical Volume—the three layers of LVM architecture.
- **AppStream**: A Red Hat feature that provides multiple versions of software packages (modules) on the same OS release.
- **chroot**: Change root. A tool to change the apparent root directory for the current running process and its children, essential for system recovery.
- **initramfs**: Initial RAM filesystem. A minimal filesystem loaded into RAM that contains essential drivers needed to mount the real root filesystem.
- **ufw**: Uncomplicated Firewall. A user-friendly interface for managing firewall rules.
- **debootstrap**: A tool used to create a minimal Debian/Ubuntu base system from scratch without an installer.
- **Checksum (SHA256)**: Fingerprint used to verify the integrity of a downloaded ISO image.
- **GPG (GNU Privacy Guard)**: Encryption tool used to verify the authenticity of repositories and packages.
- **lsblk / fdisk / parted**: Commands for inspecting and managing disks and partitions.

## Learning objectives

By the end of this course, students should be able to:

1. **Master Linux System Installation & Storage Design**
   - Create and verify authentic installation media using checksums and GPG signatures.
   - Design complex storage layouts using MBR/GPT partitioning and Logical Volume Management (LVM).
   - Implement persistent storage configurations using UUIDs and `/etc/fstab`.
2. **Configure & Troubleshoot the Boot Process**
   - Trace the boot sequence from firmware (BIOS/UEFI) to `systemd`.
   - Customize GRUB2 boot parameters and recover from boot failures using emergency shells.
   - Utilize `initramfs` concepts to understand early-stage hardware initialization.
3. **Advanced Software & Library Management**
   - Diagnose and resolve missing shared library errors using `ldd` and `ldconfig`.
   - Manage the system-wide library cache and custom search paths.
   - Master both low-level (`dpkg`, `rpm`) and high-level (`apt`, `dnf`) package tools.
4. **Enterprise Maintenance & Security**
   - Perform system rollbacks using `dnf history`.
   - Implement server hardening via `ufw` and SSH configuration best practices.
   - Use `chroot` environments for advanced system recovery and repair from live media.

## Assessment

Teaching strategies adopted:
The specific assessment method is: Continuous assessment, Practical work, Final exam.

Standard school protocol:

- Continuous assessment (CC) accounts for 30% of the overall mark, broken down as follows: (Participation in tutorials 20%, Completion of activities 20%, Attendance/presence in class 20%, Completion of practical work 40%)
- The written exam accounts for 70%.

## CHAPTER 1 - Introduction to the Linux Ecosystem

### 1.1. Philosophy and Foundations

- Kernel vs. OS (GNU/Linux)
- Open Source & GPL freedoms
- CLI-first approach: Remote management, automation, and reproducibility

### 1.2. Distribution Families

- Debian Family (Debian, Ubuntu)
- Red Hat Family (RHEL, Fedora, AlmaLinux)
- Independent and Rolling Release models
- Choosing a distribution based on stability vs. modernity

### 1.3. Preparing Installation Media

- ISO image integrity (SHA256 checksums)
- Authenticity verification with GPG signatures
- Creating bootable media using `dd` and GUI tools

## CHAPTER 2 — Disk Design and Filesystems

### 2.1. Advanced Partitioning

- MBR vs. GPT: Capacity limits and redundancy
- Protective MBR and GPT headers
- Inspection tools: `lsblk`, `fdisk`, `parted`

### 2.2. Linux Filesystems and Journaling

- Ext4, XFS, and Btrfs (Copy-on-Write and Snapshots)
- The role of Journaling in data integrity
- Swap space and virtual memory

### 2.3. The Filesystem Hierarchy Standard (FHS)

- Role of major directories (`/etc`, `/var`, `/boot`, `/usr`, `/dev`)
- Root home vs. user home

### 2.4. Mounting and Persistence

- Anatomy of `/etc/fstab`
- The critical role of UUIDs in unpredictable cloud environments
- Mount options for performance and security

## CHAPTER 3 - Installation and management of bootloaders

### 3.1. The Linux Boot Chain

- 4-Phase boot process: Firmware -> GRUB2 -> Kernel/Initramfs -> Systemd
- BIOS vs. UEFI and Secure Boot
- The role of `initramfs` in early hardware initialization

### 3.2. GRUB2 Configuration

- The golden rule: Never edit `grub.cfg`
- Customizing `/etc/default/grub`
- Updating GRUB on Debian vs. Red Hat systems

### 3.3. Boot Troubleshooting

- Emergency password reset via `init=/bin/bash`
- Working with the GRUB Rescue Shell (`grub>`)
- Identifying partitions from the boot shell

## CHAPTER 4 — Shared Library Management

### 4.1. Linking Fundamentals

- Static vs. Dynamic linking: Pros, cons, and memory usage
- Shared Object naming and the `soname` compatibility mechanism

### 4.2. Library Cache and Search Paths

- The dynamic linker (`ld.so`)
- Managing `/etc/ld.so.conf.d/` for custom applications
- Rebuilding the cache with `ldconfig`

### 4.3. Troubleshooting Dependencies

- Inspecting binaries with `ldd` and `readelf`
- Resolving "not found" errors for custom libraries

## CHAPTER 5 — Package management in Debian and derivatives

### 5.1. Low-Level Management with `dpkg`

- Installing, removing, and purging packages
- System inspection: `dpkg -l`, `-S`, `-L`
- The fatal flaw: Lack of automatic dependency resolution

### 5.2. Advanced `apt` Operations

- The update/install workflow
- Full-upgrades vs. standard upgrades
- Repository management in `sources.list`

### 5.3. Security and Maintenance

- Modern GPG key management in `trusted.gpg.d`
- Repairing broken states with `apt --fix-broken install`
- Housekeeping: `autoremove` and `clean`

## CHAPTER 6 - Package management in Red Hat and derivatives

### 6.1. Low-Level Management with `rpm`

- RPM flags: `-ivh`, `-e`, `-qa`, `-V`
- Verifying package integrity against the RPM database

### 6.2. Modern Management with `dnf`

- Automatic metadata refresh
- Enterprise feature: `dnf history` for transactions and rollbacks (undo)
- Modularity and AppStreams for multiple software versions

### 6.3. Repository Configuration

- Anatomy of `.repo` files
- Essential repositories: The role of EPEL

## CHAPTER 7 - Logical Volume Management (LVM)

### 7.1. LVM Architecture

- The abstraction layers: Physical Volumes (PV), Volume Groups (VG), Logical Volumes (LV)
- The Brick and Wall analogy

### 7.2. Practical LVM Management

- Creating the LVM stack: `pvcreate`, `vgcreate`, `lvcreate`
- Formatting and mounting LVs

### 7.3. Dynamic Storage Operations

- Online volume extension: `lvextend`
- Resizing filesystems: `resize2fs` (Ext4) and `xfs_growfs` (XFS)
- Benefits for the "Phoenix Server" architecture

## CHAPTER 8 - Hardening and Emergency Recovery

### 8.1. Post-Installation Hardening

- SSH security: Disabling root login and password authentication
- Firewall management with `ufw`
- Unattended upgrades for automated security patches

### 8.2. Advanced Recovery with `chroot`

- The `chroot` (change root) concept
- Emergency procedure: Repairing a broken system from live media
- Bind mounting system directories (`/dev`, `/proc`, `/sys`)

### 8.3. Manual Builds

- Creating minimal base systems with `debootstrap`
- Use cases for containers and custom cloud images

## Activities

- Learning activity (tutorials), Assessment activity (tutorials + corrected assignments), Self-assessment activity (self-assessment test or multiple-choice questions), Summative activity (problem situation).

## Bibliographies and list of links

- Provide a list of resources for further study of the course content.
