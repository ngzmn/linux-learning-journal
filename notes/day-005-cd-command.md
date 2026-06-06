# Day 005 - The cd Command

## 🧠 Introduction

The `cd` command stands for **Change Directory**.

It is used to move between directories in the Linux filesystem.

If `pwd` tells you where you are and `ls` shows what is around you, then `cd` allows you to move to another location.

It is one of the most frequently used commands in Linux.

---

## Basic Usage

To enter a directory:

```bash
cd notes
```

If the directory exists, your current location will change to that directory.

Verify it with:

```bash
pwd
```

Example output:

```text
/home/john/linux-learning-journal/notes
```

---

## Moving Back One Directory

Use:

```bash
cd ..
```

The two dots (`..`) represent the parent directory.

Example:

Current location:

```text
/home/john/linux-learning-journal/notes
```

Run:

```bash
cd ..
```

New location:

```text
/home/john/linux-learning-journal
```

---

## Moving to Your Home Directory

You can return to your home directory at any time:

```bash
cd
```

or

```bash
cd ~
```

Example output from `pwd`:

```text
/home/john
```

---

## Using Absolute Paths

An absolute path starts from the root directory (`/`).

Example:

```bash
cd /var/log
```

This works regardless of your current location.

---

## Using Relative Paths

A relative path starts from your current directory.

Example:

```bash
cd notes
```

This only works if the `notes` directory exists inside your current location.

---

## Real-World Example

Navigate into your Linux learning project:

```bash
cd ~/linux-learning-journal
```

Then move into the notes directory:

```bash
cd notes
```

Check your location:

```bash
pwd
```

Example output:

```text
/home/john/linux-learning-journal/notes
```

---

## Common Mistakes

### Typing a Non-Existent Directory

```bash
cd myfolder
```

Error:

```text
No such file or directory
```

Always verify available directories using:

```bash
ls
```

---

### Forgetting Where You Are

Use:

```bash
pwd
```

before making important changes.

---

## 🎯 Summary

The `cd` command is used to move through the Linux filesystem.

Common examples:

```bash
cd notes
cd ..
cd ~
cd /var/log
```

Together with `pwd` and `ls`, the `cd` command forms the foundation of Linux navigation.
