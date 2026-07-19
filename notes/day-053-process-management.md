# Day 053 - Process Management with `ps`, `top`, and `htop`

## 🧠 Introduction

Every running program in Linux is called a **process**.

Whenever you open a terminal, launch a browser, start a web server, or execute a script, Linux creates one or more processes.

Managing processes is a fundamental skill because it allows you to:

- Monitor CPU usage
- Monitor memory usage
- Find running applications
- Stop unresponsive programs
- Troubleshoot server performance

Three of the most important tools are:

- `ps`
- `top`
- `htop`

---

# What is a Process?

Every process has a unique identifier called a **PID (Process ID)**.

Example:

```text
PID    COMMAND

1452   sshd

2138   nginx

4820   python3
```

The PID is used to identify and manage processes.

---

# The `ps` Command

The `ps` command displays information about running processes.

Basic syntax:

```bash
ps
```

Example output:

```text
PID TTY          TIME CMD

3261 pts/0    00:00:00 bash

3325 pts/0    00:00:00 ps
```

This only shows processes running in the current terminal.

---

# Show All Processes

Display every running process:

```bash
ps -e
```

or

```bash
ps -A
```

Both commands produce similar results.

---

# Full Process Information

A common command is:

```bash
ps aux
```

Columns include:

```text
USER

PID

%CPU

%MEM

COMMAND
```

Example:

```text
root      912   0.1   0.5   sshd

john     2018   4.3   2.1   firefox
```

This is one of the most frequently used Linux commands.

---

# Searching for a Process

Find a running process:

```bash
ps aux | grep nginx
```

Another example:

```bash
ps aux | grep python
```

This combines:

```text
ps

+

grep
```

to locate specific applications.

---

# The `top` Command

`top` provides a real-time view of system activity.

Run:

```bash
top
```

You'll see:

- CPU usage
- Memory usage
- Running processes
- System uptime
- Load average

The display refreshes automatically.

Press:

```text
q
```

to exit.

---

# Understanding the Top Display

Important fields:

```text
PID

USER

%CPU

%MEM

TIME+

COMMAND
```

These values help identify processes consuming excessive resources.

---

# Sorting Inside Top

While `top` is running:

```text
P
```

Sort by CPU usage.

```text
M
```

Sort by memory usage.

```text
T
```

Sort by running time.

These shortcuts are useful when troubleshooting performance.

---

# The `htop` Command

`htop` is an improved version of `top`.

Start it:

```bash
htop
```

Advantages:

- Colorful interface
- Easier navigation
- Mouse support
- Scrollable process list
- Interactive process management

If not installed:

Ubuntu/Debian:

```bash
sudo apt install htop
```

Fedora:

```bash
sudo dnf install htop
```

---

# Killing Processes

Sometimes a program becomes unresponsive.

Terminate it:

```bash
kill PID
```

Example:

```bash
kill 4820
```

If it refuses to stop:

```bash
kill -9 4820
```

Option:

```text
-9 = Force termination
```

Use this only when necessary.

---

# Killing by Process Name

Instead of finding the PID:

```bash
pkill firefox
```

Kill every Python process:

```bash
pkill python
```

This is often faster than using `kill`.

---

# Real-World Examples

Display all processes:

```bash
ps aux
```

Search for SSH:

```bash
ps aux | grep ssh
```

Monitor the system:

```bash
top
```

Launch the enhanced monitor:

```bash
htop
```

Terminate a process:

```bash
kill 2451
```

Force termination:

```bash
kill -9 2451
```

Kill by name:

```bash
pkill nginx
```

These commands are used daily on Linux servers.

---

# Common Mistakes

### Killing the Wrong Process

Always verify the PID:

```bash
ps aux | grep process_name
```

before running:

```bash
kill PID
```

---

### Overusing `kill -9`

`kill -9` immediately terminates a process without allowing it to clean up.

Try:

```bash
kill PID
```

first.

Only use `-9` if the process refuses to exit.

---

### Confusing CPU and Memory Usage

High CPU usage:

```text
Process is actively working.
```

High memory usage:

```text
Process is consuming RAM.
```

These indicate different types of resource consumption.

---

# Why Process Management Matters

Imagine your Linux server suddenly becomes slow.

A common troubleshooting workflow is:

View all processes:

```bash
ps aux
```

Monitor the system:

```bash
top
```

Identify the process using the most CPU.

Terminate it if necessary:

```bash
kill PID
```

Within minutes, you can restore normal system performance.

This is one of the most common responsibilities of Linux administrators.

---

# 🎯 Summary

Linux provides powerful tools for monitoring and managing processes.

Common commands:

```bash
ps

ps -e

ps aux

ps aux | grep nginx

top

htop

kill PID

kill -9 PID

pkill process_name
```

Important concepts:

```text
PID        Process ID

ps         View running processes

top        Real-time system monitor

htop       Interactive process monitor

kill       Stop a process

pkill      Stop processes by name
```

Understanding process management allows you to monitor system health, identify resource-intensive applications, troubleshoot performance issues, and safely manage running programs on Linux systems.
