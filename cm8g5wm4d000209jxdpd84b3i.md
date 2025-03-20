---
title: "Day 2: EC2 Fundamentals - AWS Solutions Architect Preparation"
seoTitle: "AWS EC2 Basics: Day 2 Exam Guide"
seoDescription: "Learn key concepts of EC2, budget setup, instance types, purchasing options, and security groups in AWS Solutions Architect exam preparation"
datePublished: Wed Mar 19 2025 16:54:07 GMT+0000 (Coordinated Universal Time)
cuid: cm8g5wm4d000209jxdpd84b3i
slug: day-2-ec2-fundamentals-aws-solutions-architect-preparation
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1742403165880/e338a451-180c-4593-bc45-c4ab6eeb9963.png
tags: aws, cloud-computing, solutionarchitect

---

## Introduction

These are my notes while preparing for the **AWS Solutions Architect Associate-Level exam**. I'll cover foundational concepts, hands-on activities, and best practices. Let's start with the first topic: **AWS Budget Setup.**

---

## AWS Budget Setup (Hands-On)

1. **Navigate to Billing & Cost Management:**
    
    * Click on **Billing & Cost Management**.
        
2. **Fixing IAM Permission Issues:**
    
    * Some IAM users might face "permission denied" issues even with admin privileges.
        
    * To fix this:
        
        * **Login as root** → **Accounts** → **IAM user & role access to billing info** → **Edit** → **Activate IAM access**.
            
            ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1742452721624/21d5b971-18e8-4277-a133-840f2fe10636.png align="center")
            
            ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1742452770660/dc9631db-822c-4e64-93c5-1c8b239aba11.png align="center")
            
3. **Exploring Billing & Cost Management:**
    
    * View **bills** & check **charges by service**.
        
    * Explore **Free Tier** & check **AWS bill forecast**.
        
4. **Setting Up EC2 Budget:**
    
    * **Zero Cost Budget:**
        
        * **Billing & Cost Management** → **Budget** → **Create Budget** → **Use a template** → **Zero Spend Budget** → **Add email** → **Create Budget**.
            
            ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1742453341869/062894a3-f5a2-466b-ada0-62fbfa1e6034.png align="center")
            
            ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1742453406368/98ff453b-3130-46ba-8f6e-c1e44ed910e3.png align="center")
            
    * **Monthly Cost Budget ($10 Example):**
        
        * Follow the same procedure, in templates select what you want like “Monthly cost budget“
            
        * When actual spending reaches **85%**, an alert is sent to the email.
            
            ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1742453557211/68c276d4-7b52-461b-8947-05bbb3ed82cc.png align="center")
            

---

## EC2 - Elastic Compute Cloud

### Overview

* **Most popular AWS offering** → Infrastructure as a Service (IaaS)
    
* **Key Capabilities:**
    
    * Renting VMs (**EC2**)
        
    * Storing data on virtual drives (**EBS**)
        
    * Distributing load across machines (**ELB**)
        
    * Scaling (**ASG**)
        
* **EC2 is fundamental to understanding how the cloud works.**
    

### EC2 Sizing & Configuration Options:

* **OS:** Linux, Windows, Mac
    
* **CPU:** Compute power & cores
    
* **RAM:** Memory allocation
    
* **Storage:** EBS, EFS, or Instance Store
    
* **Network:** Speed, public IP availability
    
* **Firewall Rules:** Security Group settings
    

### EC2 User Data

* **Bootstrapping instance through user data scripts**
    
* **Runs commands when the machine starts**
    
* **Executes only once**
    
* **Automates boot tasks like installations**
    
* **Runs with root user privileges**
    

### EC2 Instance Types

* **General-purpose:** `t2.micro`, `t2.xlarge`
    
* **Compute-optimized:** `c5d.4xlarge`
    
* **Memory-optimized:** `m5.8xlarge`
    

---

## Hands-On: Launching an EC2 Instance & Hosting a Website

### Steps to Launch an EC2 Instance

1. **Launch Instance**
    
    * Name: `<some name>`
        
    * Add tags (optional)
        
    * **AMI:** Amazon Linux (Free Tier)
        
    * **Instance Type:** `t2.micro`
        
    * **Key Pair:** Create a new key pair
        
        * Name: `<key pair name>`
            
        * Type: RSA
            
        * Format: `.pem` (Mac, Windows 10+) or `.ppk` (Windows 7)
            
    * **Security Group:** Allow **Ports 22 (SSH) & 80 (HTTP)**
        
2. **User Data (Auto-Startup Script):**
    

```bash
#!/bin/bash
yum update -y
yum install httpd -y
systemctl enable httpd
systemctl start httpd
echo "<h1>Hello world from $(hostname -f)</h1>" > /var/www/html/index.html
```

3. **Launch the Instance**
    
    * Instance will start within **a minute**.
        
    * Once ready, note the **public IP** to access the website.
        

> **Note:** If the instance stops and starts again, the **public IP will change**, but the **private IP remains the same**.

---

## EC2 Instance Types & Use Cases

### 1\. **General Purpose** (e.g., `m5.xlarge`)

* Balanced compute, memory & networking.
    
* **Use Case:** Web servers, code repositories.
    

### 2\. **Compute Optimized** (e.g., `c5`, `c6`)

* For **compute-intensive tasks**.
    
* **Use Case:** Batch processing, machine learning, media transcoding.
    

### 3\. **Memory Optimized** (e.g., `r5`, `r6`)

* For **high-performance workloads that process large datasets**.
    
* **Use Case:** In-memory databases, BI applications.
    

### 4\. **Storage Optimized**

* **For storage-intensive applications.**
    
* **Use Case:** Online transaction processing (OLTP), NoSQL databases, distributed file systems.
    

---

## Introduction to Security Groups

* Fundamental of network security in AWS
    
* They controls how traffic is allowed in or out of EC2 instance.
    
* **Only Allow Rules (No Deny Rules).**
    
* Security groups can reference each other by IP.
    
* There are firewalls on EC2 instances.
    
* **Security Groups are regional & VPC-specific.**
    

### Security Groups Regulates:

✅ **Access to ports**  
✅ **Inbound traffic rules**  
✅ **Outbound traffic rules**

> **Tip:** Maintain a separate **Security Group for SSH access**.

### **Good to know**

* Can be attached to multiple instances
    
* Locked down to a region/VPC combination
    
* Live outside of EC2
    
* Good to maintain one separate security group for ssh access.
    
* If EC2 is not accessible (timeout), then it's an inbound traffic issue or security group issue.
    
* Outboud traffic is authorized by default & Inbound traffic is blocked by default
    

### Common Ports to Know

* **22** → SSH (Secure Shell) & SFTP (Secure File Transfer Protocal)
    
* **21** → FTP (File Transfer Protocol)
    
* **80** → HTTP (Unsecure Web Traffic)
    
* **443** → HTTPS (Secure Web Traffic)
    
* **3389** → RDP (Windows Remote Desktop)
    

### Hands-On: Testing Security Group Rules

* EC2 &gt; security groups &gt; click any security group &gt; details, inbound, outbound rules of the security group present.
    
* Deleting port 80 from the security group, the html page that was loaded will say timeout.
    
* Now add back the rule you deleted.
    

---

## SSH into EC2 Instances

### Ways to SSH:

1. **SSH (Linux & Mac)**
    
2. **Putty (Windows)**
    
3. **EC2 Instance Connect** (No need for key pair)
    

### Hands-On: EC2 Instance Connect

1. **Try connecting using EC2 Instance Connect.**
    
2. **Remove Port 22 from Security Group**.
    
3. **Observe: EC2 Instance Connect fails.**
    

---

### **EC2 Instance Roles Demo**

* In our aws instance we will have AWS CLI already installed.
    
* let's say we want to perform some task like “aws iam list-users”, we will need to configure aws cli in this instance by adding secret access key & access key ID.
    
* Now this is a very bad idea as anyone using my account may get access to these credentials.
    
* Never apply these keys in real instance & hence an alternative is IAM roles
    

### **Hands-ON**

* Go to Management Console &gt; IAM.
    
* Create a role with the policy readIAMonly.
    
* Return to the instance &gt; actions &gt; security &gt; modify IAM role.
    
* Select the role and save to attach it.
    
* Now, run “aws iam list-users” and it works. Hurrah!
    

## EC2 Purchasing Options

### 1\. **On-Demand**

* Pay per second/minute.
    
* No upfront cost.
    
* **Best for:** Short-term, unpredictable workloads.
    

### 2\. **Reserved Instances (1–3 years)**

* Up to **72% discount** vs. On-Demand.
    
* Best for **steady-state workloads** (e.g., databases).
    
* **Convertible Reserved Instances** allow flexibility in type/region.
    

### 3\. **Savings Plans (1–3 years)**

* Commitment to a **specific usage ($ amount)**.
    
* **Flexible across instance sizes & OS.**
    

### 4\. **Spot Instances (90% Discount)**

* **Best for fault-tolerant workloads** (e.g., batch jobs, data analysis).
    
* **Instances may be interrupted if demand spikes.**
    

### 5\. **Dedicated Hosts**

* **Full physical server dedicated to you.**
    
* **Best for:** Compliance & custom licensing.
    

### 6\. **Dedicated Instances**

* **Hardware dedicated to your AWS account.**
    
* **No control over instance placement.**
    

### 7\. **Capacity Reservations**

* **Reserve capacity in an AZ without time commitment.**
    
* **Best for short-term capacity needs.**
    

---

## AWS Public IP Costs

* **Free Tier:** 750 hours/month for public IPv4.
    
* **After Free Tier:** ~$3.6 per month per public IP.
    
* **Load Balancers & RDS Databases:** No free tier, public IPv4 costs apply.
    

---

Stay tuned for **Day 3**, where we’ll dive into **AWS Storage Services!** 🚀