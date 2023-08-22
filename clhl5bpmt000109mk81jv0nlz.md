---
title: "S3 Programmatic Access with AWS CLI"
seoTitle: "S3 Programmatic Access with AWS-CLI: A Step-by-Step Guide"
seoDescription: "Learn how to create a bucket, upload files, launch an instance, create snapshots, and download files using AWS-CLI."
datePublished: Fri May 12 2023 22:44:39 GMT+0000 (Coordinated Universal Time)
cuid: clhl5bpmt000109mk81jv0nlz
slug: s3-programmatic-access-with-aws-cli
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1683864682972/683b1e8f-d159-4c7e-a8f5-49647e3fd6d3.png
tags: aws, devops, aws-cli, aws-s3, 90daysofdevops

---

Amazon S3 is a highly scalable, secure, and durable object storage service that can store and retrieve any amount of data from anywhere on the web. With AWS CLI, you can easily interact with S3 programmatically, and automate various tasks like creating buckets, uploading and downloading files, and more.

In this blog, we will explore how to access S3 programmatically with AWS CLI, and perform various tasks like creating a bucket, uploading a file, downloading a file, and more.

# ***Task-01: Accessing S3 from EC2 instance using AWS-CLI***

### <mark>Step 1: Launch an EC2 instance using the AWS Management Console and connect to it using Secure Shell (SSH)</mark>

1. Log in to the AWS Management Console and navigate to the EC2 Dashboard.
    
2. Click on the "Launch Instance" button and select your preferred Amazon Machine Image (AMI).
    
3. Choose your instance type, configure your instance details (such as VPC, subnet, security groups, etc.), and add storage as per your requirements.
    
4. Review your instance settings and launch the instance.
    
5. Once the instance is running, connect to it using Secure Shell (SSH) and the private key file that you created during the launch process.
    

## <mark>Step 2: Create an S3 bucket and upload a file to it using the AWS Management Console</mark>

1. Log in to the AWS Management Console and navigate to the S3 service.
    
2. Click on the "Create Bucket" button and provide a unique name for your bucket, choose your preferred region, and click on "Create".
    
3. Once your bucket is created, navigate to it and click on the "Upload" button.
    
4. Select the file that you want to upload to your S3 bucket and click on "Upload".
    
5. Wait for the file to be uploaded successfully.
    

## <mark>Step 3: Access the file from the EC2 instance using the AWS Command Line Interface (AWS CLI)</mark>

1. Connect to your EC2 instance using SSH.
    
2. Install AWS CLI by running the following command:
    
    ```bash
    sudo apt-get update
    sudo apt-get install awscli
    ```
    
3. Once AWS CLI is installed, configure it by running the following command:
    
    ```bash
    aws configure
    ```
    
4. Enter your AWS Access Key ID, AWS Secret Access Key, default region name, and default output format when prompted.
    
5. To access the file from your S3 bucket, run the following command:
    
    ```bash
    aws s3 cp s3://your-bucket-name/your-file-name /path/to/local/file
    ```
    
6. Replace "your-bucket-name" with the name of your S3 bucket and "your-file-name" with the name of the file that you uploaded to your S3 bucket.
    
7. Replace "/path/to/local/file" with the path on your EC2 instance where you want to save the file.
    

# ***Task-02: Creating a snapshot of EC2 instance, launching new EC2 instance, and downloading a file from S3 bucket using AWS-CLI***

## <mark>Step 1: Create a snapshot of the EC2 instance</mark>

1. Connect to your EC2 instance using SSH.
    
2. Stop the instance by running the following command:
    
    ```bash
    sudo poweroff
    ```
    
3. Once the instance is stopped, navigate to the EC2 Dashboard in the AWS Management Console.
    
4. Select the instance that you want to create a snapshot of and click on the "Create Image" button.
    
5. Provide a name and description for your image, and click on "Create Image".
    
6. Wait for the image creation process to complete.
    

## <mark>Step 2: Use the snapshot to launch a new EC2 instance</mark>

1. Navigate to the "AMIs" section in the EC2 Dashboard.
    
2. Select the image that you created in Step 1 and click on "Launch".
    
3. Choose your instance type, configure your instance details (such as VPC, subnet, security groups, etc.), and add storage as per your requirements.
    
4. Review your instance settings and launch the instance.
    

## <mark>Step 3: Download a file from the S3 bucket using the AWS CLI</mark>

1. Connect to your new EC2 instance using SSH.
    
2. Install AWS CLI by running the following command:
    
    ```bash
    sudo apt-get update
    sudo apt-get install awscli
    ```
    
3. Once AWS CLI is installed, configure it by running the following command:
    
    ```bash
    aws configure
    ```
    
4. Enter your AWS Access Key ID, AWS Secret Access Key, default region name, and default output format when prompted.
    
5. To download a file from your S3 bucket, run the following command:
    
    ```bash
    aws s3 cp s3://your-bucket-name/your-file-name /path/to/local/file
    ```
    
6. Replace "your-bucket-name" with the name of your S3 bucket and "your-file-name" with the name of the file that you uploaded to your S3 bucket.
    
7. Replace "/path/to/local/file" with the path on your EC2 instance where you want to save the file.
    
8. Verify that the contents of the file are the same on both EC2 instances by comparing the files using the "diff" command.
    

Congratulations!🥳🥳🥳🥳🥳 We have successfully completed the tasks of creating an S3 bucket, uploading a file to it, accessing the file from an EC2 instance using the AWS CLI, creating a snapshot of the EC2 instance, launching a new instance from the snapshot, downloading a file from the S3 bucket using the AWS CLI, and verifying the contents of the file on both EC2 instances.