# Day 036 - Text Processing with sort, uniq, and wc

## 🧠 Introduction

Linux provides many powerful text-processing utilities.

Three of the most useful are:

- `sort`
- `uniq`
- `wc`

These commands are often combined with pipes to analyze log files, configuration files, datasets, and command output.

Learning them is an essential step toward becoming proficient with the Linux command line.

---

# The sort Command

The `sort` command arranges lines of text in alphabetical or numerical order.

Basic syntax:

```bash
sort filename
```

Example file:

```text
orange
banana
apple
grape
```

Command:

```bash
sort fruits.txt
```

Output:

```text
apple
banana
grape
orange
```

---

## Reverse Sorting

Use:

```bash
sort -r fruits.txt
```

Output:

```text
orange
grape
banana
apple
```

Option:

```text
-r = reverse order
```

---

## Numeric Sorting

Suppose a file contains:

```text
15
100
8
42
```

Running:

```bash
sort numbers.txt
```

Produces:

```text
100
15
42
8
```

Because the values are sorted alphabetically.

Instead use:

```bash
sort -n numbers.txt
```

Output:

```text
8
15
42
100
```

Option:

```text
-n = numeric sort
```

---

# The uniq Command

The `uniq` command removes consecutive duplicate lines.

Example file:

```text
apple
apple
banana
banana
orange
```

Command:

```bash
uniq fruits.txt
```

Output:

```text
apple
banana
orange
```

Important:

`uniq` only removes adjacent duplicate lines.

For unsorted files, combine it with `sort`.

Example:

```bash
sort fruits.txt | uniq
```

---

## Counting Duplicate Lines

Use:

```bash
uniq -c
```

Example:

```bash
sort fruits.txt | uniq -c
```

Output:

```text
2 apple
3 banana
1 orange
```

Option:

```text
-c = count occurrences
```

---

# The wc Command

The `wc` command counts:

- Lines
- Words
- Characters

Example:

```bash
wc notes.txt
```

Output:

```text
25 180 1450 notes.txt
```

Meaning:

```text
25 lines
180 words
1450 characters
```

---

## Counting Only Lines

```bash
wc -l notes.txt
```

Example:

```text
25
```

---

## Counting Words

```bash
wc -w notes.txt
```

Example:

```text
180
```

---

## Counting Characters

```bash
wc -m notes.txt
```

Example:

```text
1450
```

---

# Combining These Commands

One of Linux's greatest strengths is combining simple commands.

Example:

```bash
cat names.txt | sort | uniq
```

Sorts names and removes duplicates.

Count unique names:

```bash
cat names.txt | sort | uniq | wc -l
```

Find the most common usernames:

```bash
cut -d: -f1 /etc/passwd | sort | uniq -c
```

---

# Real-World Examples

Sort installed packages:

```bash
dpkg -l | sort
```

Count running processes:

```bash
ps aux | wc -l
```

Count unique IP addresses in a log:

```bash
cut -d' ' -f1 access.log | sort | uniq -c
```

Count Markdown files:

```bash
find . -name "*.md" | wc -l
```

These commands are frequently used by system administrators and developers.

---

# Common Mistakes

### Using uniq Without Sorting

Incorrect:

```bash
uniq file.txt
```

Duplicate lines separated by other lines remain.

Better:

```bash
sort file.txt | uniq
```

---

### Forgetting Numeric Sort

Incorrect:

```bash
sort numbers.txt
```

Correct:

```bash
sort -n numbers.txt
```

Always use `-n` when sorting numbers.

---

### Confusing Characters and Bytes

`wc -m`

Counts characters.

`wc -c`

Counts bytes.

For plain English text, the numbers are often the same.

For UTF-8 text, such as Persian or Japanese, they may differ.

---

# Why These Commands Matter

Imagine a web server log containing millions of lines.

You want to know:

- How many requests were made?
- Which IP address appears most often?
- How many unique users visited?

Using:

```bash
sort

uniq

wc
```

you can answer these questions with only a few commands.

This is why these tools are fundamental in Linux system administration and data processing.

---

# 🎯 Summary

The `sort`, `uniq`, and `wc` commands are essential for processing text.

Common examples:

```bash
sort file.txt

sort -n numbers.txt

sort file.txt | uniq

sort file.txt | uniq -c

wc file.txt

wc -l file.txt

wc -w file.txt

find . -name "*.md" | wc -l
```

Important options:

```text
sort -r   Reverse order

sort -n   Numeric sort

uniq -c   Count duplicate lines

wc -l     Count lines

wc -w     Count words

wc -m     Count characters
```

Mastering these commands enables efficient text analysis, log processing, automation, and shell scripting, making them indispensable tools for Linux professionals.
