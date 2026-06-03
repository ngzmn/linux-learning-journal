# Day 003 - The pwd Command

## 🧠 Introduction

The `pwd` command stands for **Print Working Directory**.

It displays the full path of the directory you are currently working in.

This is one of the most frequently used Linux commands because it helps you understand your current location in the filesystem.

---

## Why is pwd Useful?

When navigating through multiple directories, it is easy to lose track of where you are.

The `pwd` command quickly shows your exact location.

Syntax:

```bash
pwd
```

Example output:

```text
/home/john/projects/linux-learning-journal
```

---

## Understanding the Output

Consider the following path:

```text
/home/john/projects/linux-learning-journal
```

This means:

* `/` → Root directory
* `home` → User home directory area
* `john` → Username
* `projects` → Projects folder
* `linux-learning-journal` → Current directory

---

## Real-World Usage

Imagine you have moved through several directories:

```bash
cd /home
cd john
cd projects
cd linux-learning-journal
cd notes
```

To verify your location:

```bash
pwd
```

Output:

```text
/home/john/projects/linux-learning-journal/notes
```

---

## Combining pwd with Other Commands

Create a new directory and verify your location:

```bash
mkdir test-directory
cd test-directory
pwd
```

Output:

```text
/home/john/projects/linux-learning-journal/notes/test-directory
```

---

## Common Mistake

Some beginners assume they are inside a specific directory without checking.

Running `pwd` before creating, deleting, or moving files can prevent mistakes.

---

## 🎯 Summary

The `pwd` command:

* Shows your current directory
* Helps you navigate the filesystem
* Prevents confusion while working in multiple locations
* Is one of the most useful commands for beginners

Remember:

```bash
pwd
```

Whenever you are unsure where you are in Linux.
