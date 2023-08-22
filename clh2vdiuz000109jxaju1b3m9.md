---
title: "Kubernetes Architecture: Understanding the Fundamentals"
seoTitle: "A Beginner's Guide to Kubernetes Architecture:"
seoDescription: "Learn about Kubernetes architecture, including the control plane, worker nodes, kubelet, etcd, and more. Discover the benefits of using Kubernetes."
datePublished: Sun Apr 30 2023 03:46:17 GMT+0000 (Coordinated Universal Time)
cuid: clh2vdiuz000109jxaju1b3m9
slug: kubernetes-architecture-understanding-the-fundamentals
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1682824736731/2021d1f7-500b-4cd7-8621-c4b39dcf19ff.jpeg
tags: kubernetes, devops, containers, 90daysofdevops, trainwithshubham

---

Kubernetes, commonly abbreviated as k8s, is an open-source platform for managing containerized workloads and services. It was initially developed by Google and later donated to the Cloud Native Computing Foundation (CNCF). Kubernetes automates the deployment, scaling, and management of containerized applications, making it easier to manage large and complex container environments.

# Benefits of Using Kubernetes

Kubernetes offers numerous benefits for developers and system administrators, including:

1. <mark>Scalability</mark>: Kubernetes can automatically scale the number of containers up or down based on the demand, ensuring that the applications always have the necessary resources to run.
    
2. <mark>High availability</mark>: Kubernetes supports high availability by automatically distributing workloads across multiple nodes, thereby reducing the risk of downtime.
    
3. <mark>Portability</mark>: Kubernetes allows applications to be easily moved between different environments, such as on-premise data centers or public cloud platforms.
    
4. <mark>Resource efficiency</mark>: Kubernetes helps optimize resource utilization by scheduling containers on available resources and reducing resource wastage.
    
5. <mark>Simplified deployment</mark>: Kubernetes simplifies the deployment process by automating container configuration, application updates, and rollbacks.
    

# Kubernetes Architecture

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
    

## **Control Plane**

The control plane is responsible for managing the Kubernetes cluster's overall state and consists of several components, including the API server, etcd, scheduler, and controller manager.

The API server provides a way for users to interact with the cluster and perform various operations, such as deploying and scaling applications. etcd stores the configuration data and state information for the Kubernetes cluster, while the scheduler is responsible for scheduling containers onto the worker nodes based on available resources and other constraints. The controller manager is responsible for managing the different controllers that are responsible for various cluster-level functions, such as managing nodes and services.

## **Difference between kubectl and kubelet**

kubectl is a command-line tool that allows users to interact with the Kubernetes API and perform various operations, such as deploying and scaling applications. Kubelet, on the other hand, runs on each worker node and is responsible for managing the containers on that node, ensuring that they are running correctly and healthy.

## **Role of the API server**

The API server is responsible for exposing the Kubernetes API, which allows users to interact with the cluster and perform various operations, such as deploying and scaling applications. It acts as the front-end interface for the control plane and manages the cluster's overall state. The API server receives RESTful requests and updates from the kubectl tool and other Kubernetes components and then communicates with etcd to persist the changes to the cluster's configuration data.

The API server also provides security features, such as authentication and authorization, to control access to the cluster's resources. It authenticates users, checks their credentials, and authorizes their access to Kubernetes objects based on their roles and permissions.

In summary, Kubernetes architecture provides a robust and scalable platform for managing containerized workloads and services. It comprises a master node and worker nodes that form a cluster, and the control plane is responsible for managing the cluster state. Kubernetes offers several benefits, such as scalability, high availability, portability, resource efficiency, and simplified deployment. By understanding the fundamentals of Kubernetes architecture, developers and system administrators can build and manage containerized applications effectively.

Additionally, the API server acts as the entry point for external components, such as custom controllers and third-party tools, to interact with the Kubernetes cluster. These components can use the Kubernetes API to access and manage the cluster's resources, which enables the creation of custom integrations and automation workflows.

The API server also plays a critical role in managing the cluster's resources and ensuring that the desired state of the system matches the actual state. It continuously monitors the state of the objects in the etcd datastore and notifies the appropriate components when changes occur. For example, if a user deploys a new application using kubectl, the API server updates the etcd datastore with the new application's configuration data and notifies the scheduler to deploy the application to a worker node.

In summary, the API server is a critical component of the Kubernetes architecture that manages the cluster's overall state, exposes the Kubernetes API, provides security features, and enables custom integrations and automation workflows. It ensures that the desired state of the system matches the actual state and notifies the appropriate components when changes occur.

## **What is the role of kubelet?**

Kubelet is a node-level component in the Kubernetes architecture responsible for managing the containers running on a worker node. It ensures that the containers are running correctly and have the necessary resources to function. Kubelet interacts with the container runtime, such as Docker or CRI-O, to manage the containers and their resources.

Kubelet receives instructions from the control plane, primarily from the scheduler, about which containers to run on the node and how many resources to allocate to each container. It then communicates with the container runtime to start, stop, and manage the containers accordingly.

Kubelet also monitors the health of the containers and reports any issues back to the control plane. For example, if a container crashes or stops responding, kubelet will restart the container or notify the control plane to reschedule it on another node. Additionally, kubelet ensures that the containers' resource usage remains within the specified limits to prevent resource contention and ensure the overall stability of the cluster.

In summary, kubelet is a critical component of the Kubernetes architecture that manages the containers running on a worker node. It interacts with the container runtime, receives instructions from the control plane, monitors container health, and ensures that the containers have the necessary resources to function properly.

## **What are the differences between kubectl and kubelet?**

Kubectl and kubelet are two components of the Kubernetes architecture with different roles and responsibilities.

Kubectl is a command-line tool used to interact with the Kubernetes API server and manage the cluster's resources. It provides a simple and intuitive interface for deploying, scaling, and managing containerized applications and services. Kubectl can be used to perform a wide range of tasks, such as creating and updating deployments, checking the status of pods, and viewing logs.

Kubelet, on the other hand, is a node-level component responsible for managing the containers running on a worker node. It receives instructions from the control plane, interacts with the container runtime, and monitors container health.

In summary, kubectl is a tool used to manage the Kubernetes cluster's resources, while kubelet is a node-level component responsible for managing containers running on a worker node.

## **What is etcd in Kubernetes architecture?**

Etcd is a distributed key-value store used by the control plane to store the Kubernetes cluster's configuration data. It serves as the single source of truth for the cluster's state and provides a reliable and consistent way to store and retrieve data.

Etcd uses the Raft consensus algorithm to ensure that the data stored in the datastore is consistent and up-to-date across all nodes in the cluster. The Raft algorithm guarantees that changes made to the datastore are only committed once a quorum of nodes has acknowledged them, which ensures that the data is not lost or corrupted.

In summary, etcd is a critical component of the Kubernetes architecture that provides a reliable and consistent way to store the cluster's configuration data. It uses the Raft consensus algorithm to ensure data consistency and reliability across the cluster.

## **Conclusion**

In conclusion, Kubernetes is a powerful and flexible platform for container orchestration, providing a robust architecture for managing containerized applications and services. Its architecture comprises a master node and worker nodes that form a cluster, with the control plane responsible for managing the cluster's state. Kubernetes provides several benefits, including scalability, high availability, portability, resource efficiency, and simplified deployment. By understanding the fundamentals of Kubernetes architecture, developers and system administrators can build and manage containerized applications effectively.