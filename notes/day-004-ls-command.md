# Day 004 - The ls Command

## 🧠 Introduction

The `ls` command stands for **list**.

It is used to display files and directories inside a location in the Linux filesystem.

After learning `pwd`, the next logical step is learning how to see what exists inside a directory.

---

## Basic Usage

To list the contents of the current directory:

```bash
ls
```

Example output:

```text
Documents
Downloads
Pictures
notes
README.md
```

---

## Listing Another Directory

You can inspect a directory without entering it.

Example:

```bash
ls /home
```

Output:

```text
john
alice
```

This is useful when exploring the filesystem.

---


```bash
ls /home
```

Output:

```text
john
alice
```

This is useful when exploring the filesystem.

---

## Useful Options

### ls -l

Displays detailed information.

```bash
ls -l
```

Example output:

```text
-rw-r--r-- 1 john users 1200 Jun  5 README.md
drwxr-xr-x 2 john users 4096 Jun  5 notes
```

Information shown includes:

* Permissions
* Owner
* Group
* File size
* Modification date
* Name

---

### ls -a

Shows hidden files.

```bash
ls -a
```

Example output:

```text
.
..
.git
README.md
notes
```

Files beginning with a dot (`.`) are hidden by default.

---

### ls -la

One of the most commonly used combinations.

```bash
ls -la
```

This combines:

* Detailed view (`-l`)
* Hidden files (`-a`)

---

## Real-World Example

Inside your Git repository:

```bash
pwd
```

Output:

```text
/home/john/linux-learning-journal
```

Now run:

```bash
ls -la
```

You may see:

```text
.git
README.md
notes
```

Notice the `.git` directory.

This hidden directory contains all Git history and repository information.

---

## Common Mistakes

### Forgetting Hidden Files

Running:

```bash
ls
```

will not show hidden files.

Use:

```bash
ls -a
```

instead.

---

### Using cd When Not Necessary

Many beginners enter a directory just to inspect it.

Often this is enough:

```bash
ls /var/log
```

No need to change directories.

---

## 🎯 Summary

The `ls` command is used to view files and directories.

Common options:

```bash
ls
ls -l
ls -a
ls -la
```

Learning to use `ls` efficiently is one of the most important Linux navigation skills.

