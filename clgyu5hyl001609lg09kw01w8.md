---
title: "Jenkins Declarative Pipeline with Docker"
seoTitle: "Declarative Pipeline with Docker: A Step-by-Step Guide"
seoDescription: "Learn to integrate Docker with Jenkins declarative pipeline. Includes syntax and examples for building and running Docker containers in Jenkins."
datePublished: Thu Apr 27 2023 08:00:58 GMT+0000 (Coordinated Universal Time)
cuid: clgyu5hyl001609lg09kw01w8
slug: jenkins-declarative-pipeline-with-docker
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1682580953500/90df451c-8ec4-4e42-9b4b-c21bbf1a25db.png
tags: projects, devops, jenkins, 90daysofdevops, trainwithshubham

---

# **Introduction**

Jenkins is a popular open-source automation tool that allows for continuous integration and delivery (CI/CD) of software projects. Docker, on the other hand, is a containerization platform that allows for the creation and deployment of lightweight, portable containers that can run on any system with Docker installed.

In this tutorial, we will create a Jenkins declarative pipeline that integrates Docker using the `docker` Groovy syntax inside the stage block. We will use a sample application from GitHub for demonstration purposes.

# **Prerequisites**

To follow along with this tutorial, you will need the following:

* A running Jenkins server
    
* Docker installed on the Jenkins server
    
* A GitHub account
    
* Basic knowledge of Jenkins pipelines and Docker
    

<mark>If you don't meet these prerequisites follow my previous blogs on Dockers and Jenkins.</mark>

To create a Docker-Integrated Jenkins declarative pipeline, follow the below steps:

Step 1: Create a new Jenkins Pipeline:

1. Log in to your Jenkins server and navigate to the Jenkins home page.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682565216140/e80d0523-f6c1-4f47-b5f4-7dc486f73fd3.png align="center")
    
2. Click on the "New Item" button on the left-hand side of the screen to create a new Jenkins pipeline.
    
3. In the "Enter an item name" field, type in a name for your new pipeline and select "Pipeline" as the project type.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682565289400/bbcec892-6dd0-4a12-9225-31e6ffeded8c.png align="center")
    
4. Click on the "OK" button to continue.
    
5. On the next page, scroll down to the "Pipeline" section and select "Pipeline script" as the Definition.
    
6. In the Script text area, use this following code:
    

```bash
pipeline {
    agent any
    stages {
        stage('Code Build') {
            steps {
                git url: 'https://github.com/Dhananjaykul/react_django_demo_app'
                sh 'docker build -t myapp .'
            }
        }
        stage('Test') {
            steps {
                sh 'docker run myapp python manage.py test'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker run -d -p 8001:8001 myapp python manage.py runserver 0.0.0.0:8001'
            }
        }
    }
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682659200873/ad9723b6-5e46-492f-9ec9-25c9a3ffae5c.png align="center")

1. This pipeline script defines two stages: Build and Run. In the Build stage, we use the `docker build` command to build a Docker image with the name `my-app`.
    
2. In the Run stage, we use the `docker run` command to run the Docker container with the image we just built and map the container's port 8001 to the host's port 8001.
    
3. Click on the "Save" button to create the pipeline.
    

Step 2: Run the Jenkins Pipeline:

1. To run the pipeline, click on the pipeline name on the Jenkins home page.
    
2. Click on the "Build Now" button to start the pipeline.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682659277673/6d01d7e1-e726-4d09-a3be-058964d0ece7.png align="center")
    
3. Jenkins will start executing the pipeline stages, and you can see the progress in the pipeline view.
    
4. Once the pipeline has completed successfully, you can access the running application by opening a web browser and navigating to [`http://localhost:8001/`](http://localhost:8001/).
    
5. To stop the Docker container, run the following command in a terminal window:
    

```bash
docker stop $(docker ps -aq --filter ancestor=my-docker-image)
```

This command stops all running containers that were created from the `my-docker-image` Docker image.

Conclusion:

In this tutorial, we demonstrated how to create a Docker-Integrated Jenkins declarative pipeline to build and run a sample Python application. We used a Dockerfile to define the application's environment and integrated Docker commands into the Jenkins pipeline script to build and run the Docker container. With this integration, we can significantly improve the performance and scalability of our CI/CD pipeline.