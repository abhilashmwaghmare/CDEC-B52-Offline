[vim_editor_complete_execute_visual_mode_guide.md](https://github.com/user-attachments/files/24792061/vim_editor_complete_execute_visual_mode_guide.md)
# 📝 Vim Editor – Execute Mode, Visual Mode & Complete Revision Guide

![Vim](https://img.shields.io/badge/Vim-Editor-green)
![Linux](https://img.shields.io/badge/Linux-CLI-blue)
![Interview](https://img.shields.io/badge/Interview-Preparation-orange)

> A production-focused, interview-ready guide to **Vim Editor** covering Execute Mode, Visual Mode, file operations, searching, line numbering, and full revision with real-time use cases and practice labs.

---

## 📌 Table of Contents

1. [Overview](#overview)
2. [Entering Execute Mode](#entering-execute-mode)
3. [Executing Basic Commands](#executing-basic-commands)
   - File Operations
   - Searching
   - Line Numbering
4. [Entering Visual Mode](#entering-visual-mode)
5. [Manipulating Text in Visual Mode](#manipulating-text-in-visual-mode)
6. [Complete Vim Revision](#complete-vim-revision)
7. [Hands-on Practice Labs](#hands-on-practice-labs)
8. [Interview Practice Questions](#interview-practice-questions)
9. [Quick Revision Cheat Sheet](#quick-revision-cheat-sheet)

---

## 🧭 Overview

This guide is designed for:
- Linux Administrators
- DevOps Engineers
- SREs
- Interview preparation

You will learn:
- Command (Execute) Mode usage
- Visual Mode text manipulation
- Real-time production use cases
- High-frequency interview commands

---

## ⌨️ Entering Execute Mode

Vim works mainly in **Normal (Execute) Mode**.

### How to Enter Execute Mode
- Press `Esc` from any mode

### Why Execute Mode is Important
- Navigate files
- Run commands
- Perform fast edits without mouse

### Real-time Use Case
Editing configuration files on remote production servers via SSH.

---

## 🛠 Executing Basic Commands

### 1. File Operations

| Task | Command |
|-----|--------|
| Open file | `vim file.txt` |
| Save file | `:w` |
| Quit | `:q` |
| Save & Quit | `:wq` |
| Quit without saving | `:q!` |

**Use Case:** Editing `/etc/ssh/sshd_config` safely.

---

### 2. Searching

| Task | Command |
|-----|--------|
| Search forward | `/pattern` |
| Search backward | `?pattern` |
| Next match | `n` |
| Previous match | `N` |

Example:
```vim
/error
```

**Use Case:** Finding misconfigured directives in large config files.

---

### 3. Line Numbering

```vim
:set number
:set nonumber
```

Jump to line:
```vim
:25
```

**Use Case:** Debugging stack traces referring to exact line numbers.

---

## 🖱 Entering Visual Mode

Visual mode is used to **select text**.

| Mode | Key |
|------|----|
| Character-wise | `v` |
| Line-wise | `V` |
| Block-wise | `Ctrl + v` |

**Use Case:** Selecting multiple lines for bulk edits.

---

## ✂️ Manipulating Text in Visual Mode

### Common Operations

| Task | Command |
|-----|--------|
| Delete | `d` |
| Copy (yank) | `y` |
| Paste | `p` |
| Indent right | `>` |
| Indent left | `<` |

### Example Workflow
1. Press `V` (line visual mode)
2. Select 5 lines
3. Press `>` to indent all

**Use Case:** Reformatting YAML or Python indentation.

---

## 🔄 Complete Vim Revision

### Modes Summary

| Mode | Purpose |
|-----|--------|
| Normal | Execute commands |
| Insert | Type text |
| Visual | Select text |
| Command-line | Run `:` commands |

---

### Navigation

| Action | Command |
|------|--------|
| Beginning of file | `gg` |
| End of file | `G` |
| Next word | `w` |
| Previous word | `b` |
| Beginning of line | `0` |
| End of line | `$` |

---

### Editing Shortcuts

| Task | Command |
|-----|--------|
| Delete line | `dd` |
| Copy line | `yy` |
| Replace char | `r` |
| Undo | `u` |
| Redo | `Ctrl+r` |

---

### Search & Replace

```vim
:%s/old/new/g
```

**Use Case:** Bulk replacing environment variables in config files.

---

### Multiple Files

```vim
:vs file2.txt
:sp file3.txt
Ctrl+w w
```

---

## 🧪 Hands-on Practice Labs

### Lab 1: Basic File Editing
1. Open `test.txt`
2. Enable line numbers
3. Go to line 20
4. Delete that line
5. Save and quit

---

### Lab 2: Visual Mode Practice
1. Select 10 lines using `V`
2. Indent them right
3. Copy and paste below

---

## 🎯 Interview Practice Questions

### Conceptual
1. Difference between Normal and Insert mode?
2. When to use Visual Block mode?
3. How to recover a file after crash?

### Commands Round
1. Jump to last line
2. Replace all `foo` with `bar`
3. Delete lines 10 to 20

---

## 📌 Quick Revision Cheat Sheet

| Task | Command |
|-----|--------|
| Enter normal mode | `Esc` |
| Insert mode | `i` |
| Visual mode | `v` / `V` / `Ctrl+v` |
| Save & quit | `:wq` |
| Search | `/pattern` |
| Replace | `:%s/a/b/g` |
| Line numbers | `:set number` |

---


