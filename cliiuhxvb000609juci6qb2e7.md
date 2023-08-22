---
title: "🏗️ Build Your Own AWS Infrastructure with Ease using Infrastructure as Code (IaC) Techniques 🌟"
seoTitle: "🏗️ Build Your Own AWS Infrastructure with Ease using Infrastructure a"
seoDescription: "Follow step-by-step instructions to create a Virtual Private Cloud (VPC), subnets, an Internet Gateway, launch an EC2 instance, and host a  simple website"
datePublished: Mon Jun 05 2023 12:45:44 GMT+0000 (Coordinated Universal Time)
cuid: cliiuhxvb000609juci6qb2e7
slug: build-your-own-aws-infrastructure-with-ease-using-infrastructure-as-code-iac-techniques
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1685968919098/05843830-2a38-4a47-9b59-c00707b810ed.png
tags: devops, infrastructure, terraform, 90daysofdevops

---

Welcome back to your Terraform journey! In this hands-on project, we will learn how to build your own AWS infrastructure using Terraform. We will leverage Infrastructure as Code (IaC) techniques to create a Virtual Private Cloud (VPC), subnets, an Internet Gateway, launch an EC2 instance, and host a simple website.

## Prerequisites

Before we begin, make sure you have the following:

* Basic understanding of AWS services
    
* An AWS account with appropriate permissions
    
* Terraform installed on your local machine
    
* Basic knowledge of Terraform configuration files
    

## Setting Up the Project

```bash
📁 project
  📄 terraform.tf
  📄 provider.tf 
  📄 subnet.tf 
  📄 internategateway.tf 
  📄 route.tf
  📄 ec2.tf
  📄 userdata.sh
  📄 vpc.tf
```

## Task 1: Create a VPC 🌐

The first step in building our AWS infrastructure is to create a Virtual Private Cloud (VPC). Let's define the configuration for our VPC in a [`vpc.tf`](http://vpc.tf) file.Before that add these files 📁

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685952039830/64b0e9bc-29d0-4803-9abc-9551500646c1.png align="center")

Also add a `provider.tf` file:

```bash
provider "aws" {
  region = "us-east-1"
}
```

Add the following code to create a VPC with the CIDR block `10.0.0.0/16`:

```bash
resource "aws_vpc" "main" {
  cidr_block = "10.0.0.0/16"

  tags = {
    Name = "main"
  }
}
```

Save the file and execute `terraform init` and `terraform apply` in the project directory to create the VPC. Once the command execution completes, you can check the AWS Management Console for the newly created VPC named "main". 🏢

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685959107576/17521d7b-0a5d-4088-9ef2-9c3a1524a024.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685959261921/51a64ddc-8aeb-43d1-96fc-60f468e95dcf.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685959382559/cd2cc573-dc5f-4887-8d0e-def810015ffd.png align="center")

## Task 2: Create a Private Subnet 🔒

Now, let's create a private subnet within our VPC. Open a new file named [`subnet.tf`](http://subnet.tf) and add the following code:

```bash
resource "aws_subnet" "private" {
  vpc_id            = aws_vpc.main.id
  cidr_block        = "10.0.0.0/16"
  availability_zone = " us-east-1a"

  tags = {
    Name = "private"
  }
}
```

Save the file and execute `terraform apply` to create the private subnet. Verify the subnet creation in the AWS Management Console. 🚧

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685959539708/24b46592-f8e1-41be-8179-61da999798ee.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685959998817/0d284a33-90d9-4ca3-a735-735599b0f0bb.png align="center")

## Task 3: Create a Public Subnet 🌐

Similarly, let's create a public subnet within our VPC. Open the [`subnet.tf`](http://subnet.tf) file again and add the following code:

```bash
resource "aws_subnet" "public" {
  vpc_id            = aws_vpc.main.id
  cidr_block        = "10.0.16.0/20"
  availability_zone = "us-east-1a"

  tags = {
    Name = "public"
  }
}
```

Save the file and execute `terraform apply` to create the public subnet. Verify the subnet creation in the AWS Management Console. �

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685961271593/27ad0846-e34e-407f-b5f2-18552062bd39.png align="center")

## Task 4: Create an Internet Gateway 🌐

To provide internet access to our VPC, we need to create an Internet Gateway (IGW). Create a new file named [`internetgateway.tf`](http://internetgateway.tf) and add the following code:

```bash
resource "aws_internet_gateway" "gw" {
  vpc_id = aws_vpc.main.id

  tags = {
    Name = "internet-gateway"
  }
}
```

Save the file and execute `terraform apply` to create the Internet Gateway. Verify the Internet Gateway creation in the AWS Management Console. 🌐

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685961419498/cb840521-7e63-44d1-b48b-61212f3730a8.png align="center")

## Task 5: Create a Route Table 🚦

Now, let's create a route table for our public subnet and associate it with the subnet. Open a new file named [`routetable.tf`](http://routetable.tf) and add the following code:

```bash
resource "aws_route_table" "public" {
  vpc_id = aws_vpc.main.id

  route {
    cidr_block = "0.0.0.0/0"
    gateway_id = aws_internet_gateway.gw.id
  }

  tags = {
    Name = "public"
  }
}

resource "aws_route_table_association" "public_subnet_association" {
  subnet_id      = aws_subnet.public.id
  route_table_id = aws_route_table.public.id
}
```

Save the file and execute `terraform apply` to create the route table and associate it with the public subnet. Verify the route table and subnet association in the AWS Management Console. 🚧

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685961584918/7fe4a0bf-d200-4554-af9c-61c138b89bfe.png align="center")

## Task 6: Create a Security Group 🔒

For our EC2 instance, we need to create a security group that allows SSH access and HTTP access from anywhere. Create a new file named [`securitygroup.tf`](http://securitygroup.tf) and add the following code:

```bash
resource "aws_security_group" "web_server" {
  name        = "web-server-sg"
  description = "Allow SSH and HTTP access from anywhere"

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

Save the file and execute `terraform apply` to create the security group. Verify the security group and its rules in the AWS Management Console. 🔒

## Task 7: Create an Elastic IP 🌐

To associate a static IP with our EC2 instance, we need to create an Elastic IP. Create a new file named [`elasticip.tf`](http://elasticip.tf) and add the following code:

```bash
resource "aws_eip" "ip" {
  instance = aws_instance.example.id
  vpc      = true

  tags = {
    Name = "elastic-ip"
  }
}
```

Save the file and execute `terraform apply` to create the Elastic IP. Verify the Elastic IP creation in the AWS Management Console. 🌐

## Task 8: Create User Data to Install Apache 🖥️

To host a simple website on our EC2 instance, we need to install Apache. We can use user data in Terraform to run a shell script during instance launch. Create a new file named [`userdata.sh`](http://userdata.sh) and add the following code:

```bash
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
    <p>I am going to be a DevOps Pro</p>
</body>
</html>" > /var/www/html/index.html
sudo systemctl restart apache2
```

Save the file and make sure it is in the same directory as your Terraform configuration files.

## Task 9: Create an EC2 Instance 💻

Finally, let's create our EC2 instance in the public subnet with the required configurations. Open the [`ec2.tf`](http://ec2.tf) file and add the following code :

```bash
resource "aws_instance" "example" {
  ami           = "ami-0557a15b87f6559cf"
  instance_type = "t2.micro"
  key_name      = "instance"
  subnet_id     = aws_subnet.public.id
 
  security_groups = [
    aws_security_group.web_server.id
  ]

  user_data = filebase64("userdata.sh")

  tags = {
    Name = "web-server"
  }
}
```

Later I updated few files in One:

```bash
#ec2.tf
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

resource "aws_instance" "example" {
  ami           = "ami-053b0d53c279acc90"
  instance_type = "t2.micro"
  key_name      = "myself"
  subnet_id     = aws_subnet.public.id
  associate_public_ip_address = true
  security_groups = [
    aws_security_group.web_server.id
  ]

  user_data = filebase64("userdata.sh")

  tags = {
    Name = "web-server"
  }
}
```

Save the file and execute `terraform apply` to create the EC2 instance. Once the instance is up and running, open the website URL in a browser to verify that the website is successfully hosted.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685967219927/4a823435-c328-4970-a474-6f0c6e2ab17e.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685968297430/f6447623-571d-4605-bcc5-4c4f181f66da.png align="center")

Congratulations! You have successfully built your AWS infrastructure using Terraform. 🎉

## Code Availability🌟

You can access the complete code for this project on GitHub. The code is available in the following GitHub repository: \[[link here](https://github.com/Dhananjaykul/-Build-Your-Own-AWS-Infrastructure-with-Ease-using-Infrastructure-as-Code-IaC-Techniques-)\]

Feel free to explore the code, make modifications, and contribute to the project.

## Conclusion 🌟

In this blog post, we learned how to use Infrastructure as Code (IaC) techniques with Terraform to build our own AWS infrastructure. We created a VPC, subnets, an internet gateway, a route table, a security group, and launched an EC2 instance with a web server running on it. By automating infrastructure deployment, we can save time, ensure consistency, and easily manage our infrastructure.

Stay tuned for more exciting Terraform tutorials and happy coding! 🚀👩‍💻👨‍💻