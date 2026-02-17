# 🚀 AWS Fundamentals --- DevOps Training Repository

![AWS](images/aws-architecture-cover.png)

![GitHub repo size](https://img.shields.io/badge/AWS-EC2-blue)
![DevOps](https://img.shields.io/badge/DevOps-Learning-orange)
![Level](https://img.shields.io/badge/Level-Beginner_to_Intermediate-green)

> 📘 **Clean DevOps-Style README**\
> Covers AWS Dashboard, Region vs AZ, EC2 Basics & Ubuntu Instance
> Deployment.

------------------------------------------------------------------------

# 📑 Table of Contents

-   [Introduction to AWS Dashboard](#-1️⃣-introduction-to-aws-dashboard)
-   [Region vs Availability Zone](#-2️⃣-region-vs-availability-zone-az)
-   [Introduction to EC2 Service](#-3️⃣-introduction-to-ec2-service)
-   [Launch Ubuntu EC2 Instance](#-4️⃣-create-first-ubuntu-ec2-instance)
-   [Architecture Layout](#-real-aws-architecture-layout)
-   [Interview Preparation](#-interview-preparation)

------------------------------------------------------------------------

# 🧭 1️⃣ Introduction to AWS Dashboard

![AWS Dashboard](images/aws-dashboard-overview.png)

## 🔹 Overview

AWS Management Console is the web UI used to control cloud
infrastructure.

### Core Sections

-   🔎 Search Bar
-   🌍 Region Selector
-   📂 Services Menu
-   ⭐ Recently Used Services

### DevOps Usage

-   Launch servers
-   Manage networking
-   Configure IAM
-   Monitor applications

``` bash
Best Practice:
✔ Use IAM user
✔ Enable MFA
✔ Verify Region before deployment
```

------------------------------------------------------------------------

# 🌍 2️⃣ Region vs Availability Zone (AZ)

![Region AZ Diagram](images/aws-region-az-architecture.png)

## 🔹 Region

A geographic location with multiple AWS data centers.

Examples: - ap-south-1 (Mumbai) - us-east-1 (Virginia)

## 🔹 Availability Zone

Independent data centers inside a region designed for fault tolerance.

    Region: ap-south-1
     ├── AZ-a
     ├── AZ-b
     └── AZ-c

### 📊 Comparison Table

  Feature   Region              AZ
  --------- ------------------- -------------------
  Scope     Geographic          Datacenter
  Latency   Higher              Very Low
  Purpose   Global deployment   High availability

------------------------------------------------------------------------

# 🖥️ 3️⃣ Introduction to EC2 Service

![EC2 Architecture](images/aws-ec2-architecture.png)

## 🔹 What is EC2?

Elastic Compute Cloud provides scalable virtual machines.

### Key Components

#### 🧾 AMI

Operating system template (Ubuntu, Amazon Linux)

#### ⚙️ Instance Type

Defines CPU & RAM (t2.micro, t3.medium)

#### 🔐 Key Pair

Secure SSH login

#### 🔥 Security Group

Instance firewall rules

Example DevOps Flow:

    Developer → GitHub → Jenkins → Docker → EC2 Deployment

------------------------------------------------------------------------

# 🚀 4️⃣ Create First Ubuntu EC2 Instance

![Ubuntu Launch Workflow](images/aws-ubuntu-instance-launch.png)

## Step-by-Step Deployment

### 1. Launch Instance

EC2 → Launch Instance

### 2. Choose AMI

Ubuntu Server 22.04 LTS

### 3. Instance Type

`t2.micro` (Free Tier)

### 4. Create Key Pair

RSA → `.pem`

### 5. Configure Network

Allow: - SSH (22) - HTTP (80) - HTTPS (443)

### 6. Storage

Default 8GB gp3

### 7. Launch

Wait for:

    Running
    2/2 Status Checks Passed

### 🔗 Connect via SSH

``` bash
chmod 400 ubuntu-key.pem
ssh -i ubuntu-key.pem ubuntu@<Public-IP>
```

### Install Docker (DevOps Setup)

``` bash
sudo apt update -y
sudo apt install docker.io -y
```

------------------------------------------------------------------------

# 🧠 Real AWS Architecture Layout

![Production Architecture](images/aws-production-architecture.png)

Typical Highly Available Design:

    Internet
       ↓
    Application Load Balancer
       ↓
    Auto Scaling Group (EC2 - Multi AZ)
       ↓
    RDS Database (Multi AZ)

Benefits:

✔ High Availability\
✔ Fault Tolerance\
✔ Scalability

------------------------------------------------------------------------

# 💼 🎯 Interview Preparation

## ✅ Beginner

-   What is AWS Dashboard?
-   Define Region.
-   Define Availability Zone.
-   What is EC2?
-   What is AMI?

## ⚙️ Intermediate

-   Region vs AZ difference?
-   Why Multi-AZ deployment?
-   Role of Security Groups?
-   How EC2 scales?

## 🚀 Scenario

-   AZ failure --- architecture solution?
-   Need reusable server template?
-   Secure SSH access design?

------------------------------------------------------------------------

# 📁 Suggested Repo Structure

    aws-devops-training/
    │
    ├── README.md
    └── images/
        ├── aws-dashboard-overview.png
        ├── aws-region-az-architecture.png
        ├── aws-ec2-architecture.png
        ├── aws-ubuntu-instance-launch.png
        └── aws-production-architecture.png

------------------------------------------------------------------------

# ⭐ DevOps Trainer Notes

This README follows **real DevOps repository design**:

-   Clean sections
-   Architecture visuals
-   Practical commands
-   Interview prep

Perfect for:

✔ Training batches\
✔ GitHub portfolio\
✔ AWS beginner bootcamps
