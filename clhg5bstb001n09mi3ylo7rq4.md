---
title: "AWS and IAM Basics☁"
seoTitle: "AWS IAM Basics: Understanding IAM Users, Groups, and Roles"
seoDescription: "Learn the basics of AWS Identity and Access Management (IAM), including IAM Users, Groups, and Roles."
datePublished: Tue May 09 2023 10:45:53 GMT+0000 (Coordinated Universal Time)
cuid: clhg5bstb001n09mi3ylo7rq4
slug: aws-and-iam-basics
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1683629035197/ead06297-5344-4449-a4bd-1d3fc5c6274b.png
tags: cloud, aws, devops, 90daysofdevops, trainwithshubham

---

When it comes to cloud computing, Amazon Web Services (AWS) is a top player, offering a wide range of services to meet the needs of businesses of all sizes. One of the key services offered by AWS is Identity and Access Management (IAM), which allows users to manage access to AWS resources securely. In this blog post, we'll take a closer look at AWS and IAM basics, and how they work together to provide a secure and scalable cloud computing environment.

## <mark>What is AWS?</mark>

AWS is a cloud computing platform that provides a wide range of services such as computing power, storage, and databases to organizations of all sizes. AWS allows businesses to operate their IT infrastructure without investing in physical hardware, software, and support staff. Instead, AWS provides a virtual environment where businesses can deploy their applications and services on-demand, and pay only for what they use.

AWS provides a wide range of services such as Amazon Elastic Compute Cloud (EC2) for computing power, Amazon Simple Storage Service (S3) for storage, and Amazon Relational Database Service (RDS) for databases. AWS also offers security services such as AWS Identity and Access Management (IAM), which allows users to manage access to AWS resources securely.

## <mark>What is IAM?</mark>

IAM is a security service provided by AWS that allows businesses to manage access to AWS resources securely. IAM allows users to create and manage users and groups, and assign permissions to access AWS resources. IAM provides a central place to manage access to AWS resources, and allows businesses to grant or deny access to resources based on specific criteria.

IAM uses a policy-based approach to control access to AWS resources. Policies are written in JSON format, and define the permissions that are granted to users or groups. IAM policies can be attached to users, groups, or AWS resources, and are evaluated when a request to access a resource is made.

## <mark>How does IAM work with AWS?</mark>

IAM works closely with other AWS services to provide a secure and scalable cloud computing environment. IAM allows businesses to manage access to AWS resources, such as EC2 instances, S3 buckets, and RDS databases. IAM policies can be used to control who can access these resources, and what actions they can perform.

IAM also integrates with AWS services such as AWS Key Management Service (KMS) and AWS CloudTrail to provide additional security and auditing capabilities. AWS KMS allows businesses to manage encryption keys securely, while AWS CloudTrail provides a record of all API calls made to AWS services, allowing businesses to track and audit activity.

## <mark>What is User Data in AWS?</mark>

User Data is a feature provided by AWS that allows users to automate the configuration of their instances. With User Data, users can specify scripts that will be executed when an instance is launched. These scripts can be used to install and configure software, set environment variables, and perform other tasks that are required to prepare the instance for use.

User Data scripts can be written in any language that is supported by the instance's operating system. The scripts are executed as soon as the instance is launched, and the output is logged to the console output of the instance. User Data scripts can be used to automate tasks such as:

* Installing and configuring software
    
* Setting environment variables
    
* Running custom scripts
    
* Mounting EBS volumes
    
* Configuring network interfaces
    
* Setting up cron jobs
    

## <mark>How does User Data work in AWS?</mark>

User Data is typically used in combination with Amazon Elastic Compute Cloud (EC2) instances. When launching an EC2 instance, users can specify User Data in the form of a script that will be executed when the instance starts up.

The User Data script can be provided in the following ways:

* Entered directly in the AWS Management Console when launching an instance.
    
* Specified in the EC2 API when launching an instance programmatically.
    
* Stored in an S3 bucket, and referenced when launching an instance.
    

Once the instance is launched, the User Data script is executed as soon as the instance starts up. The script can perform any tasks that are required to prepare the instance for use, such as installing software, configuring environment variables, and setting up network interfaces.

## <mark>Conclusion</mark>

In conclusion, AWS and IAM work together to provide a secure and scalable cloud computing environment. AWS provides a wide range of services to businesses of all sizes, while IAM allows businesses to manage access to these resources securely. By using IAM, businesses can control who can access AWS resources, and what actions they can perform. IAM also integrates with other AWS services such as KMS and CloudTrail to provide additional security and auditing capabilities. If you're considering moving your IT infrastructure to the cloud, AWS and IAM are definitely worth considering.

## <mark>Task 1. Create three Roles named: DevOps-User, Test-User and Admin.</mark>

IAM Users: IAM Users are individual users who can access AWS resources within an account. Each user has a unique set of credentials, including a username and password, that are used to authenticate them when they access AWS services. IAM Users can be granted permissions to perform specific actions on AWS resources, and their access can be controlled using IAM policies.

IAM Groups: IAM Groups are collections of IAM Users. By organizing IAM Users into groups, administrators can apply permissions to a group of users rather than to individual users. This makes it easier to manage access to AWS resources, especially when dealing with a large number of users. IAM Groups can be used to simplify the process of assigning permissions to multiple users who require similar access to AWS resources.

IAM Roles: IAM Roles are a way of granting permissions to entities outside of the AWS account, such as an EC2 instance or an application running on a user's device. IAM Roles define a set of permissions that can be assumed by entities that assume the role. This allows administrators to grant permissions to specific resources without having to share AWS credentials. IAM Roles can be used to grant permissions to third-party applications or services, or to automate tasks that require access to AWS resources.

Now, let's create the three roles named: DevOps-User, Test-User, and Admin:

1. DevOps-User: This role would be suitable for a user who needs to manage AWS resources related to development and operations. To create this role, follow these steps:
    

* Go to the AWS Management Console and navigate to the IAM service.
    
* Click on "Roles" in the left-hand menu, and then click on the "Create role" button.
    
* In the "Select type of trusted entity" section, choose "AWS service" and select "EC2" from the dropdown menu.
    
* In the "Select your use case" section, choose "EC2" and click "Next: Permissions".
    
* In the "Attach permissions policies" section, choose the policies that grant access to the resources that the DevOps-User needs. For example, you could choose the "AmazonEC2FullAccess" policy to grant full access to EC2 resources.
    
* Give the role a name (e.g. "DevOps-User") and click "Create role".
    

1. Test-User: This role would be suitable for a user who needs to manage AWS resources related to testing. To create this role, follow these steps:
    

* Go to the AWS Management Console and navigate to the IAM service.
    
* Click on "Roles" in the left-hand menu, and then click on the "Create role" button.
    
* In the "Select type of trusted entity" section, choose "AWS service" and select "EC2" from the dropdown menu.
    
* In the "Select your use case" section, choose "EC2" and click "Next: Permissions".
    
* In the "Attach permissions policies" section, choose the policies that grant access to the resources that the Test-User needs. For example, you could choose the "AmazonRDSFullAccess" policy to grant full access to RDS resources.
    
* Give the role a name (e.g. "Test-User") and click "Create role".
    

1. Admin: This role would be suitable for a user who needs full access to all AWS resources within an account. To create this role, follow these steps:
    

* Go to the AWS Management Console and navigate to the IAM service.
    
* Click on "Roles" in the left-hand menu, and then click on the "Create role" button.
    
* In the "Select type of trusted entity" section, choose "AWS service" and select "EC2" from the dropdown menu
    
* In the "Select your use case" section, choose "EC2" and click "Next: Permissions".
    
* In the "Attach permissions policies" section, choose the policies that grant full access to all AWS resources. For example, you could choose the "AdministratorAccess" policy to grant full administrative access to the AWS account.
    
* Give the role a name (e.g. "Admin") and click "Create role".
    

Once the roles have been created, you can assign them to IAM users or groups using IAM policies. For example, you could create an IAM policy that grants the DevOps-User role to a group of IAM users who need to manage development and operations resources, and then attach that policy to the group.

IAM Roles provide a flexible and secure way to manage access to AWS resources. By using roles to grant permissions, you can avoid sharing AWS credentials, which reduces the risk of unauthorized access to AWS resources. Additionally, by using IAM Groups to organize IAM Users and applying permissions to groups, you can simplify the process of managing access to AWS resources, especially when dealing with a large number of users.