# Day 054 - Managing Services with `systemctl`

## 🧠 Introduction

Modern Linux distributions use **systemd** as their initialization and service management system.

When Linux boots, **systemd** starts the operating system and launches background services (also called daemons).

Examples of services include:

- SSH Server
- Nginx
- Apache
- Docker
- MySQL
- Cron

The primary command used to manage these services is:

```text
systemctl
```

Learning `systemctl` is essential for Linux administration because nearly every server relies on it.

---

# What is a Service?

A service is a program that runs in the background without user interaction.

Examples:

```text
sshd

nginx

docker

mysql

cron
```

Services usually start automatically when the system boots.

---

# Check Service Status

View the current status of a service:

```bash
systemctl status ssh
```

Example output:

```text
● ssh.service - OpenBSD Secure Shell server

Loaded: loaded

Active: active (running)
```

Important fields:

```text
Loaded

Active

Main PID
```

These indicate whether the service is installed and currently running.

---

# Start a Service

Start a stopped service:

```bash
sudo systemctl start nginx
```

The service begins running immediately.

---

# Stop a Service

Stop a running service:

```bash
sudo systemctl stop nginx
```

The service is terminated but can be started again later.

---

# Restart a Service

Restart a service after changing its configuration:

```bash
sudo systemctl restart nginx
```

This is commonly used after editing configuration files.

---

# Reload a Service

Some services can reload their configuration without restarting.

Example:

```bash
sudo systemctl reload nginx
```

Reloading is often preferred because it avoids interrupting active connections.

---

# Enable a Service

Enable automatic startup at boot:

```bash
sudo systemctl enable nginx
```

The service will start automatically every time the system boots.

---

# Disable a Service

Prevent automatic startup:

```bash
sudo systemctl disable nginx
```

The service can still be started manually.

---

# Check Whether a Service Is Enabled

Display boot status:

```bash
systemctl is-enabled nginx
```

Possible output:

```text
enabled
```

or

```text
disabled
```

---

# List Running Services

Display active services:

```bash
systemctl list-units --type=service
```

Show all services:

```bash
systemctl list-unit-files --type=service
```

These commands are useful when exploring a system.

---

# View Boot Logs

Display system logs:

```bash
journalctl
```

Show logs for a specific service:

```bash
journalctl -u nginx
```

Display the latest logs:

```bash
journalctl -u nginx -n 20
```

Follow logs in real time:

```bash
journalctl -u nginx -f
```

`journalctl` is the standard logging tool for systems using `systemd`.

---

# Check System Boot Time

Display startup information:

```bash
systemd-analyze
```

Example:

```text
Startup finished in 4.5s
```

This helps diagnose slow boot times.

---

# Real-World Examples

Check if SSH is running:

```bash
systemctl status ssh
```

Restart the web server:

```bash
sudo systemctl restart nginx
```

Enable Docker at boot:

```bash
sudo systemctl enable docker
```

Stop Apache:

```bash
sudo systemctl stop apache2
```

View Docker logs:

```bash
journalctl -u docker
```

These commands are used daily by Linux administrators.

---

# Common Mistakes

### Forgetting `sudo`

Commands like:

```bash
systemctl restart nginx
```

may fail with a permission error.

Use:

```bash
sudo systemctl restart nginx
```

---

### Restarting Instead of Reloading

If supported, prefer:

```bash
systemctl reload nginx
```

instead of:

```bash
systemctl restart nginx
```

Reloading applies configuration changes without interrupting running connections.

---

### Confusing "Running" and "Enabled"

A service can be:

```text
Running but not enabled
```

or:

```text
Enabled but currently stopped
```

Remember:

```text
start    → Start now

enable   → Start automatically at boot
```

---

# Why `systemctl` Matters

Imagine you update the configuration of a web server.

After saving the changes, you run:

```bash
sudo systemctl restart nginx
```

If users report problems, you immediately check:

```bash
systemctl status nginx
```

and inspect the logs:

```bash
journalctl -u nginx
```

Within minutes, you can identify whether the service failed to start, has a configuration error, or is running normally.

Managing services with `systemctl` is a core responsibility of Linux system administrators.

---

# 🎯 Summary

The `systemctl` command manages services on modern Linux systems.

Common commands:

```bash
systemctl status ssh

sudo systemctl start nginx

sudo systemctl stop nginx

sudo systemctl restart nginx

sudo systemctl reload nginx

sudo systemctl enable nginx

sudo systemctl disable nginx

systemctl is-enabled nginx

systemctl list-units --type=service

journalctl -u nginx

systemd-analyze
```

Important concepts:

```text
start       Start a service

stop        Stop a service

restart     Restart a service

reload      Reload configuration

enable      Start automatically at boot

disable     Disable automatic startup

status      Display service status

journalctl  View system logs
```

Mastering `systemctl` allows you to manage Linux services, troubleshoot failures, analyze logs, and control system behavior efficiently on modern Linux distributions.
