# Day 037 - Text Processing with cut and paste

## 🧠 Introduction

Many Linux files store structured data.

Examples include:

- CSV files
- Configuration files
- Log files
- `/etc/passwd`
- Command output

Instead of reading entire lines, you often need only specific columns or fields.

Linux provides two useful commands for this purpose:

- `cut`
- `paste`

The `cut` command extracts selected parts of a line, while the `paste` command combines data from multiple files.

These commands are widely used in shell scripts and automation.

---

# The cut Command

The `cut` command extracts portions of each line from a file.

Basic syntax:

```bash
cut OPTION file
```

It can extract:

- Characters
- Bytes
- Fields

---

## Extracting Characters

Suppose a file contains:

```text
Linux
Ubuntu
Fedora
```

Extract the first three characters:

```bash
cut -c1-3 systems.txt
```

Output:

```text
Lin
Ubu
Fed
```

Option:

```text
-c = characters
```

---

## Extracting Fields

Suppose a CSV file contains:

```text
Alice,25,Developer
Bob,31,Designer
Charlie,28,Engineer
```

Extract the first field:

```bash
cut -d',' -f1 users.csv
```

Output:

```text
Alice
Bob
Charlie
```

Explanation:

```text
-d = delimiter

-f = field number
```

---

## Extracting Multiple Fields

Example:

```bash
cut -d',' -f1,3 users.csv
```

Output:

```text
Alice,Developer
Bob,Designer
Charlie,Engineer
```

This is useful when working with CSV files.

---

## Real Example: /etc/passwd

Each line in `/etc/passwd` contains several fields separated by colons.

Example:

```text
john:x:1000:1000:John:/home/john:/bin/bash
```

Extract usernames:

```bash
cut -d':' -f1 /etc/passwd
```

Extract login shells:

```bash
cut -d':' -f7 /etc/passwd
```

This is a very common Linux administration task.

---

# The paste Command

The `paste` command combines lines from multiple files.

Suppose:

**names.txt**

```text
Alice
Bob
Charlie
```

**cities.txt**

```text
London
Paris
Rome
```

Run:

```bash
paste names.txt cities.txt
```

Output:

```text
Alice   London
Bob     Paris
Charlie Rome
```

By default, fields are separated by tabs.

---

## Custom Delimiters

Use:

```bash
paste -d',' names.txt cities.txt
```

Output:

```text
Alice,London
Bob,Paris
Charlie,Rome
```

Option:

```text
-d = delimiter
```

---

# Combining cut with Other Commands

Extract usernames and sort them:

```bash
cut -d':' -f1 /etc/passwd | sort
```

Count users:

```bash
cut -d':' -f1 /etc/passwd | wc -l
```

Find unique login shells:

```bash
cut -d':' -f7 /etc/passwd | sort | uniq
```

These pipelines are common in server administration.

---

# Real-World Examples

Extract IP addresses:

```bash
cut -d' ' -f1 access.log
```

Display only filenames:

```bash
ls -l | cut -d' ' -f9
```

Combine two reports:

```bash
paste report1.txt report2.txt
```

Extract usernames:

```bash
cut -d':' -f1 /etc/passwd
```

These techniques save time when processing structured text.

---

# Common Mistakes

### Using the Wrong Delimiter

CSV uses:

```text
,
```

`/etc/passwd` uses:

```text
:
```

Always verify the correct delimiter.

---

### Counting Spaces Incorrectly

Some files use multiple spaces or tabs.

Using:

```bash
cut -d' '
```

may not produce the expected result.

Choose the delimiter carefully.

---

### Expecting cut to Reorder Fields

The `cut` command only extracts fields.

It does not sort or rearrange data.

Use commands like:

```bash
sort
awk
```

for more advanced processing.

---

# Why These Commands Matter

Imagine you need a list of every username on a Linux server.

Instead of opening `/etc/passwd` manually:

```bash
cut -d':' -f1 /etc/passwd
```

Need to know how many users exist?

```bash
cut -d':' -f1 /etc/passwd | wc -l
```

Need only unique login shells?

```bash
cut -d':' -f7 /etc/passwd | sort | uniq
```

These are real commands used by Linux administrators every day.

---

# 🎯 Summary

The `cut` and `paste` commands help process structured text.

Common examples:

```bash
cut -c1-5 file.txt

cut -d',' -f1 users.csv

cut -d':' -f1 /etc/passwd

paste names.txt cities.txt

paste -d',' names.txt cities.txt
```

Important options:

```text
-c   Select characters

-d   Specify delimiter

-f   Select field(s)

paste -d  Set output delimiter
```

Mastering `cut` and `paste` makes it much easier to process CSV files, configuration files, logs, and other structured text commonly found on Linux systems.
