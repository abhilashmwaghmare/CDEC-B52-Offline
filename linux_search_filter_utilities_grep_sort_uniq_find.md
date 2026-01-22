# 🔍 Linux Search & Filter Utilities – grep, sort, uniq, find

![Linux](https://img.shields.io/badge/Linux-Admin-blue)
![Tools](https://img.shields.io/badge/Tools-grep|find|sort-green)
![Interview](https://img.shields.io/badge/Interview-Preparation-orange)

> A production-ready, interview-focused guide to **Searching and Filtering Data in Linux** using `grep`, `cat`, `sort`, `uniq`, and `find` with real-time use cases, commands, labs, and interview questions.

---

## 📌 Table of Contents

1. [Introduction to Search and Filter Utilities](#introduction-to-search-and-filter-utilities)
2. [Why Searching and Filtering Matters](#why-searching-and-filtering-matters)
3. [Overview of Key Utilities](#overview-of-key-utilities)
4. [Reading and Filtering Files](#reading-and-filtering-files)
5. [Introduction to the find Utility](#introduction-to-the-find-utility)
6. [Basic Syntax of find](#basic-syntax-of-find)
7. [Advanced find Usage and Filters](#advanced-find-usage-and-filters)
8. [Practical find Examples](#practical-find-examples)
9. [Hands-on Labs](#hands-on-labs)
10. [Interview Practice Questions](#interview-practice-questions)
11. [Quick Revision Cheat Sheet](#quick-revision-cheat-sheet)

---

## 🔎 Introduction to Search and Filter Utilities

In Linux, search and filter utilities help administrators and DevOps engineers:
- Analyze log files
- Troubleshoot issues
- Process large datasets
- Automate reporting

Core tools:
- `cat` – display file content
- `grep` – search patterns
- `sort` – order data
- `uniq` – remove duplicates
- `find` – search files in filesystem

---

## 🎯 Why Searching and Filtering Matters

### Real-time Use Cases

| Scenario | Tool |
|--------|------|
| Find errors in logs | `grep` |
| Remove duplicate entries | `uniq` |
| Sort large reports | `sort` |
| Find old large files | `find` |
| Pipeline processing | `cat | grep | sort | uniq` |

---

## 🛠 Overview of Key Utilities

| Utility | Purpose | Example |
|-------|--------|--------|
| cat | Display file | `cat file.txt` |
| grep | Pattern search | `grep error app.log` |
| sort | Sort lines | `sort data.txt` |
| uniq | Remove duplicates | `uniq data.txt` |
| find | Search files | `find /var -name "*.log"` |

---

## 📄 Reading and Filtering Files

### Using cat

```bash
cat file.txt
cat -n file.txt      # with line numbers
```

### Using sort

```bash
sort names.txt
sort -n numbers.txt
sort -r names.txt   # reverse
```

### Using uniq

Note: `uniq` works on **sorted input**.

```bash
sort data.txt | uniq
sort data.txt | uniq -c    # count duplicates
sort data.txt | uniq -d   # only duplicates
```

### Combined Pipeline Example

```bash
cat access.log | grep 404 | sort | uniq -c | sort -nr
```

> Find most frequent 404 errors in web logs.

---

## 🔍 Introduction to the find Utility

`find` searches files and directories based on:
- Name
- Type
- Size
- Time
- Owner
- Permissions

Search starts from a given path and walks the directory tree.

---

## 🧩 Basic Syntax of find

```bash
find [path] [options] [expression]
```

Example:
```bash
find /home -name "file.txt"
```

Common options:
- `-name` – filename
- `-type` – file type
- `-size` – file size
- `-mtime` – modified time

---

## ⚙️ Advanced find Usage and Filters

### Find by Type

```bash
find /var -type f     # files
find /var -type d     # directories
```

### Find by Size

```bash
find / -size +100M
find / -size -10k
```

### Find by Modification Date

```bash
find /var/log -mtime -7   # last 7 days
find /var/log -mtime +30  # older than 30 days
```

### Find and Execute Command

```bash
find /tmp -type f -name "*.tmp" -delete
```

or

```bash
find /var/log -type f -exec rm -f {} \;
```

---

## 📁 Practical find Examples

### 1. Find all .log files

```bash
find /var -name "*.log"
```

### 2. Find large files over 1GB

```bash
find / -size +1G
```

### 3. Find empty files

```bash
find /home -type f -empty
```

### 4. Find files owned by user

```bash
find /home -user devops
```

### 5. Find and archive old files

```bash
find /var/log -mtime +30 -type f -print
```

---

## 🧪 Hands-on Labs

### Lab 1: Log Analysis
1. Use `grep` to find "error" in log file
2. Count unique error lines
3. Sort by frequency

```bash
grep error app.log | sort | uniq -c | sort -nr
```

---

### Lab 2: Duplicate Removal

```bash
sort users.txt | uniq > clean_users.txt
```

---

### Lab 3: Cleanup Old Files

```bash
find /tmp -type f -mtime +7 -delete
```

---

## 🎯 Interview Practice Questions

### Conceptual
1. Difference between `grep` and `find`?
2. Why must input be sorted before using `uniq`?
3. How does `find` differ from `locate`?

### Scenario-Based
1. Find top 10 IPs causing 404 errors.
2. Delete all files larger than 500MB older than 60 days.
3. Find and compress all `.log` files older than 30 days.

---

## 📌 Quick Revision Cheat Sheet

| Task | Command |
|-----|--------|
| Display file | `cat file` |
| Search pattern | `grep pattern file` |
| Sort file | `sort file` |
| Remove duplicates | `sort file | uniq` |
| Find by name | `find / -name "file"` |
| Find by size | `find / -size +100M` |
| Find by date | `find / -mtime +7` |
| Find & delete | `find /tmp -type f -delete` |

---

## 🚀 Suggested Next Topics

- awk and sed deep dive
- locate and updatedb
- xargs and parallel processing
- Advanced log analysis pipelines

---

## 🤝 Contributing

Add:
- More pipelines
- Performance tips
- Troubleshooting scenarios

---

## 📄 License

MIT License

