# Day 030 - Understanding Linux Environment Variables

## 🧠 Introduction

Environment variables are one of the fundamental concepts in Linux.

They are named values that influence the behavior of:

- The shell
- Applications
- System services
- Programming languages
- Development tools

Many Linux programs depend on environment variables to determine:

- Where files are located
- Which editor to use
- User information
- Language settings
- Configuration paths

Understanding environment variables is essential for system administration, development, and DevOps.

---

## What Is an Environment Variable?

An environment variable consists of:

```text
NAME=VALUE
```

Example:

```bash
USER=john
```

Here:

```text
NAME  = USER
VALUE = john
```

Programs can read this information while running.

---

## Viewing All Environment Variables

Display every environment variable:

```bash
env
```

Example output:

```text
USER=john
HOME=/home/john
SHELL=/bin/bash
LANG=en_US.UTF-8
PATH=/usr/local/bin:/usr/bin:/bin
```

Another common command:

```bash
printenv
```

Both commands are widely used.

---

## Viewing a Specific Variable

Use:

```bash
echo $HOME
```

Example output:

```text
/home/john
```

Display the current user:

```bash
echo $USER
```

Example:

```text
john
```

The dollar sign (`$`) tells the shell to substitute the variable's value.

---

## Important Environment Variables

### HOME

Example:

```bash
echo $HOME
```

Output:

```text
/home/john
```

Represents the user's home directory.

---

### USER

Example:

```bash
echo $USER
```

Output:

```text
john
```

Contains the current username.

---

### SHELL

Example:

```bash
echo $SHELL
```

Output:

```text
/bin/bash
```

Indicates the active shell.

---

### LANG

Example:

```bash
echo $LANG
```

Output:

```text
en_US.UTF-8
```

Controls localization and language settings.

---

### PATH

One of the most important variables:

```bash
echo $PATH
```

Example:

```text
/usr/local/bin:/usr/bin:/bin
```

The shell searches these directories when executing commands.

---

## Understanding PATH

Suppose you type:

```bash
python
```

Linux searches directories in:

```text
$PATH
```

until it finds:

```text
/usr/bin/python
```

Without PATH, commands would need full paths:

```bash
/usr/bin/python
```

PATH makes command execution convenient.

---

## Temporary Variables

Create a variable:

```bash
MY_CITY=Istanbul
```

Access it:

```bash
echo $MY_CITY
```

Output:

```text
Istanbul
```

However, this variable exists only in the current shell session.

Closing the terminal removes it.

---

## Environment Variables vs Shell Variables

Example:

```bash
MY_VAR=hello
```

This creates a shell variable.

It is not automatically available to child processes.

To make it an environment variable:

```bash
export MY_VAR
```

We will explore `export` in the next lesson.

---

## Real-World Examples

Check your home directory:

```bash
echo $HOME
```

Inspect executable paths:

```bash
echo $PATH
```

View all variables:

```bash
env
```

Check your shell:

```bash
echo $SHELL
```

These commands are used daily by Linux administrators and developers.

---

## Why Environment Variables Matter

Many tools rely on them.

Examples:

```text
JAVA_HOME
PYTHONPATH
EDITOR
DATABASE_URL
API_KEY
```

Applications read these values during startup.

Changing a variable can completely alter a program's behavior.

This is especially important in:

- Docker containers
- CI/CD pipelines
- Cloud deployments
- Development environments

---

## Common Mistakes

### Forgetting the Dollar Sign

Wrong:

```bash
echo HOME
```

Output:

```text
HOME
```

Correct:

```bash
echo $HOME
```

Output:

```text
/home/john
```

---

### Confusing PATH with a Directory

PATH is not a single folder.

It is a list:

```text
dir1:dir2:dir3
```

Linux searches each directory sequentially.

---

### Expecting Temporary Variables to Persist

Example:

```bash
MY_VAR=test
```

After closing the terminal:

```text
MY_VAR disappears
```

Permanent variables require shell configuration files.

---

## 🎯 Summary

Environment variables store information used by Linux programs and shells.

Common commands:

```bash
env
printenv

echo $HOME
echo $USER
echo $PATH
echo $SHELL
```

Important variables:

```text
HOME   User home directory
USER   Current username
PATH   Executable search paths
SHELL  Active shell
LANG   Localization settings
```

Understanding environment variables is essential because modern Linux systems, development environments, cloud services, and automation tools depend heavily on them.
