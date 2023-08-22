---
title: "Launching your First Kubernetes Cluster with Nginx running"
seoTitle: "AWS Instance Launch and Minikube Installation for Kubernetes Nginx Pod"
seoDescription: "With this guide, you'll be able to get started with Kubernetes and Minikube quickly and easily, and start deploying your own pods on a Kubernetes cluster."
datePublished: Mon May 01 2023 07:30:07 GMT+0000 (Coordinated Universal Time)
cuid: clh4it8cz000109ml8wdn8d4g
slug: launching-your-first-kubernetes-cluster-with-nginx-running
tags: linux, kubernetes, devops, hashnodebootcamp, 90daysofdevops

---

If you're looking to experiment with Kubernetes, you might be wondering how to set up a Kubernetes cluster on your local machine. Luckily, there's a tool called Minikube that allows you to quickly and easily set up a local Kubernetes cluster for development and testing purposes.

In this article, we will be covering two tasks related to Kubernetes and Minikube. The first task involves installing Minikube on your local machine, while the second task involves creating your first pod on Kubernetes through Minikube.

## **What is Minikube?**

Minikube is a tool that allows you to run a single-node Kubernetes cluster on your local machine. It's designed for developers who want to experiment with Kubernetes without needing access to a full-scale production environment. Minikube is easy to set up and use, and it's a great way to get started with Kubernetes.

## **How Does Minikube Work?**

Minikube uses a virtual machine to run the Kubernetes cluster on your local machine. It sets up a lightweight virtual machine using a tool like VirtualBox, and then installs Kubernetes inside that virtual machine. This allows you to run a Kubernetes cluster on your local machine without interfering with your host operating system.

## **Advantages of Using Minikube**

Using Minikube has several advantages:

* **Ease of use:** Minikube is easy to set up and use. You don't need a lot of experience with Kubernetes to get started.
    
* **Cost-effective:** Minikube is free and can run on a lower-end machine, which means you can experiment with Kubernetes without needing to invest in expensive hardware.
    
* **Offline development:** With Minikube, you can develop and test Kubernetes applications offline, which is especially useful if you're working on a plane or in a location without internet access.
    
* **Learning tool:** Minikube is a great learning tool for developers who want to experiment with Kubernetes before moving to a production environment.
    

## Pods:

In Kubernetes, a pod is the smallest and simplest unit in the deployment model. A pod is a logical host for one or more containers that are deployed together on the same node and share the same network namespace. Each pod has a unique IP address within the cluster and can communicate with other pods via a shared network.

A pod can contain one or more containers, which share the same network and file system. These containers can be tightly coupled and work together to provide a specific application service. For example, a pod can contain an application container and a sidecar container that performs logging or monitoring tasks.

Kubernetes manages pods as a unit, scheduling them to run on nodes in the cluster and ensuring that the desired number of replicas are always available. Pods are ephemeral and can be created, deleted, or replaced at any time by Kubernetes. Because of this, any data or state that needs to be persisted should be stored outside the pod, such as in a persistent volume.

## Task 1: Install minikube on your local

here are the steps to install Minikube on an AWS EC2 instance running Ubuntu, using Docker as the driver:

1. Launch an EC2 instance:
    
    * Go to the AWS Console and log in to your account.
        
    * Click on the "Launch Instance" button to start the instance creation wizard.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682935872475/a1531db3-7e6b-4739-9b34-eefce3d39749.png align="center")
        
    * Choose an Ubuntu Server AMI and select the t2.medium instance type with 4GB RAM and 2 CPU.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682935939358/43659727-4836-4b34-8493-6abccde73d64.png align="center")
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682936000254/d6c30bb7-9e5b-43c4-8bf5-842e9a9ecc5e.png align="center")
        
    * Follow the wizard steps to configure the instance details, storage, security group, and key pair.
        
    * Review your configuration and launch the instance.
        
2. Connect to your EC2 instance:
    
    * Once the instance is launched, you need to connect to it through SSH.
        
    * Open your terminal or command prompt and navigate to the directory where your key pair is saved, or else connect directly.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682936238589/fce66d30-8661-4ec2-9ea0-bc75d9200d7d.png align="center")
        
    * Use the following command to connect to your instance:
        
        ```bash
        ssh -i <key-pair>.pem ubuntu@<public-IP-address>
        ```
        
3. Install Docker:
    
    * Before installing Minikube, you need to install Docker on your Ubuntu instance.
        
    * Run the following commands to update your Ubuntu instance and install Docker:
        
        ```bash
        sudo apt-get update
        sudo apt-get install docker.io
        ```
        
    * Start Docker using the following command:
        
        ```bash
        sudo systemctl start docker
        ```
        
    * Verify that Docker is running by using the following command:
        
        ```bash
        sudo systemctl status docker
        ```
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682936390424/e2f7d1c1-1623-4619-8c62-d2c51e16af1a.png align="center")
        
4. Install Minikube:
    
    * To install Minikube, use the following command:
        
        ```bash
        curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
        sudo install minikube-linux-amd64 /usr/local/bin/minikube
        ```
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682936471161/fe96a8d7-ab78-4d14-805d-d4316b7c45f1.png align="center")
        
5. Start Minikube:
    
    * To start Minikube, use the following command:
        
        ```bash
        minikube start --driver=docker
        ```
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682936607167/eb05bf9a-9af8-43dc-84fb-d5b7d11f47db.png align="center")
        
    * This command will start a single-node Kubernetes cluster on your Ubuntu instance using Docker as the driver.
        
6. Verify that Minikube is running:
    
    * Use the following command to verify that Minikube is running:
        
        ```bash
        kubectl version
        ```
        
    * This command will show the version of Kubernetes that Minikube is running.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682936753264/a0094fde-bb52-4288-93e8-ea3ae600c8b6.png align="center")
        

🥳🥳🥳🥳🥳🥳🥳🥳🥳🎉🎉🎉✨✨✨✨✨✨✨✨🎉🎉🎉🎉🎉🎉🎉🎉Congratulations! You have successfully installed Minikube on your Ubuntu instance running on AWS EC2 and started a Kubernetes cluster using Docker as the driver. You can now start deploying your pods and services on the Kubernetes cluster.

## Task 2. Create Niginx pod on Kubernetes through Minikube

1. Create a deployment YAML file for Nginx using your preferred text editor. For example, create a file called `nginx-deployment.yaml` and paste the following content:
    
    ```bash
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: nginx-deployment
      labels:
        app: nginx
    spec:
      replicas: 3
      selector:
        matchLabels:
          app: nginx
      template:
        metadata:
          labels:
            app: nginx
        spec:
          containers:
          - name: nginx
            image: nginx
            ports:
            - containerPort: 80
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682941278498/5ffc2bce-1816-4c26-8d1b-73f2ac109a11.png align="center")
    
    This YAML file defines a deployment called `nginx-deployment` with three replicas, a selector, and a template that specifies an Nginx container with a single port exposed.
    
2. Apply the deployment YAML file to the Kubernetes cluster using the following command:
    
    ```bash
    kubectl apply -f nginx-deployment.yaml
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682941345474/2782b3e9-fb73-473f-a759-ba8c69f31742.png align="center")
    
    This command creates a deployment object in the Kubernetes cluster that manages the creation and scaling of the Nginx pods.
    
3. Verify that the deployment is running using the following command:
    
    ```bash
    kubectl get deployment
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682941399467/300bdc0a-116a-42f1-91ae-2a3a0df4bcf7.png align="center")
    
    This command shows the status of all the deployments running in the Kubernetes cluster, including the `nginx-deployment`.
    
4. Verify that the pods are running using the following command:
    
    ```bash
    kubectl get pods
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682941468289/d2fcec07-719c-4ff2-b3ef-e3ff69ddf2d0.png align="center")
    
    This command shows the status of all the pods running in the Kubernetes cluster, including the Nginx pods created by the `nginx-deployment`.
    
5. Verify that the Nginx service is running using the following command:
    
    ```bash
    kubectl get svc
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682941539164/f7435c9b-2471-47be-a398-dc8f1700922e.png align="center")
    
    This command shows the status of all the services running in the Kubernetes cluster, including the Nginx service created by the `nginx-deployment`.
    

🥳🥳🥳🥳🥳🥳🥳🥳🥳🎉🎉🎉✨✨✨✨✨✨✨✨🎉🎉🎉🎉🎉🎉🎉🎉

Congratulations! You have successfully created an Nginx pod on Kubernetes through Minikube. You can now access the Nginx service from a web browser or a command-line tool using the IP address or hostname of your Ubuntu instance and the port number exposed by the Nginx container (usually port 80).