---
title: "📝Provisioning an AWS EC2 Instance using Terraform 🚀"
seoTitle: "📝Provisioning an AWS EC2 Instance using Terraform 🚀"
seoDescription: "Learn how to provision AWS EC2 instances using Terraform in this detailed blog.Discover the power of infrastructure as code (IaC) and automate your infra."
datePublished: Fri Jun 02 2023 06:47:08 GMT+0000 (Coordinated Universal Time)
cuid: clie7d7xq001209l8bfvsefjr
slug: provisioning-an-aws-ec2-instance-using-terraform
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1685687642889/e6048799-675c-498e-9f4c-10d561ae5bff.webp
tags: devops, terraform, infrastructure-as-code, 90daysofdevops

---

Hello, fellow tech enthusiasts! Welcome back to another exciting day of our coding journey. Today, we have an interesting task at hand: provisioning an AWS EC2 instance using Terraform. So, let's dive right in and explore the wonderful world of infrastructure as code (IaC) with Terraform! 🌍💻

🔑 **Prerequisites:**

Before we begin, let's ensure we have a few prerequisites in place to smoothly complete our task:

1. **IAM User with Administrative Access:** Make sure you have an IAM user with administrative access on your AWS account. This will allow us to perform the necessary actions for provisioning an EC2 instance.
    
2. **AWS CLI Configuration:** To interact with AWS services, we need to configure the AWS Command Line Interface (CLI) on our local machine. Open your integrated terminal in VS Code and run the following command:
    

```bash
aws configure
```

Enter your AWS Access Key ID, AWS Secret Access Key, default region name, and default output format when prompted.

✨ **Let's get started!**

Step 1: **Create a Terraform Configuration File**

Create a new file named [`main.tf`](http://main.tf) in your project directory. This file will contain the Terraform configuration code.

Step 2: **Initialize Terraform**

In your integrated terminal, navigate to the project directory and run the following command to initialize Terraform:

```bash
terraform init
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685687098104/d965b3bb-ccdd-47c9-ab63-76647f4179c3.png align="center")

This will download the necessary provider plugins and set up your working directory.

Step 3: **Define the EC2 Instance Resource**

Inside the [`main.tf`](http://main.tf) file, add the following Terraform code to define the AWS EC2 instance resource:

```bash
resource "aws_instance" "aws_ec2_test" {
  count         = 4
  ami           = "ami-053b0d53c279acc90"
  instance_type = "t2.micro"

  tags = {
    Name = "TerraformTestServerInstance"
  }
}
```

In this code, we are provisioning four EC2 instances of type `t2.micro`, using the specified Amazon Machine Image (AMI). The instances will be tagged with the name "TerraformTestServerInstance".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685687028507/d3d5d1b6-91f5-498e-95fd-7cb28e8466e8.png align="center")

Step 4: **Provision the EC2 Instances**

To provision the EC2 instances, run the following command in your integrated terminal:

```bash
terraform apply
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685687198677/dd89bbd2-e01a-4e77-a3ac-332588497c7c.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685687233031/4775cf1e-c134-41b1-98c2-dc83d193f37d.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685687270006/694160d9-a615-4a21-b9dd-5f8ec808e381.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685687305188/9d3481a8-0fc4-438f-9505-09fe399d478a.png align="center")

Review the changes to be made, and when prompted, enter "yes" to proceed with the provisioning. Terraform will create the EC2 instances based on the provided configuration.

Step 5: **Verify the EC2 Instances**

After the provisioning is complete, navigate to your AWS Management Console. Open the EC2 service and verify that the instances have been successfully created. You should see four instances with the specified tags.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685687387561/25228ec1-39f3-4322-8f6b-fa3fde692fc5.png align="center")

Congratulations! You have successfully provisioned AWS EC2 instances using Terraform. 🎉🎉

🔒 **Clean Up:**

To avoid unnecessary costs, it's important to clean up the resources we provisioned. In your integrated terminal, run the following command:

```bash
terraform destroy
```

Review the resources to be destroyed, and when prompted, enter "yes" to proceed.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685687504271/717e49bc-aaf0-4a43-b55b-82eee9e73ec7.png align="center")

Terraform will destroy the EC2 instances, ensuring a clean environment.

📝 **Wrapping Up:**

In today's task, we explored the power of Terraform to provision infrastructure as code. We learned how to define an AWS EC2 instance resource using Terraform and successfully provisioned multiple instances. By adopting infrastructure as code practices, we can automate and version our infrastructure, making it easier to manage and collaborate.

Now that you have accomplished

this task, pat yourself on the back for a job well done! Stay tuned for more exciting adventures in our coding journey. Until then, happy coding! 😄👩‍💻👨‍💻