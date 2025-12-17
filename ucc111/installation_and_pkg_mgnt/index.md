# UCC111-2: Linux Installation and Package Management

This course is part of the Teaching Unit (TU): UCC111 - Linux Foundational (LPIC-101).

## Preamble

- **Purpose**: To provide the essential basics for installing, managing startup, and maintaining software on Linux systems, which are fundamental skills for working on servers and in cloud environments.
- **Target audience**: Students in the Professional Bachelor's Degree in Cloud Computing (Semester 1).
- **Type of access**: Paid (UoM Standard).
- **Hours**: 12
- **Teaching mode**: CS (Synchronous Chat), CA (Asynchronous Chat) (UdM Standard).
- **prerequisites**: None

## Summary

This course covers the key concepts necessary for setting up a functional Linux system. It addresses storage preparation (disk design), boot system installation, and, above all, effective management of software packages and libraries for the main Linux distribution families (Debian/RPM).

## Glossary

- **Linux distribution**: A coherent set consisting of the Linux kernel, a package manager, and a set of tools and applications (e.g., Ubuntu, Debian, Fedora).
- **Kernel**: The core of the operating system that manages hardware resources, processes, memory, and peripherals.
- **CLI (Command Line Interface)**: Command line interface, used to administer the system without a graphical interface.
- **ISO**: Installation image of an operating system containing the files necessary for installation.
- **Bootloader**: Program loaded when the PC starts up, allowing the operating system to be launched.
- **GRUB (GRand Unified Bootloader)**: Bootloader widely used on Linux systems, configurable and multi-OS.
- **UEFI (Unified Extensible Firmware Interface)**: Modern replacement for BIOS, enabling advanced boot management and GPT disk support.
- **BIOS (Basic Input/Output System)**: Legacy firmware that manages hardware initialization at startup.
- **Dual-Boot**: Configuration allowing multiple operating systems to coexist on the same machine.
- **MBR (Master Boot Record)**: Old partitioning scheme limited to 2 TB and 4 primary partitions.
- **GPT (GUID Partition Table)**: Modern partitioning scheme supporting large disks and an unlimited number of partitions.
- **Partition**: Logical division of a disk used to store systems or data.
- **Swap**: Disk space used as an extension of RAM.
- **Mount point**: Directory in which a partition or external disk is integrated into the Linux tree structure.
- **fstab**: File containing the configuration of file systems to be mounted automatically.
- **Shared library (.so)**: File containing code that can be reused by several programs simultaneously, avoiding duplication.
- **ldconfig**: Command that updates the shared library cache.
- **ld.so.conf**: File listing the paths containing dynamic libraries.
- **Dependency**: A package or file required for another program to function properly.
- **Package**: File containing a program, its data, and metadata, managed via a manager.
- **dpkg**: Low-level package manager on Debian/Ubuntu that allows you to install or remove .deb files.
- **apt (Advanced Package Tool)**: High-level manager that automatically resolves dependencies and manages repositories.
- **Repository**: Server containing software packages accessible via APT.
- **sources.list**: File containing the list of repositories used by APT.
- **RPM (Red Hat Package Manager)**: Package format and low-level manager used on RHEL, CentOS, Fedora.
- **YUM (Yellowdog Updater Modified)**: Former high-level manager for RPM systems allowing automatic installation of dependencies.
- **DNF (Dandified Yum)**: A modern replacement for YUM, faster and more reliable.
- **Package group**: A set of related software programs that can be installed together (e.g., web server, graphical environment).
- **Log**: File containing system events and actions, useful for diagnosing errors.
- **Broken package**: A package that is partially installed or contains unmet dependencies.
- **Package manager lock**: Situation where another process (e.g., automatic update) prevents the installation of new packages.
- **APT/YUM cache**: Folder containing metadata and previously downloaded packages.
- **Checksum (SHA256)**: Fingerprint used to verify the integrity of a downloaded ISO image.
- **GPG (GNU Privacy Guard)**: Encryption tool used to verify the authenticity of repositories and packages.
- **lsblk / fdisk / parted**: Commands for inspecting and managing disks and partitions.
- **mount / umount**: Commands used to mount or unmount a file system.
- **systemctl**: Command for managing services, useful for checking whether an installed service is working correctly.

## Learning objectives

By the end of this course, students should be able to:

1. **Master the installation of a Linux system**
   - Prepare installation media (ISO, bootable USB drive).
   - Choose and configure an appropriate partitioning scheme (MBR/GPT).
   - Understand and apply the file system hierarchy
2. **Configure and manage system startup**
   - Understand the role of the bootloader (GRUB).
   - Install, repair, and customize GRUB.
   - Manage multi-boot environments.
3. **Manage system libraries and dependencies.**
   - Identify shared libraries (.so).
   - Manipulate the library cache via ldconfig.
   - Resolve issues related to missing dependencies.
4. **Install, update, and remove packages.**
   - Use low-level tools (dpkg, rpm).
   - Master high-level managers (apt, yum/dnf).
   - Configure software repositories and manage GPG keys.
5. **Diagnose and maintain a functional Linux system.**
   - Detect and repair broken packages.
   - Read the logs related to package installation.

## Assessment

Teaching strategies adopted:
The specific assessment method is: Continuous assessment, Practical work, Final exam.

Standard school protocol:

- Continuous assessment (CC) accounts for 30% of the overall mark, broken down as follows: (Participation in tutorials 20%, Completion of activities 20%, Attendance/presence in class 20%, Completion of practical work 40%)
- The written exam accounts for 70%.

## CHAPTER 1 - Introduction to Linux installation

### 1.1. Understanding Linux distributions

- Definition of a distribution
- Differences between distributions (Debian, Ubuntu, RHEL, CentOS, Fedora, etc.)
- Package management models according to families

### 1.2. Life cycle of a Linux system

- Installation
- Configuration
- Maintenance
- Updates and upgrades

### 1.3. Preparing for installation

- Choosing a distribution based on context
- ISO download and integrity check (SHA256, GPG)
- Creating bootable media (Rufus, Balena, dd)

## CHAPTER 2 — Disk design and organization

### 2.1. Partitioning types

- MBR vs. GPT
- Comparison and limitations
- Primary, extended, and logical partition tables

### 2.2. Partition types

- System partition
- Swap partition
- /home partition
- /boot partition
- EFI partition (ESP)

### 2.3. Linux file systems

- Ext2, Ext3, Ext4
- XFS, Btrfs
- FAT32, NTFS (compatibility)

### 2.4. Mount points

- Role of the mount point
- File system hierarchy (FHS)
- Automatic mounting: /etc/fstab
- Mount options (rw, ro, noexec, etc.)

## CHAPTER 3 - Installation and management of bootloaders

### 3.1. How a bootloader works

- Definition and role
- BIOS/UEFI interaction
- Linux boot chain

### 3.2. GRUB2 - Installation and configuration

- GRUB structure: grub.cfg, scripts
- Menu customization
- Modifying boot options
- Recovery modes

### 3.3. Bootloader troubleshooting

- Reinstalling GRUB
- Handling common errors (error 15, no such device, etc.)
- Backup and restore

### 3.4. Special case: Multi-boot

- Dual-boot with Windows
- Automatic detection via os-prober
- Boot order

## CHAPTER 4 — Shared Library Management

### 4.1. Understanding shared libraries

- .so files
- Dynamic links
- Application dependencies

### 4.2. Library identification and configuration

- The `ldd` command
- Configuration file /etc/ld.so.conf
- Standard library directories

### 4.3. Library cache management

- ldconfig function
- Creating symbolic links
- Cache update

## CHAPTER 5 — Package management in Debian and derivative distributions

### 5.1. Basic package management with dpkg

- Local installation of a .deb
- Removal and purging
- Inspection with dpkg -l, -s, -c

### 5.2. Advanced package management

- Manipulation of configuration files
- Status and partial installation of packages
- Troubleshooting incomplete installations

### 5.3. Managing repositories with APT

- /etc/apt/sources.list
- Adding repositories and GPG keys
- Updating lists: apt update

### 5.4. Common operations with APT

- Installation, upgrade, removal
- Search and diagnostics
- Major upgrade (dist-upgrade, full-upgrade)

### 5.5. Meta package management

- Tasksel
- Functional groups

## CHAPTER 6 - Package management in RedHat, Fedora, and derivatives

### 6.1. Basic management with RPM

- Installing an .rpm
- Signature verification
- Querying RPM packages

### 6.2. Using YUM/DNF

- Manager architecture: repositories, cache, metadata
- Essential commands: installation, removal, update

### 6.3. Advanced management

- Package groups
- Cache cleanup
- Conflict and broken dependency management

### 6.4. Repository configuration

- Creating a local repository
- Adding an external repository
- Temporary activation/deactivation

## CHAPTER 7 - System maintenance and diagnostics

### 7.1. Updating the system

- Security
- Critical patches
- Automatic Updates (cron, systemd timers)

### 7.2. Diagnosing package-related problems

- Missing dependencies
- Broken packages
- Packet manager locking

### 7.3. Logging and logs

- dpkg.log
- yum.log / dnf.log
- journalctl for issues related to installed services

## CHAPTER 8 - Practical exercises

- 8.1. Lab 1: Complete installation of Linux on a VM
- 8.2. Lab 2: Manual MBR and GPT partitioning
- 8.3. TP 3: Installation and configuration of GRUB
- 8.4. TP 4: Installing packages on Debian and RedHat
- 8.5. TP 5: Creating a local repository (Debian or RPM)

## Activities

- Learning activity (tutorials), Assessment activity (tutorials + corrected assignments), Self-assessment activity (self-assessment test or multiple-choice questions), Summative activity (problem situation).

## Bibliographies and list of links

- Provide a list of resources for further study of the course content. (UdM standard)
