---
title: "✨ Supercharge Your Infrastructure Automation with Terraform and Docker🐳"
seoTitle: "✨Supercharge Your Infrastructure Automation with Terraform and Docker✔"
seoDescription: "Learn how to configure Terraform, create resource blocks, and leverage Docker to supercharge your automation workflows. 🛠️💡"
datePublished: Wed May 31 2023 04:25:47 GMT+0000 (Coordinated Universal Time)
cuid: clib7fqnx000209mm2jyr750s
slug: supercharge-your-infrastructure-automation-with-terraform-and-docker
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1685506846550/3cdf8ef8-2a44-4316-bffa-bcf31841e8f2.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1685507114353/1d605d03-c50b-42cc-834e-a198424e96f6.png
tags: docker, devops, terraform, 90daysofdevops, trainwithshubham

---

Are you ready to learn about Terraform and Docker? These powerful tools can streamline your automation processes and make managing your resources a breeze. In today's blog, we'll walk you through the steps of setting up Terraform with Docker. Let's dive in!

## Task 1: Creating a Terraform script with Blocks and Resources

To get started, we need to configure Terraform to use the Docker provider. This can be done by adding the following code block to your [main.tf](http://main.tf) file:

```bash
terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = "~> 2.21.0"
    }
  }
}
```

Note: Here, "kreuzwerker/docker" refers to the shorthand for [registry.terraform.io/kreuzwerker/docker](http://registry.terraform.io/kreuzwerker/docker).

## Provider Block

The next step is to configure the provider block for Docker. This block tells Terraform to use the Docker provider for managing resources. Add the following code to your [main.tf](http://main.tf) file:

```bash
provider "docker" {}
```

## Resource Blocks

Now it's time to define the components of your infrastructure using resource blocks. These blocks allow you to specify the resources you want to create or manage. Let's start by creating a resource block for an nginx Docker image:

```bash
resource "docker_image" "nginx" {
  name         = "nginx:latest"
  keep_locally = false
}
```

In this example, we're creating an nginx Docker image with the latest tag. The `keep_locally` attribute is set to false, which means that the image will not be kept on the local machine after use.

Next, let's create a resource block for running a Docker container with the nginx image:

```bash
resource "docker_container" "nginx" {
  image = docker_image.nginx.latest
  name  = "tutorial"
  ports {
    internal = 80
    external = 80
  }
}
```

Here, we're creating a Docker container named "tutorial" using the nginx image we defined earlier. The container will expose port 80 internally and externally.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685523696418/e113d241-a17b-4e1f-946a-1de72d42398d.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685523953717/c3ec8aeb-484a-4373-8eee-bb4f808fbd36.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685524028654/601347ae-d0a1-40b3-ac58-f854301c0881.png align="center")

![NGINX running in Docker via Terraform](https://content.hashicorp.com/api/assets?product=tutorials&version=main&asset=public%2Fimg%2Fterraform%2Fgetting-started%2Fterraform-docker-nginx.png align="left")

## Task 2: Setting up Docker

Before running your Terraform script, make sure Docker is installed on your machine. If it's not already installed, you can install it by following these steps:

Step 1: Open the terminal or command prompt. Step 2: Run the command `sudo apt-get install` [`docker.io`](http://docker.io) to install Docker. Step 3: After the installation is complete, run the command `sudo docker ps` to check the status of Docker. Step 4: Finally, run the command `sudo chown $USER /var/run/docker.sock` to set the necessary permissions.

These steps will install Docker, check its status, and ensure that the necessary permissions are set.

That's it! You're now ready to use Terraform with Docker. By leveraging the power of these tools, you can automate the provisioning and management of your resources. Stay tuned for more exciting tutorials!

Happy coding! 😄🚀