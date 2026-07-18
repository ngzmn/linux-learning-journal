# Day 051 - Secure Remote Access with SSH

## 🧠 Introduction

SSH (Secure Shell) is the standard protocol for securely accessing remote Linux machines.

Before SSH, administrators commonly used Telnet, which transmitted usernames and passwords in plain text. SSH solved this problem by encrypting all communication between the client and the server.

Today, SSH is used for:

- Remote server administration
- Secure file transfers
- Git operations (GitHub, GitLab)
- Remote command execution
- Tunneling and port forwarding

Learning SSH is one of the most important Linux skills.

---

# Basic SSH Connection

General syntax:

```bash
ssh username@hostname
```

Example:

```bash
ssh john@192.168.1.100
```

Or using a domain name:

```bash
ssh ubuntu@example.com
```

If successful, you will be prompted for the user's password (unless key authentication is configured).

---

# Connecting to a Custom Port

By default, SSH listens on port **22**.

If the server uses another port:

```bash
ssh -p 2222 john@192.168.1.100
```

Option:

```text
-p = Port
```

---

# Running a Remote Command

SSH can execute a command without opening an interactive shell.

Example:

```bash
ssh john@server "uptime"
```

Another example:

```bash
ssh john@server "df -h"
```

This is commonly used in automation scripts.

---

# Generating SSH Keys

Password authentication works, but SSH keys are more secure.

Generate a key pair:

```bash
ssh-keygen
```

Typical output:

```text
~/.ssh/id_rsa

~/.ssh/id_rsa.pub
```

Or on newer systems:

```text
~/.ssh/id_ed25519

~/.ssh/id_ed25519.pub
```

Files:

```text
Private Key → Keep secret

Public Key → Share with servers
```

---

# Copying Your Public Key

Install your public key on a remote server:

```bash
ssh-copy-id john@192.168.1.100
```

Afterward, you can usually log in without entering a password.

---

# SSH Configuration File

Instead of typing long commands every time, create:

```text
~/.ssh/config
```

Example:

```text
Host myserver
    HostName 192.168.1.100
    User john
    Port 2222
```

Now connect using:

```bash
ssh myserver
```

This saves time when managing multiple servers.

---

# Useful SSH Options

Verbose output:

```bash
ssh -v john@server
```

Very verbose:

```bash
ssh -vvv john@server
```

These options help troubleshoot connection problems.

---

# Checking the Server Fingerprint

The first time you connect, SSH displays a fingerprint:

```text
The authenticity of host ...

Are you sure you want to continue connecting?
```

Type:

```text
yes
```

The fingerprint is stored in:

```text
~/.ssh/known_hosts
```

Future connections verify that the server's identity has not changed.

---

# Real-World Examples

Connect to a remote server:

```bash
ssh ubuntu@192.168.1.20
```

Run a remote command:

```bash
ssh ubuntu@server "systemctl status nginx"
```

Generate SSH keys:

```bash
ssh-keygen
```

Copy your public key:

```bash
ssh-copy-id ubuntu@server
```

Use a custom port:

```bash
ssh -p 2222 ubuntu@server
```

Use an SSH configuration:

```bash
ssh myserver
```

These are among the most common SSH tasks.

---

# Common Mistakes

### Protecting the Private Key

Never share:

```text
id_rsa

id_ed25519
```

Only the public key should be copied to servers.

---

### Wrong File Permissions

SSH requires secure permissions.

Correct:

```bash
chmod 700 ~/.ssh

chmod 600 ~/.ssh/id_ed25519
```

Incorrect permissions may cause SSH to reject the key.

---

### Forgetting the Username

Incorrect:

```bash
ssh server.com
```

Correct:

```bash
ssh username@server.com
```

Unless your local username matches the remote one.

---

# Why SSH Matters

Imagine you manage ten Linux servers in different data centers.

Instead of sitting in front of each machine, you simply run:

```bash
ssh admin@server01
```

Within seconds, you have a secure terminal session.

You can update software, restart services, inspect logs, and troubleshoot problems from anywhere.

SSH has become the standard method for remote Linux administration.

---

# 🎯 Summary

SSH provides secure remote access to Linux systems.

Common commands:

```bash
ssh user@server

ssh -p 2222 user@server

ssh user@server "uptime"

ssh-keygen

ssh-copy-id user@server

ssh -v user@server
```

Important files:

```text
~/.ssh/id_ed25519

~/.ssh/id_ed25519.pub

~/.ssh/config

~/.ssh/known_hosts
```

Key concepts:

```text
SSH encrypts remote communication.

SSH keys are more secure than passwords.

The private key must remain secret.

The public key is installed on remote servers.

The SSH config file simplifies connections.
```

Mastering SSH is essential for secure remote administration, automation, software deployment, and everyday Linux server management.
