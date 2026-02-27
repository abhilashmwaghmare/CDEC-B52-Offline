# 🌐 Networking Fundamentals & AWS VPC – Complete DevOps Guide

> Beginner to Advanced | Interview Ready | GitHub Documentation Format

---

# 1️⃣ Basics of Networking

## 🔹 What is Networking?

Networking is the practice of connecting computers and devices to share data and resources.

In cloud computing, networking enables:
- Communication between servers
- Internet access
- Secure traffic routing
- Isolation of environments

---

## 🔹 Key Networking Components

| Component | Description |
|------------|-------------|
| IP Address | Unique identifier of a device |
| Subnet | Logical subdivision of network |
| Router | Routes traffic between networks |
| Switch | Connects devices in LAN |
| Gateway | Entry/Exit point of network |
| DNS | Resolves domain to IP |

---

## 🔹 Types of IP Addresses

### Public IP
- Accessible over internet
- Example: `3.110.20.15`

### Private IP
- Used inside private network
- Example ranges:
  - 10.0.0.0/8
  - 172.16.0.0/12
  - 192.168.0.0/16

---

## 🔹 OSI Model (Interview Favorite)

| Layer | Name | Example |
|-------|------|----------|
| 7 | Application | HTTP |
| 4 | Transport | TCP/UDP |
| 3 | Network | IP |
| 2 | Data Link | MAC |
| 1 | Physical | Cables |

---

## 🔹 TCP vs UDP

| Feature | TCP | UDP |
|----------|------|------|
| Reliable | ✅ | ❌ |
| Ordered | ✅ | ❌ |
| Fast | ❌ | ✅ |
| Example | HTTP | DNS |

---

## 🔹 Real-World Use Case

A web application:
1. User enters URL.
2. DNS resolves IP.
3. TCP connection established.
4. HTTP request sent.

---

# 2️⃣ CIDR (Classless Inter-Domain Routing)

## 🔹 What is CIDR?

CIDR is a method for allocating IP addresses and routing.

Format:
```
IP_Address/Prefix
```

Example:
```
192.168.1.0/24
```

---

## 🔹 What Does /24 Mean?

- 24 bits for network
- Remaining bits for hosts
- Formula:

```
2^(32 - prefix) = total IPs
```

Example:
```
/24 → 2^(32-24) = 256 IPs
```

Usable:
```
256 - 2 = 254
```

---

## 🔹 CIDR Quick Table

| CIDR | Total IPs | Usable |
|------|------------|---------|
| /24 | 256 | 254 |
| /25 | 128 | 126 |
| /26 | 64 | 62 |
| /27 | 32 | 30 |
| /28 | 16 | 14 |

---

## 🔹 CIDR Interview Question

**Q:** Why subtract 2 usable IPs?  
👉 Network ID & Broadcast ID reserved.

---

# 3️⃣ Introduction to VPC (Virtual Private Cloud)

## 🔹 What is VPC?

Amazon VPC is a logically isolated virtual network inside AWS where you launch resources.

Think of it as:
> Your private data center inside AWS.

---

## 🔹 VPC Core Components

- Subnet
- Route Table
- Internet Gateway
- NAT Gateway
- Security Groups
- NACL

---

## 🔹 Basic VPC Architecture

```
                 Internet
                     |
               Internet Gateway
                     |
         +--------------------------+
         |           VPC            |
         |   10.0.0.0/16            |
         |                          |
         |   Public Subnet          |
         |   10.0.1.0/24            |
         |        EC2               |
         |                          |
         |   Private Subnet         |
         |   10.0.2.0/24            |
         |        EC2               |
         +--------------------------+
```

---

## 🔹 Real-Time Use Case

- Public Subnet → Load Balancer
- Private Subnet → Application Server
- Database in Private Subnet

This is 3-tier architecture.

---

# 4️⃣ CIDR Calculation for Subnets

## 🔹 Scenario

VPC CIDR:
```
10.0.0.0/16
```

Need:
- 2 Public Subnets
- 2 Private Subnets

---

## 🔹 Step 1: Understand Available IPs

```
/16 → 2^(32-16) = 65,536 IPs
```

---

## 🔹 Step 2: Choose Subnet Size

If we choose:
```
/24
```

Each subnet:
```
256 IPs
```

---

## 🔹 Subnet Allocation Example

| Subnet | CIDR |
|----------|--------|
| Public-A | 10.0.1.0/24 |
| Public-B | 10.0.2.0/24 |
| Private-A | 10.0.3.0/24 |
| Private-B | 10.0.4.0/24 |

---

## 🔹 Interview Scenario

**Q:** If VPC is /16, can you create /15 subnet?  
👉 No. Subnet must be equal or smaller (higher prefix number).

---

# 5️⃣ Create VPC and Subnet (Step-by-Step)

---

## 🔹 Step 1: Create VPC (Console)

1. Go to VPC Dashboard
2. Click Create VPC
3. CIDR: `10.0.0.0/16`
4. Enable DNS support

---

## 🔹 Step 2: Create Subnets

- Public Subnet: `10.0.1.0/24`
- Private Subnet: `10.0.2.0/24`

Select different AZs.

---

## 🔹 Step 3: Attach Internet Gateway

1. Create IGW
2. Attach to VPC

---

## 🔹 Step 4: Create Route Table

Public Route:
```
0.0.0.0/0 → Internet Gateway
```

Associate with Public Subnet.

---

## 🔹 Step 5: Launch EC2

- Public EC2 → Auto assign public IP
- Private EC2 → No public IP

---

# 🛠 CLI Commands (Optional)

Create VPC:
```bash
aws ec2 create-vpc --cidr-block 10.0.0.0/16
```

Create Subnet:
```bash
aws ec2 create-subnet --vpc-id vpc-xxxx --cidr-block 10.0.1.0/24
```

---

# 🎯 Interview Questions

---

## 🟢 Basic

**Q1:** What is CIDR?  
👉 IP allocation method using prefix length.

**Q2:** What is VPC?  
👉 Isolated network in AWS.

---

## 🟡 Intermediate

**Q3:** Difference between public and private subnet?  
👉 Public has route to IGW.

**Q4:** Why use private subnet?  
👉 Security.

---

## 🔴 Advanced Scenario-Based

**Q5:** Design highly available 3-tier architecture.  
👉 2 public subnets + 2 private subnets across AZs.

**Q6:** How many subnets can be created from /24?  
👉 Cannot divide into larger; can divide into /25 (2 subnets).

**Q7:** Why does AWS reserve 5 IPs per subnet?  
👉 Network, Broadcast, Router, DNS, Reserved.

---

# 🎯 Extended Interview Questions – Networking, CIDR & VPC

---

# 🟢 Part 1: Networking Basics Interview Questions

## 🔹 Basic Level

**Q1. What is an IP address?**  
👉 A unique identifier assigned to a device in a network.

**Q2. Difference between Public IP and Private IP?**  
👉 Public IP is internet accessible; Private IP works inside internal networks.

**Q3. What is a subnet?**  
👉 A logical division of a network to improve security and performance.

**Q4. What is the difference between Router and Switch?**  
👉 Router connects different networks; Switch connects devices within same network.

---

## 🔹 Intermediate Level

**Q5. Explain TCP 3-way handshake.**  
👉 SYN → SYN-ACK → ACK (Connection establishment).

**Q6. What happens when you type google.com in browser?**  
👉 DNS resolution → TCP connection → HTTP request → Server response.

**Q7. What is NAT and why is it used?**  
👉 Network Address Translation allows private instances to access internet securely.

---

## 🔹 Scenario-Based

**Q8. Users cannot access your website. What networking checks will you perform?**  
👉 Check Security Group, NACL, Route Table, Internet Gateway, DNS.

**Q9. High latency in application. What could be networking causes?**  
👉 Packet loss, congestion, cross-region communication, incorrect routing.

---

# 🟢 Part 2: CIDR Interview Questions

---

## 🔹 Basic Level

**Q10. What does /24 mean in CIDR?**  
👉 24 bits for network portion.

**Q11. How many IPs are available in /26?**  
👉 64 total, 62 usable.

**Q12. Why are 2 IPs reserved in normal networking?**  
👉 Network ID & Broadcast ID.

---

## 🔹 AWS-Specific CIDR Questions

**Q13. Why does AWS reserve 5 IPs per subnet?**  
👉 Network, Broadcast, VPC Router, DNS, Future use.

**Q14. Can you create a /15 subnet inside /16 VPC?**  
👉 No. Subnet must be smaller than VPC.

**Q15. How many /24 subnets can be created from /16?**  

Calculation:
```
/16 to /24 = 8 bits difference
2^8 = 256 subnets
```

👉 256 subnets.

---

## 🔹 Advanced CIDR Math Scenario

**Q16. You have 10.0.0.0/24. Create 4 equal subnets. What will be new CIDR?**

Solution:
```
Need 4 subnets → 2^2 = 4
Add 2 bits → /26
```

Subnets:
- 10.0.0.0/26
- 10.0.0.64/26
- 10.0.0.128/26
- 10.0.0.192/26

---

# 🟢 Part 3: VPC Interview Questions

---

## 🔹 Basic Level

**Q17. What is a VPC?**  
👉 A logically isolated network in AWS.

**Q18. What makes a subnet public?**  
👉 Route to Internet Gateway.

**Q19. What is an Internet Gateway?**  
👉 A component that enables internet access for VPC.

---

## 🔹 Intermediate Level

**Q20. Difference between Security Group and NACL?**

| Feature | Security Group | NACL |
|----------|----------------|------|
| Level | Instance | Subnet |
| Stateful | Yes | No |
| Allow/Deny | Allow only | Allow & Deny |

---

**Q21. What is the difference between NAT Gateway and Internet Gateway?**  
👉 IGW allows inbound & outbound internet; NAT allows outbound only for private instances.

---

## 🔹 Scenario-Based Questions

**Q22. Your EC2 in private subnet cannot access internet. What could be the issue?**  
👉 Missing NAT Gateway or route configuration.

**Q23. Public EC2 not accessible via SSH. What do you check?**  
👉 Security Group port 22, route table, public IP attached.

**Q24. Design highly available VPC architecture.**  
👉 Multi-AZ subnets, Load Balancer, NAT per AZ, separate route tables.

---

## 🔹 Architecture & Design Questions

**Q25. How would you design a 3-tier architecture in VPC?**

Answer:
- Public Subnet → Load Balancer
- Private Subnet → App Servers
- Private Subnet → Database
- NAT Gateway for outbound traffic

---

**Q26. Can two VPCs communicate? How?**  
👉 VPC Peering, Transit Gateway, VPN, PrivateLink.

---

**Q27. What happens if you delete Internet Gateway?**  
👉 Public subnets lose internet connectivity.

---

## 🔴 Advanced Production-Level Questions

**Q28. How do you avoid CIDR overlap during multi-VPC design?**  
👉 Plan IP ranges carefully and maintain IP address strategy document.

**Q29. How would you migrate on-prem network to AWS VPC?**  
👉 Use VPN or Direct Connect + non-overlapping CIDR blocks.

**Q30. Explain how Route Tables work in VPC.**  
👉 Route table defines traffic direction rules; associated at subnet level.

---

# 🏁 Interview Answer Tip (Very Important)

For Networking & VPC questions:

1️⃣ Start with definition  
2️⃣ Explain working mechanism  
3️⃣ Give real-time example  
4️⃣ Mention security impact  
5️⃣ Add one limitation  

Example:

> "A VPC is a logically isolated network in AWS that allows us to define our own IP range using CIDR. It contains subnets, route tables, and gateways. In production, we use public subnets for load balancers and private subnets for applications to enhance security."

---


---

