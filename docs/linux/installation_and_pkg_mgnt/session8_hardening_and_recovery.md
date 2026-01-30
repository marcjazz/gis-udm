# Session 8: Hardening, Recovery, and Manual Builds

## Objectives

- Apply security best practices to a fresh installation.
- Learn the power of `chroot` for system recovery.
- Understand the `debootstrap` process for custom Linux builds.

## 1. Post-Installation Hardening

After the initial installation, securing the server is the first priority. This involves minimizing the attack surface and ensuring the system stays updated.

### SSH Security

The Secure Shell (SSH) is the primary gateway to your server. Securing it is non-negotiable.

**Recommended Configuration (`/etc/ssh/sshd_config`):**

```bash
# /etc/ssh/sshd_config snippets

# 1. Disable root login via SSH
PermitRootLogin no

# 2. Disable password-based authentication
PasswordAuthentication no

# 3. Enable public key authentication
PubkeyAuthentication yes
```

**Why these settings?**

- **`PermitRootLogin no`**: Prevents attackers from attempting to brute-force the `root` account directly. Users must log in as a standard user and use `sudo` for administrative tasks, providing an audit trail.
- **`PasswordAuthentication no`**: Eliminates the risk of brute-force and dictionary attacks against user passwords. SSH keys are significantly harder to crack.
- **`PubkeyAuthentication yes`**: Explicitly allows the use of cryptographic keys for authentication, which is the gold standard for secure remote access.

### Firewall with `ufw` (Uncomplicated Firewall)

A firewall controls incoming and outgoing traffic. For most web servers, we want to block everything by default and only allow specific ports.

**Setting up a basic web server firewall:**

1. **Set Default Policies:**

    ```bash
    sudo ufw default deny incoming
    sudo ufw default allow outgoing
    ```

    - **`deny incoming`**: Blocks all connection attempts from the outside world. This is the "Safe by Default" approach.
    - **`allow outgoing`**: Allows the server to reach out for updates, DNS, etc.

2. **Allow Essential Services:**

    ```bash
    sudo ufw allow ssh     # Open port 22
    sudo ufw allow http    # Open port 80
    sudo ufw allow https   # Open port 443
    ```

3. **Enable the Firewall:**

    ```bash
    sudo ufw enable
    ```

### Unattended Upgrades

To ensure security patches are applied without manual intervention, use the `unattended-upgrades` package.

**Installation:**

```bash
sudo apt update && sudo apt install unattended-upgrades
```

This ensures that critical security updates are downloaded and installed automatically in the background, keeping your server protected against known vulnerabilities.

## 2. System Recovery & `chroot`

`chroot` (change root) is a powerful tool that allows you to "jail" a process into a different directory, making it think that directory is the root (`/`) of the filesystem. In recovery scenarios, it allows you to enter a broken system from a live environment as if you had booted into it.

### Emergency Procedure: Fixing a Broken `/etc/fstab`

**Scenario:** You edited `/etc/fstab` to add a new drive but made a syntax error. Now, the system fails to boot and drops you into an emergency shell or simply hangs.

#### Step 1: Boot from Live Media

Insert a USB stick with a Linux installer (e.g., Ubuntu, Debian) and boot from it. Choose "Try Ubuntu" or similar to reach a live desktop/terminal.

#### Step 2: Identify and Mount Partitions

Open a terminal and identify your root partition.

```bash
lsblk
```

Look for your main partition (e.g., `/dev/sda2`). Mount it to `/mnt`:

```bash
sudo mount /dev/sda2 /mnt
```

_Note: If you have a separate `/boot` partition (e.g., `/dev/sda1`), mount it as well:_

```bash
sudo mount /dev/sda1 /mnt/boot
```

#### Step 3: Bind Mount System Directories

To make the chrooted environment functional, it needs access to the running kernel's virtual filesystems. Use this "magic incantation":

```bash
for d in /dev /dev/pts /proc /sys /run; do sudo mount --bind $d /mnt$d; done
```

- **Why?** This gives the chrooted environment access to hardware devices (`/dev`), process information (`/proc`), and system state (`/sys`, `/run`).

#### Step 4: Chroot into the System

Now, step into your broken system:

```bash
sudo chroot /mnt
```

Your prompt will change. You are now effectively "inside" your broken system.

#### Step 5: Fix the Problem

Now you can use the tools installed on your server to fix the issue. Open the broken file:

```bash
nano /etc/fstab
```

Correct the error, save, and exit.

#### Step 6: Exit and Reboot

Once fixed, leave the environment and clean up:

```bash
exit            # Exit the chroot
sudo umount -R /mnt  # Recursively unmount everything under /mnt
sudo reboot
```

## 3. Manual Builds with `debootstrap`

`debootstrap` is an advanced tool used to create a minimal Debian or Ubuntu base system from scratch in a specified directory. It doesn't require an installer; it simply downloads and extracts the necessary `.deb` packages.

### Use Cases

- **Creating Container Images:** Build a minimal filesystem for Docker or LXC.
- **Custom Cloud Images:** Create highly optimized, lightweight OS images for cloud providers.
- **Manual System Installation:** Install Debian from a non-Debian live environment (like Arch or Fedora).

### Minimal Command Example

To create a minimal Debian "Bullseye" installation in `/mnt`:

```bash
sudo debootstrap bullseye /mnt http://deb.debian.org/debian
```

Once finished, you would typically `chroot` into `/mnt` to configure the kernel, bootloader, and users.

## 4. Course Wrap-up & Lab 1 Prep

- Reviewing the "Phoenix Server" mission.
- Q&A on the topics covered in the 8 sessions.
- Final tips for the practical exam.

## Resources

- [Debian Wiki: Chroot](https://wiki.debian.org/chroot)
- [UFW Documentation](https://help.ubuntu.com/community/UFW)
