---
title: "🐳 Sending Docker Logs to Grafana: Step-by-Step Guide"
seoTitle: "Learn How to Send Docker Logs to Grafana for Real-Time Monitoring"
seoDescription: "Discover the step-by-step process of integrating Docker logs with Grafana to enable real-time monitoring."
datePublished: Tue Jun 20 2023 02:47:38 GMT+0000 (Coordinated Universal Time)
cuid: clj3oqk1b000009lbem6ufn4x
slug: sending-docker-logs-to-grafana-step-by-step-guide
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/iYkqHp5cGQ4/upload/5a96a1a24f9d650fccd6804a47ca836d.jpeg
tags: monitoring, devops, grafana, 90daysofdevops, trainwithshubham

---

## Introduction

Monitoring and analyzing logs is crucial for maintaining the health and performance of your Docker containers. Grafana, a popular open-source monitoring and visualization tool, provides a powerful platform for aggregating and visualizing logs from various sources. In this guide, we will walk through the process of setting up Grafana, Loki, and Promtail to send Docker logs to Grafana for monitoring and visualization. Let's get started! 💻📊

## Step 1: Install Grafana on Debian or Ubuntu

To begin, we need to install Grafana on our system. Follow these steps:

1. Open a terminal and execute the following commands:
    

```bash
sudo apt-get install -y apt-transport-https
sudo apt-get install -y software-properties-common wget
sudo wget -q -O /usr/share/keyrings/grafana.key https://apt.grafana.com/gpg.key
```

Stable release 🚀

```bash
echo "deb [signed-by=/usr/share/keyrings/grafana.key] https://apt.grafana.com stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
```

Beta release 🧪

```bash
echo "deb [signed-by=/usr/share/keyrings/grafana.key] https://apt.grafana.com beta main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
```

1. Update the list of available packages:
    

```bash
sudo apt-get update
```

1. Install the latest OSS release:
    

```bash
sudo apt-get install grafana
```

## Step 2: Install Loki and Promtail using Docker

Now, let's proceed with installing Loki and Promtail using Docker. Execute the following commands:

1. Download Loki Config 📂
    

```bash
wget https://raw.githubusercontent.com/grafana/loki/v2.8.0/cmd/loki/loki-local-config.yaml -O loki-config.yaml
```

1. Run Loki Docker container 🐳
    

```bash
docker run -d --name loki -v $(pwd):/mnt/config -p 3100:3100 grafana/loki:2.8.0 --config.file=/mnt/config/loki-config.yaml
```

1. Download Promtail Config 📂
    

```bash
wget https://raw.githubusercontent.com/grafana/loki/v2.8.0/clients/cmd/promtail/promtail-docker-config.yaml -O promtail-config.yaml
```

1. Run Promtail Docker container 🐳
    

```bash
docker run -d --name promtail -v $(pwd):/mnt/config -v /var/log:/var/log --link loki grafana/promtail:2.8.0 --config.file=/mnt/config/promtail-config.yaml
```

## Step 3: Start Grafana

Start Grafana by entering the following command:

```bash
sudo systemctl start grafana-server
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687571859166/4f46285f-1597-4a50-91dd-6825218b1d75.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687571959564/343cff07-c548-47b0-bad8-4b1dbc2ce474.png align="center")

This will start Grafana at [http://&lt;instance\_ip&gt;:3000](http://localhost:3000) 🚀🌐

## Step 4: Configure Loki as a Data Source in Grafana

Now, let's configure Loki as a data source in Grafana:

1. Go to [http://&lt;instance\_ip&gt;:3000](http://localhost:3000) in your web browser and login with the username "admin" and password "admin" 👤�
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687572131893/5085b653-d2cf-4123-b4ee-ddcb89d77080.png align="center")
    
2. In the navigation drawer on the left, hover over the gear icon (second last one) and click on "Data Sources".
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687572230235/25c66a60-aa00-468b-8c3f-2299d2005b9a.png align="center")
    
3. Click on "Add data source" and search for "Loki". Click on it.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687572274448/d111d363-238a-428d-b848-d8fcc11f8ab1.png align="center")
    
4. Fill in the following details in the form:
    
    * Name: "Loki" (or any name you prefer)
        
    * URL: "[http://localhost:3100](http://localhost:3100)" (the address where Loki server is running)
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687572354859/d98cd9a4-43a3-4072-bb5c-67b7740b362f.png align="center")
        
5. Click on "Save and Test". You should see a success message indicating that the data source is working correctly. ✅
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687576412262/71bb985b-1182-4fdf-96b5-4356c09c41df.png align="center")
    

## Step 5: Creating Visualizations in Grafana

Now, let's create a dashboard with multiple graphs to visualize our Docker logs in Grafana:

### Dashboard Setup

1. In the Grafana interface, click on the "+" icon in the left drawer and select "Dashboard".
    
2. Click on the "Add new panel" button to design a new panel.
    

### Panel 1: Log Counts Visualization 📈

We will make this panel show a line chart denoting the trend of the count of "INFO", "DEBUG", and "ERROR" level logs of our container.

1. Enter the following query in the query field under the panel window:
    
    ```bash
    count_over_time({job="my-container"} |~ "INFO" [5m])
    ```
    
2. Add queries for "DEBUG" and "ERROR" level logs using similar syntax.
    
3. Edit the panel title, customize the font size, and click on "Apply".
    

### Panel 2: 10-Minute-Rate of Total Logs 📉

This panel will display the 10-minute rate of the count of total logs being generated by the container.

1. Create a new panel in the same dashboard.
    
2. Use the following query to fetch the 10-minute rate of the count of total logs:
    
    ```bash
    rate({job="my-container"} [1m]) * 10 * 60
    ```
    
3. Edit the panel title, customize the font size, and apply the changes.
    

## Conclusion

By following this step-by-step guide, you have successfully set up Grafana, Loki, and Promtail to send Docker logs to Grafana for monitoring and visualization. Grafana's powerful visualization capabilities allow you to gain valuable insights into your Docker containers' log data. Explore further and unleash the full potential of Grafana to monitor and optimize your applications. Happy monitoring! 😊🔍

## Enjoy Monitoring with Beautiful Dashboards! 🚀📊