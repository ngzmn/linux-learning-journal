# Day 055 - Scheduling Tasks with `cron` and `at`

## 🧠 Introduction

Many Linux tasks need to run automatically.

Examples include:

- Backups
- Log cleanup
- Database dumps
- System updates
- Monitoring scripts
- Sending reports

Linux provides two major scheduling tools:

- `cron`
- `at`

Use:

```text
cron
```

for recurring tasks.

Use:

```text
at
```

for one-time scheduled tasks.

Automation is one of the most important Linux administration skills.

---

# What is Cron?

Cron is a background service that automatically runs commands at specific times.

It continuously checks scheduled jobs and executes them when their time arrives.

Examples:

- Run a backup every day
- Clean temporary files every week
- Restart a service every month
- Execute monitoring scripts every five minutes

---

# The Crontab

Each user can have their own cron schedule.

View your current cron jobs:

```bash
crontab -l
```

Edit your cron jobs:

```bash
crontab -e
```

Remove all cron jobs:

```bash
crontab -r
```

Use `crontab -r` carefully because it deletes every scheduled task.

---

# Cron Syntax

A cron entry contains five time fields:

```text
* * * * * command
│ │ │ │ │
│ │ │ │ └── Day of week (0-7)
│ │ │ └──── Month (1-12)
│ │ └────── Day of month (1-31)
│ └──────── Hour (0-23)
└────────── Minute (0-59)
```

Example:

```bash
30 2 * * * backup.sh
```

Meaning:

```text
Run at 02:30 every day.
```

---

# Special Characters

Every minute:

```bash
* * * * * command
```

Every hour:

```bash
0 * * * * command
```

Every day at midnight:

```bash
0 0 * * * command
```

Every Sunday:

```bash
0 3 * * 0 command
```

Every five minutes:

```bash
*/5 * * * * command
```

Every ten minutes:

```bash
*/10 * * * * command
```

---

# Useful Cron Examples

Run a backup every day:

```bash
0 2 * * * /home/john/backup.sh
```

Clear temporary files weekly:

```bash
0 1 * * 0 rm -rf /tmp/*
```

Run a script every five minutes:

```bash
*/5 * * * * /home/john/check.sh
```

Restart a service every month:

```bash
0 3 1 * * systemctl restart nginx
```

These are common administrative tasks.

---

# Redirecting Output

Cron emails command output by default.

Redirect output to a file:

```bash
0 2 * * * backup.sh > backup.log
```

Append output:

```bash
0 2 * * * backup.sh >> backup.log
```

Discard output:

```bash
0 2 * * * backup.sh > /dev/null 2>&1
```

This is commonly used for silent background jobs.

---

# What is `at`?

`at` schedules a command to run **once** at a specific time.

Example:

```bash
at 18:00
```

Then enter:

```bash
echo "Hello"
```

Finish with:

```text
Ctrl + D
```

The command will execute at 18:00.

---

# Scheduling with At

Run in one hour:

```bash
at now + 1 hour
```

Run tomorrow:

```bash
at 10:00 tomorrow
```

Run next week:

```bash
at 09:00 next week
```

The syntax is very flexible.

---

# Viewing Scheduled At Jobs

List scheduled jobs:

```bash
atq
```

Example:

```text
3 Tue Jul 21 18:00:00 2026 a john
```

Each job has an ID.

---

# Removing At Jobs

Delete a job:

```bash
atrm 3
```

This removes job number 3.

---

# Cron vs At

| Feature | cron | at |
|--------|------|----|
| Repeating tasks | ✅ | ❌ |
| One-time tasks | ❌ | ✅ |
| Recurring automation | ✅ | ❌ |
| Flexible scheduling | Moderate | Excellent |
| System administration | Excellent | Good |

General rule:

```text
cron → Repeat forever

at → Run once
```

---

# Real-World Examples

Daily backup:

```bash
0 1 * * * /usr/local/bin/backup.sh
```

Run monitoring every minute:

```bash
* * * * * check_disk.sh
```

Restart a service every Sunday:

```bash
0 4 * * 0 systemctl restart nginx
```

Shutdown after two hours:

```bash
at now + 2 hours
shutdown -h now
```

Schedule a reminder:

```bash
at 18:00
notify-send "Meeting"
```

Automation saves time and reduces human error.

---

# Common Mistakes

### Using Relative Paths

Cron may use a minimal environment.

Instead of:

```bash
backup.sh
```

use:

```bash
/home/john/scripts/backup.sh
```

Always use full paths.

---

### Forgetting Execution Permissions

Scripts should be executable:

```bash
chmod +x backup.sh
```

Otherwise cron may fail to run them.

---

### Expecting Environment Variables

Cron jobs often have fewer environment variables than interactive shells.

If necessary, define variables explicitly inside your script.

---

# Why Scheduling Matters

Imagine you manually back up a database every night.

Eventually you forget.

Instead:

```bash
0 2 * * * backup.sh
```

Linux performs the task automatically every day.

This is one of the main reasons Linux servers can run reliably for months or years with minimal human intervention.

---

# 🎯 Summary

`cron` and `at` automate tasks in Linux.

Common commands:

```bash
crontab -l

crontab -e

crontab -r

at 18:00

at now + 1 hour

atq

atrm 3
```

Common cron examples:

```bash
* * * * * command

*/5 * * * * command

0 0 * * * command

0 2 * * * backup.sh

0 3 * * 0 cleanup.sh
```

Important concepts:

```text
cron      Repeating tasks

at        One-time tasks

crontab   User cron configuration

atq       List at jobs

atrm      Remove at jobs
```

Mastering `cron` and `at` allows you to automate maintenance, backups, monitoring, reports, and repetitive administrative tasks across Linux systems.
