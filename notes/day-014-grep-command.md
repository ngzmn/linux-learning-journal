# Day 014 - Searching Text with grep

## 🧠 Introduction

The `grep` command is one of the most powerful and frequently used tools in Linux.

It is used to search for specific words, patterns, or text inside files.

Developers, system administrators, and DevOps engineers use `grep` daily to analyze logs, search configuration files, and debug applications.

---

## Basic Usage

Search for a word inside a file:

```bash
grep "error" app.log
```

Example output:

```text
ERROR: Database connection failed
```

This command displays every line containing the word "error".

---

## Case-Insensitive Search

By default, grep is case-sensitive.

Example:

```bash
grep "error" app.log
```

may not find:

```text
ERROR
```

Use:

```bash
grep -i "error" app.log
```

The `-i` option ignores uppercase and lowercase differences.

---

## Display Line Numbers

Show matching lines with their line numbers:

```bash
grep -n "error" app.log
```

Example output:

```text
15:ERROR: Database connection failed
42:ERROR: Invalid credentials
```

This makes troubleshooting easier.

---

## Search Multiple Files

Search in several files at once:

```bash
grep "Linux" file1.txt file2.txt
```

Example output:

```text
file1.txt:Linux is open source
file2.txt:Linux powers many servers
```

---

## Recursive Search

Search through all files in a directory:

```bash
grep -r "TODO" .
```

Example output:

```text
./main.py:# TODO: add validation
./config.js:// TODO: update settings
```

The `-r` option means recursive.

This is extremely useful in software projects.

---

## Inverting a Search

Show lines that do NOT match:

```bash
grep -v "DEBUG" app.log
```

Example output:

```text
INFO: Server started
ERROR: Connection failed
```

Lines containing "DEBUG" are excluded.

---

## Counting Matches

Count matching lines:

```bash
grep -c "ERROR" app.log
```

Example output:

```text
12
```

This indicates that 12 lines contain the word "ERROR".

---

## Real-World Examples

Search for a username:

```bash
grep "john" users.txt
```

Search configuration files:

```bash
grep "port" config.ini
```

Search your Linux notes:

```bash
grep "Linux" notes/*.md
```

Search command history:

```bash
history | grep git
```

This displays previously executed Git commands.

---

## Common Mistakes

### Forgetting Quotes

Incorrect:

```bash
grep error log.txt
```

Usually works for simple words, but using quotes is safer:

```bash
grep "error" log.txt
```

---

### Searching the Wrong Directory

Instead of searching the entire filesystem:

```bash
grep -r "password" /
```

limit the search:

```bash
grep -r "password" ~/projects
```

This is much faster.

---

## Combining grep with Other Commands

One of grep's greatest strengths is working with pipes.

Example:

```bash
ls -la | grep ".md"
```

Output:

```text
README.md
notes.md
```

Another example:

```bash
ps aux | grep python
```

This shows running Python processes.

---

## 🎯 Summary

The `grep` command searches for text inside files and command output.

Common examples:

```bash
grep "error" app.log
grep -i "error" app.log
grep -n "error" app.log
grep -r "TODO" .
grep -v "DEBUG" app.log
history | grep git
```

Learning `grep` is essential because it is one of the most frequently used Linux commands in real-world environments.
