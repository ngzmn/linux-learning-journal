# Day 028 - Monitoring Memory Usage with free

## 🧠 Introduction

Memory management is a critical part of Linux system administration.

When applications run, they consume:

- RAM
- Cache
- Buffers
- Swap space

If memory resources are exhausted, the system may become slow or unstable.

Linux provides the `free` command to quickly inspect memory usage.

It helps answer questions such as:

- How much RAM is installed?
- How much memory is available?
- Is swap being used?
- Is the system under memory pressure?

---

## Basic Usage

Run:

```bash
free
```

Example output:

```text
              total        used        free
Mem:        8175620     3421840     1283400
Swap:       2097148           0     2097148
```

This provides a quick overview of RAM and swap usage.

---

## Human-Readable Output

The most common form is:

```bash
free -h
```

Example:

```text
              total   used   free  shared  buff/cache  available
Mem:           7.8G   3.2G   1.2G    250M       3.4G       4.0G
Swap:          2.0G     0B   2.0G
```

Option:

```text
-h = human-readable
```

This displays values in:

- MB
- GB
- TB

instead of raw bytes.

---

## Understanding the Columns

### total

The total amount of installed memory.

Example:

```text
7.8G
```

---

### used

Memory currently in use.

Example:

```text
3.2G
```

---

### free

Unused memory.

Example:

```text
1.2G
```

---

### available

Memory that can be allocated to applications without swapping.

Example:

```text
4.0G
```

Modern Linux administrators focus on:

```text
available
```

rather than simply:

```text
free
```

---

## Understanding Buffers and Cache

Linux aggressively uses memory for caching.

Example:

```text
buff/cache = 3.4G
```

This memory is not permanently occupied.

It can be reclaimed automatically when applications need more RAM.

This behavior improves system performance.

---

## Understanding Swap Space

Swap is disk storage used as extra memory.

Example:

```text
Swap: 2.0G
```

If RAM becomes full, Linux may move inactive data into swap.

Advantages:

- Prevents crashes
- Supports memory overcommitment

Disadvantages:

- Much slower than RAM

---

## Monitoring Memory Continuously

Update every two seconds:

```bash
watch -n 2 free -h
```

Options:

```text
watch = repeat commands
-n 2  = every two seconds
```

This is useful during:

- Software installations
- Database operations
- Performance testing

---

## Real-World Examples

Check total RAM:

```bash
free -h
```

Verify swap usage:

```bash
free -h
```

Monitor memory during a compilation:

```bash
watch -n 2 free -h
```

Check memory on a cloud server:

```bash
free -g
```

These tasks are common in production environments.

---

## free vs top

### free

Example:

```bash
free -h
```

Shows:

```text
Overall memory statistics
```

Fast and lightweight.

---

### top

Example:

```bash
top
```

Shows:

```text
Per-process memory consumption
```

Useful for identifying problematic applications.

The two tools complement each other.

---

## Common Mistakes

### Thinking Cached Memory Is Wasted

Many beginners see:

```text
free = 1G
cache = 3G
```

and assume memory is exhausted.

In reality:

```text
cache memory is reusable
```

Linux automatically releases it when needed.

---

### Ignoring the Available Column

The most important metric is:

```text
available
```

It represents the memory applications can actually use.

---

### Excessive Swap Usage

If:

```text
Swap used = 100%
```

the system may experience significant slowdowns.

Possible solutions:

- Add more RAM
- Optimize applications
- Reduce workload

---

## Why Memory Monitoring Matters

Imagine a server becomes extremely slow.

First step:

```bash
free -h
```

Output:

```text
RAM: 99% used
Swap: 100% used
```

The problem becomes immediately obvious.

Memory analysis is one of the first troubleshooting steps in Linux administration.

---

## 🎯 Summary

The `free` command displays memory and swap usage.

Common examples:

```bash
free
free -h
free -g
watch -n 2 free -h
```

Important concepts:

```text
RAM       = Physical memory
Swap      = Disk-based memory extension
Cache     = Performance optimization
Available = Usable memory for applications
```

Understanding memory usage is essential because every Linux server, desktop, container, and virtual machine depends on healthy RAM management.
