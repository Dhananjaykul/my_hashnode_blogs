---
title: "Kathara Network Configuration and Documentation"
seoTitle: "Kathara Network Configuration and Documentation"
seoDescription: "Guide to setting up and testing a network with Kathara, including configuration files, network topology, and connectivity testing"
datePublished: Wed May 22 2024 09:12:23 GMT+0000 (Coordinated Universal Time)
cuid: clwhlvezx000h09ky4nr045bi
slug: kathara-network-configuration-and-documentation
tags: networking, networksimulation, kathara

---

This document provides a detailed description of setting up a network using Kathara, including configuration files, network topology, and testing connectivity. The network consists of two routers (`r1`, `r2`) and two PCs (`pc1`, `pc2`).

#### Prerequisites

Before running the lab, ensure Kathara and Docker are installed, along with xterm for terminal emulation.

1. **Install Kathara**
    

```bash
sudo add-apt-repository ppa:katharaframework/kathara
sudo apt update
sudo apt-get install kathara
```

2. **Install Docker**
    

```bash
sudo apt install docker.io
```

3. **Install xterm**
    

```bash
sudo apt-get update
sudo apt-get install xterm
```

#### Network Topology

The network topology consists of the following components:

* **Router** `r1`: Connected to `pc1` via network A and to `r2` via network B.
    
* **Router** `r2`: Connected to `pc2` via network C and to `r1` via network B.
    
* **PC** `pc1`: Connected to `r1` via network A.
    
* **PC** `pc2`: Connected to `r2` via network B.
    

The simplified IP address scheme is as follows:

* **Network A**: `192.168.1.0/24`
    
    * `pc1`: `192.168.1.5`
        
    * `r1`: `192.168.1.1`
        
* **Network B**: `10.0.0.0/30`
    
    * `r1`: `10.0.0.1`
        
    * `r2`: `10.0.0.2`
        
* **Network C**: `192.168.2.0/24`
    
    * `pc2`: `192.168.2.5`
        
    * `r2`: `192.168.2.1`
        

#### Directory Setup

First, create a directory for the lab and navigate into it:

```bash
mkdir -p ~/kathara_labs/my_lab
cd ~/kathara_labs/my_lab
```

#### Configuration Files

Create and edit the following files with the given content:

1. **lab.conf**
    

This file defines the network topology by specifying the connections between network interfaces.

```bash
nano lab.conf
```

```ini
# lab.conf: Defines the network topology

# Router r1 interfaces
# Connect r1 eth0 to network A
r1[0]=A
# Connect r1 eth1 to network B
r1[1]=B

# Router r2 interfaces
# Connect r2 eth0 to network C
r2[0]=C
# Connect r2 eth1 to network B
r2[1]=B

# PC pc1 interface
# Connect pc1 eth0 to network A
pc1[0]=A

# PC pc2 interface
# Connect pc2 eth0 to network B
pc2[0]=B
```

2. **pc1.startup**
    

This script configures the network settings for `pc1`.

```bash
nano pc1.startup
```

```bash
# pc1.startup: Configures network settings for pc1

# Assign IP address to pc1's eth0 interface and bring it up
ip address add 192.168.1.5/24 dev eth0
ip link set eth0 up
```

3. **pc2.startup**
    

This script configures the network settings for `pc2`.

```bash
nano pc2.startup
```

```bash
# pc2.startup: Configures network settings for pc2

# Assign IP address to pc2's eth0 interface and bring it up
ip address add 192.168.2.5/24 dev eth0
ip link set eth0 up
```

4. **r1.startup**
    

This script configures the network settings for `r1`.

```bash
nano r1.startup
```

```bash
# r1.startup: Configures network settings for r1

# Assign IP addresses to r1's interfaces and bring them up
ip address add 192.168.1.1/24 dev eth0
ip address add 10.0.0.1/30 dev eth1
ip link set eth0 up
ip link set eth1 up

# Add a route to network 192.168.2.0/24 via 10.0.0.2
ip route add 192.168.2.0/24 via 10.0.0.2
```

5. **r2.startup**
    

This script configures the network settings for `r2`.

```bash
nano r2.startup
```

```bash
# r2.startup: Configures network settings for r2

# Assign IP addresses to r2's interfaces and bring them up
ip address add 192.168.2.1/24 dev eth0
ip address add 10.0.0.2/30 dev eth1
ip link set eth0 up
ip link set eth1 up

# Add a route to network 192.168.1.0/24 via 10.0.0.1
ip route add 192.168.1.0/24 via 10.0.0.1
```

#### Testing the Configuration

Start the Kathara lab and test the connectivity.

1. **Start the Lab**
    

```bash
sudo kathara lstart
```

2. **Check IP configurations**
    

```bash
sudo kathara exec pc1 -- ip addr show
sudo kathara exec pc2 -- ip addr show
sudo kathara exec r1 -- ip addr show
sudo kathara exec r2 -- ip addr show
```

3. **Test connectivity**
    

```bash
sudo kathara exec pc1 -- ping 192.168.1.1  # From pc1 to r1
sudo kathara exec pc1 -- ping 192.168.2.5  # From pc1 to pc2
sudo kathara exec pc2 -- ping 192.168.2.1  # From pc2 to r2
```

This setup ensures that `pc1` and `pc2` can communicate through the network established by the two routers, demonstrating the basic functionality of a routed network using Kathara.