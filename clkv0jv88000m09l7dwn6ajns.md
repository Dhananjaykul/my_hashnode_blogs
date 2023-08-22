---
title: "Project-9: 🚀 Setting up a Kubernetes Cluster with MiniKube on AWS: Deploying Django Todo App and Managing Network and Services 🌐"
seoTitle: "Quick Guide to Kubernetes with MiniKube on AWS for Django Todo App"
seoDescription: "Learn how to set up a Kubernetes cluster using MiniKube on AWS, deploy a Django Todo app, and manage network and services for seamless communication."
datePublished: Thu Aug 03 2023 10:27:51 GMT+0000 (Coordinated Universal Time)
cuid: clkv0jv88000m09l7dwn6ajns
slug: project-9-setting-up-a-kubernetes-cluster-with-minikube-on-aws-deploying-django-todo-app-and-managing-network-and-services
tags: python, kubernetes, hashnodebootcamp, 90daysofdevops, wemakedevs

---

## **📝 Section 1: Setting up a Kubernetes Cluster with MiniKube on AWS 🚀**

### **🌟 Why MiniKube? 🌟**

MiniKube is a fantastic lightweight tool that lets you run Kubernetes on your local machine. It's perfect for development, testing, and learning purposes. With MiniKube, you can quickly and easily set up a Kubernetes environment without the hassle of a complex setup. It's especially great for developers who want to experiment with Kubernetes.

### **🚀 How to Install MiniKube on Your Local Machine 🚀**

1. Launch an EC2 instance:
    
    * Log in to your AWS account and click "Launch Instance."
        
    * Choose an Ubuntu Server AMI and select t2.medium with 4GB RAM and 2 CPU.
        
2. Connect to your EC2 instance:
    
    * Use SSH to connect to your instance: `ssh -i <key-pair>.pem ubuntu@<public-IP-address>`
        
3. Install Docker:
    
    * Update your instance and install Docker:
        
    
    ```bash
    sudo apt-get update
    sudo apt-get install docker.io
    sudo systemctl start docker
    ```
    
4. Install MiniKube:
    
    ```bash
    curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
    sudo install minikube-linux-amd64 /usr/local/bin/minikube
    ```
    
5. Start MiniKube:
    
    ```bash
    minikube start --driver=docker
    ```
    
6. Verify MiniKube:
    
    ```bash
    kubectl version
    ```
    

## **📝 Section 2: Deploying Django Todo App in Kubernetes Pods and Managing Cluster 🌐**

### **🌟 Role of Docker Containers and Kubernetes Pods 🌟**

Docker Containers package applications and their dependencies for easy deployment. In this project, we use Docker Containers to package our Django Todo app. Kubernetes Pods are the smallest units in a cluster, encapsulating one or more containers and shared resources.

### **⚙️ Importance of Deployment, Replication, Auto-Healing, and Auto-Scaling in Kubernetes ⚙️**

Deployment: Defines the desired state and management of your application, ensuring the right number of replicas with minimal downtime.

Replication: Maintains a specified number of Pod replicas, ensuring high availability and fault tolerance.

Auto-healing: Automatically detects and recovers from failures, ensuring Pods are always running.

Auto-scaling: Automatically adjusts the number of replicas based on demand, handling increased traffic.

### **🚀 Steps to Manage Features for Your Kubernetes Cluster 🚀**

1. Clone the django-todo-cicd repository from GitHub.
    
2. Build the Docker image:
    
    ```bash
    docker build -t django-todo-cicd:latest .
    docker run -d -p 8000:8000 django-todo-cicd:latest
    ```
    
3. Create a Kubernetes Service:
    
    * Create `service.yaml`:
        
    
    ```bash
    apiVersion: v1
    kind: Service
    metadata:
      name: todo-service
    spec:
      type: NodePort
      selector:
        app: todo-app
      ports:
      - name: http
        port: 80
        targetPort: 8000
        nodePort: 30007
    ```
    
    * Apply the Service:
        
    
    ```bash
    kubectl apply -f service.yaml
    ```
    
4. Create a Kubernetes Deployment:
    
    * Create `deployment.yaml`:
        
    
    ```bash
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: todo-deployment
      labels:
        app: todo-app  
    spec:
      replicas: 2
      selector:
        matchLabels:
          app: todo-app
      template:
        metadata:
          labels:
            app: todo-app
        spec:
          containers:
          - name: todo-app
            image: django-todo-cicd:latest
            ports:
            - containerPort: 8000
    ```
    
    * Apply the Deployment:
        
    
    ```bash
    kubectl apply -f deployment.yaml
    ```
    
5. Verify Pods and Test Auto-healing and Auto-scaling:
    
    ```bash
    kubectl get pods
    kubectl delete pod todo-deployment-7987844987-88mng (to test auto-healing)
    kubectl scale deployment todo-deployment --replicas=4 (to test auto-scaling)
    kubectl get deployments
    kubectl get pods
    ```
    

## **📝 Section 3: Managing Network and Services with Host IP Allocation through Proxy on AWS EC2 🌐**

### **🌟 Importance of Managing Network and Services 🌟**

Properly managing network and services in Kubernetes enables seamless communication between applications, both within and outside the Cluster. It ensures high availability, scalability, and security.

### **🚀 Managing Network and Services with Host IP Allocation through Proxy on AWS EC2 🚀**

1. Expose the Pod as a Service:
    
    * Create `service.yaml`:
        
    
    ```bash
    apiVersion: v1
    kind: Service
    metadata:
      name: todo-service
      labels:
        app: todo-app
    spec:
      type: NodePort
      selector:
        app: todo-app
      ports:
      - name: http
        port: 80
        targetPort: 8000
        nodePort: 30007
    ```
    
    * Apply the Service:
        
    
    ```bash
    kubectl apply -f service.yaml
    ```
    
2. Map the IP address to a hostname:
    
    * Edit the /etc/hosts file:
        
    
    ```bash
    sudo vim /etc/hosts
    ```
    
    * Add a new line: `<Node-IP>` [`todo-app.com`](http://todo-app.com)
        
3. Access the Django Todo app using the URL [`http://todo-app.com`](http://todo-app.com) in a web browser.
    

🎉🎉🎉 Congratulations! with these steps you will successfully set up and deployed a Django Todo app on a Kubernetes cluster using MiniKube and managed its network and services on AWS EC2 with Route53! 🎉🎉🎉

### **📁 Code Availability 📁**

The code for this project is available on GitHub. Feel free to fork the repository and make your own modifications: [GitHub Repository](https://github.com/Dhananjaykul/django-todo-cicd).

## **🎯 Conclusion 🎯**

In this project, we covered the essential steps to create a Kubernetes cluster using MiniKube on AWS EC2, deployed a Django Todo app in Kubernetes Pods, and managed the network and services through AWS EC2. By understanding these concepts, you are now equipped to explore more complex applications and unleash the full power of Kubernetes in your projects! Happy coding! 🚀🌟