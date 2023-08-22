---
title: "A Step-by-Step Guide: Setting up a Kubernetes Cluster with Kubeadm on AWS EC2 Instances"
seoTitle: "Setting up a Kubernetes Cluster with Kubeadm on AWS EC2 Instances"
seoDescription: "Learn how to set up a Kubernetes cluster using Kubeadm on AWS EC2 instances. Detailed steps for the master and worker nodes, optimized for t2.medium and t2."
datePublished: Tue May 23 2023 14:20:18 GMT+0000 (Coordinated Universal Time)
cuid: cli0d5gwy000i09mz9ae52nx2
slug: a-step-by-step-guide-setting-up-a-kubernetes-cluster-with-kubeadm-on-aws-ec2-instances
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1684851384466/55a211a8-512b-49a7-80d0-5e81d6dde4c6.webp
tags: kubernetes, devops, containerization, kubeadm

---

Kubernetes has emerged as a powerful platform for orchestrating containerized applications, providing scalability, fault tolerance, and ease of management. In this step-by-step guide, we will walk you through the process of setting up a Kubernetes cluster using Kubeadm, specifically on AWS EC2 instances. We will utilize an Ubuntu-based t2.medium instance for the master node and a t2.micro instance for the worker nodes.

### **<mark>Prerequisites</mark>**

Before we dive into the cluster setup, make sure you have the following prerequisites in place:

1. AWS Account: Access to an AWS account with appropriate permissions to create EC2 instances.
    
2. SSH Key Pair: Generate an SSH key pair to securely access the EC2 instances.
    
3. AWS EC2 Instances: Launch an Ubuntu-based t2.medium instance for the master node and t2.micro instances for the worker nodes.
    
4. Security Group Configuration: Set up inbound rules to allow SSH (port 22) and Kubernetes communication (ports 6443, 2379-2380, and 10250-10252).
    
5. AWS CLI (Command Line Interface): Install the AWS CLI on your local machine to interact with the AWS services.
    

## **<mark>Setting up the Master Node</mark>**

1. Launch an EC2 instance:
    
    * Choose the Ubuntu 20.04 LTS AMI and the t2.medium instance type.
        
    * Configure security groups to allow SSH and Kubernetes communication ports.
        
2. Connect to the master node:
    
    * Use SSH with the generated key pair to access the EC2 instance.
        
3. Update the system packages:
    
    ```bash
    sudo apt-get update
    ```
    
4. Install Docker:
    
    ```bash
    sudo apt-get install docker.io
    ```
    
5. Start and enable Docker service:
    
    ```bash
    sudo systemctl start docker
    sudo systemctl enable docker
    ```
    
6. Add your user to the Docker group:
    
    ```bash
    sudo usermod -aG docker ubuntu
    ```
    
7. Restart Docker:
    
    ```bash
    sudo systemctl restart docker
    ```
    
8. Disable swap memory:
    
    ```bash
    sudo swapoff -a
    ```
    
9. Comment out the swap entry in `/etc/fstab`:
    
    ```bash
    sudo sed -i '/ swap / s/^\(.*\)$/#\1/g' /etc/fstab
    ```
    
10. Enable bridged traffic to pass through iptables:
    
    ```bash
    sudo sysctl net.bridge.bridge-nf-call-iptables=1
    ```
    
11. Import the Kubernetes repository signing key:
    
    ```bash
    curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
    ```
    
12. Add the Kubernetes repository:
    
    ```bash
    cat <<EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
    deb https://apt.kubernetes.io/ kubernetes-xenial main
    EOF
    ```
    
13. Update the package list:
    
    ```bash
    sudo apt-get update -y
    ```
    
14. Install specific versions of Kubeadm, Kubectl, and Kubelet:
    
    ```bash
    sudo apt install kubeadm=1.20.0-00 kubectl=1.20.0-00 kubelet=1.20.0-00 -y
    ```
    
15. Initialize the Kubernetes cluster using Kubeadm:
    
    ```bash
    sudo kubeadm init
    ```
    
16. Set the `KUBECONFIG` environment variable:
    
    ```bash
    export KUBECONFIG=/etc/kubernetes/admin.conf
    ```
    
17. Deploy the Weave network plugin for pod networking:
    
    ```bash
    sudo kubectl apply -f https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml
    ```
    

## **<mark>Setting up the Worker Nodes</mark>**

1. Launch EC2 instances:
    
    * Choose the Ubuntu 20.04 LTS AMI and the t2.micro instance type.
        
    * Configure security groups to allow SSH and Kubernetes communication ports.
        
2. Connect to each worker node:
    
    * Use SSH with the generated key pair to access the EC2 instances.
        
3. Follow steps 3-10 from the "Setting up the Master Node" section to configure Docker and system settings.
    
4. Install specific versions of Kubeadm, Kubectl, and Kubelet:
    
    ```bash
    sudo apt install kubeadm=1.20.0-00 kubectl=1.20.0-00 kubelet=1.20.0-00 -y
    ```
    
5. Perform pre-flight checks to ensure the worker node is ready to join the cluster:
    
    ```bash
    sudo kubeadm reset pre-flight checks
    ```
    

### **<mark>Joining Worker Nodes to the Cluster</mark>**

1. On the master node, generate the join command by executing:
    
    ```bash
    sudo kubeadm token create --print-join-command
    ```
    
2. Copy the generated join command.
    
3. On each worker node, paste and run the join command obtained from the master node don't forget to add --v=5 at the end of token.
    

### **<mark>Verifying the Cluster</mark>**

1. Switch back to the master node.
    
2. Verify that all nodes have successfully joined the cluster:
    
    ```bash
    kubectl get nodes
    ```
    
    The output should display all the nodes in the cluster, including the master node and worker nodes.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684850845649/0a792ed3-6718-4c65-b6da-bb94e1797e43.png align="center")

Certainly! Based on the scenario, where we are able to access the cluster successfully as a superuser but faced issues when switching to the "ubuntu" user, you can add the following commands to solve this problem:

```bash
# Switch to the normal user
su ubuntu

# Set the KUBECONFIG environment variable for the user
export KUBECONFIG=/etc/kubernetes/admin.conf

# Copy the admin.conf file to the user's home directory
cp /etc/kubernetes/admin.conf $HOME/
chown $(id -u):$(id -g) $HOME/admin.conf

# Set the KUBECONFIG environment variable permanently for the user
echo 'export KUBECONFIG=$HOME/admin.conf' >> $HOME/.bashrc
```

Explanation:

1. Switch to the "ubuntu" user using `su ubuntu` to execute the following commands as that user.
    
2. Set the `KUBECONFIG` environment variable to point to the cluster configuration file `/etc/kubernetes/admin.conf` for the "ubuntu" user.
    
3. Copy the `admin.conf` file to the user's home directory (`$HOME`) and change its ownership to match the "ubuntu" user.
    
4. Append the `export KUBECONFIG=$HOME/admin.conf` command to the user's `.bashrc` file so that the `KUBECONFIG` variable is set automatically whenever the user logs in.
    

By adding these commands in your master instance, it will ensure that the "ubuntu" user can access the Kubernetes cluster using the copied configuration file. This will allow you to interact with the cluster without requiring superuser privileges.

Please note that after making these changes, you may need to restart the shell or log out and log back in for the changes to take effect.

### **<mark>Conclusion</mark>**

In this tutorial, we walked you through the step-by-step process of setting up a Kubernetes cluster using Kubeadm on AWS EC2 instances. By following these instructions, you now have a functioning Kubernetes cluster with a master node and worker nodes. Harness the power of Kubernetes to efficiently deploy and manage containerized applications, unlocking scalability and reliability in your infrastructure.

Remember to optimize the EC2 instance types according to your specific workload requirements. Happy Kubernetes clustering!