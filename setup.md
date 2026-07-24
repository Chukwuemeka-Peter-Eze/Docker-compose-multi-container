# Project Setup Guide

This guide provides a step-by-step walkthrough for deploying the multi-container application on an AWS EC2 instance using Docker Compose.

The deployment includes:

- Node.js Application
- MongoDB Database
- Mongo Express
- Docker Compose
- Docker Networking

By following this guide, the complete application stack can be reproduced consistently in any compatible environment.

---

# Table of Contents

- Solution Architecture
- Prerequisites
- AWS Infrastructure
- Launch EC2 Instance
- Connect to EC2
- Install Docker
- Install Docker Compose
- Verify Installation
- Clone Repository
- Review Project Structure
- Review docker-compose.yml
- Deploy Application Stack
- Verify Containers
- Verify Docker Network
- Verify MongoDB
- Verify Mongo Express
- Verify Node.js Application
- Monitor Services
- Stop the Stack
- Restart the Stack
- Remove the Stack
- Cleanup
- Deployment Checklist
- Summary

---

# Solution Architecture

The deployment follows the workflow below.

```text
Developer
     │
     ▼
GitHub Repository
     │
     ▼
AWS EC2 Instance
     │
     ▼
Ubuntu Linux
     │
     ▼
Docker Engine
     │
     ▼
Docker Compose
     │
 ┌───┼────────────────────┐
 ▼   ▼                    ▼
Node.js              MongoDB         Mongo Express
 │                      │                  │
 └──────────── Docker Network ─────────────┘
                │
                ▼
          Web Browser
```

Docker Compose manages the complete application lifecycle while automatically creating the network required for service-to-service communication.

---

# Prerequisites

Before beginning, ensure the following are available.

- AWS Account
- Amazon EC2 Instance
- Ubuntu Linux Server
- SSH Client
- Docker Engine
- Docker Compose
- Git
- Internet Connection
- Web Browser

---

# AWS Infrastructure

The project was deployed using the following cloud resources.

| Component | Description |
|-----------|-------------|
| Cloud Provider | Amazon Web Services |
| Compute | Amazon EC2 |
| Operating System | Ubuntu Linux |
| Container Runtime | Docker Engine |
| Orchestration | Docker Compose |
| Application | Node.js |
| Database | MongoDB |
| Database UI | Mongo Express |
| Source Control | GitHub |

---

# Step 1 — Launch an EC2 Instance

Provision an Ubuntu EC2 instance.

Recommended configuration:

- Ubuntu Server LTS
- Public IP Enabled
- SSH Enabled
- Internet Gateway Access
- Security Group Configured

Recommended inbound ports.

| Port | Purpose |
|------|----------|
| 22 | SSH |
| 3000 | Node.js Application |
| 8081 | Mongo Express |

---

# Step 2 — Connect to the Server

Connect via SSH.

```bash
ssh -i your-key.pem ubuntu@<EC2-Public-IP>
```

Verify connectivity before proceeding.

---

# Step 3 — Update the Operating System

```bash
sudo apt update

sudo apt upgrade -y
```

Keeping packages updated improves compatibility and security.

---

# Step 4 — Install Docker

Install Docker Engine.

After installation verify:

```bash
docker --version
```

Example:

```text
Docker version xx.x.x
```

---

# Step 5 — Install Docker Compose

Verify Docker Compose.

```bash
docker compose version
```

Expected output:

```text
Docker Compose version v2.x.x
```

---

# Step 6 — Verify Docker Engine

```bash
docker info
```

Verify:

- Docker Engine running
- Storage driver
- Images
- Containers
- Available resources

---

# Step 7 — Clone the Repository

Clone the project.

```bash
git clone https://github.com/Chukwuemeka-Peter-Eze/Docker-compose-multi-container.git
```

Move into the project directory.

```bash
cd Docker-compose-multi-container
```

---

# Step 8 — Verify Repository Structure

Example layout.

```text
Docker-compose-multi-container/

docker-compose.yml

README.md

commands.md

docs/

images/

app/
```

Confirm all required files exist before deployment.

---

# Step 9 — Review the Compose Configuration

Display the configuration.

```bash
cat docker-compose.yml
```

Validate the configuration.

```bash
docker compose config
```

Verify that:

- Services are defined correctly.
- Port mappings are valid.
- Environment variables are configured.
- Networks are created.
- Container names are meaningful.

---

# Step 10 — Deploy the Application Stack

Start every service.

```bash
docker compose up -d
```

Docker Compose automatically:

- Creates the application network
- Downloads required images
- Creates containers
- Configures networking
- Starts every service

Unlike individual Docker commands, one command deploys the complete application.

---

# Step 11 — Verify Running Services

Display the services.

```bash
docker compose ps
```

Or

```bash
docker ps
```

Verify:

- Node.js running
- MongoDB running
- Mongo Express running

Check container names, uptime, and exposed ports.

---

# Step 12 — Verify Docker Network

Display available Docker networks.

```bash
docker network ls
```

Inspect the Compose network.

```bash
docker network inspect <network-name>
```

Verify that:

- Node.js is connected.
- MongoDB is connected.
- Mongo Express is connected.

Docker Compose should automatically configure service discovery between these containers.

---

# Step 13 — Verify MongoDB

Confirm the MongoDB container is healthy.

```bash
docker compose logs mongodb
```

Review startup messages for successful initialization and ensure no critical errors are reported.

---

# Step 14 — Verify Mongo Express

Open a browser and navigate to the Mongo Express interface using your EC2 public IP address and the configured host port.

Verify that:

- The interface loads successfully.
- MongoDB is reachable.
- Databases and collections are visible.

---

# Step 15 — Verify the Node.js Application

Open the application in a browser using your EC2 public IP address and the configured application port.

Successful access confirms:

- The Node.js container is operational.
- Networking is functioning correctly.
- The application can communicate with MongoDB.

---

# Step 16 — Monitor the Application

Display service logs.

```bash
docker compose logs
```

Follow logs continuously.

```bash
docker compose logs -f
```

Monitor the running containers.

```bash
docker stats
```

Inspect the application container.

```bash
docker inspect node-app
```

These commands assist with troubleshooting and operational monitoring.

---

# Step 17 — Stop the Application

Stop every service.

```bash
docker compose stop
```

Containers remain available and can be started again later.

---

# Step 18 — Restart the Stack

Restart all services.

```bash
docker compose restart
```

This applies configuration changes that do not require rebuilding images.

---

# Step 19 — Remove the Stack

Shut down the application.

```bash
docker compose down
```

To remove associated volumes as well.

```bash
docker compose down -v
```

Use the second command only when persistent data is no longer required.

---

# Step 20 — Cleanup

Remove unused Docker resources.

```bash
docker system prune
```

To remove all unused images.

```bash
docker system prune -a
```

Remove unused volumes.

```bash
docker volume prune
```

Regular cleanup helps maintain available disk space.

---

# Deployment Verification Checklist

Confirm the following after deployment.

- EC2 instance is running.
- Docker Engine is installed.
- Docker Compose is installed.
- Repository cloned successfully.
- Compose configuration validated.
- Application stack deployed.
- Node.js container running.
- MongoDB container running.
- Mongo Express container running.
- Docker network created.
- Mongo Express accessible.
- Node.js application accessible.
- Logs available.
- No critical errors reported.

---

# Summary

This guide demonstrates how Docker Compose simplifies the deployment of a multi-container application by treating related services as a single application stack. Using one configuration file and a small set of commands, the Node.js application, MongoDB database, and Mongo Express interface can be deployed, managed, monitored, and removed consistently.

The workflow emphasizes repeatability, automation, service orchestration, and operational simplicity, providing a solid foundation for more advanced container orchestration platforms and cloud-native application deployments.
