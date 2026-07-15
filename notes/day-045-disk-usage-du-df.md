# Day 045 - Monitoring Disk Usage with `du` and `df`

## 🧠 Introduction

Disk space management is one of the most important responsibilities of a Linux administrator.

When a server runs out of disk space, applications may fail, logs may stop being written, and databases may become unavailable.

Linux provides two essential commands for monitoring storage:

- `df` (Disk Free)
- `du` (Disk Usage)

Although they sound similar, they serve different purposes.

- `df` shows the available space on entire filesystems.
- `du` shows how much space files and directories are using.

Together, these commands help identify storage problems quickly.

---

# The `df` Command

The `df` command displays information about mounted filesystems.

Basic syntax:

```bash
df
```

Example output:

```text
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        50G   22G   26G  46% /
tmpfs           2.0G     0  2.0G   0% /dev/shm
```

Columns:

```text
Size   Total capacity

Used   Used space

Avail  Available space

Use%   Percentage used

Mounted on  Mount point
```

---

# Human-Readable Output

Instead of displaying values in blocks:

```bash
df -h
```

Example:

```text
Filesystem      Size Used Avail Use%
/dev/sda1        50G 22G   26G  46%
```

Option:

```text
-h = Human-readable
```

This is the most commonly used form.

---

# Display Specific Filesystem

Check the filesystem containing your home directory:

```bash
df -h ~
```

Check a mounted drive:

```bash
df -h /mnt/backup
```

This is useful on systems with multiple disks.

---

# The `du` Command

The `du` command reports how much disk space files and directories consume.

Basic syntax:

```bash
du
```

This displays the size of every directory recursively.

---

# Human-Readable Directory Sizes

Use:

```bash
du -h
```

Example:

```text
4.0K    ./notes
12M     ./images
180M    ./videos
```

---

# Show Only the Total Size

Display only the total size of a directory:

```bash
du -sh Documents
```

Output:

```text
2.3G Documents
```

Options:

```text
-s = Summary

-h = Human-readable
```

This is probably the most frequently used `du` command.

---

# Display Directory Depth

Show only one level of subdirectories:

```bash
du -h --max-depth=1
```

Example:

```text
1.5G Downloads
320M Projects
45M Pictures
```

This helps identify which folders occupy the most space.

---

# Finding Large Files

Find files larger than 500 MB:

```bash
find . -type f -size +500M
```

Then inspect directory sizes:

```bash
du -sh *
```

These commands are often used together.

---

# Sorting Directory Sizes

Display the largest directories first:

```bash
du -sh * | sort -hr
```

Example:

```text
8.1G Videos
2.3G Downloads
450M Projects
120M Documents
```

Explanation:

```text
sort -h   Human-readable sorting

-r        Reverse order
```

This is one of the most practical storage analysis commands.

---

# Real-World Examples

Check available disk space:

```bash
df -h
```

Check your home directory size:

```bash
du -sh ~
```

Find the largest folders:

```bash
du -h --max-depth=1 | sort -hr
```

Inspect log directory usage:

```bash
du -sh /var/log
```

Check Docker storage:

```bash
du -sh /var/lib/docker
```

These commands are part of daily server maintenance.

---

# Common Mistakes

### Confusing `du` and `df`

Remember:

```text
df → Filesystem usage

du → Directory usage
```

They answer different questions.

---

### Forgetting Human-Readable Output

Instead of:

```bash
du
```

Use:

```bash
du -h
```

Large numbers become much easier to understand.

---

### Running `du` on the Entire Filesystem

Command:

```bash
du -sh /
```

may take a long time on large systems.

Instead, inspect specific directories first:

```bash
du -sh /home

du -sh /var

du -sh /opt
```

---

# Why `du` and `df` Matter

Imagine your server reports:

```text
Disk Full
```

First, check the filesystem:

```bash
df -h
```

You discover that `/` is 98% full.

Next, determine which directory is responsible:

```bash
du -h --max-depth=1 /
```

You find:

```text
/var = 25G
```

Continue drilling down:

```bash
du -h --max-depth=1 /var
```

Eventually, you discover that old log files are consuming most of the space.

This workflow is used daily by Linux administrators to troubleshoot storage issues.

---

# 🎯 Summary

The `df` and `du` commands are essential for monitoring disk usage.

Common examples:

```bash
df -h

df -h ~

du -sh Documents

du -h --max-depth=1

du -sh * | sort -hr
```

Important options:

```text
df -h                Human-readable filesystem usage

du -h                Human-readable directory sizes

du -sh               Show total directory size

--max-depth=1        Limit recursion depth

sort -hr             Sort human-readable values in reverse order
```

Understanding `du` and `df` enables you to monitor storage, locate large directories, troubleshoot disk space issues, and keep Linux systems running efficiently.
