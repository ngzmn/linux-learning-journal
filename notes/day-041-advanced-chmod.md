# Day 041 - Advanced File Permissions with chmod

## 🧠 Introduction

Linux is a multi-user operating system.

To protect files and directories, Linux uses a permission system that determines who can:

- Read a file
- Modify a file
- Execute a file

The `chmod` command is used to change these permissions.

Understanding `chmod` is essential for system administration, software development, and server security.

---

# Viewing File Permissions

Use:

```bash
ls -l
```

Example output:

```text
-rwxr-xr-- 1 john developers 2450 Jul 13 script.sh
```

The permission string is:

```text
-rwxr-xr--
```

Breaking it down:

```text
-          Regular file

rwx        Owner permissions

r-x        Group permissions

r--        Others permissions
```

---

# Understanding Permission Symbols

Each permission has a meaning:

```text
r = Read

w = Write

x = Execute
```

Permission values:

```text
r = 4

w = 2

x = 1
```

These numbers are added together.

Example:

```text
rwx = 7

rw- = 6

r-x = 5

r-- = 4

--- = 0
```

---

# Numeric (Octal) Permissions

The most common way to use `chmod` is with numbers.

Example:

```bash
chmod 755 script.sh
```

Meaning:

```text
Owner : 7 = rwx

Group : 5 = r-x

Others: 5 = r-x
```

Permissions become:

```text
rwxr-xr-x
```

---

## Another Example

```bash
chmod 644 notes.txt
```

Results in:

```text
rw-r--r--
```

Meaning:

Owner:

```text
Read + Write
```

Everyone else:

```text
Read only
```

This is the most common permission for text files.

---

# Symbolic Mode

Instead of numbers, you can use letters.

Give execute permission to the owner:

```bash
chmod u+x script.sh
```

Remove write permission from the group:

```bash
chmod g-w script.sh
```

Allow everyone to read:

```bash
chmod a+r script.sh
```

Symbols:

```text
u = User (owner)

g = Group

o = Others

a = All users
```

---

# Recursive Permission Changes

Change permissions for an entire directory:

```bash
chmod -R 755 website/
```

Option:

```text
-R = Recursive
```

This affects every file and subdirectory.

Be careful when using it on important directories.

---

# Special Permissions

Linux provides three advanced permission bits.

## SUID

```bash
chmod u+s program
```

Display:

```text
-rwsr-xr-x
```

When executed, the program runs with the owner's privileges.

Example:

```text
passwd
```

uses SUID so ordinary users can change their passwords.

---

## SGID

```bash
chmod g+s shared/
```

For directories:

- New files inherit the directory's group.

This is useful for shared project folders.

---

## Sticky Bit

```bash
chmod +t shared/
```

Display:

```text
drwxrwxrwt
```

Only the file owner can delete files.

Common example:

```text
/tmp
```

This improves security in shared directories.

---

# Real-World Examples

Make a shell script executable:

```bash
chmod +x backup.sh
```

Protect a configuration file:

```bash
chmod 600 secrets.conf
```

Create a public website directory:

```bash
chmod 755 public_html
```

Protect an SSH private key:

```bash
chmod 600 ~/.ssh/id_rsa
```

Git will even warn you if SSH keys are too permissive.

---

# Common Permission Values

```text
777  = Everyone has full access

755  = Executable programs

700  = Private executable files

644  = Normal text files

600  = Sensitive private files

400  = Read-only files
```

Understanding these values helps you configure systems securely.

---

# Common Mistakes

### Using 777 Everywhere

Some beginners solve permission problems with:

```bash
chmod 777 file
```

This allows everyone to:

- Read
- Write
- Execute

It creates serious security risks.

Use the minimum permissions required.

---

### Forgetting Execute Permission

Suppose you have:

```bash
backup.sh
```

Without execute permission:

```bash
./backup.sh
```

returns:

```text
Permission denied
```

Fix it:

```bash
chmod +x backup.sh
```

---

### Changing System Files Accidentally

Avoid running commands like:

```bash
chmod -R 777 /
```

This can damage your system and create major security issues.

Always verify the target directory before using recursive changes.

---

# Why chmod Matters

Imagine deploying a web application.

The web server must:

- Read HTML files
- Execute scripts
- Prevent unauthorized editing

Proper permissions make this possible.

Incorrect permissions can either break applications or expose sensitive data.

---

# 🎯 Summary

The `chmod` command changes file and directory permissions.

Common examples:

```bash
chmod 755 script.sh

chmod 644 notes.txt

chmod +x backup.sh

chmod -R 755 website/

chmod 600 ~/.ssh/id_rsa
```

Important concepts:

```text
r = Read (4)

w = Write (2)

x = Execute (1)

755 = rwxr-xr-x

644 = rw-r--r--

600 = rw-------
```

Understanding `chmod` is essential for Linux security, server administration, software deployment, and protecting sensitive files.
