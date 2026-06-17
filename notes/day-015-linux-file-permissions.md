# Day 015 - Understanding Linux File Permissions

## 🧠 Introduction

Linux is a multi-user operating system.

This means multiple users can access the same machine, so Linux needs a way to control who can read, modify, or execute files.

This control system is called **file permissions**.

Understanding permissions is essential for system administration, security, software development, and server management.

---

## Viewing Permissions

Use:

```bash
ls -l
```

Example output:

```text
-rw-r--r-- 1 john users 1250 Jun 17 notes.txt
```

The first part contains the permissions:

```text
-rw-r--r--
```

---

## Permission Structure

Example:

```text
-rw-r--r--
```

Breakdown:

```text
- rw- r-- r--
│ │   │   │
│ │   │   └── Others
│ │   └────── Group
│ └────────── Owner
└──────────── File Type
```

---

## File Types

The first character indicates the file type.

Examples:

```text
-  Regular file
d  Directory
l  Symbolic link
```

Example:

```text
drwxr-xr-x
```

means the item is a directory.

---

## Permission Types

Linux permissions are represented by three letters:

```text
r = Read
w = Write
x = Execute
```

---

## Owner Permissions

Example:

```text
rw-
```

Meaning:

- Read ✔
- Write ✔
- Execute ✖

The owner can read and modify the file.

---

## Group Permissions

Example:

```text
r--
```

Meaning:

- Read ✔
- Write ✖
- Execute ✖

Members of the file's group can only view the file.

---

## Others Permissions

Example:

```text
r--
```

Meaning:

- Read ✔
- Write ✖
- Execute ✖

All other users can read the file.

---

## Common Permission Examples

### Private File

```text
-rw-------
```

Only the owner has access.

---

### Shared Read-Only File

```text
-rw-r--r--
```

Owner can modify.

Everyone else can read.

---

### Executable Script

```text
-rwxr-xr-x
```

Owner can:

- Read
- Write
- Execute

Others can:

- Read
- Execute

---

## Real-World Example

Inspect permissions inside your project:

```bash
ls -l
```

Output:

```text
-rw-r--r-- README.md
drwxr-xr-x notes
```

Notice:

- Files often use `rw-r--r--`
- Directories often use `rwxr-xr-x`

These are common default permissions.

---

## Why Permissions Matter

Imagine a server configuration file:

```text
database-passwords.txt
```

If everyone can read it:

```text
-rw-r--r--
```

sensitive information may be exposed.

Permissions help protect important data.

---

## Common Mistakes

### Ignoring Permissions

Many beginners focus only on file contents.

In Linux, permissions are equally important.

---

### Confusing Directories and Files

Permissions work slightly differently on directories.

For example:

```text
x
```

on a directory allows entering it.

We'll explore this more later.

---

## 🎯 Summary

Linux permissions control access to files and directories.

Permission symbols:

```text
r = Read
w = Write
x = Execute
```

Permission groups:

```text
Owner
Group
Others
```

Useful command:

```bash
ls -l
```

Understanding permissions is a critical skill for anyone working with Linux systems.
