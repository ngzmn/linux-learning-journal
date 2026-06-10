# Day 008 - Viewing File Content with cat

## 🧠 Introduction

The `cat` command stands for **concatenate**.

It is used to display the content of files in the terminal.

It is one of the simplest and most frequently used Linux commands for reading files.

---

## Basic Usage

To display the content of a file:

```bash
cat file.txt
```

Example:

```bash
cat notes.txt
```

Output:

```text
This is a sample note file.
```

---

## Creating and Viewing at the Same Time

You can combine `cat` with redirection to create a file:

```bash
cat > hello.txt
```

Then type:

```text
Hello Linux!
```

Press `CTRL + D` to save.

Now view it:

```bash
cat hello.txt
```

---

## Appending Content

To add content without overwriting:

```bash
cat >> hello.txt
```

Then type:

```text
Another line added.
```

Press `CTRL + D`.

---

## Viewing Multiple Files

You can display multiple files at once:

```bash
cat file1.txt file2.txt
```

Output:

```text
Content of file1
Content of file2
```

---

## Real-World Use Case

Developers often use `cat` to:

- Quickly check logs
- View configuration files
- Debug scripts

Example:

```bash
cat /etc/hosts
```

---

## Common Mistakes

### Overwriting Files Accidentally

```bash
cat > file.txt
```

This will overwrite the file.

To avoid overwriting, use:

```bash
cat >> file.txt
```

---

### Using cat for Large Files

For very large files, `cat` is not ideal.

Instead, use:

```bash
less file.txt
```

or

```bash
more file.txt
```

---

## 🎯 Summary

The `cat` command is used to:

- View file contents
- Create files
- Append content
- Combine multiple files

Common commands:

```bash
cat file.txt
cat > file.txt
cat >> file.txt
cat file1 file2
```

It is a fundamental tool in Linux file handling.
