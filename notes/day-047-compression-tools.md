# Day 047 - Compression with `gzip`, `bzip2`, and `xz`

## 🧠 Introduction

Compression is an essential part of Linux system administration.

It helps to:

- Save disk space
- Speed up file transfers
- Reduce backup sizes
- Archive logs efficiently

Linux provides several compression tools, but the three most common are:

- `gzip`
- `bzip2`
- `xz`

Each tool offers different trade-offs between speed and compression ratio.

Choosing the right one depends on your needs.

---

# Compression vs Archiving

It is important to understand the difference.

**Compression** reduces the size of a single file.

**Archiving** combines multiple files into one archive.

For example:

```text
tar
```

creates an archive.

```text
gzip
```

compresses one file.

Together they become:

```text
archive.tar.gz
```

This is why `tar` and compression tools are often used together.

---

# gzip

`gzip` is the default compression tool on most Linux systems.

Compress a file:

```bash
gzip report.txt
```

Result:

```text
report.txt.gz
```

The original file is replaced by the compressed version.

---

## Decompress gzip Files

Use:

```bash
gunzip report.txt.gz
```

or

```bash
gzip -d report.txt.gz
```

Both commands restore the original file.

---

## Keep the Original File

Normally, `gzip` removes the original file.

To keep it:

```bash
gzip -k report.txt
```

Option:

```text
-k = Keep original file
```

---

# bzip2

`bzip2` usually provides better compression than `gzip`.

Compress:

```bash
bzip2 report.txt
```

Output:

```text
report.txt.bz2
```

Extract:

```bash
bunzip2 report.txt.bz2
```

or

```bash
bzip2 -d report.txt.bz2
```

---

# xz

`xz` generally provides the highest compression ratio.

Compress:

```bash
xz report.txt
```

Output:

```text
report.txt.xz
```

Extract:

```bash
unxz report.txt.xz
```

or

```bash
xz -d report.txt.xz
```

Because of its excellent compression ratio, `xz` is widely used for distributing Linux packages and large archives.

---

# Comparing the Tools

| Tool | Compression Speed | Compression Ratio | Typical Use |
|------|-------------------|-------------------|-------------|
| gzip | Fast | Good | Everyday compression |
| bzip2 | Medium | Better | Large text files |
| xz | Slower | Best | Backups and software releases |

General guideline:

- Need speed → `gzip`
- Need balanced compression → `bzip2`
- Need maximum compression → `xz`

---

# Viewing File Information

Display compressed file details:

```bash
ls -lh
```

Example:

```text
report.txt.gz

backup.tar.xz

logs.tar.bz2
```

Check file type:

```bash
file report.txt.gz
```

Output:

```text
gzip compressed data
```

The `file` command identifies the compression format.

---

# Compression Levels

Most tools support different compression levels.

Example:

```bash
gzip -1 report.txt
```

Fastest compression.

Maximum compression:

```bash
gzip -9 report.txt
```

Levels:

```text
-1  Fastest

-6  Default

-9  Highest compression
```

Higher compression usually takes more CPU time.

---

# Real-World Examples

Compress a log file:

```bash
gzip access.log
```

Compress a database backup:

```bash
xz database.sql
```

Compress source code:

```bash
bzip2 source.tar
```

Create and compress an archive:

```bash
tar -czf project.tar.gz project/
```

Create an XZ archive:

```bash
tar -cJf backup.tar.xz project/
```

These commands are frequently used in production environments.

---

# Common Mistakes

### Compressing an Already Compressed File

Example:

```text
video.mp4
```

Running:

```bash
gzip video.mp4
```

usually saves very little space.

Formats such as:

- MP4
- JPEG
- PNG
- ZIP

are already compressed.

---

### Forgetting the Original File is Removed

Command:

```bash
gzip report.txt
```

replaces:

```text
report.txt
```

with:

```text
report.txt.gz
```

Use:

```bash
gzip -k report.txt
```

if you want to keep both files.

---

### Choosing the Wrong Tool

For quick log rotation:

```text
gzip
```

is usually sufficient.

For long-term backups:

```text
xz
```

often provides the best storage savings.

---

# Why Compression Matters

Imagine you need to transfer a 5 GB backup over the network.

Compressing it first:

```bash
tar -cJf backup.tar.xz project/
```

may reduce the archive to 2 GB.

This saves:

- Disk space
- Network bandwidth
- Transfer time

Compression is therefore an important part of backup and deployment workflows.

---

# 🎯 Summary

Linux provides several compression tools.

Common commands:

```bash
gzip report.txt

gunzip report.txt.gz

bzip2 report.txt

bunzip2 report.txt.bz2

xz report.txt

unxz report.txt.xz

gzip -k report.txt

gzip -9 report.txt
```

Comparison:

```text
gzip   Fastest

bzip2  Better compression

xz      Highest compression
```

Understanding these tools helps you optimize storage, reduce transfer times, and create efficient backups for Linux systems.
