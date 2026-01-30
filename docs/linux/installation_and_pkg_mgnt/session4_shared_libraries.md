# Session 4: Shared Libraries and Dependencies

## Objectives

- Understand the differences between static and dynamic linking.
- Learn how the dynamic linker (`ld.so`) locates and loads shared libraries.
- Manage the system-wide library cache using `ldconfig`.
- Diagnose and fix common "library not found" errors using diagnostic tools.

---

## 1. What are Shared Libraries?

In Linux, libraries are collections of pre-compiled code that programs can use to perform common tasks (e.g., encryption, networking, or basic input/output).

### Static vs. Dynamic Linking

When a developer compiles a program, they must decide how to include these libraries:

| Feature          | Static Linking                                                                    | Dynamic Linking                                                                          |
| :--------------- | :-------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------- |
| **How it works** | Library code is physically copied into the program's binary file at compile time. | The program contains a "pointer" (reference) to the library, which is loaded at runtime. |
| **File Size**    | Large (contains all needed code).                                                 | Small (reies on external files).                                                         |
| **Updates**      | Requires recompiling the program to update the library.                           | Updating the `.so` file updates all programs using it.                                   |
| **Dependencies** | No external dependencies; self-contained.                                         | Requires the correct version of the library to be present on the system.                 |
| **Memory Use**   | Multiple programs use separate copies of the same library code.                   | Multiple programs share a single copy of the library in memory.                          |

### Library Naming and the `soname`

Shared libraries typically use the `.so` (Shared Object) extension. To manage compatibility, Linux uses a mechanism called **soname**.

- **Filename:** `libssl.so.1.1` (The actual file on disk).
- **soname:** `libssl.so.1` (The name the program looks for).

The `soname` allows multiple versions of the same library to coexist. For example, a program built for `libexample.so.1` won't accidentally try to use `libexample.so.2`, preventing crashes due to incompatible changes.

---

## 2. Managing the Library Cache

When you run a dynamically linked program, the **Dynamic Linker** (`ld.so` or `ld-linux.so`) is responsible for finding the required `.so` files and loading them into memory.

### The Library Cache: `/etc/ld.so.cache`

Searching every directory on the system for a library every time a program starts would be extremely slow. To solve this, Linux uses a **cache**:

1. The system reads configuration files (like `/etc/ld.so.conf`) to find where libraries are stored.
2. The `ldconfig` command processes these locations and creates a binary index: `/etc/ld.so.cache`.
3. The dynamic linker uses this cache for near-instant lookups.

### Adding a New Library Path

If you install a custom application in `/opt`, its libraries won't be in the standard paths (`/lib` or `/usr/lib`). Here is how to make the system aware of them:

1. **Create a configuration file:** Create a new file in the configuration directory.

    ```bash
    # Create a file for our custom app
    echo "/opt/my-app/lib" | sudo tee /etc/ld.so.conf.d/my-app.conf
    ```

2. **Update the cache:** Run `ldconfig` to rebuild `/etc/ld.so.cache`.

    ```bash
    sudo ldconfig
    ```

3. **Verify:** The system can now find libraries located in `/opt/my-app/lib`.

---

## 3. Inspection Tools

### `ldd`: List Dynamic Dependencies

The `ldd` command is your first line of defense when a program fails to start. It shows exactly which libraries a binary needs and where it's finding them.

**Example output:**

```bash
$ ldd /usr/bin/ls
    linux-vdso.so.1 (0x00007ffca7fe4000)
    libselinux.so.1 => /lib/x86_64-linux-gnu/libselinux.so.1 (0x00007f3e1b01a000)
    libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007f3e1ae28000)
    libpcre2-8.so.0 => /lib/x86_64-linux-gnu/libpcre2-8.so.0 (0x00007f3e1ad91000)
    /lib64/ld-linux-x86-64.so.2 (0x00007f3e1b076000)
```

**Troubleshooting "Not Found":**
If a library is missing or the cache isn't updated, you will see:
`libcustom.so => not found`
This indicates that either the library is not installed or its directory is not in the linker's search path.

### `readelf`: Peeking Inside the Binary

While `ldd` shows what the system _finds_, `readelf` shows what the binary _requests_. This is useful if the binary itself is broken or for checking requirements without running the code.

```bash
readelf -d /usr/bin/ls | grep NEEDED
```

_Output:_
`0x0000000000000001 (NEEDED)             Shared library: [libselinux.so.1]`

---

## 4. Practical Exercise: Troubleshooting a Broken Dependency

In this lab, we will simulate a scenario where a custom program cannot find its required library.

### Step 1: Prepare the Environment

We will create a dummy library and a dummy program to test the linker.

```bash
# Create a custom library directory
sudo mkdir -p /opt/mylib

# Create a "fake" library file
sudo touch /opt/mylib/libcustom.so

# Create a "fake" program in a standard bin path
sudo touch /usr/local/bin/myprogram
```

### Step 2: Identify the Problem

Imagine `myprogram` was compiled to require `libcustom.so`. Because `/opt/mylib` is not a standard path, the linker won't find it.

```bash
# This would normally show 'not found' if it were a real binary
# For this exercise, we simulate the check:
ldd /usr/local/bin/myprogram
```

### Step 3: Apply the Fix

We need to tell the system to look in `/opt/mylib`.

1. **Create the config file:**

    ```bash
    echo "/opt/mylib" | sudo tee /etc/ld.so.conf.d/custom.conf
    ```

2. **Update the cache:**

    ```bash
    sudo ldconfig
    ```

3. **Verify the fix:**
    Run `ldconfig -p | grep libcustom` to see if the library is now in the cache.

    ```bash
    ldconfig -p | grep libcustom
    ```

    _Expected output:_ `libcustom.so (libc6,x86-64) => /opt/mylib/libcustom.so`

---

## Resources

- `man ld.so`: Documentation for the dynamic linker.
- `man ldconfig`: Documentation for the cache management tool.
- `man ldd`: Documentation for dependency inspection.
