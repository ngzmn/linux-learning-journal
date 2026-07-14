# Day 042 - File Ownership with chown and chgrp

## 🧠 Introduction

Every file and directory in Linux has:

- An owner (user)
- A group

Ownership determines who is responsible for a file, while permissions determine what each user is allowed to do.

Understanding ownership is essential when managing Linux servers, deploying applications, configuring web servers, or working with multiple users.

---

# Viewing Ownership

Use:

```bash
ls -l
```

Example:

```text
-rw-r--r-- 1 john developers 1520 Jul 14 report.txt
```

Explanation:

```text
john        → Owner

developers  → Group
```

Every file belongs to exactly one owner and one group.

---

# The chown Command

The `chown` command changes the owner of a file or directory.

Basic syntax:

```bash
chown new_owner filename
```

Example:

```bash
sudo chown alice report.txt
```

Now:

```text
Owner → alice
```

The group remains unchanged.

Usually, changing ownership requires root privileges.

---

# Changing Owner and Group Together

You can change both at the same time.

Example:

```bash
sudo chown alice:developers report.txt
```

Result:

```text
Owner → alice

Group → developers
```

This is commonly used after deploying applications.

---

# Changing Ownership Recursively

To change ownership for an entire directory:

```bash
sudo chown -R alice:developers project/
```

Option:

```text
-R = Recursive
```

Every file and subdirectory inside `project/` will receive the new owner and group.

---

# The chgrp Command

The `chgrp` command changes only the group.

Example:

```bash
sudo chgrp developers report.txt
```

Owner:

```text
Unchanged
```

Group:

```text
developers
```

This is useful when multiple users collaborate on the same project.

---

# When to Use chown vs chgrp

Use `chown` when:

- Transferring file ownership
- Deploying applications
- Restoring backups

Use `chgrp` when:

- Assigning files to a shared team
- Updating project permissions
- Organizing collaborative work

---

# Real-World Examples

Give ownership of a website to the web server:

```bash
sudo chown -R www-data:www-data /var/www/html
```

Change ownership of your project:

```bash
sudo chown -R $USER:$USER my-project
```

Assign a shared group:

```bash
sudo chgrp developers shared-folder
```

Fix ownership after copying files:

```bash
sudo chown -R john:john Documents/
```

These are common administrative tasks.

---

# Ownership vs Permissions

These concepts are different.

Ownership answers:

```text
Who owns the file?
```

Permissions answer:

```text
What can users do with the file?
```

Example:

```text
Owner:
alice

Permissions:
rw-r--r--
```

Only Alice can modify the file.

Everyone else can read it.

---

# Common Mistakes

### Confusing chown with chmod

Incorrect assumption:

```text
chown changes permissions.
```

Reality:

```text
chown changes ownership.

chmod changes permissions.
```

They serve different purposes.

---

### Forgetting sudo

Running:

```bash
chown alice file.txt
```

may result in:

```text
Operation not permitted
```

Use:

```bash
sudo chown alice file.txt
```

when administrative privileges are required.

---

### Recursive Changes in the Wrong Directory

Always verify the target before running:

```bash
sudo chown -R
```

Changing ownership of the wrong directory can break applications or system services.

---

# Why Ownership Matters

Suppose a web application cannot write uploaded files.

Permissions appear correct:

```text
rw-rw-r--
```

However, the owner is:

```text
root
```

while the web server runs as:

```text
www-data
```

Changing the owner with:

```bash
sudo chown -R www-data:www-data uploads/
```

solves the problem.

Ownership issues are among the most common causes of deployment errors on Linux servers.

---

# 🎯 Summary

The `chown` and `chgrp` commands manage file ownership.

Common examples:

```bash
sudo chown alice report.txt

sudo chown alice:developers report.txt

sudo chown -R alice:developers project/

sudo chgrp developers report.txt

sudo chown -R www-data:www-data /var/www/html
```

Important concepts:

```text
Owner → User who owns the file

Group → Users who share access

chown → Change owner

chgrp → Change group

-R → Apply changes recursively
```

Understanding ownership is essential because Linux security depends on both permissions and ownership working together. Proper ownership prevents unauthorized access while allowing legitimate users and services to work correctly.
