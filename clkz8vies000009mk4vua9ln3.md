---
title: "Project-10: Mounting AWS S3 Bucket On Amazon EC2 Linux Using S3FS"
seoTitle: "Step-by-Step Guide to Mounting AWS S3 Bucket on Amazon EC2 Linux Using"
seoDescription: "Learn how to mount an AWS S3 bucket on an Amazon EC2 Linux instance using the s3fs tool. This guide provides step-by-step instructions on how to set up."
datePublished: Sun Aug 06 2023 09:31:56 GMT+0000 (Coordinated Universal Time)
cuid: clkz8vies000009mk4vua9ln3
slug: project-10-mounting-aws-s3-bucket-on-amazon-ec2-linux-using-s3fs
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/wh-RPfR_3_M/upload/aaa99ab891af4dd881157d803ffef005.jpeg
tags: aws, devops, s3, 90daysofdevops, trainwithshubham

---

## **What is S3FS?**

S3FS is a FUSE filesystem that allows you to mount an Amazon S3 bucket as a local filesystem. This means that you can access your S3 bucket files as if they were stored locally on your computer.

## **Why would you want to do this?**

**<mark>There are a few reasons why you might want to mount an S3 bucket as a local filesystem. For example, you might want to:</mark>**

* Access your S3 bucket files more quickly.
    
* Use local filesystem tools to manage your S3 bucket files.
    
* Share your S3 bucket files with other users on your local network.
    

## **How do I mount an S3 bucket as a local filesystem?**

<mark>To mount an S3 bucket as a local filesystem, you will need to follow these steps:</mark>

1. Create an EC2 server.
    
2. Create an IAM user with programmatic access.
    
3. Create a credential file for S3FS.
    
4. Run the `sudo s3fs` command to mount the S3 bucket.
    
5. Verify that the S3 bucket is mounted by running the `mount` command.
    

**Here are the steps in detail:**

1. **<mark>Create an EC2 server.</mark>**
    

In the AWS console, create an EC2 instance. You can use any Linux AMI that you want.

1. **<mark>Create an IAM user with programmatic access.</mark>**
    

In the IAM console, create an IAM user with programmatic access. Give the user the following permissions:

* **AmazonS3FullAccess**
    
* **AmazonS3ReadOnlyAccess**
    

1. **<mark>Create a credential file for S3FS.</mark>**
    

Create a file called `.passwd-s3fs` in your home directory. The file should contain the following line:

```bash
AWS_ACCESS_KEY_ID:AWS_SECRET_KEY_ID
```

Replace `AWS_ACCESS_KEY_ID` and `AWS_SECRET_KEY_ID` with your IAM user's access key ID and secret access key.

1. **<mark>Run the </mark>** `sudo s3fs` <mark> command to mount the S3 bucket.</mark>
    

Run the following command to mount the S3 bucket as a local filesystem:

```bash
sudo s3fs bucketname /path/to/mount -o passwd_file=.passwd-s3fs,nonempty,rw,allow_other
```

Replace `bucketname` with the name of your S3 bucket and `/path/to/mount` with the path to the directory where you want to mount the S3 bucket.

1. **<mark>Verify that the S3 bucket is mounted by running the </mark>** `mount` <mark> command.</mark>
    

Run the following command to verify that the S3 bucket is mounted:

```bash
mount
```

You should see the S3 bucket listed in the output of the `mount` command.

**That's it! You have now successfully mounted an S3 bucket as a local filesystem.**

**<mark>Here are some additional tips:</mark>**

* You can use the `fstab` file to make the S3 bucket mount persistent after a reboot.
    
* You can use the `-o url` option to specify the endpoint for your S3 bucket.
    
* You can use the `-o use_path_request_style` option to enable path-style requests for your S3 bucket.
    

**I hope this blog post has helped you to understand how to mount an S3 bucket as a local filesystem. If you have any questions, please feel free to leave a comment below.😊**