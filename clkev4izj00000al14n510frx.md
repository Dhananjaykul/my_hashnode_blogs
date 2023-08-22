---
title: "Project-5: 🚀 Deploying a Netflix Clone App on Kubernetes with Kubeadm 🎬"
seoTitle: "Deploying Netflix Clone App on Kubernetes with Kubeadm | Step-by-Step"
seoDescription: "Deploy a Netflix clone web app on Kubernetes using Kubeadm. Follow this guide to containerize, deploy, and manage the app for seamless streaming. 🚀🎬"
datePublished: Sun Jul 23 2023 03:11:38 GMT+0000 (Coordinated Universal Time)
cuid: clkev4izj00000al14n510frx
slug: project-5-deploying-a-netflix-clone-app-on-kubernetes-with-kubeadm
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1690082147240/06841ddb-5b68-4243-ae97-65fe5c75f987.gif
tags: docker, kubernetes, devops, 90daysofdevops

---

## Introduction 📜

In this project, we will walk you through the process of deploying a Netflix clone web application on a Kubernetes cluster using Kubeadm. Kubernetes is a powerful container orchestration platform that simplifies the deployment and management of containerized applications, providing benefits like high availability, scalability, and automatic failover. We will create Docker images of the web application and its dependencies, deploy them onto the Kubernetes cluster using Kubernetes manifests, and explore the Kubernetes Dashboard and kubectl for monitoring and management. Let's get started! 🎉

## Prerequisites 🛠️

Before diving into the deployment, make sure you have the following:

1. Basic knowledge of Docker and Kubernetes concepts.
    
2. A working Kubernetes cluster set up with Kubeadm. For setting up Kubernetes on AWS EC2, follow [this guide.](https://dhananjaykulkarni.hashnode.dev/a-step-by-step-guide-setting-up-a-kubernetes-cluster-with-kubeadm-on-aws-ec2-instances)
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690080451955/798757ce-e487-4194-8d40-9a305b4feafe.png align="center")
    
3. Clone the Netflix Clone app from GitHub.
    
    ```bash
    git clone https://github.com/crazy-man22/netflix-clone-react-typescript.git
    ```
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690035455060/17f5770e-a5de-47ff-81d2-381bccb2692a.png align="center")

## Step 1: Containerize the Netflix Clone App 🐳

Let's start by containerizing the Netflix Clone app using Docker. Create a Dockerfile in the root directory of our application with the following content:

```Dockerfile
FROM node:16.17.0-alpine as builder
WORKDIR /app
COPY ./package.json .
COPY ./yarn.lock .
RUN yarn install
COPY . .
ARG TMDB_V3_API_KEY
ENV VITE_APP_TMDB_V3_API_KEY=${TMDB_V3_API_KEY}
ENV VITE_APP_API_ENDPOINT_URL="https://api.themoviedb.org/3"
RUN yarn build

FROM nginx:stable-alpine
WORKDIR /usr/share/nginx/html
RUN rm -rf ./*
COPY --from=builder /app/dist .
EXPOSE 80
ENTRYPOINT ["nginx", "-g", "daemon off;"]
```

Build the Docker image and push it to Docker Hub (replace `<your_dockerhub_username>` with your Docker Hub username):

```bash
docker build -t <your_dockerhub_username>/my_netflixapp_image .
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690036020955/8e1d0a56-9f07-4488-9287-26333eee9f0a.png align="center")

```bash
docker push <your_dockerhub_username>/my_netflixapp_image
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690036267337/d70501e7-3e77-405f-9c55-49f130a43abe.png align="center")

## Step 2: Deployment Manifest 📜

Now, let's create a Kubernetes deployment manifest to deploy the Netflix Clone app. Create a file named `deployment.yml` with the following content:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: netflix-app
  labels:
    app: netflix-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: netflix-app
  template:
    metadata:
      labels:
        app: netflix-app
    spec:
      containers:
      - name: netflix-app
        image: <your_dockerhub_username>/my_netflixapp_image
        ports:
        - containerPort: 80
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690036424948/de029bd2-5a1d-4d90-a49a-f1cb1f87b5a2.png align="center")

Apply the deployment manifest to the Kubernetes cluster:

```bash
kubectl apply -f deployment.yml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690036453315/a8cef421-2067-4013-bc79-4db787273785.png align="center")

## Step 3: Service Manifest ⚙️

Next, let's create a Kubernetes service manifest to expose the Netflix Clone app. Create a file named `service.yml` with the following content:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: netflix-app
  labels:
    app: netflix-app
spec:
  type: NodePort
  ports:
  - port: 80
    targetPort: 80
    nodePort: 30007
  selector:
    app: netflix-app
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690036493282/0983939e-b74f-4813-8988-a1b967e0fb65.png align="center")

Apply the service manifest to the Kubernetes cluster:

```bash
kubectl apply -f service.yml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690036528329/539cdde0-ce16-4135-9b93-c45e48e0a591.png align="center")

## Step 4: Verify the Deployment ✔️

To ensure that the Netflix Clone app is successfully deployed, let's check the status of the deployment and service:

```bash
kubectl get deployment
kubectl get pods
kubectl get service netflix-app
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690080697380/195b04e7-8036-42cb-b88e-43670579968d.png align="center")

You should see two pods running, and the service should be exposed on port 30007.

## Step 5: Access the Netflix Clone App 🖥️

Now that the app is deployed, you can access it using the NodePort exposed on your Kubernetes cluster. Here's how to enable external access to the NodePort on AWS EC2:

1. **Find the Worker Nodes' Security Group:** Go to AWS EC2 Console &gt; Instances &gt; Select worker nodes &gt; Note the associated security group.
    
2. **Add an Inbound Rule to the Security Group:** In the security group details, add a new inbound rule:
    
    * Type: Custom TCP Rule
        
    * Port Range: Specify the NodePort used in the service manifest (e.g., 30007).
        
    * Source: Set to "Anywhere" (0.0.0.0/0) for unrestricted access or define specific IP ranges for more control.
        
    * Save the rule to apply the changes.
        

With the inbound rule added, the Netflix Clone app should now be accessible via `<worker_node_external_ip>:30007` in your web browser.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690080834586/513a8206-e194-45e2-b392-51b3f60f2a42.png align="center")

For production environments, consider using LoadBalancer or Ingress controllers for enhanced security and SSL termination.

## Step 6: Monitoring and Management 📊

Kubernetes provides several tools for monitoring and managing applications. You can use the Kubernetes Dashboard and `kubectl` to check pod logs, scale the deployment, and more. Additionally, set up monitoring and logging solutions for better visibility into your app's performance.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690081170037/3773368e-6ec9-4a38-90d9-5044ba486318.png align="center")

## Conclusion 🏁

Congratulations! 🎉 You have successfully deployed a Netflix Clone app on Kubernetes using Kubeadm. We covered containerizing the app with Docker, creating Kubernetes deployment and service manifests, and verifying the deployment. Kubernetes offers powerful features for scaling and managing containerized applications, making it an excellent choice for deploying apps at scale. Explore more of Kubernetes' capabilities to further enhance your deployment!

Now you can enjoy your Netflix Clone app running seamlessly on Kubernetes! 🍿🎥

Feel free to explore the [**Netflix Clone React TypeScript Repository**](https://github.com/Dhananjaykul/netflix-clone-react-typescript/tree/main) to get the complete source code and continue your learning journey with Kubernetes and containerization. Happy coding! 😊🚀