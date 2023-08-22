---
title: "Launching your Kubernetes Cluster with Deployment"
seoTitle: "Deploying a To-Do App on Kubernetes with Auto-Healing  and Auto-scale"
seoDescription: "Follow step-by-step instructions to create a deployment file, build and push images, and manage your deployment, replication, and auto-scaling."
datePublished: Tue May 02 2023 06:04:54 GMT+0000 (Coordinated Universal Time)
cuid: clh5v7hls000b09l4el231g2v
slug: launching-your-kubernetes-cluster-with-deployment
tags: deployment, kubernetes, devops, scalability, 90daysofdevops

---

If you're new to Kubernetes, you may be wondering what "deployment" means in the context of this powerful container orchestration system. Simply put, deployment is the process of updating or rolling out new versions of an application in a Kubernetes cluster. In this article, we'll explore deployment in Kubernetes and how it works.

## <mark>What is Deployment in Kubernetes?</mark>

In Kubernetes, a deployment is a high-level abstraction that allows you to declaratively manage your application's lifecycle. You define the desired state of your application, and Kubernetes takes care of making it happen. A deployment consists of a set of instructions for creating and updating replica sets, which are the objects that actually manage the running instances of your application.

Deployments in Kubernetes are essential because they provide several benefits. First, they allow you to easily scale your application up or down, depending on demand. Second, they provide rolling updates, which means that new versions of your application can be deployed without any downtime. Finally, deployments ensure that your application runs consistently across multiple nodes in your cluster, improving reliability and availability.

## <mark>How Deployment Works in Kubernetes</mark>

At a high level, a deployment in Kubernetes works like this:

1. You define a deployment configuration in a YAML file, which specifies the desired state of your application.
    
2. You apply the configuration to your Kubernetes cluster using the kubectl apply command.
    
3. Kubernetes creates a replica set based on the configuration, which manages the running instances of your application.
    
4. As your application needs to be updated or scaled, you modify the deployment configuration and apply it again.
    
5. Kubernetes automatically updates the replica set to match the new desired state of your application, rolling out any changes without downtime.
    

Let's look at an example deployment YAML file to see how this works in practice:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp
        image: myapp:latest
        ports:
        - containerPort: 8080
```

This YAML file defines a deployment named `myapp-deployment`, which specifies that three replicas of the `myapp` container should be created. The selector and template sections ensure that the deployment only manages pods with the `app: myapp` label, and the container definition specifies the image to use and the port to expose.

To apply this configuration to your Kubernetes cluster, you can save it to a file (e.g., `myapp-deployment.yaml`) and run the following command:

```bash
kubectl apply -f myapp-deployment.yaml
```

Kubernetes will create the replica set and manage the running instances of your application based on the configuration you specified. If you need to update the application, you can modify the YAML file and apply it again, and Kubernetes will handle the rolling update automatically.

## <mark>Task 1 : Add a deployment.yml file. Apply the deployment to your k8s (minikube) cluster by command </mark> `kubectl apply -f deployment.yml`

Here are the detailed steps to create a Deployment file to deploy a sample todo-app on Kubernetes with Auto-healing and Auto-scaling features:

1. Install Minikube and start it.
    
    * Minikube is a tool that allows you to run a single-node Kubernetes cluster locally. You can download it from the official Minikube website, then start it using the `minikube start` command.
        
        [Click to Cheack previous Blog](https://dhananjaykulkarni.hashnode.dev/launching-your-first-kubernetes-cluster-with-nginx-running)
        
2. Clone the django-todo-cicd repository from Github.
    
    * Django-todo-cicd is a sample web application that we will be deploying on Kubernetes. You can clone the repository from Github using the `git clone` [`https://github.com/Dhananjaykul/django-todo-cicd.git`](https://github.com/Dhananjaykul/django-todo-cicd.git) command.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683002875542/1b9af8d4-b148-4924-82ea-5a79fc680d36.png align="center")
        
3. Build the Docker image.
    
    * Navigate to the cloned repository and build the Docker image using the `docker build -t . django-todo-cicd:latest` command.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683003175793/a779cbdd-836a-4ef0-b4e5-10b96808dbcf.png align="center")
        
4. Run the container on port 8000 and verify the app is running using the `curl -L` [`http://172.31.89.215:8000`](http://ip:8000) command.
    
    * Run the Docker container using the `docker run -d -p 8000:8000 django-todo-cicd:latest` command.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683003403061/a28871d0-51c3-42b3-9c8a-3c9da6534589.png align="center")
        
    * Verify that the application is running by using the `curl -L` [`http://172.31.89.215:8000`](http://ip:8000) command.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683003456683/7d8b2699-72b3-4347-8d70-4b64100892fd.png align="center")
        
5. Create a new directory called k8s.
    
    * Create a new directory called k8s in the same directory where the django-todo-cicd repository is located.
        
6. Navigate to the k8s directory.
    
    * Navigate to the k8s directory using the `cd k8s` command.
        
7. Push the Docker image to your Dockerhub account.
    
    * Push the Docker image to your Dockerhub account using the `docker push django-todo-cicd:latest` command.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683004443191/f83854e0-3d84-4ed9-9aaf-23633f330e4a.png align="center")
        
8. Create a new pod.yaml file.
    
    * Create a new file called pod.yaml using your preferred text editor.
        
    * Copy the sample pod.yaml configuration from the official Kubernetes documentation, then replace the image name with your own Dockerhub image name.
        
        Create a `pod.yaml` file in the `k8s` directory with the following contents:
        
    
    ```yaml
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
    
9. Kill the previously made container.
    
    * Kill the previously made container using the `docker ps` command to find the container ID, then the `docker kill <container-id>` command to stop it
        
10. Apply the pod.yaml file using the `kubectl apply -f pod.yaml` command.
    

* Apply the pod.yaml file using the `kubectl apply -f pod.yaml` command. This will create a new pod based on the configuration specified in the pod.yaml file.
    

1. Use the `kubectl get pods` command to verify the pod is running.
    

* Use the `kubectl get pods` command to check that the pod is running.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683004750756/3e24a0a3-1125-455f-85fc-d6d8b541f0b1.png align="center")
    

1. Create a `deployment.yaml` file with the following contents:
    

```yaml
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

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683004921416/5b54e96a-9ad2-4e1e-a6f9-7a1020294d44.png align="center")

Here, we are creating a deployment with two replicas of the `todo-app` container image that we previously pushed to Docker Hub.

1. Apply the deployment to your Kubernetes cluster by running the following command:
    

```yaml
kubectl apply -f deployment.yaml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683004996641/1e4a64f8-176c-4cd8-9984-9fa70e2b695c.png align="center")

This will create the deployment and start the specified number of replicas.

1. To check the status of the deployment and its replicas, run the following commands:
    

```yaml
kubectl get deployments
kubectl get pods
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683005056857/d67341cf-a183-4a48-9767-7266b090e3d6.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683005110553/6bd5071f-d58a-4750-862e-93df3b900a94.png align="center")

You should see two pods running the `todo-app` container image.

1. To demonstrate the auto-healing feature, kill one of the running pods by running the following command:
    

```yaml
kubectl delete pod todo-deployment-7987844987-88mng
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683005217010/f6fa307b-9e2e-46ba-a5f1-387e2656ca7d.png align="center")

Kubernetes will automatically create a new pod to replace the one that was killed.

1. To demonstrate the auto-scaling feature, increase the number of replicas in the deployment by running the following command:
    

```yaml
kubectl scale deployment todo-deployment --replicas=4
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683005433779/eb4e4ed7-3078-41ac-a605-34d9497de0f5.png align="center")

This will increase the number of replicas to 4.

1. To check the status of the deployment and its replicas again, run the following commands:
    

```yaml
kubectl get deployments
kubectl get pods
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683005482051/94653f95-17ca-4ccf-b3d6-f49112b868be.png align="center")

You should now see four pods running the `todo-app` container image.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683005552635/281aa55c-e935-4c39-abd9-fb65eeca7f61.png align="center")

🥳🥳🥳🥳🥳🥳🥳🥳🥳🎉🎉🎉✨✨✨✨✨✨✨✨🎉🎉🎉🎉🎉🎉🎉🎉

By following these steps, you have successfully created a deployment file to deploy a sample `todo-app` on Kubernetes using auto-healing and auto-scaling features.

## Conclusion

Deployments are a crucial part of managing applications in Kubernetes. They allow you to declaratively manage your application's lifecycle, including scaling, updating, and ensuring consistency across multiple nodes in your cluster. By defining a deployment configuration and applying it to your cluster, you can take advantage of these benefits and ensure that your application is always running smoothly.