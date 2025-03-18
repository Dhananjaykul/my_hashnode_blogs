---
title: "AWS Solutions Architect Associate Preparation - Day 1"
seoTitle: "AWS Solutions Architect Study Guide Day 1"
seoDescription: "Prepare for the AWS Solutions Architect Associate exam with foundational concepts, AWS infrastructure, IAM basics, security tools, and best practices"
datePublished: Sun Mar 09 2025 15:35:05 GMT+0000 (Coordinated Universal Time)
cuid: cm81sogpp000208kw4yzh1uij
slug: aws-solutions-architect-associate-preparation-day-1
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1741708858743/8007ac4f-1e3f-48f0-8960-abf083570ddd.png
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
    
    ![Diagram showing three user groups: Developer, Audit, and Ops, each associated with a policy document and connected to a user icon. An additional inline policy is shown with a red X, indicating disallowed direct assignment to a user.](https://cdn.hashnode.com/res/hashnode/image/upload/v1741708527680/a154ae60-2074-4dd5-bfcb-91570cdb86c6.png align="center")
    

### AWS IAM Policy Inheritance Best Practices

* **Policies should be assigned to groups, not individuals.**
    
* **Users inherit permissions based on group membership.**
    
* **A single user should not have policies assigned directly.**
    
* **Group-based access ensures scalability and security.**
    
* **Engineers in multiple groups inherit permissions from all assigned groups.**
    
* **This approach follows AWS best practices for IAM security.**
    

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

This hands-on exercise demonstrates how IAM policies work in AWS by assigning and revoking permissions. Follow these steps while performing the actions in your AWS account.

#### **1\. Sign in as the Root User & Create an IAM User**

* Log in to the **AWS Management Console** using the root account.
    
* Navigate to **IAM (Identity and Access Management)**.
    
* Under the **Users** section, click **Add User**.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1741709430709/a081a301-2df5-4c37-883e-a616b446bff8.png align="center")
    
* Enter a username (e.g., `test-user`).
    
* Choose **"AWS Management Console access"** and set a password.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1741709700940/5e3d43c6-ca7d-4173-b2a6-a811a818dce3.png align="center")
    
* Click **Next** without assigning permissions yet.
    
* Review the details and click **Create user**.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1741709825165/17f0eef6-0be3-4b76-b8e9-924d04b6f332.png align="center")
    

#### **2\. Assign the IAM ReadOnlyAccess Policy**

* In the IAM Dashboard, go to **Users** and select the newly created user.
    
* Click on the **Permissions** tab and choose **Add Permissions** → **Attach policies directly**.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1741709908087/05781598-d52d-49ce-b3b2-e60512fef348.png align="center")
    
* Search for **ReadOnlyAccess** and select it.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1741709963300/900bd5e9-edaf-491c-b5ee-2308615e630a.png align="center")
    
* Click **Next**, review, and then **Add permissions**.
    
* The user now has read-only access to AWS resources.
    

#### **3\. Log in as the IAM User & Test Access**

* Sign out from the root account or log in from incognitive mode.
    
* Log in to the **AWS Console** using the IAM user’s credentials.
    
* Try navigating to various AWS services (e.g., EC2, S3, IAM).
    
* The user should be able to view resources but **not modify them**.
    
* Attempt to access the **IAM Dashboard**—it should be **read-only**, meaning no changes can be made.
    

#### **4\. Remove ReadOnlyAccess Permission & Re-Test**

* Sign out from the IAM user account and log back in as the **root user**.
    
* Go to **IAM** → **Users** and select the IAM user.
    
* In the **Permissions** tab, remove the **ReadOnlyAccess** policy.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1741710382793/4321fd10-e26f-4c74-a1b9-f79b79d68060.png align="center")
    
* Save changes and sign out.
    

#### **5\. Log in Again as the IAM User & Observe the Restriction**

* Log in with the IAM user’s credentials again.
    
* Try accessing any AWS service or the IAM Dashboard.
    
* **Access should now be denied**, confirming that permissions are enforced properly
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1741710455212/2a9602a7-1656-4251-9518-a27a4e973f38.png align="center")
    
* **Add back policy to the user again, which will be useful in further demos.**
    

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

1. #### **1\. Create Access Keys for IAM User**
    
    To interact with AWS using the CLI, you need access keys. Follow these steps to generate them:
    
    * Log in to the **AWS Management Console** as an IAM user with appropriate permissions.
        
    * Navigate to **IAM (Identity and Access Management)**.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1742289227376/4cdef08d-edce-4cb5-baac-9a20d0ee8d2c.png align="center")
        
    * Go to **Security Credentials** under your IAM user settings(remember the user we created earlier).
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1742289263604/797e9b2a-9d48-4e42-aaf8-61ee38251425.png align="center")
        
    * Click **Create Access Key**.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1742289286932/965acf73-5d86-4709-86e3-545d1213ed1b.png align="center")
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1742289313146/5a44649a-d0ad-4c9b-99db-98584081957a.png align="center")
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1742289369091/b05e951c-0952-4f0f-827f-a79b10e8453d.png align="center")
        
    * Copy the **Access Key ID** and **Secret Access Key** (store them securely).
        
    
    #### **2\. Configure AWS CLI (Make sure AWS CLI is installed if not then install it first)**
    
    Now, set up AWS CLI on your local machine using the generated access keys.
    
    * Open a terminal or command prompt.
        
    * Run the following command:
        
        ```sh
        aws configure
        ```
        
    * Enter the requested details:
        
        * **AWS Access Key ID**: (Paste the copied key)
            
        * **AWS Secret Access Key**: (Paste the secret key)
            
        * **Default region**: (e.g., `us-east-1` or your preferred region)
            
        * **Default output format**: (Choose `json`, `table`, or `text`)
            
            ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1742290157664/e2fd0590-51fb-4f00-9a61-f9e14fb2a54f.png align="center")
            
    
    #### **3\. Verify IAM Users via AWS CLI**
    
    Once configured, use AWS CLI commands to list IAM users:
    
    ```sh
    aws iam list-users
    ```
    
    This command retrieves a list of IAM users in your AWS account. If configured correctly, the output will display user details.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1742290206818/25695589-bf0c-4dd8-b637-61a2e61dd36b.png align="center")
    

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