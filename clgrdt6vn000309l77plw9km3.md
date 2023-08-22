---
title: "Getting Started with Jenkins"
seoTitle: "Jenkins: An Introduction to Continuous Integration and Delivery"
seoDescription: "Create a freestyle pipeline in Jenkins in just a few easy steps. Improve your knowledge of Jenkins and streamline your development workflows today!"
datePublished: Sat Apr 22 2023 02:49:07 GMT+0000 (Coordinated Universal Time)
cuid: clgrdt6vn000309l77plw9km3
slug: getting-started-with-jenkins
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1682131678225/df264305-3abe-4903-999e-664881719b8e.jpeg
tags: devops, jenkins, 90daysofdevops, trainwithshubham, devopscommunity

---

Jenkins is an open-source automation server that helps teams automate the building, testing, and deployment of their software projects. With Jenkins, developers can quickly and easily set up continuous integration (CI) and continuous delivery (CD) pipelines to streamline their workflows and improve the quality of their software.

Continuous integration involves regularly merging code changes into a central repository, testing the changes to ensure they work correctly, and integrating them with the rest of the codebase. This process helps catch errors early in the development process, preventing issues from snowballing into larger problems later on.

Continuous delivery takes continuous integration a step further by automatically deploying the changes to a staging or production environment once they pass all the necessary tests. This ensures that the software is always up to date and that any issues are caught and addressed quickly.

Jenkins provides a simple and powerful platform for setting up and managing these pipelines. It integrates with a wide range of tools and technologies, including Git, Docker, AWS, and more, and can be easily extended with plugins to meet the specific needs of your project.

To get started with Jenkins, you'll need to install it on a server or cloud instance. Once it's up and running, you can create a new project and configure your CI/CD pipeline using Jenkins' web interface. This involves setting up the build process, defining the tests to run, and specifying the deployment targets.

Once your pipeline is set up, Jenkins will automatically trigger the build process whenever changes are pushed to your code repository. It will then run the defined tests and deploy the changes if they pass. Any failures or errors will be reported back to the team, allowing them to quickly identify and fix any issues.

In addition to its automation capabilities, Jenkins also provides a wealth of data and analytics to help teams monitor and improve their processes. It can track build times, test results, and deployment success rates, providing valuable insights into where bottlenecks and issues may be occurring.

Overall, Jenkins is a powerful tool for teams looking to streamline their development workflows and improve the quality of their software. By automating key processes and providing valuable insights, it can help teams deliver better software faster and with fewer errors.

### Task 1. Create a freestyle pipeline to print "Hello World!!"

Here's a step-by-step process for creating a freestyle pipeline in Jenkins to print "Hello World!!":

1. Log in to your Jenkins instance and navigate to the dashboard.
    
2. Click on the "New Item" button in the top left corner of the screen.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682129720345/a8fc446d-b6e8-499e-9fd1-fcc6dd18a5b2.png align="center")
    
3. Enter a name for your new pipeline and select "Freestyle project" as the project type.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682129794449/6691fa23-54bf-497d-9f3e-9ccff1809e06.png align="center")
    
4. Click "OK" to create your new pipeline.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682129873931/9e717ba6-8119-44de-bd52-7c13452fd970.png align="center")
    
5. In the configuration screen that appears, scroll down to the "Build" section and click on the "Add build step" dropdown menu.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682130005886/9815342e-1c2c-4f42-afeb-54c008c28c8d.png align="center")
    
6. Select "Execute shell" from the menu.
    
7. In the "Command" field that appears, enter the following command: `echo "Hello World!!"`
    
8. Click "Save" to save your changes.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682130100827/8ce9bc63-194f-4617-8dff-e0cc415c9fcb.png align="center")
    
9. Your pipeline is now set up to print "Hello World!!" when it runs. To run the pipeline, simply click on the "Build Now" button in the left sidebar.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682130190204/b1095b7b-747a-4abd-9b0d-c20e8e7b8ad3.png align="center")
    
10. Once the build is complete, you should see the "Hello World!!" message displayed in the console output.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682130256394/aab490e5-0153-4eb5-ad22-44786cce924f.png align="center")
    

That's it! 🎉Hurrey!! You've successfully created a freestyle pipeline in Jenkins to print "Hello World!!"