# Session 7: Virtual Machine Cloning and Templates

## Session Goal

By the end of this session, students will be able to clone virtual machines correctly, choose between full and linked clones based on use case, and prepare a reusable “golden image” template without causing identity conflicts on the network.

Think of a VM not just as a disk and some RAM, but as a fully formed digital identity. Cloning copies that identity unless you deliberately erase the fingerprints first 🧬.

---

## 1. Why Clone Virtual Machines?

Cloning is used whenever you need **multiple identical systems** without repeating installation and configuration work.

Common scenarios include:

- Building identical lab machines for students
- Creating test environments that mirror production
- Rapidly deploying servers or desktops
- Preserving a clean baseline before experiments

Instead of reinstalling an OS ten times, you build once, perfect it, then copy it.

---

## 2. Types of VM Clones

Virtualization platforms support two main cloning strategies. The difference lies in **how disk data is stored and shared**.

### 2.1 Full Clones

A **full clone** is a completely independent copy of a virtual machine.

**How it works**

- The entire virtual disk is duplicated
- The clone has no dependency on the original VM

**Advantages**

- Safe and isolated
- Parent VM can be deleted with no impact
- Best choice for long-term or production use

**Disadvantages**

- Consumes significant disk space
- Takes longer to create

**Example**
A 20 GB VM cloned ten times consumes roughly 200 GB.

---

### 2.2 Linked Clones

A **linked clone** shares the original VM’s base disk and stores only changes in a small differencing disk.

**How it works**

- Parent VM disk becomes read-only
- Each clone writes changes to its own delta file

**Advantages**

- Extremely fast to create
- Minimal initial storage usage
- Ideal for labs, classrooms, and testing

**Disadvantages**

- Dependent on the parent VM
- If the parent is deleted or corrupted, all linked clones fail
- Not suitable for long-term independence

**Example**
One 20 GB parent + ten linked clones may initially use only ~21 GB total.

### Comparison Table: Full Clone vs. Linked Clone

| Feature       | Full Clone            | Linked Clone              |
| :------------ | :-------------------- | :------------------------ |
| **Disk Type** | Full Copy             | Differencing Disk (Delta) |
| **Parent VM** | Independent           | Dependent                 |
| **Storage**   | High (full disk size) | Low (only changes stored) |
| **Creation**  | Slower                | Faster                    |
| **Use Case**  | Production, Archiving | Testing, Labs, VDI        |

### Visualizing Clone Types

```text
[Parent VM Disk]
       |
       |--- [Full Clone VM Disk 1] (Independent Copy)
       |
       |--- [Full Clone VM Disk 2] (Independent Copy)

[Parent VM Disk] <--- [Linked Clone VM Delta Disk 1] (Reads from Parent)
       |
       |--- [Linked Clone VM Delta Disk 2] (Reads from Parent)
```

---

## 3. Golden Master and Templates

A **golden master VM** is a carefully prepared system that serves as the source for all clones.

### Standard Workflow

1. Install OS
2. Apply updates
3. Install required software
4. Configure system defaults
5. **Generalize the system**
6. Shut down
7. Clone or convert to a template

The generalization step is critical. Without it, all clones will share the same internal identity.

---

## 4. Generalization and Identity Conflicts

Cloning without generalization causes problems such as:

- Duplicate hostnames
- Conflicting IP leases
- Authentication and security issues
- Broken domain joins

This happens because operating systems store unique identifiers that must be reset.

---

## 5. Generalization by Operating System

### 5.1 Windows: Sysprep

Windows stores identity data in the **Security Identifier (SID)** and other system-specific values.

**Sysprep** removes this identity so Windows can regenerate it on next boot.

**Typical command**

```
sysprep /generalize /oobe /shutdown
```

**What this does**

- Removes SID
- Resets hardware-specific data
- Starts Windows setup on next boot

This is the only Microsoft-supported method for cloning Windows systems.

---

### 5.2 Linux: machine-id and Cloud-Init

Most modern Linux distributions use **systemd**, which stores a unique identifier in:

```
/etc/machine-id
```

#### Manual Generalization (Lab-Scale)

```
sudo truncate -s 0 /etc/machine-id
```

On next boot, the system generates a new ID automatically.

#### Cloud-Init (Enterprise / Cloud)

Cloud-init is the industry standard for large-scale Linux deployments.

It can:

- Generate unique machine IDs
- Set hostnames
- Inject SSH keys
- Run startup scripts
- Install packages on first boot

This is how AWS, Azure, and OpenStack deploy thousands of VMs without collisions.

---

## 6. Linked Clones in Education and VDI

Linked clones shine in environments where:

- VMs are temporary
- Storage efficiency matters
- Rapid provisioning is required

**Virtual Desktop Infrastructure (VDI)** uses this technique to deploy thousands of desktops from a single golden image, each appearing unique to the user while sharing a common base.

---

## 7. Lab Exercise

### Part 1: Prepare the Master VM (Linux)

1. Boot the master VM
2. Run:

   ```
   sudo truncate -s 0 /etc/machine-id
   ```

3. Shut down the VM

---

### Part 2: Create Clones

1. Create one **Full Clone**
   - Record disk usage on the host

2. Create one **Linked Clone**
   - Record disk usage on the host

---

### Part 3: Verification

1. Boot all three VMs
2. Confirm:
   - Unique hostnames
   - Unique IP addresses

3. On the parent VM:

   ```
   touch /tmp/parent-test
   ```

4. Verify the file does **not** appear in either clone

This confirms logical disk isolation even when a base disk is shared.

---

## 8. Corrected and Stable References

These references are authoritative and unlikely to break or mislead students:

- **Microsoft Sysprep Overview**
  [https://learn.microsoft.com/windows-hardware/manufacture/desktop/sysprep--system-preparation--overview](https://learn.microsoft.com/windows-hardware/manufacture/desktop/sysprep--system-preparation--overview)

- **systemd machine-id Documentation**
  [https://www.freedesktop.org/software/systemd/man/machine-id.html](https://www.freedesktop.org/software/systemd/man/machine-id.html)

- **Cloud-Init Official Documentation**
  [https://cloud-init.io/](https://cloud-init.io/)
