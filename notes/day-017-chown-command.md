# Day 017 - Understanding Ownership with chown

## 🧠 Introduction

In Linux, every file and directory has:

- An Owner (User)
- A Group

These ownership settings determine who can access and modify files.

The `chown` command stands for:

```text
change owner
```

It is used to change the owner and group of files and directories.

This command is especially important on servers, shared systems, and web hosting environments.

---

## Viewing Ownership

Use:

```bash
ls -l
```

Example:

```text
-rw-r--r-- 1 john developers 1250 Jun 19 notes.txt
```

Breakdown:

```text
Owner: john
Group: developers
```

The owner is the user who owns the file.

The group determines which users receive group permissions.

---

## Changing the Owner

Syntax:

```bash
sudo chown user file
```

Example:

```bash
sudo chown alice notes.txt
```

After running the command:

```text
Owner: alice
```

The file now belongs to Alice.

---

## Changing Owner and Group

Syntax:

```bash
sudo chown user:group file
```

Example:

```bash
sudo chown alice:developers notes.txt
```

Result:

```text
Owner: alice
Group: developers
```

Both values are updated.

---

## Changing Only the Group

You can modify only the group:

```bash
sudo chown :developers notes.txt
```

The owner remains unchanged.

---

## Recursive Ownership Changes

Suppose you have:

```text
project/
├── app.py
├── config.ini
└── docs/
```

Change ownership for everything:

```bash
sudo chown -R alice:developers project
```

The `-R` option means:

```text
Recursive
```

All files and subdirectories inherit the new ownership.

---

## Real-World Example

A web server may use:

```text
www-data
```

as its user.

To allow the web server to manage files:

```bash
sudo chown -R www-data:www-data website/
```

This is extremely common when deploying websites.

---

## Ownership vs Permissions

Ownership and permissions work together.

Example:

```text
-rw-r--r--
```

The owner can modify the file.

If ownership changes:

```bash
sudo chown alice file.txt
```

Alice becomes the user who can modify the file.

The permission structure stays the same, but it now applies to a different owner.

---

## Common Mistakes

### Forgetting sudo

This often fails:

```bash
chown alice file.txt
```

Error:

```text
Operation not permitted
```

Solution:

```bash
sudo chown alice file.txt
```

---

### Forgetting -R

Changing a project directory:

```bash
sudo chown alice project
```

Only changes the top directory.

To affect everything inside:

```bash
sudo chown -R alice project
```

---

## Checking Results

Verify ownership:

```bash
ls -l
```

Example output:

```text
-rw-r--r-- 1 alice developers 1250 Jun 19 notes.txt
```

Ownership changes are immediately visible.

---

## 🎯 Summary

The `chown` command changes file and directory ownership.

Common examples:

```bash
sudo chown alice file.txt
sudo chown alice:developers file.txt
sudo chown :developers file.txt
sudo chown -R alice project
```

Useful option:

```bash
-R
```

for recursive ownership changes.

Understanding ownership is a key Linux administration skill and is essential when working with servers, applications, and multi-user systems.
