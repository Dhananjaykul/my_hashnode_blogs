---
title: "Basic Git & GitHub for DevOps Engineers"
seoTitle: "Understanding Git and GitHub: Creating Repo,make changes and pushing"
seoDescription: "Learn about Git and GitHub, and how to create a new repository, make changes to files, and push them to the remote repository on GitHub."
datePublished: Sat Apr 08 2023 02:45:32 GMT+0000 (Coordinated Universal Time)
cuid: clg7dinmu000c0akzdyaggnvm
slug: basic-git-github-for-devops-engineers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1680920362305/ffdb1512-67df-4e86-9365-6f8227751f12.jpeg
tags: github, git, devops, 90daysofdevops, trainwithshubham

---

**1.What is Git?**

Git is a version control system designed for tracking changes in source code during software development. It was created by Linus Torvalds in 2005 to manage the development of the Linux kernel. Git provides a distributed and decentralized way of managing software development, allowing multiple people to work on the same project simultaneously.

With Git, developers can keep track of changes made to code, collaborate with other developers on a project, and revert to earlier versions of code if necessary. Git also makes it easy to create separate branches of code for different features or versions of a project, merge those branches together, and manage conflicts that arise when changes are made to the same piece of code by multiple developers.

Git has become the default standard for version control in software development, and is widely used by developers and organizations of all sizes.

**2.What is Github**

GitHub is a web-based hosting service for version control using Git. It provides a platform for developers to store and share their code repositories with others. GitHub offers a range of features and tools that make it easy for developers to collaborate on projects, track issues, and manage pull requests.

GitHub allows users to create and manage public or private repositories, where they can store their code and collaborate with other developers. Users can also contribute to existing projects by submitting pull requests or opening issues to report bugs or suggest new features.

In addition to code repositories, GitHub also provides features such as wikis, project management tools, and code review tools. It also offers integrations with other development tools and services, such as continuous integration and deployment services.

GitHub is widely used by developers and organizations of all sizes, and has become an essential tool for open source software development. It is now owned by Microsoft after an acquisition in 2018.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680921648307/03eff491-729c-4208-9262-d0ad5ebad7de.png align="center")

**3.What is Version Control? How many types of version controls we have?**

Version control is the process of managing changes to a set of files or code over time. It helps developers track and manage changes, collaborate with others, and revert to previous versions of code if necessary. Version control is essential for software development, where multiple people may be working on the same codebase simultaneously.

There are three main types of version control systems:

1. Local Version Control: This type of version control system stores revisions of files on a local machine. Developers can create new versions of files, compare changes between versions, and revert to previous versions as needed. Examples of local version control systems include RCS and SCCS.
    
2. Centralized Version Control: This type of version control system uses a central server to store all revisions of files. Developers can check out files from the server, make changes, and check them back in. The central server manages conflicts that may arise when multiple developers make changes to the same file. Examples of centralized version control systems include CVS and Subversion.
    
3. Distributed Version Control: This type of version control system is similar to centralized version control, but each developer has a local copy of the entire codebase. Developers can make changes to their local copy and share those changes with others through a central server or by directly sharing changes with other developers. Examples of distributed version control systems include Git and Mercurial.
    

Overall, version control systems are critical for software development and allow developers to work collaboratively and efficiently on complex projects.

**4.Why we use distributed version control over centralized version control?**

There are several reasons why distributed version control systems (DVCS) like Git are preferred over centralized version control systems (CVCS) like Subversion:

1. Offline work: With a DVCS, developers have a complete copy of the code repository on their local machines. This means they can work on code even when they're offline, without needing to be connected to a central server. In contrast, with a CVCS, developers need to be connected to the central server to make changes.
    
2. Better collaboration: In a DVCS, developers can easily create and merge branches, and can work on multiple branches simultaneously. This makes it easier for teams to collaborate on complex projects, and to experiment with new features without disrupting the main codebase. In a CVCS, branching is typically more complex, and merging can be difficult.
    
3. Faster performance: Because a DVCS stores a complete copy of the code repository on each developer's machine, operations like commit, branching, and merging can be faster than in a CVCS, where these operations require communication with a central server.
    
4. Improved security: With a DVCS, each developer has a complete copy of the code repository on their local machine, so there is less risk of data loss or corruption if the central server goes down or is compromised. In a CVCS, the central server is a single point of failure and can be a security vulnerability.
    

Overall, DVCS like Git are preferred over CVCS like Subversion because they provide better collaboration, offline work, faster performance, and improved security.

**5\. Exercises**

**5.1 Create a new repository on GitHub and clone it to your local machine**

The steps involved in creating a new repository on GitHub and cloning it to a local machine:

1. Sign in to your GitHub account and click on the "+" icon in the top-right corner of the screen.
    
2. Select "New repository" from the dropdown menu.
    
3. Give your repository a name, and optionally, a description.
    
4. Choose whether to make your repository public or private.
    
5. Select the checkbox to "Initialize this repository with a README" if you want to add a README file to your repository.
    
6. Click on the "Create repository" button to create your new repository.
    
7. On your local machine, open a terminal window and navigate to the directory where you want to clone your repository.
    
8. Copy the URL of your repository from the GitHub website.
    
9. In the terminal window, enter the command "git clone" followed by the URL of your repository.
    
10. Press Enter to clone the repository to your local machine.
    

Once you have cloned the repository to your local machine, you can start working on your code and make changes to it. You can then use Git to commit your changes and push them back to your GitHub repository.

**5.2 How to Make some changes to a file in the repository and commit them to the repository using Git**

To make changes to a file in a Git repository and commit them to the repository, follow these steps:

1. Open a terminal window and navigate to the local copy of your repository.
    
2. Use the command "git status" to see the current status of your repository and any changes that have been made.
    
3. Use the command "git add" followed by the name of the file you want to change to stage your changes for commit. For example, if you want to stage a file named "index.html", use the command "git add index.html".
    
4. Use the command "git commit" to commit your changes to the repository. You can include a commit message with the "-m" option. For example, the command "git commit -m 'Updated index.html'" will commit the changes to the "index.html" file with a commit message of "Updated index.html".
    
5. Use the command "git push" to push your changes to the remote repository on GitHub.
    
6. Enter your GitHub username and password if prompted.
    

After you have completed these steps, your changes will be saved to the remote repository on GitHub. Other users with access to the repository can now see and download your changes.

**5.3 How to Push the changes back to the repository on GitHub**

To push the changes you made locally back to the repository on GitHub, follow these steps:

1. Open a terminal window and navigate to the local copy of your repository.
    
2. Use the command "git add" followed by the name of the file you modified to stage the changes. For example, if you modified a file named "index.html", use the command "git add index.html".
    
3. Use the command "git commit" to commit your changes to the local repository. You can include a commit message with the "-m" option. For example, the command "git commit -m 'Updated index.html'" will commit the changes to the "index.html" file with a commit message of "Updated index.html".
    
4. Use the command "git push" to push the changes to the remote repository on GitHub. This will upload the changes you made locally to the repository on GitHub. You will need to enter your GitHub username and password when prompted.
    
5. Once the push is complete, the changes will be visible on the GitHub website in your repository.
    

That's it! Your changes are now stored in the repository on GitHub and are available for others to see and download.