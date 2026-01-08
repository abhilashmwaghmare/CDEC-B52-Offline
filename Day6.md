# 📚 Day 6
## Linux File System Hierarchy & Shortcuts

---

## 1. Mastering the Linux File System Hierarchy

### Understanding the Linux File System

Linux organizes files in a hierarchical tree structure, starting from the root directory (`/`).

### File System Tree Structure

```
┌─────────────────────────────────────────────────────────┐
│              LINUX FILE SYSTEM HIERARCHY                 │
└─────────────────────────────────────────────────────────┘

                        /
                        │
        ┌───────────────┼───────────────┐
        │               │               │
        ▼               ▼               ▼
      /bin            /etc            /home
        │               │               │
        ▼               ▼               ▼
   executables      config files    user dirs
```

### Complete File System Overview

```mermaid
graph TD
    A[/ Root] --> B[/bin<br/>Essential binaries]
    A --> C[/boot<br/>Boot files]
    A --> D[/dev<br/>Device files]
    A --> E[/etc<br/>Configuration]
    A --> F[/home<br/>User directories]
    A --> G[/lib<br/>Libraries]
    A --> H[/usr<br/>User programs]
    A --> I[/var<br/>Variable data]
    A --> J[/tmp<br/>Temporary files]
    A --> K[/proc<br/>Process info]
    A --> L[/sbin<br/>System binaries]
    
    style A fill:#667eea,stroke:#333,stroke-width:3px,color:#fff
    style B fill:#764ba2,stroke:#333,stroke-width:2px,color:#fff
    style C fill:#f093fb,stroke:#333,stroke-width:2px,color:#fff
    style D fill:#4facfe,stroke:#333,stroke-width:2px,color:#fff
    style E fill:#43e97b,stroke:#333,stroke-width:2px,color:#fff
    style F fill:#fa709a,stroke:#333,stroke-width:2px,color:#fff
    style H fill:#fee140,stroke:#333,stroke-width:2px,color:#000
    style I fill:#30cfd0,stroke:#333,stroke-width:2px,color:#fff
```

---

## 2. The Significance of the Linux File System Hierarchy

### Why This Structure Matters

The Linux file system hierarchy (FSH) is standardized and provides:

- **Organization:** Logical grouping of files
- **Consistency:** Same structure across Linux distributions
- **Efficiency:** Easy to locate files
- **Security:** Proper permissions and separation
- **Standards:** Follows FHS (Filesystem Hierarchy Standard)

### Benefits of Standard Hierarchy

```
┌─────────────────────────────────────────────────────────┐
│          BENEFITS OF FILE SYSTEM HIERARCHY               │
└─────────────────────────────────────────────────────────┘

✅ Organization
   • Logical file grouping
   • Easy navigation

✅ Consistency
   • Same structure everywhere
   • Predictable locations

✅ Security
   • Proper permissions
   • Separation of concerns

✅ Efficiency
   • Quick file location
   • Standard paths
```

---

## 3. Inside the Linux Root Directory: What You Need to Know

### Root Directory Contents

Let's explore what's inside the root directory (`/`):

#### View Root Directory
```bash
ls -l /
```

**Text Output:**
```
total 72
drwxr-xr-x   2 root root  4096 Jan 15 10:00 bin
drwxr-xr-x   3 root root  4096 Jan 15 10:00 boot
drwxr-xr-x  15 root root  3060 Jan 15 10:00 dev
drwxr-xr-x 120 root root 12288 Jan 15 10:00 etc
drwxr-xr-x   3 root root  4096 Jan 15 10:00 home
drwxr-xr-x  15 root root  4096 Jan 15 10:00 lib
drwxr-xr-x   2 root root  4096 Jan 15 10:00 media
drwxr-xr-x   2 root root  4096 Jan 15 10:00 mnt
drwxr-xr-x   2 root root  4096 Jan 15 10:00 opt
dr-xr-xr-x 247 root root     0 Jan 15 10:00 proc
drwx------   2 root root  4096 Jan 15 10:00 root
drwxr-xr-x  18 root root   480 Jan 15 10:00 run
drwxr-xr-x   2 root root 12288 Jan 15 10:00 sbin
drwxr-xr-x   2 root root  4096 Jan 15 10:00 srv
dr-xr-xr-x  13 root root     0 Jan 15 10:00 sys
drwxrwxrwt   8 root root  4096 Jan 15 10:00 tmp
drwxr-xr-x  11 root root  4096 Jan 15 10:00 usr
drwxr-xr-x  13 root root  4096 Jan 15 10:00 var
```

**Visual Root Directory Structure:**
```mermaid
graph TD
    A[/ Root Directory] --> B[📁 bin<br/>Essential binaries]
    A --> C[📁 boot<br/>Boot files]
    A --> D[📁 dev<br/>Device files]
    A --> E[📁 etc<br/>Configuration]
    A --> F[📁 home<br/>User directories]
    A --> G[📁 lib<br/>Libraries]
    A --> H[📁 usr<br/>User programs]
    A --> I[📁 var<br/>Variable data]
    A --> J[📁 tmp<br/>Temporary files]
    A --> K[📁 proc<br/>Process info]
    A --> L[📁 sbin<br/>System binaries]
    
    style A fill:#667eea,stroke:#333,stroke-width:4px,color:#fff
    style B fill:#764ba2,stroke:#333,stroke-width:2px,color:#fff
    style C fill:#f093fb,stroke:#333,stroke-width:2px,color:#fff
    style D fill:#4facfe,stroke:#333,stroke-width:2px,color:#fff
    style E fill:#43e97b,stroke:#333,stroke-width:2px,color:#fff
    style F fill:#fa709a,stroke:#333,stroke-width:2px,color:#fff
    style G fill:#fee140,stroke:#333,stroke-width:2px,color:#000
    style H fill:#30cfd0,stroke:#333,stroke-width:2px,color:#fff
    style I fill:#667eea,stroke:#333,stroke-width:2px,color:#fff
    style J fill:#764ba2,stroke:#333,stroke-width:2px,color:#fff
    style K fill:#f093fb,stroke:#333,stroke-width:2px,color:#fff
    style L fill:#4facfe,stroke:#333,stroke-width:2px,color:#fff
```

### Root Directory Breakdown

| Directory | Purpose | Example Contents |
|-----------|---------|------------------|
| `/` | Root of file system | All directories start here |
| `/bin` | Essential binaries | `ls`, `cp`, `mv`, `rm` |
| `/boot` | Boot files | Kernel, bootloader |
| `/dev` | Device files | `/dev/sda`, `/dev/tty` |
| `/etc` | Configuration | System config files |
| `/home` | User directories | `/home/abhilash` |
| `/lib` | Libraries | Shared libraries |
| `/media` | Removable media | USB, CD mounts |
| `/mnt` | Mount points | Temporary mounts |
| `/opt` | Optional software | Third-party apps |
| `/proc` | Process info | Virtual filesystem |
| `/root` | Root user home | Administrator home |
| `/run` | Runtime data | Process IDs, sockets |
| `/sbin` | System binaries | System admin tools |
| `/srv` | Service data | Web server data |
| `/sys` | System files | Kernel interfaces |
| `/tmp` | Temporary files | Temp files |
| `/usr` | User programs | Applications |
| `/var` | Variable data | Logs, cache |

---

## 4. Understanding the Functionality of Common Linux Directories

### Detailed Directory Explanations

#### 1. /bin - Essential Binaries

**Purpose:** Essential command binaries for all users

**View Contents:**
```bash
ls /bin | head -10
```

**Output:**
```
bash
cat
cp
date
grep
ls
mkdir
mv
rm
sh
```

**Common Commands:**
- `ls`, `cp`, `mv`, `rm` - File operations
- `cat`, `grep`, `sed` - Text processing
- `bash`, `sh` - Shells

#### 2. /etc - Configuration Files

**Purpose:** System-wide configuration files

**View Contents:**
```bash
ls /etc | head -10
```

**Output:**
```
apt
bash.bashrc
cron.d
fstab
group
hostname
hosts
init.d
passwd
ssh
```

**Important Files:**
- `/etc/passwd` - User accounts
- `/etc/group` - User groups
- `/etc/hosts` - Hostname mappings
- `/etc/fstab` - File system table

**View Specific Config:**
```bash
cat /etc/hostname
```

**Output:**
```
ubuntu-server
```

#### 3. /home - User Home Directories

**Purpose:** Personal directories for each user

**View Contents:**
```bash
ls -l /home
```

**Output:**
```
total 4
drwxr-xr-x 15 abhilash abhilash 4096 Jan 15 10:00 abhilash
drwxr-xr-x 15 user2    user2    4096 Jan 15 10:00 user2
```

**Navigate to Home:**
```bash
cd ~
pwd
```

**Output:**
```
/home/abhilash
```

**View Home Contents:**
```bash
ls -la ~
```

**Text Output:**
```
total 48
drwxr-xr-x 15 abhilash abhilash 4096 Jan 15 10:00 .
drwxr-xr-x  3 root     root     4096 Jan 15 10:00 ..
-rw-------  1 abhilash abhilash  220 Jan 15 10:00 .bash_history
-rw-r--r--  1 abhilash abhilash 3771 Jan 15 10:00 .bashrc
drwxr-xr-x  2 abhilash abhilash 4096 Jan 15 10:00 Desktop
drwxr-xr-x  2 abhilash abhilash 4096 Jan 15 10:00 Documents
drwxr-xr-x  2 abhilash abhilash 4096 Jan 15 10:00 Downloads
```

**Visual Home Directory Structure:**
```mermaid
graph TD
    A[/home/abhilash] --> B[📁 .<br/>Current directory]
    A --> C[📁 ..<br/>Parent directory]
    A --> D[📄 .bash_history<br/>Hidden file]
    A --> E[📄 .bashrc<br/>Hidden config]
    A --> F[📁 Desktop]
    A --> G[📁 Documents]
    A --> H[📁 Downloads]
    
    style A fill:#667eea,stroke:#333,stroke-width:3px,color:#fff
    style B fill:#764ba2,stroke:#333,stroke-width:2px,color:#fff
    style C fill:#f093fb,stroke:#333,stroke-width:2px,color:#fff
    style D fill:#4facfe,stroke:#333,stroke-width:2px,color:#fff
    style E fill:#43e97b,stroke:#333,stroke-width:2px,color:#fff
    style F fill:#fa709a,stroke:#333,stroke-width:2px,color:#fff
    style G fill:#fee140,stroke:#333,stroke-width:2px,color:#000
    style H fill:#30cfd0,stroke:#333,stroke-width:2px,color:#fff
```

#### 4. /usr - User Programs

**Purpose:** User programs and applications

**View Structure:**
```bash
ls /usr
```

**Output:**
```
bin  games  include  lib  local  sbin  share  src
```

**Important Subdirectories:**
- `/usr/bin` - User binaries
- `/usr/lib` - Libraries
- `/usr/local` - Locally installed software
- `/usr/share` - Shared data

**Count Programs:**
```bash
ls /usr/bin | wc -l
```

**Output:**
```
1234
```

#### 5. /var - Variable Data

**Purpose:** Variable data files (logs, cache, etc.)

**View Contents:**
```bash
ls /var
```

**Output:**
```
cache  lib  local  lock  log  mail  opt  run  spool  tmp
```

**Important Subdirectories:**
- `/var/log` - Log files
- `/var/cache` - Cache files
- `/var/tmp` - Temporary files
- `/var/spool` - Spool files

**View Logs:**
```bash
ls /var/log | head -5
```

**Output:**
```
auth.log
syslog
kern.log
dpkg.log
apt
```

**View Recent Log:**
```bash
tail -5 /var/log/syslog
```

**Output:**
```
Jan 15 10:30:01 ubuntu-server systemd: Started Daily apt upgrade and clean activities.
Jan 15 10:30:02 ubuntu-server systemd: Started Daily apt download activities.
Jan 15 10:35:15 ubuntu-server sshd: Accepted publickey for abhilash from 192.168.1.50
Jan 15 10:40:22 ubuntu-server systemd: Started Session 1 of user abhilash.
Jan 15 10:45:30 ubuntu-server kernel: [12345.678] USB device connected
```

#### 6. /tmp - Temporary Files

**Purpose:** Temporary files (cleared on reboot)

**View Contents:**
```bash
ls -l /tmp
```

**Output:**
```
total 8
-rw-r--r-- 1 abhilash abhilash 1024 Jan 15 10:50 temp_file.txt
drwx------ 2 abhilash abhilash 4096 Jan 15 10:45 temp_dir
```

**Create Temp File:**
```bash
touch /tmp/test.txt
ls -l /tmp/test.txt
```

**Output:**
```
-rw-r--r-- 1 abhilash abhilash 0 Jan 15 10:50 /tmp/test.txt
```

#### 7. /dev - Device Files

**Purpose:** Device files representing hardware

**View Devices:**
```bash
ls /dev | head -10
```

**Output:**
```
autofs
block
char
console
cpu
disk
fd
full
input
kmsg
```

**Common Devices:**
- `/dev/sda` - First hard disk
- `/dev/tty` - Terminal
- `/dev/null` - Null device
- `/dev/zero` - Zero device

**Check Disk:**
```bash
ls -l /dev/sd*
```

**Output:**
```
brw-rw---- 1 root disk 8, 0 Jan 15 10:00 /dev/sda
brw-rw---- 1 root disk 8, 1 Jan 15 10:00 /dev/sda1
brw-rw---- 1 root disk 8, 2 Jan 15 10:00 /dev/sda2
```

#### 8. /proc - Process Information

**Purpose:** Virtual filesystem with process and system info

**View Processes:**
```bash
ls /proc | head -10
```

**Output:**
```
1
10
123
456
789
acpi
buddyinfo
bus
cmdline
cpuinfo
```

**View CPU Info:**
```bash
cat /proc/cpuinfo | head -10
```

**Output:**
```
processor       : 0
vendor_id       : GenuineIntel
cpu family      : 6
model           : 158
model name      : Intel(R) Core(TM) i5-8400 CPU @ 2.80GHz
stepping        : 10
microcode       : 0xea
cpu MHz         : 2800.000
cache size      : 9216 KB
physical id     : 0
```

**View Memory Info:**
```bash
cat /proc/meminfo | head -5
```

**Output:**
```
MemTotal:        8168448 kB
MemFree:         1024000 kB
MemAvailable:    5608448 kB
Buffers:          512000 kB
Cached:          4500000 kB
```

#### 9. /sbin - System Binaries

**Purpose:** System administration binaries (usually root-only)

**View Contents:**
```bash
ls /sbin | head -10
```

**Output:**
```
agetty
blkid
fdisk
fsck
ifconfig
init
ip
mkfs
mount
reboot
```

**Common Commands:**
- `fdisk` - Disk partitioning
- `mount` - Mount filesystems
- `reboot` - Reboot system
- `ifconfig` - Network configuration

### Directory Permissions Overview

**Check Permissions:**
```bash
ls -ld /bin /etc /home /root
```

**Output:**
```
drwxr-xr-x 2 root root  4096 Jan 15 10:00 /bin
drwxr-xr-x 120 root root 12288 Jan 15 10:00 /etc
drwxr-xr-x  3 root root  4096 Jan 15 10:00 /home
drwx------  2 root root  4096 Jan 15 10:00 /root
```

**Permission Breakdown:**
- `/bin` - `drwxr-xr-x` - Readable by all, writable by root
- `/etc` - `drwxr-xr-x` - Readable by all, writable by root
- `/home` - `drwxr-xr-x` - Users can access their own
- `/root` - `drwx------` - Only root can access

---

## 5. Introduction to Linux Shortcuts: Boost Your Efficiency

### Command Line Shortcuts

Linux provides many keyboard shortcuts to improve efficiency:

### Navigation Shortcuts

#### Cursor Movement

| Shortcut | Action | Example |
|----------|--------|---------|
| `Ctrl + A` | Move to beginning of line | `^A` |
| `Ctrl + E` | Move to end of line | `^E` |
| `Alt + B` | Move back one word | `Alt+B` |
| `Alt + F` | Move forward one word | `Alt+F` |
| `Ctrl + B` | Move back one character | `^B` |
| `Ctrl + F` | Move forward one character | `^F` |

**Example:**
```bash
# Type: ls -l /home/abhilash
# Press Ctrl+A to go to beginning
# Press Ctrl+E to go to end
```

#### Text Editing

| Shortcut | Action | Example |
|----------|--------|---------|
| `Ctrl + U` | Cut text before cursor | `^U` |
| `Ctrl + K` | Cut text after cursor | `^K` |
| `Ctrl + Y` | Paste cut text | `^Y` |
| `Ctrl + W` | Cut word before cursor | `^W` |
| `Alt + D` | Cut word after cursor | `Alt+D` |
| `Ctrl + D` | Delete character under cursor | `^D` |
| `Ctrl + H` | Delete character before cursor | `^H` |

**Example:**
```bash
# Type: ls -l /home/abhilash
# Press Ctrl+U to cut everything
# Press Ctrl+Y to paste it back
```

### Command History Shortcuts

#### History Navigation

| Shortcut | Action | Example |
|----------|--------|---------|
| `↑` (Up Arrow) | Previous command | Navigate up |
| `↓` (Down Arrow) | Next command | Navigate down |
| `Ctrl + R` | Search history | `^R` then type search |
| `Ctrl + P` | Previous command | Same as ↑ |
| `Ctrl + N` | Next command | Same as ↓ |
| `!!` | Repeat last command | `!!` |
| `!n` | Execute command number n | `!123` |
| `!string` | Execute last command starting with string | `!ls` |

**Example:**
```bash
# Type: ls -l
# Press ↑ to see previous commands
# Type: !! to repeat last command
# Type: !ls to repeat last ls command
```

**Search History:**
```bash
# Press Ctrl+R
# Type: "cd"
# Shows: (reverse-i-search)`cd': cd /home/abhilash
```

### Tab Completion

#### Auto-Completion

| Action | Purpose | Example |
|--------|---------|---------|
| `Tab` | Complete command/file name | Type `ls /ho` then `Tab` |
| `Tab Tab` | Show all possibilities | Type `ls /` then `Tab Tab` |
| `Alt + *` | Expand all matches | `Alt+*` |

**Example:**
```bash
# Type: ls /ho
# Press Tab
# Completes to: ls /home/

# Type: ls /h
# Press Tab Tab
# Shows: /home/  /hosts  /hostname
```

### Process Control Shortcuts

#### Command Control

| Shortcut | Action | Example |
|----------|--------|---------|
| `Ctrl + C` | Cancel/Stop command | `^C` |
| `Ctrl + Z` | Suspend process | `^Z` |
| `Ctrl + D` | Exit/logout | `^D` |
| `Ctrl + L` | Clear screen | `^L` |
| `Ctrl + S` | Pause output | `^S` |
| `Ctrl + Q` | Resume output | `^Q` |

**Example:**
```bash
# Running a long command
# Press Ctrl+C to cancel

# Viewing long output
# Press Ctrl+S to pause
# Press Ctrl+Q to resume
```

### Directory Navigation Shortcuts

#### Quick Navigation

| Shortcut | Action | Example |
|----------|--------|---------|
| `cd ~` | Go to home | `cd ~` |
| `cd -` | Go to previous directory | `cd -` |
| `cd ..` | Go up one level | `cd ..` |
| `cd ../..` | Go up two levels | `cd ../..` |
| `pushd dir` | Save current, go to dir | `pushd /tmp` |
| `popd` | Return to saved directory | `popd` |

**Example:**
```bash
# Current: /home/abhilash/Documents
cd ~
# Now at: /home/abhilash

cd -
# Back to: /home/abhilash/Documents

cd ../..
# Now at: /home
```

### Command Aliases

#### Create Aliases

**View Current Aliases:**
```bash
alias
```

**Output:**
```
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'
```

**Create Custom Alias:**
```bash
alias ll='ls -lh'
alias ..='cd ..'
alias ...='cd ../..'
alias h='cd ~'
```

**Use Alias:**
```bash
ll
```

**Output:**
```
total 24K
drwxr-xr-x 2 abhilash abhilash 4.0K Jan 15 10:30 Desktop
drwxr-xr-x 2 abhilash abhilash 4.0K Jan 15 10:30 Documents
```

**Make Alias Permanent:**
```bash
echo "alias ll='ls -lh'" >> ~/.bashrc
source ~/.bashrc
```

### Useful Shortcut Combinations

#### Common Workflows

**1. Edit and Re-run Command:**
```bash
# Run command
ls -l /home

# Press ↑ to get command back
# Edit it: ls -la /home
# Press Enter
```

**2. Quick Directory Change:**
```bash
# Type: cd /h
# Press Tab (completes to /home/)
# Type: /a
# Press Tab (completes to /home/abhilash/)
# Press Enter
```

**3. Search and Execute:**
```bash
# Press Ctrl+R
# Type: "grep"
# Shows matching command
# Press Enter to execute
```

### Shortcut Practice Session

#### Practice Exercise

```bash
# 1. Type a long command
ls -l /home/abhilash/Documents/projects

# 2. Press Ctrl+A (go to beginning)
# 3. Press Ctrl+K (cut everything)
# 4. Press Ctrl+Y (paste it back)
# 5. Press Ctrl+U (cut before cursor)
# 6. Press Ctrl+E (go to end)
# 7. Press Ctrl+C (cancel)

# 8. Use history
# Press ↑ to see previous commands
# Press Ctrl+R and search for "ls"

# 9. Use tab completion
# Type: cd /h
# Press Tab (completes to /home/)
# Type: /a
# Press Tab (completes to /home/abhilash/)
```

### Shortcut Reference Card

```
┌─────────────────────────────────────────────────────────┐
│              QUICK SHORTCUT REFERENCE                    │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  Navigation:                                            │
│  Ctrl+A  → Beginning of line                           │
│  Ctrl+E  → End of line                                 │
│  Alt+B   → Back one word                               │
│  Alt+F   → Forward one word                           │
│                                                         │
│  Editing:                                              │
│  Ctrl+U  → Cut before cursor                          │
│  Ctrl+K  → Cut after cursor                           │
│  Ctrl+Y  → Paste                                      │
│  Ctrl+W  → Cut word before                           │
│                                                         │
│  History:                                              │
│  ↑       → Previous command                           │
│  ↓       → Next command                              │
│  Ctrl+R  → Search history                            │
│  !!      → Repeat last command                       │
│                                                         │
│  Control:                                              │
│  Ctrl+C  → Cancel command                            │
│  Ctrl+D  → Exit/logout                               │
│  Ctrl+L  → Clear screen                              │
│  Tab     → Auto-complete                             │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

---

## Summary

This guide covered 5 essential topics for Day 6:

1. **Mastering the Linux File System Hierarchy** - Understanding the tree structure
2. **The Significance of the Linux File System Hierarchy** - Why it matters
3. **Inside the Linux Root Directory** - Exploring root directory contents
4. **Understanding Common Linux Directories** - Detailed directory explanations
5. **Introduction to Linux Shortcuts** - Keyboard shortcuts for efficiency

### Key Takeaways

- **File System Hierarchy** is standardized across Linux
- **Each directory** has a specific purpose
- **Shortcuts** significantly improve efficiency
- **Practice** using shortcuts daily

### Next Steps

1. Explore different directories
2. Practice keyboard shortcuts
3. Create useful aliases
4. Learn directory permissions
5. Master file system navigation

---

**Happy Learning! 🚀**
