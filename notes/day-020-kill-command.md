# Day 020 - Terminating Processes with kill

## 🧠 Introduction

Sometimes a program becomes unresponsive, consumes too many resources, or needs to be stopped manually.

Linux provides the `kill` command to send signals to running processes.

Despite its name, `kill` does not always terminate a process. It can send different types of signals that tell a process what action to take.

Understanding `kill` is an essential skill for system administrators, developers, and DevOps engineers.

---

## Finding a Process

Before using `kill`, you need the Process ID (PID).

Example:

```bash
ps aux | grep firefox
```

Output:

```text
john      5231  5.3  3.2 firefox
```

The PID is:

```text
5231
```

---

## Basic Usage

Terminate a process:

```bash
kill 5231
```

This sends the default signal:

```text
SIGTERM (15)
```

The process receives a request to shut down gracefully.

---

## Understanding Signals

A signal is a message sent to a process.

Common signals:

```text
SIGTERM = 15
SIGKILL = 9
SIGSTOP = 19
SIGCONT = 18
```

Each signal has a different purpose.

---

## Graceful Termination

Example:

```bash
kill 5231
```

Equivalent to:

```bash
kill -15 5231
```

The application has a chance to:

- Save data
- Close files
- Shut down cleanly

This is the preferred method.

---

## Force Killing a Process

Sometimes a process ignores SIGTERM.

Force termination:

```bash
kill -9 5231
```

This sends:

```text
SIGKILL
```

The kernel immediately stops the process.

The application cannot save its work before exiting.

---

## Stopping a Process Temporarily

Pause a process:

```bash
kill -19 5231
```

Signal:

```text
SIGSTOP
```

The process remains in memory but stops running.

---

## Continuing a Stopped Process

Resume execution:

```bash
kill -18 5231
```

Signal:

```text
SIGCONT
```

The process continues from where it stopped.

---

## Using killall

Instead of a PID, you can target a process by name.

Example:

```bash
killall firefox
```

All Firefox processes will receive a termination signal.

---

## Real-World Examples

Stop a Python script:

```bash
ps aux | grep python
kill PID
```

Restart a stuck application:

```bash
kill -9 PID
```

Terminate all instances of a program:

```bash
killall node
```

These are common troubleshooting tasks on Linux servers.

---

## Checking if the Process Ended

Before:

```bash
ps aux | grep firefox
```

After using kill:

```bash
ps aux | grep firefox
```

If the process no longer appears, it has been terminated successfully.

---

## Common Mistakes

### Using SIGKILL Too Quickly

Many beginners immediately use:

```bash
kill -9 PID
```

Instead, try:

```bash
kill PID
```

first.

Graceful shutdown is safer.

---

### Killing the Wrong Process

Always verify the PID before running:

```bash
kill PID
```

Mistakes can stop important services.

---

### Confusing Process Names and PIDs

Incorrect:

```bash
kill firefox
```

Correct:

```bash
kill PID
```

or

```bash
killall firefox
```

---

## Relationship Between ps, top, and kill

A common workflow:

Find process:

```bash
ps aux
```

Monitor process:

```bash
top
```

Terminate process:

```bash
kill PID
```

These three commands are frequently used together.

---

## 🎯 Summary

The `kill` command sends signals to processes.

Common examples:

```bash
kill PID
kill -15 PID
kill -9 PID
kill -19 PID
kill -18 PID
killall firefox
```

Important signals:

```text
15 = SIGTERM
9  = SIGKILL
19 = SIGSTOP
18 = SIGCONT
```

Learning `kill` is a fundamental Linux skill because every administrator eventually encounters processes that must be managed manually.
