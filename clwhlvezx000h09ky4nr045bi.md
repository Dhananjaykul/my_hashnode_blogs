---
title: "How to Configure Kathara Static Routing"
seoTitle: "Configuring Static Routing in Kathara"
seoDescription: "Learn how to configure static routes in Kathara for network connectivity with this step-by-step guide"
datePublished: Wed May 22 2024 09:12:23 GMT+0000 (Coordinated Universal Time)
cuid: clwhlvezx000h09ky4nr045bi
slug: kathara-network-configuration-and-documentation
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1720958754263/cbf53447-cd8f-445e-9747-3a18cf994f72.png
tags: networking, networksimulation, kathara, static-routing

---

## **Introduction**

A router is essential in a network because it routes packets. It enables a computer to communicate with other computers that are not on the same network or subnet. A router accesses a routing table to determine where packets should be sent. The routing table lists destination addresses. Static and dynamic configurations can both be listed on the routing table in order to get packets to their specific destination.

Static Routing is a manually configured fixed pathway that a packet must travel through to reach a destination. Static routings uses less network resources than dynamic routings because they do not constantly calculate and analyze routing updates.

It is best to use static routes when network traffic is predictable, and the network design is simple. It is not recommended to use static routes in a large environment where networks are constantly changing because static routes would not update to any network changes. When using static routes, you would need to configure the other router to have static routes as well depending on what you are trying to do.

One example where static routes can be useful would be specifying a gateway of last resort (a default router to which all unrouteable packets are sent). Another example is to facilitate communication between routers that are not able to communicate on your current network topology.

Dynamic routing is calculated by using dynamic routing algorithms. Dynamic routing protocols automatically create and update the routing table. Most networks use dynamic routes and might have at least one or two static routes configured for special cases.

Below is an example of a topology that we are going to configure static routes for. In the topology, PC1 will not be able to communicate with PC2 and vice versa until a static route is created.

![](https://cdn-images-1.medium.com/max/800/1*c76NZG0EKnKugtRsSoGSgQ.png align="left")

This is a network diagram that is going to be used to help demonstrate IPv4 static route. In this topology, we are using /24 as our subnet mask.

## **Description**

This blog explains how to configure static routes using Kathara, an open-source network emulation tool.A step-by-step guide to setting up a simple network topology and configuring static routes to ensure network connectivity.

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

## Step 1 – Network Topology

We will set up a simple network topology with two PCs and two routers connected through different collision domains (network segments).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1716731394953/4dea2339-799a-4930-9a73-5a63eb79fff1.png align="center")

### IP Addresses and Interfaces

* `pc1`: 192.168.1.2/24 (eth0)
    
* `r1`: 192.168.1.1/24 (eth0), 10.0.0.1/30 (eth1)
    
* `r2`: 10.0.0.2/30 (eth1), 192.168.2.1/24 (eth0)
    
* `pc2`: 192.168.2.2/24 (eth0)
    

## Step 2 – The Lab Setup

### Directory Structure

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1716731523061/f7f21bfb-2660-4de4-88b0-b9c893ba3dcb.png align="center")

Create the following files in your lab directory:

* `lab.conf`
    
* `pc1.startup`
    
* `pc2.startup`
    
* `r1.startup`
    
* `r2.startup`
    

### Configuration Files

`lab.conf`

```plaintext
r1[0]=A
r1[1]=B
r2[0]=C
r2[1]=B
pc1[0]=A
pc2[0]=C
```

`pc1.startup`

```bash
ip address add 192.168.1.2/24 dev eth0
```

`pc2.startup`

```bash
ip address add 192.168.2.2/24 dev eth0
```

`r1.startup`

```bash
ip address add 192.168.1.1/24 dev eth0
ip address add 10.0.0.1/30 dev eth1
```

`r2.startup`

```bash
ip address add 192.168.2.1/24 dev eth0
ip address add 10.0.0.2/30 dev eth1
```

### Starting the Lab

Navigate to the directory containing the `lab.conf` file and start the lab using the Kathara command:

```bash
kathara lstart
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1716731616909/548e7c6e-05ff-42fb-8cbe-6dd86d6d6eb3.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1716731679614/f137a696-ab37-47ed-b7be-d2a92a9afadf.png align="center")

## Step 3 – Testing Connectivity

### Directly Connected Networks

Check connectivity within directly connected networks.

**Ping from**`pc1` to `r1`

```bash
root@pc1:~$ ping 192.168.1.1
```

Expected result:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1716731774574/9e156039-32bf-4681-9e86-919a6822fced.png align="center")

**Ping from**`pc2` to `r2`

```bash
root@pc2:~$ ping 192.168.2.1
```

Expected result:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1716731850223/99160367-8b22-4d27-bcc1-ae9f3381d0a6.png align="center")

### Indirectly Connected Networks

Attempt to ping networks that are not directly connected.

**Ping from**`pc1` to `r2`

```bash
root@pc1:~$ ping 10.0.0.2
```

Expected result:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1716732016237/72db7ec6-5819-4e23-bb4e-7c632ada7700.png align="center")

## Step 4 – Adding Default Routes on PCs

To enable `pc1` and `pc2` to reach networks beyond their directly connected segment, add default routes.

**On**`pc1`

```bash
root@pc1:~$ ip route add default via 192.168.1.1 dev eth0
```

**On**`pc2`

```bash
root@pc2:~$ ip route add default via 192.168.2.1 dev eth0
```

### Verify Default Routes

**Check routing table on**`pc1`

```bash
root@pc1:~$ ip route
```

**Check routing table on**`pc2`

```bash
root@pc2:~$ ip route
```

Expected result:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1716732263074/3aed0845-bbb7-4f70-9765-f08a451a5166.png align="center")

## Step 5 – Configuring Static Routes on Routers

To ensure the routers can forward packets between `pc1` and `pc2`, add static routes.

### On `r1`

```bash
root@r1:~$ ip route add 192.168.2.0/24 via 10.0.0.2 dev eth1
```

### On `r2`

```bash
root@r2:~$ ip route add 192.168.1.0/24 via 10.0.0.1 dev eth1
```

### Verify Static Routes

**Check routing table on**`r1`

```bash
root@r1:~$ ip route
```

Expected result:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1716733678724/5bce65af-4e52-43cd-93fc-1df79696e000.png align="center")

**Check routing table on**`r2`

```bash
root@r2:~$ ip route
```

Expected result:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1716733717113/3e0f6bcf-9ed1-4933-a4d3-0a3039e9a041.png align="center")

## Step 6 – Final Connectivity Test

### Ping from `pc1` to `pc2`

```bash
root@pc1:~$ ping 192.168.2.2
```

Expected result:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1716733771410/f5b2381e-fa37-4fd9-ae44-50d4398dd666.png align="center")

### Ping from `pc2` to `pc1`

```bash
root@pc2:~$ ping 192.168.1.2
```

Expected result:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1716733829546/77a94202-1c44-4e65-8454-b3aff6038c81.png align="center")

## Networking Concepts Explained

### IP Addressing

Each device in a network is assigned a unique IP address. In our lab, we used private IP addresses within the ranges of `192.168.1.0/24` and `192.168.2.0/24`.

### Subnets

A subnet is a segmented piece of a larger network. Subnets help to organize networks efficiently. For example, `192.168.1.0/24` represents a subnet where the first 24 bits are used for network identification and the last 8 bits for host identification.

### Routing

Routing is the process of selecting paths in a network along which to send network traffic. Routers use routing tables to determine the best path to forward packets.

### Static Routing

Static routing involves manually adding routes to a router's routing table. This is useful in small networks or for specific static paths in larger networks. Static routes do not change unless manually altered.

### Default Route

A default route is a route that a router uses when no other known route matches the destination IP address. It typically directs packets to another router that can handle them.

## Conclusion

By following this guide, you should be able to configure static routes in a simple network topology using Kathara. Understanding static routing, default routes, and subnetting is crucial for managing and troubleshooting networks effectively. To stop the lab, use the command:

```bash
kathara lclean
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1716734072546/fbd4f0c3-a5f9-4e1c-9e96-83be7487e675.png align="center")