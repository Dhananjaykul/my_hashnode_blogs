---
title: "Linux & Git-GitHub Cheat-sheet"
seoTitle: "Linux,shell Scripting ,git and github"
datePublished: Wed Apr 12 2023 09:37:45 GMT+0000 (Coordinated Universal Time)
cuid: clgdi070n000009lga7l9gwwk
slug: linux-git-github-cheat-sheet
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1681292178988/956a925a-1cf8-47ac-9758-4ec4e67e8834.jpeg
tags: linux, devops, 90daysofdevops, trainwithshubham, devopscommunity-90daysofdevops-devops-automation-scaling-infrastructure-cicd-softwaredevelopment-itoperations-agile-collaboration-communication-continuousintegration-continuousdelivery-efficiency-streamlining-quality-testing-deployment-versioning-infrastructureascode-business-competition-jobsatisfaction-employeeretention-customersatisfaction

---

### Linux Command Shell Scripting Cheatsheet:

1. Basic commands:
    

* `ls`: lists files and directories
    
* `cd`: changes directory
    
* `pwd`: prints the working directory
    
* `mkdir`: creates a new directory
    
* `rm`: removes files or directories
    
* `cp`: copies files or directories
    
* `mv`: moves files or directories
    
* `cat`: displays file contents
    
* `grep`: searches for a pattern in a file or output
    
* `echo`: prints a message to the terminal
    
* `chmod`: changes file permissions
    
* `sudo`: executes a command as the superuser
    

1. Variables:
    

* To define a variable: `variable_name=value`
    
* To access a variable: `$variable_name`
    
* To use arithmetic operations: `$(($variable_name + 1))`
    

1. Control structures:
    

* `if` statement:
    

```bash
if [ condition ]; then
  command1
else
  command2
fi
```

* `for` loop:
    

```bash
for variable in list; do
  command
done
```

* `while` loop:
    

```bash
while [ condition ]; do
  command
done
```

1. Functions:
    

* To define a function:
    

```bash
function_name() {
  command1
  command2
}
```

* To call a function: `function_name`
    

1. Input/output:
    

* `read` command: reads input from the user
    

```bash
read variable_name
```

* `echo` command: prints output to the terminal
    

```bash
echo "message"
```

Git and GitHub Cheatsheet:

1. Basic commands:
    

* `git init`: initializes a new Git repository
    
* `git clone`: clones a remote Git repository
    
* `git add`: adds changes to the staging area
    
* `git commit`: commits changes to the repository
    
* `git push`: pushes changes to a remote repository
    
* `git pull`: pulls changes from a remote repository
    
* `git status`: displays the status of the repository
    
* `git log`: displays the commit history
    

1. Branching:
    

* `git branch`: lists all branches
    
* `git branch branch_name`: creates a new branch
    
* `git checkout branch_name`: switches to a different branch
    
* `git merge branch_name`: merges a branch into the current branch
    

1. Collaboration:
    

* `git remote`: lists all remote repositories
    
* `git remote add remote_name remote_url`: adds a new remote repository
    
* `git fetch`: fetches changes from a remote repository
    
* `git merge origin/branch_name`: merges changes from a remote branch into the current branch
    
* `git pull --rebase`: pulls changes from a remote repository and rebases local changes on top
    

1. GitHub:
    

* `git push -u origin branch_name`: pushes a new branch to a remote repository
    
* `git pull-request`: creates a new pull request
    
* `git remote add upstream upstream_url`: adds the original repository as a remote upstream
    
* `git fetch upstream`: fetches changes from the original repository
    
* `git merge upstream/master`: merges changes from the original repository into the current branch
    

Note: It's important to ensure that your changes are well tested before pushing to the remote repository, and to always fetch and merge changes before pushing your own changes to prevent conflicts.