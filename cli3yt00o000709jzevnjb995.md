---
title: "Understanding Ad-hoc Commands in Ansible: A Comprehensive Guide"
seoTitle: "Understanding Ad-hoc Commands in Ansible: A Comprehensive Guide"
seoDescription: "Learn about ad-hoc commands in Ansibleping multiple servers and check server uptime.Understand their usage and gain efficiency in infrastructure management"
datePublished: Fri May 26 2023 02:49:46 GMT+0000 (Coordinated Universal Time)
cuid: cli3yt00o000709jzevnjb995
slug: understanding-ad-hoc-commands-in-ansible-a-comprehensive-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1685069135149/b647c520-e186-479a-a493-a9dd439e16bf.avif
tags: ansible, automation, devops, 90daysofdevops

---

📣 Welcome to Day 56 of our DevOps journey! Yesterday, I published a blog post on setting up Ansible and pinging different servers using an Ansible master. [To visit click here](https://dhananjaykulkarni.hashnode.dev/understanding-configuration-management-with-ansible-a-step-by-step-guide). Today, we will dive deeper into the world of Ansible by exploring ad-hoc commands. 🚀 Ad-hoc commands are handy tools that allow us to perform quick tasks without writing complex playbooks. Let's expand our knowledge and learn more about ad-hoc commands in Ansible.

## <mark>Ad-hoc Commands</mark>

Ad-hoc Commands in Ansible Before we jump into the practical examples, let's understand the essence of ad-hoc commands in Ansible. Ad-hoc commands are one-liners executed in the command-line interface (CLI) to perform specific tasks on remote servers without the need for a playbook. They provide a convenient and efficient way to achieve quick automation.

## <mark>Task 1 - Pinging Multiple Servers</mark>

Imagine you have an inventory file located at `/home/ubuntu/ansible/inventories` with the details of three servers you want to ping. Let's perform this task using an ad-hoc command:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685069023190/d8d0cb02-730d-40e2-8245-22bb706c4e83.png align="center")

Step 1: Open your terminal or command prompt and navigate to the directory where your Ansible project is located. 🖥

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685068467668/fcc39570-f392-4f5d-bad6-37bbff6eeaae.png align="center")

Step 2: Use the following ad-hoc command to ping the servers:

```bash
ansible all -i /home/ubuntu/ansible/inventories -m ping
```

🔎 Replace `/home/ubuntu/ansible/inventories` with the correct path to your inventory file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685068542464/dc99e757-461d-42c2-a6b2-e563ef40f39b.png align="center")

Step 3: Hit enter, and Ansible will execute the command. You will receive ping responses from all servers if they are reachable. 🎉

Section 3: Task 2 - Checking Server Uptime Now, let's explore another practical example of using ad-hoc commands to check the uptime of a server:

Step 1: Open your terminal or command prompt and navigate to the directory where your Ansible project is located. 🖥️

Step 2: Use the following ad-hoc command to check the server uptime:

```bash
ansible all -i /home/ubuntu/ansible/inventories/dev_inv -a "uptime"
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685068674143/c4f024d3-6580-46b1-a811-155ef04df25c.png align="center")

🔎 Replace `/home/ubuntu/ansible/inventories` with the correct path to your inventory file.

```bash
ansible all -i /home/ubuntu/ansible/inventories/prod_inv -a "uptime"
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685068716223/aa83ca58-3061-43ff-a587-20e761625966.png align="center")

Here if I don't specify the path by default inventory in my */etc/ansible/hosts* folder will get executed.let's Check

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685068879175/55890fae-b917-48f5-9b39-ca53258729c6.png align="center")

Step 3: Hit enter, and Ansible will execute the command. You will receive the uptime information from all servers specified in the inventory file. 🕒

## <mark>Conclusion</mark>

🎉 Congratulations!We have now explored ad-hoc commands in Ansible. Ad-hoc commands provide a quick and effective way to perform tasks on remote servers without the need for elaborate playbooks. Today, we covered two practical examples: pinging multiple servers and checking server uptime using ad-hoc commands.

By mastering ad-hoc commands, you can increase your productivity and efficiently manage your infrastructure using Ansible. However, keep in mind that for more complex automation scenarios, playbooks are recommended as they provide better maintainability and advanced features.

Stay tuned for tomorrow's blog post as we delve deeper into the world of DevOps. Happy automating! 🚀