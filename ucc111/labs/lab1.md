# **Lab 1: The Phoenix Server - From Ashes to Automation**

**Scenario:**

Welcome back, specialists. A critical, minimalist web server has suffered a catastrophic failure. The only thing that remains is the client's requirement: a fast, secure, and minimal Debian system. Your task is to rebuild it from the ground up. This isn't just about getting a system running; it's about building it with intention, precision, and an understanding of the components, just like you would in a real-world data center. We will use the Debian `netinst` (network install) image, which is small and requires you to pull packages from the network, forcing a deliberate choice of what goes into our system.

**Prerequisites:**

- A hypervisor (VirtualBox, KVM/QEMU, VMware) installed.
- [Debian 12 Network Install ISO](https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/debian-12.5.0-amd64-netinst.iso) downloaded.

**Core Concepts Refresher:**

Your LPIC-101/102 knowledge is sound, but a year is a long time. Refresh your memory on:

- **Logical Volume Management (LVM):** Why it's superior to standard partitions for server environments (flexibility, snapshots).
- **debootstrap:** A tool to install a basic Debian system into a subdirectory of another, already-installed system.
- **chroot:** (change root) A way to run commands and an interactive shell within a different root directory. Essential for system recovery and custom builds.

---

## **Level 1: The Foundation (Standard Complexity)**

**Goal:** Build a minimal, functional Debian server using the expert guided installer and LVM for a flexible disk layout.

**Instructions:**

1. **VM Creation:**

    - Create a new VM. Name it `phoenix-server`.
    - Assign it: 2 vCPUs, 2048 MB RAM, and a new 20 GB virtual disk.
    - Mount the Debian `netinst` ISO and boot the VM.

2. **Expert Installation:**

    - From the boot menu, select **Advanced options > Expert install**. This mode exposes every step of the installation process. Proceed through the initial steps (language, location, keyboard).

3. **Partitioning with LVM (The Core Task):**

    - When you reach the partitioning step, choose **Manual**.
    - Create a new partition table on your virtual disk.
    - Create a small 512MB primary partition at the beginning of the disk. Set its "Use as" type to **Ext4** and its mount point to `/boot`.
    - Create a second, larger primary partition using the remaining space. Set its "Use as" type to **physical volume for LVM**.
    - Now, navigate to the "Configure the Logical Volume Manager" menu.
    - Create a **Volume Group** (VG) named `vg_phoenix`.
    - Inside `vg_phoenix`, create three **Logical Volumes** (LVs):
      - `lv_root`: 10 GB, to be used for the root filesystem (`/`).
    - `lv_home`: 5 GB, to be used for user data (`/home`).
    - `lv_swap`: 2 GB, to be used for swap space.
    - Finish the LVM configuration and assign each LV its filesystem type (Ext4 for root/home, swap for swap) and mount point.

4. **Minimal Package Installation:**

    - Proceed with the base system installation.
    - When you reach "Software selection," **deselect everything**, especially the "Debian desktop environment."
    - The only two options that should be checked are:
      - **SSH server**
    - **standard system utilities**
    - This ensures our server is lean and has no unnecessary graphical components.

5. **Finalize and Verify:**
    - Install the GRUB bootloader to the primary drive (e.g., `/dev/vda`).
    - Finish the installation and reboot. The system will boot to a command-line interface.
    - From your host machine's terminal, SSH into the new server (`ssh user@<vm_ip_address>`).
    - **Verification Commands:** Run the following to confirm your setup. What does each one tell you?
      - `lsblk` (Should show your LVM layout)
    - `df -h` (Should show your filesystems mounted)
    - `free -m` (Should show your swap space is active)
    - `dpkg --get-selections | wc -l` (How many packages are installed? A minimal system is a happy system.)

---

## **Level 2: The Optimization (Advanced Complexity)**

**Goal:** Harden the base installation, automate package deployment, and prepare it for a "production" role.

**Instructions:**

1. **SSH Hardening:**

   - Modify `/etc/ssh/sshd_config` on `phoenix-server` to enhance security.
     - Disable root login (`PermitRootLogin no`).
   - Disable password-based authentication (`PasswordAuthentication no`).
   - On your host machine, generate an SSH key (`ssh-keygen`) if you don't have one, and copy the public key to the server (`ssh-copy-id user@<vm_ip_address>`).
   - Restart the SSH service (`systemctl restart sshd`) and verify you can still log in (it should now be passwordless).

2. **Firewall Configuration:**

   - Install the Uncomplicated Firewall: `apt install ufw`.
   - Configure it to deny all incoming traffic by default.
   - Explicitly allow SSH traffic. What port does SSH use?
   - Enable the firewall. Verify its status.

3. **Create a Personal Package Repository:**

   - On the server, install `nginx`: `apt install nginx`.
   - Create a simple dummy Debian package. You don't need to write code; the goal is to create the package structure.

```bash
# Install packaging tools
sudo apt install build-essential devscripts debhelper dh-make
# Create a project
mkdir ~/dummy-pkg-1.0 && cd ~/dummy-pkg-1.0
dh_make --native -s -y
# Build the package (ignore warnings)
debuild -us -uc
```

    - You will find a `.deb` file in the parent directory.
    - Create a directory in the `nginx` web root (`/var/www/html/debian`) and copy your `.deb` file there.
    - Configure `nginx` to serve this directory.
    - On the server itself, add your own `nginx` server as an APT repository in `/etc/apt/sources.list`.
    - Run `apt update` and then install your `dummy-pkg`.

---

## **Level 3: The Recovery & Deep Dive (Expert Complexity)**

**Goal:** Simulate a catastrophic failure and rebuild the system without the installer, using only command-line tools. This is the ultimate test of system understanding.

**Instructions:**

1. **Simulated Disaster: GRUB is Gone!**

   - On your working `phoenix-server` from Level 1, simulate a bootloader overwrite:
     `sudo dd if=/dev/zero of=/dev/sda bs=446 count=1`
   - Reboot the VM. It will fail to boot, likely with a "No bootable medium" error. The server is dead. Or is it?

2. **Manual System Rescue:**

   - Boot the VM using the Debian `netinst` ISO again.
   - From the main menu, select **Advanced options > Rescue mode**.
   - The rescue environment will try to find your existing installation. Let it guide you to mount your LVM `root` partition under `/target`. If it fails, you must do it manually using the provided shell.
   - The key step: **`chroot /target`**. You are now inside your broken system, with the tools from the live CD.
   - **Your task:** From within the chroot, fix the system. What commands do you need to run?
     - You'll need to mount `/boot`.
   - You'll need to reinstall GRUB. (Hint: `grub-install /dev/sda1`)
   - You might need to update GRUB's configuration.
   - Exit the `chroot`, reboot without the ISO, and watch your server rise from the ashes.

3. **The `debootstrap` Challenge:**
   - If you complete the rescue, the final challenge awaits. Destroy your VM and create a new one.
   - This time, do not use the installer at all. Boot into Rescue Mode from the start.
   - From the command line, perform a full manual installation:
     1. Partition the disk (`parted` or `fdisk`).
     2. Create the LVM structure (`pvcreate`, `vgcreate`, `lvcreate`).
     3. Format the filesystems (`mkfs.ext4`, `mkswap`).
     4. Mount everything under `/mnt` (e.g., root on `/mnt`, boot on `/mnt/boot`).
     5. Use **`debootstrap`** to install the Debian 'bookworm' release into `/mnt`.
     6. `chroot` into `/mnt` and manually install a kernel (`apt install linux-image-amd64`), GRUB (`apt install grub-pc`), configure `/etc/fstab`, set a root password (`passwd`), and create a user.
   - If you can successfully boot this manually-built system, you have demonstrated a true mastery of the Linux installation process.
