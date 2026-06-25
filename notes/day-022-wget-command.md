# Day 022 - Downloading Files with wget

## 🧠 Introduction

The `wget` command is a non-interactive tool for downloading files from the internet.

It supports:

- HTTP
- HTTPS
- FTP

System administrators and DevOps engineers frequently use `wget` to download packages, scripts, backups, and installation files directly from the terminal.

Unlike a web browser, `wget` can run inside scripts and remote servers without a graphical interface.

---

## Basic Usage

Download a file:

```bash
wget https://example.com/file.zip
```

Example output:

```text
Saving to: 'file.zip'
100% [====================] 25M
```

The file is saved in the current directory.

---

## Downloading to a Specific File Name

Use:

```bash
wget -O latest.zip https://example.com/releases/v1.0.zip
```

The `-O` option specifies the output filename.

Result:

```text
latest.zip
```

instead of:

```text
v1.0.zip
```

---

## Resuming Interrupted Downloads

Suppose a large download stops unexpectedly.

Resume it with:

```bash
wget -c https://example.com/big-file.iso
```

The `-c` option means:

```text
continue
```

Only the remaining data is downloaded.

---

## Downloading in the Background

Start a download and return immediately to the shell:

```bash
wget -b https://example.com/archive.tar.gz
```

Example output:

```text
Continuing in background, pid 4210
```

Logs are written to:

```text
wget-log
```

---

## Limiting Download Speed

Avoid consuming all available bandwidth:

```bash
wget --limit-rate=500k https://example.com/file.iso
```

This limits the transfer speed to:

```text
500 KB/s
```

Useful on shared servers.

---

## Recursive Downloads

Download an entire website:

```bash
wget -r https://example.com
```

The `-r` option means:

```text
recursive
```

Be careful—this can download many files.

---

## Real-World Examples

Download a Linux ISO:

```bash
wget https://releases.ubuntu.com/24.04/ubuntu-24.04-desktop-amd64.iso
```

Download a script:

```bash
wget https://example.com/install.sh
```

Download and rename:

```bash
wget -O backup.tar.gz https://example.com/daily-backup.tar.gz
```

Resume a failed download:

```bash
wget -c big-dataset.zip
```

These tasks are common in server environments.

---

## Checking Downloaded Files

Verify:

```bash
ls -lh
```

Example output:

```text
-rw-r--r-- 1 john users 2.3G ubuntu.iso
```

Always confirm the file size after downloading large files.

---

## Common Mistakes

### Forgetting Quotes Around Complex URLs

Incorrect:

```bash
wget https://example.com/download?file=test&version=1
```

Safer:

```bash
wget "https://example.com/download?file=test&version=1"
```

---

### Restarting Large Downloads

Instead of:

```bash
wget file.iso
```

use:

```bash
wget -c file.iso
```

to continue incomplete downloads.

---

### Running Recursive Downloads Carelessly

This command:

```bash
wget -r https://example.com
```

can consume a lot of disk space.

Always understand what will be downloaded.

---

## wget vs Browser Downloads

### Browser

- Requires a graphical interface
- Manual interaction
- Difficult to automate

### wget

- Works on remote servers
- Script-friendly
- Supports resuming downloads
- Can run in the background

For Linux administration, `wget` is often the preferred solution.

---

## 🎯 Summary

The `wget` command downloads files from the internet.

Common examples:

```bash
wget https://example.com/file.zip
wget -O backup.zip URL
wget -c big.iso
wget -b archive.tar.gz
wget --limit-rate=500k URL
wget -r https://example.com
```

Important options:

```text
-O  Set output filename
-c  Continue downloads
-b  Background mode
-r  Recursive download
```

Learning `wget` is essential because downloading files from the terminal is a routine task in Linux, DevOps, and server management.
