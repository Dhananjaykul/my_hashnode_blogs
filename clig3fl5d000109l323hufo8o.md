---
title: "🌟 Unleashing the Power of Terraform Resources 🚀"
seoTitle: "🌟 Unleashing the Power of Terraform Resources 🚀"
seoDescription: "In the world of Terraform, a resource represents a crucial component of your infrastructure. It could be anything from a physical server to a virtual machin"
datePublished: Sat Jun 03 2023 14:32:32 GMT+0000 (Coordinated Universal Time)
cuid: clig3fl5d000109l323hufo8o
slug: unleashing-the-power-of-terraform-resources
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1685753249553/b3020114-74f6-4a0e-b71e-95fdf3ac7d63.png
tags: devops, terraform, infrastructure-as-code, 90daysofdevops

---

Welcome back to our Terraform journey! In the previous blog post, we learned about Terraform blocks and resources. Today, we will take a deeper dive into working with Terraform resources and continue building our infrastructure. So, grab your cup of ☕ and let's get started!

## Understanding Terraform Resources 📚

In the world of Terraform, a resource represents a crucial component of your infrastructure. It could be anything from a physical server to a virtual machine, a DNS record, or even an S3 bucket. These resources come with their unique set of attributes that define their properties and behaviors. For instance, a virtual machine resource might have attributes like size and location, while a DNS record resource could have attributes like domain name.

To define a resource in Terraform, you need to specify the resource type, a unique name, and the attributes that characterize it. In your Terraform configuration, you'll utilize the resource block to define these resources and bring your infrastructure to life.

## Task 1: Create a security group 👥

To kick things off, we need to create a security group to allow traffic to our EC2 instance. Here's a step-by-step guide:

1. Open your [`main.tf`](http://main.tf) file and add the following code snippet to create a security group:
    

```bash
resource "aws_security_group" "web_server" {
  name_prefix = "web-server-sg"

  ingress {
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685714235013/1e146f17-15c1-424b-aeb2-76aaba6a945d.png align="center")

1. Run `terraform init` in your terminal to initialize the Terraform project.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685714848398/9221990e-8845-4977-9e78-06148447a75b.png align="center")
    
2. Execute `terraform apply` to create the security group.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685714928840/37d6ec6c-c1da-4a15-80a1-4ee9d7a46906.png align="center")
    

## Task 2: Create an EC2 instance 💻

Now, let's move on to creating an EC2 instance using Terraform. Follow these steps:

1. Open your [`main.tf`](http://main.tf) file and add the following code snippet to create an EC2 instance:
    

```bash

terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.0"
    }
  }
}

// main.tf
provider "aws" {
  region = "us-east-1"
}

resource "aws_security_group" "web_server" {
  name_prefix = "web-server-sg"
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
  
   ingress { 
     from_port   = 443 
     to_port     = 443 
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


resource "aws_instance" "web_server" {
  ami           = "ami-053b0d53c279acc90"
  instance_type = "t2.micro"
  key_name      = "myself"
  security_groups = [
    aws_security_group.web_server.name
  ]
   tags = {
    Name = "web_server"
  }

 
user_data = <<-EOF
#!/bin/bash
sudo apt update -y
sudo apt install python3 -y
 sudo apt-get install -y apache2
 sudo systemctl start apache2     
sudo systemctl enable apache2
sudo apt 
touch /home/ubuntu/index.html
echo "<html><body><h1>Welcome to my website!</h1></body></html>" > /home/ubuntu/index.html

nohup python3 -m SimpleHTTPServer 80 &
sudo chmod -R 755 /var/www/html
EOF

 provisioner "file" {
    source      = "/home/ubuntu/index.html"
    destination = "/var/www/html/index.html"
  }
}
```

Note: Replace the `ami` and `key_name` values with your own. You can find a list of available AMIs in the AWS documentation.

1. Run `terraform apply` to create the EC2 instance.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685753566663/dc067405-529a-488a-8c84-d0ab958565f5.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685753602817/83253d27-e19f-4956-a8d1-8f0633bb45dc.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685753661048/ad09c102-a080-46d7-8681-7611ee450297.png align="center")

## Task 3: Access your website 🌐

With the EC2 instance up and running, it's time to access the website hosted on it. Follow these simple steps:

1. Open your favorite web browser and enter the public IP address of your EC2 instance.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684263761139/287492ab-bdec-4b70-8b06-6d1950dbecc1.png?auto=compress,format&format=webp align="left")
    
2. Voilà! You should see your website's homepage with the message "Welcome to my website!" displayed prominently.
    

Congratulations! You have successfully created a security group, launched an EC2 instance, and accessed your website using Terraform. 🎉

In today's blog post, we explored the power of Terraform resources and witnessed firsthand how they shape our infrastructure. Stay tuned for the next article, where we'll delve into managing dependencies between resources and further enhance our infrastructure. Until then, happy coding! 💻✨