# 🔗 Linux Links & sudo – Link Count, Hard vs Soft Links and Privilege Escalation

![Linux](https://img.shields.io/badge/Linux-Admin-blue)
![Security](https://img.shields.io/badge/Security-Privilege_Escalation-red)
![Interview](https://img.shields.io/badge/Interview-Preparation-orange)

> A production-ready, interview-focused guide to **Link Count, Hard vs Soft Links, and sudo Privilege Escalation** with real-time use cases, commands, labs, and interview questions.

---

## 📌 Table of Contents

1. [Link Count Basics](#link-count-basics)
2. [Link Count for Directories](#link-count-for-directories)
3. [Link Count for Files](#link-count-for-files)
4. [Comparing Hard and Soft Links](#comparing-hard-and-soft-links)
5. [Importance of sudo for Privilege Escalation](#importance-of-sudo-for-privilege-escalation)
6. [Regular User vs sudo Commands](#regular-user-vs-sudo-commands)
7. [Configuring sudo Access](#configuring-sudo-access)
8. [sudo Command Syntax and Examples](#sudo-command-syntax-and-examples)
9. [Hands-on Labs](#hands-on-labs)
10. [Interview Practice Questions](#interview-practice-questions)
11. [Quick Revision Cheat Sheet](#quick-revision-cheat-sheet)

---

## 🔢 Link Count Basics

Every file and directory in Linux has a **link count** – the number of directory entries pointing to the same inode.

View link count:
```bash
ls -l file.txt
```

Example:
```text
-rw-r--r-- 2 user user 1024 Jan 20 10:00 file.txt
```
Here, `2` is the link count.

### Why Link Count Matters
- Determines when disk space is freed
- Helps detect hard links
- Important in backup and recovery

---

## 📂 Link Count for Directories

For directories:
- `.` → self reference
- `..` → parent directory reference

Minimum link count is **2**.

Example:
```bash
ls -ld /home/user1
drwxr-xr-x 3 user1 user1 4096 Jan 20 10:00 user1
```

Link count = 3 means:
- `.` (self)
- `..` (parent)
- One subdirectory inside

### Real-time Use Case
Counting subdirectories quickly by checking link count.

---

## 📄 Link Count for Files

For regular files:
- Link count = number of hard links

Example:
```bash
touch file1
ln file1 file2
ls -l file1 file2
```

Output:
```text
-rw-r--r-- 2 user user file1
-rw-r--r-- 2 user user file2
```

Both names point to the **same inode**.

---

## 🔗 Comparing Hard and Soft Links

### Hard Links
- Same inode
- Cannot link directories
- Cannot cross filesystems
- Survive if original file is deleted

Create:
```bash
ln original.txt hardlink.txt
```

---

### Soft (Symbolic) Links
- Different inode
- Points to filename
- Can cross filesystems
- Breaks if target deleted

Create:
```bash
ln -s original.txt softlink.txt
```

---

### Comparison Table

| Feature | Hard Link | Soft Link |
|-------|----------|----------|
| Inode | Same | Different |
| Cross FS | ❌ | ✅ |
| Link to dir | ❌ | ✅ |
| Delete target | Still works | Breaks |

---

## 🛡 Importance of sudo for Privilege Escalation

`sudo` allows a normal user to run commands as **root** securely.

Why sudo is important:
- No sharing root password
- Command-level auditing
- Least privilege principle

### Real-time Use Case
Allow DevOps engineers to restart services without full root access.

---

## ⚖ Regular User vs sudo Commands

Example:
```bash
systemctl restart nginx
```

Output:
```text
Permission denied
```

With sudo:
```bash
sudo systemctl restart nginx
```

### Key Differences

| Aspect | Normal User | With sudo |
|------|------------|-----------|
| Privileges | Limited | Elevated |
| Audit | No log | Logged |
| Risk | Low | High if misused |

---

## ⚙️ Configuring sudo Access

Always edit using:
```bash
sudo visudo
```

### Grant Full sudo
```text
user1 ALL=(ALL) ALL
```

### Grant Limited sudo
```text
user1 ALL=(ALL) NOPASSWD: /bin/systemctl
```

### Group-based sudo
```text
%devops ALL=(ALL) ALL
```

---

## 🧪 sudo Command Syntax and Examples

Syntax:
```bash
sudo [options] command
```

Examples:
```bash
sudo yum install nginx
sudo -i          # root shell
sudo -u user2 ls /home/user2
```

Check sudo rights:
```bash
sudo -l
```

---

## 🧪 Hands-on Labs

### Lab 1: Link Count Practice
1. Create file `a.txt`
2. Create two hard links
3. Check link count
4. Delete one name and verify data remains

---

### Lab 2: Hard vs Soft Links
1. Create original file
2. Create hard and soft link
3. Delete original
4. Test access from both links

---

### Lab 3: sudo Practice
1. Create user `ops1`
2. Grant sudo for `systemctl` only
3. Restart nginx using sudo

---

## 🎯 Interview Practice Questions

### Conceptual
1. What is link count?
2. Why directory link count starts from 2?
3. Hard link vs soft link differences?
4. Why sudo is preferred over su?

### Scenario-Based
1. Disk space not freed after deleting file – why?
2. Symbolic link broken – how to fix?
3. Grant user permission to restart only one service.

---

## 📌 Quick Revision Cheat Sheet

| Task | Command |
|-----|--------|
| Check link count | `ls -l file` |
| Create hard link | `ln file link` |
| Create soft link | `ln -s file link` |
| Check inode | `ls -li file` |
| Run with sudo | `sudo command` |
| Edit sudoers | `visudo` |

---

## 🚀 Suggested Next Topics

- umask and default permissions
- ACL & extended attributes
- Advanced sudo security
- Audit logs & command tracking

---

## 🤝 Contributing

Add:
- More labs
- Troubleshooting cases
- Advanced sudo rules

---

## 📄 License

MIT License

