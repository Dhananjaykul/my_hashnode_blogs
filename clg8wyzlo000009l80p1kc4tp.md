---
title: "Deep Dive in Git & GitHub for DevOps Engineers"
seoTitle: "Understanding Git and GitHub"
seoDescription: "Learn the basics of Git and GitHub, including creating a new repository, connecting a local repository to a remote repository, and pushing changes"
datePublished: Sun Apr 09 2023 04:37:52 GMT+0000 (Coordinated Universal Time)
cuid: clg8wyzlo000009l80p1kc4tp
slug: deep-dive-in-git-github-for-devops-engineers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1681010177472/75c961ac-4eac-4209-b49e-e62b5f57230a.png
tags: github, git, devops, 90daysofdevops, trainwithshubham

---

**Task 1. What is Git and why is it important?**

Git is a version control system that allows developers to track changes to their code over time. It was created by Linus Torvalds in 2005 and has since become one of the most widely used tools in the software development industry.

Git is important for several reasons:

1. Collaboration: Git enables multiple developers to work on the same codebase simultaneously without interfering with each other's work. This is achieved through branching and merging, which allow developers to create separate copies of the code and then integrate their changes seamlessly.
    
2. Version control: Git provides a complete history of changes made to the codebase, which helps developers keep track of what changes were made, who made them, and when. This is especially useful when debugging issues or rolling back to previous versions of the code.
    
3. Backup: Git also serves as a backup mechanism for code. Since every change is tracked and stored, developers can easily recover lost or deleted code from the Git repository.
    
4. Open source: Git is an open-source tool, which means it's free to use and anyone can contribute to its development. This has led to a large and active community of developers who contribute to the tool's development and help improve its functionality and features.
    

Overall, Git is an essential tool for modern software development and has revolutionized the way developers collaborate and manage code.

**Task 2. What is difference Between Main Branch and Master Branch?**

In Git, "main" and "master" branches are both used as the default branch name in different contexts. The difference between them is mostly historical and political.

Traditionally, the default branch in Git was named "master". This name was used in the original Git documentation and in many popular Git workflows. However, some people have argued that the term "master" has negative connotations due to its association with slavery, and have therefore advocated for the use of "main" instead.

In response to these concerns, many Git hosting platforms (such as GitHub and GitLab) have started using "main" as the default branch name. This has led to a shift in the industry towards using "main" instead of "master".

However, it's important to note that the difference between "main" and "master" is mostly cosmetic. They both serve the same purpose as the default branch in Git, which is to serve as the starting point for new development and to be the branch that contains the most up-to-date version of the code.

Ultimately, whether you use "main" or "master" as the default branch in your Git repository is a matter of personal preference and your organization's policies.

**Task 3. Can you explain the difference between Git and GitHub?**

Git and GitHub are related but different tools.

Git is a distributed version control system that allows developers to track changes to their code over time. It was created by Linus Torvalds in 2005 and has since become one of the most widely used tools in the software development industry. Git allows developers to work on the same codebase simultaneously, merge changes together, and track the history of changes to the codebase.

GitHub, on the other hand, is a web-based hosting service for Git repositories. It provides a graphical user interface that makes it easier to manage Git repositories and collaborate with other developers. GitHub also provides additional features such as issue tracking, pull requests, and code reviews, which help developers to work together more effectively.

In short, Git is a tool for version control, while GitHub is a platform for hosting and collaborating on Git repositories. However, it's worth noting that there are other Git hosting platforms besides GitHub, such as GitLab and Bitbucket.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681010588107/f4a9514e-b3ca-49b0-9a8e-6afccb62938a.jpeg align="center")

**Task 4. How do you create a new repository on GitHub?**

To create a new repository on GitHub, follow these steps:

1. Sign in to your GitHub account.
    
2. Click the "+" sign in the top-right corner of the page.
    
3. Select "New repository" from the dropdown menu.
    
4. Give your repository a name. The name should be descriptive and should give an idea of what your repository contains.
    
5. Optionally, add a description for your repository to give more information about it.
    
6. Choose whether you want your repository to be public or private. Public repositories are visible to anyone, while private repositories are only visible to you and any collaborators you add.
    
7. Select "Initialize this repository with a README" if you want to create a new file with some initial content.
    
8. Click "Create repository".
    

Your new repository is now created on GitHub. You can start adding files and making changes to your repository by using Git commands or by using the GitHub website interface.

**Task 5. What is difference between local & remote repository? How to connect local to remote?**

n Git, a local repository is the copy of the repository that is stored on your local machine, while a remote repository is the copy of the repository that is stored on a remote server, such as GitHub or GitLab.

The main difference between the two is that a local repository is accessible only on your local machine, while a remote repository can be accessed by multiple users and can be used for collaboration.

To connect your local repository to a remote repository, you need to perform the following steps:

1. Create a new repository on the remote server, such as GitHub or GitLab.
    
2. In your local repository, open a terminal or Git Bash window and navigate to the root directory of your local repository.
    
3. Run the following command to add a remote repository URL:
    
    ```bash
    git remote add origin <remote repository URL>
    ```
    

Replace `<remote repository URL>` with the URL of your remote repository.

1. Verify that the remote repository is added by running the following command:
    
    ```bash
    git remote -v
    ```
    
    This will list all the remote repositories that are currently connected to your local repository.
    
2. Push your local repository changes to the remote repository by running the following command:
    
    ```bash
    git push -u origin master
    ```
    
    This command will push the changes in your local repository's "master" branch to the remote repository.
    
    After these steps, your local repository will be connected to the remote repository, and you can start collaborating with others by pushing and pulling changes between the two repositories.
    
    **task-1: - Set your user name and email address, which will be associated with your commits.**
    
    To set your user name and email address in Git, you can use the following commands:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681012254498/1ec9a7e7-593c-4bf0-9d7d-0b058ab9a42e.png align="center")
    
    The `--global` flag sets these values globally, which means they will be used for all Git repositories on your machine unless you override them in a local repository using the same commands without the `--global` flag.
    
    Once you have set your user name and email address, Git will use them to associate your commits with your identity.
    
    **task-2:**
    
    **\-Create a repository named "Devops" on GitHub**
    
    **\- Connect your local repository to the repository on GitHub.**
    
    **\- Create a new file in Devops/Git/Day-02.txt & add some content to it**
    
    **\- Push your local commits to the repository on GitHub**
    
    1. To create a repository named "Devops" on GitHub, you can follow the steps I mentioned earlier:
        
        * Sign in to your GitHub account.
            
        * Click the "+" sign in the top-right corner of the page.
            
        * Select "New repository" from the dropdown menu.
            
            ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681012589517/fa73e5c5-a9ad-4c55-8c0f-c733c165e190.png align="center")
            
        * Give your repository a name as "Devops".
            
        * Optionally, add a description for your repository.
            
        * Choose whether you want your repository to be public or private.
            
        * Click "Create repository".
            
            ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681012731132/3e267ac8-4d9e-4924-9ac7-ced74ef573a6.png align="center")
            
            1. To connect your local repository to the repository on GitHub, you can follow the steps I mentioned earlier:
                
            
            * Open a terminal or Git Bash window and navigate to the root directory of your local repository.
                
            * Run the following command to add a remote repository URL:
                
                ```bash
                git remote add origin https://github.com/Dhananjaykul/Devops.git
                ```
                
        * Verify that the remote repository is added by running the following command:
            
            ```bash
            git remote -v
            ```
            
            This will list all the remote repositories that are currently connected to your local repository as shown below:
            
            ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681013953510/d876dcff-fc52-414c-9a02-3febb9ea1119.png align="center")
            

1. To create a new file in Devops/Git/Day-02.txt & add some content to it, you can follow these steps:
    
    * In your local repository, navigate to the "Devops" folder.
        
    * Create a new folder named "Git".
        
    * Navigate into the "Git" folder.
        
    * Create a new file named "Day-02.txt".
        
    * Add some content to the file.
        
2. To push your local commits to the repository on GitHub, you can follow these steps:
    

Add the new file to the staging area by running the following command:

```bash
git add .
```

This will stage all the changes you have made in your local repository.

Commit the changes by running the following command:

```bash
git commit -m "Added Day-02.txt file to Devops/Git folder"
```

Push the changes to the remote repository by running the following command:

```bash
git push -u origin master
```

This will push the changes in your local repository's "master" branch to the remote repository.

After these steps, the new file you created in the "Devops/Git" folder of your local repository should be pushed to the "Devops" repository on GitHub.