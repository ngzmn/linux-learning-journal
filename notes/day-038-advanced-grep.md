# Day 038 - Advanced Text Searching with grep

## 🧠 Introduction

The `grep` command is one of the most frequently used tools in Linux.

It searches text for patterns and displays matching lines.

Whether you are:

- Searching log files
- Finding configuration settings
- Looking for errors
- Filtering command output
- Debugging applications

`grep` is an essential command.

Today we'll go beyond the basics and explore the most useful options used by Linux professionals.

---

# Basic Search

Search for a word inside a file:

```bash
grep "Linux" notes.txt
```

Output:

```text
Linux is an operating system.
Learning Linux is fun.
```

Only matching lines are displayed.

---

# Ignore Letter Case

Normally:

```bash
grep linux notes.txt
```

does **not** match:

```text
Linux
```

Use:

```bash
grep -i linux notes.txt
```

Option:

```text
-i = ignore case
```

Now it matches:

```text
Linux
LINUX
linux
LiNuX
```

---

# Show Line Numbers

Display matching lines together with their line numbers:

```bash
grep -n Linux notes.txt
```

Example:

```text
8:Linux is powerful.
21:Learning Linux is rewarding.
```

Option:

```text
-n = line numbers
```

Very useful when editing files.

---

# Search Recursively

Search every file inside a directory:

```bash
grep -r "TODO" .
```

Example output:

```text
notes/day1.md:TODO
scripts/install.sh:TODO
```

Option:

```text
-r = recursive
```

This is commonly used in software projects.

---

# Count Matches

Instead of displaying matching lines:

```bash
grep -c Linux notes.txt
```

Example:

```text
7
```

Option:

```text
-c = count matches
```

---

# Invert the Search

Show lines that **do not** contain a word:

```bash
grep -v "^#" config.conf
```

Example:

```text
server=localhost
port=8080
```

Comment lines beginning with:

```text
#
```

are excluded.

Option:

```text
-v = invert match
```

---

# Match Whole Words

Suppose the file contains:

```text
cat
catalog
category
```

Search:

```bash
grep cat words.txt
```

Matches all three.

Instead:

```bash
grep -w cat words.txt
```

Output:

```text
cat
```

Option:

```text
-w = whole words only
```

---

# Regular Expressions

`grep` supports regular expressions.

Find lines beginning with "L":

```bash
grep "^L" notes.txt
```

Find lines ending with "."

```bash
grep "\.$" notes.txt
```

Find blank lines:

```bash
grep "^$" notes.txt
```

These patterns are extremely useful in automation.

---

# Combining grep with Pipes

Search running SSH processes:

```bash
ps aux | grep ssh
```

Find Markdown files containing "Docker":

```bash
find . -name "*.md" | grep Docker
```

Search installed packages:

```bash
dpkg -l | grep python
```

This is one of the most common Linux workflows.

---

# Real-World Examples

Find failed SSH logins:

```bash
grep "Failed password" auth.log
```

Search configuration files:

```bash
grep -r "Listen" /etc/apache2
```

Count errors:

```bash
grep -c ERROR application.log
```

Ignore comments:

```bash
grep -v "^#" config.ini
```

Display line numbers:

```bash
grep -n TODO script.sh
```

These commands are used daily by system administrators.

---

# Common Mistakes

### Forgetting Quotes

Instead of:

```bash
grep Hello World file.txt
```

Use:

```bash
grep "Hello World" file.txt
```

This searches for the entire phrase.

---

### Forgetting Recursive Search

Searching only one file:

```bash
grep TODO README.md
```

Searching an entire project:

```bash
grep -r TODO .
```

Choose the correct approach.

---

### Confusing Regular Expressions

Remember:

```text
^ = beginning of line

$ = end of line

. = any character
```

These symbols are the foundation of pattern matching.

---

# Why grep Matters

Imagine a web server log containing one million lines.

You need to answer:

- Which requests failed?
- Which IP address appears?
- Which user logged in?
- Which configuration contains a specific option?

Instead of reading the file manually:

```bash
grep
```

finds the answer in seconds.

This is why `grep` is considered one of the most important Linux commands.

---

# 🎯 Summary

The `grep` command searches text using patterns.

Common examples:

```bash
grep Linux notes.txt

grep -i linux notes.txt

grep -n TODO script.sh

grep -r Docker .

grep -c ERROR app.log

grep -v "^#" config.conf

grep -w cat words.txt
```

Important options:

```text
-i   Ignore case

-n   Show line numbers

-r   Recursive search

-c   Count matches

-v   Invert match

-w   Match whole words
```

Understanding `grep` is essential because Linux administration, software development, security analysis, and log troubleshooting all rely heavily on fast and accurate text searching.
