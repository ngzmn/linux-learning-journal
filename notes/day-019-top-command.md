# Day 019 - Monitoring Processes with top

## 🧠 Introduction

The `top` command is one of the most important Linux monitoring tools.

Unlike `ps`, which shows a snapshot of running processes, `top` provides a live and continuously updating view of system activity.

System administrators use `top` to monitor:

- CPU usage
- Memory usage
- Running processes
- System load
- Resource consumption

It is often the first command used when a Linux server feels slow.

---

## Starting top

Run:

```bash
top
```

The screen updates automatically every few seconds.

Example:

```text
top - 14:35:21 up 2 days,  4:15,  1 user
Tasks: 183 total
%Cpu(s): 12.5 us, 2.3 sy
MiB Mem : 7850 total
```

---

## Understanding the Header

The top section contains system-wide information.

Example:

```text
top - 14:35:21
```

Current system time.

---

```text
up 2 days, 4:15
```

System uptime.

---

```text
1 user
```

Number of logged-in users.

---

```text
load average: 0.20, 0.15, 0.10
```

System load during:

- Last 1 minute
- Last 5 minutes
- Last 15 minutes

Lower values generally indicate a less busy system.

---

## CPU Information

Example:

```text
%Cpu(s): 12.5 us, 2.3 sy, 85.2 id
```

Important values:

```text
us = User processes
sy = System processes
id = Idle CPU
```

High CPU usage may indicate heavy workloads.

---

## Memory Information

Example:

```text
MiB Mem : 7850 total, 2300 free, 4100 used
```

This shows:

- Total RAM
- Available RAM
- Used RAM

Monitoring memory is critical on servers and development machines.

---

## Process List

The lower section displays running processes.

Example:

```text
PID USER  %CPU %MEM COMMAND
4120 john  8.5  2.1 python
1200 root  1.0  0.5 nginx
```

Important columns:

```text
PID     Process ID
USER    Process owner
%CPU    CPU usage
%MEM    Memory usage
COMMAND Process name
```

---

## Sorting Processes

While inside top:

```text
P
```

Sort by CPU usage.

---

```text
M
```

Sort by memory usage.

These shortcuts help identify resource-hungry processes quickly.

---

## Finding Problematic Processes

Suppose the system is slow.

Run:

```bash
top
```

Look for:

```text
High %CPU
```

or

```text
High %MEM
```

Processes at the top of the list are often the cause.

---

## Exiting top

To quit:

```text
q
```

This immediately returns you to the terminal.

---

## Real-World Examples

Monitor a Python application:

```bash
top
```

and look for:

```text
python
```

Monitor a web server:

```text
nginx
```

Monitor Docker services:

```text
docker
```

These are common troubleshooting tasks.

---

## top vs ps

### ps

```bash
ps aux
```

Shows a snapshot.

---

### top

```bash
top
```

Shows live updates.

# Day 019 - Monitoring Processes with top

## 🧠 Introduction

The `top` command is one of the most important Linux monitoring tools.

Unlike `ps`, which shows a snapshot of running processes, `top` provides a live and continuously updating view of system activity.

System administrators use `top` to monitor:

- CPU usage
- Memory usage
- Running processes
- System load
- Resource consumption

It is often the first command used when a Linux server feels slow.

---

## Starting top

Run:

```bash
top
```

The screen updates automatically every few seconds.

Example:

```text
top - 14:35:21 up 2 days,  4:15,  1 user
Tasks: 183 total
%Cpu(s): 12.5 us, 2.3 sy
MiB Mem : 7850 total
```

---

## Understanding the Header

The top section contains system-wide information.

Example:

```text
top - 14:35:21
```

Current system time.

---

```text
up 2 days, 4:15
```

System uptime.

---

```text
1 user
```

Number of logged-in users.

---

```text
load average: 0.20, 0.15, 0.10
```

System load during:

- Last 1 minute
- Last 5 minutes
- Last 15 minutes

Lower values generally indicate a less busy system.

---

## CPU Information

Example:

```text
%Cpu(s): 12.5 us, 2.3 sy, 85.2 id
```

Important values:

```text
us = User processes
sy = System processes
id = Idle CPU
```

High CPU usage may indicate heavy workloads.

---

## Memory Information

Example:

```text
MiB Mem : 7850 total, 2300 free, 4100 used
```

This shows:

- Total RAM
- Available RAM
- Used RAM

Monitoring memory is critical on servers and development machines.

---

## Process List

The lower section displays running processes.

Example:

```text
PID USER  %CPU %MEM COMMAND
4120 john  8.5  2.1 python
1200 root  1.0  0.5 nginx
```

Important columns:

```text
PID     Process ID
USER    Process owner
%CPU    CPU usage
%MEM    Memory usage
COMMAND Process name
```

---

## Sorting Processes

While inside top:

```text
P
```

Sort by CPU usage.

---

```text
M
```

Sort by memory usage.

These shortcuts help identify resource-hungry processes quickly.

---

## Finding Problematic Processes

Suppose the system is slow.

Run:

```bash
top
```

Look for:

```text
High %CPU
```

or

```text
High %MEM
```

Processes at the top of the list are often the cause.

---

## Exiting top

To quit:

```text
q
```

This immediately returns you to the terminal.

---

## Real-World Examples

Monitor a Python application:

```bash
top
```

and look for:

```text
python
```

Monitor a web server:

```text
nginx
```

Monitor Docker services:

```text
docker
```

These are common troubleshooting tasks.

---

## top vs ps

### ps

```bash
ps aux
```

Shows a snapshot.

---

### top

```bash
top
```

Shows live updates.

Think of `ps` as a photograph and `top` as a live video feed.

---

## Common Mistakes

### Forgetting to Quit

Many beginners think the terminal is frozen.

Simply press:

```text
q
```

---

### Misreading Load Average

A high load average does not always mean high CPU usage.

It represents the number of processes waiting for CPU or resources.

Always check CPU and memory usage together.

---

## 🎯 Summary

The `top` command provides real-time monitoring of Linux systems.

Common usage:

```bash
top
```

Useful shortcuts:

```text
P → Sort by CPU
M → Sort by Memory
q → Quit
```

Important metrics:

```text
CPU Usage
Memory Usage
Load Average
Running Processes
```

Learning `top` is essential because it is one of the most frequently used tools for diagnosing performance problems on Linux servers.
