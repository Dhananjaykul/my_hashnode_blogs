---
title: "Understanding Configuration Management with Ansible: A Step-by-Step Guide"
seoTitle: "Understanding Configuration Management with Ansible"
seoDescription: "Explore installation steps, host configuration, and successful ping commands using Ansible. Gain insights into the benefits of configuration management"
datePublished: Thu May 25 2023 04:30:44 GMT+0000 (Coordinated Universal Time)
cuid: cli2myzd7000709mzdm160ts7
slug: understanding-configuration-management-with-ansible-a-step-by-step-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1684980886451/76e80be3-5195-43fa-b815-15996c922de2.png
tags: ansible, devops, 90daysofdevops, configuration-management

---

In the world of DevOps, efficient configuration management is vital for managing and scaling infrastructure effectively. Ansible, a powerful automation tool, simplifies configuration management by allowing you to define and manage infrastructure as code. In this blog post, we will walk through the process of installing Ansible on an AWS EC2 instance and explore its basic functionalities.

## **Task-01: Installing Ansible on AWS EC2 (Master Node)**

To begin our journey with Ansible, we need to set up the master node where Ansible will be installed. Follow these steps:

1. Log in to your AWS EC2 instance as the administrator.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684982245671/63a40133-ec62-4c68-ae1a-00d29021e349.png align="center")
    
2. Open the terminal and execute the following commands:
    
    ```bash
    sudo apt-add-repository ppa:ansible/ansible
    sudo apt update
    sudo apt install ansible
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684982487715/601d755c-ac61-4a81-9b70-0d77df40ce9b.png align="center")
    
    This will add the Ansible repository, update the package lists, and install Ansible on your EC2 instance.
    

## **Task-02: Understanding the Hosts File**

The host file in Ansible plays a crucial role in defining the inventory of servers or nodes that Ansible will manage. To learn more about the host file and its structure, follow these steps:

1. Open the terminal on your EC2 instance.
    
2. Execute the following command to open the host file in a text editor:
    
    ```bash
    sudo vim /etc/ansible/hosts
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684982589356/18151ced-2c40-4b42-b96c-75968e077228.png align="center")
    
    This command will open the hosts file using the vim text editor.
    
3. Familiarize yourself with the structure of the hosts file and make any necessary modifications to suit your infrastructure requirements.
    
4. Save the changes and exit the text editor.
    

## **Task-03: Setting Up Additional EC2 Instances (Nodes) and Testing Ansible Connectivity**

In this task, we will set up two more EC2 instances as nodes and establish connectivity between the master node and the nodes using Ansible. Follow these steps:

1. Create two additional EC2 instances with the same private keys as the previous instance. Ensure that these instances have the necessary network and security configurations.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684982979750/f4337f77-a5f1-472c-bfc7-40065a97f7b8.png align="center")
    
2. On the master node, open the terminal and navigate to the directory where the private key is located.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684983113610/18a44994-a8fe-471c-a305-af2f9930f4f0.png align="center")
    
3. Use the following command to set the appropriate permissions for the private key file:
    
    ```bash
    chmod 400 ansible_key
    ```
    
4. On the master node, open the terminal and execute the following command to open the hosts file in a text editor:
    
    ```bash
    sudo vim /etc/ansible/hosts
    ```
    
    This command will open the hosts file using the vim text editor.
    
5. Update the file with the following content:
    
    ```bash
    [servers]
    server1 ansible_host=<ip>
    server2 ansible_host=<ip>
    ```
    
    Replace `<ip>` with the actual IP address of each server you want to manage with Ansible.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684984420526/b26909c8-b66a-4e00-91d1-1e7a3af73471.png align="center")
    
6. Save the changes and exit the text editor.
    
7. Let's verify the inventory that we have created.
    
    `ansible-inventory --list -y`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684987228281/aeff65fa-4733-4483-8b1f-ecdc3a988180.png align="center")
    
8. Now, test the connectivity between the master node and the nodes by executing the following command:
    
    ```bash
    ansible all -m ping --private-key=ansible_key
    ```
    
    This command instructs Ansible to ping all the nodes defined in the hosts file using the specified private key.
    
    Oops!!Failed
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684984637688/c227ec1e-a18e-4f5e-95c3-884af757860a.png align="center")
    
    May be error with setting up the ssh connection between the asnsible master and client servers🧐🧐
    
    <mark>To resolve the connectivity issue and ensure successful pinging of the node servers using Ansible, you can follow these steps:</mark>
    
    1. *On the master server, generate a public key by executing the following command in the terminal:*
        
        ```bash
        ssh-keygen -t rsa
        ```
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684985752924/5e74eddf-13ac-40b4-be56-d79bf28c1d92.png align="center")
        
        *This command will generate a public-private key pair in the* `~/.ssh` *directory on the master server.*
        
    2. *Locate the generated public key file (*`id_rsa.pub`*) in the* `~/.ssh` *directory. You can view the contents of the public key file by using the following command:*
        
        ```bash
        cat ~/.ssh/id_rsa.pub
        ```
        
        *Note down the content of the public key.*
        
    3. *Connect to each of the node servers using SSH and navigate to the* `~/.ssh` *directory on each node.*
        
    4. *Open the* `authorized_keys` *file on each node using a text editor and paste the content of the master server's public key (*`id_rsa.pub`*) at the end of the file. Save the changes and exit the text editor.*
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684986547724/7401a7f9-c9c1-4b2e-ad4c-72611bd9d94c.png align="center")
        
    5. *Once you have copied the public key to both node servers, you can test the connectivity using Ansible. Execute the following command in the terminal on the master server:*
        
        ```bash
        ansible all -m ping
        ```
        
        *This command will use the inventory file (*`/etc/ansible/hosts` *by default) to ping all the nodes. Since you have already set up the connectivity by copying the public key, Ansible should be able to connect to the nodes and perform the ping successfully.*
        
    6. *If the connectivity is successful, you will see a response indicating a successful ping from each node.*
        
    
    *By following these steps, you should be able to establish SSH connectivity between the master server and the node servers by copying the public key. This will enable Ansible to connect to the nodes and perform operations such as pinging or executing playbooks.*
    
9. If the connectivity is successful, you will see a response indicating a successful ping from each node.
    

## **Conclusion**

Congratulations! You have successfully completed the essential tasks to understand configuration management with Ansible. In this blog post, we covered the installation of Ansible on an AWS EC2 instance, explored the hosts file, set up additional EC2 instances as nodes, and tested Ansible connectivity between the master node and the nodes. With Ansible, you can now automate and streamline your infrastructure management processes effectively. Stay tuned for our next blog post, where we will delve deeper into Ansible's powerful features and advanced configuration management techniques.