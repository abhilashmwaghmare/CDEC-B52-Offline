# 🌐 AWS VPC Advanced Networking Lab  
> Internet Gateway | Public & Private EC2 | NAT Gateway | VPC Peering  
> Production-Ready | Interview-Focused | GitHub Documentation Format

---

# 📘 1️⃣ Create Internet Gateway (IGW) and Configure Route

## 🔹 What is an Internet Gateway?

An **Internet Gateway (IGW)** enables communication between instances in your VPC and the public internet.

It performs:
- Route target for internet-bound traffic
- 1:1 NAT for public IP addresses

---

## 🏗 Architecture Overview

```
              Internet
                  |
            +-------------+
            |  Internet   |
            |   Gateway   |
            +------+------+
                   |
              +----+----+
              |   VPC   |
              |10.0.0.0/16|
              +----+----+
                   |
             Public Subnet
                   |
               EC2 (Public IP)
```

---

## 🪜 Step-by-Step: Create IGW

### Console Steps

1. Go to **VPC Dashboard**
2. Click **Internet Gateways**
3. Click **Create Internet Gateway**
4. Attach it to your VPC

---

## 🪜 Configure Route Table

1. Go to **Route Tables**
2. Select Public Route Table
3. Add route:

```
Destination: 0.0.0.0/0
Target: Internet Gateway
```

4. Associate with Public Subnet

---

## 🛠 CLI Command

```bash
aws ec2 create-internet-gateway
aws ec2 attach-internet-gateway --internet-gateway-id igw-xxxx --vpc-id vpc-xxxx
```

---

## 🎯 Interview Question

**Q:** What makes a subnet public?  
👉 A route to Internet Gateway + Public IP enabled.

---

# 📘 2️⃣ Launch Public and Private EC2 Instances

---

## 🟢 Public Instance

### Requirements:
- Public Subnet
- Route to IGW
- Auto-assign Public IP enabled
- Security Group allows SSH (22)

---

## 🔴 Private Instance

### Requirements:
- Private Subnet
- No direct route to IGW
- No public IP
- Access via Bastion Host or NAT

---

## 🏗 Architecture

```
              Internet
                  |
                 IGW
                  |
         ---------------------
         |   Public Subnet   |
         |   EC2 (Bastion)   |
         ---------------------
                  |
         ---------------------
         |  Private Subnet   |
         |   EC2 (App)       |
         ---------------------
```

---

## 🛠 Launch via CLI

```bash
aws ec2 run-instances \
--image-id ami-xxxx \
--instance-type t2.micro \
--subnet-id subnet-xxxx \
--associate-public-ip-address
```

---

## 🎯 Interview Scenario

**Q:** You cannot SSH into public EC2. What do you check?  
👉 Security Group, Route Table, Public IP, NACL.

---

# 📘 3️⃣ NAT Gateway

---

## 🔹 What is NAT Gateway?

A **NAT Gateway** allows instances in private subnet to access the internet **without allowing inbound internet traffic**.

Used for:
- OS updates
- Package installation
- API calls

---

## 🏗 NAT Architecture

```
              Internet
                  |
                 IGW
                  |
            NAT Gateway
           (Public Subnet)
                  |
            Private Subnet
               EC2 Instance
```

---

## 🪜 Step-by-Step Setup

### Step 1: Create Elastic IP
Allocate Elastic IP.

### Step 2: Create NAT Gateway
- Choose Public Subnet
- Attach Elastic IP

### Step 3: Update Private Route Table

Add route:

```
Destination: 0.0.0.0/0
Target: NAT Gateway
```

---

## 🛠 CLI Example

```bash
aws ec2 create-nat-gateway \
--subnet-id subnet-public \
--allocation-id eipalloc-xxxx
```

---

## 🎯 Interview Questions

**Q:** Difference between NAT Gateway and Internet Gateway?  

| Feature | IGW | NAT |
|----------|------|------|
| Inbound Internet | ✅ | ❌ |
| Outbound Internet | ✅ | ✅ |
| Used For | Public Subnet | Private Subnet |

---

**Q:** Why is NAT placed in Public Subnet?  
👉 It needs internet access via IGW.

---

# 📘 4️⃣ VPC Peering

---

## 🔹 What is VPC Peering?

VPC Peering allows communication between two VPCs using private IP addresses.

---

## 🏗 Architecture

```
        VPC-A (10.0.0.0/16)
                |
         Peering Connection
                |
        VPC-B (192.168.0.0/16)
```

---

## 🪜 Steps to Create VPC Peering

1. Go to VPC → Peering Connections
2. Create Peering Request
3. Accept Request (if same account or cross-account)
4. Update Route Tables in both VPCs

Example:

In VPC-A Route Table:
```
Destination: 192.168.0.0/16
Target: Peering Connection
```

In VPC-B Route Table:
```
Destination: 10.0.0.0/16
Target: Peering Connection
```

---

## 🚨 Important Notes

- CIDR must NOT overlap
- Peering is not transitive
- No need for IGW

---

## 🎯 Interview Questions

**Q:** Can VPC Peering connect 3 VPCs transitively?  
👉 No.

**Q:** What happens if CIDR overlaps?  
👉 Peering cannot be created.

**Q:** Difference between VPC Peering and Transit Gateway?  
👉 Peering is point-to-point; Transit Gateway is hub-and-spoke.

---

# 🏁 Real-Time Production Scenario

Company Setup:

- VPC-1: Production
- VPC-2: Shared Services (Monitoring, Logging)
- Private Subnets for Applications
- NAT for internet updates
- Bastion in Public Subnet
- Peering for internal communication

---

# 🔥 Advanced Scenario-Based Interview Questions

---

### Q1: Design secure 3-tier architecture with internet access.
Answer:
- Public Subnet → ALB
- Private Subnet → App Servers
- Private Subnet → DB
- NAT for outbound
- Security Groups layered

---

### Q2: Private EC2 cannot access yum repository.
Check:
- NAT Gateway
- Private Route Table
- Security Group
- NACL

---

### Q3: How to allow communication between Dev and Prod VPC?
Answer:
- VPC Peering or Transit Gateway
- Update route tables
- Security Groups

---

# 📌 Summary

- IGW provides internet access to public subnets.
- NAT provides outbound internet to private subnets.
- Public EC2 = IGW route + Public IP.
- VPC Peering connects two VPCs privately.
- Proper route table configuration is critical.

---

# 🌐 AWS VPC Networking Practical Lab 

> Step-by-Step Hands-On Guide  
> Covers: IGW, Public & Private EC2, NAT Gateway, VPC Peering  
> With Interview Questions (Basic → Advanced)

---

# 🎯 LAB ARCHITECTURE (What We Are Building)

```
                    Internet
                        |
                     [IGW]
                        |
                -----------------
                |   Public Subnet |
                |  Bastion EC2    |
                -----------------
                        |
                   [NAT Gateway]
                        |
                -----------------
                |  Private Subnet |
                |   App EC2       |
                -----------------

        +--------------------------------+
        |            VPC-1               |
        |         10.0.0.0/16            |
        +--------------------------------+

        +--------------------------------+
        |            VPC-2               |
        |        192.168.0.0/16          |
        +--------------------------------+
                 (VPC Peering)
```

---

# 🧪 PART 1: Create VPC & Subnets

---

## ✅ Step 1: Create VPC

1. Go to **VPC Dashboard**
2. Click **Create VPC**
3. Name: `Student-VPC`
4. CIDR: `10.0.0.0/16`
5. Enable DNS Hostnames

Click **Create**

---

## ✅ Step 2: Create Subnets

### 🔹 Public Subnet
- Name: `Public-Subnet`
- CIDR: `10.0.1.0/24`
- AZ: ap-south-1a
- Enable Auto-assign Public IP

### 🔹 Private Subnet
- Name: `Private-Subnet`
- CIDR: `10.0.2.0/24`
- AZ: ap-south-1a

---

# 🌍 PART 2: Create Internet Gateway (IGW)

---

## ✅ Step 3: Create IGW

1. VPC → Internet Gateways
2. Click **Create Internet Gateway**
3. Name: `Student-IGW`
4. Attach to `Student-VPC`

---

## ✅ Step 4: Update Route Table (Public)

1. Go to Route Tables
2. Select Public Route Table
3. Edit Routes
4. Add:

```
Destination: 0.0.0.0/0
Target: Internet Gateway
```

5. Associate this route table with **Public Subnet**

---

# 💻 PART 3: Launch Public and Private EC2

---

## ✅ Step 5: Launch Public EC2 (Bastion)

- Subnet: Public Subnet
- Auto-assign Public IP: Enabled
- Security Group:
  - Allow SSH (22) from your IP

Test:
```
ssh ec2-user@Public-IP
```

---

## ✅ Step 6: Launch Private EC2

- Subnet: Private Subnet
- No Public IP
- Security Group:
  - Allow SSH from Public EC2 Security Group

---

# 🔐 PART 4: Setup NAT Gateway

---

## ✅ Step 7: Allocate Elastic IP

1. EC2 → Elastic IPs
2. Allocate new Elastic IP

---

## ✅ Step 8: Create NAT Gateway

1. VPC → NAT Gateways
2. Create NAT Gateway
3. Select Public Subnet
4. Attach Elastic IP

Wait until status = Available

---

## ✅ Step 9: Update Private Route Table

Add route:

```
Destination: 0.0.0.0/0
Target: NAT Gateway
```

Associate with Private Subnet.

---

## ✅ Step 10: Test Internet from Private EC2

From Bastion:

```
ssh ec2-user@Private-IP
```

Then:

```
sudo yum update -y
```

If working → NAT configured correctly 🎉

---

# 🔗 PART 5: VPC Peering

---

## ✅ Step 11: Create Second VPC

- Name: `Student-VPC-2`
- CIDR: `192.168.0.0/16`

Create one subnet:
- `192.168.1.0/24`

---

## ✅ Step 12: Create VPC Peering

1. Go to VPC → Peering Connections
2. Create Peering
3. Select VPC-1 & VPC-2
4. Accept Request

---

## ✅ Step 13: Update Route Tables (Both VPCs)

In VPC-1 Route Table:

```
Destination: 192.168.0.0/16
Target: Peering Connection
```

In VPC-2 Route Table:

```
Destination: 10.0.0.0/16
Target: Peering Connection
```

---

## ✅ Step 14: Test Connectivity

Launch EC2 in VPC-2.

From VPC-1 EC2:

```
ping 192.168.1.x
```

If working → Peering success ✅

---

# 🎯 INTERVIEW QUESTIONS

---

# 🟢 Basic Level

**Q1: What makes a subnet public?**  
👉 Route to IGW + Public IP enabled.

**Q2: Why NAT is required?**  
👉 Private EC2 cannot access internet directly.

**Q3: Can private EC2 have internet without NAT?**  
👉 No.

---

# 🟡 Intermediate Level

**Q4: Difference between NAT Gateway and IGW?**

| Feature | IGW | NAT |
|----------|------|------|
| Inbound Traffic | Yes | No |
| Outbound Traffic | Yes | Yes |
| Used In | Public Subnet | Private Subnet |

---

**Q5: Why NAT must be in Public Subnet?**  
👉 It needs route to IGW.

---

**Q6: What happens if CIDR overlaps in VPC Peering?**  
👉 Peering will fail.

---

# 🔴 Scenario-Based Questions

**Q7: Private EC2 cannot run yum update. What will you check?**
- NAT Gateway exists?
- Private route table?
- Security Group?
- NACL?

---

**Q8: Public EC2 not reachable from internet.**
Check:
- Public IP attached?
- Route table?
- IGW attached?
- Security Group?

---

**Q9: Can VPC Peering connect 3 VPCs transitively?**
👉 No. It is not transitive.

---

**Q10: How to design highly available NAT setup?**
👉 NAT Gateway in each AZ + separate route tables.

---

# 🏁 FINAL SUMMARY FOR STUDENTS

- IGW = Internet access for public subnet
- NAT = Internet access for private subnet
- Public EC2 = Public IP + IGW route
- Private EC2 = No public IP + NAT route
- VPC Peering = Private communication between VPCs
- Route tables control traffic flow

---
