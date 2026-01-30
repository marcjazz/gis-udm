# Session 5: Debian Package Management (DPKG/APT)

## Objectives

- Master low-level (`dpkg`) and high-level (`apt`) package tools.
- Learn to manage software repositories and GPG keys.
- Solve broken package dependencies.

## 1. Low-Level Management: `dpkg`

The `dpkg` (Debian Package) tool is the foundation of package management on Debian-based systems. It is a **low-level** tool, meaning it interacts directly with `.deb` files and the local package database.

### Primary Use Cases

- **Direct Installation:** Installing a `.deb` file provided directly by a vendor (e.g., Google Chrome or Zoom) when it's not available in a standard repository.
- **System Inspection:** Querying the local database to find information about installed files and packages.

### The Fatal Flaw: No Dependency Resolution

The most critical thing to remember about `dpkg` is that **it does not resolve dependencies automatically.** If you try to install a package that requires other software not yet present on your system, `dpkg` will simply fail.

**Hypothetical Example:**
Imagine you try to install `awesome-app.deb`, which requires `libhelper`.

```bash
sudo dpkg -i awesome-app.deb
# Output:
# Selecting previously unselected package awesome-app.
# (Reading database ... 150000 files and directories currently installed.)
# Preparing to unpack awesome-app.deb ...
# Unpacking awesome-app (1.0.0) ...
# dpkg: dependency problems prevent configuration of awesome-app:
#  awesome-app depends on libhelper; however:
#   Package libhelper is not installed.
#
# dpkg: error processing package awesome-app (--install):
#  dependency problems - leaving unconfigured
```

In this state, `awesome-app` is installed but "broken" because its dependencies aren't met.

### Core Commands

| Command                | Description                                                       |
| :--------------------- | :---------------------------------------------------------------- | --------------------------------------------------- |
| `sudo dpkg -i pkg.deb` | **Install** a local `.deb` file.                                  |
| `sudo dpkg -r pkg`     | **Remove** a package (leaves configuration files).                |
| `sudo dpkg -P pkg`     | **Purge** a package (removes everything, including config files). |
| `dpkg -l               | grep nginx`                                                       | **List** installed packages and filter for "nginx". |
| `dpkg -S /bin/ls`      | **Search** which package "owns" or installed the file `/bin/ls`.  |
| `dpkg -L nginx`        | **List files** installed by the `nginx` package.                  |

---

## 2. High-Level Management: `apt`

The `apt` (Advanced Package Tool) command is the primary, user-friendly interface for day-to-day administration. It sits on top of `dpkg` and adds the critical ability to download packages from remote repositories and **automatically resolve dependencies**.

### The Essential Workflow

You should almost always follow this sequence:

1. **`sudo apt update`**: This does **not** install new software. It refreshes your local package index (a list of what's available and their versions) from the repositories.
2. **`sudo apt install <package>`** or **`sudo apt upgrade`**: Perform the actual installation or update.

**Why update first?** If your local index is outdated, you might try to download a version of a package that no longer exists on the server, resulting in "404 Not Found" errors.

### Common Commands

| Command                  | Description                                                                                       |
| :----------------------- | :------------------------------------------------------------------------------------------------ |
| `sudo apt update`        | Refresh the local database of available packages.                                                 |
| `apt search nginx`       | Search for packages related to "nginx" in the remote repositories.                                |
| `apt show nginx`         | Display detailed information about the `nginx` package (size, dependencies, description).         |
| `sudo apt install nginx` | Download and install `nginx` and all its required dependencies.                                   |
| `sudo apt upgrade`       | Upgrade all installed packages to their latest versions (safe).                                   |
| `sudo apt full-upgrade`  | Perform an upgrade that can also handle changing dependencies (may remove packages if necessary). |
| `sudo apt remove nginx`  | Remove the `nginx` package.                                                                       |

---

## 3. Repositories and Security

APT finds software by looking at "repositories" defined in configuration files.

### Anatomy of a Repository Line

The main configuration file is `/etc/apt/sources.list`. A typical line looks like this:

```text
# Type | Repository URL                 | Distribution | Components
deb      http://deb.debian.org/debian/    bullseye       main contrib non-free
```

- **`deb`**: Indicates this is a repository for binary packages (pre-compiled). `deb-src` would be for source code.
- **`http://...`**: The URL where the files are hosted.
- **`bullseye`**: The distribution/codename of the release (e.g., `bullseye`, `bookworm`, `sid`).
- **`main`**: Officially supported, 100% free software.
- **`contrib`**: Free software that depends on non-free software.
- **`non-free`**: Software that does not meet the Debian Free Software Guidelines (e.g., proprietary drivers).

### Security: GPG Keys

How do you know the package you just downloaded hasn't been modified by a hacker (a "Man-in-the-Middle" attack)? APT uses **GPG (GNU Privacy Guard)** keys.

- Each repository is signed with a private key.
- Your system holds the corresponding public key.
- If the signatures don't match, APT will refuse to install the package.

**Modern Method for Adding Keys:**
While older tutorials use `apt-key` (now deprecated), the modern and secure way is to place the `.gpg` key directly in `/etc/apt/trusted.gpg.d/`:

```bash
# Example: Adding a vendor key
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/docker.gpg
```

---

## 4. Diagnostics and Repair

Package management isn't always smooth. Here is how to handle common issues.

### The "Could Not Get Lock" Error

If you see an error like `E: Could not get lock /var/lib/dpkg/lock-frontend`, it means another process (like an automatic update or another terminal window) is currently using the package manager.

- **Solution:** Wait for the other process to finish. If you are certain no other process is running, a previous one might have crashed, leaving the "lock" file behind.

### The "Magic" Repair Command

If a `dpkg` installation failed due to missing dependencies, or if an installation was interrupted, your package database might be in a "broken" state.

```bash
sudo apt --fix-broken install
```

This command tells APT to look at the broken state of the system and try to download whatever is missing to satisfy the requirements.

### System Housekeeping

- **`sudo apt autoremove`**: Removes "orphaned" packages—dependencies that were installed for a program you've since uninstalled and are no longer needed.
- **`sudo apt clean`**: Clears out the local cache of downloaded `.deb` files (located in `/var/cache/apt/archives/`). This recovers disk space but doesn't uninstall anything.

---

## Resources

- [Debian Policy Manual](https://www.debian.org/doc/debian-policy/)
- [Debian Wiki - SourcesList](https://wiki.debian.org/SourcesList)
