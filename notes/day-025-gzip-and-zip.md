# Day 025 - Compressing Files with gzip and zip

## 🧠 Introduction

Data compression is an essential part of Linux system administration.

Compression helps:

- Save disk space
- Reduce transfer times
- Create backups efficiently
- Package files for sharing

Two popular tools are:

```text
gzip
zip
```

Although they serve similar purposes, they work differently and are used in different situations.

---

## Understanding gzip

The `gzip` command compresses a single file.

Example:

```bash
gzip notes.txt
```

Result:

```text
notes.txt.gz
```

The original file:

```text
notes.txt
```

is removed and replaced with:

```text
notes.txt.gz
```

---

## Decompressing Files

Restore the original file:

```bash
gunzip notes.txt.gz
```

Equivalent command:

```bash
gzip -d notes.txt.gz
```

Result:

```text
notes.txt
```

---

## Keeping the Original File

Sometimes you want to preserve the original.

Use:

```bash
gzip -k report.txt
```

Option:

```text
-k = keep original file
```

After compression:

```text
report.txt
report.txt.gz
```

Both files remain.

---

## Viewing Compressed Content

Read compressed text without extracting:

```bash
zcat notes.txt.gz
```

Example output:

```text
Linux is a powerful operating system.
```

This is useful for large log files.

---

## Understanding zip

Unlike gzip, `zip` can compress multiple files and directories into a single archive.

Example:

```bash
zip documents.zip file1.txt file2.txt
```

Result:

```text
documents.zip
```

The original files remain untouched.

---

## Compressing a Directory

Use recursive mode:

```bash
zip -r project.zip project/
```

Option:

```text
-r = recursive
```

All files and subdirectories are included.

---

## Extracting zip Files

Use:

```bash
unzip project.zip
```

Files are restored into the current directory.

---

## Real-World Examples

Compress a server log:

```bash
gzip server.log
```

Create a project archive:

```bash
zip -r website.zip website/
```

Extract downloaded files:

```bash
unzip backup.zip
```

Read compressed logs:

```bash
zcat access.log.gz
```

These tasks are common in Linux environments.

---

## gzip vs zip

### gzip

Advantages:

- Fast compression
- Standard on Linux
- Works perfectly with tar

Common format:

```text
.tar.gz
```

Best for:

- Backups
- Logs
- Software packages

---

### zip

Advantages:

- Cross-platform compatibility
- Popular on Windows
- Supports multiple files directly

Best for:

- Sharing files
- Sending projects
- Working across operating systems

---

## Common Mistakes

### Compressing Directories with gzip

Incorrect:

```bash
gzip my_project/
```

Error:

```text
Is a directory
```

Instead:

```bash
tar -czf my_project.tar.gz my_project/
```

or:

```bash
zip -r my_project.zip my_project/
```

---

### Forgetting That gzip Removes the Original

Running:

```bash
gzip report.txt
```

removes:

```text
report.txt
```

Use:

```bash
gzip -k report.txt
```

if you need both versions.

---

### Confusing tar.gz and zip

Remember:

```text
tar + gzip = .tar.gz
zip = single archive format
```

They solve similar problems but use different approaches.

---

## 🎯 Summary

The `gzip` and `zip` commands compress files and reduce storage requirements.

Common examples:

```bash
gzip file.txt
gunzip file.txt.gz
gzip -k report.txt
zcat logs.gz

zip archive.zip file1 file2
zip -r project.zip project/
unzip project.zip
```

Important options:

```text
-k  Keep original file
-d  Decompress
-r  Recursive compression
```

Understanding compression tools is essential because backups, software packages, logs, and file transfers rely heavily on compressed data.
