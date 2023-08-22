---
title: "🔎 Ansible Project: Automating Infrastructure Deployment 🚀"
seoTitle: "🔎 Ansible Project: Automating Infrastructure Deployment 🚀"
seoDescription: "In this tutorial, we will go through the process of setting up an Ansible environment and using it to deploy Nginx and a sample webpage on three EC2 instans"
datePublished: Sun May 28 2023 02:01:57 GMT+0000 (Coordinated Universal Time)
cuid: cli6rz7ll000209ibf69a5po3
slug: ansible-project-automating-infrastructure-deployment
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/UK78i6vK3sc/upload/67d73565f986db0e6a745e871ea13708.jpeg
tags: aws, automation, devops, 90daysofdevops, ansible-playbook

---

Learning of Day 59: Today, we will dive into the world of Ansible, a powerful automation tool for managing and configuring systems. In this tutorial, we will guide you through the process of setting up an Ansible environment and using it to deploy Nginx and a sample webpage on three EC2 instances. Let's get started! 💪

Step 1️⃣: Creating EC2 Instances To begin, create three EC2 instances using the Ubuntu t2.micro instance type. Make sure all three instances are associated with the same key pair. This key pair will allow you to access the instances securely. 🖥️🖥️🖥️

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685237054230/20a99de3-f065-4348-986d-e09f17487af2.png align="center")

Step 2️⃣: Installing Ansible Now, let's install Ansible on the host server. You can use the following commands to install Ansible on Ubuntu:

```shell
sudo apt update
sudo apt install ansible
```

Once the installation is complete, Ansible will be available on your system. ✔️

Step 3️⃣: Copying Private Key To enable communication between the Ansible host and the EC2 instances, we need to copy the private key from your local machine to the Ansible host. Use the following command to copy the private key to the `/home/ubuntu/.ssh` directory on the Ansible host:

```shell
scp -i /path/to/your/key.pem /path/to/your/key.pem ubuntu@ansible_host_ip:/home/ubuntu/.ssh/
```

Make sure to replace `/path/to/your/key.pem` with the actual path to your private key file and `ansible_host_ip` with the IP address of your Ansible host. 🔑

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685237379709/dc509d76-b129-4788-b4d2-326f17be9fa2.png align="center")

Step 4️⃣: Accessing the Inventory File Next, we need to configure the inventory file, which lists the hosts Ansible will manage. Access the inventory file using the following command:

```shell
sudo nano /etc/ansible/hosts
```

In the inventory file, add the IP addresses or hostnames of the three EC2 instances under a suitable group name, such as `[web-servers]`. Save and exit the file. 📝

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685237527560/c63f055d-666c-4733-a3d2-5117a107bdd9.png align="center")

Step 5️⃣: Creating the Playbook It's time to create a playbook that will install Nginx on the EC2 instances. Create a file named `nginx-playbook.yml` and add the following content:

```yaml
-
 name: This playbook will install nginx
 hosts: servers
 become: yes
 tasks:
  - name: install nginx
    apt:
      name: nginx
      state: latest
  - name: start nginx
    service:
      name: nginx
      state: started
      enabled: yes
```

Save the playbook file. This playbook specifies that it should be executed on the hosts in the `servers` group and installs Nginx using the `apt` module. 🌐

Step 6️⃣: Deploying a Sample Webpage Now, let's deploy a sample webpage on the EC2 instances using the Ansible playbook. Modify the `nginx-playbook.yml` file and add the following task at the end:

```yaml
    - name: Deploy sample webpage
      copy:
        src: /path/to/your/sample-webpage/index.html
        dest: /var/www/html/index.html
      become: true
      become_user: root
      become_method: sudo
```

Replace `/path/to/your/sample-webpage/index.html` with the actual path to your sample webpage file. This task copies the `index.html` file to the default Nginx web server

directory. 📄

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685238792791/8f933d73-1e95-4325-a193-3b6c8af4d9d1.png align="center")

Step 7️⃣: Running the Playbook To run the playbook and deploy Nginx with the sample webpage, use the following command:

```shell
ansible-playbook nginx-playbook.yml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685239037050/94739964-203c-4128-b2dc-4fff17d2ee19.png align="center")

Ansible will connect to the EC2 instances, install Nginx, and deploy the sample webpage. Once the playbook execution is complete, you can access the webpage by entering the IP addresses or hostnames of the EC2 instances in a web browser. 🌐

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685239146882/f1ddd432-a0d5-4691-91bd-b0b5998d4ac4.png align="center")

Congratulations! You have successfully set up an Ansible environment, installed Nginx, and deployed a sample webpage on multiple EC2 instances. Keep exploring Ansible's vast capabilities to automate and streamline your infrastructure management tasks! 🎉

That's it for today's learning adventure! We hope you enjoyed it. Stay tuned for more exciting tutorials. Happy automating! 🤖✨