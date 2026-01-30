# Session 6: Snapshots for State Management

By the end of this session, learners will be able to:

- Define VM snapshots and explain how they work internally
- Create, revert, and delete snapshots safely
- Interpret snapshot trees and understand delta disks
- Use snapshots to recover from configuration failures
- Apply snapshot best practices and avoid common pitfalls

---

## 1. What Is a Snapshot? (With Diagram)

A **snapshot** is a point-in-time record of a virtual machine’s state, mainly its disk contents and sometimes its memory.

### Snapshot Concept Diagram

```
Before Snapshot
----------------
[ VM Disk.vmdk ]
       |
       v
 Running VM

After Snapshot
--------------
[ VM Disk.vmdk ]  (Read-only)
       |
       v
[ Delta Disk 0001.vmdk ]
       |
       v
 Running VM
```

Key idea:

- The original disk is frozen
- All new changes go into a **delta disk**
- Reverting discards delta changes

---

## 2. Snapshot Tree Explained (Visual)

Snapshots can form a tree if multiple snapshots are taken.

```mermaid
Base Disk
   |
   +-- Snapshot A
   |       |
   |       +-- Snapshot B
   |
   +-- Snapshot C
```

Meaning:

- Snapshot B depends on Snapshot A
- Deleting Snapshot A affects Snapshot B
- Longer chains = slower disk performance

---

## 3. Snapshot vs Backup (Comparison Table)

| Feature         | Snapshot | Backup |
| --------------- | -------- | ------ |
| Independent     | No       | Yes    |
| Long-term use   | No       | Yes    |
| Fast rollback   | Yes      | No     |
| Production-safe | Limited  | Yes    |

Snapshots are **temporary safety checkpoints**, not archival storage.

---

## 4. When to Use Snapshots (Use Cases)

Good use cases:

- Before software installation
- Before configuration changes
- OS updates
- Training labs
- Testing risky commands

Bad use cases:

- Databases in production
- Long-term storage
- Disaster recovery

---

## 5. Advanced Snapshot Topics

### 5.1 Memory Snapshots

When taking a snapshot, you can choose to include the **VM's RAM state**.

- **Advantage:** Reverting restores the VM exactly where it was (no reboot needed).
- **Disadvantage:** Takes significantly more host disk space and takes longer to create.

### 5.2 Quiescing and Guest OS Interaction

In enterprise environments (VMware/Hyper-V), hypervisors use **Guest Tools** to "quiesce" the filesystem before taking a snapshot. This ensures that the filesystem is in a consistent state (buffers flushed) so that databases don't get corrupted.

### 5.3 Snapshot Consolidating

When you delete a snapshot, the hypervisor doesn't just delete files; it **merges** the delta changes back into the parent disk. This process is called **Consolidation**. If consolidation fails, the VM may experience "stun" (brief freezes) or disk errors.

---

## 6. Practical Lab: Snapshot Recovery with a Web Server

### Lab Objective

Use a snapshot to recover a Linux VM after breaking a web server configuration.

---

## Lab Environment

- Linux VM (Ubuntu 20.04+ recommended)
- User with sudo privileges
- Internet access

---

## Part 1: Install a Web Server (Apache)

### Step 1: Update Packages

```bash
sudo apt update
```

### Step 2: Install Apache

```bash
sudo apt install apache2 -y
```

### Step 3: Start and Enable Apache

```bash
sudo systemctl start apache2
sudo systemctl enable apache2
```

---

## Part 2: Take a Snapshot

### Snapshot Action (Hypervisor GUI)

- Snapshot name: **Working Web Server**
- Description: _Apache installed and running correctly_

---

## Part 3: Break the Web Server Configuration

### Step 1: Edit Apache Configuration

```bash
sudo nano /etc/apache2/ports.conf
```

### Step 2: Introduce an Error

Change `Listen 80` to `Listen eighty`.

### Step 3: Restart Apache

```bash
sudo systemctl restart apache2
```

Expected result: Service fails to start.

---

## Part 4: Revert to Snapshot

1. Power off VM.
2. Revert to **Working Web Server**.
3. Power on VM.
4. Verify Apache is working again (`sudo systemctl status apache2`).

---

## 7. Advanced Lab: Analyzing Delta Disks

1. Take a snapshot of your VM.
2. Find the VM's storage folder on your **Host OS**.
3. Identify the new file created (often ending in `.vmdk` or `.vdi` but with a long hex string in the name).
4. Note its size.
5. Create a large file inside the VM (`dd if=/dev/zero of=testfile bs=1M count=100`).
6. Check the delta file size on the host again. Notice how it grew while the base disk remained unchanged.

---

## 8. Best Practices Checklist

✔ Take snapshots before risky changes
✔ Use clear names and descriptions
✔ Delete snapshots when done
✘ Do not keep snapshots long-term (more than 24-72 hours)
✘ Do not use snapshots as backups

---

## Session Wrap-Up

Snapshots give virtual machines a rewind button. In this session, we explored the mechanics of delta disks, the risks of long-term snapshots, and performed a recovery lab.

Today’s key idea:

> **Snapshots protect moments. Clones and templates create futures.**
