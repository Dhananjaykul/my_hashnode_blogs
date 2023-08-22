---
title: "File Permissions and Access Control Lists"
seoTitle: "Understanding File Permissions and ACL on UNIX-like Systems"
seoDescription: "This article provides a beginner-friendly introduction to file permissions and Access Control Lists (ACL) on UNIX-like systems."
datePublished: Thu Apr 06 2023 06:15:01 GMT+0000 (Coordinated Universal Time)
cuid: clg4q4d9e000n09l4dmku36d8
slug: file-permissions-and-access-control-lists
tags: linux, devops, shell-script, 90daysofdevops, trainwithshubham

---

## **<mark>Task1. Create a simple file and do `ls -ltr` to see the details of the files. As a task change the user permissions of the file and note the changes after `ls -ltr`</mark>**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680758449074/fe706192-753b-4e9d-b2b4-8c424af8ee1d.png align="center")

### <mark>Here a file.txt is created with permissions for user as read and write,for the group also read and write and for others read only.</mark>

Now lets modify the file permisions for user to read write and execute.and deny all file access permissions to group and others.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680759172927/eb2ac049-9ab0-4247-aefe-4052b4cb63a1.png align="center")

## **<mark>Task 2.Write an article about File Permissions based on your understanding from the notes.</mark>**

File permissions are an essential aspect of any modern operating system. They are designed to control who can access, read, write or execute a file. In this article, we'll explore the basics of file permissions, including how they work, why they are important, and how to modify them.

Understanding File Permissions: File permissions are a set of rules that determine what actions can be performed on a file or directory. There are three types of permissions: read, write, and execute. Read permission allows a user to view the contents of a file, write permission allows a user to modify the contents of a file, and execute permission allows a user to run a program or script.

Each file and directory has a set of permissions associated with it. Permissions can be granted to three different groups: the file owner, the group that the file belongs to, and all other users (also known as "world" or "other"). Each group can be granted different permissions, allowing for fine-grained control over who can access a file and what they can do with it.

Permission Settings: File permissions are represented by a three-digit number. Each digit corresponds to a different group: owner, group, and world. The first digit represents the permissions for the owner, the second digit represents the permissions for the group, and the third digit represents the permissions for all other users.

Each digit can have a value between 0 and 7, with each value representing a different combination of read, write, and execute permissions. The value of 0 means no permissions are granted, while the value of 7 means all permissions are granted.

Here is a table showing the different permission settings:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680759578205/fdf4a1ef-de97-44da-8223-126b63c4cc58.png align="center")

<mark>Modifying File Permissions</mark>: File permissions can be modified using the chmod command in the terminal. The chmod command allows you to change the permissions for the owner, group, and world.

```bash
chmod [permissions] [file]
```

The \[permissions\] argument is a three-digit number that represents the new permissions. The \[file\] argument is the name of the file or directory that you want to modify the permissions for.

For example, to give the owner read, write, and execute permissions, while giving the group and world only read and execute permissions, you would use the following command:

```bash
chmod 750 myfile.txt
```

<mark>File Permissions - An Introduction</mark>

File permissions are an essential aspect of any modern operating system. They are designed to control who can access, read, write or execute a file. In this article, we'll explore the basics of file permissions, including how they work, why they are important, and how to modify them.

<mark>Understanding File Permissions</mark>

File permissions are a set of rules that determine what actions can be performed on a file or directory. There are three types of permissions: read, write, and execute. Read permission allows a user to view the contents of a file, write permission allows a user to modify the contents of a file, and execute permission allows a user to run a program or script.

Each file and directory has a set of permissions associated with it. Permissions can be granted to three different groups: the file owner, the group that the file belongs to, and all other users (also known as "world" or "other"). Each group can be granted different permissions, allowing for fine-grained control over who can access a file and what they can do with it.

<mark>Permission Settings</mark>

File permissions are represented by a three-digit number. Each digit corresponds to a different group: owner, group, and world. The first digit represents the permissions for the owner, the second digit represents the permissions for the group, and the third digit represents the permissions for all other users.

Each digit can have a value between 0 and 7, with each value representing a different combination of read, write, and execute permissions. The value of 0 means no permissions are granted, while the value of 7 means all permissions are granted.

Here is a table showing the different permission settings:

| **Value** | **Binary** | **Permissions** |
| --- | --- | --- |
| 0 | 000 | No permissions |
| 1 | 001 | Execute permission only |
| 2 | 010 | Write permission only |
| 3 | 011 | Write and execute permissions |
| 4 | 100 | Read permission only |
| 5 | 101 | Read and execute permissions |
| 6 | 110 | Read and write permissions |
| 7 | 111 | All permissions |

<mark>Modifying File Permissions</mark>

File permissions can be modified using the chmod command in the terminal. The chmod command allows you to change the permissions for the owner, group, and world.

The syntax of the chmod command is as follows:

```bash
chmod [permissions] [file]
```

The \[permissions\] argument is a three-digit number that represents the new permissions. The \[file\] argument is the name of the file or directory that you want to modify the permissions for.

For example, to give the owner read, write, and execute permissions, while giving the group and world only read and execute permissions, you would use the following command:

```bash
chmod 750 myfile.txt
```

This command sets the owner to have all permissions (7), the group to have read and execute permissions (5), and the world to have no permissions (0).It is important to note that changing file permissions can have security implications. You should only modify file permissions for files that you own and for which you have a good reason to modify the permissions.

<mark>Conclusion</mark>: File permissions are an essential aspect of any modern operating system. They allow for fine-grained control over who can access a file and what they can do with it. By understanding how file permissions work, you can ensure that your files and directories are secure and that only authorized users have access to them.

## **<mark>Task 3. Read about ACL and try out the commands `getfacl` and `setfacl`.</mark>**

ACL stands for Access Control List, which is a set of permissions attached to a file or directory that specifies which users or groups are granted access to the object and what actions they can perform. ACL provides a more flexible way of defining access permissions than the traditional UNIX file permissions, which only allow permissions for the owner, group, and others.

The `getfacl` command is used to view the ACL of a file or directory, while the `setfacl` command is used to modify the ACL. These commands are available on most UNIX-like systems.

Here are some examples of how to use these commands:

1. `getfacl`
    
    ACL stands for Access Control List, which is a set of permissions attached to a file or directory that specifies which users or groups are granted access to the object and what actions they can perform. ACL provides a more flexible way of defining access permissions than the traditional UNIX file permissions, which only allow permissions for the owner, group, and others.
    
    The `getfacl` command is used to view the ACL of a file or directory, while the `setfacl` command is used to modify the ACL. These commands are available on most UNIX-like systems.
    
    Here are some examples of how to use these commands:
    
    1. `getfacl`
        
    
    To view the ACL of a file, use the `getfacl` command followed by the file name:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680760205160/31db8271-b0cf-4788-b69b-655e21267aff.png align="center")
    
2. `setfacl`
    
    To modify the ACL of a file or directory, use the `setfacl` command followed by the options and file name:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680760671458/03170d7d-df8f-4521-978b-9efb28a4b7ea.png align="center")
    

This command grants read, write, and execute permissions to the user "ubuntu" for the file "file.txt". The `-m` option specifies that we are modifying the ACL, while the `u:ubuntu:rwx` option specifies the permission to be granted.

Here are some other options that can be used with the `setfacl` command:

* `-x`: remove a permission from a user or group.
    
* `-b`: remove all ACL entries from a file or directory.
    
* `-d`: set the default ACL for a directory. The default ACL is applied to all files and subdirectories created within the directory.
    

It's worth noting that not all filesystems support ACLs, so it's important to check whether your filesystem supports ACLs before using these commands.

In conclusion, ACL provides a more flexible way of defining access permissions than the traditional UNIX file permissions. The `getfacl` and `setfacl` commands allow you to view and modify the ACL of a file or directory.