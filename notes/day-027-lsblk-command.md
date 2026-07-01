# Day 027 - Understanding Storage Devices with lsblk

## 🧠 Introduction

Linux systems may contain multiple storage devices:

- Hard drives (HDD)
- Solid-state drives (SSD)
- USB flash drives
- External disks
- Virtual machine disks

The `lsblk` command helps visualize these devices and their relationships.

Its name means:

```text
ls = list
blk = block devices
```

System administrators use `lsblk` to understand:

- Available disks
- Partitions
- Mount points
- Storage layouts
- USB devices

This command is extremely useful when installing Linux, managing servers, or troubleshooting storage problems.

---

## Basic Usage

Run:

```bash
lsblk
```

Example output:

```text
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda      8:0    0  500G  0 disk
├─sda1   8:1    0    1G  0 part /boot
├─sda2   8:2    0   16G  0 part [SWAP]
└─sda3   8:3    0  483G  0 part /
```

This tree structure shows the relationship between disks and partitions.

---

## Understanding the Columns

### NAME

```text
sda
sdb
nvme0n1
```

The device name.

---

### SIZE

```text
500G
1T
64G
```

The total capacity.

---

### TYPE

Possible values:

```text
disk
part
rom
loop
```

Meaning:

- disk = physical device
- part = partition
- rom = optical media
- loop = virtual filesystem image

---

### MOUNTPOINTS

Example:

```text
/
/boot
/home
```

This indicates where the partition is attached within the filesystem.

---

## Human-Readable Output

Most systems already display human-readable sizes.

If needed:

```bash
lsblk --bytes
```

shows exact byte counts.

Example:

```text
536870912000
```

instead of:

```text
500G
```

---

## Display Filesystem Information

Use:

```bash
lsblk -f
```

Example:

```text
NAME FSTYPE LABEL UUID MOUNTPOINT
sda1 ext4         a12b-34cd /boot
sda2 swap         e56f-78gh [SWAP]
sda3 ext4         i90j-12kl /
```

Important fields:

```text
FSTYPE = ext4, xfs, swap
UUID   = Unique identifier
LABEL  = Human-friendly name
```

This is one of the most useful options.

---

## Listing Only Specific Columns

Customize output:

```bash
lsblk -o NAME,SIZE,TYPE,MOUNTPOINTS
```

Option:

```text
-o = output columns
```

Useful in scripts and automation.

---

## Viewing USB Devices

Insert a USB drive and run:

```bash
lsblk
```

Example:

```text
sdb      8:16   1  32G  0 disk
└─sdb1   8:17   1  32G  0 part /media/john/USB
```

This quickly identifies removable devices.

---

## Real-World Examples

Check available disks:

```bash
lsblk
```

Find filesystem types:

```bash
lsblk -f
```

Prepare for partitioning:

```bash
lsblk
```

Identify a newly attached SSD:

```bash
lsblk
```

These tasks are common in cloud servers and virtual machines.

---

## lsblk vs df

### lsblk

```bash
lsblk
```

Shows:

```text
Physical devices and partitions
```

Questions answered:

- What disks exist?
- How are they partitioned?
- Where are they mounted?

---

### df

```bash
df -h
```

Shows:

```text
Filesystem usage
```

Questions answered:

- How much space remains?
- Is the disk full?

The two commands complement each other.

---

## Common Mistakes

### Confusing Devices and Partitions

Example:

```text
sda  = entire disk
sda1 = first partition
sda2 = second partition
```

These are different entities.

---

### Ignoring Mount Points

A partition without a mount point may not be accessible through the filesystem.

Always check:

```text
MOUNTPOINTS
```

---

### Misunderstanding Loop Devices

Example:

```text
loop0
loop1
```

These often come from:

- Snap packages
- ISO images
- Container environments

They are usually normal.

---

## Why This Matters

Imagine connecting a new SSD.

Questions:

```text
Did Linux detect it?
What is its device name?
Does it have partitions?
Is it mounted?
```

The first command most administrators run is:

```bash
lsblk
```

It provides an immediate overview of the storage system.

---

## 🎯 Summary

The `lsblk` command displays storage devices and partitions.

Common examples:

```bash
lsblk
lsblk -f
lsblk --bytes
lsblk -o NAME,SIZE,TYPE,MOUNTPOINTS
```

Important concepts:

```text
disk  = Physical device
part  = Partition
UUID  = Unique filesystem identifier
Mount Point = Directory where storage is attached
```

Understanding storage layouts is essential because Linux servers, virtual machines, cloud environments, and personal computers all rely on properly configured disks and partitions.
