---
title: "Understanding Amazon Relational Database Service (RDS) on AWS - A Beginner's Guide"
seoTitle: "Amazon RDS on AWS - Setting up a Free-Tier MySQL Instance"
seoDescription: "Learn how to set up a free-tier MySQL instance on Amazon RDS, a managed database service on AWS."
datePublished: Sun May 14 2023 00:55:07 GMT+0000 (Coordinated Universal Time)
cuid: clhmpfcd6000309mh38v9anvz
slug: understanding-amazon-relational-database-service-rds-on-aws-a-beginners-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1683866295557/292153de-35fa-44ec-b04b-173c0b81cf66.png
tags: aws, devops, 90daysofdevops

---

Are you looking for a scalable and efficient way to set up and manage your relational databases in the cloud? Look no further than Amazon Relational Database Service (RDS) on AWS. In this blog, we will explore the basics of RDS, its features, and how to set up a free-tier MySQL RDS instance on AWS. We will also walk you through the steps to create an EC2 instance, an IAM role with RDS access, and how to connect your EC2 instance with your RDS instance using a MySQL client.

## <mark>What is Amazon Relational Database Service (RDS)?</mark>

Amazon RDS is a managed database service that allows you to set up, operate, and scale a relational database in the cloud. You can choose from six different database engines including Amazon Aurora, PostgreSQL, MySQL, MariaDB, Oracle, and Microsoft SQL Server. With RDS, you can offload the administrative tasks of managing a database to AWS so you can focus on your application development.

## <mark>Benefits of using Amazon RDS</mark>

* Fully Managed Service: AWS manages the infrastructure, upgrades, backups, and patching of your database.
    
* Scalability: You can easily scale your database up or down as your application demands.
    
* High Availability: RDS supports Multi-AZ deployments, which automatically replicates data to a secondary instance in a different Availability Zone (AZ).
    
* Security: RDS provides security features such as encryption at rest, encryption in transit, and network isolation.
    
* Cost-Effective: You only pay for the resources you use, and there is no upfront cost or long-term commitment.
    

## <mark>Setting up a free-tier RDS instance of MySQL on AWS</mark>

Follow the steps below to create a free-tier RDS instance of MySQL on AWS:

### ***Step 1: Sign in to AWS***

*Sign in to your AWS account using your credentials.*

### *Step 2: Create a Security Group for RDS*

*Create a Security Group that allows inbound traffic from your EC2 instance to your RDS instance. You can do this by going to the EC2 Dashboard, clicking on Security Groups on the left sidebar, and then clicking on Create Security Group.*

### *Step 3: Create a Free-tier RDS instance of MySQL*

*Navigate to the RDS Dashboard, click on Create Database, and then select MySQL. Choose the free-tier option and set the necessary configurations, such as instance class, storage type, and allocated storage. Set the Security Group created in Step 2 as the inbound source.*

### *Step 4: Create an EC2 Instance*

*Create an EC2 instance that will host your application. You can follow the steps provided in the AWS documentation to launch an EC2 instance.*

### *Step 5: Create an IAM role with RDS access*

*Create an IAM role that has permissions to access RDS resources. You can do this by navigating to the IAM Dashboard, clicking on Roles on the left sidebar, and then clicking on Create role. Choose EC2 as the trusted entity, and attach the AmazonRDSFullAccess policy to the role.*

### *Step 6: Assign the IAM role to your EC2 instance*

*Assign the IAM role you created in Step 5 to your EC2 instance. You can do this by going to the EC2 Dashboard, selecting your instance, clicking on Actions, and then clicking on Instance Settings &gt; Attach/Replace IAM Role.*

### *Step 7: Connect your EC2 instance with your RDS instance*

*Once your RDS instance is up and running, you can get the credentials to connect to your MySQL database using a MySQL client. You can find the necessary details, such as endpoint, port, username, and password in the RDS Dashboard.*

*Connect to your EC2 instance using SSH or any other remote access method and install a MySQL client. You can use the following command to install the MySQL client on an Amazon Linux 2 instance:*

```bash
sudo amazon-linux-extras install epel
sudo yum install mysql
```

*After installing the MySQL client, you can connect to your RDS instance using the following command:*

```bash
mysql -h <endpoint> -P <port> -u <username> -p
```

*Replace* `<endpoint>`*,* `<port>`*,* `<username>`*, and* `<password>` *with the details obtained from the RDS Dashboard.*

*Congratulations, you have successfully set up a free-tier RDS instance of MySQL on AWS and connected it to your EC2 instance using a MySQL client. You can now start developing your application and let AWS manage your database for you.*

### <mark>Conclusion</mark>

Amazon RDS is a powerful managed database service that simplifies the process of setting up, operating, and scaling relational databases in the cloud. In this blog, we walked you through the steps to create a free-tier RDS instance of MySQL, an EC2 instance, and an IAM role with RDS access. We also showed you how to connect your EC2 instance with your RDS instance using a MySQL client. With RDS, you can focus on your application development while AWS manages your database for you.