---
marp: true
theme: gaya
size: 16:9
paginate: true
header: 'UCC111-2: Linux Installation and Package Management'
footer: 'Lab 1: The Phoenix Server'
---

<style>
/* Global styles for a dark theme */
section {
  background-color: #202124;
  color: #e8eaed;
}
h1, h2, h3, h4, h5, h6 {
  color: #e8eaed;
}
a {
  color: #8ab4f8;
}
/* Adjust lead class for dark theme */
section.lead {
  display: flex;
  flex-direction: column;
  justify-content: center;
  text-align: center;
}
</style>

<!-- _class: lead -->

# **Lab 1: Mission Briefing**
## The Phoenix Server: From Ashes to Automation

**Your mission, should you choose it...**

<!--
notes:
- Welcome everyone.
- Today, we're moving beyond basic theory. You all have the foundational knowledge from your LPIC certifications.
- Our goal today is to apply that knowledge under pressure and learn to build a server with the precision of a true sysadmin.
-->

---

## Your Mission: Build with Intention

Your goal is not just to "install Linux," but to construct a server with **precision, efficiency, and control.**

- **Scenario:** You will be rebuilding a critical server from scratch.
- **Method:** You will use the Debian `netinst` image for a minimal base.
- **Philosophy:** Every package and every configuration choice must be deliberate.

---

## Key Concepts You Will Master

1.  **Logical Volume Management (LVM)**
2.  **Post-Installation Hardening**
3.  **The `chroot` Environment**
4.  **Disaster Recovery (GRUB)**
5.  **`debootstrap` for Manual Installation**

<!--
notes:
- We're going to touch on five key areas today.
- Some of this will be a refresher, but we'll be going deeper than standard textbook examples.
- We'll start with the foundation: the filesystem layout.
-->

---

## 1. Logical Volume Management (LVM)

LVM adds a flexible abstraction layer between your physical disks and your filesystems. It is the **industry standard** for servers.

<style>
.lvm-diagram { display: flex; flex-direction: column; align-items: center; justify-content: center; gap: 5px; font-family: monospace; }
.lvm-box { border: 2px solid #999; padding: 10px; text-align: center; border-radius: 5px; color: #e8eaed; }
.vg-pool { border: 2px dashed #999; padding: 10px; margin-top: 5px; }
.lv-pool { display: flex; gap: 10px; }
</style>

<div class="lvm-diagram">
  <div class="lvm-box" style="background-color: #4a2d2d;">/dev/vda2 (Physical Disk Partition)</div>
  &darr;
  <div class="lvm-box" style="background-color: #2d3a4a;">Physical Volume (PV)</div>
  &darr;
  <div class="vg-pool">
    <strong>Volume Group (VG) - "vg_phoenix" (A Pool of Storage)</strong>
    <div class="lv-pool">
      <div class="lvm-box" style="background-color: #2d4a3a;">LV: root</div>
      <div class="lvm-box" style="background-color: #2d4a3a;">LV: home</div>
      <div class="lvm-box" style="background-color: #2d4a3a;">LV: swap</div>
    </div>
  </div>
</div>

<!--
notes:
- Think of it like this: You give raw disk space to LVM to create a "Physical Volume".
- You then pool one or more PVs into a "Volume Group", which is just a big bucket of storage.
- From that bucket, you can carve out "Logical Volumes" of any size you want. These are your actual partitions.
- The magic is that you can resize these LVs later without having to repartition the physical disk.
-->
---

## LVM in Lab 1: Your Target Layout

This is the professional disk layout you will build. Note the separation of `/boot`.

<!-- _class: spot -->
```
/dev/vda
  ├─ /dev/vda1  (512M, ext4, mounted on /boot)
  └─ /dev/vda2  (19.5G, LVM Physical Volume)
      └─ vg_phoenix (Volume Group)
          ├─ lv_root (10G, ext4, mounted on /)
          ├─ lv_home (5G, ext4, mounted on /home)
          └─ lv_swap (2G, swap)
```

**Why is `/boot` separate?** The bootloader (GRUB) runs very early in the boot process. It needs to read the kernel and initramfs directly from a simple, standard filesystem. It doesn't understand LVM, so `/boot` must be outside of it.

---

## 2. Post-Installation Hardening

A fresh install is a vulnerable install. In Level 2, you will be challenged to harden the server:

- **SSH Hardening:** You will disable direct root login and enforce the use of secure SSH keys.

- **Firewall (`ufw`):** You will implement a "default-deny" policy and explicitly allow only the services you need.

- **Custom APT Repository:** You will practice deploying your own software by creating a local package repository with `nginx`.

---

## The Professional's Superpower:
# `chroot`

---

## The `chroot` Environment

`chroot` (Change Root) creates a temporary "bubble." When you `chroot` into a directory, that directory becomes the `/` root for all commands you run.

**Why this is a superpower:**
- **System Recovery:** You can boot from a live CD, `chroot` into your broken system, and run commands to fix it *as if you were actually logged in*. You can reinstall kernels, fix configs, and manage packages.
- **Custom Builds:** You can install a new system into a folder (`debootstrap`), `chroot` in, and configure it before it ever boots for the first time.

---

## 4. Your Mission: Disaster & Recovery

In the lab, you will intentionally break your server by wiping the bootloader, then bring it back to life.

**Your recovery mission will be:**

1.  **Boot** from a Live ISO (the `netinst` CD).
2.  **Mount** the broken system's partitions into a temporary location.
3.  **`chroot`** into the mounted root filesystem.
4.  **Re-install GRUB** using `grub-install`.
5.  **Reboot** the resurrected server.

This is a fundamental, resume-worthy skill.

---

## The Expert Challenge:
# `debootstrap`

---

## 5. The `debootstrap` Challenge

For those who finish early, `debootstrap` is the ultimate tool for control. It allows you to install a complete Debian base system into a directory **without needing an installer.**

**You will be challenged to:**
1. Manually partition disks from a live CD.
2. Mount them to a temporary directory.
3. Run `debootstrap` to create the system files.
4. `chroot` into the new system to install a kernel and configure it from scratch.

This is how custom Linux images and many automated deployments are born.

---

<!-- _class: lead -->

## Mission Briefing Complete.

**Focus. Be precise. Learn from failure.**

**Good luck.**
