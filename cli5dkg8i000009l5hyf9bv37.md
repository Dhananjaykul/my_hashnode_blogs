---
title: "Ansible Playbooks: Simplify Server Management with Automation 🤖"
seoTitle: "Ansible Playbooks: Simplify Server Management with Automation 🤖"
seoDescription: "Learn how to automate server management tasks using Ansible playbooks. Explore examples of file creation, user creation, and Docker installation playbooks."
datePublished: Sat May 27 2023 02:30:48 GMT+0000 (Coordinated Universal Time)
cuid: cli5dkg8i000009l5hyf9bv37
slug: ansible-playbooks-simplify-server-management-with-automation
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1685154553650/0bca1b29-2b9a-4f6f-ad83-4e46e2b2e38f.png
tags: ansible, devops, 90daysofdevops, ansible-playbook, trainwithshubham

---

Welcome back to our ongoing journey through the world of Ansible! In our previous blog on Ansible ad-hoc commands, we explored how to ping and update servers using simple one-liners. Today, we'll delve deeper into Ansible's power by introducing playbooks – a fundamental component of Ansible automation.

But before we dive into the playbook magic, let's add a touch of fun and excitement to make your reading experience even more enjoyable! 🎉✨ Here are some points to guide you along the way:

* 📜 Playbook Definition
    
* 📂 File Creation Playbook
    
* 👤 User Creation Playbook
    
* 🐳 Docker Installation Playbook
    

Now, let's begin by understanding what Ansible playbooks are and how they can streamline server management tasks.

## 📜 Playbook Definition

Ansible playbooks are human-readable and machine-parseable files that define a set of tasks, executed in sequence, to automate infrastructure configurations and deployments. They use a simple and intuitive YAML syntax that allows you to express complex automation workflows with ease.

Playbooks enable you to define the desired state of your infrastructure, and Ansible takes care of bringing the actual state in line with it. By using playbooks, you can eliminate repetitive manual tasks, ensure consistency across multiple servers, and improve efficiency in managing your infrastructure.

Now, let's explore three practical examples of using Ansible playbooks.

## 📂 File Creation Playbook

Imagine you need to create a file on multiple servers simultaneously. Instead of connecting to each server individually, you can use an Ansible playbook to perform this task seamlessly. Here's an example playbook to create a file named "file.txt" on a group of servers:

```yaml
---
- name: This playbook will create a file
  hosts: all
  become: true
  tasks:
  - name: Create a file
    file:
     path: /home/ubuntu/file.txt
     state: touch
```

In this playbook:

* The `name` field provides a description of the playbook.
    
* `hosts` specifies the target hosts or groups of hosts where the tasks will be executed.
    
* `become: true` ensures the tasks are executed with administrative privileges.
    
* `tasks` define a list of tasks to be performed, and each task consists of a `name` and a module (in this case, the `file` module).
    
* The `file` module is used with the `path` parameter to specify the file path and the `state` parameter to indicate that the file should be created (touched).
    

By running this playbook, Ansible will create the "file.txt" file on all the servers.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685153659729/83003eda-51d4-4915-a4da-6f15b56a025f.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685153821525/bfcd5e36-7544-4f54-ad4e-68426e88cd94.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685153957134/dc4a59bb-94ab-44d0-aa65-45602a89b4be.png align="center")

## 👤 User Creation Playbook

Next, let's look at a playbook for creating a new user on multiple servers. This playbook allows you to automate the user creation process, saving you time and effort. Here's an example playbook:

```yaml
---
- name: this playbook will create a user
  hosts: all
  become: true
  tasks:
  - name: to create a user named Ironman
    user: name=Ironman
```

In this playbook:

* The `user` module is used to create the user account.
    
* The `name` parameter specifies the username.
    

By executing this playbook, Ansible will create a user named "Ironman" on all the servers.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685153967313/949ee0c8-a406-4e1b-94f6-8c85e90caf50.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685154116160/ea394e22-ed91-408d-9f3c-f8ef2bb45493.png align="center")

## 🐳 Docker Installation Playbook

Lastly, let's explore how to automate the installation of Docker on a group of servers. Docker simplifies the deployment and management of applications within containers. By using an Ansible playbook, you can quickly set up Docker across multiple servers.

Here's an example playbook:

```yaml
---
- name: This playbook will install Docker
  hosts: all
  become: true
  tasks:
  - name: Add Docker GPG apt Key
    apt_key:
     url: https://download.docker.com/linux/ubuntu/gpg
     state: present

  - name: Add Docker Repository
    apt_repository:
     repo: deb https://download.docker.com/linux/ubuntu focal stable
     state: present

  - name: Install Docker
    apt:
     name: docker-ce
     state: latest
```

In this playbook:

* The `apt_key` module is used to add the Docker GPG apt key.
    
* The `apt_repository` module is used to add the Docker repository.
    
* The `apt` module is used to install the latest version of Docker.
    

By executing this playbook, Ansible will install Docker on all the servers.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685154203601/1bad2e39-8ef3-4265-81be-abc5212b9334.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685154358880/6d0f0386-6445-44b6-8734-83554c2898ff.png align="center")

## Wrapping Up

🥳🥳 on completing today's exploration of Ansible playbooks! 🎉 We covered the basics and showcased three practical examples: file creation, user creation, and Docker installation. By leveraging playbooks, you can streamline and automate various server management tasks, enabling you to focus on more critical aspects of your infrastructure.

On day day 59, we will dive even deeper into Ansible's advanced features, so make sure to stay tuned! If you missed our previous blog on Ansible ad-hoc commands, don't forget to catch up. Until next time, happy automating! 🤖💻