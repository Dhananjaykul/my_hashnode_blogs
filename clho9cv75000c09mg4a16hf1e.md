---
title: "Deploy Wordpress website on AWS"
seoTitle: "How to Deploy a WordPress Website on AWS using Ubuntu EC2 Instance"
seoDescription: "Learn to deploy a WordPress site on AWS using an Ubuntu EC2 instance in this step-by-step guide. Build a scalable, reliable, and secure site on the cloud"
datePublished: Mon May 15 2023 03:00:50 GMT+0000 (Coordinated Universal Time)
cuid: clho9cv75000c09mg4a16hf1e
slug: deploy-wordpress-website-on-aws
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1684119441737/baf190c8-f2d2-407c-b592-d2bd4e7c8610.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1684119640601/50e6b5bd-5dfd-416b-ac8c-7d309fdb69b7.jpeg
tags: aws, wordpress, devops, 90daysofdevops, trainwithshubham

---

WordPress is a popular content management system (CMS) used by over 30% of all websites on the internet. It's a versatile platform that can be used to create a wide variety of websites, from simple blogs to complex e-commerce sites. In this guide, we'll show you how to deploy a WordPress website on AWS using an Ubuntu EC2 instance.

### **<mark>Why Use AWS to Deploy WordPress?</mark>**

Amazon Web Services (AWS) is a cloud computing platform that provides a wide range of services, including hosting and infrastructure management. By using AWS to deploy your WordPress website, you can take advantage of the platform's scalability, security, and reliability. AWS makes it easy to set up and manage your WordPress site, so you can focus on creating great content and growing your audience.

### **<mark>Prerequisites</mark>**

Before we get started, you'll need to have the following:

* An AWS account
    
* An Ubuntu EC2 instance
    
* A domain name (optional)
    
* Basic knowledge of WordPress and Linux command line
    

### **<mark>Step 1: Create an RDS Instance</mark>**

The first step in deploying a WordPress website on AWS is to create an Amazon RDS instance to store your data. Here's how to do it:

1. Log in to the AWS Management Console.
    
2. Click on "Services" and select "RDS" under the "Database" category.
    
3. Click the "Create database" button.
    
4. Choose the "Standard create" option.
    
5. Select "MySQL" as the engine type.
    
6. Choose the version of MySQL you want to use.
    
7. Select the "Free tier" option for the instance class.
    
8. Set the username and password for the database.
    
9. Choose a name for your database and leave the rest of the options as default.
    
10. Click "Create database" to launch the RDS instance.
    

### **<mark>Step 2: Launch an Ubuntu EC2 Instance</mark>**

Next, you'll need to launch an Ubuntu EC2 instance to host your WordPress site. Here's how to do it:

1. Log in to the AWS Management Console.
    
2. Click on "Services" and select "EC2" under the "Compute" category.
    
3. Click the "Launch instance" button.
    
4. Choose the Ubuntu Server AMI.
    
5. Choose an instance type that is appropriate for your needs.
    
6. Configure the instance details, including the number of instances and the VPC settings.
    
7. Add storage as needed.
    
8. Add any required tags to your instance.
    
9. Configure your security group to allow access to your instance.
    
10. Launch the instance.
    

### **<mark>Step 3: Connect to Your EC2 Instance</mark>**

Once your Ubuntu EC2 instance is up and running, you'll need to connect to it using SSH. Here's how to do it:

1. Open a terminal window on your local machine.
    
2. Navigate to the directory where your EC2 key pair is stored.
    
3. Run the following command to change the permissions of your EC2 key pair file:
    

```bash
chmod 400 your-key-pair.pem
```

1. Run the following command to connect to your EC2 instance:
    

```bash
ssh -i your-key-pair.pem ubuntu@your-ec2-instance-public-ip
```

### **<mark>Step 4: Install and Configure WordPress</mark>**

Now that you're connected to your Ubuntu EC2 instance, you can install and configure WordPress. Here's how to do it:

1. Update your Ubuntu server by running the following command:
    

```bash
sudo apt update && sudo apt upgrade -y
```

1. Install Apache by running the following command:
    

```bash
sudo apt install apache2 -y
```

1. Install MySQL client by running the following command:
    

```bash
sudo apt install mysql-client -y
```

1. Install PHP and required modules by running the following command:
    

```bash
sudo apt install php libapache2-mod-php php-mysql php-curl php-gd php-json php-zip php-xml -y
```

1. Restart Apache by running the following command:
    

```bash
sudo systemctl restart apache2
```

1. Download the latest version of WordPress by running the following command:
    

```bash
wget https://wordpress.org/latest.tar.gz
```

1. Extract the WordPress files by running the following command:
    

```bash
tar -xvzf latest.tar.gz
```

1. Copy the WordPress files to the Apache document root directory by running the following command:
    

```bash
sudo cp -r wordpress/* /var/www/html/
```

1. Create a new MySQL database and user for WordPress by running the following commands:
    

```bash
mysql -u root -p
CREATE DATABASE wordpress;
CREATE USER 'wordpressuser'@'%' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON wordpress.* TO 'wordpressuser'@'%';
FLUSH PRIVILEGES;
exit;
```

1. Rename the WordPress configuration file and add your database details by running the following command:
    

```bash
cd /var/www/html
sudo mv wp-config-sample.php wp-config.php
sudo nano wp-config.php
```

1. In the wp-config.php file, replace the following lines with your database details:
    

```bash
define('DB_NAME', 'database_name_here');
define('DB_USER', 'username_here');
define('DB_PASSWORD', 'password_here');
define('DB_HOST', 'localhost');
```

with:

```bash
define('DB_NAME', 'wordpress');
define('DB_USER', 'wordpressuser');
define('DB_PASSWORD', 'password');
define('DB_HOST', 'your-rds-endpoint');
```

Note: You can find your RDS endpoint on the RDS console.

1. Save and close the wp-config.php file by pressing "Ctrl+X", then "Y", and finally "Enter".
    

### **<mark>Step 5: Launch Your WordPress Site</mark>**

Now that you've installed and configured WordPress, you can launch your site by visiting your EC2 instance's public IP address or domain name in your web browser.

If you want to use a domain name, you'll need to create an A record in your DNS provider's settings that points to your EC2 instance's public IP address.

Congratulations! You've successfully deployed a WordPress website on AWS using an Ubuntu EC2 instance.

### **<mark>Conclusion</mark>**

Deploying a WordPress website on AWS using an Ubuntu EC2 instance is a great way to take advantage of AWS's powerful cloud infrastructure. By following the steps in this guide, you can set up a WordPress site that is scalable, reliable, and secure. With your WordPress site up and running, you can focus on creating great content and growing your audience.