# Day 029 - Monitoring System Performance with vmstat

## 🧠 Introduction

Linux systems constantly manage multiple resources:

- CPU
- Memory
- Processes
- Disk I/O
- Swap space

The `vmstat` command provides a compact overview of all these metrics in a single place.

Its name means:

```text
Virtual Memory Statistics
```

Despite its name, `vmstat` reports much more than memory information.

System administrators use it to diagnose:

- High CPU usage
- Memory bottlenecks
- Disk performance issues
- Excessive swapping
- System overloads

It is one of the most valuable troubleshooting tools in Linux.

---

## Basic Usage

Run:

```bash
vmstat
```

Example output:

```text
procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
 r  b swpd free buff cache si so bi bo in cs us sy id wa st
 1  0    0 850000 24000 560000 0 0 10 12 120 250 5 2 92 1 0
```

The first line shows averages since system startup.

---

## Continuous Monitoring

Update every two seconds:

```bash
vmstat 2
```

This prints a new line every two seconds.

Example:

```text
vmstat 2
```

For five updates only:

```bash
vmstat 2 5
```

Meaning:

```text
Every 2 seconds
For 5 reports
```

---

## Understanding Process Statistics

Columns:

```text
r = Running processes
b = Blocked processes
```

Example:

```text
r = 4
```

means four processes are waiting for CPU time.

Large values may indicate CPU pressure.

---

## Understanding Memory Statistics

Columns:

```text
swpd = Swap memory used
free = Free RAM
buff = Buffers
cache = Filesystem cache
```

Example:

```text
swpd = 0
```

means swap is not being used.

Generally, lower swap usage is better.

---

## Understanding Swap Activity

Columns:

```text
si = Swap in
so = Swap out
```

Example:

```text
si = 0
so = 0
```

This indicates healthy memory usage.

If these numbers increase continuously, the system may require additional RAM.

---

## Understanding Disk I/O

Columns:

```text
bi = Blocks received from disk
bo = Blocks written to disk
```

Example:

```text
bi = 150
bo = 300
```

High values may indicate:

- Database activity
- Large file transfers
- Backup operations

Disk bottlenecks often appear here.

---

## Understanding CPU Statistics

Important columns:

```text
us = User CPU time
sy = System CPU time
id = Idle CPU
wa = Waiting for I/O
st = Stolen CPU time
```

Example:

```text
us = 20
sy = 5
id = 70
wa = 5
```

Interpretation:

- CPU is mostly idle
- Some time is spent waiting for disk operations

---

## The Meaning of wa (I/O Wait)

Example:

```text
wa = 35
```

This means:

```text
35% of CPU time is waiting for disk operations
```

High I/O wait may indicate:

- Slow disks
- Heavy database workloads
- Storage bottlenecks

This is a common production issue.

---

## Understanding st (Steal Time)

Example:

```text
st = 15
```

This metric appears mainly in virtual machines.

It means:

```text
The hypervisor is taking CPU time away from your VM.
```

High values suggest overloaded cloud infrastructure.

---

## Real-World Examples

Monitor system activity:

```bash
vmstat 2
```

Take five measurements:

```bash
vmstat 1 5
```

Check swap activity:

```bash
vmstat | grep -v si
```

Analyze disk performance:

```bash
vmstat 3
```

These workflows are common in server administration.

---

## vmstat vs free

### free

```bash
free -h
```

Shows:

```text
Memory only
```

---

### vmstat

```bash
vmstat
```

Shows:

```text
Memory
CPU
Processes
Disk I/O
Swap activity
```

`vmstat` provides a broader system overview.

---

## vmstat vs top

### top

```bash
top
```

Best for:

```text
Per-process analysis
```

---

### vmstat

```bash
vmstat
```

Best for:

```text
System-wide statistics
```

Many administrators use both tools together.

---

## Common Mistakes

### Ignoring the First Line

The first report shows averages since boot.

The second line and beyond show current activity.

Always pay attention to later outputs.

---

### Misinterpreting Free Memory

Low free memory is not always bad.

Linux intentionally uses RAM for caching.

Check:

```text
swap activity
```

before concluding there is a problem.

---

### Ignoring I/O Wait

High:

```text
wa
```

can make a system feel slow even when CPU usage appears low.

Storage performance matters.

---

## Why vmstat Matters

Imagine a production server becomes sluggish.

Questions:

```text
Is the CPU overloaded?
Is memory exhausted?
Is swap active?
Are disks too slow?
```

Running:

```bash
vmstat 2
```

provides answers within seconds.

It is one of the fastest diagnostic tools available on Linux systems.

---

## 🎯 Summary

The `vmstat` command displays system-wide performance metrics.

Common examples:

```bash
vmstat
vmstat 2
vmstat 1 5
```

Important columns:

```text
r   Running processes
swpd Swap usage
si   Swap in
so   Swap out
bi   Disk reads
bo   Disk writes
us   User CPU time
sy   System CPU time
id   Idle CPU time
wa   I/O wait
st   Steal time
```

Understanding `vmstat` is essential because effective Linux troubleshooting depends on observing CPU, memory, disk, and process behavior together rather than in isolation.
