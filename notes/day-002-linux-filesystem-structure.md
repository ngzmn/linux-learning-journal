# Day 002 - Linux Filesystem Structure

## 🧠 Introduction

Unlike Windows, Linux does not use drive letters such as C:\ or D:\.

Everything in Linux starts from a single root directory:

```text
/
```

This root directory is the starting point of the entire filesystem.

All files, directories, storage devices, and mounted partitions exist somewhere under `/`.

---

## 📂 Important Directories

### /

The root directory.

This is the top-level directory of the Linux filesystem.

---

### /home

Contains personal files and directories for users.

Example:

```text
/home/john
/home/alice
```

---

### /root

Home directory of the root (administrator) user.

Example:

```text
/root
```

---

### /bin

Contains essential command-line programs.

Examples:

```bash
ls
cp
mv
cat
```

---

### /etc

Contains system configuration files.

Examples:

```text
/etc/passwd
/etc/hosts
```

---

### /var

Stores variable data such as:

- Logs
- Cache
- Temporary application data

Examples:

```text
/var/log
```

---

### /tmp

Temporary files are stored here.

Many programs use this directory during execution.

---

### /usr

Contains installed applications, libraries, and documentation.

This is one of the largest directories in a Linux system.

---

## 📌 Real Example

Check your current location:

```bash
pwd
```

Example output:

```text
/home/username
```

List top-level directories:

```bash
ls /
```

Example output:

```text
bin  boot  dev  etc  home  root  tmp  usr  var
```

---

## 🎯 Summary

Linux uses a single hierarchical filesystem that starts from `/`.

Important directories include:

- /home → User files
- /root → Root user's home
- /bin → Essential commands
- /etc → Configuration files
- /var → Logs and variable data
- /tmp → Temporary files
- /usr → Installed applications

Understanding these directories makes navigating Linux much easier.
