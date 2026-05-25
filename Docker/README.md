# Docker for DevOps Engineers

# Introduction

Docker is a containerization platform used to package applications and dependencies together.

Docker solves:
- environment inconsistency
- dependency conflicts
- deployment failures
- scaling issues

Docker allows applications to run consistently across:
- laptops
- servers
- cloud environments
- Kubernetes clusters

---

# What is Containerization?

Containerization packages:
- application code
- runtime
- libraries
- dependencies

inside a lightweight isolated unit called a container.

---

# Virtual Machines vs Containers

| Virtual Machines | Containers |
|---|---|
| Heavyweight | Lightweight |
| Full OS required | Share host kernel |
| Slow startup | Fast startup |
| More resource usage | Less resource usage |

---

# Docker Architecture

Docker consists of:
- Docker Client
- Docker Daemon
- Docker Images
- Docker Containers
- Docker Registry

---

# Install Docker on Ubuntu

# Update Packages

Purpose:
- updates package repository metadata

Command:

```bash
sudo apt update
```

---

# Install Docker

Purpose:
- installs Docker engine

Command:

```bash
sudo apt install docker.io -y
```

---

# Enable Docker Service

Purpose:
- starts Docker automatically after reboot

Command:

```bash
sudo systemctl enable docker
```

---

# Start Docker Service

Purpose:
- starts Docker daemon immediately

Command:

```bash
sudo systemctl start docker
```

---

# Verify Docker Status

Purpose:
- checks whether Docker service is running

Command:

```bash
sudo systemctl status docker
```

---

# Verify Docker Installation

Purpose:
- displays Docker version

Command:

```bash
docker --version
```

---

# Run First Container

Purpose:
- tests Docker installation using hello-world image

Command:

```bash
sudo docker run hello-world
```

---

# Docker Images

Images are read-only templates used to create containers.

---

# Pull Docker Image

Purpose:
- downloads image from Docker Hub

Command:

```bash
docker pull nginx
```

---

# List Docker Images

Purpose:
- displays downloaded images

Command:

```bash
docker images
```

---

# Remove Docker Image

Purpose:
- deletes unused image

Command:

```bash
docker rmi IMAGE_ID
```

---

# Docker Containers

Containers are running instances of images.

---

# Run Container

Purpose:
- creates and starts container

Command:

```bash
docker run nginx
```

---

# Run Container in Detached Mode

Purpose:
- runs container in background

Command:

```bash
docker run -d nginx
```

---

# Run Container with Port Mapping

Purpose:
- maps host port to container port

Command:

```bash
docker run -d -p 8080:80 nginx
```

Real World Use:
- access nginx on browser using server-ip:8080

---

# Name Container

Purpose:
- assigns readable container name

Command:

```bash
docker run -d --name my-nginx nginx
```

---

# List Running Containers

Purpose:
- shows active containers

Command:

```bash
docker ps
```

---

# List All Containers

Purpose:
- shows running and stopped containers

Command:

```bash
docker ps -a
```

---

# Stop Container

Purpose:
- gracefully stops running container

Command:

```bash
docker stop CONTAINER_ID
```

---

# Start Container

Purpose:
- starts stopped container

Command:

```bash
docker start CONTAINER_ID
```

---

# Restart Container

Purpose:
- restarts running container

Command:

```bash
docker restart CONTAINER_ID
```

---

# Remove Container

Purpose:
- deletes stopped container

Command:

```bash
docker rm CONTAINER_ID
```

---

# Force Remove Container

Purpose:
- deletes running container forcefully

Command:

```bash
docker rm -f CONTAINER_ID
```

---

# Container Logs

Purpose:
- displays application logs

Command:

```bash
docker logs CONTAINER_ID
```

Follow logs:

```bash
docker logs -f CONTAINER_ID
```

---

# Execute Command Inside Container

Purpose:
- opens interactive shell inside container

Command:

```bash
docker exec -it CONTAINER_ID bash
```

---

# Docker Volumes

Volumes provide persistent storage.

---

# Create Volume

Purpose:
- creates persistent storage volume

Command:

```bash
docker volume create my-volume
```

---

# List Volumes

Purpose:
- shows Docker volumes

Command:

```bash
docker volume ls
```

---

# Mount Volume

Purpose:
- persists container data

Command:

```bash
docker run -d -v my-volume:/data nginx
```

---

# Bind Mount

Purpose:
- mounts host directory inside container

Command:

```bash
docker run -d -v /host/path:/container/path nginx
```

---

# Docker Networking

Docker supports:
- bridge
- host
- overlay
- none

---

# List Networks

Purpose:
- shows Docker networks

Command:

```bash
docker network ls
```

---

# Create Network

Purpose:
- creates custom Docker network

Command:

```bash
docker network create my-network
```

---

# Run Container in Network

Purpose:
- attaches container to custom network

Command:

```bash
docker run -d --network my-network nginx
```

---

# Dockerfile

Dockerfile automates image creation.

---

# Create Dockerfile

Purpose:
- defines container build instructions

Command:

```bash
vim Dockerfile
```

Example:

```dockerfile
FROM nginx

COPY . /usr/share/nginx/html
```

---

# Build Docker Image

Purpose:
- creates custom image from Dockerfile

Command:

```bash
docker build -t my-nginx .
```

---

# Run Custom Image

Purpose:
- starts container using custom image

Command:

```bash
docker run -d -p 8080:80 my-nginx
```

---

# Docker Compose

Docker Compose manages multi-container applications.

---

# Install Docker Compose

Purpose:
- installs Docker Compose

Command:

```bash
sudo apt install docker-compose -y
```

---

# Create Compose File

Purpose:
- defines multi-container application

Command:

```bash
vim docker-compose.yml
```

Example:

```yaml
version: '3'

services:
  web:
    image: nginx
    ports:
      - "8080:80"
```

---

# Start Compose Application

Purpose:
- starts all services

Command:

```bash
docker-compose up -d
```

---

# Stop Compose Application

Purpose:
- stops all services

Command:

```bash
docker-compose down
```

---

# Docker Registry

Docker Hub stores images.

---

# Login to Docker Hub

Purpose:
- authenticates Docker client

Command:

```bash
docker login
```

---

# Tag Image

Purpose:
- prepares image for push

Command:

```bash
docker tag my-nginx username/my-nginx:v1
```

---

# Push Image

Purpose:
- uploads image to Docker Hub

Command:

```bash
docker push username/my-nginx:v1
```

---

# Docker System Cleanup

Purpose:
- removes unused resources

Command:

```bash
docker system prune -a
```

---

# Multi-stage Builds

Purpose:
- reduces final image size

Example:

```dockerfile
FROM maven AS build

FROM openjdk
```

---

# Container Resource Limits

Purpose:
- limits CPU and memory usage

Command:

```bash
docker run -d --memory="512m" nginx
```

---

# Docker Security Best Practices

- avoid root user
- scan images
- use minimal base images
- avoid hardcoded secrets
- use read-only filesystem
- limit capabilities

---

# Docker Troubleshooting

# Check Docker Service

Purpose:
- verifies Docker daemon health

Command:

```bash
systemctl status docker
```

---

# Check Container Logs

Purpose:
- investigates application failures

Command:

```bash
docker logs CONTAINER_ID
```

---

# Inspect Container

Purpose:
- displays detailed metadata

Command:

```bash
docker inspect CONTAINER_ID
```

---

# Check Resource Usage

Purpose:
- monitors container CPU and memory

Command:

```bash
docker stats
```

---

# 50 Most Used Docker Commands

| Command | Purpose |
|---|---|
| docker --version | check Docker version |
| docker info | display Docker system information |
| docker pull | download image |
| docker images | list images |
| docker rmi | remove image |
| docker run | start container |
| docker ps | list running containers |
| docker ps -a | list all containers |
| docker stop | stop container |
| docker start | start container |
| docker restart | restart container |
| docker rm | remove container |
| docker logs | view logs |
| docker exec | access container shell |
| docker inspect | inspect container |
| docker stats | monitor usage |
| docker top | view container processes |
| docker cp | copy files |
| docker rename | rename container |
| docker attach | attach terminal |
| docker commit | create image from container |
| docker save | export image |
| docker load | import image |
| docker tag | tag image |
| docker push | upload image |
| docker login | login to registry |
| docker logout | logout registry |
| docker network ls | list networks |
| docker network create | create network |
| docker network inspect | inspect network |
| docker volume ls | list volumes |
| docker volume create | create volume |
| docker build | build image |
| docker history | image layers |
| docker diff | container filesystem changes |
| docker events | Docker events |
| docker stats | container metrics |
| docker system df | disk usage |
| docker system prune | cleanup |
| docker-compose up | start compose |
| docker-compose down | stop compose |
| docker-compose logs | compose logs |
| docker-compose ps | compose containers |
| docker-compose build | build services |
| docker swarm init | initialize swarm |
| docker service ls | list swarm services |
| docker node ls | list swarm nodes |
| docker secret ls | list secrets |
| docker plugin ls | list plugins |

---

# Real World Production Scenarios

# Scenario 1 — Container Keeps Restarting

Symptoms:
- container exits repeatedly

Investigation:

```bash
docker logs CONTAINER_ID
```

Possible Causes:
- application crash
- wrong environment variable
- missing dependency

---

# Scenario 2 — Docker Host Disk Full

Investigation:

```bash
docker system df
```

Cleanup:

```bash
docker system prune -a
```

---

# Scenario 3 — Port Already Allocated

Symptoms:
- container fails to start

Investigation:

```bash
ss -tulpn
```

Fix:
- use different port
- stop conflicting service

---

# Scenario 4 — Container Cannot Access Internet

Investigation:

```bash
docker network ls
docker inspect CONTAINER_ID
```

Possible Causes:
- network misconfiguration
- DNS issue

---

# Scenario 5 — High Memory Usage

Investigation:

```bash
docker stats
```

Fix:
- set memory limits
- optimize application

---

# Production Troubleshooting Workflow

# Step 1 — Check Container Status

```bash
docker ps -a
```

---

# Step 2 — Check Logs

```bash
docker logs CONTAINER_ID
```

---

# Step 3 — Inspect Container

```bash
docker inspect CONTAINER_ID
```

---

# Step 4 — Check Resource Usage

```bash
docker stats
```

---

# Step 5 — Verify Networking

```bash
docker network ls
```

---

# Step 6 — Verify Storage

```bash
docker volume ls
```

---

# Docker in Kubernetes

Kubernetes manages containers created using container runtimes.

Docker concepts are foundational for:
- Kubernetes Pods
- container images
- registries
- networking
- storage

---

# 50 Docker Interview Questions

## Beginner

1. What is Docker?
2. What is containerization?
3. Difference between VM and container?
4. What is Docker image?
5. What is Docker container?
6. What is Docker Hub?
7. What is Dockerfile?
8. Difference between CMD and ENTRYPOINT?
9. What is Docker Compose?
10. What is Docker volume?

---

## Intermediate

11. Difference between image and container?
12. Explain Docker architecture.
13. What is layered filesystem?
14. Difference between bind mount and volume?
15. Explain Docker networking.
16. What is bridge network?
17. Difference between COPY and ADD?
18. What is Docker registry?
19. Explain multi-stage builds.
20. What is container isolation?

---

## Advanced

21. How Docker internally works?
22. What are namespaces and cgroups?
23. Explain overlay filesystem.
24. What is container runtime?
25. Explain Docker daemon.
26. What is rootless Docker?
27. Explain Docker security risks.
28. What is OCI?
29. Difference between Docker and containerd?
30. Explain image caching.

---

## Production Based

31. Container keeps crashing. How to troubleshoot?
32. Docker host disk full troubleshooting.
33. Container memory leak debugging.
34. Docker networking issue investigation.
35. CI/CD Docker build optimization.
36. Securing production containers.
37. Docker image vulnerability handling.
38. Persistent storage issues in containers.
39. Docker daemon not starting.
40. Production image tagging strategy.

---

## Scenario Based

41. Application works locally but not inside container.
42. Docker container cannot connect database.
43. Port binding failure in production.
44. Container exits immediately after startup.
45. High CPU usage in container.
46. Docker build extremely slow.
47. Accidentally deleted container.
48. Docker registry authentication failed.
49. Kubernetes pod image pull failure.
50. Explain your Docker workflow in DevOps projects.

---

# Summary

Docker is one of the most important technologies in DevOps.

Strong Docker skills are essential for:
- Kubernetes
- CI/CD
- microservices
- cloud deployments
- scalable applications
- modern infrastructure

Senior DevOps engineers spend significant time:
- building images
- debugging containers
- optimizing deployments
- securing workloads
- managing container infrastructure
