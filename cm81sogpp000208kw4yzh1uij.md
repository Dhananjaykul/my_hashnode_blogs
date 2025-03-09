---
title: "AWS Solutions Architect Associate Preparation - Day 1"
seoTitle: "AWS Solutions Architect Study Guide Day 1"
seoDescription: "Prepare for the AWS Solutions Architect Associate exam with foundational concepts, AWS infrastructure, IAM basics, security tools, and best practices"
datePublished: Sun Mar 09 2025 15:35:05 GMT+0000 (Coordinated Universal Time)
cuid: cm81sogpp000208kw4yzh1uij
slug: aws-solutions-architect-associate-preparation-day-1
tags: aws, solutionarchitect

---

## Introduction

These are my notes while preparing for the **AWS Solutions Architect Associate-Level exam**. I'll cover foundational concepts, hands-on activities, and best practices. Let's start with the first topic: **AWS History and Global Infrastructure.**

---

## AWS History

* AWS was launched in **2002**, focusing on infrastructure as a core strength.
    
* In **2004**, AWS introduced **SQS (Simple Queue Service)** for external use.
    
* Many top organizations, including **Netflix, NASA, and Amazon**, leverage AWS services.
    
* AWS generated **$90 billion in revenue in 2023**.
    
* **Use case:** AWS enables the development of scalable applications and websites.
    

---

## AWS Global Infrastructure

AWS operates a vast global infrastructure, ensuring redundancy, scalability, and low latency.

### AWS Regions

AWS regions are globally distributed and consist of clusters of data centers. Most AWS services are region-specific.

#### **How to Decide Where to Launch Your AWS Services?**

Factors to consider:

1. **Compliance:** Government regulations on data storage.
    
2. **Proximity:** Reduce latency by selecting the closest region (e.g., users in India should use the India region).
    
3. **Availability of Services:** Some AWS services are available only in specific regions.
    
4. **Pricing:** Costs vary based on the selected region.
    

### **AWS Availability Zones (AZs)**

* Each AWS region consists of multiple **Availability Zones** (AZs).
    
* An AZ includes **one or more discrete data centers** with redundant power, networking, and connectivity.
    
* AZs are **isolated from disasters** and connected via **high-bandwidth, low-latency networking**.
    

### **AWS Points of Presence (Edge Locations)**

* AWS has **400+ Points of Presence** in **90+ cities across 40+ countries**.
    
* Ensures content is delivered to users with the lowest possible latency.
    

### **AWS Global vs. Region-Specific Services**

#### **Global Services:**

* IAM (Identity & Access Management)
    
* Route 53 (DNS service)
    
* CloudFront (CDN service)
    
* WAF (Web Application Firewall)
    

#### **Region-Specific Services:**

* Amazon EC2 (Infrastructure as a Service - IaaS)
    
* Elastic Beanstalk (Platform as a Service - PaaS)
    
* AWS Lambda (Function as a Service - FaaS)
    
* Amazon Rekognition (Software as a Service - SaaS)
    

---

## Hands-On: Creating an AWS Account

1. Sign up on [AWS Console](https://aws.amazon.com/)
    
2. In the **AWS search bar**, search for any service.
    
3. The **top right corner** will display the selected region.
    
    * **EC2:** Shows the selected region.
        
    * **Route 53:** Appears as a global service.
        

---

## IAM (Identity & Access Management) & AWS CLI

### IAM Basics

* **IAM is a global service** that manages identities and permissions.
    
* The **root account** is created by default but should never be used for daily operations.
    
* **IAM Users:** Represent individuals in an organization and can belong to one or more **IAM Groups**.
    
* **IAM Permissions:** Managed through **policies** (JSON-based documents).
    

### **IAM Hands-On: Users & Groups**

* IAM **Policy Inheritance**: Users can belong to multiple groups (e.g., **Developers, Operations, Audit Team**).
    
* **IAM Policy Structure**:
    

```json
{
  "Version": "2012-10-17",
  "Id": "ExamplePolicy",
  "Statement": [
    {
      "Sid": "AllowReadAccess",
      "Effect": "Allow",
      "Principal": { "AWS": "<User ARN>" },
      "Action": "iam:ListUsers",
      "Resource": "*"
    }
  ]
}
```

#### **Hands-On: IAM Policy Testing**

1. Sign in as the **root user** and create an IAM user.
    
2. Assign the **IAM ReadOnlyAccess** policy.
    
3. Log in as the IAM user and try accessing the **IAM Dashboard**.
    
4. Remove the **ReadOnlyAccess** permission and test access again.
    
5. Observe that access is revoked.
    

---

## Securing AWS Accounts

### **1\. Password Policy**

* Set strong passwords.
    
* Define a minimum password length.
    
* Allow password changes.
    
* Set password expiration.
    
* Prevent password reuse.
    

### **2\. Multi-Factor Authentication (MFA)**

* **Password + MFA = Secure Login**
    
* **MFA Device Options:**
    
    * Virtual MFA apps (Google Authenticator, Authy)
        
    * Hardware security keys
        
    * SMS-based MFA
        

#### **Setting Up MFA in AWS**

1. Navigate to **IAM &gt; Security Credentials**.
    
2. Enable **MFA** and link it to an authentication device.
    
3. Test login with **MFA enabled**.
    

---

## Accessing AWS Services

Three ways to access AWS:

1. **AWS Management Console**: Web-based UI, login via password & MFA.
    
2. **AWS CLI**: Command-line access using **Access Key ID & Secret Key**.
    
3. **AWS SDK**: Programmatic access using APIs (Supports Python, Java, Node.js, etc.).
    

### **AWS CLI Setup on Windows**

1. **Download AWS CLI** [from AWS](https://aws.amazon.com/cli/)
    
2. **Verify installation**: Open CLI and run:
    
    ```sh
    aws --version
    ```
    
3. **Configure AWS CLI**:
    
    ```sh
    aws configure
    ```
    
4. Enter **Access Key ID** and **Secret Access Key**.
    
5. Test with:
    
    ```sh
    aws iam list-users
    ```
    

#### **Hands-On: AWS CLI**

1. **Create Access Keys**: IAM &gt; Security Credentials &gt; Create Access Key.
    
2. **Use AWS CLI**:
    
    ```sh
    aws configure
    aws iam list-users
    ```
    

---

## CloudShell: AWS Terminal

* **AWS CloudShell** is a browser-based terminal (free to use).
    
* Not available in all AWS regions.
    
* Can upload/download files, run AWS CLI commands.
    

#### **Hands-On: CloudShell**

1. Open **CloudShell** from AWS Console.
    
2. Check installed AWS CLI version:
    
    ```sh
    aws --version
    ```
    
3. List IAM users:
    
    ```sh
    aws iam list-users
    ```
    

---

## IAM Roles for AWS Services

Some AWS services need roles to perform actions on your behalf.

* **Common IAM Roles:**
    
    * EC2 Instance Role
        
    * Lambda Function Role
        
    * Roles for CloudFormation
        

#### **Hands-On: Creating an IAM Role**

1. Navigate to **IAM &gt; Roles &gt; Create Role**.
    
2. Select **AWS Service &gt; Use Case = EC2**.
    
3. Attach **IAM ReadOnlyAccess Policy**.
    
4. Name the role and create it.
    

---

## IAM Security Tools

### **IAM Credentials Report (Account Level)**

* Lists all users and credential status.
    
* Download from **IAM &gt; Credentials Report**.
    

### **IAM Access Advisor (User Level)**

* Shows last accessed AWS services for each user.
    
* Helps refine IAM permissions.
    

---

## IAM Best Practices

✅ Avoid using the root account. ✅ One physical user = One IAM user. ✅ Assign users to groups and manage permissions at the group level. ✅ Implement **strong password policies & MFA**. ✅ Use **IAM Roles** for AWS services. ✅ Audit permissions using **IAM Credentials Report & IAM Access Advisor**. ✅ **Never share** IAM access keys.

---

Stay tuned for **Day 2**, where we’ll dive into **EC2 & Storage Services!** 🚀