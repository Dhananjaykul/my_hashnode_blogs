---
title: "Project-8: 🚀 Deploying 2048 Game to AWS Elastic Beanstalk with GitHub Actions 🎮"
seoTitle: "Deploying a dockerize application on Elastic BeanStalk using Githuh Ac"
seoDescription: "learn how to deploy the popular 2048 game to AWS Elastic Beanstalk using GitHub Actions!"
datePublished: Wed Aug 02 2023 09:03:05 GMT+0000 (Coordinated Universal Time)
cuid: clkti30s5001708l6bedggxdo
slug: project-8-deploying-2048-game-to-aws-elastic-beanstalk-with-github-actions
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690966758636/663b5a96-b4fc-4cfc-bf65-ade9557cea14.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1690966816758/2ecc88cc-9de7-44ab-9c6f-e007050ac704.png
tags: devops, hashnode, 90daysofdevops, wemakedevs

---

## **Introduction 🌟**

Welcome to this step-by-step tutorial where we'll learn how to deploy the popular 2048 game to AWS Elastic Beanstalk using GitHub Actions! 🚀 AWS Elastic Beanstalk simplifies the deployment and management of web applications, while GitHub Actions automates the deployment process with Continuous Integration and Continuous Deployment (CICD) workflows. Let's get ready for an exciting journey! 😃

## Why Use AWS Elastic Beanstalk and GitHub Actions? 🤔

#### **AWS Elastic Beanstalk 🌐**

AWS Elastic Beanstalk is a fully managed Platform-as-a-Service (PaaS) offering from Amazon Web Services (AWS). It simplifies the process of deploying and scaling applications by automatically managing the underlying infrastructure, such as EC2 instances, load balancers, and databases. Elastic Beanstalk supports multiple programming languages and platforms, making it suitable for various types of applications.

<mark>Benefits of using AWS Elastic Beanstalk include:</mark>

* **Simplicity:** *Elastic Beanstalk abstracts away the complexities of infrastructure management, allowing developers to focus on writing code and deploying applications with ease.*
    
* **Automatic Scaling:** *Elastic Beanstalk can automatically scale your application based on traffic or performance metrics, ensuring that it can handle varying workloads efficiently.*
    
* **Integrated Monitoring:** *Elastic Beanstalk provides built-in monitoring capabilities to help you track the health and performance of your applications.*
    
* **Platform Choice:** *With support for multiple platforms, Elastic Beanstalk accommodates developers working with different programming languages and frameworks.*
    

#### **GitHub Actions ⚙️**

GitHub Actions is a powerful workflow automation tool integrated with GitHub repositories. It allows developers to define custom workflows, including building, testing, and deploying applications. GitHub Actions provides a seamless CI/CD solution for software development projects, enabling teams to automate repetitive tasks and improve collaboration.

<mark>Benefits of using GitHub Actions include:</mark>

* **Continuous Integration:** *GitHub Actions allows developers to automatically build and test code changes whenever they are pushed to the repository, promoting early detection of issues.*
    
* **Continuous Deployment:** *With GitHub Actions, you can automate the deployment process to different environments, such as staging and production, based on predefined conditions.*
    
* **Flexibility:** *GitHub Actions supports custom workflows with various triggers, allowing you to define complex build and deployment pipelines.*
    
* **Integration with GitHub:** *Being integrated directly into GitHub, GitHub Actions provides a familiar interface for developers to manage their workflows and monitor their progress.*
    

## **Prerequisites ✅**

Before we dive into the deployment process, make sure you have the following prerequisites:

* An AWS account with Elastic Beanstalk access.
    
* A GitHub repository with the 2048 game application code. (We have this docker file where there is no need for code, the docker file explicitly pulls the code and creates a container out of it. )
    
* Basic knowledge of Git, Docker, and AWS services.
    
* Install Docker and docker-compose on your EC2 instance:
    
    ```bash
    sudo apt update
    sudo apt install -y docker.io
    sudo usermod -aG docker $USER
    sudo systemctl enable docker
    sudo systemctl restart docker
    sudo apt install -y docker-compose
    ```
    

## **Step 1: 📦 Setting up the Dockerfile 🐳**

To begin, we'll create a Dockerfile that packages our 2048 game application. 🎁 (Make sure you have docker and docker-compose installed 🐳)The Dockerfile will specify the necessary instructions to build a Docker container for our game. Follow these steps:

1. Create a new file named `Dockerfile` in the root of your 2048 game repository.
    
2. Copy and paste the following code into your Dockerfile:
    

```Dockerfile
FROM ubuntu:22.04

RUN apt-get update && apt-get install -y nginx zip curl
RUN sed -i '/daemon off;/d' /etc/nginx/nginx.conf
RUN echo "daemon off;" >> /etc/nginx/nginx.conf
RUN curl -o /var/www/html/master.zip -L https://github.com/gabrielecirulli/2048/archive/master.zip
RUN cd /var/www/html/ && unzip master.zip && mv 2048-master/* . && rm -rf 2048-master master.zip

EXPOSE 80
CMD ["nginx", "-c", "/etc/nginx/nginx.conf"]
```

## **Step 2: 🐳 Developing 2048 Application inside a Docker Container 💻**

Now, let's develop our 2048 game application inside a Docker container. 🐳 If you don't have Docker installed on your local system, we'll set up an EC2 instance with Docker for this purpose. Follow these steps:

1. Set up an EC2 instance on AWS with Docker installed. You can find guides on how to do this in the AWS documentation.
    
2. Once the EC2 instance is ready, SSH into the instance and create a new directory for our game.
    
3. Copy the Dockerfile created in Step 1 into the new directory.
    
4. Build the Docker container using the following command:
    

```bash
docker build -t 2048-game .
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690862825124/1be9262d-053e-4c41-b6b5-6918dd9c0b67.png align="center")

## **Step 3: 🏗️ Creating a Docker Compose File 📝**

With our Docker container ready, let's create a Docker Compose file to define the services and configurations for our 2048 game application. Follow these steps:

1. Create a new file named `docker-compose.yml` in the root of your 2048 game repository.
    
2. Copy and paste the following code into the `docker-compose.yml` file:
    

```yaml
version: "3.8"
services:
  nginx:
    build:
      context: .
      dockerfile: Dockerfile
    ports:
      - "80:80"
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690862899020/5af28bbe-d48f-4fcf-b80b-371b7a03468c.png align="center")

## **Step 4: 🌐 Testing Your Application on EC2 Instance 🧪**

Great job! It's time to test our 2048 game application to make sure it's running smoothly on our EC2 instance. 🧪 Follow these steps:

1. Deploy the application on the EC2 instance using Docker Compose:
    

```bash
docker-compose up -d
```

1. Open your web browser and navigate to the public IP of your EC2 instance. You should see the 2048 game running and ready to play! 🎉
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690862952819/8133b3ec-663c-4532-bb79-8f327de5a0da.png align="center")

## **Step 5: ⚙️ Deploying to AWS Elastic Beanstalk with GitHub Actions 🚀**

Now comes the exciting part – deploying our 2048 game to AWS Elastic Beanstalk using GitHub Actions! ⚙️ Let's create the GitHub Actions workflow. Follow these steps:

1. In your GitHub repository, create a new folder named `.github`.
    
2. Inside the `.github` folder, create another folder named `workflows`.
    
3. In the `workflows` folder, create a new file named `deploy-aws.yml`.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690863377143/a8742972-a965-40b2-a5a8-3b471f057a47.png align="center")

## **Step 6: 🗝️ Configuring GitHub Actions 🔑**

Now, let's configure the `deploy-aws.yml` file to define our GitHub Actions workflow for CICD. Follow these steps:

1. Copy and paste the following code into the `deploy-aws.yml` file:
    

```yaml
name: Deploy to AWS Elastic Beanstalk

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Repository
        uses: actions/checkout@v2

      - name: Set up AWS CLI
        run: |
          sudo apt update
          sudo apt install -y python3-pip
          pip3 install --user awscli

      - name: Configure AWS Credentials
        run: |
          aws configure set aws_access_key_id ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws configure set aws_secret_access_key ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws configure set region us-east-1

      - name: Deploy to AWS Elastic Beanstalk
        run: |
          aws elasticbeanstalk create-application-version --application-name YOUR_APPLICATION_NAME --version-label v${{ github.sha }} --source-bundle S3Bucket=elasticbeanstalk-us-east-1-YOUR_ACCOUNT_ID, S3Key=2048-game.tar
          aws elasticbeanstalk update-environment --environment-name YOUR_ENVIRONMENT_NAME --version-label v${{ github.sha }}
```

Replace `YOUR_APPLICATION_NAME`, `YOUR_ENVIRONMENT_NAME`, and `YOUR_ACCOUNT_ID` with the appropriate values for your AWS Elastic Beanstalk application and environment.

## **Step 7: 🌐 Configuring AWS Elastic Beanstalk Environment 🔄**

Before we deploy our 2048 game application to AWS Elastic Beanstalk, we need to configure the Elastic Beanstalk environment to run our application smoothly. Follow these steps to set up the environment:

1. **Login to AWS Console:** Sign in to your AWS Management Console using your AWS account credentials.
    
2. **Navigate to Elastic Beanstalk:** Once logged in, navigate to the AWS Elastic Beanstalk service by clicking on "Services" in the top navigation bar, then selecting "Elastic Beanstalk" under the "Compute" section.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690864595805/b15215b7-7815-4a58-91ec-9c3e54599d65.png align="center")
    
3. **Create a New Application:** In the Elastic Beanstalk dashboard, click on "Create a new application." Give your application a name, such as "2048-game," and choose a platform that matches your Docker container (e.g., "Docker" for our case). Click "Create."
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690891775944/c31e2e95-4a02-4ee2-9025-913cf3bac9c3.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690891849273/0f4f96b4-ec8c-4d3a-bd3a-037f0b16bb25.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690891868537/122cc64b-6de8-4a81-a78e-2e33906b0dec.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690891891318/25382a43-275a-43ac-85be-03e8059d07e7.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690891916005/1225be45-323d-4479-b20c-3a10938938ba.png align="center")
    
4. **Create an Environment:** After creating the application, click on the "Create environment" button to create a new environment for your application.
    
    * **Environment Type:** Choose "Web server environment" to create an environment with a load balancer.
        
    * **Base Configuration:** Select "Docker" as the platform and choose the appropriate Docker version.
        
    * **Upload Your Code:** click on sample application
        
    * **Environment Information:** Provide a unique and descriptive name for your environment, such as "2048-game-environment."
        
    * **Instance Type:** Choose an instance type that suits your application's requirements. For testing purposes, you can select the default instance type.
        
    * **Security:** Configure the security settings based on your project requirements. You can use the default settings for testing purposes.
        
    * **Additional Configuration:** Optionally, you can configure additional settings like scaling options, environment variables, and more based on your application's needs.
        
    * **Create Environment:** Click on the "Create environment" button to create the environment.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690892091591/9d615836-34cb-45b3-9b85-c9bcd678ae36.png align="center")
        
5. **Wait for Environment Creation:** AWS Elastic Beanstalk will now start creating the environment for your application. This process may take a few minutes to complete. Once the environment is successfully created, you'll see the status as "Ready" in the Elastic Beanstalk dashboard.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690952568864/ca05ab15-ce65-4337-a07d-fd5bb80b8ab8.png align="center")
    
6. **Test the Environment:** After the environment is ready, you can test your application by navigating to the URL provided in the Elastic Beanstalk dashboard. It should display the demo application running on AWS Elastic Beanstalk.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690952515730/616dcd3b-68cf-4716-9c19-08d5f8d86ec0.png align="center")

Congratulations! 🎉 You have successfully configured your AWS Elastic Beanstalk environment to run the demo application. Now, we're all set to deploy the application using GitHub Actions.

In the next steps, we'll continue with the deployment using GitHub Actions. We'll create the necessary GitHub Actions workflow that automatically triggers the deployment process whenever changes are pushed to the main branch of your GitHub repository. Let's proceed with the final steps!

## **Step 8: 🏃‍♂️ Deploying with GitHub Actions 🚀**

With all the configurations in place, we're now ready to deploy our 2048 game application to AWS Elastic Beanstalk using GitHub Actions! 🏃‍♂️

1. Commit your changes and push to the `main` branch in your GitHub repository.
    
2. GitHub Actions will automatically trigger the deployment workflow, and your application will be deployed to AWS Elastic Beanstalk.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690952738092/bc111656-b35b-49dd-aa59-4d14bca63b86.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690965625151/91d1b8ec-5d19-4438-9f6d-57a72d1ded1a.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690966299554/79602a8f-ca05-49ba-b174-3f6844536df4.png align="center")

## Code Availability:

The complete source code for deploying the 2048 Game to AWS Elastic Beanstalk with GitHub Actions is available on GitHub. You can find the repository at the following link:

GitHub Repository: [https://github.com/Dhananjaykul/2048-game-aws-eb-github-actions](https://github.com/Dhananjaykul/2048-game-aws-eb-github-actions)

Feel free to clone the repository, explore the code, and follow along with the step-by-step tutorial in the blog. If you have any questions or feedback, don't hesitate to reach out. Happy coding! 🚀

## **Conclusion 🎉**

Congratulations! 🎉 You've successfully deployed the 2048 game to AWS Elastic Beanstalk using GitHub Actions. This powerful combination allows you to streamline your deployment process and make updates to your application with ease. Happy gaming! 🎮

I hope you find this step-by-step guide helpful and that it guides you through the process of deploying the 2048 game to AWS Elastic Beanstalk using GitHub Actions. If you have any further questions or need additional assistance, feel free to ask! 😊