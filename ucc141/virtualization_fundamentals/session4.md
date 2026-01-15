# UCC141-1, Session 4: VM Hardware and Configuration

---

## 1. Modifying VM Settings: Why Power State Matters

Virtual hardware behaves like real hardware in one important way:
**some components must exist before the computer turns on**.

### Powered Off Changes (Most Hardware)

When the VM is off, the hypervisor can safely rewire the virtual motherboard.

You typically must power off the VM to change:

* RAM size
* Number of CPU cores
* Storage controllers
* Adding or removing virtual hard disks

Why?
Because the guest OS detects these at boot time, just like a real BIOS/UEFI scan.

### Running Changes (Hot-plug Features)

Some components are designed to be hot-swappable:

* Network adapter connection (plug/unplug the cable)
* CD/DVD ISO files
* USB devices

These behave like plugging in a USB stick or Ethernet cable on a real computer.

---

## 2. CPU and RAM: The Performance Balancing Act

Your **host OS** and **guest OS** share the same physical hardware. Virtualization is not magic; it is negotiation.

### RAM Allocation (System > Motherboard)

* RAM assigned to the VM is **reserved while the VM runs**.
* If you give too much RAM to the VM:

  * The host OS slows down
  * Everything becomes laggy

That green zone in VirtualBox is a safety buffer.
Staying inside it keeps the host breathing comfortably. 🫁

**Best practice:**

* Linux VMs: 1–2 GB for light tasks, 4 GB+ for desktops
* Windows VMs: 4 GB minimum for usability

### CPU Allocation (System > Processor)

* Each VM “core” is a **virtual CPU thread**, not a physical core.
* Assigning more cores:

  * Helps with compilation, compression, databases
  * Does *not* help much for single-threaded tasks

#### Execution Cap

This is a CPU speed governor:

* 100% = VM can use full assigned CPU time
* 50% = VM can only use half of its allowed CPU

This is useful on shared machines or labs where one VM must not dominate.

#### PAE/NX

* **PAE** allows 32-bit OSs to access more than 4 GB RAM
* **NX** helps with memory protection and security

Most modern OSs expect this to be enabled.

---

## 3. Virtual Storage: The VM’s Memory Palace

Virtual disks are just files on the host, but to the guest OS they look like real drives.

### 3.1 Storage Controllers Explained

The controller defines how the disk “connects” to the VM.

* **IDE**

  * Old and slow
  * Used mainly for legacy OSs or CD/DVD drives

* **SATA**

  * Default and reliable
  * Good compatibility and performance

* **NVMe**

  * Simulates modern SSDs
  * Faster I/O, lower latency
  * Best for modern Linux and Windows guests

Choose SATA for compatibility, NVMe for performance.

---

### 3.2 Virtual Disk Formats: Why They Matter

Each format is like a suitcase built for a different airline.

* **VDI**

  * Best choice for VirtualBox
  * Supports snapshots, resizing, encryption

* **VMDK**

  * Good for moving VMs between VirtualBox and VMware
  * Common in enterprise environments

* **VHD/VHDX**

  * Designed for Microsoft ecosystems
  * Ideal for Hyper-V and Azure

* **QCOW2**

  * Advanced features like compression and snapshots
  * Mostly used with KVM/QEMU

**Rule of thumb:**
Stay native unless you plan to migrate.

---

### 3.3 Fixed vs Dynamic Disks

This is about **when** disk space is reserved.

#### Dynamically Allocated

* The file grows as data is written
* A 50 GB disk with 5 GB used = ~5 GB on host
* Ideal for labs and testing

Downside:
The disk file expands in chunks, which can slightly reduce performance over time.

#### Fixed Size

* Entire disk space reserved immediately
* Faster and more predictable performance
* Preferred for databases and servers

Trade-off:
Uses full space even if mostly empty.

---

## 4. Adding a Second Virtual Disk: What Really Happens

When you add a new disk in VirtualBox:

* The hypervisor creates a new disk file
* It connects it to the virtual controller
* The guest OS sees it as **raw hardware**

The OS does **not** automatically use it.

### Inside the Guest OS (Linux Example)

1. `lsblk` shows:

   * `sda` → original system disk
   * `sdb` → new, empty disk
2. You must:

   * Create a partition
   * Format it (ext4, xfs, etc.)
   * Mount it to a directory

This separation mirrors real-world system administration skills.

---

## 5. Display, Audio, and Network Tweaks

### Display

* **Video Memory**

  * Higher values allow higher resolutions
  * Important for GUI desktops

* **Graphics Controller**

  * VMSVGA → Linux
  * VBoxSVGA → Windows

Wrong choice = black screens or poor performance.

### Audio

* Disabling audio:

  * Saves CPU and RAM
  * Useful for server VMs

### Network

* Network adapters behave like virtual NICs
* Mode (NAT, Bridged, Host-Only) defines how the VM talks to the world
* Covered fully in the next session

---

## 6. Lab Exercises: What You Are Learning

Each lab task maps directly to real admin skills:

### Resource Tuning

You learn:

* Capacity planning
* Performance trade-offs
* Host vs guest resource management

### Adding Storage

You learn:

* Disk provisioning
* Storage expansion without downtime (enterprise reality)
* OS-level disk management

### Disk Initialization

You practice:

* Identifying block devices
* Partitioning and formatting
* Filesystem mounting

This is exactly what sysadmins do on cloud VMs every day.

---

### Final Thought

Virtual machines are not fake computers.
They are **software-defined hardware**. Once you understand that, configuring VMs stops being clicking menus and starts being engineering.