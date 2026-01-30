# Session 6: RedHat Package Management (RPM/DNF)

## Objectives

- Understand the RPM format and ecosystem.
- Master `dnf` for enterprise-grade package management.
- Learn about Yum repositories and AppStreams.

## 1. Low-Level Management: `rpm`

The `rpm` (Red Hat Package Manager) tool is the low-level foundation for handling `.rpm` files, directly analogous to `dpkg` in the Debian world. It interacts with the local RPM database and individual package files.

### The Key Limitation: No Dependency Resolution

Like `dpkg`, `rpm` **cannot resolve dependencies automatically**. If you attempt to install an RPM that requires other packages, the installation will fail, leaving you to manually find and install the requirements.

### Core Commands

| Command                 | Description                                                               |
| :---------------------- | :------------------------------------------------------------------------ |
| `sudo rpm -ivh pkg.rpm` | **Install** a local package with verbose output and a progress bar.       |
| `sudo rpm -e httpd`     | **Erase** (remove) an installed package.                                  |
| `rpm -qa \| grep httpd` | **Query All** installed packages and filter for "httpd".                  |
| `rpm -qf /etc/passwd`   | **Query File** to find which package owns `/etc/passwd`.                  |
| `rpm -V httpd`          | **Verify** the integrity of the `httpd` package against the RPM database. |

### Understanding the Flags

- **`-i` (Install):** Installs a new package.
- **`-v` (Verbose):** Provides detailed output during the process.
- **`-h` (Hash):** Prints hash marks (`#`) to show installation progress.
- **`-e` (Erase):** Removes a package from the system.
- **`-q` (Query):** Asks the RPM database for information.
- **`-a` (All):** When used with `-q`, searches all installed packages.
- **`-f` (File):** When used with `-q`, searches for the package that owns a specific file.
- **`-V` (Verify):** Compares the current state of files against the original metadata (MD5, size, permissions).

---

## 2. High-Level Management: `dnf`

`dnf` (Dandified Yum) is the modern, primary tool for managing software on Red Hat-based systems (Fedora, RHEL, CentOS Stream, AlmaLinux, Rocky Linux). It succeeded `yum` and is built for better performance and dependency resolution.

### Key Difference from APT

Unlike `apt`, `dnf` **automatically refreshes its repository metadata** before performing operations. This means you generally do not need to run a separate "update" command (like `apt update`) before installing new software.

### Dnf Core Commands

| Command                  | Description                                                        |
| :----------------------- | :----------------------------------------------------------------- |
| `dnf search httpd`       | Search repositories for packages related to "httpd".               |
| `dnf info httpd`         | Show detailed information about the `httpd` package.               |
| `sudo dnf install httpd` | Download and install `httpd` along with all its dependencies.      |
| `sudo dnf update`        | Upgrade all installed packages to their latest available versions. |
| `sudo dnf remove httpd`  | Remove the `httpd` package and its unused dependencies.            |

### Enterprise Power Feature: `dnf history`

One of DNF's most powerful features for system administrators is the ability to track and undo transactions.

- **`dnf history`**: Lists all recent package transactions with IDs.
- **`dnf history info <id>`**: Shows exactly what happened in a specific transaction (which packages were added/removed).
- **`sudo dnf history undo <id>`**: Roll back the changes made in a specific transaction. This is essential for recovering from a problematic update.

### Modularity and AppStreams

RHEL-family systems use **AppStreams** to provide multiple versions of the same software stack (e.g., Python 3.8 vs. 3.9 or Node.js 14 vs. 16) on the same OS release.

- **`dnf module list`**: Shows available software modules and their versions (streams).
- **`sudo dnf module install nodejs:16`**: Installs a specific version of a module.

---

## 3. Repository Configuration

Repository information is stored in files ending in `.repo` within the `/etc/yum.repos.d/` directory.

### Anatomy of a `.repo` File

```ini
[baseos]
name=Red Hat Enterprise Linux $releasever - BaseOS
baseurl=http://mirror.example.com/rhel/$releasever/BaseOS/$basearch/os/
enabled=1
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release
```

- **`[baseos]`**: A unique ID for the repository.
- **`name`**: A human-readable name for the repository.
- **`baseurl`**: The URL where the package files are hosted.
- **`enabled=1`**: Tells DNF to use this repository (set to `0` to disable).
- **`gpgcheck=1`**: Ensures DNF verifies the GPG signature of packages before installation.

### Essential Repositories: EPEL

For RHEL, AlmaLinux, or Rocky Linux, the **EPEL (Extra Packages for Enterprise Linux)** repository is almost always required. It provides high-quality, community-maintained packages that are not included in the standard RHEL repositories (e.g., `htop`, `nginx`, `certbot`).

---

## 4. Practical Comparison: APT vs. DNF

| Feature / Action        | Debian/Ubuntu (`apt`)      | RHEL/CentOS (`dnf`)         |
| :---------------------- | :------------------------- | :-------------------------- |
| **Refresh Metadata**    | `sudo apt update`          | (Automatic)                 |
| **Install Package**     | `sudo apt install <pkg>`   | `sudo dnf install <pkg>`    |
| **Upgrade System**      | `sudo apt upgrade`         | `sudo dnf update`           |
| **Search**              | `apt search <term>`        | `dnf search <term>`         |
| **Package Info**        | `apt show <pkg>`           | `dnf info <pkg>`            |
| **Remove Package**      | `sudo apt remove <pkg>`    | `sudo dnf remove <pkg>`     |
| **Cleanup Unused**      | `sudo apt autoremove`      | `sudo dnf autoremove`       |
| **Transaction History** | `/var/log/apt/history.log` | `dnf history` (interactive) |

## Resources

- [DNF Documentation](https://dnf.readthedocs.io/en/latest/)
