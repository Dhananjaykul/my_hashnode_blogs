---
title: "📝 Meta-Arguments in Terraform 🚀"
seoTitle: "📝 Meta-Arguments in Terraform 🚀"
seoDescription: "Learn how to leverage the power of meta-arguments, specifically count and for_each, in Terraform to efficiently manage multiple instances of resources."
datePublished: Fri Jun 09 2023 12:13:17 GMT+0000 (Coordinated Universal Time)
cuid: clioj3m3l000h09jk4upi6voy
slug: meta-arguments-in-terraform
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1686312618032/78adbdd1-85c4-462b-b432-e0a8976531c1.png
tags: aws, terraform, infrastructure-as-code, 90daysofdevops

---

In Terraform, when you define a resource block, it typically represents a single resource to be created. However, there are situations where you may need to manage multiple instances of the same resource without duplicating code. This is where meta-arguments such as `count` and `for_each` come into play. These meta-arguments help simplify your code, reduce overhead, and allow for more efficient management of resources. Let's dive into these concepts and explore their practical use in Terraform.

## Count: Managing Multiple Instances

The `count` meta-argument is a powerful feature in Terraform that allows you to create multiple instances of a resource based on a specified count. Each instance will have its own distinct infrastructure object associated with it, enabling individual management of resources. This is particularly useful when you want to create a set number of identical resources.

Let's look at an example using the `aws_instance` resource:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686308826401/5c21c16a-7c83-4666-9b4c-bcc4cae24667.png align="center")

In this example, we use `count = 4` to create four instances of the `aws_instance` resource. Each instance will have a unique name based on the `count.index` value, which starts from 0. The resulting infrastructure will include four separate instances that can be managed individually.

## For\_each: Managing Resources with Different Values

While `count` is useful for creating multiple instances of identical resources, the `for_each` meta-argument comes in handy when you need to manage resources with different values. Instead of specifying a count, `for_each` accepts a map or a set of strings, allowing you to create resources with varying attributes.

Let's consider an example where we need to create different instances of the `aws_instance` resource using different Amazon Machine Image (AMI) IDs:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686312484815/3acbefd5-24ef-4284-b1ee-fbc9d3e6cf58.png align="center")

In this example, we define a local variable `ami_ids` as a set of two different AMI IDs. By using `for_each = local.ami_ids`, Terraform will create two instances of the `aws_instance` resource, one for each AMI ID. Each instance will have a unique name based on the `each.key` value, which corresponds to the key in the `ami_ids` map.

Alternatively, if you have a map with multiple key-value pairs, you can iterate over them using the \`for\_each

\` meta-argument like this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686312641482/1b719c14-53be-4a6e-a870-d583b491ea7c.png align="center")

In this case, Terraform will create two instances of the `aws_instance` resource, using the AMI IDs specified in the map. The resulting infrastructure will consist of resources named according to their respective keys.

## Task-01: Demonstrate the Use of Count and for\_each

To demonstrate the use of `count` and `for_each`, follow these steps:

1. Set up your Terraform configuration with the appropriate provider and version constraints.
    
2. Copy the code examples provided above into your Terraform files.
    
3. Run `terraform init` to initialize the Terraform environment.
    
4. Run `terraform apply` to create the infrastructure based on the configuration.
    
5. Observe how Terraform creates the specified number of instances using `count` or `for_each`.
    
6. To manage these instances individually, you can use the respective keys or indices provided by `count` or `for_each`.
    

By completing this task, you will have a practical understanding of how to leverage `count` and `for_each` meta-arguments in Terraform to manage multiple instances of resources efficiently.

🌟 Happy learning and Terraforming! 🚀🌍✨