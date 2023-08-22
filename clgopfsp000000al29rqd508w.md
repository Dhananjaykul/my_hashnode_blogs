---
title: "Docker Cheat Sheet"
seoTitle: "Cheat Sheet for Dockers"
seoDescription: "This cheat sheet covers all the basic and advanced commands for Docker, Docker Compose, and Docker Swarm that are essential for DevOps engineers."
datePublished: Thu Apr 20 2023 05:51:19 GMT+0000 (Coordinated Universal Time)
cuid: clgopfsp000000al29rqd508w
slug: docker-cheat-sheet
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1681970005004/1ff2d10f-e6ed-4099-9258-86f21f288f5d.png
tags: docker, devops, docker-images, 90daysofdevops, trainwithshubham

---

This cheat sheet covers all the basic and advanced commands for Docker, Docker Compose, and Docker Swarm that are essential for DevOps engineers.

### **Docker Basics**

#### Images

Images are the blueprints for Docker containers.

##### **Build**

Build an image from a Dockerfile:

```bash
docker build -t <image-name> .
```

##### **List**

List all the images present on the Docker host:

```bash
docker image ls
```

##### **Remove**

Remove an image:

```bash
docker image rm <image-id>
```

##### **Prune**

Remove all unused images:

```bash
docker image prune
```

##### **Save**

Save an image to a tar file:

```bash
docker image save -o <filename>.tar <image-name>
```

##### **Load**

Load an image from a tar file:

```bash
docker image load -i <filename>.tar
```

##### **Tag**

Tag an image:

```bash
docker image tag <image-id> <new-image-name>
```

#### Containers

Containers are instances of Docker images.

##### **Run**

Run a container from an image:

```bash
docker run <image-name>
```

##### **Run with Port Forwarding**

Run a container from an image with port forwarding:

```bash
docker run -p <host-port>:<container-port> <image-name>
```

##### **Run with Volume Mounting**

Run a container from an image with volume mounting:

```bash
docker run -v <host-path>:<container-path> <image-name>
```

##### **List**

List all the containers present on the Docker host:

```bash
docker ps -a
```

##### **Start**

Start a stopped container:

```bash
docker start <container-id>
```

##### **Stop**

Stop a running container:

```bash
docker stop <container-id>
```

##### **Remove**

Remove a container:

```bash
docker rm <container-id>
```

##### **Prune**

Remove all stopped containers:

```bash
docker container prune
```

##### **Exec**

Run a command inside a running container:

```bash
docker exec -it <container-id> <command>
```

##### **Logs**

View the logs of a container:

```bash
docker logs <container-id>
```

##### **Stats**

View the real-time resource usage of a container:

```bash
docker stats <container-id>
```

#### Volumes

Volumes are persistent data storage mechanisms that allow data to persist across container restarts and can be shared between multiple containers.

##### **Create**

Create a new volume:

```bash
docker volume create <volume-name>
```

##### **List**

List all the volumes present on the Docker host:

```bash
docker volume ls
```

##### **Inspect**

Inspect a specific volume to view the details, including the mountpoint and driver:

```bash
docker volume inspect <volume-name>
```

##### **Mount**

Mount a volume to a specific container:

```bash
docker run -v <volume-name>:<container-mountpoint> <image-name>
```

##### **Remove**

Remove a volume:

```bash
docker volume rm <volume-name>
```

##### **Prune**

Delete all the unused volumes present on the Docker host:

```bash
docker volume prune
```

##### **Backup**

Back up a volume:

```bash
docker run --rm -v <volume-name>:/volume -v $(pwd):/backup <image-name> tar -czvf /backup/<volume-name>-backup.tar.gz /volume
```

##### **Restore**

Restore a volume from a backup:

```bash
docker run --rm -v <volume-name>:/volume -v $(pwd):/backup busybox tar -xzvf /backup/<volume-name>-backup.tar.gz
```

### **Docker Compose**

Docker Compose is a tool for defining and running multi-container Docker applications.

#### Basic Usage

##### **Define**

Define a multi-container Docker application in a \`docker-compose.yml

file:

```bash
version: '3'
services:
  web:
    build: .
    ports:
      - "80:80"
  db:
    image: postgres
    volumes:
      - db-data:/var/lib/postgresql/data
volumes:
  db-data:
```

##### **Start**

Start a multi-container Docker application defined in a `docker-compose.yml` file:

```bash
docker-compose up
```

##### **Stop**

Stop a running multi-container Docker application:

```bash
docker-compose down
```

##### **List**

List all running multi-container Docker applications:

```bash
docker-compose ps
```

#### Advanced Usage

##### **Build**

Build the images for a multi-container Docker application defined in a `docker-compose.yml` file:

```bash
docker-compose build
```

##### **Scale**

Scale a specific service in a multi-container Docker application:

```bash
docker-compose up --scale <service-name>=<number-of-instances>
```

##### **Exec**

Run a command inside a specific container in a multi-container Docker application:

```bash
docker-compose exec <service-name> <command>
```

##### **Logs**

View the logs of a specific service in a multi-container Docker application:

```bash
docker-compose logs <service-name>
```

##### **Restart**

Restart a specific service in a multi-container Docker application:

```bash
docker-compose restart <service-name>
```

##### **Stop and Remove**

Stop and remove all containers, networks, and volumes associated with a multi-container Docker application:

```bash
docker-compose down --volumes --remove-orphans
```

### **Docker Swarm**

Docker Swarm is a native Docker tool for container orchestration.

#### Basic Usage

##### **Initialize**

Initialize a Docker Swarm:

```bash
docker swarm init
```

##### **Join**

Join a Docker Swarm as a worker:

```bash
docker swarm join --token <token> <manager-ip-address>
```

##### **Deploy**

Deploy a Docker stack:

```bash
docker stack deploy -c <compose-file> <stack-name>
```

##### **List**

List all the services running in a Docker Swarm:

```bash
docker service ls
```

##### **Scale**

Scale a specific service in a Docker Swarm:

```bash
docker service scale <service-name>=<number-of-instances>
```

##### **Remove**

Remove a Docker stack:

```bash
docker stack rm <stack-name>
```

##### **Leave**

Leave a Docker Swarm:

```bash
docker swarm leave --force
```

#### Advanced Usage

##### **Update**

Update a specific service in a Docker Swarm:

```bash
docker service update <service-name> --image <new-image-name>
```

##### **Logs**

View the logs of a specific service in a Docker Swarm:

```bash
docker service logs <service-name>
```

##### **Drain**

Drain a node in a Docker Swarm:

```bash
docker node update --availability drain <node-id>
```

##### **Promote**

Promote a worker node to a manager node in a Docker Swarm:

```bash
docker node promote <node-id>
```

##### **Demote**

Demote a manager node to a worker node in a Docker Swarm:

```bash
docker node demote <node-id>
```

##### **Inspect**

Inspect a specific node in a Docker Swarm:

```bash
docker node inspect <node-id>
```

##### **Visualize**

Visualize a Docker Swarm using the Docker Swarm Visualizer:

```bash
docker run -it -d -p 8080:8080 -v /var/run/docker.sock:/var/run/docker.sock dockersamples/visualizer
```