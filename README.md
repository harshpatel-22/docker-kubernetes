# Docker & Kubernetes Complete Guide

This guide will take you from the basics of Docker and Kubernetes to advanced concepts. By following this documentation, you will become proficient in both technologies and learn how to manage containerized applications effectively.

---

## Table of Contents

1. [Introduction to Docker](#1-introduction-to-docker)
   - What is Docker?
   - How Docker Works
   - Docker Architecture
   - Installing Docker
2. [Docker Fundamentals](#2-docker-fundamentals)
   - Docker Images and Containers
   - Working with Docker Commands
   - Dockerfile and Docker Images
   - Docker Volumes and Networking
   - Docker Compose
3. [Advanced Docker Concepts](#3-advanced-docker-concepts)
   - Docker Swarm
   - Docker Security Best Practices
   - Docker Registry
4. [Introduction to Kubernetes](#4-introduction-to-kubernetes)
   - What is Kubernetes?
   - Kubernetes Architecture
   - Key Concepts: Pods, Nodes, Clusters, etc.
5. [Kubernetes Fundamentals](#5-kubernetes-fundamentals)
   - Deploying Applications on Kubernetes
   - Kubernetes Services and Networking
   - ConfigMaps and Secrets
   - Managing Volumes in Kubernetes
   - Scaling Applications in Kubernetes
6. [Advanced Kubernetes Concepts](#6-advanced-kubernetes-concepts)
   - StatefulSets vs. Deployments
   - Helm: Kubernetes Package Management
   - Auto-scaling in Kubernetes
   - Monitoring & Logging
   - Security in Kubernetes
7. [Docker + Kubernetes Integration](#7-docker--kubernetes-integration)
   - Building a CI/CD Pipeline with Docker and Kubernetes
   - Deploying Dockerized Applications on Kubernetes
   - Handling Persistent Storage in Kubernetes
8. [Troubleshooting & Best Practices](#8-troubleshooting--best-practices)
   - Docker Troubleshooting
   - Kubernetes Troubleshooting
   - Performance Tuning and Resource Management
9. [Conclusion](#9-conclusion)

---

## 1. Introduction to Docker

### What is Docker?
Docker is a platform that enables developers to create, deploy, and run applications inside **containers**. Containers are lightweight, portable, and isolated environments that contain everything an application needs to run.

### How Docker Works
- **Docker Engine:** The core part of Docker, responsible for running containers.
- **Containers:** Small, lightweight, and portable environments for running applications.
- **Images:** Read-only templates used to create containers.
- **Docker Hub:** A public registry where you can share and pull images.

### Docker Architecture
- **Docker Daemon:** The background service that manages Docker containers.
- **Docker CLI (Command-Line Interface):** Interface through which you interact with Docker.
- **Docker Registry:** A storage and distribution system for Docker images (Docker Hub).

---

## 2. Docker Fundamentals

### Docker Images and Containers
- **Images:** Blueprint for creating containers (e.g., `docker pull ubuntu`).
- **Containers:** Running instances of an image (e.g., `docker run -it ubuntu`).

### Docker Commands
- **docker build:** Build an image from a Dockerfile.
- **docker run:** Create and run a container from an image.
- **docker ps:** List running containers.
- **docker stop:** Stop a running container.
- **docker exec:** Execute commands inside a running container.
- **docker rm:** Remove a container.

### Dockerfile and Docker Images
A **Dockerfile** defines the steps for building a Docker image.
```Dockerfile
FROM node:14
WORKDIR /app
COPY . .
RUN npm install
CMD ["node", "app.js"]
```

### Docker Volumes and Networking
A **Volumes**: Persistent storage that lives outside containers.
- docker volume create my_volume
- docker run -v my_volume:/data my_image

**Networking**: Docker supports different network modes like bridge, host, and overlay networks.

### Docker Compose
Docker Compose is a tool for defining and running multi-container applications. You define services, networks, and volumes in a docker-compose.yml file.
```yaml
version: '3'
services:
  web:
    image: nginx
    ports:
      - "8080:80"
```

**Commands**:
- ```bash
    docker-compose up 
  ```
- ```bash
    docker-compose down 
  ```

## 3. Advanced Docker Concepts
### Docker Swarm
- Docker Swarm is a native clustering and orchestration tool for Docker.
- It allows you to manage a group of Docker engines as a single, virtual Docker engine.
- **Commands**:
    - docker swarm init (initialize a swarm)
    - docker service create (create a service)

### Docker Security Best Practices
- Use official images or trusted sources.
- Limit container privileges.
- Keep images and containers updated.
- Use Docker secrets to manage sensitive data.
### Docker Registry
- Docker images are stored in registries.
- You can either use Docker Hub (public) or create your own private registry.
- Push and pull images using:
    - docker push <image-name>
    - docker pull <image-name>
## 4. Introduction to Kubernetes
### What is Kubernetes?
Kubernetes (K8s) is an open-source system for automating the deployment, scaling, and management of containerized applications.

### Kubernetes Architecture
- **Master Node**: Controls and manages the cluster.
    - **API Server**: Exposes the Kubernetes API.
    - **Controller Manager**: Ensures that the desired state of the cluster is maintained.
    - **Scheduler**: Assigns work to worker nodes.
- **Worker Node**: Runs application containers.
    - **Kubelet**: Manages containers on the node.
    - **Kube Proxy**: Handles network routing.

### Key Concepts
- **Pod**: The smallest deployable unit in Kubernetes, a group of containers.
- **Node**: A physical or virtual machine in the Kubernetes cluster.
- **Cluster**: A set of nodes that run containerized applications.


## 5. Kubernetes Fundamentals
### Deploying Applications on Kubernetes
- Kubernetes uses YAML files to describe application deployments. Example of a deployment YAML:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp
        image: myapp:1.0
```
### Kubernetes Services and Networking
- **Service**: Exposes a set of Pods as a network service.
- **Types of Services**:
    - ClusterIP (default)
    - NodePort
    - LoadBalancer
### ConfigMaps and Secrets
- **ConfigMap**: Stores non-sensitive configuration data in key-value pairs.
- **Secret**: Stores sensitive data (e.g., passwords) in Kubernetes.
### Managing Volumes in Kubernetes
- Kubernetes supports multiple volume types like persistent volumes (PVs) and persistent volume claims (PVCs).
### Scaling Applications in Kubernetes
- Use kubectl scale to scale deployments:
    - kubectl scale deployment myapp --replicas=5


## 6. Advanced Kubernetes Concepts
### StatefulSets vs. Deployments
- **StatefulSet**: Used for stateful applications where pods need persistent storage and unique identifiers.
- **Deployment**: Used for stateless applications.
### Helm: Kubernetes Package Management
- Helm is a package manager for Kubernetes, enabling easy management of Kubernetes applications.
- Helm charts are pre-configured Kubernetes resources packaged together.
### Auto-scaling in Kubernetes
- **Horizontal Pod Autoscaler (HPA)**: Automatically adjusts the number of pods based on resource usage.
- **Vertical Pod Autoscaler (VPA)**: Adjusts CPU and memory resources of containers.
### Monitoring & Logging
- Tools like **Prometheus** (for monitoring) and **Fluentd** (for logging) are commonly integrated into Kubernetes clusters for monitoring and log aggregation.
### Security in Kubernetes
- Best practices include Role-Based Access Control (RBAC), Network Policies, and using Kubernetes secrets for sensitive data.


## 7. Docker + Kubernetes Integration
### CI/CD with Docker & Kubernetes
- **Continuous Integration (CI)**: Automate the process of building and testing Docker images.
- **Continuous Deployment (CD)**: Automatically deploy Dockerized applications to Kubernetes.
- Popular tools: Jenkins, GitLab CI, CircleCI.
### Deploying Dockerized Apps on Kubernetes
- Build your Docker container, push it to a registry, and create a Kubernetes Deployment to manage the containers.
### Persistent Storage in Kubernetes
- Use **Persistent Volumes (PVs)** and **Persistent Volume Claims (PVCs)** to manage data in Kubernetes.


## 8. Troubleshooting & Best Practices
### Docker Troubleshooting
- Use docker logs <container-id> to view logs.
- Check the health of containers with docker inspect <container-id>.
### Kubernetes Troubleshooting
- Use kubectl describe pod <pod-name> to get detailed info about a pod.
- Check logs with kubectl logs <pod-name>.
### Performance Tuning and Resource Management
- Set appropriate resource limits (CPU, memory) for containers and pods.
- Use Kubernetes **Vertical Pod Autoscaler** to adjust resources based on usage.

## 9. Conclusion
Docker and Kubernetes are powerful tools that, when combined, provide a robust platform for building and running containerized applications. Mastering both can significantly improve your ability to manage scalable and resilient applications in production.