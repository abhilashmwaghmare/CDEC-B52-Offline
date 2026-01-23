[01_users_and_groups_readme.md](https://github.com/user-attachments/files/24819111/01_users_and_groups_readme.md)
# 👤 Users & Groups in Linux 

## 1️⃣ Introduction to Users in Linux

In Linux, **every person who logs in is a user**.

Think of Linux like a hostel:
- Each student = one user  
- Each room = user home directory  
- Warden = root user  

Linux does not allow anonymous work. **Every action is done by some user.**

---

## 2️⃣ Why User Management is Important

User management helps to:

- Control who can log in
- Protect important files
- Give limited access to users
- Track who did what

Example:
- Developer can access code folder
- Tester cannot access production folder

---

## 3️⃣ Types of Users

There are **three main types of users**:

### 1. Root User
- Super admin of Linux
- UID = 0
- Full control over system

Example:
```bash
whoami
# output: root
```

### 2. System Users
- Created for system services
- Example: sshd, apache, mysql
- Usually UID < 1000

### 3. Normal Users
- Real human users
- UID >= 1000
- Limited permissions

Check your UID:
```bash
id
```

---

## 4️⃣ Understanding UID and GID

- UID = User ID  
- GID = Group ID  

Example:
```bash
id abhilash
# uid=1001(abhilash) gid=1001(abhilash)
```

This means:
- User name = abhilash
- User ID = 1001
- Primary group ID = 1001

---

## 5️⃣ Important User Files

### 📄 /etc/passwd
Stores basic user information.

Format:
```
username:x:UID:GID:comment:home:shell
```

Example:
```bash
cat /etc/passwd | head -3
```

### 📄 /etc/shadow
Stores **encrypted passwords**.

Only root can read it.

Example:
```bash
sudo cat /etc/shadow
```

### 📄 /etc/group
Stores group information.

Format:
```
groupname:x:GID:members
```

Example:
```bash
cat /etc/group | head -3
```

---

## 6️⃣ Creating Users with useradd

Create a new user:
```bash
sudo useradd john
```

Create user with home directory:
```bash
sudo useradd -m john
```

Check user created:
```bash
id john
```

---

## 7️⃣ Setting and Changing Passwords

Set password for user:
```bash
sudo passwd john
```

User changes own password:
```bash
passwd
```

Lock a user account:
```bash
sudo passwd -l john
```

Unlock a user account:
```bash
sudo passwd -u john
```

---

## 8️⃣ User Home Directories

Every user has a home directory:

Example:
- root → /root  
- john → /home/john  

Check:
```bash
ls /home
```

Files inside home belong to that user.

---

## 9️⃣ Managing User Groups

A **group** is a collection of users.

Why groups?
- Share files
- Give common permissions

Create a group:
```bash
sudo groupadd devops
```

Check group:
```bash
grep devops /etc/group
```

---

## 🔟 Adding and Removing Users from Groups

Add user to group:
```bash
sudo usermod -aG devops john
```

Check groups of user:
```bash
groups john
```

Remove user from group:
```bash
sudo gpasswd -d john devops
```

---

## 1️⃣1️⃣ Removing Users

Delete user only:
```bash
sudo userdel john
```

Delete user with home directory:
```bash
sudo userdel -r john
```

---

## 1️⃣2️⃣ Switching Between Users

Switch to another user:
```bash
su - john
```

Go back:
```bash
exit
```

---

## 1️⃣3️⃣ Using su Command

Become root:
```bash
su -
```

This needs root password.

---

## 1️⃣4️⃣ Using sudo Command

Run command as root:
```bash
sudo apt update
```

Check sudo access:
```bash
sudo -l
```

Why sudo is better than root login?
- Safer
- Logged actions
- Limited access

---

## 🧪 15️⃣ Hands-on Labs

### Lab 1: Create a User
1. Create user `student1`
2. Set password
3. Check UID

### Lab 2: Group Practice
1. Create group `training`
2. Add student1 to training
3. Verify group membership

### Lab 3: Switch User
1. Login as student1
2. Create a file in home directory

---

## ⚠️ 16️⃣ Common Mistakes

- Forgetting `-a` while adding group (removes old groups)
- Deleting user without backup
- Giving sudo to everyone
- Editing system files manually

---

## 📝 17️⃣ Practice Questions

### Basic
1. What is a user?
2. What is UID?
3. Difference between root and normal user?

### Hands-on
1. Create a user `test1` with home directory.
2. Add test1 to group `qa`.
3. Lock the user account.

---

## 🎯 18️⃣ Interview & Scenario Questions

1. A user cannot login. How will you check?
2. How do you give sudo access to a user?
3. Difference between `su` and `sudo`?
4. Where are passwords stored in Linux?

---

## 📌 19️⃣ Quick Revision Summary

| Topic | Command |
|------|--------|
| Create user | useradd |
| Delete user | userdel |
| Set password | passwd |
| Create group | groupadd |
| Add to group | usermod -aG |
| Switch user | su |
| Run as root | sudo |

---

