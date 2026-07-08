# Day 035 - Pipes and the Pipe (`|`) Operator

## 🧠 Introduction

The pipe (`|`) is one of the most powerful features of Linux.

Instead of saving the output of one command to a file and then reading that file with another command, a pipe connects commands directly.

It sends the output of one command to the input of another command.

```text
Command A --> Command B
```

This makes command-line workflows:

- Faster
- Cleaner
- More efficient
- Easier to automate

Pipes are used constantly by Linux users, system administrators, and DevOps engineers.

---

## Basic Syntax

```bash
command1 | command2
```

Meaning:

```text
stdout of command1
        ↓
stdin of command2
```

Instead of displaying the output on the screen, Linux passes it directly to the next command.

---

## Example 1: Count Files

List files and count them:

```bash
ls | wc -l
```

Explanation:

```text
ls
```

lists files.

```text
wc -l
```

counts the number of lines.

If the directory contains:

```text
file1.txt
file2.txt
notes/
README.md
```

Output:

```text
4
```

---

## Example 2: Search Output

List files and search for Markdown files:

```bash
ls | grep ".md"
```

Example output:

```text
README.md
notes.md
```

Instead of manually reading the list, `grep` filters it automatically.

---

## Example 3: Find Running Processes

Show only Git processes:

```bash
ps aux | grep git
```

Example output:

```text
john   4211  git status
```

This is one of the most common Linux commands.

---

## Example 4: Sort Results

Sort file names alphabetically:

```bash
ls | sort
```

Reverse order:

```bash
ls | sort -r
```

Sorting becomes very useful when processing large datasets.

---

## Example 5: Remove Duplicate Lines

Suppose a file contains:

```text
apple
banana
apple
orange
banana
```

Run:

```bash
sort fruits.txt | uniq
```

Output:

```text
apple
banana
orange
```

Notice that `uniq` works best on sorted input.

---

## Chaining Multiple Pipes

Pipes can be chained together.

Example:

```bash
ps aux | grep ssh | sort
```

Or:

```bash
cat access.log | grep ERROR | sort | uniq
```

Each command processes the output from the previous one.

This modular design is one of Linux's greatest strengths.

---

## Real-World Examples

Count installed packages:

```bash
dpkg -l | wc -l
```

Find open SSH connections:

```bash
ss -t | grep ssh
```

Count Markdown files:

```bash
find . -name "*.md" | wc -l
```

Display the five largest directories:

```bash
du -h | sort -h | tail -5
```

These commands are frequently used in production environments.

---

## Pipe vs Redirection

Pipe:

```bash
ls | grep ".txt"
```

The output goes directly to another command.

Redirection:

```bash
ls > files.txt
```

The output is written to a file.

Think of it this way:

```text
Pipe        → Another command

Redirection → A file
```

---

## Common Mistakes

### Forgetting Spaces

Correct:

```bash
ls | wc -l
```

Incorrect:

```bash
ls|wc -l
```

Although Bash usually accepts it, adding spaces greatly improves readability.

---

### Using cat Unnecessarily

Instead of:

```bash
cat file.txt | grep Linux
```

You can write:

```bash
grep Linux file.txt
```

This is simpler and more efficient.

However, `cat` is useful when combining multiple inputs.

---

### Confusing Pipes with Logical Operators

Pipe:

```bash
|
```

Logical OR:

```bash
||
```

They have completely different purposes.

---

## Why Pipes Matter

Imagine you want to find the five largest log files.

Instead of performing several manual steps, you can use:

```bash
find /var/log -type f | xargs du -h | sort -h | tail -5
```

A complex task becomes a single command.

This is why experienced Linux users often solve problems by combining simple commands with pipes.

---

## 🎯 Summary

The pipe operator (`|`) connects commands together.

Common examples:

```bash
ls | wc -l

ls | grep ".md"

ps aux | grep ssh

find . -name "*.txt" | wc -l

du -h | sort -h | tail -5
```

Important concepts:

```text
|        Send output to another command
grep     Filter text
sort     Sort data
uniq     Remove duplicate lines
wc -l    Count lines
tail     Show the last lines
```

Mastering pipes is essential because they allow you to combine small Linux commands into powerful workflows for system administration, automation, log analysis, and software development.
