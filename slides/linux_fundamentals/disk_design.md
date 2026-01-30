---
marp: true
theme: gaya
size: 16:9
paginate: true
header: 'Disk Design and Organization'
footer: 'Simplified Introduction'
---

<style>
/* Global styles for a dark theme */
section {
  background-color: #202124;
  color: #e8eaed;
}
h1, h2, h3, h4, h5, h6 {
  color: #e8eaed;
}
a {
  color: #8ab4f8;
}
/* Adjust lead class for dark theme */
section.lead {
  display: flex;
  flex-direction: column;
  justify-content: center;
  text-align: center;
}
</style>

<!-- _class: lead -->

# **Disk Design and Organization**

## The Foundation of Linux

Understanding how to arrange your storage.

---

## What is Disk Organization?

Imagine your computer's hard drive is a big, empty library.

- **Disk Organization** is how you decide to divide that library into rooms (partitions) and how you store books (files) inside those rooms using different shelving systems (filesystems).

Why is this important? It helps your computer:

- Store different types of information separately.
- Run multiple operating systems.
- Work efficiently.

---

## Partitions: Dividing Your Disk

A **partition** is like a separate room in your library. You carve up the entire hard drive into smaller, manageable sections.

### **Why Partition?**

- **Organization:** Keep your system files separate from your personal files.
- **Security/Stability:** If one partition gets corrupted, others might be safe.
- **Multi-Boot:** Install Windows and Linux on the same computer.

---

## MBR vs. GPT: The Blueprint

These are two different ways to draw the "floor plan" for your partitions.

- **MBR (Master Boot Record):**
  - **Older:** Like an old-school blueprint.
- **Limits:** Only works well for disks up to 2TB. Can only have 4 main sections (primary partitions).

- **GPT (GUID Partition Table):**
  - **Modern:** The new, flexible blueprint.
- **No Limits:** Works with very large disks (terabytes and beyond). Can have many, many sections (partitions).
- **Needed for UEFI:** Most new computers use GPT with a modern startup system called UEFI.

---

## Partition Types (MBR Specific)

If using MBR, you have specific types of "rooms":

- **Primary Partitions:** The main rooms. You can have up to 4.
- **Extended Partition:** A special type of primary partition that acts like a hallway. You can only have one.
- **Logical Partitions:** Smaller rooms _inside_ the extended partition. You can have many of these.

  _(GPT doesn't use "extended" or "logical" – it's simpler, almost all partitions are "primary" in concept)_

---

## Common Linux Partitions

On a Linux system, we often set up specific partitions for different purposes:

- **`/` (Root Partition):**
  - **The Main Brain:** This is where the operating system itself lives (all your Linux core files).
- Every other directory is under `/`.

- **`/boot` Partition:**
  - **The Starting Blocks:** Contains the Linux kernel and files needed to start your computer.
- Often kept separate, especially when using advanced storage like LVM.

---

## Common Linux Partitions (Continued)

- **`swap` Partition:**

  - **RAM's Backup:** Used by the system when your computer runs out of physical RAM. It's like a temporary overflow area on your hard drive.

- **`/home` Partition:**
  - **Your Personal Space:** This is where all your user accounts store their files, documents, pictures, etc.
- Good to keep separate, so you can reinstall the operating system without losing your personal data.

- **EFI System Partition (ESP):**
  - **For Modern Boots:** If your computer uses UEFI (and most new ones do), this small partition stores files needed by the UEFI firmware to boot the operating system.

---

## Filesystems: How Data is Stored

A **filesystem** is the method your computer uses to organize and manage files on a partition. It's like the shelving system _inside_ your library rooms.

- **What it Does:** Keeps track of where files begin and end, their size, who owns them, etc.

### **Common Linux Filesystems:**

- **Ext4:** (Extended Filesystem 4)
  - **The Popular Choice:** The most common and recommended filesystem for Linux today. It's reliable and efficient.
- **XFS, Btrfs:**
  - **For Big Jobs:** More advanced filesystems, often used in servers for better performance, data integrity, or special features (like snapshots).

---

## Filesystems: Compatibility

- **Talking to Windows:**
  - **FAT32, NTFS:** Filesystems mainly used by Windows. Linux can usually read and write to these, which is handy for sharing files.

---

## Mount Points: Connecting Everything

A **mount point** is an empty directory where a partition (or another storage device) is "attached" and made accessible to the system.

- **Analogy:** You build a room (partition) in your library, but it's empty. A mount point is like putting a door on that room and giving it a name (e.g., `/home`). Now, when you go through the `/home` door, you enter that specific partition.

- **`/etc/fstab`:** This special file tells your Linux system which partitions to automatically attach (mount) to which directories (mount points) every time the computer starts.

---

<!-- _class: lead -->

## Summary: Key Takeaways

- **Disks are Divided:** Hard drives are split into **partitions**.
- **MBR vs. GPT:** Old vs. new ways to manage partitions.
- **Linux Uses Specific Partitions:** (`/`, `/boot`, `swap`, `/home`, EFI).
- **Filesystems Organize Data:** (`Ext4` is common, `XFS/Btrfs` are advanced).
- **Mount Points Connect:** Partitions are made accessible via **mount points**, configured automatically with `/etc/fstab`.

---

<!-- _class: lead -->

# **Understanding the Foundation**

## Empowers Your Linux Journey
