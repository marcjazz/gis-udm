# Session 7: Cloning and Templates

## Overview

This session focuses on extending the utility of existing virtual machines by learning techniques for creating copies. We will differentiate between full and linked clones and establish best practices for using a golden master image as a template.

### Key Topics

1. **Creating Copies of VMs**
    - When is cloning necessary (e.g., setting up identical test environments)?
    - The process of cloning within a virtualization management interface.
2. **Full Clones vs. Linked Clones**
    - **Full Clone:** An independent copy of the original VM, including its own independent virtual disk file(s).
      - **Pros:** Total independence from the parent.
      - **Cons:** High storage consumption and longer creation time.
    - **Linked Clone (Snapshot Clone):** A copy that shares the base disk data with the parent VM via a delta/differencing disk file.
      - **Pros:** Fast creation, near-zero initial storage.
      - **Cons:** Dependency on the parent VM; if the parent is deleted or corrupted, the linked clone is destroyed.
3. **Using a Master VM as a Template**
    - Preparation steps for a master image (generalization, removing unique IDs).
    - The workflow: Perfect the master -> Halt -> Clone/Template deployment.

---

## 4. Advanced Topic: Generalization and SID/UUID Management

When cloning a VM, you aren't just copying files; you are copying a "personality." This can lead to conflicts if both VMs run on the same network.

### 4.1 Windows: Sysprep

Microsoft provides a tool called **Sysprep** (System Preparation). Running `sysprep /generalize /oobe` removes unique identifiers like the **Security Identifier (SID)** and resets the hardware activation clock. Upon the next boot, the OS generates new IDs.

### 4.2 Linux: Machine-ID and Cloud-Init

On modern Linux distros (systemd-based), the unique ID is stored in `/etc/machine-id`.

- **Manual Reset:** You can truncate this file to regenerate it on boot.
- **Cloud-Init:** The industry-standard tool for generalizing Linux images in cloud environments (AWS, OpenStack). It handles SSH key injection, hostname setting, and package installation on the first boot of a cloned VM.

---

## 5. Less Common Use Case: Linked Clones for Rapid Lab Deployment

Imagine you need to deploy 10 identical Linux servers for a class.

1. **Full Clone Method:** 10 VMs x 20 GB = **200 GB** storage.
2. **Linked Clone Method:** 1 Parent (20 GB) + 10 Clones (100 MB each initially) = **~21 GB** storage.

This technique is used by **VDI (Virtual Desktop Infrastructure)** solutions to provide thousands of employee desktops from a single "Golden Image."

---

## Lab/Assessment

Create a "master" Linux VM (which you should have from previous sessions).

### Part 1: Manual Generalization (Linux)

1. Inside your master VM, run: `sudo truncate -s 0 /etc/machine-id`.
2. Shut down the VM.

### Part 2: Creating the Clones

1. Create one **Full Clone**. Note the disk space used on the host.
2. Create one **Linked Clone**. Note the disk space used.

### Part 3: Verification

1. Boot all three VMs.
2. Verify unique hostnames and IP addresses.
3. On the parent VM, create a file in `/tmp`. Verify that it **does not** appear in the clones (proving disk isolation despite shared base).

---

## Advanced Topic References

- [VMware Documentation on Cloning Virtual Machines](https://docs.vmware.com/en/vSphere-client/latest/vsphere-ui/GUID-D26E3E2F-C34A-471A-A1B4-83B23D04942F.html)
- [Understanding Linked Clones vs. Full Clones](https://www.storagereview.com/articles/linked-clones-vs-full-clones-in-virtualization)
- [Microsoft Sysprep Guide](https://learn.microsoft.com/en-us/windows-hardware/customize/desktop/run-sysprep)
- [Systemd Machine-ID Documentation](https://www.freedesktop.org/software/systemd/man/machine-id.html)
