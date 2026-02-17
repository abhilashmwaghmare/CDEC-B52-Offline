# 💾 AWS EBS Advanced --- Partitions, Permanent Mount & Snapshot Automation

> 📘 DevOps Practical Guide (GitHub README Ready)\
> Covers Linux Partitions, Permanent Mount using fstab, EBS Snapshots,
> and Automated Snapshot Policies.

------------------------------------------------------------------------

# 📑 Table of Contents

-   Partitions in Linux
-   Permanent Mount using fstab
-   Backup using EBS Snapshot
-   Automate Snapshot using Policy
-   DevOps Best Practices
-   Interview Preparation

------------------------------------------------------------------------

# 🧩 1️⃣ Partitions in Linux

![Linux Disk Partition Architecture](images/linux-partition-diagram.png)

## 🔹 What is a Partition?

A partition divides a disk into logical sections.

Example:

    Disk: /dev/xvdf
     └── Partition: /dev/xvdf1

Why partitions are used:

✔ Organize storage\
✔ Separate application data\
✔ Improve security and management

------------------------------------------------------------------------

## 🔹 Check Available Disks

``` bash
lsblk
```

------------------------------------------------------------------------

## 🔹 Create Partition using fdisk

``` bash
sudo fdisk /dev/xvdf
```

Inside fdisk:

    n  → new partition
    p  → primary
    w  → save

Verify:

``` bash
lsblk
```

------------------------------------------------------------------------

# 📌 2️⃣ Permanent Mount using fstab

![fstab Permanent Mount Flow](images/linux-fstab-mount.png)

## 🔹 Temporary vs Permanent Mount

  Mount Type   Description
  ------------ ------------------------
  Temporary    Lost after reboot
  Permanent    Auto mounts on startup

------------------------------------------------------------------------

## 🔹 Format Volume

``` bash
sudo mkfs.ext4 /dev/xvdf1
```

------------------------------------------------------------------------

## 🔹 Create Mount Directory

``` bash
sudo mkdir /data
```

------------------------------------------------------------------------

## 🔹 Mount Volume

``` bash
sudo mount /dev/xvdf1 /data
```

Check:

``` bash
df -h
```

------------------------------------------------------------------------

## 🔹 Make Mount Permanent

Edit fstab:

``` bash
sudo nano /etc/fstab
```

Add entry:

    /dev/xvdf1  /data  ext4  defaults,nofail  0  2

Test configuration:

``` bash
sudo mount -a
```

------------------------------------------------------------------------

# 📸 3️⃣ Take Backup using Snapshot

![AWS EBS Snapshot Architecture](images/aws-ebs-snapshot.png)

## 🔹 What is Snapshot?

Snapshot is a **backup of EBS volume** stored in Amazon S3.

Benefits:

✔ Point-in-time backup\
✔ Disaster recovery\
✔ Easy restore

------------------------------------------------------------------------

## 🔹 Create Snapshot (Manual)

Steps:

1.  Go to EC2 → Volumes
2.  Select Volume
3.  Actions → Create Snapshot
4.  Provide description

------------------------------------------------------------------------

## 🔹 Real DevOps Use Case

Before deploying application updates:

    Take Snapshot → Deploy → Rollback if failure

------------------------------------------------------------------------

# ⚙️ 4️⃣ Automate Snapshot using Snapshot Policy

![Snapshot Automation Architecture](images/aws-snapshot-policy.png)

## 🔹 What is Snapshot Policy?

AWS Data Lifecycle Manager (DLM) automates snapshot creation.

Example:

    Daily backup at 2 AM
    Retention: 7 days

------------------------------------------------------------------------

## 🔹 Steps to Create Snapshot Policy

1.  EC2 → Lifecycle Manager
2.  Create Lifecycle Policy
3.  Select:

```{=html}
<!-- -->
```
    Resource Type: EBS Volume
    Schedule: Daily
    Retention: 7 Snapshots

4.  Apply Tags to Target Volumes

------------------------------------------------------------------------

## 🔹 DevOps Automation Flow

    Tagged EBS Volume
           ↓
    Lifecycle Policy
           ↓
    Automated Snapshots

Benefits:

✔ No manual backup\
✔ Automated compliance\
✔ Reduced risk

------------------------------------------------------------------------

# 🧠 DevOps Best Practices

    ✔ Use UUID instead of device name in fstab
    ✔ Always test fstab with mount -a
    ✔ Take snapshot before resizing volume
    ✔ Automate backups using lifecycle policy
    ✔ Use tags to manage snapshot automation

------------------------------------------------------------------------

# 💼 🎯 Interview Preparation

## ✅ Beginner Questions

1.  What is a partition?
2.  Command to check disks?
3.  What is fstab?
4.  What is EBS snapshot?
5.  Why take backup?

------------------------------------------------------------------------

## ⚙️ Intermediate Questions

1.  Temporary vs permanent mount?
2.  Snapshot vs AMI difference?
3.  What is lifecycle policy?
4.  Why use UUID in fstab?

------------------------------------------------------------------------

## 🚀 Scenario-Based Questions

1.  Volume mounted but disappears after reboot --- reason? 👉 Missing
    fstab entry.

2.  Need daily automated backups --- solution? 👉 Snapshot lifecycle
    policy.

3.  Application update failed --- recovery method? 👉 Restore from
    snapshot.

------------------------------------------------------------------------

# 📁 Suggested GitHub Repo Structure

    aws-ebs-advanced/
    │
    ├── README.md
    └── images/
        ├── linux-partition-diagram.png
        ├── linux-fstab-mount.png
        ├── aws-ebs-snapshot.png
        └── aws-snapshot-policy.png

------------------------------------------------------------------------

# ⭐ DevOps Trainer Notes

This README follows real DevOps repo design:

-   Practical Linux implementation
-   AWS architecture diagrams
-   Automation-focused learning
-   Interview-ready explanations
