---
title: "Terraform Variables: A Guide to Getting Started 🚀"
seoTitle: "Terraform Variables: A Guide to Getting Started 🚀"
seoDescription: "🎯 This comprehensive guide walks you through the significance of variables, easy steps to create them, and a deep dive into different data types. 🌟"
datePublished: Thu Jun 01 2023 02:00:25 GMT+0000 (Coordinated Universal Time)
cuid: clichonav000309k1dmfj4x9q
slug: terraform-variables-a-guide-to-getting-started
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/Hcfwew744z4/upload/704659072b72ff3df4d9f21bc611d837.jpeg
tags: devops, terraform, infrastructure-as-code, 90daysofdevops

---

Welcome to this beginner-friendly guide on Terraform variables! 🎉 In this blog post, we'll walk through the basics of using variables in Terraform and how they can enhance your infrastructure-as-code experience. So, let's dive right in! 💪

## Why Are Variables Important in Terraform?

Variables in Terraform play a crucial role in storing and managing values such as instance names, configurations, and more. They provide flexibility and reusability, making your infrastructure code more dynamic and adaptable. Let's learn how to leverage variables effectively!

## Creating a Variables File

To begin, we'll create a dedicated file called [`variables.tf`](http://variables.tf) to store all our variables. This file acts as a central repository for defining and managing your variables. Here's an example:

📄 [**variables.tf**](http://variables.tf)

```bash
variable "filename" {
  default = "C:\\Users\\DHANANJAY KULKARNI\\Desktop\\Terraform\\day_63\\demo-var.txt"
}

variable "content" {
  default = "This is coming from a variable which was updated"
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685584196787/62627996-ce9c-445f-9ea6-c4cdafe7d8b4.png align="center")

Here, we define two variables: `filename` and `content`. You can modify their default values to suit your needs. Now, let's see how to access these variables in your main Terraform configuration file.

## Task-01: Creating a Local File with Terraform

Now, let's leverage Terraform to create a local file using the variables we defined earlier. Follow these steps:

1️⃣ Open your preferred text editor, such as **VS Code**, on your **Windows** machine. 2️⃣ Create a new file and name it [`main.tf`](http://main.tf). 3️⃣ Add the following code to the [`main.tf`](http://main.tf) file:

```bash
resource "local_file" "devops" {
  filename = var.filename
  content  = var.content
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685584289255/214edc52-11b5-4179-8e36-73678fcd1515.png align="center")

4️⃣ Save the file.

That's it! You've just created a local file using Terraform. The `local_file` resource block utilizes the `filename` and `content` variables from [`variables.tf`](http://variables.tf) to populate the file.

## Understanding Data Types in Terraform

Terraform supports various data types, including **Map**, **List**, **Set**, and **Object**. Let's explore them further!

### Map

A **Map** is a collection of key-value pairs. It allows you to associate values with specific keys. Here's an example of using a Map variable:

```bash
variable "file_contents" {
  type = map
  default = {
    "statement1" = "this is cool"
    "statement2" = "this is cooler"
  }
}
```

In the above code, we define a `file_contents` variable of type `map`. It contains two key-value pairs representing statements. Maps are incredibly useful for organizing related data.

## Task-02: Demonstrating Usage of List, Set, and Object Data Types

Now, let's demonstrate how to utilize the **List**, **Set**, and **Object** data types in Terraform. Follow these steps:

1️⃣ After saving the [`main.tf`](http://main.tf) file, execute the command `terraform init` to initialize your Terraform configuration.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685584407066/5f83baeb-bc0c-4865-83b0-761e22aefb89.png align="center")

2️⃣ Execute the command `terraform apply` to apply the configuration and create the local file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685584476603/8f9d5bea-29e7-441e-8a4d-9e8b35e93b6c.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685584542297/99ce62e3-25e1-4bb2-9d42-3191a79570c9.png align="center")

3️⃣ Once the operation is successful, execute the command `terraform refresh` to reload the variables and refresh the state by your configuration file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685584603299/b0533b5b-67c6-4ef3-bde5-e9f23c25a8d7.png align="center")

By completing these steps, you'll have successfully implemented Terraform to create a local file and explored various data types.

That's a wrap! You've learned the basics of Terraform variables and

explored different data types. Now, you can confidently leverage variables in your Terraform projects to enhance flexibility and maintainability.

Happy Terraforming! 🌍🚀🔧