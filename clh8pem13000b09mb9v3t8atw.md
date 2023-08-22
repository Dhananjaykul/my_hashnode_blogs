---
title: "Working with Services in Kubernetes"
seoTitle: "Understanding Kubernetes Services: What They Are and How They Work"
seoDescription: "Discover the four different types of services and how they work, along with a step-by-step guide on how to create and apply a Service definition in Kubernet"
datePublished: Thu May 04 2023 05:45:47 GMT+0000 (Coordinated Universal Time)
cuid: clh8pem13000b09mb9v3t8atw
slug: working-with-services-in-kubernetes
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1683178905679/a4fe9eea-a065-4edf-b5f8-2356bc923861.png
tags: opensource, kubernetes, devops, 90daysofdevops, trainwithshubham

---

Kubernetes, also known as K8s, is an open-source platform that automates container orchestration, deployment, and management. It provides a set of powerful primitives to manage distributed systems, including containers, microservices, and cloud-native applications.

One of the most critical components of Kubernetes is its ability to manage services. In this blog post, we will discuss what services are in Kubernetes and how they work.

## What are Services in Kubernetes?

In Kubernetes, a service is an abstraction layer that represents a logical set of pods and provides a stable IP address and DNS name for accessing them. Services enable decoupling of the application layer from the infrastructure layer, providing a consistent way to access pods regardless of their location or number.

Services act as a load balancer for a set of pods and provide a single entry point for accessing the pods. They also provide features such as load balancing, service discovery, and health checking.

## Service Types in Kubernetes

Kubernetes supports four types of services, each with a different purpose:

1. <mark>ClusterIP</mark>: This is the default service type in Kubernetes. It provides a stable IP address and DNS name for accessing pods within the cluster. The ClusterIP service is only accessible from within the cluster.
    
2. <mark>NodePort</mark>: This service type exposes the service on a static port on each node in the cluster. It provides a way to access the service from outside the cluster.
    
3. <mark>LoadBalancer</mark>: This service type provides a load balancer for the service in cloud environments that support load balancers. It automatically creates a load balancer and assigns a public IP address to the service.
    
4. <mark>ExternalName</mark>: This service type provides a way to access an external service by creating a DNS CNAME record. It does not create any endpoints or perform any load balancing.
    

## How do Services work in Kubernetes?

When you create a service in Kubernetes, it creates a virtual IP address and DNS name for accessing the pods. The service then selects a set of pods based on labels and forwards traffic to them using a load balancing algorithm.

When a pod is added or removed from the set, the service automatically updates its list of endpoints. Services also provide health checking by periodically sending requests to the pods to ensure they are still running.

## Task 1 : Create and Apply a Service Definition in Kubernetes

Create a Service definition for your todo-app Deployment in a YAML file. Apply the Service definition to your K8s (minikube) cluster using the `kubectl apply -f service.yml -n <namespace-name>` command. Verify that the Service is working by accessing the todo-app using the Service's IP and Port in your Namespace.

<mark>Step 1: Create a Service definition</mark>

To create a Service definition, you will need to define the following in a YAML file:

* <mark>apiVersion</mark>: The version of the Kubernetes API you are using.
    
* <mark>kind</mark>: The type of Kubernetes object you are creating, in this case a Service.
    
* <mark>metadata</mark>: Information about the Service, such as its name and labels.
    
* <mark>spec</mark>: The Service specification, including the port and targetPort.
    

Here's an example of what your Service definition YAML file might look like:

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
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683177328600/be3dd734-2c1d-417a-802a-41a7e1535fa9.png align="center")

<mark>Step 2: Apply the Service definition</mark>

Once you have created your Service definition YAML file, you can apply it to your K8s (minikube) cluster using the `kubectl apply -f service.yml -n <namespace-name>` command. Make sure to replace `<namespace-name>` with the name of your Namespace.

```bash
kubectl apply -f service.yml -n todo-namespace
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683177389272/20928a9d-0abb-4f87-a0c4-dcb14f1f110f.png align="center")

<mark>Step 3: Verify the Service is working</mark>

To verify that your Service is working, you can access the todo-app using the Service's IP and Port in your Namespace. You can find the IP and Port of your Service by running the following command:

```bash
minikube service todo-service -n todo-namespace --url
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683177459425/ac63a859-3df4-40fb-b910-963a095654f5.png align="center")

This will return the URL you can use to access the todo-app. Copy the URL and paste it into your web browser. If everything is working correctly, you should see the todo-app running in your web browser.Or else use belo command to access

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683177607701/d0c67111-617c-4786-9a4d-8163c484aa6a.png align="center")

That's it! You now know how to create and apply a Service definition in Kubernetes, and how to verify that your Service is working correctly. With this knowledge, you can take your Kubernetes deployment to the next level and build robust, scalable, and secure applications.

## Task-2 : Create a ClusterIP Service for accessing the todo-app from within the cluster

<mark>Create a ClusterIP Service definition for your todo-app Deployment in a YAML file. Apply the ClusterIP Service definition to your K8s (minikube) cluster using the </mark> `kubectl apply -f cluster-ip-service.yml -n <namespace-name>` <mark> command. Verify that the ClusterIP Service is working by accessing the todo-app from another Pod in the cluster in your Namespace.</mark>

Here's an example of what the YAML file for a ClusterIP Service might look like:

```bash
apiVersion: v1
kind: Service
metadata:
  name: todo-service-cluster-ip
  labels:
    app: todo-app
spec:
  selector:
    app: todo-app
  ports:
    - name: http
      port: 80
      targetPort: 8000
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683177700294/9a200a6b-07f5-4094-8c74-db5192a4e2da.png align="center")

In this example, the `metadata` section specifies the name and labels of the Service, and the `spec` section specifies the selector and port configuration. The `selector` field is used to match the Service to the Pods that it should route traffic to, and the `ports` field specifies the port configuration for the Service.

To apply the Service definition to your K8s cluster, save the YAML file with a filename (e.g. `cluster-ip-service.yml`) and use the `kubectl apply` command:

```bash
kubectl apply -f cluster-ip-service.yml -n todo-namespace
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683177749848/ba8be2ff-54f9-4773-b9a4-b1003c3ed52e.png align="center")

To verify that the ClusterIP Service is working, you can create another Pod in the same namespace and try accessing the todo-app using the Service's name as the hostname. For example, if your ClusterIP Service is named `todo-service-cluster-ip`, you can try running the following command in another Pod:

```bash
curl http://todo-service-cluster-ip
```

If the Service is working correctly, you should see the response from the todo-app.

## Task 3 : Create a LoadBalancer Service for accessing the todo-app from outside the cluster

<mark>Create a LoadBalancer Service definition for your todo-app Deployment in a YAML file. Apply the LoadBalancer Service definition to your K8s (minikube) cluster using the </mark> `kubectl apply -f load-balancer-service.yml -n <namespace-name>` <mark> command.Verify that the LoadBalancer Service is working by accessing the todo-app from outside the cluster in your Namespace.</mark>

Create YAML file for a LoadBalancer Service that you can use to access your `todo-app` Deployment from outside the cluster:

```bash
apiVersion: v1
kind: Service
metadata:
  name: todo-service-load-balancer
  labels:
    app: todo-app
spec:
  type: LoadBalancer
  selector:
    app: todo-app
  ports:
    - name: http
      port: 80
      targetPort: 8000
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683178066542/252a3a31-b71f-4fbf-b109-11cfd6a851c4.png align="center")

In this example, the `metadata` section specifies the name and labels of the Service, and the `spec` section specifies the selector and port configuration. The `type` field is set to `LoadBalancer`, which creates a load balancer that can route external traffic to the Service. The `ports` field specifies the port configuration for the Service.

To apply the Service definition to your K8s cluster, save the YAML file with a filename (e.g. `load-balancer-service.yml`) and use the `kubectl apply` command:

```bash
kubectl apply -f load-balancer-service.yml -n todo-namespace
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683178139591/7de48705-1016-4051-b00d-b7e831372b5b.png align="center")

Once the Service is created, you can verify that it's working by accessing the `todo-app` from outside the cluster using the load balancer's IP address and port. If you're using Minikube, you can get the load balancer's IP address by running the following command:

```bash
minikube service todo-service-load-balancer -n todo-namespace --url
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683178231811/c7085ce9-bd2e-4200-9830-59ca675800d2.png align="center")

This command will output the URL that you can use to access the `todo-app` from outside the cluster.

If you're not using Minikube, the process for accessing the `todo-app` from outside the cluster will depend on your specific environment and network setup. However, you can typically access the Service using the load balancer's IP address and port.

## Conclusion

In conclusion, services are a critical component of Kubernetes that enable decoupling of the application layer from the infrastructure layer. They provide a consistent way to access pods and provide features such as load balancing, service discovery, and health checking. Kubernetes supports four types of services, each with a different purpose, and services work by creating a virtual IP address and DNS name for accessing the pods and forwarding traffic to them using a load balancing algorithm.

By understanding what services are in Kubernetes and how they work, you can effectively manage and scale your distributed applications on Kubernetes.