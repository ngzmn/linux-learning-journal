# Day 039 - Stream Editing with sed

## 🧠 Introduction

The `sed` (Stream Editor) command is one of the most powerful text-processing tools in Linux.

Unlike a traditional text editor, `sed` edits text automatically from the command line.

It is commonly used to:

- Replace text
- Delete lines
- Insert new lines
- Modify configuration files
- Process logs
- Automate repetitive editing tasks

System administrators and DevOps engineers frequently use `sed` in shell scripts because it can modify large files quickly without opening an editor.

---

# Basic Syntax

The general syntax is:

```bash
sed 'command' filename
```

Example:

```bash
sed 's/Linux/Ubuntu/' notes.txt
```

The `s` command means:

```text
s = substitute
```

It replaces the first occurrence of **Linux** with **Ubuntu** on each line.

---

# Replace Text

Suppose `notes.txt` contains:

```text
Linux is powerful.
Linux is open source.
```

Run:

```bash
sed 's/Linux/Ubuntu/' notes.txt
```

Output:

```text
Ubuntu is powerful.
Ubuntu is open source.
```

Notice that only the displayed output changes—the original file remains unchanged.

---

# Replace All Matches

By default, only the first match on each line is replaced.

Example:

```text
Linux Linux Linux
```

Command:

```bash
sed 's/Linux/Ubuntu/g' file.txt
```

Output:

```text
Ubuntu Ubuntu Ubuntu
```

Option:

```text
g = global (replace every match)
```

---

# Edit Files In Place

To modify the original file directly:

```bash
sed -i 's/Linux/Ubuntu/g' notes.txt
```

The `-i` option means:

```text
Edit the file itself.
```

Be careful, because the original content is overwritten.

---

# Delete Lines

Delete the third line:

```bash
sed '3d' notes.txt
```

Delete blank lines:

```bash
sed '/^$/d' notes.txt
```

Delete comment lines:

```bash
sed '/^#/d' config.conf
```

This is useful when cleaning configuration files.

---

# Print Specific Lines

Display only line 5:

```bash
sed -n '5p' notes.txt
```

Display lines 10 through 15:

```bash
sed -n '10,15p' notes.txt
```

Option:

```text
-n = suppress normal output
```

---

# Insert and Append Text

Insert a line before line 3:

```bash
sed '3i\New line inserted' notes.txt
```

Append a line after line 3:

```bash
sed '3a\New line appended' notes.txt
```

These commands are often used when generating configuration files automatically.

---

# Combining sed with Pipes

Replace text from another command:

```bash
echo "Linux is awesome" | sed 's/Linux/GNU\/Linux/'
```

Output:

```text
GNU/Linux is awesome
```

Search and replace inside a pipeline:

```bash
cat config.txt | sed 's/localhost/127.0.0.1/'
```

This avoids creating temporary files.

---

# Real-World Examples

Replace HTTP with HTTPS:

```bash
sed 's/http:/https:/g' links.txt
```

Remove comments from a configuration file:

```bash
sed '/^#/d' nginx.conf
```

Delete empty lines:

```bash
sed '/^$/d' notes.txt
```

Replace tabs with spaces:

```bash
sed 's/\t/    /g' file.txt
```

Edit a configuration file directly:

```bash
sed -i 's/DEBUG=true/DEBUG=false/' app.conf
```

These are practical tasks performed on Linux servers every day.

---

# Common Mistakes

### Forgetting the Global Flag

Command:

```bash
sed 's/test/demo/' file.txt
```

Only the first match on each line is replaced.

To replace every occurrence:

```bash
sed 's/test/demo/g' file.txt
```

---

### Editing Files Without a Backup

Running:

```bash
sed -i
```

changes the original file immediately.

For important files, create a backup first:

```bash
cp config.conf config.conf.bak
```

---

### Forgetting Quotes

Incorrect:

```bash
sed s/Linux/Ubuntu/ file.txt
```

Correct:

```bash
sed 's/Linux/Ubuntu/' file.txt
```

The editing expression should always be enclosed in quotes.

---

# Why sed Matters

Imagine a project containing hundreds of configuration files.

You need to change:

```text
localhost
```

to:

```text
127.0.0.1
```

Instead of editing every file manually, a simple `sed` command can perform the task automatically.

This ability makes `sed` an essential tool for automation, scripting, and server management.

---

# 🎯 Summary

The `sed` command edits text streams efficiently from the command line.

Common examples:

```bash
sed 's/Linux/Ubuntu/' file.txt

sed 's/Linux/Ubuntu/g' file.txt

sed -i 's/Linux/Ubuntu/g' file.txt

sed '3d' file.txt

sed '/^#/d' config.conf

sed -n '5p' file.txt

echo "Linux" | sed 's/Linux/GNU\/Linux/'
```

Important concepts:

```text
s      Substitute text

g      Replace all matches

-i     Edit the original file

d      Delete lines

p      Print selected lines

-n     Suppress automatic output
```

Mastering `sed` is essential because it enables fast, automated text editing for configuration files, log processing, deployment scripts, and many other Linux administration tasks.
