---
theme: gaia
---

# UCC141-1: Virtualization Fundamentals
## Session 3: Creating Your First Virtual Machine

---

## The "New Machine" Wizard

We are building a computer out of software.

**Key Decisions:**
1.  **Name:** Be descriptive (e.g., `Web-Server-01`, not `Test`).
2.  **Type/Version:** Sets hidden flags for performance (e.g., enabling PAE/NX for Linux).
3.  **Folder:** Where the configuration and disk files live.

---

## Hardware Allocation: RAM & CPU

**Memory (RAM):**
-   Taken from your *Physical* Free RAM.
-   **Warning:** If Host RAM + Guest RAM > Total RAM, your system will **swap** (crawl to a halt).
-   *Recommendation:* Give the VM 2GB - 4GB for a modern Linux desktop.

**Processors (vCPU):**
-   Standard: 1 vCPU.
-   Recommended: 2 vCPUs for smoother GUI performance.
-   *Limit:* Don't exceed your physical core count (Green zone in slider).

---

## vCPU vs. Core vs. Thread

How does the math work?

- **Physical Core:** An actual hardware unit.
- **Thread (SMT/Hyper-Threading):** A core split into two "logical" paths.
- **vCPU:** One "logical" path given to a VM.

**Example:**
A laptop with **4 Cores / 8 Threads** can comfortably run several VMs with 1 or 2 vCPUs each.

---

## Virtual Storage (The Hard Disk)

The "Hard Drive" is just a file on your laptop.

**Formats:**
-   **VDI:** VirtualBox Native (Use this one).
-   **VMDK:** VMware compatible (Use if sharing with VMware users).

**Allocation:**
-   **Fixed:** Fast, but eats space immediately (e.g., 20GB file created now).
-   **Dynamic:** Efficient. Starts small, grows as you fill it. (e.g., 20GB limit, starts at 2MB).

---

## The "Install Disc": ISO Images

How do we install the OS?

-   We don't use DVDs anymore.
-   We use **.iso** files (exact digital copies of a disc).
-   **Process:**
    1.  Download Linux ISO (e.g., Ubuntu, Debian, CentOS).
    2.  Open VM **Settings -> Storage**.
    3.  Select the "Empty" Optical Drive.
    4.  Choose the ISO file ("Insert Disk").

---

## The Installation Lifecycle

1.  **Create** empty VM.
2.  **Mount** ISO image.
3.  **Power On** VM.
4.  **Install** OS (Format virtual disk, create user).
5.  **Unmount** ISO (remove "disk").
6.  **Reboot** into new OS.

---

## Lab Time!

**Goal:** Get a working Linux Desktop.

1.  **Create VM:** `Lab1-Linux`, 2GB RAM, 20GB Dynamic VDI.
2.  **Settings:** Mount the `Lubuntu` or `Debian` ISO.
3.  **Start:** Run the installer.
    -   *Tip:* Use "Erase disk and install" (Don't worry, it only erases the *virtual* disk!).
4.  **Finish:** Eject ISO and reboot.

---

## Questions?

**Next Session:** VM Hardware Configuration & Performance Tuning
