---
marp: true
theme: default
paginate: true
header: 'Virtualization Fundamentals Exam'
footer: 'Time Allowed: 1h 30min | 1.5 min per question'
---

# Virtualization Fundamentals Exam
**Duration:** 1 hour 30 minutes
**Total Questions:** 60
**Format:** Multiple Choice

---

## Session 1: Introduction to Virtualization

### Question 1
What is the primary goal of virtualization in a data center?
A) To increase the physical size of servers.
B) To allow multiple operating systems to run on a single physical machine.
C) To eliminate the need for an operating system.
D) To make hardware completely indestructible.

---

### Question 2
In virtualization terminology, what is the "Host"?
A) The operating system running inside a virtual machine.
B) The physical computer and its operating system that provides resources to VMs.
C) The user who is logged into the virtual machine.
D) The network router connecting the servers.

---

### Question 3
In virtualization terminology, what is the "Guest"?
A) The physical hardware.
B) The person visiting the data center.
C) The virtual machine and the operating system running inside it.
D) The software used to download ISO images.

---

### Question 4
Which of the following is a key benefit of "Server Consolidation" through virtualization?
A) Increased hardware costs.
B) Reduced physical footprint, power consumption, and cooling requirements.
C) Making it harder to manage servers.
D) Requiring a separate physical monitor for every VM.

---

### Question 5
What does "Isolation" mean in the context of virtual machines?
A) VMs cannot talk to each other over the network.
B) A crash or security breach in one VM does not directly affect the host or other VMs.
C) You can only run one VM at a time.
D) The VM is disconnected from the internet.

---

### Question 6
What is "Portability" as it relates to virtual machines?
A) The ability to carry a physical server in a backpack.
B) The ease of moving a VM (as a set of files) from one physical host to another.
C) The ability to run a VM on a smartphone.
D) The speed at which a VM can download files.

---

### Question 7
Before virtualization, what was the typical "One Server, One App" model's biggest drawback?
A) Too much processing power.
B) Hardware underutilization (often using only 5-15% of capacity).
C) Servers were too small to hold applications.
D) Operating systems were too expensive.

---

## Session 2: Hypervisors Deep Dive

### Question 8
What is the primary function of a Hypervisor (VMM)?
A) To act as a web server.
B) To manage and allocate physical hardware resources (CPU, RAM, Disk) to virtual machines.
C) To provide a graphical user interface for the host OS.
D) To encrypt all files on the hard drive.

---

### Question 9
What defines a "Type 1" (Bare-metal) Hypervisor?
A) It runs as an application on top of a standard OS like Windows or Linux.
B) It runs directly on the physical hardware, without an underlying host OS.
C) It requires a specialized "Type 1" keyboard.
D) It can only run one guest OS at a time.

---

### Question 10
Which of the following is an example of a Type 1 Hypervisor?
A) Oracle VM VirtualBox
B) VMware Workstation
C) VMware ESXi
D) Parallels Desktop

---

### Question 11
What defines a "Type 2" (Hosted) Hypervisor?
A) It is built into the motherboard's BIOS.
B) It runs as a software application on top of an existing Host Operating System.
C) It does not require RAM to function.
D) It is only used for high-performance databases.

---

### Question 12
Which of the following is an example of a Type 2 Hypervisor?
A) Microsoft Hyper-V (in its native server role)
B) Xen
C) Oracle VM VirtualBox
D) KVM

---

### Question 13
Why are Type 1 Hypervisors generally preferred for enterprise data centers?
A) They have a smaller overhead and provide better performance and security.
B) They are cheaper than Type 2 hypervisors.
C) They include a built-in office suite.
D) They are easier for home users to install.

---

### Question 14
What is KVM (Kernel-based Virtual Machine)?
A) A Type 2 hypervisor for Windows.
) A virtualization module in the Linux kernel that turns Linux into a Type 1 hypervisor.
C) A brand of physical monitors.
D) A specialized file format for virtual disks.

---

### Question 15
In a Type 2 hypervisor setup, if the Host OS crashes, what happens to the Guest VMs?
A) They continue running unaffected.
B) They also crash or stop because the hypervisor application they depend on has failed.
C) They automatically migrate to the cloud.
D) They start their own host OS.

---

## Session 3: Creating Your First Virtual Machine

### Question 16
What is an "ISO Image" typically used for in VM creation?
A) To store the VM's configuration settings.
B) As a virtual installation disc to boot the VM and install the Guest OS.
C) To increase the VM's RAM.
D) To take a screenshot of the VM.

---

### Question 17
When allocating RAM to a VM, what is a crucial "Host" consideration?
A) You should give the VM all of the host's RAM for maximum speed.
B) You must leave enough RAM for the Host OS to function, otherwise, the whole system will become unstable.
C) RAM doesn't matter for VMs; only CPU does.
D) Virtual RAM is not real RAM.

---

### Question 18
What happens if you allocate 4 virtual CPUs to a VM on a host that only has 2 physical CPU cores?
A) The VM will run 2x faster.
B) The hypervisor will physically grow more CPU cores.
C) The VM may experience significant performance degradation due to CPU overcommitment and contention.
D) The VM will refuse to start.

---

### Question 19
During the VM creation wizard, what is the purpose of a "Virtual Hard Disk"?
A) To store the VM's temporary web cache.
B) To act as the persistent storage (hard drive) for the Guest OS and its files.
C) To speed up the internet connection.
D) To backup the host's physical hard drive.

---

### Question 20
Which component must be "mounted" in the VM's virtual optical drive to start the OS installation?
A) The .vdi file.
B) The .iso file.
) The .xml configuration file.
D) The host's BIOS.

---

### Question 21
What are "Guest Additions" (or VM Tools)?
A) Software installed on the Host to make it faster.
B) Drivers and utilities installed inside the Guest OS to improve performance, resolution, and integration (like mouse sharing).
C) Extra RAM chips for the physical server.
D) Free games included with the hypervisor.

---

### Question 22
Which of the following is NOT a common virtual hardware component you can configure for a VM?
A) Network Adapter
B) USB Controller
C) Physical Power Supply Voltage
D) Sound Card

---

## Session 4: VM Hardware and Configuration

### Question 23
What is a "Dynamically Allocated" (or Thin Provisioned) virtual disk?
A) A disk that immediately takes up its maximum size on the host's physical drive.
B) A disk that starts small and grows on the host's physical drive only as data is added inside the VM.
C) A disk that changes its format every time the VM reboots.
D) A disk that is stored in the RAM.

---

### Question 24
What is the main advantage of a "Fixed Size" (or Thick Provisioned) virtual disk?
A) It saves physical disk space on the host.
B) It is faster to create.
C) It generally offers slightly better and more consistent performance because the space is pre-allocated.
D) It can be easily emailed.

---

### Question 25
Which virtual disk format is the native default for Oracle VM VirtualBox?
A) VMDK
B) VHD
C) VDI
D) QCOW2

---

### Question 26
Which virtual disk format is widely used by VMware products?
A) VDI
B) VMDK
C) RAW
D) DMG

---

### Question 27
If you need to move a VM from VirtualBox to a Microsoft Hyper-V environment, which disk format should you ideally use?
A) VDI
B) VHD or VHDX
C) ISO
D) EXE

---

### Question 28
Can you change the amount of RAM allocated to a VM while it is running?
A) Yes, always.
B) No, most hypervisors require the VM to be powered off to change core hardware like RAM or CPU (unless "hot-plug" features are supported and enabled).
C) Yes, but only if you are using a Type 1 hypervisor.
D) RAM is fixed at the time of creation and can never be changed.

---

### Question 29
What is "CPU Overcommit"?
A) Allocating fewer CPUs than the host has.
B) Assigning more virtual CPUs to your VMs in total than the host has physical cores.
C) Running the CPU at a higher clock speed.
D) Sharing one VM between two physical CPUs.

---

### Question 30
What is the purpose of the "VT-x" or "AMD-V" settings in a physical computer's BIOS/UEFI?
A) To enable hardware-assisted virtualization, allowing the hypervisor to run more efficiently.
B) To increase the resolution of the monitor.
C) To speed up the boot time of Windows.
D) To protect the computer from viruses.

---

## Session 5: Virtual Networking

### Question 31
In "NAT" (Network Address Translation) mode, how does the VM access the internet?
A) It gets a public IP address directly from the ISP.
B) It shares the host's IP address; the hypervisor acts like a router for the VM.
C) It uses a dial-up connection.
D) It cannot access the internet in NAT mode.

---

### Question 32
What is a limitation of standard "NAT" mode for a VM?
A) The VM cannot browse the web.
B) External machines on the physical network cannot easily initiate connections to the VM (e.g., to reach a web server inside it).
C) The host cannot see the VM.
D) It requires a physical network cable for every VM.

---

### Question 33
In "Bridged" networking mode, how does the VM appear on the network?
A) As a hidden process on the host.
B) As a completely independent device with its own IP address from the physical network's DHCP server.
C) As a sub-directory of the host's IP.
D) It doesn't appear on the network at all.

---

### Question 34
When should you use "Host-Only" networking?
A) When you want the VM to be accessible to everyone on the internet.
B) When you want a private network between the host and the VM, with no access to the outside physical network.
C) When you have no network card in your host.
D) To browse the web faster.

---

### Question 35
What is "Internal Networking" mode in a hypervisor like VirtualBox?
A) It connects the VM to the host's internal clock.
B) It creates a private network that only other VMs on the same host can see, excluding even the Host OS.
C) It allows the VM to access the host's files.
D) It is another name for NAT.

---

### Question 36
If you want to run a web server inside a VM and have it accessible to other physical computers in your office, which mode is best?
A) Host-Only
B) Internal
C) Bridged
D) NAT without Port Forwarding

---

### Question 37
What is "Port Forwarding" used for in NAT mode?
A) To change the VM's MAC address.
B) To allow external traffic on a specific host port to be directed to a specific port inside the VM.
C) To speed up the VM's boot time.
D) To connect a printer to the VM.

---

### Question 38
What is a "Virtual Switch"?
A) A physical hardware device you plug into the server.
B) A software-based logic in the hypervisor that routes traffic between virtual network cards and physical adapters.
C) A button on the VM's toolbar to turn off the internet.
D) A way to switch between different VMs.

---

## Session 6: Snapshots for State Management

### Question 39
What is a VM "Snapshot"?
A) A photo taken with the VM's camera.
B) A saved state of the VM (disk, RAM, settings) at a specific point in time.
C) A backup of the entire physical host.
D) A way to delete the VM quickly.

---

### Question 40
When is the best time to take a snapshot?
A) After you have already broken the OS.
B) Right before performing a risky operation, like a major software update or configuration change.
C) Every 5 seconds while typing.
D) Only when the VM is powered off.

---

### Question 41
What does "Reverting" to a snapshot do?
A) It deletes the snapshot.
B) It returns the VM to the exact state it was in when the snapshot was taken, discarding all changes made since then.
C) It upgrades the Guest OS to the latest version.
D) It moves the VM to another host.

---

### Question 42
Can a VM have multiple snapshots?
A) No, only one.
B) Yes, and they can often be organized in a "tree" structure showing different points in time or branches of configuration.
C) Yes, but only if they are stored on different disks.
D) Only if the VM is running Linux.

---

### Question 43
What is a potential disadvantage of keeping a snapshot for a very long time (months) on a busy VM?
A) The VM will become too small.
B) The snapshot "difference" file can grow very large, consuming disk space and potentially slowing down disk performance.
C) The snapshot will expire and delete itself.
D) The VM will forget its password.

---

### Question 44
Do snapshots replace a proper backup strategy?
A) Yes, snapshots are all you need.
B) No; snapshots are for state management/reversion, but they depend on the original disk files. If the original files are lost or corrupted, the snapshots are also lost.
C) Only if you take more than 10 snapshots.
D) Only for Type 2 hypervisors.

---

### Question 45
What happens to the data created *after* a snapshot is taken if you revert to that snapshot?
A) It is moved to a "recovery" folder.
B) It is permanently lost, as the disk is reset to the snapshot's point in time.
C) It is automatically merged into the snapshot.
D) It is emailed to the administrator.

---

## Session 7: Cloning and Templates

### Question 46
What is VM "Cloning"?
A) Renaming a VM.
B) Creating an exact duplicate of an existing virtual machine, including its virtual disks and configuration.
C) Running two VMs at the same time.
D) Installing a VM on two different monitors.

---

### Question 47
What is a "Full Clone"?
A) A clone that only copies the configuration file.
B) A completely independent copy of the VM that does not share any files with the original.
C) A clone that requires the original VM to be running.
D) A clone that is twice as large as the original.

---

### Question 48
What is a "Linked Clone"?
A) A clone that is physically connected via a cable.
B) A copy that "links" to the original VM's virtual disk, saving space but requiring the original disk to remain present.
C) A clone used only for networking tasks.
D) A clone that cannot be deleted.

---

### Question 49
What is the primary advantage of a "Linked Clone" over a "Full Clone"?
A) It is more secure.
B) It is much faster to create and uses significantly less disk space (initially).
C) It can run without a hypervisor.
D) It automatically updates when the original VM updates.

---

### Question 50
In the context of virtualization, what is a "Template" (or Master Image)?
A) A drawing of a VM.
B) A pre-configured, "clean" VM used as a starting point for creating many other identical VMs.
C) A specialized type of virtual disk that cannot be written to.
D) A manual on how to use VirtualBox.

---

### Question 51
After cloning a Windows or Linux VM, what is a common "Cleanup" task you should perform on the new clone?
A) Delete the Guest OS.
B) Change the hostname and network configuration to avoid conflicts with the original VM.
C) Reinstall the hypervisor.
D) Buy a new license for the hypervisor.

---

### Question 52
If you delete the "Parent" (original) VM of a linked clone, what happens to the linked clone?
A) It becomes a full clone automatically.
B) It stops working because it can no longer access the base disk files it depends on.
C) It continues to work perfectly.
D) It is also deleted automatically.

---

### Question 53
What is the "Sysprep" tool (in Windows) or "machine-id" reset (in Linux) used for when creating templates?
A) To make the VM faster.
B) To generalize the OS by removing unique identifiers (like SIDs or hardware IDs) before cloning.
C) To install a web server.
D) To backup the VM.

---

## Session 8: Automation and Portability

### Question 54
What is the purpose of the OVF (Open Virtualization Format) / OVA?
A) To encrypt virtual machines.
B) To provide a standardized, vendor-neutral format for exporting and importing VMs between different hypervisors.
C) To replace the ISO format.
D) To run VMs in a web browser.

---

### Question 55
What is "Vagrant"?
A) A type of computer virus.
B) A command-line tool for building and managing reproducible virtual machine environments using a configuration file.
C) A cloud storage provider.
D) A physical server rack.

---

### Question 56
What is the name of the configuration file used by Vagrant to define a VM?
A) `Vagrant.config`
B) `Vagrantfile`
C) `settings.xml`
D) `.vmrc`

---

### Question 57
In Vagrant, what does the command `vagrant up` do?
A) It shuts down the VM.
B) It creates and starts the virtual environment as defined in the Vagrantfile.
C) It updates the Vagrant software.
D) It uploads the VM to the internet.

---

### Question 58
What is a "Box" in the context of Vagrant?
A) The physical box the server came in.
B) A package format for Vagrant environments, essentially a pre-built base VM image.
C) A popup window in the hypervisor.
D) A specialized network router.

---

### Question 59
Which command is used to completely remove a Vagrant-managed VM and all its associated resources?
A) `vagrant stop`
B) `vagrant delete`
C) `vagrant destroy`
D) `vagrant remove`

---

### Question 60
What is "Infrastructure as Code" (IaC) as it relates to virtualization?
A) Writing code inside a VM.
B) Managing and provisioning infrastructure (like VMs and networks) through machine-readable definition files rather than manual configuration.
C) Using a computer to build a house.
D) Printing out the source code of the hypervisor.

---

## Answer Key

**1-10:** 1. B | 2. B | 3. C | 4. B | 5. B | 6. B | 7. B | 8. B | 9. B | 10. C
**11-20:** 11. B | 12. C | 13. A | 14. B | 15. B | 16. B | 17. B | 18. C | 19. B | 20. B
**21-30:** 21. B | 22. C | 23. B | 24. C | 25. C | 26. B | 27. B | 28. B | 29. B | 30. A
**31-40:** 31. B | 32. B | 33. B | 34. B | 35. B | 36. C | 37. B | 38. B | 39. B | 40. B
**41-50:** 41. B | 42. B | 43. B | 44. B | 45. B | 46. B | 47. B | 48. B | 49. B | 50. B
**51-60:** 51. B | 52. B | 53. B | 54. B | 55. B | 56. B | 57. B | 58. B | 59. C | 60. B
