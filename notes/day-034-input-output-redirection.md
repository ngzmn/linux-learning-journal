# Day 034 - Input and Output Redirection

## 🧠 Introduction

Every Linux command communicates using three standard data streams:

```text
Standard Input  (stdin)
Standard Output (stdout)
Standard Error  (stderr)
```

By default:

- Input comes from the keyboard.
- Output is displayed on the terminal.
- Errors are also shown on the terminal.

Redirection allows you to change this behavior by sending input or output to files instead of the screen.

This is one of the most important concepts in Bash and shell scripting.

---

## Understanding the Three Standard Streams

Each stream has a file descriptor:

```text
0 = stdin
1 = stdout
2 = stderr
```

Although these numbers are often hidden, they become useful when redirecting output.

---

## Redirecting Standard Output

Use the `>` operator to send output to a file.

Example:

```bash
ls > files.txt
```

Instead of displaying the directory contents on the screen, Linux writes them into:

```text
files.txt
```

If the file does not exist, it is created.

If it already exists, it is overwritten.

---

## Appending Output

Sometimes you want to keep the existing contents.

Use:

```bash
ls >> files.txt
```

The new output is added to the end of the file instead of replacing it.

Difference:

```text
>   Overwrite

>>  Append
```

---

## Redirecting Standard Input

Use the `<` operator.

Example:

```bash
sort < names.txt
```

Instead of waiting for keyboard input, the `sort` command reads data directly from the file.

This is useful for scripts and automation.

---

## Redirecting Standard Error

Errors can be redirected separately.

Example:

```bash
ls missing_directory 2> errors.txt
```

Instead of displaying:

```text
No such file or directory
```

the error message is written to:

```text
errors.txt
```

The normal output is unaffected.

---

## Redirecting Both Output and Errors

Save both streams in the same file:

```bash
ls existing missing > output.txt 2>&1
```

Explanation:

```text
> output.txt   Save stdout

2>&1           Send stderr to the same place as stdout
```

This technique is commonly used in automation and logging.

---

## Discarding Output

Sometimes you do not care about the output.

Linux provides a special file:

```text
/dev/null
```

Example:

```bash
ls missing_directory 2> /dev/null
```

Errors disappear.

Discard everything:

```bash
command > /dev/null 2>&1
```

This is useful for silent execution.

---

## Real-World Examples

Save a directory listing:

```bash
ls -lh > directory.txt
```

Append running processes to a log:

```bash
ps aux >> processes.log
```

Save disk usage:

```bash
df -h > disk_usage.txt
```

Suppress errors:

```bash
find / -name test 2> /dev/null
```

Redirect both output and errors:

```bash
bash backup.sh > backup.log 2>&1
```

These patterns appear frequently in production systems.

---

## Common Mistakes

### Accidentally Overwriting Files

Running:

```bash
echo Hello > notes.txt
```

replaces everything inside:

```text
notes.txt
```

If you intended to keep the existing contents, use:

```bash
echo Hello >> notes.txt
```

---

### Redirecting Only Standard Output

Example:

```bash
ls missing > output.txt
```

The error still appears on the screen because it is sent to:

```text
stderr
```

Redirect it separately if needed.

---

### Forgetting /dev/null

Many scripts produce unnecessary output.

Instead of displaying everything:

```bash
command > /dev/null 2>&1
```

keeps execution silent.

---

## Why Redirection Matters

Imagine creating a daily server report.

Instead of manually copying terminal output:

```bash
df -h > report.txt

free -h >> report.txt

uptime >> report.txt
```

You now have a neatly formatted report stored in a file.

This approach is widely used in monitoring, automation, and scheduled tasks.

---

## 🎯 Summary

Redirection changes where commands receive input and send output.

Common examples:

```bash
ls > files.txt

ls >> files.txt

sort < names.txt

ls missing 2> errors.txt

command > output.log 2>&1

command > /dev/null 2>&1
```

Important operators:

```text
>     Redirect stdout (overwrite)

>>    Redirect stdout (append)

<     Redirect stdin

2>    Redirect stderr

2>&1  Combine stderr with stdout

/dev/null  Discard unwanted output
```

Mastering input and output redirection is essential because shell scripting, automation, logging, and system administration all rely heavily on controlling command input and output.
