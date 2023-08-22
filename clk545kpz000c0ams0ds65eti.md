---
title: "Project-4: 🔢 11 Steps to Deploy a Web App using Docker Swarm on AWS: A Production-Ready Guide 🚀🐳"
seoTitle: "Deploying Web App Using Docker Swarm on AWS: Step-by-Step Guide"
seoDescription: "Learn how to deploy a web application using Docker Swarm on AWS. Simplify application management and achieve high availability with Docker Swarm."
datePublished: Sun Jul 16 2023 07:26:42 GMT+0000 (Coordinated Universal Time)
cuid: clk545kpz000c0ams0ds65eti
slug: project-4-11-steps-to-deploy-a-web-app-using-docker-swarm-on-aws-a-production-ready-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1689491690154/c8a524b0-d1a3-49bb-9f13-93fc62ea6a06.png
tags: aws, devops, 90daysofdevops, trainwithshubham, docker-dockerswarm-aws-webapplication-deployment-scalability-highavailability-devops

---

In today's blog, we will explore the process of deploying a web application using Docker Swarm on AWS. Docker Swarm allows us to create a cluster of Docker nodes, making it easier to manage and scale our applications. Let's dive into the step-by-step process:

## **🔸 Step 1: Create Instances**

To begin, head over to the AWS portal and create three new instances: Swarm-manager, Swarm-worker1, and Swarm-worker2. These instances will form our Docker Swarm cluster.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689480647719/94590551-2194-47be-b8c8-9bcd0ebd3a39.png align="center")

## **🔸 Step 2: Configure Inbound Rules**

For each instance, you need to add the following rules to allow communication within the Docker Swarm:

1. Custom TCP port 2377: This port is used by Docker Swarm for cluster management and communication between the swarm manager and worker nodes.
    
2. Custom TCP port 8001 (or any other port you specified in your service): This port is specific to your application and allows external access to the service running inside the Docker containers.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689480880221/85e85296-a3e1-4bc0-84a9-10fbfa87b332.png align="center")

## **🔸 Step 3: Install Docker**

Next, install Docker on all three nodes.

```bash
sudo apt-get update
sudo apt-get install docker.io -y
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689481134584/813fde7d-0507-4649-acbd-2cb09e883c71.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689481209749/440e9432-1757-415f-a1ad-0a49d346017e.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689481299050/caa2d572-da12-42de-9a89-17717f6e94be.png align="center")

Docker installed on all three VMs 😉

## **🔸 Step 4: Initialize the Swarm**

On the Swarm Manager node, open the terminal and run the command

```bash
sudo docker swarm init
```

This command will initialize an empty swarm.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689481406973/fff79bcb-9663-4d08-8b46-5ebad541ebff.png align="center")

## **🔸 Step 5: Add Nodes to the Swarm**

After initializing the swarm on the swarm-manager node, a key will be generated. Copy and run this key on the remaining servers to add them as workers to the swarm.

Node-1: Got an error then realized I need to use sudo

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689481556604/5cb6cbfc-10f6-4662-9dd5-150d3d4e8714.png align="center")

Node-2

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689481718588/f8d507cf-c581-4258-8a55-344f795eb1f2.png align="center")

Now! The family is complete! 😅

## **🔸 Step 6: Check Swarm Nodes**

To verify the status of all the nodes in the swarm manager, run the command:

```bash
sudo docker node ls
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689481991286/a614657f-d8e2-4d5d-afea-6fb025c1f3d2.png align="center")

## **🔸 Step 7: Create a Service**

On the Manager Node, create a service using the command

```bash
sudo docker service create --name django-app-service --replicas 3 --publish 8001:8001 trainwithshubham/react-django-app:latest
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689491021115/5423e33f-f024-46e8-9e30-abb8f1e87902.png align="center")

## **🔸 Step 8: Verify Service Deployment**

Run below command to verify that the service has been created and is running.

```bash
sudo docker service ls
```

## **🔸 Step 9: Check Container Status**

To check the containers running on the manager node, use the below command :

```bash
sudo docker ps
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689491062435/50092833-4d97-4827-98ba-bbab9a97b971.png align="center")

## **🔸 Step 10: Access the Web Application**

The web application service will now be running on all three nodes. To access it, grab the IP address of any of the nodes followed by port 8001. For example, &lt;ip\_of\_3\_vms&gt;:8001.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689490965601/2c20b23f-027d-4de1-9d94-e452e76a862e.png align="center")

## **🔸 Step 11: Removing Nodes**

If you need to remove any node from the swarm, run below command on the specific worker node.

```bash
sudo docker swarm leave
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689491097487/f3e58e20-258b-4d97-8f08-27ad117baa77.png align="center")

This will remove the node from the swarm environment.

By following these steps, you can deploy your web application using Docker Swarm on AWS, ensuring a scalable and reliable production-ready environment. Docker Swarm simplifies the process of managing your application across multiple nodes, allowing for efficient scaling and high availability.

Feel free to share your experiences and ask any questions in the comments below. Happy deploying! 🚀🐳

#Docker #DockerSwarm #AWS #WebApplication #Deployment #Scalability #HighAvailability #DevOps