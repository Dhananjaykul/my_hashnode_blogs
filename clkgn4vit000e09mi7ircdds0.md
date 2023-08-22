---
title: "Project-6: Deploying a Node.js App on AWS ECS Fargate and ECR: Step-by-Step Guide 😃"
seoTitle: "Deploy Node.js App on AWS ECS Fargate & ECR 🚀 | Step-by-Step Guide"
seoDescription: "Learn to deploy Node.js app on AWS ECS Fargate and AWS ECR with this step-by-step guide. Build Docker image, create ECR repo, and run your project on AWS"
datePublished: Mon Jul 24 2023 09:03:30 GMT+0000 (Coordinated Universal Time)
cuid: clkgn4vit000e09mi7ircdds0
slug: project-6-deploying-a-nodejs-app-on-aws-ecs-fargate-and-ecr-step-by-step-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690189158332/a42eb5fa-1e0d-414f-949d-9c8159cd6178.gif
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1690189272180/ba46fd6b-58c2-419e-a7e3-b03c95c140f0.png
tags: aws, devops, serverless, 90daysofdevops

---

## Introduction 🚀

Welcome to this step-by-step guide on deploying a Node.js application on AWS ECS Fargate and AWS ECR. In this project, we will take you through the process of setting up an ECS cluster, creating a task definition, building a Docker image, and running the project. By the end of this tutorial, you will have your Node.js app up and running on AWS, ready to be shared with the world! 🌍

## Prerequisites 📋

Before we dive into the deployment process, make sure you have the following prerequisites in place:

1. AWS Account: Create an AWS account if you don't have one already. You can sign up [here](https://aws.amazon.com/), and launch an EC2 instance and keep it ready.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690171639247/dd6c4e0d-87b8-4d62-9763-6f8841db60b7.png align="center")
    
2. Node.js App: We will use the Node.js application from [GitHub](https://github.com/Dhananjaykul/node-todo-cicd) as our example project. Clone or download the repository to get started.
    
    ```bash
    git clone https://github.com/Dhananjaykul/node-todo-cicd.git
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690171787542/db6bbec3-0198-47f4-be74-ba0e318fc2bf.png align="center")
    
3. AWS CLI: Install the AWS Command Line Interface (CLI) on your local machine to interact with AWS services. You can find installation instructions [here](https://aws.amazon.com/cli/). For Ubuntu use below command :
    
    ```bash
    sudo apt-get update -y
    sudo apt-get install awscli
    ```
    

## Step 1: Build the Docker Image 🐳

In this step, we'll build the Docker image for our Node.js application.

1. Navigate to the root directory of the cloned Node.js app repository.
    
2. Locate the `Dockerfile` in the repository. This file contains instructions for building the Docker image.
    
3. Make sure to install docker
    
    ```bash
    sudo apt-get install docker.io
    ```
    
4. Open a terminal or command prompt and run the following command to build the Docker image:
    

```bash
sudo docker build . -t node-todo-app
```

## Step 2: Setup AWS CLI and Login 🔧

To push the Docker image to AWS ECR, we need to set up the AWS CLI and log in to our AWS account.

1. Install AWS CLI: If you haven't installed the AWS CLI already, refer to the prerequisites section for the installation link.
    
2. Create IAM user with all required permissions as shown below
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690172842776/12852b24-b533-4b3c-b5a1-427061016e14.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690172865571/ade1cceb-e93c-44cc-aa50-ab33db6ee257.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690172942172/e19e6586-425b-4f44-9778-3ed683dbec33.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690172975711/3112b46b-4ecf-4614-acdd-1ab46cb7dcfd.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690173029685/606ffbe8-18df-42b1-9760-041eb3dd0fb7.png align="center")
    
    Keep Everything default and continue
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690173132413/cb3a7ef6-65b7-4e58-8e87-ce638b88472b.png align="center")
    
3. Configure AWS CLI: Run the following command and enter your AWS access key, secret key, region, and output format as prompted:
    

```bash
aws configure
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690173320673/22216e80-3204-40a7-b197-0da64c142989.png align="center")

## **Step 3: Create an ECR Repository 🏭**

Before we can push our Docker image to ECR, we need to create a repository for it.

1. In the AWS Management Console, navigate to the Elastic Container Registry (ECR) service.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690174122904/6df33221-8455-4b42-b716-ee897b5889e4.png align="center")
    
2. Click on "Create repository."
    
3. Enter a name for your repository, such as "node-app-repo"
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690174205480/3bd496dc-6b08-43e0-ad1b-b9b006b83d55.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690174227085/26ddd564-5701-4308-bcca-af858158c292.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690174245621/3ce8206f-d398-4c5f-8b59-9fdc9e48f94f.png align="center")
    
4. Configure the repository settings as needed, or leave them as default.
    
5. Click "Create repository" to create the ECR repository for your Docker image.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690174291788/e8c2000f-1417-4689-9735-a90c42ecf752.png align="center")

1. Click on "View push commands"
    
2. And Follow the on screen instructions.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690174530120/4c1d0d66-befa-4005-b22d-848070c84e75.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690180426465/e7514e08-bccf-414c-a4b7-23f91895e666.png align="center")
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690182455424/79927bfb-7dda-470f-901a-a1edaccbff4d.png align="center")

## Step 4: Setup ECS Cluster 💻

Next, let's set up an ECS cluster to run our Node.js application.

1. Sign in to your AWS Management Console.
    
2. Navigate to the ECS service.
    
3. Click on "Clusters" in the left sidebar and then click "Create Cluster."
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690182524231/7afdfdf0-8b51-49fa-bb76-144d6b619e3b.png align="center")
    
4. Choose the "Networking Only" cluster template for simplicity.
    
5. Give your cluster a name, such as "NodeAppCluster"
    
6. Configure the networking settings as per your requirements.
    
7. Review the settings and click "Create." 🌐
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690182764187/c6e3f0db-adf0-49d9-a37e-5722e314e685.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690182784930/b41478b0-c6fb-46d7-9354-1e61c6f8735b.png align="center")
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690182893280/37822abd-4f08-409e-bed0-193d4977194b.png align="center")

## Step 5: Create Task Definition with a New Role 📦

A task definition is required to specify how our containerized application should run within the ECS cluster. In this step, we will create a new task definition and set up a new IAM role to meet the specific needs of our Node.js application.

1. In the ECS service dashboard, click on "Task Definitions" in the left sidebar.
    
2. Click on "Create new Task Definition."
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690183561429/b5120e53-907c-4b40-a05f-01dc0a4607c5.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690183584104/5d4ec8f1-ee9f-4eac-856b-edb78bc27082.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690183603992/56242756-c7dd-4803-8ec5-f4ea1ffaa55d.png align="center")
    
3. Click next
    
4. Select "Fargate" as the launch type compatibility.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690183989270/c4aced4a-53cf-4275-9438-17fe10c247d5.png align="center")
    
5. Choose a task role based on your application's needs or create a new one.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690184050908/c93a661b-f145-4d0e-9785-953bf1970cd3.png align="center")
    
    * I kept rest of the things default
        
    * If you need to create a new role:
        
        * Click on the "Create new role" button.
            
        * This will redirect you to the IAM console.
            
        * Click on "Create role."
            
        * Choose the service that will use this role (ECS in this case).
            
        * Select "Allows ECS tasks to have permissions within your AWS resources."
            
        * Click "Next" until you reach the "Tags" section (you can add tags if necessary), and then click "Next" again.
            
        * Give your role a name, such as "ECS-NodeApp-Role," and provide a description if desired.
            
        * Click "Create role" to create the new IAM role.
            
6. Back in the ECS console, you should see your newly created role in the dropdown list.
    
7. Click "Add container" and fill in the container details:
    
8. Once you have configured all the container details and task requirements, click "Add" to add the container to the task definition.
    
9. Review all the settings to ensure they are correct.
    
10. Click "Create" to save the task definition.
    

Your task definition is now ready to be used to run your Node.js app on AWS ECS Fargate! 🎉

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690184318021/7c91b6b7-b1d4-425d-9b1f-d8f7a720b4bf.png align="center")

## Step 6: Run the Project ▶️

With the task definition in place, it's time to run our Node.js app on ECS Fargate.

1. In the ECS service dashboard, select the cluster you created earlier.
    
2. Click on the "Tasks" tab and then click "Run new Task."
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690184521837/3ec34e3d-fffa-45f3-9e02-b09c5d02252c.png align="center")
    
3. Choose your task definition from the dropdown.
    
4. Configure the task settings as per your requirements, such as the number of tasks to run, VPC, subnets, etc.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690184760352/555c836a-b34d-41f2-85a1-e1e7814bc070.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690184635005/5a2f97f2-c0e1-4563-baaa-76965ea9535e.png align="center")
    
5. Click "Run Task" to start running your Node.js app on ECS Fargate! 🚀
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690185248539/395042ab-b873-4642-bb09-b25ddb3138a3.png align="center")
    

## Conclusion 🎉

Congratulations! You have successfully deployed a Node.js application on AWS ECS Fargate and AWS ECR. Now, your application is accessible through the public IP or load balancer associated with the ECS Fargate tasks.

If this blog helped you, remember to share your achievements on LinkedIn, tag me and showcase your cloud computing skills!

Happy coding and sharing! 😊