---
theme: gaia
---

# Virtualization Fundamentals
## Session 4: VM Hardware & Configuration

---

## Review: Session 3

- **Created a VM:** Defined CPU, RAM, and Disk.
- **ISO:** The installation media.
- **Guest Additions:** Drivers for better performance.

Today: We open the hood and upgrade the parts!

---

## 1. Changing the Specs

Unlike physical hardware, virtual hardware is elastic.

- **Power State:**
    - Most changes (RAM, CPU, HDD) require **Power Off**.
    - Some changes (Network, CD-ROM, USB) work while **Running**.
- **The "Settings" Menu:** Your virtual toolbox.

---

## 2. Tuning CPU & RAM

Balancing Host health vs. Guest performance.

- **RAM (Memory):**
    - Too little? Guest swaps/crashes.
    - Too much? Host starves/crashes.
    - *Tip:* Stay in the Green Zone.
- **CPU (Processors):**
    - **Cores:** Assigning more cores = better multi-tasking.
    - **Execution Cap:** Limit a VM to e.g., 50% of a physical core to prevent overheating/lag.

---

## 3. Storage Deep Dive: Controllers

VMs mimic physical storage connections.

- **SATA (Serial ATA):** The modern standard. Used for Hard Disks and SSDs.
- **IDE:** Legacy. Slower. Often used for the CD-ROM drive for compatibility.
- **NVMe:** High speed. Emulates modern SSD interfaces (good for newer OSs).

---

## 4. Storage Deep Dive: Formats

Which file type for your virtual disk?

- **VDI (VirtualBox):** Native. Best feature support.
- **VMDK (VMware):** widely compatible. Good for sharing VMs.
- **VHD (Microsoft):** Hyper-V compatible.
- **QCOW2 (Linux KVM):** Advanced features, Linux standard.

---

## 5. Storage Deep Dive: Allocation

- **Dynamic:**
    - "Pay as you go."
    - 50GB disk uses 2MB initially. Grows as you save files.
    - *Best for:* Labs, testing, saving space.
- **Fixed:**
    - "Pay up front."
    - 50GB disk uses 50GB immediately.
    - *Best for:* Production databases, high performance.

---

## 6. Adding a Second Disk

Why? Separate OS from Data, or Logs, or Backups.

1.  **Power Off.**
2.  **Settings > Storage > Controller: SATA.**
3.  **"Add Hard Disk"** icon.
4.  **Create New Disk.**
5.  **Boot & Format:** The OS sees a raw, empty drive. You must format it (NTFS/ext4) to use it.

---

## 7. Display & Graphics

- **Video Memory:** default is often low (16MB).
    - Increase to 128MB for smooth desktop performance.
    - Required for high resolution or multiple monitors.
- **Graphics Controller:**
    - **VMSVGA:** Linux Guests.
    - **VBoxSVGA:** Windows Guests.

---

## Lab Time!

1.  **Tuning:**
    -   Modify RAM allocation.
    -   Add a CPU core (if possible).
2.  **Storage Expansion:**
    -   Add a secondary **5 GB** Virtual Hard Disk.
    -   Boot the VM and verify the OS sees it (`lsblk` in terminal).

---

## Questions?

**Next Session:** Virtual Networking (NAT, Bridged, Host-Only).
