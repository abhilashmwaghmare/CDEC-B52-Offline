# 🔐 Linux Password & Group Management

![Linux](https://img.shields.io/badge/Linux-Admin-blue)
![DevOps](https://img.shields.io/badge/DevOps-Ready-green)
![Interview](https://img.shields.io/badge/Interview-Preparation-orange)

> A complete, production-oriented guide to **Linux Password and Group Management** with commands, real-world use cases, labs, and interview questions.

---

## 📌 Table of Contents

1. [Overview](#overview)
2. [Importance of Password Security](#importance-of-password-security)
3. [Using `passwd` Command](#using-passwd-command)
4. [Password Policy Settings](#password-policy-settings)
5. [Account Locking and Expiration](#account-locking-and-expiration)
6. [Understanding `/etc/shadow`](#understanding-etcshadow)
7. [Using `chage` Command](#using-chage-command)
8. [Introduction to Linux Groups](#introduction-to-linux-groups)
9. [`/etc/group` and `/etc/gshadow`](#etcgroup-and-etcgshadow)
10. [Types of Groups](#types-of-groups)
11. [Creating and Deleting Groups](#creating-and-deleting-groups)
12. [Modifying Groups](#modifying-groups)
13. [Managing Group Memberships](#managing-group-memberships)
14. [Viewing and Editing Group Information](#viewing-and-editing-group-information)
15. [Hands-on Labs](#hands-on-labs)
16. [Interview Practice Questions](#interview-practice-questions)
17. [Quick Revision Cheat Sheet](#quick-revision-cheat-sheet)
18. [Next Topics](#next-topics)

---

## 🧭 Overview

This repository covers:
- Password security and policies
- Account locking & expiry
- Linux groups and permissions
- Production use cases
- Interview and scenario-based questions

Target roles:
- Linux Administrator
- DevOps Engineer
- SRE

---

## 🔐 Importance of Password Security

### Why it matters
- Prevents unauthorized access
- Protects sensitive production data
- Mandatory for compliance (ISO, SOC2, PCI-DSS)

### Real-world Use Case
- Brute-force SSH attacks exploiting weak passwords
- Immediate account lockdown after suspicious activity

### Best Practices
- Min length: 8–12 characters
- Enable aging and expiry
- Lock inactive users

---

## 🛠 Using `passwd` Command

### Change Own Password
```bash
passwd
```

### Change Another User Password
```bash
sudo passwd user1
```

### Lock & Unlock Account
```bash
sudo passwd -l user1   # Lock
sudo passwd -u user1   # Unlock
```

### Delete Password (Not Recommended)
```bash
sudo passwd -d user1
```

**Use Case:** Disable access for resigned employee immediately.

---

## 🧩 Password Policy Settings

Configuration files:
- `/etc/security/pwquality.conf`
- `/etc/pam.d/system-auth`

### Example Policy
```conf
minlen = 10
minclass = 3
retry = 3
```

### Enforce via PAM
```bash
password requisite pam_pwquality.so retry=3 minlen=10
```

**Use Case:** Enforcing strong passwords across enterprise servers.

---

## 🔒 Account Locking and Expiration

### Lock / Unlock User
```bash
sudo usermod -L user1
sudo usermod -U user1
```

### Set Account Expiry
```bash
sudo chage -E 2026-12-31 user1
```

**Use Case:** Auto-expire contractor accounts after project end.

---

## 📂 Understanding `/etc/shadow`

Example entry:
```text
user1:$6$abc123$hash:19600:0:90:7:14:180:
```

| Field | Description |
|------|------------|
| 1 | Username |
| 2 | Encrypted password |
| 3 | Last change (days since 1970) |
| 4 | Min days |
| 5 | Max days |
| 6 | Warning days |
| 7 | Inactive days |
| 8 | Expiry date |

---

## ⏳ Using `chage` Command

### View Policy
```bash
chage -l user1
```

### Set Expiry Rules
```bash
sudo chage -M 90 -m 7 -W 14 user1
```

---

## 👥 Introduction to Linux Groups

Why groups are important:
- Role-based access control
- Easier permission management
- Shared directory access

Example:
- `developers` → access to `/var/www`

---

## 📄 `/etc/group` and `/etc/gshadow`

### /etc/group Format
```text
developers:x:1001:user1,user2
```

| Field | Meaning |
|------|--------|
| 1 | Group name |
| 2 | Password placeholder |
| 3 | GID |
| 4 | Members |

`/etc/gshadow` stores encrypted group passwords and admins.

---

## 🧱 Types of Groups

| Type | Description |
|-----|-------------|
| Primary | Default group of user |
| Secondary | Additional access |
| System | For services (nginx, docker) |

---

## ➕ Creating and Deleting Groups

```bash
sudo groupadd devops
sudo groupadd -g 2001 qa
sudo groupdel qa
```

---

## ✏️ Modifying Groups

```bash
sudo groupmod -n engineers devops
sudo groupmod -g 3001 engineers
```

---

## 🔗 Managing Group Memberships

### Add User
```bash
sudo usermod -aG docker user1
```

### Remove User
```bash
gpasswd -d user1 docker
```

### View Groups
```bash
groups user1
id user1
```

---

## 👀 Viewing and Editing Group Information

```bash
getent group
getent group docker
sudo vigr
```

---

## 🧪 Hands-on Labs

### Lab 1: Secure User Setup
1. Create user `intern1`
2. Set max password age 60 days
3. Expire account after 3 months

### Lab 2: Group Access Control
1. Create group `appteam`
2. Add two users
3. Create `/opt/app`
4. Give group write access

---

## 🎯 Interview Practice Questions

### Conceptual
1. Difference between `/etc/passwd` and `/etc/shadow`?
2. What does `!` mean in shadow file?
3. Primary vs Secondary group?

### Scenario-Based
1. User cannot login – how to check if account is locked?
2. Enforce 45-day password expiry for all users.
3. Remove user from `sudo` and `docker` safely.

---

## 📌 Quick Revision Cheat Sheet

| Task | Command |
|-----|--------|
| Change password | `passwd user1` |
| Lock user | `usermod -L user1` |
| Set expiry | `chage -E 2026-12-31 user1` |
| Create group | `groupadd devops` |
| Add to group | `usermod -aG docker user1` |
| View groups | `groups user1` |

---

## 🚀 Next Topics

- sudoers & privilege escalation
- PAM authentication flow
- LDAP / FreeIPA integration
- Audit with `faillog` and `lastlog`

---

## 🤝 Contributing

Feel free to:
- Add more labs
- Add MCQs
- Improve troubleshooting scenarios

---

## 📄 License

MIT License

