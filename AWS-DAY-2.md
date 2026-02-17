# 🚀 AWS Fundamentals — Dashboard, Region, AZ & EC2 Ubuntu Launch (Complete Guide)

> 📘 **Single GitHub README File**  
> Beginner → Intermediate | DevOps & AWS Foundation  
> Covers AWS Dashboard, Region vs AZ, EC2 Basics, and Launching Your First Ubuntu Instance.

---

# 🧭 1️⃣ Introduction to AWS Dashboard

![AWS Dashboard Overview](images/aws-dashboard-overview.png)

## 🔹 What is AWS Dashboard?

The **AWS Management Console** is a web-based interface used to create, manage, and monitor AWS resources.

It acts as the **central control panel** for:

- Launching servers
- Managing storage
- Configuring networking
- Monitoring applications

When you login to AWS, this dashboard is your starting point.

---

## 🔹 Main Sections of AWS Dashboard

### 🧱 Navigation Bar

Located at the top:

- 🔎 Service Search (EC2, S3, IAM)
- 🌍 Region Selector
- 👤 Account Settings
- 🔔 Notifications

💡 **DevOps Tip:** Always confirm the selected region before creating resources.

---

### 📂 Services Menu

AWS groups services into categories:

| Category | Example Services | Usage |
|---|---|---|
| Compute | EC2, Lambda | Virtual servers |
| Storage | S3, EBS | Data storage |
| Database | RDS, DynamoDB | Managed DB |
| Networking | VPC, Route53 | Network control |
| Security | IAM, WAF | Access & protection |

---

### ⭐ Recently Used Services

Shows services you accessed frequently:

- EC2
- IAM
- CloudWatch
- S3

Helps DevOps engineers work faster.

---

## 🔹 Real-Time DevOps Use Case

A DevOps engineer uses AWS Dashboard to:

- Launch EC2 servers
- Configure security groups
- Monitor logs
- Deploy scalable applications

---

## 🔹 Dashboard Best Practices

✔ Enable MFA
✔ Use IAM users instead of root
✔ Tag resources properly
✔ Select correct region


---

# 🌍 2️⃣ Region vs Availability Zone (AZ)

![AWS Region and Availability Zone Architecture](images/aws-region-az-architecture.png)

## 🔹 What is a Region?

A **Region** is a physical geographic location containing multiple AWS data centers.

Examples:

- ap-south-1 → Mumbai
- us-east-1 → North Virginia
- eu-west-1 → Ireland

### Why Regions Matter?

- Reduce latency
- Meet compliance requirements
- Disaster recovery planning

---

## 🔹 What is an Availability Zone (AZ)?

An Availability Zone is an **isolated data center** within a region.

Example:

Region: ap-south-1
├── ap-south-1a
├── ap-south-1b
└── ap-south-1c


Each AZ has:

- Independent power supply
- Separate networking
- Physical isolation

---

## 🔹 Why Multiple AZs Exist?

AWS designs AZs for **High Availability**.

If one AZ fails:

👉 Application continues running in another AZ.

---

## 🔹 Region vs AZ Comparison

| Feature | Region | Availability Zone |
|---|---|---|
| Scope | Geographic area | Datacenter group |
| Latency | Higher between regions | Very low |
| Isolation Level | High | Medium |
| Purpose | Global deployment | Fault tolerance |

---

## 🔹 Real Industry Example

E-commerce Architecture:

Load Balancer
├── App Server (AZ-a
Benefits:

✔ High availability  
✔ Disaster recovery  

---

# 🖥️ 3️⃣ Introduction to EC2 Service

![Amazon EC2 Architecture Diagram](images/aws-ec2-architecture.png)

## 🔹 What is Amazon EC2?

EC2 (Elastic Compute Cloud) provides **virtual servers** in AWS.

👉 Equivalent to a virtual machine but hosted in cloud.

---

## 🔹 Why DevOps Engineers Use EC2?

- Host web applications
- Deploy Docker containers
- Run Jenkins pipelines
- Create Kubernetes clusters

---

## 🔹 EC2 Core Components

### 🧾 AMI (Amazon Machine Image)

Template containing:

- Operating system
- Software configuration
- Security setup

Examples:

- Ubuntu Server
- Amazon Linux
- Windows Server

---

### ⚙️ Instance Type

Defines hardware:

| Instance | Use Case |
|---|---|
| t2.micro | Practice / Free tier |
| t3.medium | Application server |
| m5.large | Production workloads |

---

### 🔐 Key Pair

Used for secure SSH login.

Formats:

- `.pem` → Linux/Mac
- `.ppk` → Windows PuTTY

---

### 🔥 Security Group

Acts as a virtual firewall.

Common Rules:

| Port | Purpose |
|---|---|
| 22 | SSH |
| 80 | HTTP |
| 443 | HTTPS |

---

## 🔹 Real DevOps Pipeline Example


└── App Server (AZ-b)
Database Replica (AZ-c)

GitHub → Jenkins → Build Docker Image → Deploy on EC2


---

# 🚀 4️⃣ Create First Ubuntu EC2 Instance (Step-by-Step)

![Launch Ubuntu EC2 Workflow](images/aws-ubuntu-instance-launch.png)

## 🔹 Step 1 — Open EC2 Dashboard

AWS Console → Search **EC2** → Click **Launch Instance**.

---

## 🔹 Step 2 — Name Your Instance

Example:

devops-ubuntu-server


---

## 🔹 Step 3 — Choose AMI

Select:

👉 Ubuntu Server 22.04 LTS

Why Ubuntu?

- Stable
- DevOps-friendly
- Supports Docker & Kubernetes

---

## 🔹 Step 4 — Choose Instance Type

t2.micro (Free Tier Eligible)


---

## 🔹 Step 5 — Create Key Pair

Key Name: ubuntu-key
Type: RSA
Format: .pem



⚠️ Download and store safely.

---

## 🔹 Step 6 — Configure Network Settings

Enable inbound rules:

✔ SSH (22)
✔ HTTP (80)
✔ HTTPS (443)


---

## 🔹 Step 7 — Configure Storage

Default:
8 GB gp3 volume


Benefits of gp3:

- Better performance
- Adjustable IOPS

---

## 🔹 Step 8 — Launch Instance

Click **Launch Instance**.

Wait until:

Running
2/2 Status Checks Passed


---

## 🔹 Step 9 — Connect to Ubuntu Server

```bash
chmod 400 ubuntu-key.pem
ssh -i ubuntu-key.pem ubuntu@<Public-IP>


What is AWS Dashboard? → Web interface for AWS services.

Define Region. → Geographic AWS location.

Define Availability Zone. → Isolated datacenter.

What is EC2? → Virtual server in cloud.

What is AMI? → OS template.

Default Ubuntu user? → ubuntu.

Security Group? → Instance firewall.

Free tier instance? → t2.micro.

SSH port? → 22.

Why multiple AZs? → High availability.

EC2 belongs to? → IaaS.

Public IP? → Internet-accessible address.

Key Pair purpose? → Secure login.

Region selection reason? → Lower latency.

Status check meaning? → Instance health verification.

Region vs AZ difference? → Location vs datacenter.

Why Multi-AZ deployment? → Fault tolerance.

Role of AMI? → Standardization.

Open SSH risk? → Unauthorized access.

Scaling EC2? → Auto Scaling Groups.

gp3 advantage? → Performance control.

Why avoid root login? → Security risk.

Elastic IP use case? → Static IP.

Public vs Private subnet? → Internet vs internal.

DevOps use of EC2? → CI/CD hosting.

🚀 Scenario-Based (5)

AZ failure occurs — solution? → Multi-AZ architecture.

Need reusable server template? → Create AMI.

SSH access restricted? → Limit security group IPs.

Startup deploys web app quickly? → Launch Ubuntu EC2.

Reusable infrastructure setup? → Launch Template.


