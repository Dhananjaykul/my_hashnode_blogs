---
title: "Building a Scalable and Fault-tolerant Kubernetes Cluster on AWS with MiniKube"
seoTitle: "Built a Kubernetes Cluster on AWS from scratch to deploy a todo-app"
seoDescription: "Try building your own Kubernetes cluster on AWS ,experiment with deploying different types of applications  with detailed instructions and code snippets"
datePublished: Thu May 04 2023 10:24:12 GMT+0000 (Coordinated Universal Time)
cuid: clh8zcnwu000109jw0k06d1zm
slug: building-a-scalable-and-fault-tolerant-kubernetes-cluster-on-aws-with-minikube
tags: docker, projects, kubernetes, devops, trainwithshubham

---

# <mark>Introduction</mark>

Kubernetes, commonly abbreviated as k8s, is an open-source platform for managing containerized workloads and services. It was initially developed by Google and later donated to the Cloud Native Computing Foundation (CNCF). Kubernetes automates the deployment, scaling, and management of containerized applications, making it easier to manage large and complex container environments.

## 1.Benefits of Using Kubernetes

Kubernetes offers numerous benefits for developers and system administrators, including:

1. <mark>Scalability</mark>: Kubernetes can automatically scale the number of containers up or down based on the demand, ensuring that the applications always have the necessary resources to run.
    
2. <mark>High availability</mark>: Kubernetes supports high availability by automatically distributing workloads across multiple nodes, thereby reducing the risk of downtime.
    
3. <mark>Portability</mark>: Kubernetes allows applications to be easily moved between different environments, such as on-premise data centers or public cloud platforms.
    
4. <mark>Resource efficiency</mark>: Kubernetes helps optimize resource utilization by scheduling containers on available resources and reducing resource wastage.
    
5. <mark>Simplified deployment</mark>: Kubernetes simplifies the deployment process by automating container configuration, application updates, and rollbacks.
    

## 2.Kubernetes Architecture

Kubernetes architecture consists of a master node and worker nodes that form a cluster. The master node is responsible for managing the cluster state and making decisions about the placement of containers on the worker nodes. The worker nodes are responsible for running the containers and providing the necessary computing resources.

![Components of Kubernetes](https://d33wubrfki0l68.cloudfront.net/2475489eaf20163ec0f54ddc1d92aa8d4c87c96b/e7c81/images/docs/components-of-kubernetes.svg align="left")

The Kubernetes architecture includes the following components:

1. <mark>Control plane</mark>: The control plane is responsible for managing the Kubernetes cluster's overall state and consists of the API server, etcd, scheduler, and controller manager.
    
2. <mark>API server</mark>: The API server exposes the Kubernetes API, which allows users to interact with the cluster and perform various operations, such as deploying and scaling applications.
    
3. <mark>etcd</mark>: etcd is a distributed key-value store that stores the configuration data and state information for the Kubernetes cluster.
    
4. <mark>Scheduler</mark>: The scheduler is responsible for scheduling containers onto the worker nodes based on the available resources and other constraints.
    
5. <mark>Controller manager</mark>: The controller manager is responsible for managing the different controllers that are responsible for various cluster-level functions, such as managing nodes and services.
    
6. <mark>Worker nodes</mark>: The worker nodes are responsible for running the containers and providing the necessary computing resources. Each worker node runs a kubelet, which communicates with the API server to receive instructions about which containers to run.
    
7. <mark>Kubelet</mark>: The kubelet is responsible for managing the containers on a worker node, ensuring that they are running correctly and healthily.
    
8. <mark>Container runtime</mark>: The container runtime is responsible for running the containers on the worker nodes.
    

### **Control Plane**

The control plane is responsible for managing the Kubernetes cluster's overall state and consists of several components, including the API server, etcd, scheduler, and controller manager.

The API server provides a way for users to interact with the cluster and perform various operations, such as deploying and scaling applications. etcd stores the configuration data and state information for the Kubernetes cluster, while the scheduler is responsible for scheduling containers onto the worker nodes based on available resources and other constraints. The controller manager is responsible for managing the different controllers that are responsible for various cluster-level functions, such as managing nodes and services.

### **Difference between kubectl and kubelet**

kubectl is a command-line tool that allows users to interact with the Kubernetes API and perform various operations, such as deploying and scaling applications. Kubelet, on the other hand, runs on each worker node and is responsible for managing the containers on that node, ensuring that they are running correctly and healthy.

### **Role of the API server**

The API server is responsible for exposing the Kubernetes API, which allows users to interact with the cluster and perform various operations, such as deploying and scaling applications. It acts as the front-end interface for the control plane and manages the cluster's overall state. The API server receives RESTful requests and updates from the kubectl tool and other Kubernetes components and then communicates with etcd to persist the changes to the cluster's configuration data.

The API server also provides security features, such as authentication and authorization, to control access to the cluster's resources. It authenticates users, checks their credentials, and authorizes their access to Kubernetes objects based on their roles and permissions.

In summary, Kubernetes architecture provides a robust and scalable platform for managing containerized workloads and services. It comprises a master node and worker nodes that form a cluster, and the control plane is responsible for managing the cluster state. Kubernetes offers several benefits, such as scalability, high availability, portability, resource efficiency, and simplified deployment. By understanding the fundamentals of Kubernetes architecture, developers and system administrators can build and manage containerized applications effectively.

Additionally, the API server acts as the entry point for external components, such as custom controllers and third-party tools, to interact with the Kubernetes cluster. These components can use the Kubernetes API to access and manage the cluster's resources, which enables the creation of custom integrations and automation workflows.

The API server also plays a critical role in managing the cluster's resources and ensuring that the desired state of the system matches the actual state. It continuously monitors the state of the objects in the etcd datastore and notifies the appropriate components when changes occur. For example, if a user deploys a new application using kubectl, the API server updates the etcd datastore with the new application's configuration data and notifies the scheduler to deploy the application to a worker node.

In summary, the API server is a critical component of the Kubernetes architecture that manages the cluster's overall state, exposes the Kubernetes API, provides security features, and enables custom integrations and automation workflows. It ensures that the desired state of the system matches the actual state and notifies the appropriate components when changes occur.

### **What is the role of kubelet?**

Kubelet is a node-level component in the Kubernetes architecture responsible for managing the containers running on a worker node. It ensures that the containers are running correctly and have the necessary resources to function. Kubelet interacts with the container runtime, such as Docker or CRI-O, to manage the containers and their resources.

Kubelet receives instructions from the control plane, primarily from the scheduler, about which containers to run on the node and how many resources to allocate to each container. It then communicates with the container runtime to start, stop, and manage the containers accordingly.

Kubelet also monitors the health of the containers and reports any issues back to the control plane. For example, if a container crashes or stops responding, kubelet will restart the container or notify the control plane to reschedule it on another node. Additionally, kubelet ensures that the containers' resource usage remains within the specified limits to prevent resource contention and ensure the overall stability of the cluster.

In summary, kubelet is a critical component of the Kubernetes architecture that manages the containers running on a worker node. It interacts with the container runtime, receives instructions from the control plane, monitors container health, and ensures that the containers have the necessary resources to function properly.

### **What are the differences between kubectl and kubelet?**

Kubectl and kubelet are two components of the Kubernetes architecture with different roles and responsibilities.

Kubectl is a command-line tool used to interact with the Kubernetes API server and manage the cluster's resources. It provides a simple and intuitive interface for deploying, scaling, and managing containerized applications and services. Kubectl can be used to perform a wide range of tasks, such as creating and updating deployments, checking the status of pods, and viewing logs.

Kubelet, on the other hand, is a node-level component responsible for managing the containers running on a worker node. It receives instructions from the control plane, interacts with the container runtime, and monitors container health.

In summary, kubectl is a tool used to manage the Kubernetes cluster's resources, while kubelet is a node-level component responsible for managing containers running on a worker node.

### **What is etcd in Kubernetes architecture?**

Etcd is a distributed key-value store used by the control plane to store the Kubernetes cluster's configuration data. It serves as the single source of truth for the cluster's state and provides a reliable and consistent way to store and retrieve data.

Etcd uses the Raft consensus algorithm to ensure that the data stored in the datastore is consistent and up-to-date across all nodes in the cluster. The Raft algorithm guarantees that changes made to the datastore are only committed once a quorum of nodes has acknowledged them, which ensures that the data is not lost or corrupted.

In summary, etcd is a critical component of the Kubernetes architecture that provides a reliable and consistent way to store the cluster's configuration data. It uses the Raft consensus algorithm to ensure data consistency and reliability across the cluster.

## 3\. Motivation behind building a Kubernetes Cluster on AWS

1. Scaling and managing containerized applications can be a complex task, especially as the number of containers and nodes increases. Kubernetes provides a robust platform for container orchestration, allowing us to automate deployment, scaling, and management of containerized applications with ease.
    
2. As businesses move towards cloud-native applications and microservices, the need for a scalable and resilient platform becomes critical. Kubernetes provides a proven framework for building, deploying, and managing cloud-native applications, making it an ideal choice for modern IT infrastructure.
    
3. AWS offers a comprehensive set of cloud services that provide virtually unlimited compute, storage, and network resources. By combining AWS with Kubernetes, we can leverage the power of the cloud to build a highly available and scalable container platform that can meet the demands of any workload.
    
4. Kubernetes on AWS provides a flexible and cost-effective platform for building, deploying, and managing containerized applications. Whether you're running a small test environment or a large-scale production deployment, Kubernetes on AWS offers a consistent and reliable platform that can adapt to your changing needs.
    

# <mark>Section 1: Setting up a Kubernetes Cluster with MiniKube on AWS</mark>

## 1.Why Minicube

1. MiniKube is a lightweight and easy-to-use tool that allows you to run Kubernetes locally on your machine. It provides a single-node Kubernetes cluster that can be used for development, testing, and learning purposes.
    
2. MiniKube is an ideal tool for setting up a Kubernetes environment quickly and easily. It eliminates the need for a complex and time-consuming setup process, making it an excellent choice for developers who want to experiment with Kubernetes.
    
3. One of the main benefits of MiniKube is its portability. Since it runs locally on your machine, you can easily test and develop your applications without the need for a dedicated Kubernetes cluster or cloud infrastructure.
    
4. For this project, I chose MiniKube because it allowed me to set up a Kubernetes cluster quickly and easily on my AWS EC2 instance. It provided me with a simple and efficient way to experiment with Kubernetes, test out different configurations, and troubleshoot any issues that arose during the deployment process.
    
5. Another reason why I chose MiniKube for this project is its ease of use. Its simple command-line interface and comprehensive documentation made it easy to get started and navigate through the various features and functionalities of Kubernetes.
    

## 2.Steps to **Install minikube on your local:**

here are the steps to install Minikube on an AWS EC2 instance running Ubuntu, using Docker as the driver:

1. Launch an EC2 instance:
    
    * Go to the AWS Console and log in to your account.
        
    * Click on the "Launch Instance" button to start the instance creation wizard.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682935872475/a1531db3-7e6b-4739-9b34-eefce3d39749.png?auto=compress,format&format=webp align="left")
        
    * Choose an Ubuntu Server AMI and select the t2.medium instance type with 4GB RAM and 2 CPU.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682935939358/43659727-4836-4b34-8493-6abccde73d64.png?auto=compress,format&format=webp align="left")
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682936000254/d6c30bb7-9e5b-43c4-8bf5-842e9a9ecc5e.png?auto=compress,format&format=webp align="left")
        
    * Follow the wizard steps to configure the instance details, storage, security group, and key pair.
        
    * Review your configuration and launch the instance.
        
2. Connect to your EC2 instance:
    
    * Once the instance is launched, you need to connect to it through SSH.
        
    * Open your terminal or command prompt and navigate to the directory where your key pair is saved, or else connect directly.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682936238589/fce66d30-8661-4ec2-9ea0-bc75d9200d7d.png?auto=compress,format&format=webp align="left")
        
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
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682936390424/e2f7d1c1-1623-4619-8c62-d2c51e16af1a.png?auto=compress,format&format=webp align="left")
        
4. Install Minikube:
    
    * To install Minikube, use the following command:
        
        ```bash
          curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
          sudo install minikube-linux-amd64 /usr/local/bin/minikube
        ```
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682936471161/fe96a8d7-ab78-4d14-805d-d4316b7c45f1.png?auto=compress,format&format=webp align="left")
        
5. Start Minikube:
    
    * To start Minikube, use the following command:
        
        ```bash
          minikube start --driver=docker
        ```
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682936607167/eb05bf9a-9af8-43dc-84fb-d5b7d11f47db.png?auto=compress,format&format=webp align="left")
        
    * This command will start a single-node Kubernetes cluster on your Ubuntu instance using Docker as the driver.
        
6. Verify that Minikube is running:
    
    * Use the following command to verify that Minikube is running:
        
        ```bash
          kubectl version
        ```
        
    * This command will show the version of Kubernetes that Minikube is running.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682936753264/a0094fde-bb52-4288-93e8-ea3ae600c8b6.png?auto=compress,format&format=webp align="left")
        

# <mark>Section 2: Deploying Django Todo App in Kubernetes Pods and Managing Cluster</mark>

## 1.Role of Docker Containers and Kubernetes Pods in this project

Docker Containers are used to package your application and its dependencies into a portable, self-contained unit that can run on any machine with Docker installed. In this project, We used Docker Containers to package our Django Todo application and its dependencies so that they can be easily deployed and managed in a Kubernetes Cluster.

Kubernetes Pods are the smallest deployable units in a Kubernetes Cluster. They encapsulate one or more containers and their shared resources, such as network and storage. In this project, We deployed our Docker Containers as Kubernetes Pods in the Kubernetes Cluster. Each Pod contained one or more containers, with each container running a specific component of your Django Todo application.

Kubernetes Pods provide several benefits, such as:

* They enable easy scaling of application components by allowing you to add or remove containers from Pods as needed.
    
* They provide a higher level of abstraction than individual containers, making it easier to manage complex applications with multiple components.
    
* They ensure that containers in a Pod share the same network and storage resources, making it easier to manage these resources across containers.
    

Overall, Docker Containers and Kubernetes Pods play a crucial role in deploying and managing applications in a Kubernetes Cluster, enabling you to package and deploy your application components in a portable and scalable way.

## 2.Importance of deployment, replication, auto-healing, and auto-scaling in Kubernetes

1. <mark>Deployment</mark>: Deployments in Kubernetes define the desired state of your application and the way it should be managed. Deployments provide a declarative way to specify the desired number of replicas of your application, as well as the update strategy to use when rolling out changes. Deployments also allow for rolling back to a previous version of the application if there are issues with the new version. By using Deployments, you can ensure that your application is running the desired version, with the desired number of replicas, and with minimal downtime.
    
2. <mark>Replication</mark>: Kubernetes provides replication of Pods to ensure that the desired number of replicas of your application is running. Replication Controllers, which are now replaced by ReplicaSets, are responsible for maintaining a specified number of replicas of Pods. By ensuring that multiple replicas of your application are running, Kubernetes provides high availability and fault tolerance. If a Pod fails or becomes unavailable, the Replication Controller will automatically create a new replica to replace it.
    
3. <mark>Auto-healing</mark>: Kubernetes includes self-healing mechanisms that automatically detect and recover from failures. If a Pod fails, Kubernetes automatically restarts the Pod, ensuring that the desired number of replicas of your application is always running. Kubernetes also supports liveness and readiness probes, which are used to detect whether a container is running and ready to accept traffic. If a container is not ready, Kubernetes will automatically restart the container.
    
4. <mark>Auto-scaling</mark>: Kubernetes provides horizontal scaling capabilities that allow you to scale your application based on demand. By using Kubernetes' auto-scaling features, you can automatically adjust the number of replicas of your application based on metrics such as CPU utilization or network traffic. This helps ensure that your application is able to handle increased traffic without manual intervention.
    

## 3.Steps to manage these features for your Kubernetes Cluster

1. Clone the django-todo-cicd repository from Github.
    
    * Django-todo-cicd is a sample web application that we will be deploying on Kubernetes. You can clone the repository from Github using the `git clone` [`https://github.com/Dhananjaykul/django-todo-cicd.git`](https://github.com/Dhananjaykul/django-todo-cicd.git) command.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683002875542/1b9af8d4-b148-4924-82ea-5a79fc680d36.png?auto=compress,format&format=webp align="left")
        
2. Build the Docker image.
    
    * Navigate to the cloned repository and build the Docker image using the `docker build -t . django-todo-cicd:latest` command.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683003175793/a779cbdd-836a-4ef0-b4e5-10b96808dbcf.png?auto=compress,format&format=webp align="left")
        
3. Run the container on port 8000 and verify the app is running using the `curl -L` [`http://172.31.89.215:8000`](http://172.31.89.215:8000) command.
    
    * Run the Docker container using the `docker run -d -p 8000:8000 django-todo-cicd:latest` command.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683003403061/a28871d0-51c3-42b3-9c8a-3c9da6534589.png?auto=compress,format&format=webp align="left")
        
    * Verify that the application is running by using the `curl -L` [`http://172.31.89.215:8000`](http://172.31.89.215:8000) command.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683003456683/7d8b2699-72b3-4347-8d70-4b64100892fd.png?auto=compress,format&format=webp align="left")
        
4. Create a new directory called k8s.
    
    * Create a new directory called k8s in the same directory where the django-todo-cicd repository is located.
        
5. Navigate to the k8s directory.
    
    * Navigate to the k8s directory using the `cd k8s` command.
        
6. Push the Docker image to your Dockerhub account.
    
    * Push the Docker image to your Dockerhub account using the `docker push django-todo-cicd:latest` command.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683004443191/f83854e0-3d84-4ed9-9aaf-23633f330e4a.png?auto=compress,format&format=webp align="left")
        
7. Create a new pod.yaml file.
    
    * Create a new file called pod.yaml using your preferred text editor.
        
    * Copy the sample pod.yaml configuration from the official Kubernetes documentation, then replace the image name with your own Dockerhub image name.
        
        Create a `pod.yaml` file in the `k8s` directory with the following contents:
        

```bash
    apiVersion: v1
    kind: Pod
    metadata:
      name: todo-pod
    spec:
      containers:
        - name: todo-app
          image: dhananjaykulkarni/django-todo-cicd:latest
          ports:
            - containerPort: 8000
```

Here, we are creating a pod with the `todo-app` container image that we previously pushed to Docker Hub.

1. Kill the previously made container.
    
    * Kill the previously made container using the `docker ps` command to find the container ID, then the `docker kill <container-id>` command to stop it
        
2. Apply the pod.yaml file using the `kubectl apply -f pod.yaml` command.
    

* Apply the pod.yaml file using the `kubectl apply -f pod.yaml` command. This will create a new pod based on the configuration specified in the pod.yaml file.
    

1. Use the `kubectl get pods` command to verify the pod is running.
    

* Use the `kubectl get pods` command to check that the pod is running.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683004750756/3e24a0a3-1125-455f-85fc-d6d8b541f0b1.png?auto=compress,format&format=webp align="left")
    

1. Create a `deployment.yaml` file with the following contents:
    

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
        image: dhananjaykulkarni/django-todo-cicd:latest
        ports:
        - containerPort: 8000
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683004921416/5b54e96a-9ad2-4e1e-a6f9-7a1020294d44.png?auto=compress,format&format=webp align="left")

Here, we are creating a deployment with two replicas of the `todo-app` container image that we previously pushed to Docker Hub.

1. Apply the deployment to your Kubernetes cluster by running the following command:
    

```bash
kubectl apply -f deployment.yaml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683004996641/1e4a64f8-176c-4cd8-9984-9fa70e2b695c.png?auto=compress,format&format=webp align="left")

This will create the deployment and start the specified number of replicas.

1. To check the status of the deployment and its replicas, run the following commands:
    

```bash
kubectl get deployments
kubectl get pods
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683005056857/d67341cf-a183-4a48-9767-7266b090e3d6.png?auto=compress,format&format=webp align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683005110553/6bd5071f-d58a-4750-862e-93df3b900a94.png?auto=compress,format&format=webp align="left")

You should see two pods running the `todo-app` container image.

1. To demonstrate the auto-healing feature, kill one of the running pods by running the following command:
    

```bash
kubectl delete pod todo-deployment-7987844987-88mng
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683005217010/f6fa307b-9e2e-46ba-a5f1-387e2656ca7d.png?auto=compress,format&format=webp align="left")

Kubernetes will automatically create a new pod to replace the one that was killed.

1. To demonstrate the auto-scaling feature, increase the number of replicas in the deployment by running the following command:
    

```bash
kubectl scale deployment todo-deployment --replicas=4
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683005433779/eb4e4ed7-3078-41ac-a605-34d9497de0f5.png?auto=compress,format&format=webp align="left")

This will increase the number of replicas to 4.

1. To check the status of the deployment and its replicas again, run the following commands:
    

```bash
kubectl get deployments
kubectl get pods
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683005482051/94653f95-17ca-4ccf-b3d6-f49112b868be.png?auto=compress,format&format=webp align="left")

You should now see four pods running the `todo-app` container image.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683005552635/281aa55c-e935-4c39-abd9-fb65eeca7f61.png?auto=compress,format&format=webp align="left")

This is how I successfully created a deployment file to deploy a sample `todo-app` on Kubernetes using auto-healing and auto-scaling features.

# <mark>Section 3: Managing Network and Services with Host IP Allocation through Proxy on AWS EC2 and Route53</mark>

## 1.Importance of managing network and services in Kubernetes

Managing network and services in Kubernetes is important because it allows applications to communicate with each other and with the outside world, and provides a way to expose the application to external traffic.

Kubernetes provides several ways to manage networking and services, including:

1. <mark>Service discovery</mark>: Kubernetes uses DNS to provide a dynamic, load-balanced, and scalable way to discover services. Services are assigned a stable IP address and DNS name, which allows other Pods in the Cluster to access them by name.
    
2. <mark>Load balancing</mark>: Kubernetes provides built-in load balancing for services, distributing traffic evenly among the available Pods. This helps ensure that the application is highly available and can handle increased traffic.
    
3. <mark>Ingress</mark>: Ingress is a Kubernetes resource that allows you to expose HTTP and HTTPS routes from outside the Cluster to services within the Cluster. Ingress allows you to define rules for routing traffic to different services based on the URL path, host, or other criteria.
    
4. <mark>Network policies</mark>: Kubernetes provides network policies that allow you to define rules for controlling inbound and outbound network traffic to Pods. Network policies can be used to enforce security and compliance requirements, and to limit access to sensitive resources.
    

## 2.The process of managing network and services with host IP allocation through proxy on AWS EC2 and Route53

detailed steps with commands:

1. To list the Pods with their IPs, run the following command:
    
    ```bash
    kubectl get pods -o wide
    ```
    
    This will show a table of all the Pods in the Kubernetes Cluster, along with their IP addresses.
    
2. To test accessing the Pod's IP address directly, run the following command:
    
    ```bash
    curl -L <Pod-IP>
    ```
    
    This will likely fail, since the Pod is not exposed outside of the Kubernetes Cluster.
    
3. To expose the Pod as a Service, create a new YAML file called `service.yaml` with the following content:
    
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
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683192667055/1db17136-b1ee-4bc4-8fd8-585c4e4d43d6.png align="center")
    
    This will create a new Kubernetes Service object named `todo-service` that maps port 80 of the Service to port 8000 of the Pods, and exposes the Service on port 30007 of the Kubernetes Nodes.
    
4. Apply the `service.yml` file to the Kubernetes Cluster using the following command:
    
    ```bash
    kubectl apply -f service.yml
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683193395264/256f5c94-6fed-450c-8799-8a21dd6acc1e.png align="center")
    
    This will create the new Service object in the Kubernetes Cluster.
    
5. To get the URL for the new Service, run the following command:
    
    ```bash
    minikube service todo-service --url
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683193476049/0dfd4a94-e37c-44c5-b316-16afce1b09e3.png align="center")
    
    This will display the URL for the new Service, which should look something like `http://<Node-IP>:30007`.
    
6. To access the new Service using the URL, run the following command:
    
    ```bash
    curl -L http://192.168.49.2:30007
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683193579869/d3a692f6-1e94-4090-ba2c-406040cee1a1.png align="center")
    
    This should return the output of the Django Todo app as shown above.
    
7. To map the IP address to a hostname, edit the `/etc/hosts` file using the following command:
    
    ```bash
    sudo vim /etc/hosts
    ```
    
    Then add a new line to the file with the IP address and hostname, like this:
    
    ```bash
    <Node-IP> todo-app.com
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683193707409/2fb5c20e-7ab9-43da-a36d-1356760e9c16.png align="center")
    
    This will map the IP address to the hostname [`todo-app.com`](http://todo-app.com).
    

After completing these steps, you should be able to access the Django Todo app using the URL [`http://todo-app.com`](http://todo-app.com) in a web browser.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683194012864/7e36fbfa-4b9c-44d7-ad5a-4b76088f5c55.png align="center")

🎉🎉🎉🎉🎉🎉🎉🎉Yess its Done!!!🎉🎉🎉🎉🎉🎉🎉🎉

<mark>Lets talk about this error below</mark>: Docker was out of space so was creating an error starting Minicube so what i did was delete unwanted unused data using command

```bash
docker system prune
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683193061045/130e4ed3-f9b7-4abc-bdcc-21788c3580a6.png align="center")

## **Code Availability**

The code for this project is available on GitHub at [click here](https://github.com/Dhananjaykul/django-todo-cicd) . The repository includes all the necessary files and documentation to deploy the project on your own Kubernetes cluster. Feel free to fork the repository and make your own modifications to the code.

# <mark>Conclusion:</mark>

In this project, I demonstrated the process of building a Kubernetes cluster on AWS from scratch with MiniKube. I also explained the process of setting up Docker containers for a Django Todo application in Kubernetes pods, as well as managing deployment, replication, auto-healing, and auto-scaling in Kubernetes.

Also emphasized the importance of managing network and services in Kubernetes and explained the process of managing network and services with host IP allocation through proxy on AWS EC2 and Route53.

Some key takeaways from this project are the importance of containerization and orchestration for modern application development, the advantages of using Kubernetes for managing containers at scale, and the benefits of using cloud platforms like AWS for deploying Kubernetes clusters.