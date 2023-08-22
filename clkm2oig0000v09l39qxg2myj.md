---
title: "Project-7: 🚀 Deploying a Portfolio App on AWS S3 using GitHub Actions 🚀"
seoTitle: "Deploy Portfolio App on AWS S3 using GitHub Actions"
seoDescription: "Learn how to deploy your Portfolio app on AWS S3 using GitHub Actions. Automate CI/CD, host on S3, and showcase your work. Step-by-step tutorial."
datePublished: Fri Jul 28 2023 04:17:31 GMT+0000 (Coordinated Universal Time)
cuid: clkm2oig0000v09l39qxg2myj
slug: project-7-deploying-a-portfolio-app-on-aws-s3-using-github-actions
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690517624658/145e9160-e59d-4a31-b6aa-184d70c87dee.png
tags: aws, devops, ci-cd, github-actions-1, 90daysofdevops

---

Welcome to this detailed guide on how to deploy your Portfolio app on AWS S3 using GitHub Actions. In this step-by-step tutorial, we will cover each concept and explain every single step to ensure a smooth deployment process. But first, let's understand the key concepts of GitHub Actions.

## What is GitHub Actions? 🤖

GitHub Actions is a powerful continuous integration and continuous deployment (CI/CD) platform provided by GitHub. It enables you to automate your software development workflows, allowing you to build, test, and deploy code directly from your GitHub repositories. With GitHub Actions, you can create custom workflows using YAML-based configuration files, defining the sequence of steps that need to be executed.

## Key Benefits of GitHub Actions:

* **Integrated with GitHub:** GitHub Actions is tightly integrated with GitHub repositories, making it seamless to use for developers who already host their code on GitHub.
    
* **YAML Configuration:** Workflows are defined using simple YAML files, making it easy to understand and version-controlled along with your codebase.
    
* **Event-Driven:** Workflows can be triggered based on various events, such as code pushes, pull requests, or other custom events in your repository.
    
* **Extensibility:** A rich ecosystem of community-created actions is available, allowing you to extend the functionality of your workflows.
    
* **Scalability:** GitHub provides scalable infrastructure to run your workflows, ensuring high availability and performance.
    

## Now, Let's Begin the Deployment Process! 🚀

### Step 1: Create a New Repository - "my-portfolio" 📁

To start the deployment process, create a new GitHub repository named "my-portfolio" where we will host our Portfolio app.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690514766956/0cbe3f3d-37c9-41c0-8c1e-24c85d35c729.png align="center")

### Step 2: Add and Commit Code to GitHub Repository 📝

Once the repository is created, add your Portfolio app's code to it. Use the `git` commands to commit the code and push it to your GitHub repository or use the github UI.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690514912994/09676f48-3a17-402c-8774-3ef07d2023f1.png align="center")

### Step 3: Create an S3 Bucket - "dhananjay-portfolio-bucket" ☁️

Now, head over to the AWS Management Console and create an S3 Bucket named "dhananjay-portfolio-bucket" to store your Portfolio app's files. Remember to select a region for the bucket. Also allow public access.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690515378768/39836148-24fe-4508-979d-28aeacde9c14.png align="center")

### Step 4: Configure Bucket Policy for Public Access 🔒

To allow public access to the objects in your S3 Bucket, you need to set up a bucket policy. Navigate to the bucket's properties, select "Permissions," and click on "Bucket Policy." Add the following policy:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadForGetBucketObjects",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::<bucket name>/*"
        }
    ]
}
```

Remember to replace `<bucket name>` with the actual name of your S3 Bucket.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690515520340/e771de4d-ae01-4433-a4a5-0f4b7896ed42.png align="center")

### Step 5: Create an IAM User and Generate Security Credentials 🔑

To securely interact with AWS services from GitHub Actions, we need an IAM User with sufficient permissions. If you already have an IAM User, you can use it; otherwise, create a new one.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690515763444/53c0a159-ccc1-4f83-9b2e-e2b6bcc25876.png align="center")

Assign the necessary IAM policies to this user, allowing access to S3 and any other services required for your deployment.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690515789237/9533f199-5b4f-4d58-a919-33d042aad1f9.png align="center")

Generate the IAM User's access key and secret key, as we will need them later to configure GitHub Secrets.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690515818924/7a7b5017-10a3-46d5-82a3-abb87f5b40e0.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690515857591/c989939c-2f3d-46f1-b6da-833aa527c857.png align="center")

### Step 6: Set Up GitHub Secrets for AWS Credentials 🔒

Go to your GitHub repository, click on "Settings," then "Secrets." Here, click on "New Repository Secret" to add your AWS access key and secret key as secrets named `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`, respectively.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690515931665/35d68718-dda4-4ed4-b9d8-5cdf276663ee.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690515958715/298f3a83-29e2-4121-9fc6-10002ae08f92.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690516026630/9fc53256-b11f-4705-9855-28bfd3f3859e.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690516100870/5b0ec28b-b849-4bbf-91f1-9c8dabe3f7ec.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690516130437/cfa017e3-762e-4c2f-b03e-1ecf0f252694.png align="center")

### Step 7: Create the GitHub Actions Workflow 🔄

In your GitHub repository, navigate to the "Actions" tab and click on "Set up a workflow yourself."

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690516186001/babb9559-9d82-4b70-8bad-d6d080681567.png align="center")

Create a new file named `.github/workflows/main.yml`, and add the following content:

```yaml
name: my-portfolio-deployment # Name of the deployment

on:
  push: # Trigger the workflow when changes are pushed
    branches:
      - main

jobs: # Any name can be provided
  build-and-deploy:
    runs-on: ubuntu-latest # Latest version of Ubuntu
    steps:
      - name: Checkout # Check out the repository's code into the workflow's execution environment.
        uses: actions/checkout@v1 # Script actions

      - name: Configure AWS Credentials
        uses: aws-actions/configure-aws-credentials@v1
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-east-1

      - name: Deploy static site to S3 bucket
        run: aws s3 sync . s3://dhananjay-portfolio-bucket --delete # Change bucket name
```

### Step 8: Commit Changes and Trigger Deployment 🚀

Commit the `.github/workflows/main.yml` file to your repository and push the changes. This will trigger the GitHub Actions workflow to deploy your Portfolio app to the S3 Bucket.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690516427158/d1598a5d-bc42-48f0-982d-4203b3740f42.png align="center")

### Step 9: Enable Static Website Hosting for the S3 Bucket 🏠

Once the deployment is complete, go to your S3 Bucket's properties, select "Static website hosting," and enable it. Specify the "Index document" as `index.html`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690516613563/9e94076f-92d2-44c1-8a45-70ce5e3dda65.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690516631389/97e561c4-11d1-448f-b323-8c7f9c51da1a.png align="center")

### Step 10: Access Your Portfolio Website 🌐

Now, visit the URL endpoint provided by S3 Static Website Hosting, and you'll see your deployed Portfolio app live and accessible to the public!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690516941972/36e42320-aa04-44de-bfcb-656040fc1e2b.png align="center")

Congratulations! You have successfully deployed your Portfolio app on AWS S3 using GitHub Actions.

Feel free to explore the [`Github Repository`](https://github.com/Dhananjaykul/my-portfolio) to get the complete source code and continue your learning journey.