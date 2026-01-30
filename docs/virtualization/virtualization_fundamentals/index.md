# Virtualization Fundamentals

## Course Information Sheet

- **Title:** Virtualization Fundamentals
- **Prerequisites:** None. Basic computer literacy is assumed.
- **Duration:** 12 hours (8 sessions of 1.5 hours each).
- **Objectives:**
  - Understand the core concepts of hypervisor-based virtualization.
  - Gain practical skills to create, configure, and manage virtual machines (VMs).
  - Learn to manage VM states and networking for various use cases.
- **Assessment:** Continuous assessment (Practical Labs), final exam.

## 8-Session Breakdown

### Session 1: Introduction to Virtualization

- **Lesson:** What is virtualization? Key concepts (Host vs. Guest), benefits (consolidation, isolation, portability), and common use cases (development, testing, servers). A brief history of virtualization.
- **Lab/Assessment:** Research and compare three different virtualization solutions available today (e.g., VMware, KVM, Hyper-V).

### Session 2: Hypervisors Deep Dive

- **Lesson:** Understanding the role of the hypervisor. In-depth comparison of Type 1 (Bare-metal) and Type 2 (Hosted) hypervisors.
- **Lab/Assessment:** Install VirtualBox on a host machine and explore its global settings and preferences.

### Session 3: Creating Your First Virtual Machine

- **Lesson:** Step-by-step walkthrough of the VM creation wizard. Allocating virtual hardware (CPU, RAM). Creating and attaching a virtual hard disk. Mounting an ISO image for OS installation.
- **Lab/Assessment:** Create a new VM and install a lightweight Linux distribution (e.g., Lubuntu or Debian Netinstall).

### Session 4: VM Hardware and Configuration

- **Lesson:** Modifying VM settings. Understanding different virtual disk formats (VDI, VMDK, QCOW2) and their characteristics (fixed vs. dynamically allocated).
- **Lab/Assessment:** Add a second virtual hard disk to your VM. Resize the RAM and CPU allocation and observe the performance impact.

### Session 5: Virtual Networking

- **Lesson:** Exploring different virtual network modes: NAT, Bridged, Host-Only, and Internal Networking. Understanding the use case for each mode.
- **Lab/Assessment:** Configure two VMs. One in Host-Only mode to communicate only with the host, and another in Bridged mode to get an IP from the local network. Verify connectivity.

### Session 6: Snapshots for State Management

- **Lesson:** The power of snapshots. How to create, revert to, and delete snapshots. Understanding the snapshot tree and potential pitfalls.
- **Lab/Assessment:** On your Linux VM, install a web server. Take a snapshot. "Break" the web server configuration. Revert to the snapshot to restore functionality.

### Session 7: Cloning and Templates

- **Lesson:** Creating copies of VMs. Full clones vs. Linked clones: understanding the difference in disk usage and independence. Using a master VM as a template.
- **Lab/Assessment:** Create a "master" Linux VM. Create one full clone and one linked clone from it. Verify that they all run independently.

### Session 8: Automation and Portability

- **Lesson:** Introduction to VM automation with tools like Vagrant. Understanding the `Vagrantfile`. The importance of importing/exporting VMs in the Open Virtualization Format (OVF).
- **Lab/Assessment:** Install Vagrant. Use a public Vagrant box to spin up a pre-configured VM with a single command (`vagrant up`).

---

# Glossary of Terms

- **Cloning**: The process of creating an exact copy of a virtual machine. A **full clone** is an independent copy, while a **linked clone** depends on the original VM.
- **Guest OS**: The operating system running inside a virtual machine.
- **Host OS**: The operating system running on the physical computer where the hypervisor is installed.
- **Hypervisor**: The software that creates and runs virtual machines. **Type 1** runs directly on the host's hardware, while **Type 2** runs on a conventional operating system.
- **ISO Image**: A file containing the complete contents of an optical disc (CD, DVD, etc.), often used to install operating systems on VMs.
- **KVM (Kernel-based Virtual Machine)**: A Type 1 hypervisor built into the Linux kernel.
- **NAT (Network Address Translation)**: A virtual network mode where the VM shares the host's IP address and is typically not directly accessible from the external network.
- **Bridged Networking**: A virtual network mode that connects the VM to the physical network as if it were another physical machine, getting its own IP address.
- **Host-Only Networking**: A virtual network mode that creates a private network between the host and its VMs, with no external access.
- **Snapshot**: A saved state of a virtual machine at a specific point in time, including its memory, settings, and disk state.
- **Vagrant**: A tool for building and managing virtual machine environments in a single workflow, often used for development environments.
- **Virtual Machine (VM)**: A software-based emulation of a physical computer that can run its own operating system and applications.
- **Virtual Disk**: A file on a host file system that appears as a physical hard disk to a guest operating system (e.g., VDI, VMDK files).
- **VirtualBox**: A popular, cross-platform Type 2 hypervisor for desktop use.