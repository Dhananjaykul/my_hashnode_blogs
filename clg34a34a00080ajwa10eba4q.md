---
title: "Advanced Linux Shell Scripting for DevOps Engineers with User management"
seoTitle: "Efficient and Safe Linux Management with Bash, User Managing and Cron"
seoDescription: ""Maximizing Your Linux System's Efficiency and Security: A Guide to Bash Scripting, User Management, and Cron Automation""
datePublished: Wed Apr 05 2023 03:15:50 GMT+0000 (Coordinated Universal Time)
cuid: clg34a34a00080ajwa10eba4q
slug: advanced-linux-shell-scripting-for-devops-engineers-with-user-management
tags: linux, devops, shell-scripting, 90daysofdevops, trainwithshubham

---

**Task 1.** **Write a bash script createDirectories.sh that when the script is executed with three given arguments (one is directory name and second is start number of directories and third is the end number of directories ) it creates specified number of directories with a dynamic directory name.**

Here is a bash script named createDirectories.sh that creates a specified number of directories with a dynamic directory name based on the three given arguments:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680661219761/24ec3b8b-1e29-4db7-a09a-ca671056f2f4.png align="center")

To use this script, save it as [`createDirectories.sh`](http://createDirectories.sh), make it executable (`chmod 700`[`createDirectories.sh`](http://createDirectories.sh)), and then run it with three arguments in the following format:

./[createDirectories.sh](http://createDirectories.sh) &lt;directory\_name&gt; &lt;start\_number&gt; &lt;end\_number&gt;

For example, to create 5 directories named "my\_directory\_1" to "my\_directory\_5", you would run:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680662196886/d949f46b-dd82-4aec-8873-e98ace95a8b5.png align="center")

Note that if the directory name or any of the numbers have spaces or special characters, you should enclose them in quotes to ensure that they are parsed correctly.

**Task 2.** **Create a Script to backup all your work done till now.**

Here is a simple bash script that creates a backup of all your work done till now:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680662764898/9c949264-e831-4e3c-9a4b-04c42f5a9841.png align="center")

This script creates a backup archive of the current working directory in a new directory named `my_backups` under your home directory. The backup archive is compressed in gzip format and has a filename that includes the current date and time, in the format of `backup_YYYYMMDD_HHMMSS.tar.gz`.

To use this script, save it as [`backup.sh`](http://backup.sh) in your home directory or any other directory you prefer, make it executable (`chmod +x` [`backup.sh`](http://backup.sh)), and then run it:

```bash
./backup.sh
```

This will create a backup of all your work done till now and save it in the `my_backups` directory. You can also schedule this script to run periodically using a cron job or any other scheduling tool to ensure regular backups of your work.

**Task 3.** **Write About Cron and Crontab, to automate the backup Script.**

Cron is a time-based job scheduler in Unix-like operating systems that can be used to automate tasks at specific times or intervals. Cron works by reading a configuration file called the crontab file, which contains commands and instructions for running tasks at specific times or intervals.

To automate the backup script using cron, you can follow these steps:

1. Open your crontab file using the following command:
    
    ```bash
    crontab -e
    ```
    
    This will open the crontab file in the default text editor for your system.
    
2. Add a new line at the end of the file with the following format:
    
    ```bash
    * * * * * /path/to/backup.sh
    ```
    
    This line schedules the backup script to run every minute. You can customize the schedule by modifying the five fields in the line, which represent the minute, hour, day of the month, month, and day of the week, respectively. For example, to run the script every day at 2:00 AM, you can use the following line:
    
    ```bash
    0 2 * * * /path/to/backup.sh
    ```
    

Save and exit the crontab file.

After adding the line to your crontab file, cron will automatically run the backup script at the scheduled times. You can check the system logs to see if the script is running successfully and the backups are being created.

**Note** that the backup script should be executable and have the correct path specified in the crontab file. Also, it's important to test the backup script and the cron job to ensure that they are working correctly and the backups are being created as expected.

**Task 4.** **Write about User Management**

User management refers to the process of creating, modifying, and deleting user accounts on a computer system. It is an important aspect of system administration and security, as it enables the system administrator to control access to the system and the resources it contains.

In most operating systems, user accounts are associated with unique usernames and passwords, which are used to authenticate users and grant them access to the system. User accounts may also be associated with specific permissions, privileges, and settings, which control what actions a user can perform and what resources they can access.

User management tasks may include:

1. Creating new user accounts and assigning them appropriate permissions and privileges.
    
2. Modifying existing user accounts, such as changing their passwords, permissions, or settings.
    
3. Deleting user accounts that are no longer needed or have been compromised.
    
4. Managing user groups, which enable the system administrator to assign permissions and privileges to multiple users at once.
    
5. Auditing user activity, which involves monitoring and logging user actions on the system to detect potential security threats or policy violations.
    

User management is an essential part of system administration and security, as it enables the system administrator to control who has access to the system and what they can do with it. Effective user management practices can help reduce the risk of security breaches, data loss, and other security incidents.

**Task 5.** **Create 2 users and just display their Usernames**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680664072853/035965ea-134b-4012-a7d4-0889789128c4.png align="center")

The `useradd` command is used to create new user accounts. By default, it creates a new user with the specified username and assigns them a home directory and a default set of permissions and settings.

The `id -un` command is used to display the username of a user account, given their user ID (UID). The `-u` option specifies that the UID should be used instead of the username, and the `-n` option specifies that the output should be in the form of a name instead of a number.

The above commands will create two users named `user1` and `user2`, respectively, and display their usernames on the console. You can replace `user1` and `user2` with the desired usernames for your system.