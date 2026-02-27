# 📂 NFS & Amazon EFS – Production-Ready DevOps Guide

> Complete Beginner-to-Advanced Documentation  
> Suitable for GitHub Portfolio | Interview Preparation | AWS Hands-on Labs

---

# 📚 1️⃣ Introduction to NFS (Network File System)

## 🔹 What is NFS?

**NFS (Network File System)** is a distributed file system protocol that allows a client machine to access files over a network as if they were on local storage.

It follows a **client-server architecture**.

---

## 🔹 How NFS Works (Architecture)

- NFS Server exports a directory.
- NFS Client mounts the remote directory.
- Files are accessed over TCP/IP network.

### 🏗 ASCII Architecture Diagram

```
                +---------------------+
                |     NFS Server      |
                |  /data (exported)   |
                +----------+----------+
                           |
                      TCP 2049
                           |
                +----------+----------+
                |      NFS Client     |
                |  Mounted at /mnt    |
                +---------------------+
```

---

## 🔹 NFS Versions

| Version | Features |
|----------|----------|
| NFSv3 | Stateless, widely supported |
| NFSv4 | Stateful, better security, ACL support |

---

## 🔹 Ports Used

| Service | Port |
|----------|------|
| NFS | 2049 |
| RPCBind | 111 |

---

## 🔹 Real-Time Industry Use Cases

- Shared application uploads folder
- Shared logs directory
- Centralized configuration files
- Dev/Test shared storage
- Media rendering farms

---

## 🔹 Advantages

- Easy to configure
- Cost-effective
- Good for shared storage
- Centralized data management

---

## 🔹 Limitations

- Network dependency
- Performance latency
- Security risk if misconfigured
- Not ideal for high IOPS workloads

---

## 🔐 Security Considerations

- Restrict access via IP
- Use NFSv4
- Configure firewall rules
- Use IAM-based solutions (in cloud)
- Encrypt traffic when possible

---

## 🔍 Comparison: Local Storage vs NFS vs EBS vs EFS

| Feature | Local Disk | NFS | EBS | EFS |
|----------|------------|------|------|------|
| Network Based | ❌ | ✅ | ❌ | ✅ |
| Multi Instance Access | ❌ | ✅ | ❌ (except multi-attach) | ✅ |
| Managed Service | ❌ | ❌ | ✅ | ✅ |
| Scalable | ❌ | Limited | Limited | Auto-scale |

---

## 🖼 Image Section

![NFS Architecture](images/nfs-architecture.png)

---

# ☁️ 2️⃣ Amazon EFS Deep Explanation

## 🔹 What is Amazon EFS?

**Amazon Elastic File System (EFS)** is a fully managed, scalable NFS file system provided by AWS.

It supports:
- Linux workloads
- Multi-AZ access
- Auto-scaling storage

---

## 🔹 How EFS Works Internally

- Regional service
- Mount targets created in each AZ
- Accessible via NFS protocol
- Scales automatically

---

## 🏗 AWS EFS Architecture

```
                AWS Region
  -------------------------------------------------
        AZ-a                AZ-b
  +-------------+      +-------------+
  | Mount Target|      | Mount Target|
  +------+------+      +------+------+
         |                     |
     EC2 Instance         EC2 Instance
         |                     |
         +---------- EFS -----------+
```

---

## 🔹 Performance Modes

| Mode | Best For |
|------|----------|
| General Purpose | Low latency workloads |
| Max I/O | High throughput workloads |

---

## 🔹 Throughput Modes

| Mode | Description |
|------|------------|
| Bursting | Based on size |
| Provisioned | Fixed throughput |
| Elastic | Auto scaling (newer mode) |

---

## 🔐 Security Features

- Security Groups (Allow port 2049)
- IAM-based access control
- Encryption at rest (KMS)
- Encryption in transit (TLS)
- NACL control

---

## 🔍 Comparison: EFS vs EBS vs S3

| Feature | EFS | EBS | S3 |
|----------|------|------|------|
| File Storage | ✅ | ❌ | ❌ |
| Block Storage | ❌ | ✅ | ❌ |
| Object Storage | ❌ | ❌ | ✅ |
| Multi Instance Access | ✅ | Limited | Via API |
| Auto Scaling | ✅ | ❌ | ✅ |

---

## 🖼 Image Sections

![EFS Console Screenshot](images/efs-console.png)  
![EFS Architecture](images/efs-architecture.png)

---

# ⚙️ 3️⃣ Step-by-Step Practical Implementation

---

## Step 1️⃣: Launch EC2 Instances

Launch 2 Amazon Linux instances in same VPC.

![EC2 Launch](images/ec2-launch.png)

---

## Step 2️⃣: Create EFS File System

Console:
- Go to EFS → Create File System
- Choose VPC
- Create mount targets

CLI:
```bash
aws efs create-file-system --creation-token my-efs-token
```

---

## Step 3️⃣: Configure Security Groups

Allow inbound:
- Type: NFS
- Port: 2049
- Source: EC2 Security Group

---

## Step 4️⃣: Install NFS Utilities

Amazon Linux:
```bash
sudo yum install -y amazon-efs-utils
```

Ubuntu:
```bash
sudo apt install -y nfs-common
```

---

## Step 5️⃣: Mount EFS on EC2

```bash
sudo mkdir /mnt/efs
sudo mount -t efs fs-xxxx:/ /mnt/efs
```

OR via DNS:

```bash
sudo mount -t nfs4 fs-xxxx.efs.ap-south-1.amazonaws.com:/ /mnt/efs
```

---

## Step 6️⃣: Auto-Mount Using /etc/fstab

```bash
fs-xxxx:/ /mnt/efs efs defaults,_netdev 0 0
```

Test:
```bash
sudo mount -a
```

---

## Step 7️⃣: Test Shared Storage

On EC2-1:
```bash
echo "Hello from Server1" > /mnt/efs/test.txt
```

On EC2-2:
```bash
cat /mnt/efs/test.txt
```

Expected Output:
```
Hello from Server1
```

![Mount Command Output](images/mount-output.png)

---

## 🛠 Troubleshooting Tips

| Issue | Solution |
|-------|----------|
| Mount timeout | Check Security Group |
| Permission denied | Check IAM or POSIX permissions |
| Slow performance | Check throughput mode |
| DNS failure | Verify VPC settings |

---

# 🚀 4️⃣ Real-Time DevOps Use Cases

### ✅ WordPress Multi-Instance Setup
Shared wp-content directory across multiple EC2.

### ✅ Jenkins Shared Workspace
Pipeline artifacts stored centrally.

### ✅ Kubernetes Persistent Volume
Used with EKS via EFS CSI driver.

### ✅ Microservices Logging
Centralized log storage.

### ✅ Shared Uploads for Web Servers
Auto scaling group with shared storage.

---

# 🏆 5️⃣ Production Best Practices

- Create mount targets in all AZs
- Enable lifecycle policy (IA storage)
- Enable automatic backups
- Monitor via CloudWatch
- Use encryption at rest & transit
- Restrict via Security Groups
- Use IAM authorization
- Avoid hardcoding filesystem IDs

---

# 🎯 6️⃣ Advanced Interview Questions

---

## 🔹 Basic Questions

**Q1:** What protocol does EFS use?  
👉 NFS (v4.1)

**Q2:** Can EFS be mounted on multiple EC2 instances?  
👉 Yes.

---

## 🔹 Scenario-Based Questions

**Q:** Your WordPress site runs on Auto Scaling group. How will you share uploads?  
👉 Use EFS mounted across instances.

---

## 🔹 Troubleshooting Question

**Q:** EFS mount fails. What to check first?  
👉 Security Group allowing port 2049.

---

## 🔹 Architecture Design Question

**Q:** Design shared storage for 10 microservices across 3 AZs.  
👉 Use EFS with mount targets in each AZ + security group control.

---

# 🎯 Extended Interview Questions – NFS & Amazon EFS

---

# 🟢 Part 1: NFS Interview Questions

## 🔹 Basic Level

**Q1. What is NFS and why is it used?**  
👉 NFS (Network File System) allows multiple systems to share files over a network as if they were local.

**Q2. What is the default port used by NFS?**  
👉 TCP 2049.

**Q3. Difference between NFSv3 and NFSv4?**  
👉 NFSv3 is stateless; NFSv4 is stateful and supports ACLs and stronger security.

**Q4. What is meant by "exporting" a directory in NFS?**  
👉 Making a directory available for remote clients to mount.

---

## 🔹 Intermediate Level

**Q5. What happens if the NFS server goes down?**  
👉 Clients lose access to mounted storage; applications may hang depending on mount options.

**Q6. What are soft vs hard mounts in NFS?**  

| Mount Type | Behavior |
|------------|----------|
| Hard | Retries indefinitely |
| Soft | Fails after timeout |

**Q7. How do you secure an NFS server?**  
👉 Restrict IPs in exports file, firewall rules, use NFSv4, encrypt traffic.

---

## 🔹 Scenario-Based

**Q8. Your application performance is slow when using NFS. What could be the reasons?**  
👉 Network latency, insufficient throughput, server overload, improper mount options.

**Q9. Can NFS be used across regions?**  
👉 Not recommended due to latency; use cloud-native solutions instead.

---

# 🟢 Part 2: Amazon EFS Interview Questions

---

## 🔹 Basic Level

**Q10. What is Amazon EFS?**  
👉 Fully managed, scalable file storage service using NFS protocol.

**Q11. Which NFS version does EFS use?**  
👉 NFSv4.1.

**Q12. Can EFS be mounted on multiple EC2 instances simultaneously?**  
👉 Yes.

**Q13. Is EFS regional or zonal?**  
👉 Regional (with mount targets in multiple AZs).

---

## 🔹 Intermediate Level

**Q14. Difference between EFS and EBS?**

| Feature | EFS | EBS |
|----------|------|------|
| Storage Type | File | Block |
| Multi-Attach | Yes | Limited |
| Auto Scaling | Yes | No |

**Q15. What are EFS performance modes?**  
👉 General Purpose and Max I/O.

**Q16. What are throughput modes in EFS?**  
👉 Bursting, Provisioned, Elastic.

**Q17. How do you secure EFS?**  
👉 Security Groups, IAM policies, encryption at rest & in transit.

---

## 🔹 Advanced Scenario-Based Questions

**Q18. Design storage for Auto Scaling web servers.**  
👉 Use EFS mounted across instances to share uploads.

**Q19. EFS mount is timing out. What do you check first?**  
👉 Security Group allowing port 2049.

**Q20. How would you implement centralized logging for microservices using EFS?**  
👉 Mount EFS on all instances and store logs centrally.

**Q21. How can you reduce EFS cost?**  
👉 Enable lifecycle policy to move files to Infrequent Access (IA).

**Q22. When would you NOT use EFS?**  
👉 High IOPS database workloads → use EBS instead.

---

# 🟢 Part 3: Troubleshooting & Practical Questions

**Q23. How do you make EFS auto-mount after reboot?**  
👉 Add entry in `/etc/fstab` with `_netdev` option.

**Q24. What happens if mount target is missing in one AZ?**  
👉 EC2 in that AZ cannot connect to EFS.

**Q25. Can Windows EC2 mount EFS?**  
👉 No (EFS supports Linux-based systems).

**Q26. How does EFS scale automatically?**  
👉 Storage grows and shrinks based on usage.

---

# 🟢 Part 4: Architecture & Design Questions

**Q27. Design highly available shared storage across 3 AZs.**  
👉 EFS with mount targets in all AZs + properly configured security groups.

**Q28. How would you use EFS in Kubernetes (EKS)?**  
👉 Deploy EFS CSI driver and create Persistent Volume.

**Q29. How does encryption work in EFS?**  
👉 Data encrypted at rest via AWS KMS and in transit via TLS.

**Q30. Compare EFS vs S3 for shared storage.**  
👉 EFS = file system mount; S3 = object storage accessed via API.

---

# 🏁 Interview Tip

When answering:
- Start with definition
- Explain architecture
- Mention real-world use case
- Add one limitation
- Suggest best practice

Example Answer Structure:
> "EFS is a managed NFS file system in AWS that allows multiple EC2 instances to share storage across AZs. It is ideal for auto-scaling web applications, but not recommended for high-performance databases where EBS would be better."

---

✅ This extended section strengthens:
- Portfolio README
- AWS interview preparation
- DevOps architecture discussions

---



---
