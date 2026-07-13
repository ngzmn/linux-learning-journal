# Day 040 - Text Processing with awk

## 🧠 Introduction

The `awk` command is one of the most powerful text-processing tools available on Linux.

It is designed to process structured text by working with rows and columns.

Unlike `grep`, which searches for patterns, or `sed`, which edits text, `awk` can:

- Extract columns
- Filter rows
- Perform calculations
- Format output
- Generate reports
- Process large text files

Because of its flexibility, `awk` is widely used in system administration, DevOps, data analysis, and shell scripting.

---

# Understanding Records and Fields

`awk` views text as:

- Records (lines)
- Fields (columns)

For example, consider the following file:

```text
Alice 25 Developer
Bob 31 Designer
Charlie 28 Engineer
```

Each line is a **record**.

Each word separated by spaces is a **field**.

```text
$1 = First field
$2 = Second field
$3 = Third field
```

---

# Basic Syntax

General syntax:

```bash
awk 'pattern { action }' file
```

If no pattern is provided, `awk` processes every line.

Example:

```bash
awk '{print $1}' users.txt
```

Output:

```text
Alice
Bob
Charlie
```

---

# Printing Multiple Fields

Display the first and third fields:

```bash
awk '{print $1, $3}' users.txt
```

Output:

```text
Alice Developer
Bob Designer
Charlie Engineer
```

---

# Printing the Entire Line

Use:

```bash
awk '{print $0}' users.txt
```

Here:

```text
$0 = Entire line
```

Output:

```text
Alice 25 Developer
Bob 31 Designer
Charlie 28 Engineer
```

---

# Using Custom Delimiters

Suppose a CSV file contains:

```text
Alice,25,Developer
Bob,31,Designer
Charlie,28,Engineer
```

Specify the delimiter:

```bash
awk -F',' '{print $1}' users.csv
```

Output:

```text
Alice
Bob
Charlie
```

Option:

```text
-F = field separator
```

---

# Filtering Data

Display users older than 30:

```bash
awk '$2 > 30 {print $1}' users.txt
```

Output:

```text
Bob
```

`awk` can compare numbers directly.

---

# Performing Calculations

Print salaries with tax:

```text
Alice 3000
Bob 4200
Charlie 2800
```

Command:

```bash
awk '{print $1, $2*0.9}' salaries.txt
```

Output:

```text
Alice 2700
Bob 3780
Charlie 2520
```

`awk` can perform arithmetic operations while processing data.

---

# Built-in Variables

Some useful variables include:

```text
NR  = Current record number

NF  = Number of fields

$0  = Entire record
```

Example:

```bash
awk '{print NR, $0}' users.txt
```

Output:

```text
1 Alice 25 Developer
2 Bob 31 Designer
3 Charlie 28 Engineer
```

Display the number of fields:

```bash
awk '{print NF}' users.txt
```

Output:

```text
3
3
3
```

---

# Combining awk with Pipes

Display running process names:

```bash
ps aux | awk '{print $11}'
```

Show usernames:

```bash
cut -d':' -f1 /etc/passwd | awk '{print $1}'
```

Display mounted filesystems:

```bash
df -h | awk '{print $1, $5}'
```

These commands are commonly used in system monitoring.

---

# Real-World Examples

Display disk usage percentages:

```bash
df -h | awk '{print $5}'
```

Extract usernames:

```bash
awk -F':' '{print $1}' /etc/passwd
```

Count records:

```bash
awk 'END {print NR}' users.txt
```

Display only active users:

```bash
awk '$3 == "Developer"' users.txt
```

Generate simple reports:

```bash
ps aux | awk '{print $1, $11}'
```

These examples demonstrate why `awk` is considered a reporting tool.

---

# Common Mistakes

### Forgetting the Field Separator

CSV files require:

```bash
-F','
```

Without it, the entire line becomes a single field.

---

### Using the Wrong Field Number

Remember:

```text
$1 = First field

$2 = Second field

$3 = Third field
```

Verify the file structure before writing commands.

---

### Confusing NR and NF

```text
NR = Current line number

NF = Number of fields on the current line
```

They represent different concepts.

---

# Why awk Matters

Imagine a server with thousands of running processes.

You only need:

- Process name
- CPU usage
- Memory usage

Instead of reading every column manually:

```bash
ps aux | awk '{print $11, $3, $4}'
```

Within seconds, you have a clean report.

This ability makes `awk` one of the most valuable tools for Linux professionals.

---

# 🎯 Summary

The `awk` command processes structured text efficiently.

Common examples:

```bash
awk '{print $1}' file.txt

awk '{print $1, $3}' file.txt

awk -F',' '{print $2}' users.csv

awk '$2 > 30 {print $1}' users.txt

awk '{print NR, $0}' file.txt

awk 'END {print NR}' file.txt
```

Important concepts:

```text
$0   Entire line

$1   First field

$2   Second field

NR   Current record number

NF   Number of fields

-F   Field separator
```

Mastering `awk` enables advanced reporting, automation, log analysis, and structured data processing, making it one of the most powerful utilities in the Linux command line.
