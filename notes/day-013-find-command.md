# Day 013 - Searching Files and Directories with find

## 🧠 Introduction

The `find` command is one of the most powerful tools in Linux.

It is used to search for files and directories based on various criteria such as:

- Name
- Type
- Size
- Modification date
- Permissions

System administrators and developers use `find` daily to locate files quickly across large systems.

---

## Basic Usage

Search for a file by name:

```bash
find . -name "notes.txt"
```

Example output:

```text
./notes/notes.txt
```

Explanation:

- `.` means start searching in the current directory.
- `-name` specifies the file name to search for.

---

System administrators and developers use `find` daily to locate files quickly across large systems.

---

## Basic Usage

Search for a file by name:

```bash
find . -name "notes.txt"
```

Example output:

```text
./notes/notes.txt
```

Explanation:

- `.` means start searching in the current directory.
- `-name` specifies the file name to search for.

---

## Searching from the Root Directory

Search the entire system:

```bash
find / -name "python3"
```

Example output:

```text
/usr/bin/python3
```

Note:

This may produce permission errors unless run with elevated privileges.

---

## Finding Directories

Search only for directories:

```bash
find . -type d
```

Output example:

```text
.
./notes
./projects
```

The option:

```bash
-type d
```

means "directory".

---

## Finding Files Only

Search only for files:

```bash
find . -type f
```

Output example:

```text
./README.md
./notes/day-013-find-command.md
```

The option:

```bash
-type f
```

means "file".

---

## Wildcard Searches

Find all Markdown files:

```bash
find . -name "*.md"
```

Example output:

```text
./README.md
./notes/day-001-what-is-linux.md
./notes/day-013-find-command.md
```

This is extremely useful in large projects.

---

## Searching Case-Insensitive

Normally:

```bash
find . -name "readme.md"
```

may not find:

```text
README.md
```

Instead use:

```bash
find . -iname "readme.md"
```

The `-iname` option ignores letter case.

---

## Finding Large Files

Find files larger than 100 MB:

```bash
find . -size +100M
```

Example output:

```text
./backups/archive.tar.gz
```

Useful when disk space is running low.

---

## Real-World Example

Find all Markdown notes in your Linux learning project:

```bash
find . -name "*.md"
```

Find the README file:

```bash
find . -name "README.md"
```

Find all directories:

```bash
find . -type d
```

These commands are commonly used in development environments.

---

## Common Mistakes

### Forgetting Quotes

Incorrect:

```bash
find . -name *.md
```

Correct:

```bash
find . -name "*.md"
```

Quotes prevent the shell from expanding the wildcard before `find` runs.

---

### Searching the Entire System Unnecessarily

Instead of:

```bash
find / -name "config.json"
```

use a smaller scope:

```bash
find ~/projects -name "config.json"
```

This is much faster.

---

## 🎯 Summary

The `find` command helps locate files and directories.

Common examples:

```bash
find . -name "file.txt"
find . -name "*.md"
find . -type f
find . -type d
find . -iname "readme.md"
find . -size +100M
```

Learning `find` is an important step toward becoming comfortable with Linux system administration and development workflows.
