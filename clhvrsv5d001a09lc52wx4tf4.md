---
title: "Getting Started with AWS CodeCommit: A Comprehensive Guide🚀 ☁"
seoTitle: "Getting Started with AWS CodeCommit: A Comprehensive Guide"
seoDescription: "Learn how to set up a CodeCommit repository, clone it locally, and configure GitCredentials in AWS IAM for secure authentication."
datePublished: Sat May 20 2023 09:11:33 GMT+0000 (Coordinated Universal Time)
cuid: clhvrsv5d001a09lc52wx4tf4
slug: getting-started-with-aws-codecommit-a-comprehensive-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1684574106654/a980ba0e-45ae-4ccf-8dac-b7e878950d31.jpeg
tags: aws, git, devops, cicd, aws-codecommit

---

In today's rapidly evolving software development landscape, efficient source code management is crucial for successful project collaboration and version control. AWS CodeCommit, a managed source control service provided by Amazon Web Services (AWS), offers developers a secure and scalable solution to store, manage, and version their source code and artifacts. This blog post will introduce you to CodeCommit and guide you through the process of setting up a code repository, cloning it on your local machine, and performing essential tasks such as adding a new file, committing changes, and pushing them to your CodeCommit repository.

## <mark>Task-01: Setting up a Code Repository on CodeCommit</mark>

AWS CodeCommit provides a seamless interface for creating and managing code repositories. Let's get started by following these steps:

1. Sign in to the AWS Management Console and navigate to the CodeCommit service.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684570014476/c9d553e6-ab97-429b-aa0c-4073169ebe4e.png align="center")
    
2. Click on the "Create repository" button and provide a unique name for your repository.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684570164871/99b2a9f6-9580-4a87-8bcb-29029b1ea7ce.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684570227704/c34eff6e-8fe1-4549-871a-e59abdaf078b.png align="center")
    
3. Optionally, you can add a repository description and configure repository settings such as permissions, notifications, and triggers.
    
4. After creating the repository, note down the repository URL, as we will be using it in the next steps.
    

Now, let's set up GitCredentials in your AWS IAM and configure them on your local machine:

1. Open the AWS IAM console and navigate to the "Users" section.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684570491742/698e5366-303e-456c-8672-2d3af543014a.png align="center")
    
2. Locate your IAM user or create a new one if needed.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684570581172/9f08bcde-333e-4641-9539-5be5ad439014.png align="center")
    
3. Under the "Security credentials" tab, click on "Create access key" to generate your access key ID and secret access key.
    
4. Copy the access key ID and secret access key to a secure location.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684571069135/0a19602e-9417-4132-8a16-7ea44ca418e1.png align="center")
    

You need to setup GitCredentials in your AWS IAM.

1. Navigate to the IAM section again
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684571533706/8bed687a-eab5-4d7e-ba40-90d1ebe83a50.png align="center")
    
2. Provide the permission to the user for CodeCommit.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684571706916/d112dc86-bfd9-4793-9460-94dcb52a0b2b.png align="center")
    
3. Then, navigate to the credential section of the user and generate username and password in order to login to the CodeCommit.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684572149859/aa92f39f-6cff-4bce-8e00-d5bd0cc7830d.png align="center")
    

Now, let's clone the repository from CodeCommit to your local machine:

1. Navigate to the desired directory on your local machine where you want to clone the repository.
    
2. Run the following Git command, replacing `<repository_url>` with the URL of your CodeCommit repository:
    

```bash
git clone <repository_url>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684572708738/d69e3137-8c4e-49a5-830c-de50ae796b49.png align="center")

1. You will be prompted for your AWS IAM credentials. Enter the access key ID and secret access key generated earlier.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684572776635/67932b1b-eeec-4552-a20c-1cd5395398a1.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684572953144/3f8f69af-9f4f-4a20-b747-b75e18d829bc.png align="center")
    

Congratulations!🤩🎇🎇🎇🎉🎉🥳🥳🥳🥳🥳🥳🥳🥳🥳 You have successfully set up a code repository on CodeCommit and cloned it on your local machine.

## <mark>Task-02: Adding a New File, Committing Changes, and Pushing to CodeCommit</mark>

Now that you have the repository on your local machine, let's perform some essential tasks:

1. Open your preferred code editor and create a new file or make changes to an existing file within the cloned repository.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684573068397/4b52a866-4391-4a9a-aa41-b7c716453503.png align="center")
    
2. Save the changes and return to your terminal or command prompt.
    

To commit the changes to your local branch:

1. Run the following Git commands within the repository directory:
    

```shell
git add .
git commit -m "Add/update file: <file_name>"
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684573525679/99cc00b7-e246-4b2c-a84d-dd89f43b87e5.png align="center")

1. Replace `<file_name>` with the name of the file you added or modified.
    

**To push the local changes to your CodeCommit repository:**

1. Run the following Git command:
    

```shell
git push origin <branch_name>
```

1. Replace `<branch_name>` with the name of the branch you want to push the changes to. Typically, the default branch is "master" or "main."
    

1. ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684573618398/37f3836d-dad5-41f2-a1cb-ea2c0ed6244f.png align="center")
    

### **Conclusion:**

AWS CodeCommit offers developers a reliable and scalable solution for managing source code and collaborating on projects. In this blog post, we covered the basics of setting up a code repository on CodeCommit, cloning it on your local machine, and performing essential tasks such as adding a new file, committing changes, and pushing them to your CodeCommit repository. With CodeCommit, you can streamline your software development workflow, set up continuous integration and deployment pipelines, and ensure secure and efficient version control for your projects.