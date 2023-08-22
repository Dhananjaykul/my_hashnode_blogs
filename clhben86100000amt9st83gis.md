---
title: "Managing Persistent Volumes in Your Deployment"
seoTitle: "Managing Persistent Volumes in our Deployment"
seoDescription: "Follow the steps to add a Persistent Volume to a Deployment, access the data from within a Pod, and verify that it is being persisted across restarts."
datePublished: Sat May 06 2023 03:07:51 GMT+0000 (Coordinated Universal Time)
cuid: clhben86100000amt9st83gis
slug: managing-persistent-volumes-in-your-deployment
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1683341862013/e8557e7e-a773-46d4-9fa4-3e0816fb9bf8.png
tags: kubernetes, devops, containerization, 90daysofdevops, trainwithshubham

---

## <mark>What are Persistent Volumes in k8s?</mark>

In Kubernetes, a Persistent Volume (PV) is a cluster-wide storage resource that can be used by pods to persist data beyond the lifetime of the pod. A Persistent Volume is a separate entity from the pod, and its lifecycle is managed independently from the pod.

A Persistent Volume is created by a cluster administrator and made available for use by the cluster's users. Once a Persistent Volume is created, it can be bound to a Persistent Volume Claim (PVC), which is a request for a specific amount of storage that a pod can use. When a pod requests storage using a PVC, the Kubernetes scheduler finds an available Persistent Volume that matches the request, binds the volume to the claim, and mounts the volume in the pod's container.

Persistent Volumes are a way to abstract the underlying storage infrastructure from the pod, allowing the pod to access storage resources in a portable way. This means that pods can be moved between nodes in the cluster, and the storage resources will follow the pod.

Many types of Persistent Volumes can be used in Kubernetes, including network-attached storage (NAS), storage area network (SAN), local storage, and cloud-based storage. Kubernetes also provides a plugin architecture for storage providers, allowing third-party storage systems to be integrated into the Kubernetes cluster.

## <mark>Task 1: Add a Persistent Volume to your Deployment todo app</mark>

Create a Persistent Volume using a file on your node. Create a Persistent Volume Claim that references the Persistent Volume. Update your deployment.yml file to include the Persistent Volume Claim. Apply the updated deployment using the command: `kubectl apply -f deployment.yml`.Verify that the Persistent Volume has been added to your Deployment by checking the status of the Pods and Persistent Volumes in your cluster. Use this commands `kubectl get pods`, `kubectl get pv`

steps to add a Persistent Volume to your Deployment in Kubernetes for a todo app:

1. Create a Persistent Volume using a file on your node:
    

Create a file named `pv.yaml` with the following contents:

```bash
apiVersion: v1
kind: PersistentVolume
metadata:
  name: todo-pv
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: /data/todo
```

This will create a Persistent Volume of 1GB in size and will use the `/data/todo` directory on the node as its storage location.

Apply the Persistent Volume using the command:

```bash
kubectl apply -f pv.yaml
```

1. Create a Persistent Volume Claim that references the Persistent Volume:
    

Create a file named `pvc.yaml` with the following contents:

```bash
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: todo-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
```

This will create a Persistent Volume Claim that requests 1GB of storage with ReadWriteOnce access mode.

Apply the Persistent Volume Claim using the command:

```bash
kubectl apply -f pvc.yaml
```

1. Update your deployment.yml file to include the Persistent Volume Claim:
    

Add the following YAML block to your `deployment.yml` file, under the `spec.template.spec.containers` section:

```bash
volumeMounts:
- name: todo-pv
  mountPath: /app/data
volumes:
- name: todo-pv
  persistentVolumeClaim:
    claimName: todo-pvc
```

This will mount the Persistent Volume Claim `todo-pvc` to the `/app/data` directory in the container.

1. Apply the updated deployment using the command:
    

```bash
kubectl apply -f deployment.yml
```

1. Verify that the Persistent Volume has been added to your Deployment:
    

Check the status of the Pods and Persistent Volumes in your cluster using the following commands:

```bash
kubectl get pods
kubectl get pv
```

You should see the status of the pods and the persistent volume. If everything is working correctly, you should see that the Pod is running and the Persistent Volume is bound to the Persistent Volume Claim.

1. Verify that data is being persisted:
    

Create a sample todo item in your app, and then delete the Pod running the app. Verify that the todo item is still present when a new Pod is created to replace the deleted one.

To do this, first find the name of the Pod running the app:

```bash
kubectl get pods
```

Then delete the Pod:

```bash
kubectl delete pod <pod-name>
```

Finally, verify that the todo item is still present in the app by visiting the app in your web browser.

Congratulations! 🎉🥳You have successfully added a Persistent Volume to your Deployment in Kubernetes for a todo app, and you have verified that data is being persisted across Pod restarts.

## <mark>Task 2: Accessing data in the Persistent Volume</mark>

Connect to a Pod in your Deployment using command : `kubectl exec -it <pod-name> -- /bin/bash` . Verify that you can access the data stored in the Persistent Volume from within the Pod

steps to access data in the Persistent Volume from within the Pod:

1. Connect to a Pod in your Deployment:
    

Find the name of the Pod running your app using the command:

```bash
kubectl get pods
```

Then connect to the Pod using the command:

```bash
kubectl exec -it <pod-name> -- /bin/bash
```

This will open a shell session in the Pod.

1. Verify that you can access the data stored in the Persistent Volume from within the Pod:
    

Navigate to the `/app/data` directory in the Pod using the command:

```bash
cd /app/data
```

List the contents of the directory using the command:

```bash
ls
```

You should see the data that was stored in the Persistent Volume from when you created the todo item earlier.

If you can access the data stored in the Persistent Volume from within the Pod, then you have successfully added and accessed a Persistent Volume in Kubernetes.

1. Create a new file in the Persistent Volume:
    

Create a new file in the `/app/data` directory using the command:

```bash
echo "This is a new file in the Persistent Volume" > newfile.txt
```

List the contents of the directory again using the command:

```bash
ls
```

You should now see the new file listed in the output.

1. Verify that the new file is persisted across Pod restarts:
    

Delete the Pod using the command:

```bash
kubectl delete pod <pod-name>
```

Wait a few moments for the Pod to be recreated.

Verify that the new file is still present in the `/app/data` directory in the new Pod by connecting to the new Pod using the `kubectl exec` command as described earlier, navigating to the `/app/data` directory, and listing the contents of the directory.

If the new file is still present, then you have successfully verified that data is being persisted across Pod restarts in the Persistent Volume.

Congratulations!🥳🎉 You have successfully accessed data in the Persistent Volume from within a Pod in Kubernetes, and you have verified that data is being persisted across Pod restarts.

## <mark>Conclusion:</mark>

In today's tasks, we learned about Persistent Volumes in Kubernetes, and how they can be used to persist data across Pod restarts. We also went through the process of adding a Persistent Volume to a Deployment for a todo app, and verifying that data is being persisted. Finally, we accessed the data stored in the Persistent Volume from within a Pod, and verified that the data is being persisted across Pod restarts.

Persistent Volumes are an important feature of Kubernetes, and are essential for stateful applications that require data to be persisted across Pod restarts. By using Persistent Volumes, you can ensure that your application's data is always available, even in the event of Pod failures or restarts.