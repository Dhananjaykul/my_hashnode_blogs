---
title: "Scaling with Terraform 🚀"
seoTitle: "Scaling with Terraform 🚀"
seoDescription: "Terraform makes it easy to scale your infrastructure by providing a declarative way to define your resources."
datePublished: Wed Jun 07 2023 13:56:43 GMT+0000 (Coordinated Universal Time)
cuid: clilrwx46000909l55uvlhf0a
slug: scaling-with-terraform
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1686138616724/0cfa6a29-f302-445c-984c-971c977e2bfd.webp
tags: aws, devops, terraform, 90daysofdevops, trainwithshubham

---

Yesterday, we explored how to create an AWS S3 Bucket with Terraform. Today, let's dive into the exciting world of scaling our infrastructure using Terraform.

## Understanding Scaling 📈

Scaling is the process of adding or removing resources to match the changing demands of your application. As your application grows, you will need to add more resources to handle the increased load. And as the load decreases, you can remove the extra resources to save costs.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686145292344/5b862070-fa6b-4554-8f51-8395afb943b7.png align="center")

Terraform makes it easy to scale your infrastructure by providing a declarative way to define your resources. You can define the number of resources you need, and Terraform will automatically create or destroy the resources as needed.

## Pre-requisites 🔑

Before we start, let's set up a few things:

1. Create a [`terraform.tf`](http://terraform.tf) file to declare the providers required for the system.
    
    ```json
    terraform {
      required_providers {
        aws = {
          source  = "hashicorp/aws"
          version = "~> 4.0"
        }
      }
    }
    ```
    
2. Create a [`provider.tf`](http://provider.tf) file to specify the region.
    
    ```json
    # Configure the AWS Provider
    provider "aws" {
      region = "us-east-1"
    }
    ```
    
3. Create a [`userdata.sh`](http://userdata.sh) file with the following content:
    
    ```json
    #!/bin/bash
    sudo apt-get update -y
    sudo apt-get install -y apache2
    sudo systemctl start apache2
    sudo systemctl enable apache2
    echo "<!DOCTYPE html>
    <html>
    <head>
        <title>Introduction</title>
        <style>
            body {
                background-color: #d8e2dc;
                font-family: Arial, sans-serif;
                color: #3c415e;
                text-align: center;
                padding: 50px;
            }
            h1 {
                font-size: 3em;
                margin-bottom: 20px;
                text-shadow: 0 2px 2px rgba(0,0,0,0.1);
            }
            p {
                font-size: 1.5em;
                line-height: 1.5;
                margin-bottom: 30px;
            }
        </style>
    </head>
    <body>
        <h1>This is Dhananjay.</h1>
        <p>I am going to be a Terraform Pro</p>
    </body>
    </html>" > /var/www/html/index.html
    sudo systemctl restart apache2
    ```
    
4. Create a [`vpc.tf`](http://vpc.tf) file to set up the VPC for our instances.
    
    ```json
    # Create a VPC
    resource "aws_vpc" "main" {
      cidr_block = "10.0.0.0/16"
    
      tags = {
        Name = "main"
      }
    }
    ```
    
5. Define two public subnets in a [`subnet.tf`](http://subnet.tf) file. We will later use these subnets for multi-subnet initialization in our auto-scaling group.
    
    ```json
    #subnet.tf
    resource "aws_subnet" "public_subnet_1a" {
      vpc_id            = aws_vpc.main.id
      cidr_block        = "10.0.32.0/20"
      availability_zone = "us-east-1a"
    
      tags = {
        Name = "public subnet 1"
      }
    }
    
    resource "aws_subnet" "public_subnet_1b" {
      vpc_id            = aws_vpc.main.id
      cidr_block        = "10.0.16.0/20"
      availability_zone = "us-east-1a"
    
      tags = {
        Name = "public subnet 2"
      }
    }
    ```
    
6. Create an [`internetgateway.tf`](http://internetgateway.tf) file to configure the internet gateway.
    
    ```json
    resource "aws_internet_gateway" "gw" {
      vpc_id = aws_vpc.main.id
    
      tags = {
        Name = "internet-gateway"
      }
    }
    ```
    
7. Set up routing configurations in a [`routetable.tf`](http://routetable.tf) file.
    
    ```json
    resource "aws_route_table" "route_table" {
      vpc_id = aws_vpc.main.id
    
      route {
        cidr_block = "0.0.0.0/0"
        gateway_id = aws_internet_gateway.gw.id
      }
    
      tags = {
        Name = "route_table"
      }
    }
    
    resource "aws_route_table_association" "public_subnet_association_1a" {
      subnet_id      = aws_subnet.public_subnet_1a.id
      route_table_id = aws_route_table.route_table.id
    }
    resource "aws_route_table_association" "public_subnet_association_1b" {
      subnet_id      = aws_subnet.public_subnet_1b.id
      route_table_id = aws_route_table.route_table.id
    }
    ```
    
8. Create a security group in a [`securitygroup.tf`](http://securitygroup.tf) file to allow SSH, HTTP, and egress traffic to the instances.
    
    ```json
    #securitygroup
    resource "aws_security_group" "web_server" {
      name        = "web-server-sg"
      description = "Allow SSH and HTTP access from anywhere"
      vpc_id = aws_vpc.main.id
      ingress {
        from_port   = 22
        to_port     = 22
        protocol    = "tcp"
        cidr_blocks = ["0.0.0.0/0"]
      }
    
      ingress {
        from_port   = 80
        to_port     = 80
        protocol    = "tcp"
        cidr_blocks = ["0.0.0.0/0"]
      }
    
      egress {
        from_port   = 0
        to_port     = 0
        protocol    = "-1"
        cidr_blocks = ["0.0.0.0/0"]
      }
      }
    ```
    

## Task 1: Create an Auto Scaling Group 🏢

Auto Scaling Groups automatically add or remove EC2 instances based on the current demand. Follow these steps to create an Auto Scaling Group:

1. Create [`main.tf`](http://autoscaling.tf) file that contains the EC2 configuration along with auto-scaling configurations.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686199720731/b0f76aab-0ddc-4f86-aaf3-603aecdf0a6a.png align="center")
    
2. Run `terraform apply` to create the Auto Scaling Group and all its dependent resources, as mentioned in the pre-requisites.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686145009670/0dba7439-a7a0-411e-a278-7ab8642ecfc1.png align="center")
    
3. Let's navigate to the AWS Management Console to check the created Auto Scaling Group. Since we set the desired capacity to 2 in the auto-scaling Terraform configuration, there should be two instances created.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686145153638/ebb6c664-bb83-4982-a641-c4112e7272d5.png align="center")
    

## Task 2: Test Scaling 🧪

1. Go to the AWS Management Console and select the Auto Scaling Groups service.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686145418368/8b6c37aa-e5f5-4216-a00e-5ebb71897bb2.png align="center")
    
2. Choose the Auto Scaling Group you just created and click on the "Edit" button.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686145477933/678dffb6-6565-445b-8c24-29240356b589.png align="center")
    
3. Increase the "Desired Capacity" to 3 and click on the "Save" button.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686145559573/6a08aa8f-0be5-4f78-bbe3-b97da2a9ee4c.png align="center")
    
4. Wait a few minutes for the new instances to be launched.
    
5. Go to the EC2 Instances service and verify that the new instances have been successfully launched.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686145759720/0bbb65eb-d5db-4c5b-b47d-78d8f6bd91a0.png align="center")
    
6. Decrease the "Desired Capacity" to 1 and wait for a few minutes for the extra instances to be terminated.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686145803676/75950f71-f51d-4473-a53b-1369c9ccd7ea.png align="center")
    
7. Check the EC2 Instances service again to ensure that the additional instances have been terminated.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686145867313/34310dff-34f1-4220-989a-1766b9ed2b36.png align="center")
    

That's it! Congratulations! 🎊🎉 You have successfully scaled your infrastructure using Terraform.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686146031095/4bafe4ec-b62c-4ed5-8a6a-ba1038d6ef1b.png align="center")

Happy Learning! 😊