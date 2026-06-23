# Day 021 - Network Connections with netstat and ss

## 🧠 Introduction

Linux systems constantly communicate over networks.

Web servers, databases, SSH sessions, and applications all use network connections.

To troubleshoot networking issues, administrators need tools to answer questions such as:

- Which ports are open?
- Which services are listening?
- Which remote hosts are connected?
- Which process owns a network connection?

Two common tools are:

```bash
netstat
```

and

```bash
ss
```

Today, `ss` is generally preferred because it is faster and more modern.

---

## What is a Port?

A port is a communication endpoint used by applications.

Examples:

```text
22   SSH
80   HTTP
443  HTTPS
3306 MySQL
```

A service listens on a port and waits for incoming connections.

---

## Viewing Listening Ports with ss

Show listening TCP and UDP ports:

```bash
ss -tuln
```

Options:

```text
-t = TCP
-u = UDP
-l = Listening
-n = Numeric output
```

Example output:

```text
Netid State  Local Address:Port
tcp   LISTEN 0.0.0.0:22
tcp   LISTEN 0.0.0.0:80
```

This shows that SSH and a web server are accepting connections.

---

## Display Process Information

Show which process owns each port:

```bash
sudo ss -tulpn
```

Example:

```text
tcp LISTEN 0.0.0.0:22 users:(("sshd",pid=834))
```

This tells us:

```text
Process: sshd
PID: 834
Port: 22
```

Very useful when troubleshooting.

---

## Viewing Established Connections

Show active connections:

```bash
ss -ta
```

Example:

```text
ESTAB 192.168.1.10:22 192.168.1.50:52341
```

Meaning:

A remote device is connected via SSH.

---

## Filtering Results

Find SSH connections:

```bash
ss -tulpn | grep 22
```

Find web server ports:

```bash
ss -tulpn | grep 80
```

Find HTTPS:

```bash
ss -tulpn | grep 443
```

Combining `ss` with `grep` is very common.

---

## Using netstat

Older Linux systems may use:

```bash
netstat -tulpn
```

Output is similar:

```text
Proto Local Address State PID/Program name
tcp   0.0.0.0:22    LISTEN 834/sshd
```

Many administrators still know and use this command.

---

## Comparing ss and netstat

### ss

```bash
ss -tulpn
```

Advantages:

- Faster
- Modern
- Included in most Linux distributions

---

### netstat

```bash
netstat -tulpn
```

Advantages:

- Familiar to older administrators
- Found on legacy systems

For modern Linux environments, `ss` is usually recommended.

---

## Real-World Examples

Check whether SSH is running:

```bash
ss -tulpn | grep 22
```

Verify a website is listening:

```bash
ss -tulpn | grep 80
```

Check HTTPS:

```bash
ss -tulpn | grep 443
```

Find which process is using a specific port:

```bash
sudo ss -tulpn
```

These tasks are performed daily by server administrators.

---

## Common Mistakes

### Forgetting sudo

Without sudo:

```bash
ss -tulpn
```

some process information may be hidden.

Use:

```bash
sudo ss -tulpn
```

for complete results.

---

### Confusing LISTEN and ESTAB

```text
LISTEN
```

means a service is waiting for connections.

```text
ESTAB
```

means a connection is currently active.

These states have different meanings.

---

## Why This Matters

Imagine a website is not working.

Questions to ask:

```text
Is the web server running?
Is port 80 open?
Is port 443 listening?
```

The `ss` command helps answer these questions quickly.

---

## 🎯 Summary

The `ss` and `netstat` commands are used to inspect network connections and listening ports.

Common examples:

```bash
ss -tuln
ss -tulpn
ss -ta
netstat -tulpn
ss -tulpn | grep 22
```

Important concepts:

```text
LISTEN = Waiting for connections
ESTAB  = Active connection
Port   = Network communication endpoint
```

Learning `ss` is essential because network troubleshooting is a core Linux administration skill.
