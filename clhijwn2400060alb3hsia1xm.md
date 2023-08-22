---
title: "Setting up an Application Load Balancer with AWS EC2 🚀 ☁"
seoTitle: "Understanding Load Balancing and Creating an Application Load Balancer"
seoDescription: "Follow step-by-step instructions to create an Application Load Balancer (ALB) in AWS and add EC2 instances as target groups to it."
datePublished: Thu May 11 2023 03:09:32 GMT+0000 (Coordinated Universal Time)
cuid: clhijwn2400060alb3hsia1xm
slug: setting-up-an-application-load-balancer-with-aws-ec2
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1683774432267/5dcf2e99-d27e-42d4-ba6a-d6383d8b148a.png
tags: aws, devops, load-balancing, 90daysofdevops

---

Hi, I hope you had a great day yesterday learning about the launch template and instances in EC2. Today, we are going to dive into one of the most important concepts in EC2: Load Balancing.

Load balancing is the process of distributing incoming network traffic across multiple servers, in order to optimize resource utilization, improve performance, and ensure high availability and reliability of applications. It is a critical component of modern computing systems, particularly for large-scale and scalable applications.

Elastic Load Balancing (ELB) is a popular load balancing service provided by Amazon Web Services (AWS) that automatically distributes incoming traffic across multiple EC2 instances. ELB offers three types of load balancers to suit different types of applications and workloads:

1. Application Load Balancer (ALB) operates at layer 7 of the OSI model and is ideal for applications that require advanced routing and microservices. ALB supports features such as content-based routing, SSL termination, and HTTP/2 support.
    
2. Network Load Balancer (NLB) operates at layer 4 of the OSI model and is ideal for applications that require high throughput and low latency. NLB supports features such as static IP addresses, TCP/UDP traffic routing, and TLS termination.
    
3. Classic Load Balancer (CLB) operates at layer 4 of the OSI model and is ideal for applications that require basic load balancing features. CLB supports features such as health checks, SSL termination, and sticky sessions.
    

Overall, load balancing is a critical aspect of modern computing systems, and ELB is a powerful and flexible load balancing service that can help you optimize the performance and reliability of your applications.

***<mark>Task 1:</mark> Launch 2 EC2 instances with an Ubuntu AMI and use User Data to install the Apache Web Server.2.Modify the index.html file to include your name so that when your Apache server is hosted, it will display your name also do it for 2nd instance which include " TrainWithShubham Community is Super Aweasome :) ". Copy the public IP address of your EC2 instances. Open a web browser and paste the public IP address into the address bar.You should see a webpage displaying information about your PHP installation.***

1. Open the AWS Management Console and navigate to the EC2 service.
    
2. Click on the "Launch Instance" button to start the process of launching an EC2 instance.
    
3. In the "Step 1: Choose an Amazon Machine Image (AMI)" section, select the "Ubuntu Server" AMI.
    
4. In the "Step 2: Choose an Instance Type" section, select an instance type that meets your requirements.
    
5. In the "Step 3: Configure Instance Details" section, leave the default settings or modify them as required.
    
6. In the "Step 4: Add Storage" section, leave the default settings or modify them as required.
    
7. In the "Step 5: Add Tags" section, add any tags that you want to associate with the instance.
    
8. In the "Step 6: Configure Security Group" section, create a new security group and add rules to allow incoming traffic on port 80 (HTTP) and 22 (SSH).
    
9. In the "Step 7: Review Instance Launch" section, review the settings and click on the "Launch" button.
    
10. Select an existing key pair or create a new key pair to securely access your instance.
    
11. Click on the "Launch Instances" button to launch the instance.
    
12. Repeat the above steps to launch a second EC2 instance.
    
13. In the User Data section of each EC2 instance, enter the following script to install Apache web server:
    

```bash
#!/bin/bash
apt-get update -y
apt-get install -y apache2
```

1. Modify the index.html file in the default Apache document root directory (/var/www/html/) of each instance to include your name and the message specified in the task.
    
2. Copy the public IP address of each EC2 instance.
    
3. Open a web browser and paste the public IP address of each instance into the address bar.
    
4. You should see a webpage displaying information about your PHP installation, along with the modified index.html file.
    

***<mark>Task 2: </mark> Create an Application Load Balancer (ALB) in EC2 using the AWS Management Console. Add EC2 instances which you launch in task-1 to the ALB as target groups. Verify that the ALB is working properly by checking the health status of the target instances and testing the load balancing capabilities.***

1. Open the AWS Management Console and navigate to the EC2 service.
    
2. Click on the "Load Balancers" tab and then click on the "Create Load Balancer" button.
    
3. Select "Application Load Balancer" and click on the "Create" button.
    
4. In the "Configure Load Balancer" section, give a name to your load balancer, and select the VPC where your EC2 instances are launched.
    
5. In the "Configure Security Settings" section, select "HTTP" as the protocol and leave other settings as default.
    
6. In the "Configure Routing" section, create a new target group and specify a name and the port (80) of the EC2 instances.
    
7. In the "Register Targets" section, add the two EC2 instances that you launched in Task 1.
    
8. In the "Review" section, review the settings and click on the "Create" button.
    
9. Wait for the load balancer to be created and the target instances to be registered.
    
10. Verify that the ALB is working properly by checking the health status of the target instances and testing the load balancing capabilities. You can do this by accessing the load balancer URL in a web browser and refreshing the page multiple times to see if the requests are being distributed among the instances.
    

## <mark>Conclusion</mark>

we discussed the concept of load balancing, which involves distributing workloads across multiple servers to ensure consistent and optimal resource utilization. We also looked at Elastic Load Balancing (ELB), a service provided by Amazon Web Services (AWS) that automatically distributes incoming traffic across multiple EC2 instances. We then outlined two tasks that involved launching EC2 instances with Ubuntu AMI, installing Apache Web Server, modifying index.html files to include our name, copying the public IP address of EC2 instances, and creating an Application Load Balancer (ALB) in EC2 using the AWS Management Console. Finally, we added EC2 instances as target groups to the ALB and verified its proper functioning by checking the health status of target instances and testing the load balancing capabilities.