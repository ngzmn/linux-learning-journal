# Day 011 - Removing Files and Directories with rm

## 🧠 Introduction

The `rm` command stands for **remove**.

It is used to permanently delete files and directories from the filesystem.

Unlike the Recycle Bin in Windows, files deleted with `rm` are usually not easy to recover. For this reason, it is considered one of the most powerful and potentially dangerous Linux commands.

---

## Removing a File

Delete a file:

```bash
rm notes.txt
```

After running the command, the file is removed immediately.

Verify with:

```bash
ls
```

The file will no longer appear in the directory listing.

---

## Removing Multiple Files

Delete several files at once:

```bash
rm file1.txt file2.txt file3.txt
```

All specified files will be deleted.

---

## Interactive Mode

To avoid accidental deletion:

```bash
rm -i notes.txt
```

Example:

```text
rm: remove regular file 'notes.txt'?
```

Linux asks for confirmation before deleting the file.

---

## Removing Empty Directories

For empty directories, you can use:

```bash
rmdir old-folder
```

However, most users prefer using `rm` for both files and directories.

---

## Removing Directories Recursively

To delete a directory and everything inside it:

```bash
rm -r project
```

Example structure:

```text
project/
├── notes.txt
├── config.txt
└── docs/
```

After running:

```bash
rm -r project
```

the entire directory and all contents are removed.

---

## Force Deletion

Use:

```bash
rm -f file.txt
```

The `-f` option means **force**.

Linux will not ask for confirmation.

You can combine options:

```bash
rm -rf project
```

This command recursively and forcefully deletes a directory and everything inside it.

---

## Real-World Example

Remove temporary files:

```bash
rm temp.txt
```

Delete an old backup:

```bash
rm -r linux-learning-journal-backup
```

Clean up log files:

```bash
rm *.log
```

---

## Common Mistakes

### Using rm -rf Carelessly

This command:

```bash
rm -rf important-folder
```

can permanently delete valuable data.

Always double-check the path before pressing Enter.

---

### Deleting the Wrong File

Before deleting, inspect files:

```bash
ls
```

or

```bash
ls -l
```

This helps prevent mistakes.

---

## Best Practice

When unsure, use:

```bash
rm -i filename
```

instead of:

```bash
rm filename
```

Interactive mode provides an extra layer of safety.

---

## 🎯 Summary

The `rm` command is used to delete files and directories.

Common examples:

```bash
rm file.txt
rm file1.txt file2.txt
rm -i file.txt
rm -r project
rm -rf project
```

It is one of the most powerful commands in Linux and should always be used carefully.
