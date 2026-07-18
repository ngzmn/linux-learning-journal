# Day 050 - Networking Basics with `ping`, `ip`, and `ss`

## 🧠 Introduction

Networking is one of the most important topics in Linux.

Whether you are managing a server, troubleshooting internet connectivity, or deploying applications, you will constantly use networking tools.

Three of the most useful commands are:

- `ping`
- `ip`
- `ss`

These commands allow you to:

- Verify network connectivity
- View IP addresses
- Inspect network interfaces
- Display routing information
- Monitor open ports
- Diagnose network problems

These tools are used daily by Linux administrators and DevOps engineers.

---

# The `ping` Command

`ping` checks whether another host is reachable over the network.

Basic syntax:

```bash
ping google.com
```

Example output:

```text
64 bytes from 142.250.190.14:
icmp_seq=1 ttl=117 time=18.2 ms
```

Important values:

```text
icmp_seq   Packet number

ttl        Time To Live

time       Response time
```

Press:

```text
Ctrl + C
```

to stop the command.

---

# Sending a Specific Number of Packets

Instead of running forever:

```bash
ping -c 4 google.com
```

Option:

```text
-c = Count
```

Only four packets are sent.

---

# Understanding Ping Results

Successful response:

```text
64 bytes from...
```

No response:

```text
Request timeout
```

Unknown host:

```text
Temporary failure in name resolution
```

These messages help identify different network problems.

---

# The `ip` Command

The `ip` command replaces several older networking utilities such as:

- ifconfig
- route
- arp

It is the standard networking tool on modern Linux systems.

---

# Display IP Addresses

Show all network interfaces:

```bash
ip addr
```

Short version:

```bash
ip a
```

Example output:

```text
2: eth0

inet 192.168.1.25/24
```

Here:

```text
eth0 → Interface name

192.168.1.25 → IP address
```

---

# Show Network Interfaces

Display interface status:

```bash
ip link
```

Output:

```text
lo

eth0

wlan0
```

States include:

```text
UP

DOWN
```

---

# Display Routing Table

View routes:

```bash
ip route
```

Example:

```text
default via 192.168.1.1 dev eth0
```

This shows the default gateway.

Short version:

```bash
ip r
```

---

# Enable or Disable an Interface

Disable:

```bash
sudo ip link set eth0 down
```

Enable:

```bash
sudo ip link set eth0 up
```

These commands are useful when troubleshooting network interfaces.

---

# The `ss` Command

`ss` stands for **Socket Statistics**.

It displays active network connections and listening ports.

It replaces the older `netstat` command.

---

# Show All Connections

```bash
ss
```

This displays active sockets.

---

# Listening Ports

Display listening services:

```bash
ss -l
```

Show TCP ports:

```bash
ss -lt
```

Show UDP ports:

```bash
ss -lu
```

---

# Display Process Information

Show which process owns each connection:

```bash
sudo ss -tulpn
```

Options:

```text
-t = TCP

-u = UDP

-l = Listening

-p = Process

-n = Numeric output
```

Example:

```text
LISTEN

0.0.0.0:22

users:(("sshd"))
```

This means the SSH server is listening on port 22.

---

# Real-World Examples

Test internet connectivity:

```bash
ping -c 4 google.com
```

View your IP address:

```bash
ip a
```

View the routing table:

```bash
ip r
```

Display listening ports:

```bash
ss -lt
```

See which applications are using ports:

```bash
sudo ss -tulpn
```

These are among the first commands Linux administrators use when diagnosing network issues.

---

# Common Mistakes

### Assuming Ping Always Works

Some servers block ICMP packets.

Even if:

```bash
ping server.com
```

fails, services like SSH or HTTP may still be available.

---

### Confusing Private and Public IP Addresses

Private addresses include:

```text
192.168.x.x

10.x.x.x

172.16.x.x - 172.31.x.x
```

Public IP addresses are reachable from the Internet.

---

### Forgetting Root Privileges

Some `ss` options require elevated permissions.

Instead of:

```bash
ss -tulpn
```

use:

```bash
sudo ss -tulpn
```

to view process names.

---

# Why These Commands Matter

Imagine users report that your website is unavailable.

A common troubleshooting sequence is:

Check internet connectivity:

```bash
ping 8.8.8.8
```

Verify your IP address:

```bash
ip a
```

Check the routing table:

```bash
ip r
```

Confirm the web server is listening:

```bash
sudo ss -tulpn
```

Within minutes, you can identify whether the issue is network connectivity, routing, or an application that is not listening on the expected port.

---

# 🎯 Summary

The `ping`, `ip`, and `ss` commands are fundamental networking tools.

Common commands:

```bash
ping google.com

ping -c 4 google.com

ip a

ip link

ip r

sudo ip link set eth0 down

sudo ip link set eth0 up

ss -lt

ss -lu

sudo ss -tulpn
```

Important concepts:

```text
ping      Test network connectivity

ip a      Show IP addresses

ip link   Show network interfaces

ip r      Display routing table

ss        Display socket statistics

ss -lt    Show listening TCP ports

ss -tulpn Show listening ports with process names
```

Mastering these commands provides the foundation for Linux networking, allowing you to troubleshoot connectivity issues, inspect interfaces, monitor network services, and diagnose server problems efficiently.
