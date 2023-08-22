---
title: "Jenkins Freestyle Project for DevOps Engineers"
seoTitle: "Creating a Jenkins Project to Deploy Docker Image of a Node.js App"
seoDescription: "This tutorial covers the step-by-step process to create a Jenkins project to deploy a Docker image of a Node.js app on an AWS EC2 instance."
datePublished: Sun Apr 23 2023 03:41:03 GMT+0000 (Coordinated Universal Time)
cuid: clgsv3u66000309jx9e7z6sgk
slug: jenkins-freestyle-project-for-devops-engineers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1682213645255/614584b3-d1f0-4bd4-831c-c798dd8728e6.webp
tags: github, git, devops, jenkins, 90daysofdevops

---

### What is CI/CD?

CI/CD stands for Continuous Integration/Continuous Delivery (or Continuous Deployment) and is a software development approach that aims to automate and streamline the process of building, testing, and deploying code changes.

Continuous Integration refers to the practice of regularly merging code changes from multiple developers into a shared repository, where automated builds and tests are run to detect any issues or conflicts early on.

Continuous Delivery, on the other hand, is the practice of automatically deploying code changes to production environments after they have been tested and validated. This ensures that the code is always ready to be released to end-users, without any delays or manual intervention.

Continuous Deployment takes this one step further by automating the release process so that code changes are automatically pushed to production as soon as they pass all tests and checks.

CI/CD is an essential part of modern software development, as it allows teams to move faster, improve code quality, and reduce the risk of errors and downtime.

### What Is a Build Job?

A Jenkins build job contains the configuration for automating a specific task or step in the application building process. These tasks include gathering dependencies, compiling, archiving, or transforming code, and testing and deploying code in different environments. Jenkins supports several types of build jobs, such as freestyle projects, pipelines, multi-configuration projects, folders, multibranch pipelines, and organization folders.

### What is Freestyle Projects ?? 🤔

A freestyle project in Jenkins is a type of project that allows you to build, test, and deploy software using a variety of different options and configurations. Here are a few tasks that you could complete when working with a freestyle project in Jenkins:

Task 1: Create a new Jenkins freestyle project for your app. In the "Build" section of the project, add a build step to run the "docker build" command to build the image for the container. Add a second step to run the "docker run" command to start a container using the image created in step 2.

1. Log in to Jenkins:
    
    * Open your web browser and navigate to the URL of your Jenkins instance (publicIPadress:8080) As shown below.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682217381224/7b351249-eac2-463b-9d41-fe4cc9101a98.png align="center")
        
    * Log in using your Jenkins username and password.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682217540582/9b9c419a-7b12-433d-a2f0-cdee4b66fdf1.png align="center")
        
2. Create a new Jenkins Freestyle Project:
    
    * Click on "New Item" on the Jenkins dashboard.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682217703202/32daff3b-1556-498e-ada5-a34d37318c82.png align="center")
        
    * Enter a name for the project in the "Enter an item name" field, for example, "node-todo-cicd".
        
    * Select "Freestyle project" and click "OK".
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682217781619/f0f14e5b-1758-463c-a780-e7abeb205344.png align="center")
        
3. Configure the Jenkins Freestyle Project:
    
    * In the "General" tab, select "Git hub " and enter the github link
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682218006434/52418cec-8169-437e-8cb5-67022ddf3199.png align="center")
        
    * In the "Source Code Management" tab, select "Git" and enter the URL of your Git repository.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682218212979/f8e167e5-1ef5-4ea0-9f1d-b6b673a4e9b4.png align="center")
        
    * In the "Build" tab, click on "Add build step" and select "Execute shell".
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682218309512/ea619d1b-bcc0-4ea8-af25-3bce4fd89fcb.png align="center")
        
    * Enter the following command to build the Docker image:
        
        ```bash
        docker build -t node-todo-cicd:latest .
        ```
        
    * Add a second build step to start a container using the image:
        
        ```bash
        docker run -d -p 8000:8000 node-todo-cicd:latest
        ```
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682220096503/5fd89657-7486-46be-8d85-f0055e1c1378.png align="center")
        
4. Save the Jenkins Freestyle Project:
    
    * Click on "Save" to save the project configuration.
        
5. Build the Jenkins Freestyle Project:
    
    * Click on "Build Now" to start the build process.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682219520855/0ceaffbb-9812-4e0a-a356-4c6363169b79.png align="center")
        
    * Jenkins will run the build steps and display the console output in real-time.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682220203755/055bc00f-89dd-4651-8305-00d82e5df734.png align="center")
        
    * Once the build is complete, you can access your Node-Todo-CICD app by navigating to `http://<Jenkins-server-IP-address>:8080`.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682220283320/2d12d9a0-470a-4a6c-a04a-762c8e61a563.png align="center")
        

Task 2: Create Jenkins project to run "docker-compose up -d" command to start the multiple containers defined in the compose file (Hint- use day-19 Application & Database docker-compose file) .Set up a cleanup step in the Jenkins project to run "docker-compose down" command to stop and remove the containers defined in the compose file.

To create a Jenkins project to run "docker-compose up -d" command, and a cleanup step to run "docker-compose down", you can follow these steps:

1. Log in to your Jenkins server and create a new freestyle project.
    
2. Give your project a name ("node-todo-app-deployment") and click "OK".
    
3. In the "General" section of the project configuration, check the "GitHub project" box and enter the URL of your GitHub repository.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682220780055/035fe404-34f5-44d8-8906-184c376a5c27.png align="center")
    
4. In the "Source Code Management" section, select "Git" as the repository type and enter the URL of your GitHub repository. Optionally, you can specify the branch to build.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682220845497/24028975-fe7e-4539-aa6b-c5ee56875388.png align="center")
    
5. In the "Build" section, click the "Add build step" drop-down menu and select "Execute shell".
    
6. In the "Command" text box, enter the following command to start the containers defined in the Docker Compose file:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682220937527/0b787a58-ea47-4b02-b3c8-d3f660cbdd36.png align="center")
    
7. Click "Save" to save the project configuration.
    

Now, when you run the Jenkins project, it will start the containers defined in the Docker Compose file using the "docker-compose up -d" command, and stop and remove the containers using the "docker-compose down" command when the build finishes.

That's it! 🎉🎉✨✨✨✨✨✨✨✨✨✨✨✨✨✨✨✨✨✨✨✨✨✨✨✨✨✨✨✨You have successfully created a Jenkins freestyle project for your Node-Todo-CICD app and added build steps to build the Docker image and start a container using the image as well as using docker compose