# Day 006 - Creating Directories with mkdir

## 🧠 Introduction

The `mkdir` command stands for **Make Directory**.

It is used to create new directories (folders) in Linux.

Creating directories is one of the most common tasks when organizing projects, storing files, and managing system resources.

---

## Basic Usage

Create a directory:

```bash
mkdir projects
```

Verify it was created:

```bash
ls
```

Example output:

```text
Documents
Downloads
projects
```

---

## Creating Multiple Directories

You can create several directories at once:

```bash
mkdir project1 project2 project3
```

Result:

```text
project1
project2
project3
```

All three directories will be created in the current location.

---

## Creating Nested Directories

Sometimes you need a complete directory structure.

Without special options:

```bash
mkdir projects/linux/notes
```

This may fail if intermediate directories do not exist.

Instead use:

```bash
mkdir -p projects/linux/notes
```

The `-p` option creates all missing parent directories automatically.

Result:

```text
projects/
└── linux/
    └── notes/
```

---

## Real-World Example

Suppose you are starting a new Linux project.

Create a structured workspace:

```bash
mkdir -p my-project/{docs,src,logs}
```

Result:

```text
my-project/
├── docs
├── src
└── logs
```

This technique is commonly used by developers and system administrators.

---

## Checking Directory Creation

Use:

```bash
ls
```

or

```bash
ls -l
```

to verify that directories exist.

Example:

```bash
ls -l
```

Output:

```text
drwxr-xr-x 2 john users 4096 Jun 10 projects
```

The leading `d` indicates that the item is a directory.

---

## Common Mistakes

### Creating an Existing Directory

Running:

```bash
mkdir projects
```

when the directory already exists will produce:

```text
mkdir: cannot create directory 'projects': File exists
```

To avoid errors when creating nested directories, use:

```bash
mkdir -p projects
```

---

### Using Spaces Incorrectly

Incorrect:

```bash
mkdir my project
```

This creates two directories:

```text
my
project
```

Correct:

```bash
mkdir "my project"
```

or

```bash
mkdir my-project
```

---

## 🎯 Summary

The `mkdir` command creates directories.

Common examples:

```bash
mkdir projects
mkdir project1 project2
mkdir -p projects/linux/notes
```

The `-p` option is especially useful because it creates parent directories automatically and prevents unnecessary errors.
