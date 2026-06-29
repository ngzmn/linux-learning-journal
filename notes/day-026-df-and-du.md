# Day 026 - Disk Usage with df and du

## 🧠 Introduction

Storage management is one of the most important responsibilities in Linux administration.

A full disk can cause:

- Application failures
- Database issues
- System crashes
- Failed updates
- Log collection problems

Linux provides two essential commands:

```text
df = Disk Free
du = Disk Usage
```

Although their names are similar, they answer different questions.

```text
df → How much space is available on a filesystem?

du → How much space does a file or directory consume?
```

Understanding this distinction is critical.

---

## Using df

Display filesystem usage:

```bash
df
```

Example output:

```text
Filesystem     1K-blocks     Used Available Use%
/dev/sda1       52428800 24576000 27852800 47%
```

This shows:

- Total capacity
- Used space
- Available space
- Usage percentage

---

## Human-Readable Output

Use:

```bash
df -h
```

Example:

```text
Filesystem      Size Used Avail Use%
/dev/sda1        50G  24G   26G  47%
```

Option:

```text
-h = human-readable
```

This is the most commonly used form.

---

## Display Specific Filesystems

Check only the root partition:

```bash
df -h /
```

Check a mounted USB drive:

```bash
df -h /mnt/usb
```

This helps identify storage problems quickly.

---

## Understanding du

The `du` command measures directory and file sizes.

Example:

```bash
du notes/
```

Output:

```text
4 notes/day-001.md
8 notes/day-002.md
20 notes/
```

The numbers represent disk usage.

---

## Human-Readable Directory Sizes

Use:

```bash
du -sh notes/
```

Example:

```text
12M notes/
```

Options:

```text
-s = summarize
-h = human-readable
```

This is one of the most useful combinations.

---

## Viewing Subdirectory Sizes

Display the size of everything inside a directory:

```bash
du -h projects/
```

Example:

```text
20M projects/web-app
15M projects/api
35M projects/
```

This helps identify large folders.

---

## Sorting Large Directories

Find the biggest directories:

```bash
du -h . | sort -h
```

Example:

```text
4K  ./scripts
12M ./downloads
25M ./videos
```

This is a practical troubleshooting technique.

---

## Real-World Examples

Check overall disk usage:

```bash
df -h
```

Find the size of your notes:

```bash
du -sh notes/
```

Inspect your Downloads directory:

```bash
du -sh ~/Downloads
```

Find large files:

```bash
du -ah | sort -h | tail
```

System administrators use these commands daily.

---

## df vs du

### df

Example:

```bash
df -h
```

Shows:

```text
Entire filesystem usage
```

Questions answered:

- How much free space remains?
- Is the disk full?

---

### du

Example:

```bash
du -sh projects/
```

Shows:

```text
Directory size
```

Questions answered:

- Which folder is consuming space?
- Which files are largest?

---

## Common Mistakes

### Confusing df and du

Incorrect expectation:

```bash
df notes/
```

This does not show the size of `notes/`.

Instead:

```bash
du -sh notes/
```

---

### Forgetting -h

Without:

```bash
-h
```

you may see:

```text
10485760
```

instead of:

```text
10M
```

Human-readable output is usually preferable.

---

### Ignoring Hidden Directories

Large hidden folders such as:

```text
.cache
.local
```

often consume significant storage.

Check them with:

```bash
du -sh ~/.cache
```

---

## Why Disk Monitoring Matters

Imagine a server suddenly stops working.

A quick check:

```bash
df -h
```

reveals:

```text
Use% = 100%
```

The disk is full.

Next:

```bash
du -sh /var/log/*
```

identifies massive log files.

This workflow solves countless real-world problems.

---

## 🎯 Summary

The `df` and `du` commands help monitor storage usage.

Common examples:

```bash
df -h
df -h /

du -sh notes/
du -h projects/
du -ah | sort -h | tail
```

Important concepts:

```text
df = Filesystem usage
du = Directory usage
-h = Human-readable output
-s = Summary mode
```

Understanding storage management is essential because every Linux system depends on healthy disk usage and proper capacity planning.
