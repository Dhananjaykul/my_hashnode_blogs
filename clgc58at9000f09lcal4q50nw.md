---
title: "Advance Git & GitHub for DevOps Engineers: Part-2"
seoTitle: "Advance Git & Github"
seoDescription: "Go through some advance concepts used in git such as git stash, rebase and resolving merge conflicts"
datePublished: Tue Apr 11 2023 10:52:22 GMT+0000 (Coordinated Universal Time)
cuid: clgc58at9000f09lcal4q50nw
slug: advance-git-github-for-devops-engineers-part-2
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1681207307197/67b10f23-5afa-412f-8757-4d38487219ed.jpeg
tags: linux, devops, 90daysofdevops, trainwithshubham

---

**Git stash**

Git stash is a command that allows you to temporarily save changes you have made in your working directory, without committing them. This is useful when you need to switch to a different branch to work on something else, but you don't want to commit the changes you've made in your current branch yet. To use Git stash, you first create a new branch and make some changes to it. Then you can use the command git stash to save those changes. This will remove the changes from your working directory and record them in a new stash. You can apply these changes later. git stash list command shows the list of stashed changes. You can also use git stash drop to delete a stash and git stash clear to delete all the stashes.

**Cherry-pick**

Git cherry-pick is a command that allows you to select specific commits from one branch and apply them to another. This can be useful when you want to selectively apply changes that were made in one branch to another. To use git cherry-pick, you first create two new branches and make some commits to them. Then you use git cherry-pick &lt;commit\_hash&gt; command to select the specific commits from one branch and apply them to the other.##

**Resolving Conflicts:** Conflicts can occur when you merge or rebase branches that have diverged, and you need to manually resolve the conflicts before git can proceed with the merge/rebase. git status command shows the files that have conflicts, git diff command shows the difference between the conflicting versions and git add command is used to add the resolved files.

**Task-01** \- Create a new branch and make some changes to it. - Use git stash to save the changes without committing them. - Switch to a different branch, make some changes and commit them. - Use git stash pop to bring the changes back and apply them on top of the new commits.

here are the steps to complete the task:

1. Create a new branch using the following command:
    
    ```bash
    git checkout -b my-new-branch
    ```
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681208668263/b180404a-345e-47dd-8a6f-ab3729deab19.png align="center")

1. Make some changes to the new branch, such as adding or modifying code files.
    
2. Use git stash to save the changes without committing them, using the following command:
    
    ```bash
    git stash save "My new branch changes"
    ```
    
3. Switch to a different branch, such as the main branch, using the following command:
    
    ```bash
    git checkout main
    ```
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681208846593/21d06a6a-3e83-4bd3-9d76-97efad8e0fb7.png align="center")

1. Make some changes to the main branch, such as adding or modifying code files.
    
2. Commit the changes to the main branch using the following command:
    
    ```bash
    git add .
    git commit -m "Commit message"
    ```
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681208963766/24b78cac-af98-4c9d-a521-1604aec6b436.png align="center")

1. Use git stash pop to bring the changes back and apply them on top of the new commits, using the following command:
    
    ```bash
    git stash pop
    ```
    

1. Resolve any conflicts that may arise, using the steps outlined in the previous answer.
    
2. Review the changes and commit them to the main branch if they are correct, using the following commands:
    
    ```bash
    git add .
    git commit -m "My new branch changes applied to main branch"
    ```
    

1. Push the changes to the remote repository, using the following command:
    
    ```bash
    git push origin main
    ```
    
    And that's it! You've successfully created a new branch, made changes to it, switched to a different branch, made changes and committed them, and applied the new branch changes on top of the new commits using git stash.
    

**Task-02** - In version01.txt of development branch add below lines after “This is the bug fix in development branch” that you added in Day10 and reverted to this commit. - Line2&gt;&gt; After bug fixing, this is the new feature with minor alteration” Commit this with message “ Added feature2.1 in development branch” - Line3&gt;&gt; This is the advancement of previous feature Commit this with message “ Added feature2.2 in development branch” - Line4&gt;&gt; Feature 2 is completed and ready for release Commit this with message “ Feature2 completed” - All these commits messages should be reflected in Production branch too which will come out from Master branch (Hint: try rebase).

here are the steps to complete the task:

1. Initialize a new Git repository by running the following command in the terminal:
    

```bash
git init
```

1. Create a new file called version01.txt by running the following command:
    

```bash
touch version01.txt
```

1. Open version01.txt in a text editor and add the following line:
    

```bash
This is the bug fix in development branch
```

1. Commit the changes with the message "Initial commit" using the following commands:
    

```bash
git add .
git commit -m "Initial commit"
```

1. Add the following line to version01.txt:
    

```bash
After bug fixing, this is the new feature with minor alteration
```

1. Commit the changes with the message "Added feature2.1 in development branch" using the following commands:
    

```bash
add .
git commit -m "Added feature2.1 in development branch"
```

1. Add the following line to version01.txt:
    

```bash
This is the advancement of previous feature
```

1. Commit the changes with the message "Added feature2.2 in development branch" using the following commands:
    

```bash
codegit add .
git commit -m "Added feature2.2 in development branch"
```

1. Add the following line to version01.txt:
    

```bash
Feature 2 is completed and ready for release
```

1. Commit the changes with the message "Feature2 completed" using the following commands:
    

```bash
git add .
git commit -m "Feature2 completed"
```

1. Create a new branch called production from the master branch using the following command:
    

```bash
git checkout master
git branch production
```

1. Switch to the production branch using the following command:
    

```bash
git checkout production
```

1. Merge the changes from the development branch to the production branch using the following command:
    

```bash
git merge --no-ff development
```

1. Rebase the commits in the production branch with the commits in the development branch using the following command:
    

```bash
git rebase development
```

1. Push the changes to the remote repository using the following command:
    

```bash
git push origin production
```

And that's it! You've successfully added new lines to version01.txt, committed them with appropriate messages, created a production branch from the master branch, merged the changes from the development branch to the production branch, and rebased the commits in the production branch with the commits in the development branch.

**Task-03** - In Production branch Cherry pick Commit “Added feature2.2 in development branch” and added below lines in it: - Line to be added after Line3&gt;&gt; This is the advancement of previous feature - Line4&gt;&gt;Added few more changes to make it more optimized. - Commit: Optimized the feature

here are the steps to complete the task:

1. Make sure you have the latest version of the production branch by running the following command:
    

```bash
git checkout production
git pull origin production
```

1. Cherry-pick the commit "Added feature2.2 in development branch" using the following command:
    

```bash
git cherry-pick <commit-hash>
```

Note: Replace `<commit-hash>` with the actual hash of the commit you want to cherry-pick. You can get the commit hash by running `git log` and finding the commit you want.

1. Open the version01.txt file in a text editor and add the following line after "This is the advancement of previous feature":
    

```bash
Added few more changes to make it more optimized.
```

1. Commit the changes with the message "Optimized the feature" using the following commands:
    

```bash
git add .
git commit -m "Optimized the feature"
```

1. Push the changes to the remote repository using the following command:
    

```bash
git push origin production
```

And that's it! You've successfully cherry-picked a commit from the development branch to the production branch and added new lines to it.