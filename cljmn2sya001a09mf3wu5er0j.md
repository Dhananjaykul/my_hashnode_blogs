---
title: "Project-2: Jenkins Declarative Pipeline: Deploying and Automating the 2048 Game"
seoTitle: "Deploying the 2048 Game with Jenkins: A Step-by-Step Guide"
seoDescription: "Learn how to deploy the popular 2048 game using Jenkins, Docker, and a declarative pipeline. Follow step-by-step guide to automate the deployment process"
datePublished: Mon Jul 03 2023 09:08:48 GMT+0000 (Coordinated Universal Time)
cuid: cljmn2sya001a09mf3wu5er0j
slug: project-2-jenkins-declarative-pipeline-deploying-and-automating-the-2048-game
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1688365052713/35fd7890-270d-44ad-b3c8-70efce38076f.png
tags: docker, devops, jenkins, 90daysofdevops, trainwithshubham

---

Jenkins, an open-source automation server, plays a vital role in enabling continuous integration and continuous delivery (CI/CD) for software development projects. Among the powerful features Jenkins offers, the Declarative Pipeline Syntax stands out. This tutorial will guide you through the creation of a Jenkins job using the Declarative Pipeline Syntax, using the popular 2048 game as an interesting example. Let's dive in!

## **What is a Pipeline in Jenkins? 🔧📜**

A pipeline in Jenkins is a collection of interconnected steps or jobs that execute sequentially. It serves as the foundation for the "Pipeline-as-code" approach, allowing the CD pipeline to be versioned and reviewed like any other code. The pipeline's definition is written in a text file called a Jenkinsfile, which can be committed to the project's source control repository.

## **Why Use Declarative Pipeline Syntax? 💡💻**

Declarative Pipeline Syntax is a more recent and advanced implementation of pipelines as code. It offers a structured and opinionated way of defining pipelines. Its concise and readable syntax simplifies pipeline creation, making it easier for developers to understand and modify pipelines. By committing the Jenkinsfile to source control, you gain immediate benefits such as creating a Pipeline build process for all branches and pull requests and facilitating code review and iteration on the Pipeline along with the remaining source code.

## **What is CI/CD? 🔄💻**

CI/CD, which stands for Continuous Integration/Continuous Delivery (or Continuous Deployment), is an essential software development approach that automates and streamlines the process of building, testing, and deploying code changes.

Continuous Integration (CI) involves regularly merging code changes from multiple developers into a shared repository, where automated builds and tests are run to detect issues and conflicts early on.

Continuous Delivery (CD) goes a step further, automatically deploying code changes to production environments after thorough testing and validation. This ensures that the code is always ready for release to end-users without delays or manual intervention.

Continuous Deployment (CD) automates the release process, pushing code changes to production as soon as they pass all tests and checks.

## **What Is a Build Job? 🚀👷‍♀️**

In Jenkins, a build job encompasses the configuration for automating a specific task or step in the application-building process. These tasks include gathering dependencies, compiling, archiving, transforming code, and testing and deploying code in different environments. Jenkins supports various types of build jobs, such as freestyle projects, pipelines, multi-configuration projects, folders, multibranch pipelines, and organization folders.

## **Setting Up Jenkins on an AWS EC2 Instance Running Ubuntu: 🚀☁️**

Let's start by setting up Jenkins on an AWS EC2 instance running Ubuntu. Follow these steps:

1️⃣ Launch an AWS EC2 instance with Ubuntu as the operating system. Ensure that port 8080 is open for Jenkins, and port 80 is open for the application in the security group.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688365403634/f2664229-1c17-4b66-b20e-7fa75b5b8cd8.png align="center")

2️⃣ Once the instance is launched and running, log in to the instance using SSH.

3️⃣ Install Java, Jenkins, and Docker by running the provided commands in the terminal.

```bash
sudo apt update
sudo apt install openjdk-11-jre
java -version
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
/usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
https://pkg.jenkins.io/debian binary/ | sudo tee \
/etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt-get update
sudo apt-get install jenkins

sudo apt install docker.io
sudo usermod -aG docker jenkins
sudo systemctl restart jenkins
```

4️⃣ Start Jenkins using the provided command.

```bash
sudo systemctl start jenkins
```

5️⃣ Access Jenkins in a web browser by navigating to http://&lt;instance\_ip&gt;:8080 and follow the on-screen instructions to set it up.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688372549208/e82756c0-df54-4244-9fcd-4d5ba0d3d0e5.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688372624662/a8fffa58-0a88-454e-bc38-f90e4b3ef6a3.png align="center")

Copy this string and paste it in the administrator password

## **Creating a Dockerfile and Docker Compose File for the 2048 Game: 🐳📦**

To build and run the 2048 game application, we'll create a Dockerfile and a docker-compose.yml file. Here's how:

1⃣ Create a Dockerfile in the root directory of your project and add the provided content.

```bash
FROM ubuntu:22.04
RUN apt-get update && apt-get install -y nginx zip curl
RUN sed -i '/daemon off;/d' /etc/nginx/nginx.conf
RUN echo "daemon off;" >> /etc/nginx/nginx.conf
RUN curl -o /var/www/html/master.zip -L https://github.com/gabrielecirulli/2048/archive/master.zip
RUN cd /var/www/html/ && unzip master.zip && mv 2048-master/* . && rm -rf 2048-master master.zip
EXPOSE 80
CMD ["nginx", "-c", "/etc/nginx/nginx.conf"]
```

2️⃣ Create a docker-compose.yml file in the root directory of your project and add the provided content.

```bash
version: "3.8"
services:
  nginx:
     build:
        context: .
        dockerfile: Dockerfile
     ports:
       - "80:80"
```

3️⃣ Build and run the application using the provided commands.

```bash
 sudo docker build . -t myapp
 sudo docker run -d -p 80:80 --name myapp myapp
```

## **Deploying the Application Using a Declarative Pipeline: 🚀🔧**

Now, let's deploy the 2048 game application using a declarative pipeline. Follow these steps:

1️⃣ Create a new Jenkins pipeline job and configure it as described.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688372777683/d57cc4db-16a7-4254-a0db-95a7b85bf437.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688372812751/47bfd50a-fe15-40dd-b936-add5cb371f17.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688372877865/152b8f60-d07f-49fe-a4b7-402c783b81ac.png align="center")

2️⃣ Enter the provided pipeline script in the pipeline configuration.

```bash
pipeline {
    agent any
    
    stages {
        stage('Clone') {
            steps {
                script {
                    // Check if repository directory exists
                    if (!fileExists('/var/lib/jenkins/workspace/2048_deployment/2048_game_deployment')) {
                        sh 'git clone https://github.com/Dhananjaykul/2048_game_deployment.git'
                    } else {
                        echo 'Repository already cloned'
                    }
                }
            }
        }
        
        stage('Build') {
            steps {
                dir('/var/lib/jenkins/workspace/2048_deployment/2048_game_deployment') {
                    sh 'docker build -t myapp .'
                }
            }
        }
        
        stage('Deploy') {
            steps {
                dir('/var/lib/jenkins/workspace/2048_deployment/2048_game_deployment') {
                    script {
                        sh 'docker stop myapp || true'
                        sh 'docker rm myapp || true'
                        sh 'docker run -d -p 80:80 --name myapp myapp'
                    }
                }
            }
        }
        
        stage('Test') {
            steps {
                dir('/var/lib/jenkins/workspace/2048_deployment/2048_game_deployment') {
                    script {
                        def ec2PrivateIP = sh(returnStdout: true, script: "curl -s http://169.254.169.254/latest/meta-data/local-ipv4").trim()
                        sh "curl -s http://${ec2PrivateIP}:80" // Make a GET request to the application
                        sh "curl -s http://${ec2PrivateIP}:80 | grep '2048'" // Verify that the response contains "2048"
                    }
                }
            }
        }
    }
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688372955345/619eeca1-8116-4490-aba9-6e4cc52a4881.png align="center")

3️⃣ Save the pipeline configuration.

4️⃣ Run the pipeline job by clicking "Build Now."

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688374324312/ff43e1fe-6ab4-4aee-a193-ac636e72d7e6.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688374370863/a4e3a025-38ab-4b9b-97f5-2f726c8d26d4.png align="center")

5️⃣ Verify the deployment by accessing the application in a web browser using the EC2 instance's public IP address and port 80.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688374552597/c86ec99b-6597-4cf5-9977-c6f40d64682b.png align="center")

## **Code Availability: 💻🔗**

The code for this project, including all necessary files and documentation, is available on GitHub. Feel free to fork the repository and make modifications to suit your needs. The repository can be found [here](https://github.com/Dhananjaykul/2048_game_deployment).

## **Conclusion: 🔚✨**

In this tutorial, we explored the Jenkins Declarative Pipeline Syntax and its significance in automating CI/CD processes. We successfully deployed the 2048 game application using Docker and Jenkins, and then automated the deployment using a declarative pipeline. By following the steps outlined in this blog, you can gain hands-on experience in setting up Jenkins, building Docker images, deploying applications, and automating the entire process. Enjoy exploring the possibilities of Jenkins Declarative Pipelines in your own projects!