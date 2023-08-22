---
title: "🚀 Grafana Setup 📈"
seoTitle: "Setting Up Grafana: A Comprehensive Guide for DevOps Enthusiasts"
seoDescription: "Learn how to set up Grafana in your local environment on AWS EC2 with this step-by-step guide. Discover the process of installing Grafana."
datePublished: Thu Jun 15 2023 04:46:39 GMT+0000 (Coordinated Universal Time)
cuid: cliwnsct2000d09i678nm1lp9
slug: grafana-setup
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1686802499163/ebe77e6c-5754-4a57-b973-51f87d50e0ad.gif
tags: devops, grafana, 90daysofdevops, trainwithshubham

---

Hope we are now clear with the basics of Grafana, like why we use it, where we use it, what can we do with this, and so on.

Now, let's get our hands dirty and perform some practical tasks.

### 📈Set up Grafana in your local environment on AWS EC2. Create an EC2 instance in the AWS management console. 🖥️

**🔒 Step 1: Install Dependencies Login to the server and install the following dependencies for Grafana.**

```bash
sudo apt-get install -y apt-transport-https
sudo apt-get install -y software-properties-common wget
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686803486768/589de118-60c8-454b-9008-cc237a3878ef.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686803552552/0f95ba54-f84d-47c1-9b5e-a382ffa5d488.png align="center")

**🔑 Step 2: Download the Key Download the key required to set up Grafana on the server.**

```bash
sudo wget -q -O /usr/share/keyrings/grafana.key https://packages.grafana.com/gpg.key
```

**⚙️ Step 3: Install Grafana Install the stable version of Grafana on the server.**

**Stable release**

```bash
echo "deb [signed-by=/usr/share/keyrings/grafana.key] apt.grafana.com stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
sudo apt-get update
sudo apt-get install grafana
```

**🚀 Step 4: Start and Enable Grafana Start and enable the Grafana server using the following commands.**

```bash
sudo systemctl start grafana-server
sudo systemctl enable grafana-server
```

**🔍 Step 5: Check Grafana Status You can check the current status of Grafana using the following command.**

```bash
sudo systemctl status grafana-server
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686803967664/7de16814-b3d9-46c0-bcd8-20edb7a395c7.png align="center")

**🔒 Step 6: Open Port 3000 Grafana by default runs on port 3000. Therefore, open port 3000 for the EC2 instance.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686804070876/3e38b2a7-e595-4d0b-b7b7-59cc4b801e88.png align="center")

**🌐 Step 7: Access Grafana Navigate through the public URL of the instance using the port number (e.g., http://&lt;public\_ip&gt;:3000) to access the Grafana webpage.**

**🔐 Step 8: Login to Grafana Login to Grafana using the default ID and password, i.e., admin/admin. Then change the password upon the first login for security purposes.**

**🎉 Step 9: Welcome to Grafana Finally, you have successfully entered the Grafana web application! 🎉**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686804245423/b503d52d-9a5f-42f3-acca-604f2860499f.png align="center")

Grafana provides a powerful platform for visualizing and analyzing your data. With its intuitive interface and rich set of features, you can create stunning dashboards, set up alerts, and gain valuable insights from your metrics and logs.

Stay tuned for more exciting DevOps adventures! 🚀👨‍💻