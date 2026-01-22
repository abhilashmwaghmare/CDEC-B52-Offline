# 🔐 Linux File Permissions & File Types – Complete Guide

![Linux](https://img.shields.io/badge/Linux-Admin-blue)
![DevOps](https://img.shields.io/badge/DevOps-Ready-green)
![Interview](https://img.shields.io/badge/Interview-Preparation-orange)

> A production-ready, interview-focused guide to **Linux File Permissions and File Types** covering rwx permissions, `ls -l` output, permission strings, and system/user defined file types with real-time use cases and practice labs.

---

## 📌 Table of Contents

1. [Importance of File Permissions in Linux](#importance-of-file-permissions-in-linux)
2. [Explanation of rwx Permissions](#explanation-of-rwx-permissions)
3. [How Permissions are Displayed with `ls -l`](#how-permissions-are-displayed-with-ls--l)
4. [Breaking Down a Permission String](#breaking-down-a-permission-string)
5. [Introduction to File Types](#introduction-to-file-types)
6. [User Defined File Types](#user-defined-file-types)
7. [System Defined File Types](#system-defined-file-types)
8. [Hands-on Labs](#hands-on-labs)
9. [Interview Practice Questions](#interview-practice-questions)
10. [Quick Revision Cheat Sheet](#quick-revision-cheat-sheet)

---

## 🧭 Importance of File Permissions in Linux

Linux is a **multi-user OS**, so file permissions control:
- Who can read, write, or execute a file
- Protection of system and user data
- Prevention of accidental or malicious changes

### Real-time Use Case
- Preventing developers from modifying `/etc/passwd`
- Allowing only application users to modify app config files

Without proper permissions:
- Data leaks
- Privilege escalation
- Accidental deletion of critical files

---

## 🧩 Explanation of rwx Permissions

Each file has three permission sets:

| Entity | Meaning |
|------|--------|
| User (u) | Owner of the file |
| Group (g) | Group owner |
| Others (o) | Everyone else |

Each set has:

| Symbol | Meaning |
|------|--------|
| r | Read (4) |
| w | Write (2) |
| x | Execute (1) |

### Numeric Values

| Permission | Value |
|-----------|------|
| r | 4 |
| w | 2 |
| x | 1 |

Example:
- `rwx` = 4+2+1 = **7**
- `r-x` = 4+0+1 = **5**
- `r--` = 4+0+0 = **4**

---

## 📂 How Permissions are Displayed with `ls -l`

Example:
```bash
ls -l file.txt
-rwxr-xr-- 1 user1 developers 1024 Jan 20 10:00 file.txt
```

Fields:
1. File type & permissions
2. Link count
3. Owner
4. Group
5. Size
6. Date
7. File name

---

## 🔍 Breaking Down a Permission String

Example:
```text
-rwxr-xr--
```

| Position | Meaning |
|---------|--------|
| 1 | File type (`-` = regular file) |
| 2-4 | Owner permissions (`rwx`) |
| 5-7 | Group permissions (`r-x`) |
| 8-10 | Others permissions (`r--`) |

### Interpretation
- Owner: read, write, execute
- Group: read, execute
- Others: read only

Numeric form:
```text
754
```

---

## 🗂 Introduction to File Types

The first character in permission string shows **file type**.

| Symbol | File Type |
|------|----------|
| `-` | Regular file |
| `d` | Directory |
| `l` | Symbolic link |
| `c` | Character device |
| `b` | Block device |
| `s` | Socket |
| `p` | Named pipe |

Example:
```bash
drwxr-xr-x 2 root root 4096 Jan 20 bin
```

---

## 👤 User Defined File Types

User-defined (common in daily work):

| Type | Example |
|-----|--------|
| Regular file | `.txt`, `.log`, `.conf` |
| Directory | `myfolder/` |
| Symbolic link | `ln -s file link` |
| Executable script | `.sh`, `.py` |

### Use Case
- Creating executable deployment scripts
- Linking config files across directories

---

## ⚙️ System Defined File Types

System and special files:

| Type | Description |
|-----|------------|
| Block device | Disks (`/dev/sda`) |
| Char device | Terminals (`/dev/tty`) |
| Socket | IPC communication |
| Pipe | Inter-process communication |

View in `/dev`:
```bash
ls -l /dev
```

---

## 🧪 Hands-on Labs

### Lab 1: Permission Analysis
1. Create file `test.txt`
2. Run `ls -l`
3. Change permission to `754`
4. Verify using `ls -l`

```bash
touch test.txt
chmod 754 test.txt
ls -l test.txt
```

---

### Lab 2: File Type Identification
1. List files with `ls -l`
2. Identify all directories
3. Identify symbolic links

---

## 🎯 Interview Practice Questions

### Conceptual
1. Why are file permissions critical in Linux?
2. Difference between `rwxr-xr--` and `rwx------`?
3. What does the first character in `ls -l` represent?

### Scenario-Based
1. User cannot execute a script – how to fix?
2. Secure a file so only owner can read/write.
3. Identify all device files in `/dev`.

### Commands Round
- Set permission to 640
- Find all executable files in a directory

---

## 📌 Quick Revision Cheat Sheet

| Task | Command |
|-----|--------|
| View permissions | `ls -l` |
| Change permission | `chmod 754 file` |
| Symbolic form | `chmod u+rwx,g+rx,o+r file` |
| Find executables | `find . -type f -perm -111` |

---

## 🚀 Suggested Next Topics

- chmod numeric vs symbolic
- Special permissions (SUID, SGID, Sticky bit)
- ACLs (setfacl, getfacl)
- umask and defaults

---

## 🤝 Contributing

Add:
- More labs
- Troubleshooting cases
- Advanced permission scenarios

---

## 📄 License

MIT License
