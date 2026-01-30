# Session 7: Logical Volume Management (LVM)

## Objectives

- Understand the abstraction layers of LVM.
- Learn to create and resize logical volumes.
- Understand the benefits of LVM for server administration.

---

## 1. The LVM Architecture

Logical Volume Management (LVM) provides a layer of abstraction between your physical storage and the operating system. Unlike traditional partitioning, which is static and rigid, LVM allows for flexible storage management.

### The Construction Analogy

To demystify the layers, think of LVM like building with bricks:

- **PV (Physical Volume):** These are your **Bricks**. Individual disks or partitions that you prepare to be used by LVM.
- **VG (Volume Group):** This is the **Pile of Bricks**. You throw all your PVs into one big pool of storage.
- **LV (Logical Volume):** This is the **Wall**. You build specific "walls" (partitions) by taking bricks out of the pile. You can always add more bricks to the pile or make a wall taller later.

### Visual Representation

The flow of data storage in LVM looks like this:

```text
Physical Disks  --->  Physical Volumes (PV)  --->  Volume Group (VG)  --->  Logical Volumes (LV)  --->  Filesystem
(e.g., /dev/sdb)      (pvcreate /dev/sdb)          (Storage Pool)           (lvcreate)                  (mkfs.ext4)
```

| Layer        | Component | Description                                                        |
| :----------- | :-------- | :----------------------------------------------------------------- |
| **Physical** | PV        | The physical storage device (disk or partition).                   |
| **Grouping** | VG        | A collection of PVs that forms a single administrative unit.       |
| **Logical**  | LV        | A virtual partition carved from a VG, formatted with a filesystem. |

**Why this abstraction?** Because the filesystem is no longer tied to the physical boundaries of a single disk, you can resize volumes, span them across multiple disks, and take "snapshots" of your data effortlessly.

---

## 2. Managing LVM: A Step-by-Step Tutorial

In this tutorial, we will prepare a new 20GB disk (`/dev/sdb`) for use as a web data partition.

### Step 1: Create Physical Volume

First, we tell LVM that `/dev/sdb` is available for use.

```bash
sudo pvcreate /dev/sdb
```

_Output:_ `Physical volume "/dev/sdb" successfully created.`

### Step 2: Create Volume Group

Next, we add our "brick" to a new "pile" (storage pool) named `data_vg`.

```bash
sudo vgcreate data_vg /dev/sdb
```

_Output:_ `Volume group "data_vg" successfully created.`

### Step 3: Create Logical Volume

Now, we carve out a 10GB "wall" named `web_data` from our pool.

```bash
sudo lvcreate -L 10G -n web_data data_vg
```

- `-L 10G`: Specifies the size.
- `-n web_data`: Specifies the name of the LV.
- `data_vg`: The pool to take space from.

### Step 4: Format the Logical Volume

The LV behaves just like a standard partition. We must format it before use.

```bash
sudo mkfs.ext4 /dev/data_vg/web_data
```

### Step 5: Mount the Logical Volume

Finally, create a mount point and attach the volume.

```bash
sudo mkdir -p /var/www
sudo mount /dev/data_vg/web_data /var/www
```

### Inspecting your work

You can verify each layer using these "scan" commands:

- `sudo pvs`: Shows summary of Physical Volumes.
- `sudo vgs`: Shows summary of Volume Groups.
- `sudo lvs`: Shows summary of Logical Volumes.

---

## 3. Dynamic Resizing

One of LVM's greatest strengths is the ability to grow volumes on the fly.

### Scenario: The web data is filling up!

We need to add 5GB of space to our `/var/www` partition.

#### Step 1: Extend the Logical Volume

```bash
sudo lvextend -L +5G /dev/data_vg/web_data
```

**Important:** This only expands the "block device" (the container). The filesystem inside (the Ext4 structure) still thinks it's 10GB.

#### Step 2: Resize the Filesystem

To tell the filesystem to fill the new space:

```bash
# For Ext4 filesystems:
sudo resize2fs /dev/data_vg/web_data

# For XFS filesystems:
# sudo xfs_growfs /var/www
```

### The "Online" Advantage

This entire process can be performed **online** while the volume is mounted and in use. There is no downtime for your users, which is critical for production servers.

---

## 4. Why LVM for the "Phoenix Server"?

In our "Phoenix Server" architecture, LVM is not just a tool; it's a strategy for longevity and recovery.

1. **Extreme Flexibility:** If `/var/log` starts filling up due to an application error, you can instantly grow it by taking space from a less-used volume, avoiding a system crash.
2. **Resilience through Separation:** By putting `/` (root) and `/home` on separate Logical Volumes, you can completely reinstall or upgrade the OS (formatting the root LV) while leaving the user data on the `/home` LV completely untouched.
3. **Physical Abstraction:** If you run out of space in your `data_vg`, you can simply plug in a new physical hard drive, run `pvcreate` and `vgextend`, and your storage pool grows without you ever having to unmount your filesystems.

---

## Resources

- [LVM HOWTO](https://tldp.org/HOWTO/LVM-HOWTO/)
- [Red Hat: Configuing LVM](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/configuring_and_managing_logical_volumes/index)
