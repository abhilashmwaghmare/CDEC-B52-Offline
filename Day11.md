# 🔐 File Permissions in Linux 

## 1️⃣ Introduction to File Permissions

In Linux, **every file and folder has permissions**.

Permissions decide:
- Who can read the file
- Who can modify the file
- Who can run the file

Think like this:

| Real Life | Linux |
|----------|-------|
| House | Directory |
| Door lock | File permission |
| Owner | File owner |

---

## 2️⃣ Why File Permissions are Important

File permissions protect the system from:

- Accidental deletion
- Unauthorized access
- Security attacks

Example:
- Only root can edit `/etc/passwd`
- Normal users cannot delete system files

---

## 3️⃣ Understanding Read, Write, Execute (rwx)

There are **three basic permissions**:

| Permission | Symbol | Meaning (File) | Meaning (Directory) |
|-----------|-------|---------------|--------------------|
| Read | r | Read file content | List files |
| Write | w | Modify file | Create/Delete files |
| Execute | x | Run the file | Enter directory |

Example:
```bash
cat file.txt   # needs read
nano file.txt  # needs write
./script.sh    # needs execute
```

---

## 4️⃣ Viewing Permissions with ls -l

Command:
```bash
ls -l
```

Example output:
```
-rwxr-xr-- 1 john devops 1024 file.sh
```

This line contains:
- File type
- Permissions
- Owner
- Group

---

## 5️⃣ Breaking Down a Permission String

Example:
```
-rwxr-xr--
```

Break it into parts:

| Part | Meaning |
|------|--------|
| - | Regular file |
| rwx | Owner permissions |
| r-x | Group permissions |
| r-- | Others permissions |

So:
- Owner: read, write, execute
- Group: read, execute
- Others: read only

---

## 6️⃣ Types of Ownership

Every file has:

1. Owner (user who created it)  
2. Group (group of the owner)  
3. Others (everyone else)  

Check ownership:
```bash
ls -l file.txt
```

---

## 7️⃣ File Types in Linux

First character shows file type:

| Symbol | Type |
|------|------|
| - | Regular file |
| d | Directory |
| l | Link |
| c | Character device |
| b | Block device |

Example:
```bash
ls -ld /etc
# drwxr-xr-x
```

---

## 8️⃣ Changing Permissions with chmod

### 🔹 Symbolic Method

Add execute to owner:
```bash
chmod u+x script.sh
```

Remove write from group:
```bash
chmod g-w file.txt
```

Give read to others:
```bash
chmod o+r file.txt
```

---

### 🔹 Numeric Method

Permission values:

| Permission | Value |
|-----------|------|
| r | 4 |
| w | 2 |
| x | 1 |

Examples:

| Number | Meaning |
|-------|--------|
| 7 | rwx |
| 6 | rw- |
| 5 | r-x |
| 4 | r-- |

Set permission 755:
```bash
chmod 755 script.sh
```

Meaning:
- Owner = 7 (rwx)
- Group = 5 (r-x)
- Others = 5 (r-x)

---

## 9️⃣ Changing Ownership with chown

Change owner:
```bash
sudo chown john file.txt
```

Change owner and group:
```bash
sudo chown john:devops file.txt
```

---

## 🔟 Changing Group with chgrp

Change only group:
```bash
sudo chgrp qa file.txt
```

---

## 1️⃣1️⃣ Special Permissions

### 🔸 SUID (Set User ID)

Runs program as file owner.

Example:
```bash
ls -l /usr/bin/passwd
# -rwsr-xr-x
```

### 🔸 SGID (Set Group ID)

Files inherit group of directory.

Example:
```bash
chmod g+s shared_dir
```

### 🔸 Sticky Bit

Only file owner can delete files in directory.

Example:
```bash
ls -ld /tmp
# drwxrwxrwt
```

---

## 1️⃣2️⃣ Real-Time Use Cases

1. Make script executable:
```bash
chmod +x deploy.sh
```

2. Protect a file from others:
```bash
chmod 600 secret.txt
```

3. Share directory with group:
```bash
chmod 770 shared_dir
```

---

## 🧪 1️⃣3️⃣ Hands-on Labs

### Lab 1: Basic Permissions
1. Create file test.txt
2. Check permission
3. Remove write from others

### Lab 2: Directory Permissions
1. Create folder `project`
2. Allow only owner to access

### Lab 3: Ownership
1. Change owner of file
2. Change group of file

---

## ⚠️ 1️⃣4️⃣ Common Mistakes

- Giving 777 to everything
- Forgetting execute on scripts
- Using chown without sudo
- Breaking permissions of system files

---

## 📝 1️⃣5️⃣ Practice Questions

### Basic
1. What does `rwx` mean?
2. Difference between file and directory permissions?
3. What is chmod?

### Hands-on
1. Set permission 644 on a file.
2. Make a script executable.
3. Change owner of file to root.

---

## 🎯 1️⃣6️⃣ Interview & Scenario Questions

1. A script is not running. What will you check?
2. What does permission 777 mean?
3. How do you give only read access to others?
4. What is sticky bit and where is it used?

---

## 📌 1️⃣7️⃣ Quick Revision Summary

| Task | Command |
|-----|--------|
| View permissions | ls -l |
| Change permissions | chmod |
| Change owner | chown |
| Change group | chgrp |
| Check file type | ls -l |

---

✅ This guide is designed for:
- Students
- Beginners
- Classroom teaching
- Self-learning
- Interview preparation

---

Next recommended topic:

👉 🔍 Search & Filter (grep, find) or 📦 Archiving & Compression

