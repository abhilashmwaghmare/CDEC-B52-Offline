# 📦 Linux Archiving, Compression & Cron – Complete Automation Guide

![Linux](https://img.shields.io/badge/Linux-Admin-blue)
![DevOps](https://img.shields.io/badge/DevOps-Automation-green)
![Interview](https://img.shields.io/badge/Interview-Preparation-orange)

> A production-ready, interview-focused guide to **Archiving, Compression, and Cron Automation in Linux** with real-world use cases, commands, hands-on labs, and interview questions.

---

## 📌 Table of Contents

1. [Overview of Archiving](#overview-of-archiving)
2. [Common Use Cases](#common-use-cases)
3. [Creating and Extracting Archives with tar](#creating-and-extracting-archives-with-tar)
4. [Managing Archive Contents](#managing-archive-contents)
5. [Introduction to Compression](#introduction-to-compression)
6. [Role of Compression](#role-of-compression)
7. [Compression Formats Comparison](#compression-formats-comparison)
8. [Using gzip and gunzip](#using-gzip-and-gunzip)
9. [Using bzip2 and bunzip2](#using-bzip2-and-bunzip2)
10. [Using xz and unxz](#using-xz-and-unxz)
11. [Combining Archiving and Compression](#combining-archiving-and-compression)
12. [Practical: Compressing with tar + gzip/bzip2/xz](#practical-compressing)
13. [Practical: Decompressing Archives](#practical-decompressing)
14. [Introduction to CronTab](#introduction-to-crontab)
15. [Understanding CronTab Syntax](#understanding-crontab-syntax)
16. [Creating and Managing Cron Jobs](#creating-and-managing-cron-jobs)
17. [Automating Routine Tasks](#automating-routine-tasks)
18. [Hands-on Labs](#hands-on-labs)
19. [Interview Practice Questions](#interview-practice-questions)
20. [Quick Revision Cheat Sheet](#quick-revision-cheat-sheet)

---

## 🧭 Overview of Archiving

**Archiving** means combining multiple files/directories into a single file for:
- Easy storage
- Transfer
- Backup

Archiving does **not** reduce size by itself (compression does that).

---

## 🎯 Common Use Cases

| Use Case | Example |
|---------|--------|
| Backups | Daily `/etc` backup |
| Data Transfer | Sending logs to another server |
| Organization | Packing project folders |

**Real-time Use Case:**
Nightly backup of `/var/www` using tar + gzip.

---

## 📦 Creating and Extracting Archives with tar

### Create Archive
```bash
tar -cvf backup.tar /data
```

Options:
- `c` → create
- `v` → verbose
- `f` → file name

### Extract Archive
```bash
tar -xvf backup.tar
```

Extract to specific directory:
```bash
tar -xvf backup.tar -C /restore
```

---

## 📂 Managing Archive Contents

### List Contents
```bash
tar -tvf backup.tar
```

### Extract Single File
```bash
tar -xvf backup.tar file1.txt
```

### Append Files
```bash
tar -rvf backup.tar newfile.txt
```

---

## 🗜 Introduction to Compression

**Compression** reduces file size to:
- Save disk space
- Speed up transfers

Compression is applied **after archiving** or on single files.

---

## 📉 Role of Compression in Reducing File Sizes

Benefits:
- Less storage cost
- Faster backups
- Efficient network usage

Trade-off:
- CPU usage during compress/decompress

---

## ⚖ Compression Formats Comparison

| Format | Command | Speed | Compression | Extension |
|------|--------|------|-------------|-----------|
| gzip | gzip | Fast | Medium | .gz |
| bzip2 | bzip2 | Slow | High | .bz2 |
| xz | xz | Slowest | Highest | .xz |

---

## 🟦 Using gzip and gunzip

### Compress
```bash
gzip file.txt
```

### Decompress
```bash
gunzip file.txt.gz
```

Keep original:
```bash
gzip -k file.txt
```

---

## 🟨 Using bzip2 and bunzip2

```bash
bzip2 file.txt
bunzip2 file.txt.bz2
```

---

## 🟥 Using xz and unxz

```bash
xz file.txt
unxz file.txt.xz
```

---

## 🔗 Combining Archiving and Compression

Most common combinations:

| Command | Result |
|-------|--------|
| `tar -czf` | tar + gzip (.tar.gz) |
| `tar -cjf` | tar + bzip2 (.tar.bz2) |
| `tar -cJf` | tar + xz (.tar.xz) |

---

## 🧪 Practical: Compressing Files

### Using gzip
```bash
tar -czf backup.tar.gz /data
```

### Using bzip2
```bash
tar -cjf backup.tar.bz2 /data
```

### Using xz
```bash
tar -cJf backup.tar.xz /data
```

---

## 🧪 Practical: Decompressing Files

```bash
tar -xzf backup.tar.gz
tar -xjf backup.tar.bz2
tar -xJf backup.tar.xz
```

Single-file decompress:
```bash
gunzip file.gz
bunzip2 file.bz2
unxz file.xz
```

---

## ⏰ Introduction to CronTab

`cron` is used to **schedule recurring jobs**.

Examples:
- Daily backups
- Log cleanup
- System updates

Edit crontab:
```bash
crontab -e
```

---

## 🧩 Understanding The CronTab Syntax

Format:
```text
* * * * * command
| | | | |
| | | | +-- Day of week (0-7)
| | | +---- Month (1-12)
| | +------ Day of month (1-31)
| +-------- Hour (0-23)
+---------- Minute (0-59)
```

Example:
```bash
0 2 * * * /backup.sh
```
Runs daily at 2 AM.

---

## ⚙️ Creating and Managing Cron Jobs

### List Jobs
```bash
crontab -l
```

### Remove Jobs
```bash
crontab -r
```

### System-wide Cron

Directories:
- `/etc/cron.hourly`
- `/etc/cron.daily`
- `/etc/cron.weekly`

---

## 🤖 Automating Routine Tasks

### Backup Automation
```bash
0 1 * * * tar -czf /backup/etc_$(date +\%F).tar.gz /etc
```

### Cleanup Logs
```bash
0 3 * * 0 find /var/log -type f -mtime +30 -delete
```

### System Updates
```bash
0 4 * * 6 yum update -y
```

---

## 🧪 Hands-on Labs

### Lab 1: Backup Automation
1. Create `/backup` directory
2. Create tar.gz of `/etc`
3. Schedule via cron daily at 1 AM

---

### Lab 2: Compression Comparison
1. Compress same folder using gzip, bzip2, xz
2. Compare file sizes and time taken

---

## 🎯 Interview Practice Questions

### Conceptual
1. Difference between archiving and compression?
2. gzip vs bzip2 vs xz?
3. Where are cron jobs stored?

### Scenario-Based
1. Automate daily backup of `/var/www`.
2. Cleanup logs older than 15 days every Sunday.
3. Restore only one file from a tar archive.

---

## 📌 Quick Revision Cheat Sheet

| Task | Command |
|-----|--------|
| Create tar | `tar -cvf a.tar dir` |
| Extract tar | `tar -xvf a.tar` |
| tar.gz | `tar -czf a.tar.gz dir` |
| List cron | `crontab -l` |
| Edit cron | `crontab -e` |

---

## 🚀 Suggested Next Topics

- rsync & incremental backups
- logrotate configuration
- systemd timers
- Backup strategies in production

---

## 🤝 Contributing

Add:
- More labs
- Production cron examples
- Backup scripts

---

## 📄 License

MIT License

