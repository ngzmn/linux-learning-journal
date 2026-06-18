# Day 016 - Changing Permissions with chmod

## 🧠 Introduction

After learning how Linux permissions work, the next step is learning how to change them.

The `chmod` command stands for:

```text
change mode
```

It is used to modify file and directory permissions.

This is one of the most important Linux commands for system administration, security, and software development.

---

## Viewing Current Permissions

Before changing permissions, check them:

```bash
ls -l
```

Example:

```text
-rw-r--r-- script.sh
```

Current permissions:

- Owner: read, write
- Group: read
- Others: read

---

## Symbolic Method

Permissions can be changed using letters.

Symbols:

```text
u = user (owner)
g = group
o = others
a = all
```

Operations:

```text
+ add permission
- remove permission
= set exact permission
```

---

## Add Execute Permission

Make a script executable:

```bash
chmod +x script.sh
```

Before:

```text
-rw-r--r--
```

After:

```text
-rwxr-xr-x
```

Now the script can be executed.

---

## Remove Write Permission

```bash
chmod -w notes.txt
```

The file becomes read-only.

---

## Grant Permission to Owner Only

```bash
chmod u+rwx private.txt
```

Owner receives:

- Read
- Write
- Execute

permissions.

---

## Numeric Method

Linux permissions can also be represented using numbers.

Values:

```text
r = 4
w = 2
x = 1
```

Add them together:

```text
7 = rwx = 4+2+1
6 = rw- = 4+2
5 = r-x = 4+1
4 = r--
```

---

## Common Examples

### chmod 755

```bash
chmod 755 script.sh
```

Meaning:

```text
Owner  = rwx = 7
Group  = r-x = 5
Others = r-x = 5
```

Result:

```text
-rwxr-xr-x
```

Common for executable scripts.

---

### chmod 644

```bash
chmod 644 README.md
```

Meaning:

```text
Owner  = rw-
Group  = r--
Others = r--
```

Result:

```text
-rw-r--r--
```

Common for text files.

---

### chmod 600

```bash
chmod 600 secrets.txt
```

Result:

```text
-rw-------
```

Only the owner can access the file.

Useful for private configuration files.

---

## Real-World Examples

Make a shell script executable:

```bash
chmod +x backup.sh
```

Secure an SSH private key:

```bash
chmod 600 id_rsa
```

Set a website deployment script:

```bash
chmod 755 deploy.sh
```

These are tasks Linux users perform regularly.

---

## Common Mistakes

### Forgetting Execute Permission

Trying to run:

```bash
./script.sh
```

may result in:

```text
Permission denied
```

Fix:

```bash
chmod +x script.sh
```

---

### Using chmod 777

Example:

```bash
chmod 777 file.txt
```

This grants everyone:

```text
rwxrwxrwx
```

While useful for testing, it is usually insecure and should be avoided on production systems.

---

## 🎯 Summary

The `chmod` command changes permissions on files and directories.

Common examples:

```bash
chmod +x script.sh
chmod 644 README.md
chmod 755 deploy.sh
chmod 600 secrets.txt
```

Important permission values:

```text
755 → rwxr-xr-x
644 → rw-r--r--
600 → rw-------
```

Understanding `chmod` is essential for managing Linux systems securely and effectively.
