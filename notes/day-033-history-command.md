# Day 033 - Command History and the history Command

## 🧠 Introduction

Every command you execute in a Linux terminal is typically saved in your shell history.

This allows you to:

- Recall previous commands
- Avoid typing long commands repeatedly
- Search for commands you've used before
- Re-run commands quickly
- Improve productivity

The Bash shell stores command history in a file located in your home directory.

```text
~/.bash_history
```

Learning to use command history efficiently is one of the easiest ways to become more productive on Linux.

---

## Viewing Command History

Display your command history:

```bash
history
```

Example output:

```text
1  pwd
2  ls
3  cd projects
4  git status
5  nano README.md
```

Each command has a unique history number.

---

## Viewing the Last Commands

Display only the last 10 commands:

```bash
history 10
```

Example:

```text
421 git pull
422 ls
423 cd notes
424 nano day-033-history-command.md
```

This is useful when your history contains hundreds or thousands of commands.

---

## Re-running Commands

Execute a command again using its history number.

Example:

```bash
!423
```

This immediately runs:

```bash
cd notes
```

without typing it again.

---

## Repeating the Previous Command

Run the last command again:

```bash
!!
```

Example:

```bash
sudo !!
```

Suppose you forgot to use `sudo`:

```bash
apt update
```

Permission denied.

Instead of typing everything again:

```bash
sudo !!
```

Bash expands it to:

```bash
sudo apt update
```

This is a favorite shortcut among Linux administrators.

---

## Searching Command History

Press:

```text
Ctrl + R
```

A search prompt appears:

```text
(reverse-i-search)
```

Type part of a previous command.

Example:

```text
git
```

The terminal searches backward through your history until it finds the most recent matching command.

Press:

```text
Ctrl + R
```

again to continue searching older matches.

Press:

```text
Enter
```

to execute the selected command.

---

## Searching with history and grep

You can also search manually:

```bash
history | grep git
```

Example output:

```text
115 git status
142 git add .
143 git commit -m "Update README"
```

Another example:

```bash
history | grep ssh
```

This helps locate previously used commands quickly.

---

## Clearing History

Clear the current shell history:

```bash
history -c
```

This removes history from the current session.

To also clear the history file:

```bash
history -w
```

Be careful, as this action may permanently overwrite your saved history.

---

## Understanding ~/.bash_history

Bash stores history in:

```text
~/.bash_history
```

View its contents:

```bash
cat ~/.bash_history
```

Count the number of saved commands:

```bash
wc -l ~/.bash_history
```

This file is updated when the shell exits.

---

## Configuring History Size

Display the current limit:

```bash
echo $HISTSIZE
```

Example:

```text
1000
```

Increase it temporarily:

```bash
export HISTSIZE=5000
```

To make it permanent, add the command to:

```text
~/.bashrc
```

---

## Real-World Examples

Find previous Git commands:

```bash
history | grep git
```

Search for SSH sessions:

```bash
history | grep ssh
```

Run the previous command as root:

```bash
sudo !!
```

Open the history file:

```bash
cat ~/.bash_history
```

These techniques save significant time during daily work.

---

## Common Mistakes

### Forgetting Ctrl + R

Many beginners manually retype long commands.

Using:

```text
Ctrl + R
```

is much faster.

---

### Clearing History Accidentally

Running:

```bash
history -c
```

removes the current session's history.

Think carefully before clearing it.

---

### Storing Sensitive Commands

Commands containing passwords or sensitive tokens may appear in history.

For example:

```bash
mysql -u root -pMyPassword
```

Avoid passing secrets directly on the command line whenever possible.

---

## Why Command History Matters

Imagine you've used a long Docker command several days ago.

Instead of searching online again:

```text
Ctrl + R
docker
```

Within seconds, Bash finds the exact command.

This feature greatly improves efficiency for developers, DevOps engineers, and system administrators.

---

## 🎯 Summary

The `history` command helps you view, search, and reuse previously executed commands.

Common commands:

```bash
history
history 20

history | grep git

!!

!125

history -c

cat ~/.bash_history
```

Important concepts:

```text
history          Show command history
Ctrl + R         Interactive history search
!!               Repeat last command
!number          Execute a command by its history number
~/.bash_history  File where Bash stores command history
HISTSIZE         Maximum number of stored commands
```

Mastering command history makes everyday Linux work faster, more efficient, and less error-prone.
