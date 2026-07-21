# Day 057 - Linux Permissions in Depth

## 🧠 Introduction

Linux is a multi-user operating system.

Multiple users and processes may access the same files and directories. To protect data and control access, Linux uses a permission system.

Every file and directory has three basic permission categories:

```text
User      (u) → The owner

Group     (g) → Members of the file's group

Others    (o) → Everyone else
```

And three basic permissions:

```text
r → Read

w → Write

x → Execute
```

Understanding permissions is essential for Linux security and administration.

---

# Viewing Permissions

Use:

```bash
ls -l
```

Example:

```text
-rwxr-xr-- 1 john developers 1200 script.sh
```

The first ten characters represent permissions:

```text
- rwx r-x r--
│ │   │   │
│ │   │   └── Others
│ │   └────── Group
│ └────────── User
└──────────── File type
```

---

# Permission Meanings

## Read (`r`)

For files:

```text
Read the file's contents.
```

For directories:

```text
List the directory's contents.
```

---

## Write (`w`)

For files:

```text
Modify the file.
```

For directories:

```text
Create, delete, or rename files inside the directory.
```

---

## Execute (`x`)

For files:

```text
Run the file as a program or script.
```

For directories:

```text
Enter or access the directory.
```

---

# Changing Permissions with `chmod`

The `chmod` command changes file permissions.

Example:

```bash
chmod u+x script.sh
```

This gives the owner execute permission.

Remove write permission from others:

```bash
chmod o-w file.txt
```

Add read permission for the group:

```bash
chmod g+r file.txt
```

---

# Symbolic Permission Syntax

The basic format is:

```text
chmod [who][operator][permission] file
```

Users:

```text
u → User

g → Group

o → Others

a → All
```

Operators:

```text
+ → Add permission

- → Remove permission

= → Set exact permissions
```

Examples:

```bash
chmod u+x script.sh

chmod g+w project.txt

chmod o-r secret.txt

chmod a+r public.txt
```

---

# Numeric Permissions

Permissions can also be represented numerically.

Values:

```text
r = 4

w = 2

x = 1
```

Add the values together:

```text
rwx = 4 + 2 + 1 = 7

rw- = 4 + 2 = 6

r-x = 4 + 1 = 5

r-- = 4
```

Example:

```bash
chmod 755 script.sh
```

Means:

```text
User:   7 → rwx

Group:  5 → r-x

Others: 5 → r-x
```

Another example:

```bash
chmod 644 file.txt
```

Means:

```text
User:   6 → rw-

Group:  4 → r--

Others: 4 → r--
```

---

# Common Permission Combinations

```text
777 → rwxrwxrwx

755 → rwxr-xr-x

700 → rwx------

644 → rw-r--r--

600 → rw-------
```

Common usage:

```text
755 → Executable scripts and directories

644 → Regular files

700 → Private files and directories

600 → Sensitive files
```

Avoid using:

```bash
chmod 777
```

unless you fully understand the security implications.

---

# Changing Ownership with `chown`

The `chown` command changes the owner of a file.

Example:

```bash
sudo chown john file.txt
```

Change owner and group:

```bash
sudo chown john:developers file.txt
```

Change ownership recursively:

```bash
sudo chown -R john:developers project/
```

Option:

```text
-R = Recursive
```

Be careful when using recursive ownership changes.

---

# Changing Groups with `chgrp`

Change only the group:

```bash
sudo chgrp developers project/
```

Recursive:

```bash
sudo chgrp -R developers project/
```

---

# The `umask` Command

`umask` controls the default permissions of newly created files and directories.

Check the current value:

```bash
umask
```

Example:

```text
0022
```

A common default is:

```text
0022
```

This usually results in:

```text
Files:       644

Directories: 755
```

The reason is that newly created files typically start from:

```text
666
```

and directories from:

```text
777
```

The `umask` removes permissions from these defaults.

---

# Special Permission Bits

Linux also has three special permission mechanisms:

```text
SUID

SGID

Sticky Bit
```

These are particularly important for security and shared directories.

---

# SUID

SUID means **Set User ID**.

When an executable has SUID set, it runs with the permissions of the file owner.

Example:

```text
-rwsr-xr-x
```

The `s` appears in the owner's execute position.

Numeric form:

```bash
chmod 4755 program
```

A classic example is:

```text
/usr/bin/passwd
```

This allows regular users to change their password even though password-related files require elevated privileges.

SUID should be used carefully.

---

# SGID

SGID means **Set Group ID**.

For executable files:

```text
The program runs with the file's group permissions.
```

For directories:

```text
New files inherit the directory's group.
```

Example:

```bash
chmod 2775 shared/
```

This is useful for collaborative directories.

Example:

```text
shared/
├── file1.txt
└── file2.txt
```

All new files can automatically inherit the shared group's ownership.

---

# Sticky Bit

The Sticky Bit is commonly used on shared directories.

Example:

```text
/tmp
```

Typical permissions:

```text
drwxrwxrwt
```

The `t` at the end represents the Sticky Bit.

It means:

```text
Users can create files,

but generally cannot delete files belonging to other users.
```

Set it with:

```bash
chmod 1777 shared/
```

---

# Special Permission Summary

```text
SUID       4000

SGID       2000

Sticky Bit 1000
```

Examples:

```bash
chmod 4755 file

chmod 2775 directory

chmod 1777 shared/
```

---

# Real-World Examples

Make a script executable:

```bash
chmod +x deploy.sh
```

Set standard script permissions:

```bash
chmod 755 deploy.sh
```

Protect a private key:

```bash
chmod 600 ~/.ssh/id_ed25519
```

Change ownership:

```bash
sudo chown user:group file.txt
```

Create a shared directory:

```bash
sudo mkdir /shared
sudo chmod 2775 /shared
```

Protect a shared temporary directory:

```bash
sudo chmod 1777 /shared
```

These commands are commonly used in real Linux environments.

---

# Common Mistakes

### Using `chmod 777` Everywhere

This gives everyone full access.

It can create serious security problems.

Use the minimum permissions required.

---

### Forgetting Directory Execute Permission

A user may have read permission on a directory but still be unable to access files inside it.

Directories generally need:

```text
x
```

to be entered or traversed.

---

### Changing Ownership Recursively Without Care

This command:

```bash
sudo chown -R user:group /
```

would be extremely dangerous.

Always verify the target path before using:

```text
-R
```

---

### Confusing File and Directory Permissions

For a file:

```text
x → Execute the file
```

For a directory:

```text
x → Enter or traverse the directory
```

The same permission has different practical meanings.

---

# Why Permissions Matter

Imagine a web server running as:

```text
www-data
```

Your application files may need to be:

```text
Readable by www-data
```

but private configuration files should not be:

```text
Writable by every user
```

A correct permission model can prevent:

- Unauthorized data access
- Accidental file modification
- Privilege escalation
- Compromised services from modifying sensitive files

Permissions are one of the most important layers of Linux security.

---

# 🎯 Summary

Linux permissions control who can access files and directories.

Basic permissions:

```text
r → Read

w → Write

x → Execute
```

Permission categories:

```text
u → User

g → Group

o → Others
```

Important commands:

```bash
ls -l

chmod

chown

chgrp

umask
```

Common numeric permissions:

```text
755 → rwxr-xr-x

644 → rw-r--r--

700 → rwx------

600 → rw-------
```

Special permissions:

```text
SUID       4000

SGID       2000

Sticky Bit 1000
```

Mastering Linux permissions is essential for system security, multi-user environments, server administration, and safely managing applications and sensitive data.
