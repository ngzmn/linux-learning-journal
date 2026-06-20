# Day 018 - Managing Processes with ps

## 🧠 Introduction

A process is simply a running program.

Whenever you open an application, run a command, or start a service, Linux creates one or more processes.

The `ps` command stands for:

```text
process status
```

It is used to view information about currently running processes.

Understanding processes is an important step toward system administration, troubleshooting, and DevOps.

---

## Basic Usage

Display processes running in the current terminal:

```bash
ps
```

Example output:

```text
PID TTY          TIME CMD
3251 pts/0    00:00:00 bash
4127 pts/0    00:00:00 ps
```

Explanation:

- PID = Process ID
- TTY = Terminal
- TIME = CPU time used
- CMD = Command name

---

## Viewing All Processes

Show every running process:

```bash
ps -e
```

or

```bash
ps -A
```

Example:

```text
PID TTY          TIME CMD
1   ?        00:00:03 systemd
2   ?        00:00:00 kthreadd
...
```

This displays system-wide processes.

---

## Detailed Process Information

Use:

```bash
ps -ef
```

Example output:

```text
UID        PID  PPID CMD
root         1     0 systemd
john      3210  3120 bash
```

Additional columns include:

- UID = User running the process
- PID = Process ID
- PPID = Parent Process ID

This format is widely used by administrators.

---

## Using ps with grep

Search for a specific process:

```bash
ps -ef | grep ssh
```

Example output:

```text
root  1200  1  sshd
john  4521  3210 grep ssh
```

This is one of the most common Linux troubleshooting techniques.

---

## Understanding PID

Every process has a unique Process ID.

Example:

```text
PID 4520
```

Linux uses the PID to identify and manage processes.

Many commands such as:

```bash
kill
```

require a PID.

---

## Real-World Example

Check if a web server is running:

```bash
ps -ef | grep nginx
```

Check if Python is running:

```bash
ps -ef | grep python
```

Check if Docker is running:

```bash
ps -ef | grep docker
```

These commands are commonly used in production environments.

---

## Process Hierarchy

Linux processes form a tree structure.

Example:

```text
systemd (PID 1)
 ├── sshd
 ├── nginx
 └── bash
      └── python
```

Every process usually has a parent process.

The parent PID is shown as:

```text
PPID
```

in `ps -ef`.

---

## Common Mistakes

### Forgetting grep Matches Itself

Example:

```bash
ps -ef | grep python
```

Output may include:

```text
grep python
```

because grep itself is also running.

This is normal.

---

### Confusing PID and PPID

Example:

```text
PID  = Process ID
PPID = Parent Process ID
```

They are different values and serve different purposes.

---

## Useful Variations

Show processes for the current user:

```bash
ps -u $USER
```

Show processes in a tree format:

```bash
ps -ejH
```

Show CPU and memory information:

```bash
ps aux
```

Example:

```bash
ps aux | grep chrome
```

This format is extremely popular on Linux systems.

---

## 🎯 Summary

The `ps` command displays running processes.

Common examples:

```bash
ps
ps -e
ps -ef
ps aux
ps -ef | grep nginx
```

Important concepts:

```text
PID  = Process ID
PPID = Parent Process ID
UID  = Process Owner
```

Understanding processes is essential because almost every Linux server task involves monitoring, troubleshooting, or managing running processes.
