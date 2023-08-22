---
title: "AWS IAM: Creating a User with EC2 Access and Installing Jenkins and Docker on Linux Instance"
seoTitle: "AWS IAM: How to Create Users, Groups, and Policies"
seoDescription: "Follow step-by-step instructions to set up a devops team, grant EC2 access, and more. Improve your AWS security and access management with IAM."
datePublished: Mon May 08 2023 09:28:38 GMT+0000 (Coordinated Universal Time)
cuid: clhen4m9m000a09mb30av81ce
slug: aws-iam-creating-a-user-with-ec2-access-and-installing-jenkins-and-docker-on-linux-instance
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1683538016250/2db1e6c1-44d0-4a34-871a-df3d826822be.png
tags: aws, kubernetes, devops, 90daysofdevops, trainwithshubham

---

## <mark>Introduction</mark>

Amazon Web Services (AWS) provides a wide range of services for businesses of all sizes. One of the most important services for managing your AWS resources is AWS Identity and Access Management (IAM). In this blog, we will discuss what IAM is, its benefits, and how to use it effectively.

## <mark>What is AWS IAM?</mark>

AWS IAM is a web service that enables you to manage access to AWS services and resources securely. It allows you to create and manage AWS users and groups, and control access to AWS resources by creating policies that determine what actions can be performed on those resources.

## <mark>The benefits of using AWS IAM</mark>

Using AWS IAM has several benefits for businesses, including:

1. *Secure access to AWS resources*: IAM allows you to control who can access your AWS resources, and what they can do with them. This helps you maintain the security of your AWS environment and protect sensitive data.
    
2. *Granular control*: IAM enables you to grant different levels of access to different users, depending on their roles and responsibilities. This helps you maintain a least privilege access model and reduces the risk of accidental or intentional data breaches.
    
3. *Centralized management*: IAM allows you to manage all your AWS users, groups, and policies from a single location. This helps you save time and effort, and ensures consistency across your AWS environment.
    
4. *Compliance:* IAM helps you meet compliance requirements by providing detailed audit logs and reports that show who has accessed your AWS resources, when, and what actions they performed.
    

## <mark>Task 1: Creating an IAM User with EC2 Access and Installing Jenkins and Docker</mark>

Steps and Shell Script to create an IAM user with EC2 access, launch a Linux instance through the IAM user, and install Jenkins and Docker on the instance via a single Shell Script:

### **<mark>Step 1: Create an IAM user</mark>**

1. Log in to your AWS account and navigate to the IAM console.
    
2. Click on "Users" and then click on the "Add user" button.
    
3. Enter a username of your choice and select "Programmatic access" and "AWS Management Console access" as the access type.
    
4. Click "Next" and then create a password or let AWS generate one for you.
    
5. Click "Next" again and then add the user to a group or create a new group with the appropriate permissions.
    
6. Click "Next" and then review the user details before clicking "Create user".
    
7. Take note of the Access key ID and Secret access key, as you will need them later.
    

### **<mark>Step 2: Launch a Linux instance through the IAM user</mark>**

1. Log in to the AWS Management Console using the IAM user you just created.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683605939343/1ccca990-4ef5-43b5-8c9d-d9a5b4728102.png align="center")
    
2. Navigate to the EC2 console and click on "Launch Instance".
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683606032569/7de590e0-c778-40a7-be8c-75cf218174f4.png align="center")
    
3. Choose a Linux AMI that is compatible with Jenkins and Docker, such as Amazon Linux 2.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683606105066/e5658d94-afc5-4701-89c5-1df00a43b2cf.png align="center")
    
4. Select an instance type, such as t2.micro, and configure the instance details as needed.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683606170659/5ad62cee-ad04-4a58-9f49-c3dbf9263171.png align="center")
    
5. In the "Configure Security Group" step, create a new security group and allow inbound traffic on ports 22, 80, and 8080.
    
6. Review the instance details and launch the instance.
    

### **<mark>Step 3: Install Jenkins and Docker via Shell Script</mark>**

1. Connect to your instance using SSH or another remote connection method.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683606478234/a23b0c0e-7449-49d9-b57d-4e104c88d608.png align="center")
    
2. Create a new Shell Script file with the following content:
    

```bash
#!/bin/bash

# Update package repositories
sudo yum update -y

# Install Jenkins
sudo yum install java-devel
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
sudo yum install -y jenkins

# Install Docker
sudo yum install -y docker
sudo service docker start
sudo usermod -aG docker $USER

# Start Jenkins and Docker on boot
sudo systemctl enable jenkins.service
sudo systemctl enable docker.service
```

1. Save the file as "[install-jenkins-docker.sh](http://install-jenkins-docker.sh)".
    
2. Make the file executable by running the command: `chmod +x` [`install-jenkins-docker.sh`](http://install-jenkins-docker.sh).
    
3. Run the Shell Script by running the command: `./`[`install-jenkins-docker.sh`](http://install-jenkins-docker.sh).
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683607356514/95b14219-f516-4eba-8587-28d4fe8bf1bb.png align="center")
    
4. Wait for the installation process to complete.
    
5. Access Jenkins by navigating to the instance's public IP address on port 8080 in your web browser.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684293723658/df85e343-8c16-437c-9574-333f79d2beda.png align="center")
    

That's it! 🥳🥳You have now created an IAM user with EC2 access, launched a Linux instance through the IAM user, and installed Jenkins and Docker on the instance via a single Shell Script.

## <mark>Task 2: Creating a DevOps Team of Avengers with IAM Users and Policies</mark>

Steps to create a DevOps team of avengers by creating 3 IAM users and assigning them to a DevOps group with the appropriate IAM policy:

## **<mark>Step 1: Create the IAM Users</mark>**

1. Log in to your AWS account and navigate to the IAM console.
    
2. Click on "Users" and then click on the "Add user" button.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684295815274/0aa1438f-861c-45ea-b1da-66519b286d65.png align="center")
    
3. Enter a username of your choice for the first DevOps team member and select "Programmatic access" and "AWS Management Console access" as the access type.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684296059451/83c8b197-d224-4c3e-a7fa-eeeeb5a83ba1.png align="center")
    
4. Click "Next" and then create a password or let AWS generate one for you.
    
5. Click "Next" again and then add the user to a group or create a new group called "Avengers DevOps Group".
    
6. Click "Next" and then review the user details before clicking "Create user".
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684296160780/f60135c4-4847-4928-8bff-992a52e38317.png align="center")
    
7. Repeat these steps to create two more IAM users for the other two DevOps team members.
    

## **<mark>Step 2: Create an IAM policy</mark>**

1. Navigate to the IAM console and click on "Policies".
    
2. Click on the "Create policy" button.
    
3. Choose the "JSON" tab and enter the following policy document:
    

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "ec2:*",
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": "s3:*",
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": "iam:*",
      "Resource": "*"
    }
  ]
}
```

This policy allows the DevOps team members to have full access to EC2, S3, and IAM.

1. Click "Review policy".
    
2. Enter a name and description for the policy.
    
3. Click "Create policy".
    

## **<mark>Step 3: Assign the IAM policy to the DevOps group</mark>**

1. Navigate to the IAM console and click on "Groups".
    
2. Click on the "Avengers DevOps Group" group that you created earlier.
    
3. Click on the "Permissions" tab.
    
4. Click on the "Attach Policy" button.
    
5. Search for the policy you just created and select it.
    
6. Click "Attach policy".
    

## **<mark>Step 4: Assign the IAM users to the DevOps group</mark>**

1. Navigate to the IAM console and click on "Groups".
    
2. Click on the "Avengers DevOps Group" group that you created earlier.
    
3. Click on the "Members" tab.
    
4. Click on the "Add Users to Group" button.
    
5. Select the three IAM users you created earlier.
    
6. Click "Add Users".
    

That's it! You have now created a DevOps team of avengers by creating 3 IAM users and assigning them to a DevOps group with the appropriate IAM policy. The team members will now have full access to EC2, S3, and IAM.