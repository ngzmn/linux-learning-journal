# Day 031 - Managing Environment Variables with export

## 🧠 Introduction

In the previous lesson, we learned that Linux programs use environment variables to determine their behavior.

However, simply creating a variable does not automatically make it available to child processes.

This is where the `export` command becomes important.

The `export` command marks variables so that:

- Child shells can access them
- Programs launched from the terminal can use them
- Scripts inherit their values
- Development tools receive configuration information

Understanding `export` is fundamental for shell scripting, DevOps, and software development.

---

## Shell Variables vs Environment Variables

Create a normal shell variable:

```bash
MY_NAME=Alice
```

Display it:

```bash
echo $MY_NAME
```

Output:

```text
Alice
```

Now start a child shell:

```bash
bash
```

Check the variable:

```bash
echo $MY_NAME
```

Output:

```text
(empty)
```

The child process cannot see it.

---

## Using export

Instead:

```bash
export MY_NAME=Alice
```

Start a child shell:

```bash
bash
```

Check:

```bash
echo $MY_NAME
```

Output:

```text
Alice
```

The variable is now inherited.

---

## Exporting Existing Variables

You can export a variable after creating it.

Example:

```bash
PROJECT=linux-journal
export PROJECT
```

Verify:

```bash
printenv PROJECT
```

Output:

```text
linux-journal
```

---

## Viewing Exported Variables

Display all exported variables:

```bash
export
```

Example output:

```text
declare -x HOME="/home/john"
declare -x PATH="/usr/bin:/bin"
declare -x USER="john"
```

Another method:

```bash
printenv
```

Both are useful for debugging.

---

## Temporary Environment Variables

You can create variables for a single command:

```bash
EDITOR=nano nano notes.txt
```

Only that process receives:

```text
EDITOR=nano
```

After the command finishes, the value disappears.

This technique is common in automation scripts.

---

## Real-World Examples

Set a default editor:

```bash
export EDITOR=nano
```

Configure Java:

```bash
export JAVA_HOME=/usr/lib/jvm/java-21-openjdk
```

Set a custom application path:

```bash
export APP_ENV=development
```

Store an API endpoint:

```bash
export API_URL=https://api.example.com
```

These patterns appear everywhere in development environments.

---

## Using export in Shell Scripts

Example script:

```bash
#!/bin/bash

export PROJECT_NAME="Linux Notes"

bash child.sh
```

Inside:

```bash
child.sh
```

the variable remains available:

```bash
echo $PROJECT_NAME
```

This is critical for multi-script systems.

---

## Understanding PATH with export

One of the most common uses:

```bash
export PATH=$PATH:/home/john/scripts
```

Explanation:

```text
Existing PATH
+
New directory
```

Now commands inside:

```text
/home/john/scripts
```

can run directly:

```bash
mytool
```

instead of:

```bash
/home/john/scripts/mytool
```

---

## Common DevOps Environment Variables

Examples include:

```text
DATABASE_URL
SECRET_KEY
API_TOKEN
NODE_ENV
JAVA_HOME
PYTHONPATH
```

Container platforms such as Docker and Kubernetes rely heavily on environment variables for configuration.

Modern cloud applications use them extensively.

---

## Common Mistakes

### Forgetting export

Incorrect:

```bash
API_KEY=abc123
python app.py
```

The application may not receive the variable.

Correct:

```bash
export API_KEY=abc123
python app.py
```

---

### Overwriting PATH

Dangerous:

```bash
export PATH=/home/john/scripts
```

System commands may stop working.

Safer:

```bash
export PATH=$PATH:/home/john/scripts
```

Always append instead of replacing.

---

### Expecting Variables to Survive Reboots

Example:

```bash
export MY_VAR=test
```

After reopening the terminal:

```text
MY_VAR disappears
```

Permanent variables require configuration files such as:

```text
~/.bashrc
~/.profile
```

We will study those next.

---

## Why export Matters

Imagine deploying an application.

Questions arise:

```text
Where is Java installed?
Which database should be used?
Which API key is valid?
What environment is this server running?
```

Environment variables answer all these questions.

The `export` command makes that information available to applications and scripts.

---

## 🎯 Summary

The `export` command converts shell variables into environment variables.

Common examples:

```bash
export MY_VAR=hello

PROJECT=linux-journal
export PROJECT

export PATH=$PATH:/home/john/scripts

printenv
export
```

Important concepts:

```text
Shell Variable       = Current shell only
Environment Variable = Available to child processes
PATH                 = Executable search directories
JAVA_HOME            = Java installation path
API_KEY              = Application configuration
```

Understanding `export` is essential because Linux shells, automation scripts, cloud deployments, Docker containers, and modern software systems all depend heavily on environment variables.
