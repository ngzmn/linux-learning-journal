# Day 058 - Advanced File Searching with `find`

## 🧠 Introduction

The `find` command is one of the most powerful tools available on Linux.

Basic searches can find files by name or type, but `find` can do much more.

Advanced usage allows you to:

- Search by owner and group
- Search by permissions
- Search by modification time
- Combine multiple conditions
- Execute commands on matching files
- Delete matching files
- Use regular expressions
- Build powerful automation workflows

---

# Searching by Owner

Find all files owned by a specific user:

```bash
find /home -user john
```

Find files owned by root:

```bash
find / -user root
```

This is useful when investigating file ownership.

---

# Searching by Group

Find files belonging to a specific group:

```bash
find /var/www -group developers
```

You can combine owner and group conditions:

```bash
find /var/www -user john -group developers
```

---

# Searching by Permissions

Find files with exact permissions:

```bash
find . -perm 644
```

Find executable files:

```bash
find . -perm /111
```

Find files writable by everyone:

```bash
find . -perm -002
```

This can be useful during security audits.

---

# Searching by Modification Time

Find files modified within the last 24 hours:

```bash
find . -mtime 0
```

Find files modified more than 30 days ago:

```bash
find . -mtime +30
```

Find files modified less than 7 days ago:

```bash
find . -mtime -7
```

Time-based searches are extremely useful for backups and cleanup tasks.

---

# Searching by Access Time

Find files accessed within the last day:

```bash
find . -atime 0
```

Find files accessed more than 30 days ago:

```bash
find . -atime +30
```

---

# Searching by Change Time

Find files whose metadata changed recently:

```bash
find . -ctime -7
```

Important:

```text
mtime → Content modification time

atime → Last access time

ctime → Metadata/status change time
```

---

# Searching by File Size

Find files larger than 1 GB:

```bash
find / -size +1G
```

Find files smaller than 10 MB:

```bash
find . -size -10M
```

Find files exactly 100 MB:

```bash
find . -size 100M
```

Common units:

```text
c → Bytes

k → Kilobytes

M → Megabytes

G → Gigabytes
```

---

# Combining Conditions

Find all `.log` files larger than 100 MB:

```bash
find /var/log -type f -name "*.log" -size +100M
```

Find files modified in the last 7 days:

```bash
find . -type f -mtime -7
```

Find files that are both large and old:

```bash
find . -type f -size +500M -mtime +30
```

By default, multiple conditions are combined using logical AND.

---

# Using OR Conditions

Find files ending in `.log` or `.txt`:

```bash
find . \( -name "*.log" -o -name "*.txt" \)
```

Operators:

```text
-o → OR

!  → NOT
```

Example:

```bash
find . -type f \( -name "*.jpg" -o -name "*.png" \)
```

---

# Excluding Directories

Search everywhere except a specific directory:

```bash
find . -path "./node_modules" -prune -o -type f -print
```

This is useful when working with large projects.

For example:

```text
project/
├── src/
├── public/
└── node_modules/
```

You may want to search the project without scanning `node_modules`.

---

# The `-exec` Option

One of the most powerful features of `find` is:

```text
-exec
```

It allows you to run a command on every matching file.

Example:

```bash
find . -name "*.log" -exec ls -l {} \;
```

Here:

```text
{}  → Current matching file

\;  → End of the command
```

For every `.log` file, Linux runs:

```bash
ls -l filename
```

---

# Using `-exec` with Commands

Find all shell scripts and make them executable:

```bash
find . -name "*.sh" -exec chmod +x {} \;
```

Find all `.tmp` files and display their sizes:

```bash
find . -name "*.tmp" -exec du -h {} \;
```

Change ownership:

```bash
find /var/www -type f -exec chown www-data {} \;
```

Be careful when executing commands recursively.

---

# Using `+` Instead of `\;`

Compare:

```bash
find . -name "*.log" -exec ls -l {} \;
```

and:

```bash
find . -name "*.log" -exec ls -l {} +
```

With:

```text
\;
```

the command runs once per file.

With:

```text
+
```

multiple files are passed to the command at once.

The second version is usually more efficient.

---

# Deleting Matching Files

Delete all `.tmp` files:

```bash
find . -name "*.tmp" -delete
```

Delete logs older than 30 days:

```bash
find /var/log -name "*.log" -mtime +30 -delete
```

⚠️ Always test first:

```bash
find . -name "*.tmp"
```

Only after verifying the output should you use:

```bash
-delete
```

---

# Regular Expressions

`find` can search using regular expressions:

```bash
find . -regextype posix-extended \
-regex ".*\.(log|txt)$"
```

This finds files ending with:

```text
.log

.txt
```

Regular expressions allow more complex search patterns.

---

# The `-print0` Option

Filenames can contain spaces or special characters.

Instead of:

```bash
find . -type f -print
```

use:

```bash
find . -type f -print0
```

This separates filenames using a null character.

It is commonly combined with:

```bash
xargs -0
```

Example:

```bash
find . -type f -print0 | xargs -0 ls -l
```

This safely handles filenames containing spaces.

---

# `find` with `xargs`

Example:

```bash
find . -name "*.log" -print0 | xargs -0 rm
```

This deletes matching files efficiently.

However, always be careful when combining:

```text
find

+

xargs

+

rm
```

Test your search before executing destructive commands.

---

# Practical Security Audit

Find world-writable files:

```bash
find / -type f -perm -002 2>/dev/null
```

Find SUID files:

```bash
find / -perm -4000 -type f 2>/dev/null
```

Find files owned by a deleted user:

```bash
find / -nouser 2>/dev/null
```

Find files belonging to a deleted group:

```bash
find / -nogroup 2>/dev/null
```

These commands can help identify security and system maintenance issues.

---

# `find` vs `locate`

`find`:

```text
Searches the filesystem directly.

Results are current.

Can filter using many conditions.
```

`locate`:

```text
Searches a pre-built database.

Usually much faster.

The database may not be up to date.
```

Example:

```bash
locate nginx.conf
```

Update the database:

```bash
sudo updatedb
```

General rule:

```text
Need accurate results → find

Need fast filename search → locate
```

---

# Real-World Examples

Find large log files:

```bash
find /var/log -type f -size +100M
```

Delete temporary files older than 7 days:

```bash
find /tmp -type f -mtime +7 -delete
```

Make all shell scripts executable:

```bash
find . -name "*.sh" -exec chmod +x {} +
```

Find SUID binaries:

```bash
find / -perm -4000 -type f 2>/dev/null
```

Find files modified today:

```bash
find . -type f -mtime 0
```

Find files owned by a user:

```bash
find /home -user john
```

These commands demonstrate the power of combining search conditions and actions.

---

# Common Mistakes

### Deleting Before Testing

Never immediately run:

```bash
find . -delete
```

First verify:

```bash
find . -name "*.tmp"
```

Then add:

```text
-delete
```

---

### Forgetting Spaces in Expressions

Correct:

```bash
find . \( -name "*.log" -o -name "*.txt" \)
```

Incorrect:

```bash
find . \(-name "*.log"-o-name "*.txt"\)
```

Shell syntax matters.

---

### Running Dangerous Commands as Root

Be extremely careful with:

```bash
sudo find / -exec rm {} \;
```

A small mistake can destroy an entire system.

Always test commands on a limited directory first.

---

# Why Advanced `find` Matters

Imagine a server with millions of files.

You need to:

- Find files larger than 1 GB
- Locate old logs
- Identify insecure permissions
- Find files owned by a deleted user
- Modify hundreds of files at once

Instead of manually searching through directories, you can automate the entire process with `find`.

This makes `find` one of the most powerful tools for Linux administration, automation, and security auditing.

---

# 🎯 Summary

Advanced `find` usage allows you to search and manipulate files using powerful conditions.

Important options:

```text
-user       Search by owner

-group      Search by group

-perm       Search by permissions

-mtime      Search by modification time

-atime      Search by access time

-ctime      Search by metadata change time

-size       Search by file size

-exec       Execute commands on results

-delete      Delete matching files

-regex      Search using regular expressions

-print0     Safely handle special filenames
```

Useful combinations:

```bash
find . -type f -size +100M

find . -type f -mtime +30

find . -name "*.sh" -exec chmod +x {} +

find / -perm -4000 -type f 2>/dev/null

find . -print0 | xargs -0 ls -l
```

Mastering advanced `find` allows you to automate file management, perform security audits, clean up systems, and efficiently manage large Linux filesystems.
