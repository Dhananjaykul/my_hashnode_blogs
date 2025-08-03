---
title: "Azure DevOps Series - Day 2: Ditching the Server Rack for Your First VM!"
seoTitle: "Creating Your First Azure VM"
seoDescription: "Learn to launch your first Azure VM, customize NGINX, and prepare for web traffic spikes in this hands-on Azure DevOps tutorial"
datePublished: Sun Aug 03 2025 12:54:40 GMT+0000 (Coordinated Universal Time)
cuid: cmdvoodv0000402l2g903bmhr
slug: azure-devops-series-day-2-ditching-the-server-rack-for-your-first-vm
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1754225592618/2e7cd6a5-0d93-4010-9725-385b45dd0f5c.jpeg
tags: cloud, azure, devops

---

Warning: This is Not Your Typical IT Tutorial

We're about to dive in and move beyond cloud theory. If you're eager to build something rather than just watch videos, you're in the right place.

Welcome back to my Azure DevOps journey! Yesterday, we explored the basics of the cloud. Today, we're stepping into the Azure Portal to launch our very first virtual machine.

Ready? Let's get started.

### First, You Need Access (AKA, a Free Account)

To build on Azure, you'll need an account. The good news is that Azure offers a free trial with credits and numerous free services, making it an ideal playground for us.

**Here's what you need to do:**

* Visit the [Azure Free Account page](https://azure.microsoft.com/en-us/free/).
    
* Click the "Start free" button.
    
* Complete the form. A credit card is required for verification, but you won't be charged unless you choose to upgrade.
    

Once you're set up, you'll enter the Azure Portal, where all the action happens.

# Understanding Azure's Structure

![Diagram that illustrates the four levels of scope in Azure from Microsoft learn](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/media/overview/scope-levels.png align="center")

Before diving in, let's understand how Azure is organized. Think of it as a filing system, from the top-level cabinet to individual documents.

* **Management Groups:** Used by large companies to enforce rules across departments. For now, we can skip this.
    
* **Subscriptions:** This is your account. Every resource is tied to a subscription, which is how Azure manages billing.
    
* **Resource Groups:** Think of this as your project folder. Group related resources together for easy management.
    
* **Resources:** These are the actual components you create, like VMs, databases, and websites.
    

**Tip for Resource Groups:** Always group related items together. For a test app, place the VM, database, and network in a single Resource Group. This makes cleanup simple and cost-effective.

# Deploying a Virtual Machine

Let's launch your first cloud-based machine. It's simpler than you might think.

**Create a Resource Group:**

* In the Azure Portal search bar, type "Resource groups."
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1754223166359/bc27dd2e-c0f8-48ec-a483-c7b40b4dda0e.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1754223197904/d49479ce-6076-442f-b7a5-00afdb3bbbea.png align="center")
    
* Click Create.
    
* Name it Learning-RG and select a nearby region.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1754223280002/1dc885ae-c8dc-4e80-a131-24981c3b005c.png align="center")
    
* Click Review + create -&gt; Create. Done.
    

**Launch a VM:**

* In the search bar, type "Virtual machines."
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1754223344463/9b823582-94b8-4e19-88f8-60fef734df61.png align="center")
    
* Click Create -&gt; Azure virtual machine.
    
* Select your Learning-RG and name your VM MyFirstVM.
    
* Choose a Linux image like Ubuntu Server 22.04 LTS.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1754223533448/806a2150-5b9e-4415-9c04-0f4447803832.png align="center")
    
* For Size, Standard B1s is a great choice for learning.
    
* Select SSH public key under Administrator account. Create a new key pair, name it MySSHKey, and download the private key file (.pem). Keep it secure!
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1754223604961/962957f7-24aa-4b2a-bf73-def5466ae741.png align="center")
    

**Connect to Your Machine:**

* After deployment, find your VM's Public IP address in the Azure Portal and copy it.
    
* Open your terminal (or PowerShell on Windows).
    
* Secure your key file:
    
    ```bash
    chmod 400 /path/to/MySSHKey.pem
    ```
    
* Connect using the default username for Ubuntu, which is azureuser:
    
    ```bash
    ssh -i /path/to/MySSHKey.pem azureuser@<Your_VM_Public_IP>
    ```
    
* Confirm the security prompt. You're now inside a Microsoft data center!
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1754224602594/556456c9-2bb6-4f39-8d48-dbf71db5ea5f.png align="center")
    

**Install a Web Server:**

* Install NGINX, a lightweight web server:
    
    ```bash
    sudo apt update
    sudo apt install nginx -y
    ```
    
* Allow web traffic by adding an inbound port rule in the Azure Portal. Set the Destination port ranges to 80 and name it AllowHTTP.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1754224802993/23e47eff-2ad9-4745-a3b0-c59c9df5588a.png align="center")
    
* Enter your VM’s public IP in a web browser to see the NGINX welcome page!
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1754224886187/9b6ec583-29c6-47ae-8d6a-6f920a2d4deb.png align="center")
    

**Customize Your Content:**

* Modify the default NGINX HTML file:
    
    ```bash
    sudo nano /var/www/html/index.nginx-debian.html
    ```
    
* Replace the content with:
    
    ```html
    <!DOCTYPE html>
    <html>
    <head>
        <title>Azure Learning Series</title>
    </head>
    <body>
        <h1>I AM LEARNING AZURE!</h1>
    </body>
    </html>
    ```
    
* Save and exit (Ctrl + X, Y, Enter).
    
* Refresh your browser to see your custom page!
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1754225089886/4008ed7c-9161-4f13-9370-abff9141961a.png align="center")
    

# Your Challenge: Prepare for Traffic Spikes

What if your site goes viral? A sudden influx of visitors could overwhelm your VM. This is where auto-scaling comes in.

**Research Azure Virtual Machine Scale Sets:**

* What are they, and how do they differ from a single VM?
    
* How do they manage traffic by adding and removing VMs?
    
* Why is a load balancer necessary?
    

We'll explore this in the next post, but understanding it now will enhance your skills.

### Keep Following Me!

You've accomplished more than many do in their careers by building something from scratch in the cloud. Celebrate your achievement!

Did you successfully display your "I AM LEARNING AZURE!" page? Encounter any issues? Share your experience in the comments. Your feedback helps everyone. Also Don’t forget to delete that RG we created.

Stay tuned for our next post, where we'll transform our single VM into a robust, auto-scaling web application. See you then!