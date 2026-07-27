# Docker Compose Command Reference

## Overview

This document contains the Docker and Docker Compose commands used throughout this project, along with a brief explanation of each command.

---

# Verify Docker Installation

Display the installed Docker version.

```bash
docker --version
```

Display the installed Docker Compose version.

```bash
docker compose version
```

Display Docker system information.

```bash
docker info
```

---

# Clone the Repository

Clone the GitHub repository.

```bash
git clone https://github.com/Chukwuemeka-Peter-Eze/Docker-compose-multi-container.git
```

Navigate into the project directory.

```bash
cd Docker-compose-multi-container
```

---

# View Project Files

List files in the current directory.

```bash
ls
```

Display the current working directory.

```bash
pwd
```

---

# Review the Compose File

Display the contents of the Docker Compose configuration.

```bash
cat docker-compose.yml
```

Validate the Docker Compose configuration.

```bash
docker compose config
```

---

# Deploy the Application

Start all services in detached mode.

```bash
docker compose up -d
```

Start all services in the foreground.

```bash
docker compose up
```

Rebuild images before starting.

```bash
docker compose up --build
```

---

# View Running Services

Display Docker Compose services.

```bash
docker compose ps
```

Display running containers.

```bash
docker ps
```

Display all containers, including stopped containers.

```bash
docker ps -a
```

---

# View Logs

Display logs for every service.

```bash
docker compose logs
```

Follow logs in real time.

```bash
docker compose logs -f
```

Display logs for the Node.js application.

```bash
docker compose logs node-app
```

Display logs for MongoDB.

```bash
docker compose logs mongodb
```

Display logs for Mongo Express.

```bash
docker compose logs mongo-express
```

---

# Access Containers

Open a shell inside the Node.js container.

```bash
docker exec -it node-app sh
```

Open a shell inside the MongoDB container.

```bash
docker exec -it mongodb bash
```

Open a shell inside the Mongo Express container.

```bash
docker exec -it mongo-express sh
```

---

# Restart Services

Restart every service.

```bash
docker compose restart
```

Restart a specific service.

```bash
docker compose restart mongodb
```

---

# Stop the Application

Stop all running services.

```bash
docker compose stop
```

Stop and remove the application stack.

```bash
docker compose down
```

Stop and remove containers, networks, and volumes.

```bash
docker compose down -v
```

---

# Docker Networks

List Docker networks.

```bash
docker network ls
```

Inspect a Docker network.

```bash
docker network inspect <network-name>
```

---

# Docker Images

List local images.

```bash
docker images
```

Remove an image.

```bash
docker rmi <image-name>
```

Pull an image manually.

```bash
docker pull mongo
```

```bash
docker pull mongo-express
```

---

# Docker Volumes

List Docker volumes.

```bash
docker volume ls
```

Inspect a Docker volume.

```bash
docker volume inspect <volume-name>
```

---

# Inspect Docker Resources

Inspect a container.

```bash
docker inspect node-app
```

Inspect MongoDB.

```bash
docker inspect mongodb
```

Inspect Mongo Express.

```bash
docker inspect mongo-express
```

---

# Resource Cleanup

Remove unused Docker resources.

```bash
docker system prune
```

Remove unused Docker resources, including unused images.

```bash
docker system prune -a
```

> **Note:** Review the resources that will be removed before confirming the command.

---

# Git Commands

Check repository status.

```bash
git status
```

Stage all changes.

```bash
git add .
```

Commit changes.

```bash
git commit -m "Add Docker Compose project documentation"
```

Push changes to GitHub.

```bash
git push origin main
```

---

# Summary

These commands cover the complete workflow for this project, from verifying the environment and deploying the application to troubleshooting, inspecting Docker resources, and cleaning up the system. Keeping them in one place provides a convenient reference for future projects and reinforces familiarity with the Docker Compose command-line interface.