# Day 009 - Copying Files with cp

## 🧠 Introduction

The `cp` command stands for **copy**.

It is used to create copies of files and directories.

Instead of moving or modifying the original file, `cp` creates a duplicate while keeping the original intact.

This command is commonly used for backups, configuration management, and project organization.

---

## Basic Usage

Copy a file:

```bash
cp file.txt backup.txt
```

Result:

```text
file.txt
backup.txt
```

Both files contain the same content.

---

## Copying Files to Another Directory

Suppose you have:

```text
documents/
backup/
```

Copy a file into the backup directory:

```bash
cp documents/report.txt backup/
```

The original file remains unchanged.

---

## Copying Multiple Files

You can copy several files at once:

```bash
cp file1.txt file2.txt file3.txt backup/
```

All files will be copied into the backup directory.

---

## Copying Directories

By default, `cp` cannot copy directories.

This will fail:

```bash
cp my-project backup-project
```

Use the recursive option:

```bash
cp -r my-project backup-project
```

Example:

```text
my-project/
```

becomes:

```text
backup-project/
```

with all files and subdirectories included.

---

## Useful Options

### cp -r

Copy directories recursively.

```bash
cp -r source destination
```

---

### cp -i

Interactive mode.

```bash
cp -i file.txt backup.txt
```

If the destination file exists, Linux will ask before overwriting it.

---

### cp -v

Verbose mode.

```bash
cp -v file.txt backup.txt
```

Output:

```text
'file.txt' -> 'backup.txt'
```

Useful for understanding exactly what was copied.

---

## Real-World Example

Create a backup of your Linux learning journal:

```bash
cp -r linux-learning-journal linux-learning-journal-backup
```

Now you have a complete backup of your project.

---

## Common Mistakes

### Forgetting -r

Trying to copy a directory without `-r`:

```bash
cp project backup
```

Error:

```text
cp: -r not specified; omitting directory 'project'
```

Always use `-r` when copying directories.

---

### Accidentally Overwriting Files

This command:

```bash
cp report.txt backup.txt
```

will overwrite `backup.txt` if it already exists.

To be safer:

```bash
cp -i report.txt backup.txt
```

---

## 🎯 Summary

The `cp` command is used to copy files and directories.

Common examples:

```bash
cp file.txt backup.txt
cp file1.txt file2.txt backup/
cp -r project backup-project
cp -i file.txt backup.txt
```

It is one of the most important commands for backups and file management in Linux.
