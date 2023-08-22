---
title: "Docker Project for DevOps Engineers"
seoTitle: "Docker project for Devops"
seoDescription: "This tutorial guides you through the process of creating a Dockerfile for a simple web application, building an image, running the container."
datePublished: Mon Apr 17 2023 15:45:24 GMT+0000 (Coordinated Universal Time)
cuid: clgl0c8qi00010alfgzvx0wf4
slug: docker-project-for-devops-engineers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1682409196714/7126aeb9-bfb1-47d4-9791-17a31ae849af.png
tags: linux, docker, devops, dockerfile, 90daysofdevops

---

# **Task:**

# **\- Create a Dockerfile for a simple web application (Django application)**

# **\- Build the image using the Dockerfile and run the container**

# **\- Verify that the application is working as expected by accessing it in a web browser**

# **\- Push the image to a public or private repository (e.g. Docker Hub )**

# Steps to create a Docker container for a Django application

1. Log in to your AWS EC2 console on your Ubuntu machine.
    
2. Install Docker on your Ubuntu instance by running the following commands:
    
    ```bash
    sudo apt update
    sudo apt install docker.io
    ```
    
    These commands will update the package index and install Docker on your Ubuntu instance.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682405634378/c0ca8b3e-d1b4-4e06-9c8e-7ec59107d400.png align="center")
    
3. Add your current user to the Docker group using the following command:
    
    ```bash
    sudo usermod -aG docker $USER
    ```
    
    This command adds the current user to the Docker group, allowing the user to run Docker commands without using `sudo` every time.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682405744515/f5e8128d-aece-4e4f-9c4d-5cd029c04b99.png align="center")
    
4. Clone the code from the provided GitHub repository by running the following command:
    
    ```bash
    git clone https://github.com/Dhananjaykul/react_django_demo_app.git
    ```
    
    This command will create a new directory named `react_django_demo_app` in your current directory, which contains the source code for the demo application.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682405799230/6c2ef474-6f5b-4dd0-a0f2-df01ab6ba852.png align="center")
    
5. Navigate to the `react_django_demo_app` directory using the `cd` command.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682405916864/bb922450-566d-48c4-832f-28f2982acf89.png align="center")
    
6. Create a new file named `Dockerfile` in this directory using the `vim` command, and open it .
    
7. create the content as per the requirements.txt into the `Dockerfile` and save it.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682407741694/85615372-6804-4fb6-8352-efb1c4aa0c2b.png align="center")
    
8. Build the Docker image using the following command:
    
    ```bash
    docker build . -t react-django-app:latest
    ```
    
    This command will build a new Docker image named react-django-app from the `Dockerfile` in the current directory (`.`).
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682406959042/be7787e3-95b7-4522-a3cf-864a08e7af45.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682407028435/9d432495-222c-43c3-998c-0056aca3d0be.png align="center")
    
9. Open your AWS EC2 console and navigate to the "Instances" page.
    
10. Select the instance you are running the Docker container on and click on the "Security" tab.
    
11. Click on the security group associated with your instance.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682407179722/79d4d910-05ea-4d5a-8bfd-8e6ddba12280.png align="center")
    
12. Click on the "Edit inbound rules" button.
    
13. Add a new rule to allow inbound traffic on port 8000 from all IPv4 addresses by selecting "Custom TCP rule" as the "Type", entering "8000" as the "Port range", selecting "0.0.0.0/0" as the "Source", and leaving the "Description" field blank.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682407901212/157c5394-7f16-464d-9164-45aff8aca4cd.png align="center")
    
14. Click on the "Save rules" button to apply the changes.
    
15. Once the image is built, you can start a new Docker container using the following command:
    
    ```bash
    docker run -d -p 8000:8000 react-django-app:latest
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682408211992/60b1f220-3cf2-4bac-8164-2d856378b665.png align="center")
    
16. This command will start a new Docker container from the react-django-app image, and map the container's port 8000 to the host machine's port 8000.
    
17. If there are no errors, you should see the Django development server start up in the terminal. You can now access your Django application by opening a web browser and navigating to `http://<your-ec2-instance-public-ip>:8000`.
    

Note: Replace `<your-ec2-instance-public-ip>` with the public IP address of your AWS EC2 instance.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682408329505/2ebf75d1-e050-4c10-98af-c699d9080c8c.png align="center")

Congratulations! ✨🎉🎉🎉🎉🎉🎉🎉🎉🎉🎉🎉🎉🎉🎉🎉🎉🎉🎉🎉🎉🎉You have successfully installed Docker on your Ubuntu instance, added the current user to the Docker group, created a Docker container for the provided React-Django demo application, and exposed port 8000 for everyone using IPv4 in the inbound rule of your instance's security group.