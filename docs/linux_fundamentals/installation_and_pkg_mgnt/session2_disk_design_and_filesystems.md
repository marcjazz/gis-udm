# Session 2: Disk Design and Filesystems

## Objectives

- Master the differences between MBR and GPT partitioning.
- Understand the Linux Filesystem Hierarchy Standard (FHS).
- Learn to configure mount points and `/etc/fstab`.

## 1. Partitioning Theory

Understanding how data is organized on a disk is fundamental to server administration and cloud infrastructure.

### MBR vs. GPT

- **MBR (Master Boot Record):**
  - **Legacy Standard:** Introduced in the early 1980s.
  - **Capacity Limit:** Uses 32-bit values for addressing, limiting disk size to **2TB**.
  - **Partition Limit:** Supports only **4 primary partitions**. To exceed this, one must be configured as an "extended partition" containing multiple "logical partitions".
  - **Single Point of Failure:** The partition table is stored only at the beginning of the disk.

- **GPT (GUID Partition Table):**
  - **Modern Standard:** Part of the UEFI specification.
  - **Massive Capacity:** Uses 64-bit addressing, supporting disks up to **9.4 Zettabytes**.
  - **Unlimited Partitions:** Theoretically unlimited, though most OS implementations (like Linux) default to **128**.
  - **Redundancy & Integrity:** Stores a backup copy of the partition table at the end of the disk and uses Cyclic Redundancy Checks (CRC) to detect corruption.
  - **Protective MBR:** GPT includes a "protective MBR" at the very beginning (LBA 0). This is a dummy MBR partition table that covers the entire disk, making legacy tools see the disk as a single, unknown partition rather than an empty disk. This prevents older tools from accidentally overwriting GPT partitions.

### Inspection Tools

To list and verify partitions on a system, use these essential commands:

```bash
# List all block devices in a tree format with filesystem info
lsblk -f

# List partition tables for all disks (requires sudo)
sudo fdisk -l

# Identify a specific disk's partition scheme (e.g., /dev/sda)
sudo parted /dev/sda print
```

## 2. Linux Filesystems

A filesystem defines how data is stored and retrieved. Selecting the right one is critical for performance and reliability.

### Key Filesystem Types

- **Ext4 (Fourth Extended Filesystem):**
  - The most widely used filesystem in the Linux world.
  - Highly stable, supports volumes up to 1EB and files up to 16TB.
- **XFS:**
  - A high-performance 64-bit journaling filesystem.
  - Excellent at handling large files and high I/O throughput; default for RHEL and CentOS.
- **Btrfs (B-Tree FS):**
  - **Copy-on-Write (CoW):** Instead of overwriting data in place, Btrfs writes new data to a different block and then updates the metadata.
  - **Snapshots:** This CoW nature allows for near-instantaneous, space-efficient snapshots. If a system update fails, you can roll back the entire filesystem to a previous state instantly.
- **Swap:**
  - Dedicated disk space used as "virtual memory" when physical RAM is exhausted.

### The Importance of Journaling

Most modern filesystems (Ext4, XFS) use **Journaling** to ensure data integrity.

1. **The Problem:** In a non-journaling filesystem, if the system crashes while writing a file, the filesystem structure (metadata) might be left in an inconsistent state, requiring a slow `fsck` (filesystem check) on the next boot.
2. **The Solution:** A journal is a dedicated area (a log). Before making changes to the actual data blocks, the filesystem writes the intended changes to the **journal**.
3. **Recovery:** If a crash occurs, the system simply checks the journal. It either completes the pending operations (replay) or ignores incomplete ones, bringing the filesystem back to a consistent state in seconds rather than hours.

## 3. The Filesystem Hierarchy Standard (FHS)

The FHS defines the directory structure and directory contents in Linux distributions. It ensures that software can predict the location of installed files and libraries.

### Key Directories and Their Purpose

- **`/etc` (System Configuration):**
  - Contains all of the system-wide configuration files.
  - _Examples:_ `/etc/passwd` (user database), `/etc/ssh/sshd_config` (SSH server config), `/etc/nginx/nginx.conf` (Web server config).
- **`/var` (Variable Data):**
  - Files to which the system writes data during the course of its operation.
  - _Examples:_ `/var/log/syslog` (system logs), `/var/lib/mysql` (database storage), `/var/spool/mail` (mail queues).
- **`/home` (User Data):**
  - Personal directories for regular users.
  - _Examples:_ `/home/alice/Documents`, `/home/bob/.bashrc`.
- **`/root` (Root Home):**
  - The home directory for the root user (separate from `/home` to ensure availability if `/home` is on a different, unmounted partition).
- **`/boot` (Boot Loader):**
  - Static files required to boot the system.
  - _Examples:_ `vmlinuz` (the Linux kernel), `initrd.img` (initial RAM disk).
- **`/bin` & `/sbin` (Essential Binaries):**
  - `/bin`: Command-line binaries essential for all users (e.g., `ls`, `cp`, `bash`).
  - `/sbin`: System administration binaries essential for the root user (e.g., `fdisk`, `reboot`, `iptables`).
- **`/usr` (User Binaries):**
  - The largest share of data on a system; contains user-facing programs and libraries.
  - _Examples:_ `/usr/bin/python3`, `/usr/share/doc`.
- **`/dev` (Device Files):**
  - Hardware representation files.
  - _Examples:_ `/dev/sda` (first SATA disk), `/dev/null` (the "black hole").

## 4. Mounting & Persistence

In Linux, storage devices are not automatically available; they must be "mounted" to a directory in the FHS.

### The `/etc/fstab` File

The File System Table (`/etc/fstab`) determines how disk partitions, remote storage, or other file systems are integrated into the system at boot.

#### Anatomy of an `fstab` entry

```text
UUID=a1b2c3d4...  /var/log  ext4  defaults,noatime  0  2
(1)               (2)       (3)   (4)               (5)(6)
```

1. **`<file system>`:** The device identifier. While `/dev/sda1` works, **UUIDs** (Universally Unique Identifiers) are preferred (see below).
2. **`<mount point>`:** The directory where the filesystem will be accessible.
3. **`<type>`:** The filesystem type (e.g., `ext4`, `xfs`, `nfs`, `swap`).
4. **`<options>`:** Mount parameters. `defaults` includes `rw`, `suid`, `dev`, `exec`, `auto`, `nouser`, and `async`. `noatime` is often used on SSDs or cloud instances to reduce writes by not updating "last access" times.
5. **`<dump>`:** Used by the `dump` utility (legacy). Usually set to `0`.
6. **`<pass>`:** Used by `fsck` to determine the order of filesystem checks at boot. `1` for the root filesystem, `2` for others, `0` to disable.

### The Importance of UUIDs

In cloud and server environments, **Device Names are Unpredictable**.

- If you add a new disk to a virtual machine, what was `/dev/sdb` might become `/dev/sdc`.
- If a hardware controller initializes disks in a different order, your system might fail to boot if it relies on `/dev/sdX` names in `fstab`.

**UUIDs** solve this by providing a unique string tied to the filesystem itself, regardless of which physical port or controller it's connected to.

#### How to find a UUID

```bash
# Display the UUID and filesystem type for all block devices
sudo blkid
```

## Resources

- [FHS Specification](https://refspecs.linuxfoundation.org/FHS_3.0/fhs/index.html)
