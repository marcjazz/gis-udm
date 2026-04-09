---
marp: true
theme: default
paginate: true
header: 'Linux Installation & Package Management Exam'
footer: 'Time Allowed: 1h 30min | 1.5 min per question'
---

# Linux Installation and Package Management Exam
**Duration:** 1 hour 30 minutes
**Total Questions:** 60
**Format:** Multiple Choice

---

## Session 1: Introduction and Ecosystem

### Question 1
Which kernel design does the Linux operating system use?
A) Microkernel
B) Monolithic kernel
C) Hybrid kernel
D) Exokernel

---

### Question 2
What is the primary role of the GNU project in the Linux ecosystem?
A) Providing the core kernel architecture.
B) Providing the GUI (Graphical User Interface).
C) Providing essential user-space tools and libraries (e.g., glibc, bash).
D) Managing hardware device drivers.

---

### Question 3
Which of the following distributions is directly derived from Debian?
A) Fedora
B) CentOS
C) Ubuntu
D) openSUSE

---

### Question 4
What does POSIX compliance primarily ensure for a Linux system?
A) High performance in graphical rendering.
B) Compatibility and portability of applications across UNIX-like systems.
C) Built-in network security firewalls.
D) Automated hardware detection.

---

### Question 5
In the standard Linux directory structure, what is the `/etc` directory used for?
A) Storing user home directories.
B) Storing essential system binaries.
C) Storing system-wide configuration files.
D) Storing log files.

---

### Question 6
Which command displays information about the currently running Linux kernel version?
A) `lsb_release -a`
B) `uname -r`
C) `cat /etc/os-release`
D) `dmesg`

---

## Session 2: Disk Design and Filesystems

### Question 7
What is the maximum number of primary partitions allowed on a basic MBR (Master Boot Record) disk?
A) 2
B) 4
C) 8
D) 128

---

### Question 8
Which partitioning scheme allows for disks larger than 2TB and supports up to 128 partitions by default?
A) MBR
B) LVM
C) GPT
D) EXT4

---

### Question 9
Which Linux filesystem is the default for most modern Red Hat-based distributions and excels at handling large files?
A) ext2
B) ext3
C) ext4
D) XFS

---

### Question 10
What does the concept of "journaling" in a filesystem provide?
A) It compresses files to save disk space.
B) It encrypts data at rest.
C) It keeps a log of pending disk changes to recover quickly from crashes.
D) It tracks user login attempts.

---

### Question 11
Which file is consulted by the system at boot time to determine which filesystems should be automatically mounted?
A) `/etc/mtab`
B) `/etc/mounts`
C) `/etc/fstab`
D) `/proc/mounts`

---

### Question 12
You need to create a new ext4 filesystem on `/dev/sdb1`. Which command should you use?
A) `mkfs.xfs /dev/sdb1`
B) `mkfs.ext4 /dev/sdb1`
C) `fdisk -t ext4 /dev/sdb1`
D) `mount -t ext4 /dev/sdb1`

---

### Question 13
Which command provides a summary of available and used disk space on mounted filesystems?
A) `df -h`
B) `du -sh`
C) `lsblk`
D) `fdisk -l`

---

### Question 14
If you want to unmount the filesystem currently mounted at `/mnt/data`, which command is correct?
A) `unmount /mnt/data`
B) `umount /mnt/data`
C) `rmmount /mnt/data`
D) `detach /mnt/data`

---

## Session 3: Boot Process and GRUB2

### Question 15
What is the correct high-level order of the Linux boot sequence?
A) Bootloader -> BIOS/UEFI -> Kernel -> Init
B) BIOS/UEFI -> Bootloader -> Kernel -> Init
C) BIOS/UEFI -> Kernel -> Bootloader -> Init
D) Kernel -> BIOS/UEFI -> Bootloader -> Init

---

### Question 16
What is the purpose of the `initramfs` (or `initrd`)?
A) To launch the graphical user interface.
B) To mount the temporary root filesystem and load drivers needed to mount the real root filesystem.
C) To store the GRUB boot menu configuration.
D) To execute user-level startup scripts.

---

### Question 17
On a UEFI system, where are the bootloaders typically stored?
A) In the MBR (sector 0) of the hard drive.
B) In the `/boot/grub2` directory.
C) On a dedicated EFI System Partition (ESP) formatted with FAT32.
D) Directly within the BIOS ROM.

---

### Question 18
Which file should you edit to safely change GRUB2 settings (like timeout or default kernel) before regenerating the configuration?
A) `/boot/grub2/grub.cfg`
B) `/etc/grub2.conf`
C) `/etc/default/grub`
D) `/boot/grub/menu.lst`

---

### Question 19
After editing GRUB2 settings on a Debian/Ubuntu system, which command applies the changes?
A) `grub-install`
B) `update-grub`
C) `grub-mkconfig`
D) `systemctl restart grub`

---

### Question 20
Which system and service manager is the default "Init" process (PID 1) on almost all modern Linux distributions?
A) SysVinit
B) Upstart
C) systemd
D) OpenRC

---

### Question 21
What command is used to set the default boot target (runlevel) in a systemd environment?
A) `systemctl set-default <target_name>`
B) `init <runlevel>`
C) `telinit <runlevel>`
D) `chkconfig --level <runlevel> on`

---

## Session 4: Shared Libraries

### Question 22
What is the standard filename extension for a shared library in Linux?
A) `.dll`
B) `.lib`
C) `.so`
D) `.a`

---

### Question 23
Which command is used to display the shared libraries required by an executable program?
A) `ldconfig`
B) `ldd`
C) `nm`
D) `strace`

---

### Question 24
Which environment variable can be used to temporarily instruct the dynamic linker to search a custom directory for shared libraries before the default system paths?
A) `LIBRARY_PATH`
B) `LD_LIBRARY_PATH`
C) `PATH`
D) `SHARED_LIBS`

---

### Question 25
You placed a new shared library in `/opt/mylibs/`. How do you permanently add this directory to the system's library search path?
A) Edit `/etc/fstab` and mount the library.
B) Add the path to `/etc/ld.so.conf` (or a file in `/etc/ld.so.conf.d/`) and run `ldconfig`.
C) Run `ldd --add /opt/mylibs/`.
D) Append the path to the `PATH` environment variable in `/etc/profile`.

---

### Question 26
What is the purpose of the `ldconfig` command?
A) To compile source code into shared libraries.
B) To configure the IP address of the local domain.
C) To update the cache (`/etc/ld.so.cache`) of available shared libraries and create necessary symbolic links.
D) To debug shared library load errors dynamically.

---

### Question 27
Which of the following is an example of a soname (Shared Object Name) indicating a specific ABI version?
A) `libcrypto.so`
B) `libcrypto.so.1.1`
C) `libcrypto.a`
D) `libcrypto.h`

---

## Session 5: Debian Package Management

### Question 28
Which command installs a standalone local Debian package file (e.g., `app_1.0.deb`) without automatically resolving external dependencies?
A) `apt-get install app_1.0.deb`
B) `dpkg -i app_1.0.deb`
C) `apt install app_1.0.deb`
D) `apt-cache add app_1.0.deb`

---

### Question 29
Which command removes a package along with its configuration files on a Debian-based system?
A) `dpkg -r package_name`
B) `apt-get remove package_name`
C) `apt-get purge package_name`
D) `apt-get clean package_name`

---

### Question 30
What does the `apt update` command do?
A) It upgrades all installed packages to their latest versions.
B) It downloads package information from all configured sources to update the local package index.
C) It updates the core system kernel.
D) It removes unused dependency packages.

---

### Question 31
Which file primarily defines the remote repositories used by APT?
A) `/etc/apt/apt.conf`
B) `/etc/dpkg/dpkg.cfg`
C) `/etc/apt/sources.list`
D) `/etc/repositories.list`

---

### Question 32
If an installation via `dpkg -i` fails due to missing dependencies, which command can typically resolve and install those dependencies automatically?
A) `apt-get -f install`
B) `dpkg --resolve`
C) `apt-cache depends`
D) `apt update`

---

### Question 33
Which command allows you to search for a package in the configured APT repositories by keyword?
A) `apt-search keyword`
B) `apt-cache search keyword`
C) `dpkg -s keyword`
D) `apt-get find keyword`

---

### Question 34
How can you list all installed packages on a Debian-based system?
A) `apt list --installed` or `dpkg -l`
B) `dpkg -L`
C) `apt-get check`
D) `dpkg -S`

---

### Question 35
You want to find out which installed Debian package provides a specific file (e.g., `/bin/ls`). Which command should you use?
A) `dpkg -f /bin/ls`
B) `dpkg -S /bin/ls`
C) `apt-file show /bin/ls`
D) `apt-cache policy /bin/ls`

---

## Session 6: Red Hat Package Management

### Question 36
Which low-level package manager is the native tool for installing, querying, and verifying packages on RHEL/CentOS systems?
A) dpkg
B) apt
C) rpm
D) yum

---

### Question 37
Which RPM command queries the system to list all currently installed packages?
A) `rpm -ql`
B) `rpm -qa`
C) `rpm -qi`
D) `rpm -Uvh`

---

### Question 38
You have downloaded `software-2.0.rpm`. Which command installs the package and prints a hash-mark progress bar?
A) `rpm -ivh software-2.0.rpm`
B) `rpm -qa software-2.0.rpm`
C) `rpm -e software-2.0.rpm`
D) `rpm -U software-2.0.rpm`

---

### Question 39
What is the primary advantage of using `yum` or `dnf` over `rpm`?
A) They use a faster installation algorithm.
B) They automatically resolve and download required dependencies.
C) They do not require root privileges.
D) They bypass GPG signature checks for faster installation.

---

### Question 40
In modern Fedora and RHEL 8/9 systems, which command replaces `yum` as the default package manager?
A) `zypper`
B) `apt`
C) `dnf`
D) `pacman`

---

### Question 41
Where are the repository configuration files for YUM/DNF located?
A) `/etc/yum.conf`
B) `/etc/yum/repos.list`
C) `/etc/yum.repos.d/`
D) `/var/cache/yum/`

---

### Question 42
Which command downloads and installs all available security and software updates for your installed RPM packages?
A) `yum upgrade` or `dnf upgrade`
B) `rpm --update-all`
C) `dnf refresh`
D) `yum check-update`

---

### Question 43
How do you query an RPM database to find out which package installed the `/etc/passwd` file?
A) `rpm -qf /etc/passwd`
B) `rpm -ql /etc/passwd`
C) `yum provides /etc/passwd`
D) Both A and C

---

## Session 7: LVM (Logical Volume Management)

### Question 44
What is the correct hierarchical structure of LVM?
A) Logical Volumes (LV) contain Volume Groups (VG) which contain Physical Volumes (PV).
B) Physical Volumes (PV) are pooled into Volume Groups (VG), which are divided into Logical Volumes (LV).
C) Volume Groups (VG) consist of Logical Volumes (LV) which are formatted as Physical Volumes (PV).
D) None of the above.

---

### Question 45
Which command initializes a physical disk partition (e.g., `/dev/sdc1`) for use in LVM?
A) `lvcreate /dev/sdc1`
B) `vgcreate /dev/sdc1`
C) `pvcreate /dev/sdc1`
D) `fdisk /dev/sdc1`

---

### Question 46
Which command creates a new Volume Group named `vg_data` consisting of `/dev/sdb1` and `/dev/sdc1`?
A) `vgcreate vg_data /dev/sdb1 /dev/sdc1`
B) `vgextend vg_data /dev/sdb1 /dev/sdc1`
C) `lvcreate -n vg_data /dev/sdb1 /dev/sdc1`
D) `groupadd vg_data /dev/sdb1 /dev/sdc1`

---

### Question 47
You need to create a 50GB Logical Volume named `lv_web` within the `vg_data` volume group. Which command is correct?
A) `lvcreate -L 50G -n lv_web vg_data`
B) `lvcreate -s 50G vg_data lv_web`
C) `vgcreate -L 50G lv_web vg_data`
D) `lvextend -L 50G /dev/vg_data/lv_web`

---

### Question 48
After extending a Logical Volume (`lvextend`), what crucial step must be taken to make the newly added space usable by the OS?
A) Reboot the system.
B) Resize the filesystem residing on the Logical Volume (e.g., `resize2fs` or `xfs_growfs`).
C) Reformat the Logical Volume using `mkfs`.
D) Run `vgscan`.

---

### Question 49
Which tool is used to display detailed attributes and information about existing Volume Groups?
A) `pvdisplay`
B) `vgdisplay`
C) `lvdisplay`
D) `vgs`

---

### Question 50
True or False: LVM allows you to resize Logical Volumes while the system is running and the volume is mounted.
A) True
B) False

---

## Session 8: Hardening and Recovery

### Question 51
When a system fails to boot properly, what mode can you boot into via GRUB to gain a minimal root shell for troubleshooting and repairing without fully starting all services?
A) Multi-user mode
B) Graphical mode
C) Single-user mode (or Rescue mode / Emergency target)
D) Safe Mode

---

### Question 52
What kernel parameter is commonly added to the GRUB boot line to interrupt the boot process and reset a forgotten root password?
A) `init=/bin/bash` or `rd.break`
B) `password_reset=1`
C) `systemd.unit=multi-user.target`
D) `root=/dev/null`

---

### Question 53
What is the purpose of the `chroot` command during a system recovery?
A) To change the ownership of root files to a standard user.
B) To change the root directory of the current running process to a mounted broken filesystem, allowing you to run commands as if booted into it.
C) To format the root partition.
D) To backup the root directory.

---

### Question 54
Which mechanism provides Mandatory Access Control (MAC) on Linux systems, enforcing security policies beyond standard file permissions?
A) iptables
B) SELinux or AppArmor
C) sudo
D) ufw

---

### Question 55
In SELinux, what are the three primary modes of operation?
A) Enabled, Disabled, Broken
B) Allow, Deny, Log
C) Enforcing, Permissive, Disabled
D) Strict, Targeted, Minimum

---

### Question 56
What command is used to change the standard Linux file permissions (Read, Write, Execute)?
A) `chown`
B) `chgrp`
C) `chmod`
D) `chattr`

---

### Question 57
If a file has the permissions `rwxr-x---`, what is its numeric (octal) permission equivalent?
A) 750
B) 770
C) 755
D) 640

---

### Question 58
Which command secures a system by configuring the local firewall rules?
A) `firewalld` / `firewall-cmd`
B) `iptables`
C) `ufw`
D) All of the above

---

### Question 59
What is the purpose of the `/etc/shadow` file?
A) It stores the plaintext user passwords.
B) It stores the securely hashed user passwords and password aging policies.
C) It stores the history of user commands.
D) It stores temporary session tokens.

---

### Question 60
To harden SSH access, which configuration directive in `/etc/ssh/sshd_config` should be set to "no" to prevent the root user from logging in directly over the network?
A) `PermitEmptyPasswords`
B) `PasswordAuthentication`
C) `PermitRootLogin`
D) `AllowUsers`

---

## Answer Key

**1-10:** 1. B | 2. C | 3. C | 4. B | 5. C | 6. B | 7. B | 8. C | 9. D | 10. C
**11-20:** 11. C | 12. B | 13. A | 14. B | 15. B | 16. B | 17. C | 18. C | 19. B | 20. C
**21-30:** 21. A | 22. C | 23. B | 24. B | 25. B | 26. C | 27. B | 28. B | 29. C | 30. B
**31-40:** 31. C | 32. A | 33. B | 34. A | 35. B | 36. C | 37. B | 38. A | 39. B | 40. C
**41-50:** 41. C | 42. A | 43. D | 44. B | 45. C | 46. A | 47. A | 48. B | 49. B | 50. A
**51-60:** 51. C | 52. A | 53. B | 54. B | 55. C | 56. C | 57. A | 58. D | 59. B | 60. C