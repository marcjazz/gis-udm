---
theme: gaia
---

# UCC141-1: Virtualization Fundamentals
## Session 2: Hypervisors Deep Dive

---

## Review: What is Virtualization?

- **Abstraction:** Decoupling software from hardware.
- **Benefits:** Consolidation, Isolation, Portability.
- **Key Players:**
    - **Host:** The physical machine.
    - **Guest:** The virtual machine.
    - **Hypervisor:** The software that bridges them.

---

## The Hypervisor (VMM)

The **Virtual Machine Monitor** is the "traffic cop" of virtualization.

- **Allocates:** Distributes CPU, RAM, and Disk to VMs.
- **Isolates:** Keeps VMs separate from each other.
- **Schedules:** Decides which VM gets access to the physical CPU and when.

---

## Type 1: Bare-Metal

Runs directly on the hardware. No Host OS.

**Hardware -> Hypervisor -> VMs**

- **Performance:** Excellent (Direct hardware access).
- **Efficiency:** No wasted resources on a Host OS GUI.
- **Examples:**
    - VMware ESXi
    - Microsoft Hyper-V (Server)
    - KVM (Linux Kernel)

---

## Type 2: Hosted

Runs as an app on your existing OS.

**Hardware -> Host OS -> Hypervisor -> VMs**

- **Convenience:** Easy to install and use on your laptop.
- **Performance:** Good, but has overhead from the Host OS.
- **Examples:**
    - Oracle VirtualBox
    - VMware Workstation
    - Parallels Desktop

---

## Comparison Summary

| Feature | Type 1 | Type 2 |
| :--- | :--- | :--- |
| **Installation** | Boot from ISO (Replaces OS) | Install like an App (`.exe` / `.deb`) |
| **OS Overhead** | Minimal | Significant |
| **Primary Use** | Servers / Cloud | Development / Desktop |
| **Cost** | Often Licensed (Enterprise) | Often Free / Open Source |

---

## Our Tool: Oracle VirtualBox

Why VirtualBox?

1.  **Free & Open Source:** (GPLv2).
2.  **Cross-Platform:** Works on Windows, Linux, and Mac.
3.  **Feature Rich:** Snapshots, seamless mode, shared folders.

**Key File:** The Extension Pack (adds USB 3.0, RDP support).

---

## Lab Time!

1.  **Install VirtualBox.**
2.  **Open Preferences (`Ctrl+G`):**
    -   Check the **Default Machine Folder**. Does it have space?
3.  **Check Network Manager:**
    -   Verify if a Host-Only adapter exists (e.g., `vboxnet0`).

---

## Questions?

**Next Session:** Creating Your First Virtual Machine
