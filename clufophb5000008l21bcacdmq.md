---
title: "Secure & Resilient VPC Setup for Production Servers - AWS Cloud"
seoTitle: "Secure & Resilient VPC Setup for Production Servers - AWS Cloud"
seoDescription: "set up a secure and resilient VPC environment for hosting production servers on the AWS Cloud."
datePublished: Sun Mar 31 2024 15:36:48 GMT+0000 (Coordinated Universal Time)
cuid: clufophb5000008l21bcacdmq
slug: secure-resilient-vpc-setup-for-production-servers-aws-cloud
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1711899224203/53e078c2-c255-49a4-8fbd-c69cfd8137ab.png
tags: aws, security, devops

---

### Introduction:

Welcome to this comprehensive guide on setting up a secure and resilient Virtual Private Cloud (VPC) environment for hosting production servers on the AWS Cloud. In this tutorial, we'll walk you through the step-by-step process of creating a robust infrastructure that ensures both security and high availability.

### Step-by-Step Guide:

#### Step 1: Creating the VPC

1. Navigate to the AWS Management Console and click on "VPC and more"
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711885579878/d3cf0bb2-5bfe-4f20-9b5c-55f5b1eb144f.png align="center")
    
2. ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711885665062/b72c8642-5fbc-4f4d-9fbd-8062df4b7f78.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711885846257/22f5e914-1939-48ea-98bd-430dd89ed908.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711885876965/272b810e-06dd-488c-8387-d80dfac9fd57.png align="center")
    
    Select the VPC option.
    
3. Customize your VPC by selecting and deselecting resources based on your requirements.
    
4. AWS will begin creating the selected resources. Please wait until the process completes
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711885918800/9ea5952e-28a6-478c-9e7f-a6b86ad18ddc.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711885941477/ebe7b6be-934e-4b82-b63e-d00ad8d40d4b.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711886120286/92d5b63c-5e7f-44ee-b5a9-8de8c9b3d5ad.png align="center")
    

#### Step 2: Setting up Auto Scaling Group (ASG) and Launch Templates

1. Navigate to the EC2 Dashboard and click on "Auto Scaling Groups" under "Auto Scaling".
    
2. Click on "Launch Templates" and provide the necessary details:
    
    * Name and description for the launch template.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711886402369/673b89ae-9a90-409a-a1c8-951817c7ee5e.png align="center")
        
    * Instance configuration (e.g., Ubuntu t2.micro).
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711886431224/99114f3f-c88a-425a-9742-5ad3ce82f7bd.png align="center")
        
        * ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711886648409/a957204b-76be-446c-a3f2-e0084bee8d44.png align="center")
            
            ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711886830489/d8651dfd-7b75-42eb-b096-62079cbcd28d.png align="center")
            
            ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711886896005/b60311ca-483d-4350-a768-a7c85c70e0d6.png align="center")
            
            Security group allowing SSH (port 22) and HTTP (port 80) access.
            
    * Select the VPC created in Step 1.
        
3. Next, create an Auto Scaling Group with the following configurations:
    
    * Choose the launch template created earlier.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711887081021/37a2e417-d230-44d1-9d61-94f7801d1f1b.png align="center")
        
    * Select the VPC and two private subnets.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711887132596/eb767473-4020-4c46-87f0-bb221aff4240.png align="center")
        
    * Choose "No load balancer in ASG".
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711887155737/63f82768-6627-4072-b87f-18be6a39b765.png align="center")
        
    * Set desired capacity to 2, minimum to 1, and maximum to 4.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711887241786/a23de498-dd05-4cc2-863e-aa1c4ced364f.png align="center")
        
    * Configure scaling policies and notifications as needed.
        
    * Launch the Auto Scaling Group.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711887308402/0640f33e-43f0-4b10-8ce1-0d4e429b8450.png align="center")
        

#### Step 3: Deploying a Bastion Host for Secure SSH Access

1. Launch an EC2 instance named "Bastion Host" with the following settings:
    
    * AMI: Ubuntu
        
    * Instance type: t2.micro
        
    * Key pair for SSH access
        
    * Security group allowing SSH access (port 22)
        
    * Network settings within the same VPC with auto-assign public IP enabled.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711887467932/ee6fc7b3-9e2f-497b-b3e5-e1ba641320ce.png align="center")
        
2. SSH into the bastion host and from there,we will SSH into the servers in the private subnets.
    
3. Copy the .pem key from your local machine to the remote servers using SCP.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711894786480/8c9c1eb3-277d-4100-b8d4-e0d1bc465bd3.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711895182284/e47d7d43-27e5-47f3-abce-e456b8028374.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711895211022/ae6f274d-e078-4044-8cd2-5172b548a4ef.png align="center")
    
    I have succesfully logged in to my server in private subnet with ip ending with 81 (I had few issues with my previous pem key so i reconfigured the instance and created a new key).
    
4. Create an index.html file on each instance and run the command `python3 -m http.server 80` to set up a basic web server.
    
    Server B
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711896198978/849a2f7e-0165-4fbc-96ef-ddf2643af567.png align="center")
    
    Server A
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711896212828/8b139832-562b-464d-8eb6-f9dc5278e041.png align="center")
    

#### Step 4: Setting up Load Balancer

1. Navigate to the EC2 Dashboard and click on "Load Balancers" under "Load Balancing".
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711896347085/506e104a-7812-44d2-8751-ca2d73c020fb.png align="center")
    
2. Create an Application Load Balancer with the following configurations:
    
    * Name and description.
        
    * Internet-facing scheme.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711896387452/7ea3c8f8-d659-4a6e-a286-1fd155accc09.png align="center")
        
    * Select the VPC and availability zones.
        
    * Choose public subnets.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711896524606/c6cfcdad-c12a-4690-8618-d3198c10f729.png align="center")
        
    * Select the security group allowing traffic on port 80.
        
    * ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711896616777/32817da7-1927-42a5-9e33-4cc578295566.png align="center")
        
        Configure listeners and routing for HTTP (port 80).
        
    * Create a target group specifying instances and port 80.
        
3. ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711896675035/bccecf59-8edf-4550-880e-19177cf498d7.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711896822374/24b6d42a-5d5f-48c7-a395-124bba79f073.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711896839384/a5a9299e-250a-4fe8-be76-9beaf2074ed9.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711896850812/750da08f-9d10-4d0b-80f1-35d53fa27159.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711896873180/c4628b35-9b3a-4418-987e-14c1917fb769.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711896909602/1cf65ff1-e6b9-442d-be44-c92be9f263bd.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711896964313/5b9857b5-a858-4f48-8b95-82b8e2d24e82.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711897021169/21bbce51-b4b1-4cfd-9105-1d0200c281b6.png align="center")
    
    Review and create the load balancer.
    
4. Once provisioned, access the application via the load balancer's DNS name.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711898256336/abd1cdae-b920-4102-8fad-dab9230a7a9f.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711898944680/76f6d728-e4c5-4c8d-a869-194082d14047.png align="center")
    
    Load balancer evenly distributes requests, ensuring high availability and scalability.
    

### Conclusion:

Congratulations! You have successfully set up a secure and resilient VPC environment for hosting production servers on the AWS Cloud. Each component, including the VPC, Auto Scaling Group, Bastion Host, and Load Balancer, plays a critical role in ensuring the integrity, availability, and scalability of your application.