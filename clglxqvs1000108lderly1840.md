---
title: "Docker for DevOps Engineers(Docker Compose)"
seoTitle: "The Ultimate Guide to Docker Compose and YAML"
seoDescription: "Learn how to use Docker Compose and YAML to set up your environment, configure services, and link containers."
datePublished: Tue Apr 18 2023 07:20:34 GMT+0000 (Coordinated Universal Time)
cuid: clglxqvs1000108lderly1840
slug: docker-for-devops-engineersdocker-compose
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1682513529668/a0b2d31b-9172-418f-b8b6-178ce9852a42.webp
tags: docker, devops, docker-compose, 90daysofdevops, trainwithshubham

---

### Introduction

In recent years, Docker has become one of the most popular tools for creating, deploying, and managing applications. Docker Compose and YAML are two essential components that enable developers to streamline the process of building and deploying complex applications. In this blog post, we will explore Docker Compose and YAML, their importance in the world of DevOps, and how they can be used to create more efficient and scalable applications.

# What is Docker Compose?

Docker Compose is a tool that allows developers to define and run multi-container Docker applications. With Docker Compose, you can define the services, networks, and volumes required by your application in a single YAML file. This makes it easier to manage and deploy complex applications that rely on multiple containers.

Docker Compose provides a simple and efficient way to manage the lifecycle of your containers. You can use it to start, stop, and restart your containers with a single command. Docker Compose also enables you to scale your application by adding or removing containers as required.

# What is YAML?

YAML (Yet Another Markup Language) is a human-readable data serialization language. It is commonly used for configuration files and data exchange between applications. YAML is similar to JSON, but it is more readable and easier to use.

YAML is widely used in DevOps and infrastructure as code (IaC) to define the configuration of applications and infrastructure. It is used in tools like Ansible, Kubernetes, and Docker Compose to define configuration files for services, networks, and volumes.

# Why are Docker Compose and YAML important?

Docker Compose and YAML are important because they enable developers to define and manage complex applications in a more efficient and scalable way. By defining the services, networks, and volumes required by your application in a single YAML file, you can easily manage and deploy your containers.

Using Docker Compose and YAML also enables you to define your application as code. This means that you can version control your application configuration, make changes to it easily, and collaborate with your team more effectively.

# How to use Docker Compose and YAML?

To use Docker Compose and YAML, you will need to define your application configuration in a YAML file. The YAML file should include the services, networks, and volumes required by your application.

Here is an example YAML file for a simple web application:

```bash
version: '3'

services:
  web:
    build: .
    ports:
      - "5000:5000"
  redis:
    image: "redis:alpine"
```

In this example, we have defined two services: web and redis. The web service builds the Dockerfile in the current directory and exposes port 5000. The redis service uses the Redis image from Docker Hub.

To start the application, you can use the following command:

```bash
$ docker-compose up
```

This will start the containers defined in the YAML file. You can then access the web application by visiting [**http://localhost:5000**](http://localhost:5000) in your web browser.

Conclusion

Docker Compose and YAML are important tools for developers working with Docker. They enable you to define and manage complex applications in a more efficient and scalable way. By defining your application configuration as code, you can version control it, make changes to it easily, and collaborate with your team more effectively. If you're not already using Docker Compose and YAML, it's time to start!

### **Task 1. Learn how to use the docker-compose.yml file, to set up the environment, configure the services and links between different containers, and also to use environment variables in the docker-compose.yml file.**

Docker Compose is a tool for defining and running multi-container Docker applications. It enables developers to define the services, networks, and volumes required by their applications in a single YAML file. In this guide, we will learn how to use the docker-compose.yml file to set up an environment, configure services and links between different containers, and use environment variables in the docker-compose.yml file.

Setting up the Environment

Before we start configuring the services in the docker-compose.yml file, we need to set up the environment for our application. This involves creating a directory for our application and creating a Dockerfile for each service.

Let's create a directory for our application called `myapp`:

```bash
$ mkdir myapp
$ cd myapp
```

Now let's create a Dockerfile for our first service, which will be a web server. Create a file called `Dockerfile` in the `myapp` directory and add the following content:

```bash
FROM nginx
COPY index.html /usr/share/nginx/html
```

This Dockerfile will use the official nginx image and copy a file called `index.html` to the web server's document root.

Now let's create the `index.html` file:

```bash
$ echo "Hello World!" > index.html
```

Configuring Services

Now that we have set up the environment, let's configure our services in the docker-compose.yml file. In this example, we will have two services: the web server and a Redis database.

Create a file called `docker-compose.yml` in the `myapp` directory and add the following content:

```bash
version: '3'

services:
  web:
    build: .
    ports:
      - "80:80"
    environment:
      - REDIS_URL=redis://redis:6379
  redis:
    image: "redis:alpine"
```

This docker-compose.yml file defines two services: `web` and `redis`. The `web` service will build the Dockerfile in the current directory and expose port 80 to the host machine. The `environment` section defines an environment variable called `REDIS_URL` with a value of `redis://redis:6379`. This will be used to connect the web server to the Redis database.

The `redis` service will use the Redis image from Docker Hub.

Links between Containers

We have defined the services, but we still need to link them together. We can use the `links` section in the docker-compose.yml file to establish links between containers.

Update the docker-compose.yml file to add a link between the `web` service and the `redis` service:

```bash
version: '3'

services:
  web:
    build: .
    ports:
      - "80:80"
    environment:
      - REDIS_URL=redis://redis:6379
    links:
      - redis
  redis:
    image: "redis:alpine"
```

This docker-compose.yml file adds the `links` section to the `web` service, with a link to the `redis` service.

Using Environment Variables

In the previous example, we used an environment variable to define the Redis URL. We can use environment variables in the docker-compose.yml file to make it more flexible and reusable.

Let's update the docker-compose.yml file to use environment variables for the web server's port and the Redis image tag:

```bash
version: '3'

services:
  web:
    build: .
    ports:
      - "${WEB_PORT:-80}:80"
    environment:
      - REDIS_URL=redis://redis:6379
    links:
      - redis
  redis:
    image: "redis:${REDIS_TAG:-alpine}"
```

### Task-2

### 1.Pull a pre-existing Docker image from a public repository (e.g. Docker Hub) and run it on your local machine. 2.Run the container as a non-root user (Hint- Use `usermod` command to give user permission to docker). 3.Make sure you reboot instance after giving permission to user. - Inspect the container's running processes and exposed ports using the docker inspect command. 4. Use the docker logs command to view the container's log output. 5.Use the docker stop and docker start commands to stop and start the container. 6Use the docker rm command to remove the container when you're done.

To complete this task, you will need to have Docker installed on your local machine. If you don't have Docker installed, you can download it from the official Docker website.

1. Pulling and Running a Docker Image as a Non-Root User
    

To pull a pre-existing Docker image from Docker Hub and run it on your local machine as a non-root user, follow these steps:

a. Open a terminal window and run the following command to pull the `nginx` image from Docker Hub:

```bash
docker pull nginx
```

b. Run the following command to create a new user and add them to the `docker` group:

```bash
sudo useradd -m -s /bin/bash <username>
sudo usermod -aG docker <username>
```

Note: Replace `<username>` with the username you want to use.

c. Restart the instance or logout and login again so that the new user's group membership takes effect.

d. Run the following command to start the `nginx` container as the non-root user:

```bash
docker run --name mynginx -p 80:80 -d --user <username> nginx
```

Note: Replace `<username>` with the username you created in step b.

e. Open a web browser and go to [`http://localhost`](http://localhost) to confirm that the nginx web server is running.

1. Inspecting the Container's Running Processes and Exposed Ports
    

To inspect the container's running processes and exposed ports, run the following command:

```bash
docker inspect mynginx
```

This will output a JSON object with detailed information about the container, including the running processes and exposed ports.

1. Viewing the Container's Log Output
    

To view the container's log output, run the following command:

```bash
docker logs mynginx
```

This will output the container's log messages to the console.

1. Stopping and Starting the Container
    

To stop the container, run the following command:

```bash
docker stop mynginx
```

To start the container again, run the following command:

```bash
docker start mynginx
```

1. Removing the Container
    

To remove the container when you're done, run the following command:

```bash
docker rm mynginx
```

This will remove the `mynginx` container from your local machine.