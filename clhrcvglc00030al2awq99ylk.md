---
title: "Building and Scaling Web Applications on AWS: A Step-by-Step Guide"
seoTitle: "Building and Scaling Web Applications on AWS"
seoDescription: "Mastering AWS: Launching EC2, deploying web apps, scaling with Auto Scaling. Level up your cloud skills with these hands-on tasks! 💻🚀"
datePublished: Wed May 17 2023 07:02:35 GMT+0000 (Coordinated Universal Time)
cuid: clhrcvglc00030al2awq99ylk
slug: building-and-scaling-web-applications-on-aws-a-step-by-step-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1684306796197/9d3f4451-0bbd-455e-a9b5-352ff12d7a68.avif
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1684307075617/619fa03e-3ac6-4ff2-b909-6af41136e50e.avif
tags: cloud, aws, devops, apache, 90daysofdevops

---

## **Task-01: Launch an EC2 instance, install a web server, and deploy a simple web application**

1. **<mark>Launch an EC2 instance using the AWS Management Console:</mark>**
    
    * Log in to the AWS Management Console.
        
    * Open the EC2 service.
        
    * Click on "Launch Instance" to start the instance launch wizard.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684304259011/3417974b-4059-4802-bf68-dfd5a3c61cab.png align="center")
        
    * Select "Ubuntu Server 18.04 LTS" or the desired version.
        
    * ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684304336285/8a21addf-5a7e-4a9e-9a15-3249878d7f82.png align="center")
        
    * Select an instance type - Choose "t2.micro" for this example.
        
    * ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684304396340/8dd6e651-6ed4-4477-b770-4e43cc0fd75f.png align="center")
        
    * Configure instance details:
        
        * Number of instances - Set to 1.
            
        * Network - Choose the desired VPC and subnet.
            
        * Auto-assign Public IP - Set to "Enable".
            
    * Add storage as per your requirements.
        
    * Add tags (optional) for better identification of the instance.
        
    * Configure security groups:
        
        * Create a new security group or select an existing one.
            
        * Allow inbound SSH (port 22) from your IP or a specific IP range.
            
        * ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684304690686/b06e7c59-c9cc-4550-8847-64a72604f15c.png align="center")
            
    * Review your configuration and click "Launch" to start the instance.
        
    * ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684304501752/1f95e6fd-3436-4607-9275-430590748344.png align="center")
        
    * Select an existing key pair or create a new one to connect to the instance using SSH. Make sure to download the private key file (e.g., `key.pem`) and keep it secure.
        
2. **<mark>Connect to the EC2 instance using SSH:</mark>**
    
    * Use the SSH command to connect to the EC2 instance:
        
        ```bash
        ssh -i /path/to/key.pem ubuntu@<public-ip>
        ```
        
    * Replace `/path/to/key.pem` with the actual path to your private key file and `<public-ip>` with the public IP of your EC2 instance.
        
3. **<mark>Install a web server (Apache) on the EC2 instance:</mark>**
    
    * Update the package manager:
        
        ```bash
        sudo apt update
        ```
        
    * Install Apache:
        
        ```bash
        sudo apt install apache2 -y
        ```
        
    * Start the Apache service:
        
        ```bash
        sudo systemctl start apache2
        ```
        
    * Enable the Apache service to start on boot:
        
        ```bash
        sudo systemctl enable apache2
        ```
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684305096786/16fdee4d-d37d-447a-892f-06729622cf4a.png align="center")
        
4. **<mark>Deploy a simple web application:</mark>**
    
    * Copy your web application files to the appropriate directory for the web server to serve them. In this example, we'll assume your web application files are in a directory named `my-web-app`.
        
        ```bash
        sudo cp -R /path/to/my-web-app/* /var/www/html
        ```
        
        Replace `/path/to/my-web-app` with the actual path to your web application files.
        
    * Make sure the web server has permissions to access the files:
        
        ```bash
        sudo chown -R www-data:www-data /var/www/html
        ```
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684305421173/9cc44e85-4ed9-42ca-b67d-db233b18fd3f.png align="center")
        
5. **<mark>Verify the deployment:</mark>**
    
    * Open a web browser and enter the public IP of your EC2 instance.
        
    * If the Apache default page or your web application is displayed, it means the deployment was successful.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684306573432/084f10c3-3891-4881-a862-d4acafece30b.png align="center")
        

🥳🥳🥳🥳🎇🎇🎇🎇🎇🎇🎇🎇🎇🎇🎇🎇🎇🎇🎇🎇🎇🎇🎇With these steps, you will be able to launch an EC2 instance, install a web server (Apache), and deploy your web application on the EC2 instance.

You can find the complete source code for the CEO Trivia Challenge web application in the GitHub repository: [GitHub - Dhananjaykul/CEO-Trivia-Challenge](https://github.com/Dhananjaykul/CEO-Trivia-Challenge). Feel free to explore the repository for more details and to contribute to the project.

## **Task-02: Create Auto Scaling Group, Monitor Performance, and Verify with AWS CLI**

1. **<mark>Create an Auto Scaling group using the AWS Management Console:</mark>**
    
    * Log in to the AWS Management Console.
        
    * Navigate to the EC2 service.
        
    * Click on "Auto Scaling Groups" in the sidebar.
        
    * Click on "Create Auto Scaling group" to start the Auto Scaling group creation wizard.
        
    * Configure the launch template or launch configuration for the instances in the Auto Scaling group.
        
    * Set the desired capacity, minimum and maximum capacity limits, and other scaling policies based on your requirements.
        
    * Configure the network settings, load balancer (if applicable), and health check settings.
        
    * Review your configuration and create the Auto Scaling group.
        
2. **<mark>Use Amazon CloudWatch to monitor the performance of the Auto Scaling group and EC2 instances:</mark>**
    
    * Go to the CloudWatch service in the AWS Management Console.
        
    * Create alarms or configure metrics to monitor the Auto Scaling group's scaling activities, instance health, CPU utilization, or other relevant metrics.
        
    * Set up notifications to receive alerts if any issues arise with the Auto Scaling group or its instances.
        
    * Utilize CloudWatch logs and metrics to troubleshoot any performance or health-related issues.
        
3. **<mark>Use the AWS CLI to view the state of the Auto Scaling group and EC2 instances:</mark>**
    
    * Install and configure the AWS CLI on your local machine.
        
    * Open a terminal or command prompt.
        
    * Use the AWS CLI commands to view the state of the Auto Scaling group and the EC2 instances and verify that the correct number of instances are running.
        
    * To view the state of the Auto Scaling group:
        
        ```bash
        aws autoscaling describe-auto-scaling-groups --auto-scaling-group-names <auto-scaling-group-name>
        ```
        
    * To view the state of the EC2 instances in the Auto Scaling group:
        
        ```bash
        aws autoscaling describe-auto-scaling-instances --instance-ids $(aws autoscaling describe-auto-scaling-groups --auto-scaling-group-names <auto-scaling-group-name> --query "AutoScalingGroups[].Instances[].InstanceId" --output text)
        ```
        
    * Verify that the correct number of instances are running by comparing the "DesiredCapacity" and "Instances" count in the output.
        
    
    These commands use the AWS CLI to fetch information about the Auto Scaling group and EC2 instances associated with it. Replace `<auto-scaling-group-name>` with the actual name of your Auto Scaling group.
    
    By following these instructions, you will be able to create an EC2 instance, install a web server, deploy a web application, monitor the instance using CloudWatch, create an Auto Scaling group, monitor its performance, and use the AWS CLI to verify the state of the Auto Scaling group and instances.