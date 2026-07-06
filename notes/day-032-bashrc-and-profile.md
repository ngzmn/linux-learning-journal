# Day 032 - Shell Configuration Files (.bashrc and .profile)

## 🧠 Introduction

In the previous lesson, we learned that environment variables created with `export` exist only for the current shell session.

When you close the terminal, they disappear.

Linux solves this problem using shell configuration files.

These files allow you to:

- Store permanent environment variables
- Create aliases
- Customize the shell prompt
- Configure startup behavior
- Automatically execute commands when a shell starts

Understanding these files is essential for every Linux user.

---

## What Happens When You Open a Terminal?

Every time a terminal starts, Bash reads one or more configuration files.

Depending on how Bash starts, different files are loaded.

The two most common files are:

```text
~/.bashrc
~/.profile
```

Both are located in your home directory.

---

## Understanding ~/.bashrc

The `.bashrc` file is executed whenever an interactive Bash shell starts.

Typical uses include:

- Aliases
- Shell functions
- Prompt customization
- Environment variables
- Useful startup commands

View the file:

```bash
cat ~/.bashrc
```

Edit it:

```bash
nano ~/.bashrc
```

---

## Understanding ~/.profile

The `.profile` file is executed when you log in.

Typical uses include:

- Login environment variables
- PATH configuration
- Startup applications
- Session-wide settings

View the file:

```bash
cat ~/.profile
```

Edit it:

```bash
nano ~/.profile
```

---

## When Are These Files Loaded?

### ~/.profile

Runs:

- At login
- SSH sessions
- Graphical desktop login

Usually runs only once per login session.

---

### ~/.bashrc

Runs:

- Every interactive Bash terminal
- Every new terminal window
- Every new Bash shell

This makes it ideal for shell customization.

---

## Adding a Permanent Environment Variable

Open:

```bash
nano ~/.bashrc
```

Add:

```bash
export PROJECT_NAME="Linux Journal"
```

Save the file.

Reload it:

```bash
source ~/.bashrc
```

Verify:

```bash
echo $PROJECT_NAME
```

Output:

```text
Linux Journal
```

The variable will now be available whenever a new terminal starts.

---

## Creating Aliases

Aliases create shortcuts for commands.

Example:

```bash
alias ll="ls -lh"
```

Now instead of:

```bash
ls -lh
```

you can simply type:

```bash
ll
```

Another useful alias:

```bash
alias update="sudo apt update && sudo apt upgrade"
```

This saves time during daily administration.

---

## Customizing the Prompt

The shell prompt is controlled by:

```text
PS1
```

Example:

```bash
export PS1="\u@\h:\w\$ "
```

Result:

```text
john@ubuntu:~/projects$
```

Many Linux users personalize their prompt for productivity.

---

## Reloading Configuration Files

After editing `.bashrc`, changes do not apply automatically.

Reload the file:

```bash
source ~/.bashrc
```

Equivalent command:

```bash
. ~/.bashrc
```

No logout is required.

---

## Real-World Examples

Create a permanent alias:

```bash
alias gs="git status"
```

Store a custom PATH:

```bash
export PATH=$PATH:$HOME/scripts
```

Set a preferred editor:

```bash
export EDITOR=nano
```

Create a project variable:

```bash
export PROJECT_ROOT=$HOME/projects
```

These customizations are common among developers and system administrators.

---

## Common Mistakes

### Forgetting to Reload .bashrc

After editing:

```bash
nano ~/.bashrc
```

many users expect changes immediately.

Instead, run:

```bash
source ~/.bashrc
```

---

### Editing the Wrong File

Use:

```text
.bashrc
```

for interactive shell settings.

Use:

```text
.profile
```

for login-related configuration.

Knowing the difference avoids confusion.

---

### Overwriting PATH

Incorrect:

```bash
export PATH=$HOME/scripts
```

Correct:

```bash
export PATH=$PATH:$HOME/scripts
```

Always append to the existing PATH unless you intentionally want to replace it.

---

## Why These Files Matter

Imagine opening a new terminal.

Immediately, you have:

- Your favorite aliases
- A customized prompt
- Environment variables
- Development tools in PATH
- Project-specific settings

All of this is possible because `.bashrc` and `.profile` are loaded automatically.

Every experienced Linux user customizes these files.

---

## 🎯 Summary

The `.bashrc` and `.profile` files configure your Linux shell environment.

Common commands:

```bash
cat ~/.bashrc
nano ~/.bashrc

cat ~/.profile
nano ~/.profile

source ~/.bashrc
```

Useful additions:

```bash
export PROJECT_NAME="Linux Journal"

alias ll="ls -lh"

export PATH=$PATH:$HOME/scripts
```

Key concepts:

```text
.bashrc  = Interactive shell configuration
.profile = Login session configuration
source   = Reload configuration without restarting the shell
alias    = Command shortcut
PS1      = Shell prompt customization
```

Understanding these configuration files is essential because they allow you to build a productive, personalized, and permanent Linux working environment.
