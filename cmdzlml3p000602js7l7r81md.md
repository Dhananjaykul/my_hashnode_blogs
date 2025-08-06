---
title: "Azure Networking Basics: Hands-On Learning for Beginners Part 1"
seoTitle: "Azure Networking Basics: Beginner's Guide"
seoDescription: "Learn Azure networking basics with a guide for beginners. Build secure networks using Resource Groups, VNets, NSGs, and ASGs"
datePublished: Wed Aug 06 2025 06:40:22 GMT+0000 (Coordinated Universal Time)
cuid: cmdzlml3p000602js7l7r81md
slug: azure-networking-basics-hands-on-learning-for-beginners-part-1
tags: cloud, azure, networking, cybersecurity-1

---

If you're new to the cloud, networking can seem like a complex maze of abstract rules and virtual devices. But what if you could build a secure, scalable network with your own hands, understanding every component along the way?

That's exactly what we're going to do.

This guide is a comprehensive, hands-on lab that will take you from an empty Azure subscription to a functional, multi-tier network. We'll explore the theory behind each step. By the end, you'll have a practical understanding of Resource Groups, Virtual Networks (VNets), Network Security Groups (NSGs), and Application Security Groups (ASGs).

**Our Goal:** To build a simple but secure two-tier application network, with a web tier accessible from the internet and an application tier that can only talk to the web tier.

Ready? Let's begin.

### Section 1: Setting the Foundation (Resource Group & VNet)

Before we can have virtual machines, we need a place to put them and a network for them to live in.

#### Step 1.1: Create a Resource Group

**The Theory:** A Resource Group is the most fundamental building block in Azure. It's a logical container that holds related resources for an application. Think of it as a folder for your project. Grouping resources makes them easier to manage, monitor, and clean up.

**The Lab:**

* Sign in to the Azure Portal.
    
* Click Create a resource.
    
* Search for Resource group and click Create.
    
* Give it a name. Let's use a consistent naming convention: Network-Lab-RG.
    
* Select a Region (e.g., East US).
    
* Click Review + create, and then Create.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1754458620105/fff96382-e5fa-4682-bb7b-52836f493388.png align="center")
    

#### Step 1.2: Create a Virtual Network (VNet)

**The Theory:** A Virtual Network (VNet) is your private, isolated network in the Azure cloud. It's where your virtual machines and other resources will live and communicate. When you define a VNet, you assign it a private IP address space using CIDR (Classless Inter-Domain Routing) notation.

**The Lab:**

* In the portal, search for Virtual Network and click Create.
    
* **Basics Tab:**
    
    * Select the Network-Lab-RG Resource group we just created.
        
    * Name your VNet: Main-VNet.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1754458730440/1159c448-153e-4a1a-a241-860d5c4fa654.png align="center")
        
* **IP Addresses Tab:**
    
    * The default address space might be something like 10.0.0.0/16. Let's define our own: 10.10.0.0/16. This gives us over 65,000 private IP addresses to use within this network.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1754458769952/5268e973-43a2-41a9-a5d8-1ae66a87ae7a.png align="center")
        

#### Step 1.3: Create our First Subnet

**The Theory:** A Subnet is a smaller, logical division of your VNet. Subnetting allows you to segment your network, for example, into a 'web tier', an 'application tier', and a 'data tier'. This is crucial for organizing resources and applying specific security rules.

**The Lab:**

* While still in the VNet creation menu, you'll see a section to add a subnet.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1754458866642/05ed2f69-c6c4-4048-849e-d2458f8a07e1.png align="center")
    
* Click + Add subnet.
    
* Subnet name: Web-Subnet.
    
* Subnet address range: 10.0.1.0/24. This carves out 256 addresses from our main VNet for this specific subnet.
    
* Click Add.
    
* Finally, click Review + create, and Create to deploy your VNet and its first subnet.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1754458989479/e31b6e40-b344-4e94-9bf8-f448f906c797.png align="center")
    

### Section 2: Launching a Web Server & Exposing it to the World

Now that we have our network, let's place a VM in it and make it a web server.

#### Step 2.1: Launch the Web VM

* Create a new Virtual machine.
    
* **Basics Tab:**
    
    * Resource group: Network-Lab-RG.
        
    * Virtual machine name: webvm01.
        
    * Image: Ubuntu Server (any recent LTS version).
        
    * Set up your administrator account with a password or SSH key.
        
* **Networking Tab:**
    
    * Virtual network: Main-VNet.
        
    * Subnet: Web-Subnet (10.10.1.0/24).
        
    * Public IP: Let Azure create a new one.
        
    * NIC network security group: Select Basic.
        
    * Click Review + create, and Create.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1754459682642/f643d83d-a513-416a-b36a-5f2eef759180.png align="center")
        

#### Step 2.2: Install Nginx

Once your VM is deployed, find its Public IP address on the Overview page and SSH into it. Then, install the Nginx web server.

```bash
sudo apt-get update
sudo apt-get install nginx -y
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1754459829329/8696afca-db52-49ad-a068-25844cbeda2d.png align="center")

#### Step 2.3: Understanding Network Security Groups (NSGs)

**The Theory:** A Network Security Group (NSG) is a virtual firewall for your VMs. It contains a list of security rules that allow or deny network traffic to resources connected to your VNet. When we created webvm01, Azure automatically created an NSG called webvm01-nsg and attached it directly to the VM's Network Interface Card (NIC).

#### Step 2.4: Test the Connection

* From your browser: Try to navigate to `http://<your_public_ip>`. The request will time out.
    
* **Why?** By default, NSGs have a rule called DenyAllInBound which blocks all traffic from the outside world. It's a security-first approach. We need to explicitly allow the traffic we want.
    

#### Step 2.5: Create an Inbound Rule to Allow HTTP

* Navigate to the webvm01 resource in the Azure Portal.
    
* Go to the Networking blade.
    
* Click Add inbound port rule.
    
* **Configure the rule:**
    
    * Source: Any. We want to allow traffic from anywhere on the internet.
        
    * Source port ranges: \*. The source port is random, so we allow any.
        
    * Destination: Any.
        
    * Service: HTTP. This is a shortcut that automatically fills in the important parts:
        
        * Destination port ranges: 80
            
        * Protocol: TCP
            
        * Action: Allow.
            
    * Priority: 300. A custom number. Lower numbers are processed first.
        
    * Name: Allow-HTTP.
        
* Click Add.
    

Now, refresh your browser. The "Welcome to nginx!" page appears!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1754460024785/09f218e4-1a6f-41dc-8a9c-2d9573e00eb0.png align="center")

### Section 3: The Power of NSG Priority

**The Theory:** NSG rules don't just exist; they have a hierarchy. Rules are processed based on their Priority number, from lowest to highest. The first rule that matches the traffic pattern is applied, and all other rules are ignored.

Let's prove it by adding a Deny rule with a higher priority (a lower number).

* In the webvm01 Networking settings, add another inbound rule.
    
* **Configure it:**
    
    * Source: Any
        
    * Destination port ranges: 70-100 (this range includes our web server port, 80).
        
    * Action: Deny.
        
    * Priority: 290. This is a lower number than our allow rule's 300.
        
    * Name: Deny-Web-Ports.
        
* Click Add.
    

Wait a minute for the rule to apply, then refresh your browser. The connection is blocked again! Even though a rule exists to allow port 80, the rule to deny the 70-100 range is processed first because 290 &lt; 300.

> **Key Takeaway:** Priority is the most critical setting in an NSG rule. A misconfigured priority can easily override your intentions.

**Cleanup:** Delete the Deny-Web-Ports rule to restore access.

### Section 4: Internal Communication & The "Hidden" Rules

What about traffic inside our VNet?

#### Step 4.1: Create the 'App' Tier

* Go to Main-VNet &gt; Subnets &gt; + Subnet.
    
* Name: App-Subnet.
    
* Address range: 10.0.2.0/24.
    
* Click Save.
    

#### Step 4.2: Launch the App VM

* Create a new VM named appvm01.
    
* Place it in the Network-Lab-RG resource group.
    
* On the Networking tab, select Main-VNet and the new App-Subnet.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1754460730495/54053dcd-43f5-48fc-a25f-aeeda54df17e.png align="center")
    

#### Step 4.3: The Critical Experiment

* Go back to webvm01 &gt; Networking and delete the Allow-HTTP rule. Now there are no custom inbound rules on webvm01.
    
* SSH into your new appvm01.
    
* From appvm01's command line, try to curl the private IP of webvm01 (you can find this on webvm01's overview page, it will be something like 10.0.1.4).
    

```bash
# This command is run from inside appvm01
curl http://<private_ip_of_webvm01>
```

It works! You'll get the Nginx HTML back. But how? We have no rule allowing port 80!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1754461000065/8ce08cd1-412b-423f-96d6-17c5fa944961.png align="center")

#### Step 4.4: The "Aha!" Moment - Default Rules

**The Theory:** Every NSG comes with three default inbound rules that you cannot remove. One of them is the key:

* **AllowVnetInBound:** Priority 65000. This rule allows any and all traffic originating from within the same VNet. This is why appvm01 can talk to webvm01 without any custom rules. It's also why our curl from the public IP of appvm01 to webvm01 will fail because that is not "VNet Inbound" traffic.
    

### Section 5: A Better Way - Centralized Subnet-Level NSGs

Attaching an NSG to every VM is inefficient. A much better practice is to apply NSGs to subnets, enforcing the same rules for all VMs within that subnet.

* **Create a Central NSG:** Search for Network security groups and create a new one called Global-App-NSG in the Network-Lab-RG.
    
* **Disassociate NIC NSGs:** Go to webvm01 &gt; Networking. Click on its Network Interface resource. Go to Network security group and click Disassociate. Repeat for appvm01. You can now safely delete the old nsgs to keep things tidy.
    
* **Associate NSG to Subnets:** Go to your new Global-App-NSG. Under Settings, go to Subnets &gt; Associate. Select Main-VNet and associate the NSG with both Web-Subnet and App-Subnet.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1754461930544/532b5f90-fcf8-4192-8049-6bdffecc0945.png align="center")
    
* **Create Centralized Rules:** Now add rules to Global-App-NSG:
    
    * **Rule 1:** Allow HTTP to the web tier. Name it Allow-HTTP-Inbound. Set Destination Port to 80.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1754462182708/74e8cfdd-dd1e-42e2-81a5-c56847b79d4b.png align="center")
        
    * **Rule 2:** Allow SSH from anywhere. Name it Allow-SSH-Inbound. Set Destination Port to 22.
        

All VMs in both subnets now inherit these rules from a single, centrally managed NSG.

### Section 6: The Ultimate Scalability - Application Security Groups (ASGs)

Our setup is better, but our HTTP rule allows port 80 traffic to every VM in both subnets. We need to be more specific. We could hardcode webvm01's IP address in the rule, but what if we have 50 web servers? We will need to keep adding IP addresses of these VM.

**The Theory:** An Application Security Group (ASG) solves this. It's not a security device itself; it's a tag. You group VMs by tagging them with an ASG (e.g., "webservers"), and then you can use that tag as a source or destination in your NSG rules.

**The Lab:**

* **Create an ASG:** Search for Application security groups and create one named web-servers-asg inside Network-Lab-RG.
    
* **Launch a Second Web Server:** Create webvm02 in the Web-Subnet and install Nginx on it.
    
* **Tag the VMs:**
    
    * Go to webvm01 &gt; Networking &gt; Application security groups tab. Click Configure... and add it to the web-servers-asg.
        
    * Repeat for webvm02.
        
* **The Final Rule Update:**
    
    * Go to our Global-App-NSG and edit the Allow-HTTP-Inbound rule.
        
    * Change the Destination type from Any to Application security group.
        
    * For the Destination application security group, select web-servers-asg.
        
    * Save the rule.
        

**The Payoff:** Now, only VMs tagged with web-servers-asg will receive traffic on port 80. You can add or remove web servers, and you never have to touch the NSG rule again. You simply add/remove the ASG tag on the VM. This is secure, scalable, and easy to manage.

### Conclusion

You did it! You've built a network from scratch and explored the most important concepts for securing it.

Let's recap the journey:

* We started with a Resource Group for organization.
    
* We created a VNet for isolation and partitioned it with Subnets.
    
* We learned that NSGs are our firewalls and that Priority dictates rule processing.
    
* We discovered the default rules, like AllowVnetInBound, that govern internal traffic.
    
* We evolved from messy NIC-level NSGs to clean Subnet-level NSGs.
    
* Finally, we achieved true scalability by using ASGs to apply rules to logical groups of servers.
    

You now have the foundational knowledge to design and manage secure networks in Azure. Happy building!