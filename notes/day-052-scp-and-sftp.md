# Day 052 - Secure File Transfer with `scp` and `sftp`

## 🧠 Introduction

After learning SSH, the next logical step is learning how to transfer files securely between Linux machines.

Two of the most common tools are:

- `scp` (Secure Copy)
- `sftp` (SSH File Transfer Protocol)

Both tools use the SSH protocol, meaning all transferred data is encrypted.

These commands are widely used for:

- Uploading website files
- Downloading server logs
- Backing up configuration files
- Transferring project files
- Managing remote servers

---

# What is SCP?

`scp` is a command-line utility that copies files between computers over SSH.

General syntax:

```bash
scp source destination
```

Example:

```bash
scp report.txt john@192.168.1.100:/home/john/
```

This uploads `report.txt` to the remote server.

---

# Downloading Files

Copy a file from a remote server to your local machine:

```bash
scp john@192.168.1.100:/home/john/report.txt .
```

Here:

```text
. = Current directory
```

The file is downloaded into your current working directory.

---

# Copying Directories

To copy an entire directory:

```bash
scp -r project/ john@server:/home/john/
```

Option:

```text
-r = Recursive
```

Without `-r`, SCP cannot copy directories.

---

# Using a Custom SSH Port

If the SSH server uses a different port:

```bash
scp -P 2222 report.txt john@server:/home/john/
```

Option:

```text
-P = Port
```

Notice that SCP uses an uppercase `-P`.

---

# Preserving File Attributes

Keep timestamps and permissions:

```bash
scp -p report.txt john@server:/home/john/
```

Option:

```text
-p = Preserve timestamps and permissions
```

---

# What is SFTP?

SFTP stands for **SSH File Transfer Protocol**.

Unlike SCP, SFTP provides an interactive shell for browsing and managing remote files.

Start a session:

```bash
sftp john@192.168.1.100
```

You will enter an interactive prompt:

```text
sftp>
```

---

# Common SFTP Commands

Display remote directory:

```bash
pwd
```

Display local directory:

```bash
lpwd
```

List remote files:

```bash
ls
```

Change remote directory:

```bash
cd Documents
```

Change local directory:

```bash
lcd Downloads
```

These commands work similarly to a Linux shell.

---

# Uploading Files with SFTP

Upload a file:

```bash
put report.txt
```

Upload a directory:

```bash
put -r project/
```

---

# Downloading Files with SFTP

Download a file:

```bash
get report.txt
```

Download an entire directory:

```bash
get -r project/
```

---

# Exiting SFTP

Leave the session:

```bash
exit
```

or

```bash
bye
```

---

# SCP vs SFTP

| Feature | SCP | SFTP |
|---------|-----|------|
| Copy files | ✅ | ✅ |
| Interactive shell | ❌ | ✅ |
| Browse directories | ❌ | ✅ |
| Resume transfers | Limited | Better |
| Easy scripting | ✅ | Possible |
| File management | ❌ | ✅ |

Rule of thumb:

- Need a quick copy → **SCP**
- Need to browse and manage files → **SFTP**

---

# Real-World Examples

Upload a backup:

```bash
scp backup.tar.gz admin@server:/backups/
```

Download logs:

```bash
scp admin@server:/var/log/syslog .
```

Copy an entire project:

```bash
scp -r website/ admin@server:/var/www/
```

Start an SFTP session:

```bash
sftp admin@server
```

Upload a configuration file:

```bash
put nginx.conf
```

Download log files:

```bash
get access.log
```

These are common tasks in Linux administration.

---

# Common Mistakes

### Forgetting `-r`

Incorrect:

```bash
scp project/ server:/backup/
```

Correct:

```bash
scp -r project/ server:/backup/
```

---

### Using the Wrong Port Option

SSH:

```bash
ssh -p 2222 server
```

SCP:

```bash
scp -P 2222 file.txt server:/tmp/
```

Notice the uppercase `P` for SCP.

---

### Confusing Local and Remote Paths

Remember:

```text
Local file → No hostname

Remote file → username@hostname:path
```

Example:

```bash
scp notes.txt john@server:/home/john/
```

---

# Why SCP and SFTP Matter

Imagine you've updated your website locally.

Instead of using a USB drive or an insecure protocol, simply run:

```bash
scp -r website/ admin@server:/var/www/html/
```

Or connect with:

```bash
sftp admin@server
```

to browse, upload, download, rename, or delete files securely.

Because both tools use SSH, your data remains encrypted during transfer.

---

# 🎯 Summary

`scp` and `sftp` provide secure file transfers over SSH.

Common commands:

```bash
scp file.txt user@server:/home/user/

scp user@server:/home/user/file.txt .

scp -r project/ user@server:/home/user/

scp -P 2222 file.txt user@server:/tmp/

sftp user@server

put file.txt

get file.txt

exit
```

Important options:

```text
-r      Copy directories recursively

-P      Specify SSH port

-p      Preserve timestamps and permissions

put     Upload files in SFTP

get     Download files in SFTP

exit    Close the SFTP session
```

Mastering `scp` and `sftp` allows you to securely transfer files, deploy applications, manage servers remotely, and perform encrypted file operations with confidence.
