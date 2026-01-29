---
theme: gaia
---

# UCC141-1: Virtualization Fundamentals
## Session 6: Snapshots for State Management

---

## Session Objectives

By the end of this session, you will be able to:

- Define VM snapshots and their internal mechanics.
- Create, revert, and delete snapshots safely.
- Understand snapshot trees and delta disks.
- Use snapshots to recover from configuration failures.
- Apply snapshot best practices.

---

## 1. What Is a Snapshot?

A **snapshot** is a point-in-time record of a virtual machine’s state.

- **Captures:** Disk contents (and optionally memory/CPU state).
- **The "Undo" Button:** Allows you to return the VM to exactly how it was.
- **Speed:** Taking a snapshot is nearly instant.

---

## 2. How it Works: Delta Disks

When you take a snapshot, the original disk is **frozen**.

**Before Snapshot:**
`[ Base Disk (Read/Write) ] <--- VM`

**After Snapshot:**
`[ Base Disk (Read-Only) ]`
`          |`
`[ Delta Disk (Read/Write) ] <--- VM`

- New changes only go into the **Delta Disk**.
- Reverting simply deletes the Delta Disk.

---

## 3. Snapshot Trees

Snapshots can be "stacked" to create multiple points in time.

```
Base Disk (Original OS)
   |
   +-- Snapshot A (Software Installed)
   |       |
   |       +-- Snapshot B (Configured)
   |
   +-- Snapshot C (Experimental Setup)
```

- **Caution:** Long chains can slow down disk performance.
- Each snapshot depends on the one before it.

---

## 4. Snapshot vs. Backup

| Feature | Snapshot | Backup |
| :--- | :--- | :--- |
| **Independence** | No (Needs Base Disk) | Yes (Self-contained) |
| **Longevity** | Short-term | Long-term |
| **Rollback** | Very Fast | Slower |
| **Safe for Prod** | Limited | Yes |

**Rule:** Snapshots are *temporary checkpoints*, not permanent storage.

---

## 5. When to Use Snapshots

**Good Use Cases:**
- Before installing new software.
- Before editing critical config files.
- Before running OS updates.
- Training labs (easy resets).

**Bad Use Cases:**
- High-traffic Databases.
- Long-term archival.
- Disaster recovery (if the physical host fails).

---

## 5. Snapshot Lifecycle

```
Take Snapshot
     |
     v
Make Changes
     |
     v
[ Works? ] ---- Yes ----> Delete Snapshot
     |
    No
     |
     v
Revert to Snapshot
```

---

## 6. Lab: The "Time Travel" Recovery

**Objective:** Use a snapshot to recover a Linux VM after breaking a web server.

**Scenario:**
1. Install Apache Web Server.
2. Take a "Known Good" snapshot.
3. Intentionally break the configuration.
4. "Time travel" back to fix it.

---

## Part 1: Setup Apache

1.  **Update:** `sudo apt update`
2.  **Install:** `sudo apt install apache2 -y`
3.  **Start:** `sudo systemctl start apache2`
4.  **Verify:** Open the VM's IP in a browser. You should see the "Apache2 Ubuntu Default Page".

---

## Part 2: The Safety Net

**Take a Snapshot now!**

- **Name:** `Working Web Server`
- **Description:** `Apache installed and verified.`

---

## Part 3: Sabotage

1.  **Edit Config:** `sudo nano /etc/apache2/ports.conf`
2.  **Break it:** Change `Listen 80` to `Listen eighty`.
3.  **Restart:** `sudo systemctl restart apache2`
4.  **Check Status:** `sudo systemctl status apache2`

**Result:** The service fails. The website is down.

---

## Part 4: Revert & Verify

1.  **Action:** Use the Hypervisor menu to **Revert to Snapshot**.
2.  **Boot:** Start the VM.
3.  **Check:**
    -   `sudo systemctl status apache2` (Should be running)
    -   Check browser (Should be back online)

**Outcome:** The broken configuration file was physically replaced by the version in the snapshot.

---

## 7. Best Practices Checklist

- [ ] **Delete** snapshots once they aren't needed.
- [ ] Use **descriptive names** (e.g., "Pre-PHP-Update").
- [ ] Shut down the VM before taking snapshots for maximum stability (though "Hot" snapshots are possible).
- [ ] **Never** rely on snapshots as your only backup.

---

## Questions?

**Next Session:** Clones & Templates (Scaling your Infrastructure).
