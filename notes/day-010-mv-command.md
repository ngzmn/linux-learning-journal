# Day 010 - Moving and Renaming Files with mv

## 🧠 Introduction

The `mv` command stands for **move**.

It is used to:

- Move files between directories
- Move directories between locations
- Rename files and directories

Unlike `cp`, the `mv` command does not create a copy. It transfers the original file to a new location.

---

## Basic Usage

Move a file:

```bash
mv file.txt documents/
```

Result:

```text
file.txt
```

will no longer exist in the current directory.

Instead, it will be located inside:

```text
documents/
```

---

## Renaming Files

The `mv` command is also used to rename files.

Example:

```bash
mv notes.txt linux-notes.txt
```

Result:

```text
notes.txt
```

becomes:

```text
linux-notes.txt
```

No copy is created. The file simply gets a new name.

---

## Moving Multiple Files

Move several files into another directory:

```bash
mv file1.txt file2.txt file3.txt backup/
```

All files will be transferred to the backup directory.

---

## Moving Directories

You can move entire directories:

```bash
mv project archive/
```

Result:

```text
archive/project
```

The entire directory and its contents are moved.

---

## Useful Options

### mv -i

Interactive mode.

```bash
mv -i file.txt backup/
```

Linux asks before overwriting an existing file.

Example:

```text
overwrite 'backup/file.txt'?
```

---

### mv -v

Verbose mode.

```bash
mv -v file.txt backup/
```

Output:

```text
renamed 'file.txt' -> 'backup/file.txt'
```

Useful when moving many files.

---

## Real-World Example

Rename a project file:

```bash
mv draft-report.md final-report.md
```

Move project backups:

```bash
mv linux-learning-journal-backup backups/
```

These are common tasks for developers and system administrators.

---

## Common Mistakes

### Accidentally Overwriting Files

If a destination file already exists:

```bash
mv report.txt backup/report.txt
```

it may be replaced.

Safer approach:

```bash
mv -i report.txt backup/
```

---

### Thinking mv Creates Copies

Many beginners confuse `mv` with `cp`.

Remember:

```bash
cp
```

creates a duplicate.

```bash
mv
```

moves the original.

---

## Comparing cp and mv

Copy:

```bash
cp report.txt backup/
```

Result:

```text
report.txt
backup/report.txt
```

Both files exist.

Move:

```bash
mv report.txt backup/
```

Result:

```text
backup/report.txt
```

The original location becomes empty.

---

## 🎯 Summary

The `mv` command is used to move and rename files and directories.

Common examples:

```bash
mv file.txt documents/
mv notes.txt linux-notes.txt
mv project archive/
mv -i file.txt backup/
```

It is one of the most important Linux commands for organizing files and managing projects.
