---
title: "Building a Seamless CI/CD Pipeline on AWS: Exploring CodeCommit, CodeBuild, and CodeDeploy🚀 ☁"
seoTitle: "How to Use CodeDeploy to Deploy Your Applications to AWS"
seoDescription: "CodeDeploy is a valuable tool for any organization that wants to automate the deployment of their applications to AWS. CodeDeploy can help you save time"
datePublished: Tue May 23 2023 06:57:22 GMT+0000 (Coordinated Universal Time)
cuid: clhzxbuyg000409mi707m1d9w
slug: building-a-seamless-cicd-pipeline-on-aws-exploring-codecommit-codebuild-and-codedeploy
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1684824788730/edaaa558-13a2-490f-a989-23ee70694a62.png
tags: aws, devops, codenewbies, 90daysofdevops, aws-cicd

---

Welcome to Day 52 of our DevOps journey! In our previous blog posts, we have explored the power of AWS CodeCommit for version control and AWS CodeBuild for streamlining the build process. If you missed them, catch up on our CodeCommit blog [<mark>her</mark>](https://dhananjaykulkarni.hashnode.dev/getting-started-with-aws-codecommit-a-comprehensive-guide)<mark>e</mark> and our CodeBuild blog [here](https://dhananjaykulkarni.hashnode.dev/streamlining-codebuild-simplify-your-build-process-with-aws-codebuild). Today, we take the next step forward as we dive into AWS CodeDeploy. This blog post will guide you through deploying applications with CodeDeploy and completing your end-to-end CI/CD pipeline on AWS. Let's get started!

### **<mark>Summary of Our CI/CD Pipeline on AWS</mark>**

In our CI/CD pipeline journey, we began by harnessing the capabilities of CodeCommit for secure source control and collaboration. Next, we optimized our build process using CodeBuild, automating compilation, testing, and packaging. Now, with CodeDeploy, we complete the final piece of the puzzle—automated deployments to ensure fast, reliable, and scalable application releases.

### **<mark>Deploying Applications with AWS CodeDeploy</mark>**

AWS CodeDeploy is a fully managed deployment service that automates application deployments across various compute platforms. Let's walk through the key steps involved in deploying applications with CodeDeploy:

1. **Deployment Groups**: *Create deployment groups within CodeDeploy to specify the instances or Auto Scaling groups where your application will be deployed. Define the target environment for your deployments.*
    
2. **AppSpec File**: *Customize the AppSpec file, which contains deployment instructions, including pre- and post-deployment steps, file mappings, and more. Tailor it to suit your application's specific requirements.*
    
3. **Deployment Configuration**: *Configure the deployment settings, including the deployment type (in-place or blue/green), traffic routing options, and alarms for monitoring deployment health and rollback criteria*.
    
4. **Automated Deployments**: *Leverage the power of CodeDeploy to perform automated deployments based on your desired deployment strategy. Whether it's gradually rolling out new features or performing canary deployments, CodeDeploy provides flexibility and control.*
    

### **To complete Task 1 and Task 2, follow the steps below:**

### **<mark>Task 1: Deploying index.html on EC2 using Nginx and setup a CodeDeploy agent in order to deploy code on EC2 CodeDeploy</mark>**

1. Set up an Application in CodeDeploy: Create a new application in CodeDeploy and name it as "demo-cicd-app". Select the compute platform as EC2.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684736996549/524670da-fdbd-474a-a2db-828abb685a3a.png align="center")
    
2. Create a Deployment Group: Within the application, create a deployment group named "demo-app-deploy-grp". Specify the deployment type as "in-place" and assign the CodeDeploy service role.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684737070127/763f8d1e-b3d7-448d-a7f5-0dd5efa8bd15.png align="center")
    
    <mark>CodeDeploy Services Role</mark>: [click here to create a CodeDeploy Service Role](https://docs.aws.amazon.com/pdfs/codedeploy/latest/userguide/codedeploy-user.pdf#getting-started-create-service-role)
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684808742168/4c19d91f-9542-43d0-be3b-a4c8f931f809.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684808884213/d8444392-a115-46ba-b51f-3ad4d12ff526.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684740138887/3d83b9c6-d4ee-40eb-8801-edc29c3bfd11.png align="center")
    
3. Configure Environment: Set up the environment configuration by launching an EC2 instance. Select the "demo-app-ec2" EC2 instance and provide a key-value pair, with the key as "name" and the value as "demo-app-ec2".
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684809317277/3e4b6448-7eb3-43e1-91f2-ad875c95a70b.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684809413166/da5ccfa5-107c-4d30-a915-469f5595c8f9.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684809469320/3c2ff8df-0afe-4c29-b8d6-7a0c610c43f2.png align="center")
    
4. Install CodeDeploy Agent: Connect to the EC2 instance and install the CodeDeploy agent. Run the following commands:
    
    * Run `vim` [`install.sh`](http://install.sh) and paste the script that contains all the required dependencies.
        
        ```bash
        #!/bin/bash 
        # This installs the CodeDeploy agent and its prerequisites on Ubuntu 22.04.  
        sudo apt-get update 
        sudo apt-get install ruby-full ruby-webrick wget -y 
        cd /tmp 
        wget https://aws-codedeploy-us-east-1.s3.us-east-1.amazonaws.com/releases/codedeploy-agent_1.3.2-1902_all.deb 
        mkdir codedeploy-agent_1.3.2-1902_ubuntu22 
        dpkg-deb -R codedeploy-agent_1.3.2-1902_all.deb codedeploy-agent_1.3.2-1902_ubuntu22 
        sed 's/Depends:.*/Depends:ruby3.0/' -i ./codedeploy-agent_1.3.2-1902_ubuntu22/DEBIAN/control 
        dpkg-deb -b codedeploy-agent_1.3.2-1902_ubuntu22/ 
        sudo dpkg -i codedeploy-agent_1.3.2-1902_ubuntu22.deb 
        systemctl list-units --type=service | grep codedeploy 
        sudo service codedeploy-agent status
        ```
        
    * Execute `bash` [`install.sh`](http://install.sh) to install the dependencies.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684742216738/e0900875-f2e0-4ea7-9dba-7f6cbad5abf8.png align="center")
        
    * In the project directory, add an `appspec.yml` file with the following contents:
        
    
    ```yaml
    version: 0.0
    os: linux
    files:
      - source: /
        destination: /var/www/html
    hooks:
      AfterInstall:
        - location: scripts/install-nginx.sh
          timeout: 300
          runas: root
      ApplicationStart:
        - location: scripts/start-nginx.sh
          timeout: 300
          runas: root
    ```
    
5. Add Script Files: Inside the `scripts` folder, add two files: [`install-nginx.sh`](http://install-nginx.sh) and [`start-nginx.sh`](http://start-nginx.sh). These scripts will install and start the Nginx server on the EC2 instance.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684744626164/61b58aa4-96e9-4a25-a340-ec729ed0b76a.png align="center")
    
6. Push Changes to CodeCommit Repository: Commit and push the changes made to the CodeCommit repository.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684744700770/f2969b5c-45e3-437c-9d22-6a503a41ac1f.png align="center")
    
7. Build the Demo App: Trigger the build process again to incorporate the latest changes.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684810002765/f32a7c4e-2e29-4250-9689-baf2c4fa56e7.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684810348581/f1cb435a-40b5-4167-a540-257da7d6c26f.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684810431842/2586acf9-98d6-480b-a66a-2b6d7d3d628c.png align="center")
    

### **<mark>Task 2: Deploying using appspec.yaml and creating a deployment</mark>**

1. Create a Deployment: Within the CodeDeploy console, create a deployment. Select the deployment group created earlier and choose the revision type as "Amazon S3". Make sure to create an Amazon S3 bucket to store the deployment files.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684812688730/43cbfb00-002a-420a-ab81-f58a43b3730a.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684812807270/989cb538-d7d2-4866-96c9-4aa66010fd1b.png align="center")
    
    ## **To create an Amazon S3 bucket (console)**
    
    1. Open the Amazon S3 console at [https://console.aws.amazon.com/s3/](https://console.aws.amazon.com/s3/).
        
    2. In the Amazon S3 console, choose **Create bucket**.
        
    3. In the **Bucket name** box, type a name for the bucket.
        
    4. In the **Region** list, choose the target region, and then choose **Create**.
        
    
    ### Give permissions to the Amazon S3 bucket and your AWS account
    
    You must have permissions to upload to the Amazon S3 bucket. You can specify these permissions through an Amazon S3 bucket policy. For example, in the following Amazon S3 bucket policy, using the wildcard character (\*) allows AWS account `111122223333` to upload files to any directory in the Amazon S3 bucket named `codedeploydemobucket`:
    
    ```bash
    {
        "Statement": [
            {
                "Action": [
                    "s3:PutObject"
                ],
                "Effect": "Allow",
                "Resource": "arn:aws:s3:::codedeploydemobucket/*",
                "Principal": {
                    "AWS": [
                        "111122223333"
                    ]
                }
            }
        ]
    }
    ```
    
2. Provide S3 URL: Paste the URL of the S3 bucket containing the deployment files and initiate the deployment.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684813821841/77a28499-b994-4bb3-8232-fbc8b4ca7873.png align="center")
    
3. Grant EC2 Permissions: Assign the "ec2-code-deploy" IAM role to the EC2 instance to grant necessary permissions. Modify the security group to allow inbound traffic on port 80.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684813983314/6d9c773f-b5cb-4763-a072-3126e934f64f.png align="center")
    
4. Update IAM Role: Connect to the EC2 instance and run the command `sudo service codedeploy-agent restart` to restart the CodeDeploy agent.
    
    [To create a service role for CodeDeploy](https://docs.aws.amazon.com/codedeploy/latest/userguide/getting-started-create-service-role.html)
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684814257125/fa085a50-1ee0-44eb-83de-5f43247642e8.png align="center")
    
5. Check Deployment Status: The deployment status should now show as "deployed" upon successful completion.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684823351091/14020b5b-e494-4650-8a66-0a2696a324c6.png align="center")
    

By following these steps, you will successfully deploy the index.html file on an EC2 instance using AWS CodeDeploy, creating a seamless CI/CD pipeline.

### **<mark>Conclusion</mark>**

By incorporating AWS CodeDeploy into our CI/CD pipeline, we have achieved a seamless and automated end-to-end software delivery process on AWS. From source control with CodeCommit to streamlined builds with CodeBuild and automated deployments with CodeDeploy, we have established a foundation for fast, efficient, and reliable application releases.

Stay tuned for our upcoming blog posts, where we will dive deeper into advanced DevOps practices and explore additional tools and services to further enhance our CI/CD pipeline.

Unlock the full potential of your CI/CD pipeline with AWS CodeDeploy! Read my previous blog posts on CodeBuild and CodeCommit to complete the journey. #DevOps #CI/CDPipeline #AWSCodeDeploy