---
title: "Project-1: Automating Deployment of a Simple Web Application Using Jenkins and GitHub Webhook 🚀"
seoTitle: "Automating Deployment with Jenkins and GitHub Webhooks: A Step-by-Step"
seoDescription: "Discover how to automate the deployment of a web application using Jenkins and GitHub webhooks.Detailed guide to set up Jenkins, integrate it with GitHub."
datePublished: Sun Jul 02 2023 04:09:15 GMT+0000 (Coordinated Universal Time)
cuid: cljkwxq9c000209ma2q8j2wb2
slug: project-1-automating-deployment-of-a-simple-web-application-using-jenkins-and-github-webhook
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1688270735997/92023368-3b4b-4544-9cc0-323a15810ebc.png
tags: github, devops, jenkins, ci-cd, 90daysofdevops

---

In this blog post, we will explore how to automate the deployment of a simple web application using Jenkins and trigger it automatically using a GitHub webhook. We'll go through the step-by-step process of setting up Jenkins, integrating it with GitHub, configuring a Jenkins job, and finally, implementing a webhook to automatically trigger deployments upon code changes. Let's dive in! 💻🔧

**Step 1: Launch an AWS EC2 Instance (Jenkins-server) 🚀**

To start, we need to set up an EC2 instance on AWS. This instance will serve as our Jenkins server. Launch the instance and ensure you have the necessary access credentials to log in.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688262151439/b1f10036-e063-497f-a9b3-ed9476a5fcf2.png align="center")

Step 2: Install Java Development Kit (JDK) and Jenkins 📦☕

Log in to your AWS EC2 instance and follow these commands to install the required dependencies:

```bash
sudo apt update
sudo apt install openjdk-11-jre
java -version
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688262247542/17bcddbb-4d26-4ff7-8e0d-f73559c89d9b.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688262284422/16337e0c-c334-43d3-be5b-76cec9fd55ac.png align="center")

Now, let's install Jenkins by running the following commands:

```bash
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
/usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
https://pkg.jenkins.io/debian binary/ | sudo tee \
/etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt-get update
sudo apt-get install jenkins
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688262291167/35c5774a-a4a9-4c45-a428-9ddad1ca5b21.png align="center")

Once the installation is complete, Jenkins will be active and running.

Step 3: Expose Jenkins on Port 8080 🔓

By default, Jenkins runs on port 8080. To access it from your web browser, we need to expose port 8080. Follow these steps:

1. Navigate to the security settings of your AWS EC2 instance.
    
2. ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688262350620/680740d2-15fc-4f24-91b5-46edc729185b.png align="center")
    
    Click on "Security Groups" and edit the inbound rules.
    
3. ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688262384520/0b39d412-24e0-49e8-a2d6-ad1a1ee51400.png align="center")
    
    Add a new rule with custom TCP and port range as 8080, and set the source as your IP address.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688262417862/d70bd6cb-f184-48f2-9ace-88ebb096e1d1.png align="center")

Now, you can access Jenkins by entering your IP address followed by port 8080 in your web browser.

Step 4: Setting Up Jenkins for the Web Application Deployment 🚀

1. Access Jenkins using the IP address and port 8080.
    
2. ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688262507778/911cde92-2dd9-4bda-a585-5389de3abe18.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688262565022/eadc38f3-3b41-4972-8956-95c5ef654ee4.png align="center")
    
    Paste this above string in Administrator password
    
3. Click on "Install suggested plugins" and set up your username and password.
    
4. ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688262680380/4d14bc64-194f-4616-be97-00be0f6a032f.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688262771842/2975c267-9d1b-46cc-b30a-827afab62dc7.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688262794120/920d326b-2b4f-449b-8a3c-964dfd582cdc.png align="center")
    
    Create a new item and select "GitHub project."
    
5. ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688262877599/c1afdda1-4ccc-487a-ba18-3b64b7a83d48.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688262953512/69779e85-5282-46e7-a5b9-fd5f26c0675e.png align="center")
    
    Enter the URL of your GitHub project and configure the source code management by selecting Git and entering the Git URL.
    
6. ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688263112709/369d6be2-8b36-4dec-a43a-4cb1cc1f86da.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688263185273/477d7dcb-9ecc-4eb3-a603-4e944ea0ea2e.png align="center")
    
    Set the branch as "main"
    
7. ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688263248405/ea9b20a6-8946-4945-9b4f-553de02ce65d.png align="center")
    
    Generate SSH keys by typing "ssh-keygen" in the console.
    
8. ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688263386243/f9b38674-2005-45a4-88d0-05798aba5ff9.png align="center")
    
    Copy the public key from the `.ssh` directory.
    
9. ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688263465652/e17e34a9-6249-483f-ac5e-f6d1bc2594af.png align="center")
    
    Navigate to your GitHub accounts settings and add a new SSH key with the copied public key.
    
10. ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688265525185/f3d336e9-4493-4a9e-b60b-680c29943694.png align="center")
    
    Add credentials for GitHub integration, selecting the domain as "Global credentials."
    
11. ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688265653988/223529fb-9560-4b17-9f1e-ded32b69e542.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688265868650/0e0abe45-0f4d-46c7-b8b6-85e6e3a62cc1.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688265890419/60afa3da-ad22-4692-a2ac-c6e35ea8b1fe.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688266014037/f5423c3b-5227-425c-946b-e11b56c7ff45.png align="center")
    
    Configure the web app by adding an "Execute shell" build step.
    
12. Save the configuration and click on "Build Now."
    

Step 5: Dockerizing the Application 🐳

1. Install Docker on your system:
    

```bash
sudo apt-get update
sudo apt install docker.io
sudo usermod -aG docker jenkins
sudo systemctl restart jenkins
```

1. Configure the Jenkins job to use Git as the source code management.
    
2. Add the following build steps in the "Execute shell":
    

```bash
docker build -t my-web-app .
docker run -d -p 80:80 my-web-app
```

1. ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688266320379/c84e05a0-008c-4f20-93de-bce2956b1d9f.png align="center")
    
    Save the configuration and click on "Build Now" to build the Docker image and run the container.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688266502510/5cda8a7b-c373-4f14-94bd-a5cfeb2a16c1.png align="center")

1. Application will be running on port &lt;ip\_address&gt;:80
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688266551705/3504f845-b38f-4936-a25c-bf9f1fe81c2d.png align="center")

Step 6: Configuring GitHub

Webhook for Automatic Deployment 🎣

1. Install the "GitHub Integration Plugin" in Jenkins from the "Manage Jenkins" section.
    
2. ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688266736340/419efa95-e4e9-4b77-b1d7-4fcbd3c81195.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688266813147/cfb92efb-e8fe-44af-9cde-40786a9efbdc.png align="center")
    
    Go to your GitHub repository settings and add a new webhook.
    
3. ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688266858443/69d60fdb-11e2-4b3c-b1f4-caece64414de.png align="center")
    
    Set the payload URL as `<ip-address:8080>/github-webhook/`. Make sure port 8080 is accessible.
    
4. Select the content type as "application/json."
    
5. Select "Just the push event" to trigger the webhook.
    
6. Activate the webhook.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688266958123/bda9c9f6-e4dc-41f6-acee-c33209b13cfe.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688267012651/e1895bb6-4a45-42f3-b22a-8d63f19fbf2d.png align="center")

Step 7: Configure Jenkins Job for GitHub Webhook Trigger 🎯

1. Open the respective job configuration.
    
2. Select "Build Triggers" and enable "GitHub hook trigger for GITScm polling."
    
3. Save the configuration.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688267080712/faf317d4-d235-417b-b023-6096775cf239.png align="center")

Step 8: Stopping the Previous Docker Container and Building a New One 🐳🔄

To ensure that the previous container is stopped before building and running a new one, let's update the Jenkins job configuration with the following steps:

1. Add an additional "Execute shell" build step after the previous steps.
    
2. Update the shell commands to include stopping the previous container, building a new image, and running the updated container:
    

```shell
docker-compose down
docker-compose up -d
```

1. Save the configuration.
    

Now, whenever a code change is triggered by the GitHub webhook, Jenkins will stop the previous container, build a new Docker image, and run the updated container with the latest changes.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688270527984/557ba34c-c626-4b7b-8121-c13182177d2f.png align="center")

**GitHub Link to the Project 🔗**

To explore the code and delve deeper into the project, you can access the GitHub repository below:

[**Link to my GitHub Project**](https://github.com/Dhananjaykul/web-app_jenkins_webhook_deployment)

Feel free to explore the codebase, collaborate, and contribute to this exciting project!

**Conclusion 🌟**

With the added steps to stop the previous container and update the Docker image, Jenkins job is now equipped to handle continuous deployments seamlessly. Each code change will trigger Jenkins to stop the previous container, build a new image, and run the updated container, ensuring your web application always reflects the latest changes. Enjoy the automated and up-to-date deployments! 🚀🎉