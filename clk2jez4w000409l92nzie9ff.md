---
title: "Project-3: React App on AWS S3 with Static Hosting | Practical AWS Projects"
seoTitle: "Host Your React App on AWS S3 with Static Hosting"
seoDescription: "Learn how to deploy and scale your React app using AWS S3 for static hosting. Step-by-step guide with easy-to-follow instructions and tips."
datePublished: Fri Jul 14 2023 12:10:36 GMT+0000 (Coordinated Universal Time)
cuid: clk2jez4w000409l92nzie9ff
slug: project-3-react-app-on-aws-s3-with-static-hosting-practical-aws-projects
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1689336425250/9f285409-4f89-4f96-8338-d585ebe1e3a3.png
tags: aws, reactjs, devops, 90daysofdevops

---

Welcome to Day 82 of 90DaysOfDevOps Challange, where we explore hands-on projects using Amazon Web Services (AWS) and Devops tools. In this project, we will learn how to host a React app on AWS S3 with static hosting. 🚀

## Introduction to AWS S3

Amazon S3 (Simple Storage Service) is a highly scalable object storage service provided by AWS. It allows you to store and retrieve any amount of data using a simple web services interface. We will leverage the power of AWS S3 to host our React app as a static website. Let's get started! 💪

### Prerequisites

Before we begin, make sure you have the following:

✅ Node.js and npm installed on your local computer

✅ AWS account with access to the AWS Management Console

## Step 1: Setting up the React App

1. 📂 Create a directory called `react-app` on your local computer.
    
2. 💻 Open a terminal (PowerShell) and navigate to the `react-app` directory.
    
3. Install `npm` (Node Package Manager) if you haven't already installed it on your system.
    

## Step 2: Creating the React App

1. Run the following command to create a new React app:
    

```bash
npx create-react-app demo-app
```

1. 📂 Move into the newly created app directory:
    

```bash
cd demo-app
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689317168697/a13f3aa3-6e0f-4bac-9b91-15d5a303f261.png align="center")

1. Start the development server for your React app:
    

```bash
npm start
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689317420315/1ff948e1-1c3b-4317-b0d2-702c38b04974.png align="center")

1. 🌐 Your application will be running on [`localhost:3000`](http://localhost:3000) in your web browser.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689317481635/8049f8b3-b5a6-4ee0-9485-6a0d015d5a17.png align="center")

## Step 3: Building the Production Version

1. To create a production build of your React app, use the following command:
    

```bash
npm run build
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689317901186/130e5b41-a36f-4dea-baa3-a22e4a7d0374.png align="center")

## Step 4: Setting up AWS S3 Bucket

1. 🌐 Go to the AWS Management Console and navigate to the S3 service.
    
2. Let's create two buckets: one with the name "[www.devopssimplified.io](http://www.devopssimplified.io)" and the other with "[devopssimplified.io](http://devopssimplified.io)". The reason for two buckets will be explained later.
    
3. Leave all the default settings while creating the buckets. We will make changes to them later.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689327341494/50aa4ef4-2e3c-4f82-8b53-943204e0c31d.png align="center")
    

## Step 5: Uploading the Website Files

1. 📤 Go to the "[www.devopssimplified.io](http://www.devopssimplified.io)" bucket.
    
2. Upload the files by clicking on the "Add files" button. Navigate to the `build` directory of your React app.
    
3. Select all the files in the directory and upload them. Also, upload the `static` folder located within the `build` directory.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689327495523/4de495a6-5fc3-46d9-abad-726f953a85b9.png align="center")

## Step 6: Configuring Bucket Permissions

1. 👥 Click on the "Permissions" tab of the "[www.devopssimplified.io](http://www.devopssimplified.io)" bucket.
    
2. Disable the "Block public access" setting, which is enabled by default. Click on "Edit" and disable it.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689327581803/4debef22-11f5-4075-bce6-e70c5963316a.png align="center")
    
3. Save the changes and go to the "Bucket Policy" tab.
    
4. Edit the bucket policy to allow public access to the website files. Replace the existing policy with the following:
    

```json
    {
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::www.devopssimplified.io/*"
            ]
        }
    ]
}
```

1. Save the changes.
    

## Step 7: Verifying the Website

1. 🌐 Go to the "Objects" tab of the "[www.devopssimplified.io](http://www.devopssimplified.io)" bucket.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689327706738/cac053b0-4c1f-42f9-a1aa-ac19071e631d.png align="center")
    
2. Locate the `index.html` file and click on the object URL. Open it in a new tab.
    
3. The index.html page will load, but the CSS and other files might be missing. You won't see the React logo at this point.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689327785061/b1f26c97-23ef-49cc-95df-6083067c7551.png align="center")

## Step 8: Enabling Static Website Hosting

1. 🛠️ Go to the "Properties" tab of the "[www.devopssimplified.io](http://www.devopssimplified.io)" bucket.
    
2. Scroll down to "Static website hosting" and click on "Edit."
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689327868525/c3913824-ad58-4fe4-ad8e-d9f9fa5cff0f.png align="center")
    
3. Enable static website hosting and set the "Index document" field to `index.html`.
    
4. Save the changes.
    
5. For our other bucket do the below settings
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689328127448/94b9b057-0cf9-4047-8d29-a55c2a675ce4.png align="center")
    

## Step 9: Setting up DNS with Route 53

1. 🌐 Register a domain name for your website using AWS Route 53. Let's use "[devopssimplified.io](http://devopssimplified.io)" as an example.
    
2. Click on "Registered domains" in the AWS Management Console and choose "Register domain."
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689328222304/b38ab242-c21f-402b-9d26-1dea316f2667.png align="center")
    
3. Select your desired domain name (e.g., "[devopssimplified.](http://devopssimplified.io)net"), add it to the cart, and proceed to checkout.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689328356370/97c558d2-6927-4806-aaf7-7f0f71c3627c.png align="center")
    
4. Provide the necessary contact information and complete the registration process.
    
5. ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689328484250/ffe7b1c3-1faf-41d8-8e69-caa6a964caaf.png align="center")
    
6. Ohh! It's Expensive😑
    
7. If you have already purchased a domain you can follow the bellow steps
    

## Step 10: Configuring DNS Records

1. 🌐Go to the "Hosted zones" section in Route 53.
    
2. Click on the "[devopssimplified.io](http://devopssimplified.io)" hosted zone and create two records: one for "[www.devopssimplified.io](http://www.devopssimplified.io)" and another for the non-www version.
    
3. Select "Simple routing" for both records and define the record names accordingly.
    
4. Choose the endpoint alias as the S3 website endpoint and select the appropriate region (e.g., us-east-1).
    
5. Choose the corresponding S3 bucket for each record.
    
6. Disable target health and click on "Define simple record" to save the changes.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689335866843/755c8d33-edb5-4902-9d60-6da0c88c0586.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689335964382/4dbe6938-85fd-46a4-94f0-4b7c89a031d1.png align="center")

## Step 11: Final Steps

1. 🌐 Wait for the DNS changes to propagate, which may take some time (typically a few minutes to hours).
    
2. Once the changes have propagated, your React app will be available at the URL you registered (e.g., [https://www.devopssimplified.io](https://www.devopssimplified.io)).
    
3. I didn't B'coz It will take time for me to register my own DNS
    

Congratulations! 🎉 You have successfully hosted your React app on AWS S3 with static hosting. Now you can share your website with the world. Feel free to explore other AWS services to enhance your app and make it even more powerful.

Stay tuned for more Practical AWS Projects where we explore different AWS use cases and build exciting applications! 👨‍💻🌐