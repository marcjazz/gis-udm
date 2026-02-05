---
theme: gaia
---

# Virtualization Fundamentals

## Session 7: Virtual Machine Cloning and Templates

---

## Slide 1 – Session Overview

**Topic:** Cloning and Templates in Virtualization

**Focus:**

- Copying virtual machines efficiently
- Understanding clone types
- Preparing reusable master images

**Outcome:** Deploy multiple identical VMs safely and correctly

---

## Slide 2 – Learning Objectives

By the end of this session, you will be able to:

- Explain why VM cloning is used
- Compare full clones and linked clones
- Create and use a golden master VM
- Generalize Windows and Linux systems before cloning

---

## Slide 3 – Why Clone Virtual Machines?

Cloning allows you to:

- Avoid repeated OS installations
- Create identical lab environments
- Rapidly deploy test systems
- Preserve clean baselines

**Key idea:** Build once, reuse many times

---

## Slide 4 – What Is Being Cloned?

A VM includes more than files:

- Operating system
- Installed software
- Configuration settings
- Unique system identifiers

Cloning copies the _entire system identity_

---

## Slide 5 – Clone Types Overview

Two primary cloning methods:

1. **Full Clone**
2. **Linked Clone**

Difference is based on **disk independence vs disk sharing**

---

## Slide 5.1 – Full vs. Linked Clone Comparison

| Feature       | Full Clone            | Linked Clone              |
| :------------ | :-------------------- | :------------------------ |
| **Disk Type** | Full Copy             | Differencing Disk (Delta) |
| **Parent VM** | Independent           | Dependent                 |
| **Storage**   | High (full disk size) | Low (only changes stored) |
| **Creation**  | Slower                | Faster                    |
| **Use Case**  | Production, Archiving | Testing, Labs, VDI        |

---

### Visualizing Clone Types

```
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

## Slide 6 – Full Clone

**Definition:**
A completely independent copy of a VM

**Characteristics:**

- Full disk duplication
- No dependency on parent

---

## Slide 7 – Full Clone: Pros and Cons

**Advantages:**

- Safe and isolated
- Parent VM can be deleted
- Suitable for production

**Disadvantages:**

- High storage usage
- Slower creation time

---

## Slide 8 – Linked Clone

**Definition:**
A clone that shares the base disk with a parent VM

**Characteristics:**

- Uses a differencing (delta) disk
- Parent disk is read-only

---

## Slide 9 – Linked Clone: Pros and Cons

**Advantages:**

- Very fast to create
- Minimal initial storage use
- Ideal for labs and classrooms

**Disadvantages:**

- Dependent on parent VM
- Parent deletion breaks clones

---

## Slide 10 – Storage Comparison Example

**Scenario:** 10 Linux VMs (20 GB each)

- Full clones: ~200 GB
- Linked clones: ~21 GB

**Use linked clones when VMs are temporary**

---

## Slide 11 – Golden Master Concept

A **Golden Master VM** is:

- Fully configured
- Fully updated
- Carefully prepared

Used as the source for all clones

---

## Slide 12 – Golden Master Workflow

1. Install OS
2. Apply updates
3. Install software
4. Configure defaults
5. **Generalize system**
6. Shut down
7. Clone or convert to template

---

## Slide 13 – Why Generalization Matters

Without generalization, clones may share:

- Hostnames
- IP addresses
- System identifiers

This causes network and security conflicts

---

## Slide 14 – Windows Generalization (Sysprep)

Windows uses unique identifiers called **SIDs**

**Sysprep** removes system identity

**Common command:**

```
sysprep /generalize /oobe /shutdown
```

---

## Slide 15 – What Sysprep Does

- Removes SID
- Resets hardware-specific data
- Forces first-boot setup

**Only supported way to clone Windows systems**

---

## Slide 16 – Linux Generalization Overview

Linux uses a unique ID stored in:

```
/etc/machine-id
```

Must be reset before cloning

---

## Slide 17 – Linux Manual Generalization

**Command:**

```
sudo truncate -s 0 /etc/machine-id
```

On next boot:

- New machine ID is generated automatically

---

## Slide 18 – Cloud-Init (Linux at Scale)

Cloud-init is used in:

- AWS
- OpenStack

Handles:

- Hostnames
- SSH keys
- Packages
- First-boot configuration

---

## Slide 19 – Linked Clones in Education and VDI

Common use cases:

- Student labs
- Training environments
- Virtual Desktop Infrastructure (VDI)

Thousands of desktops from one image

---

## Slide 20 – Lab Overview

**Goal:** Create and test clones from a master VM

You will:

- Generalize a Linux VM
- Create full and linked clones
- Verify isolation and identity

---

## Slide 21 – Lab Part 1: Prepare Master VM

Inside the master VM:

```
sudo truncate -s 0 /etc/machine-id
```

Then shut down the VM

---

## Slide 22 – Lab Part 2: Create Clones

- Create **one full clone**

- Record disk usage

- Create **one linked clone**

- Record disk usage

---

## Slide 23 – Lab Part 3: Verification

Boot all VMs and verify:

- Unique hostnames
- Unique IP addresses

Create a file on parent VM:

```
touch /tmp/parent-test
```

---

## Slide 24 – Lab Verification Result

The file should:

- Exist on the parent VM
- NOT appear on either clone

This confirms disk isolation

---

## Slide 25 – Key Takeaways

- Cloning saves time and effort
- Full clones provide independence
- Linked clones provide efficiency
- Generalization is mandatory
- Golden images enable scale

---

## Slide 26 – End of Session

Next session:

- Automation and Portability
