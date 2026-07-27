# Setup Guide

## Overview

This document provides a step-by-step guide for setting up and running the Docker Compose multi-container application on a local development machine.

The application consists of three services:

- Node.js Application
- MongoDB Database
- Mongo Express

Docker Compose orchestrates these services using a single configuration file, simplifying deployment and lifecycle management.

---

# Prerequisites

Before starting, ensure the following software is installed.

| Requirement | Purpose |
|-------------|---------|
| Docker Desktop (or Docker Engine) | Container runtime |
| Docker Compose | Multi-container orchestration |
| Git | Version control |
| Web Browser | Accessing the application |
| Visual Studio Code (Optional) | Editing project files |

---

# Clone the Repository

Clone the project to your local machine.

```bash
git clone https://github.com/Chukwuemeka-Peter-Eze/Docker-compose-multi-container.git
```

Navigate into the project directory.

```bash
cd Docker-compose-multi-container
```

---

# Verify the Project Structure

Confirm that the required project files are present.

```bash
ls
```

Expected files include:

```text
README.md
docker-compose.yml
app/
docs/
images/
architecture/
LICENSE
```

---

# Review the Docker Compose Configuration

Inspect the Docker Compose configuration before deployment.

```bash
cat docker-compose.yml
```

Review the following sections:

- Services
- Images
- Environment variables
- Port mappings
- Networks
- Restart policies

Understanding the configuration before deployment helps identify potential issues and provides insight into how the application stack is organized.

---

# Start the Application Stack

Launch all services in detached mode.

```bash
docker compose up -d
```

Docker Compose automatically:

- Reads the configuration file.
- Pulls required images.
- Creates the application network.
- Creates containers.
- Starts every service.

Verify that the deployment completed successfully before proceeding.

---

# Verify Running Containers

Display all running containers.

```bash
docker ps
```

Confirm that the following containers are running:

- Node.js Application
- MongoDB
- Mongo Express

Review:

- Container names
- Running status
- Published ports

---

# Verify Docker Compose Services

Display the services managed by Docker Compose.

```bash
docker compose ps
```

Verify that each service is healthy and running.

---

# Verify Docker Networks

List available Docker networks.

```bash
docker network ls
```

Identify the network created by Docker Compose.

Inspect the network.

```bash
docker network inspect <network-name>
```

Replace `<network-name>` with the actual network name.

Verify that all application containers are connected to the same network.

---

# Access the Node.js Application

Open your web browser and navigate to the application's published port.

Example:

```text
http://localhost:3000
```

> Replace the port if your Docker Compose configuration uses a different value.

Successful access confirms that:

- The Node.js application is running.
- Port forwarding is functioning correctly.
- The application is reachable from the host machine.

---

# Access Mongo Express

Open Mongo Express in your browser.

Example:

```text
http://localhost:8081
```

> Replace the port if necessary.

Verify that:

- Mongo Express loads successfully.
- MongoDB is accessible.
- The database interface is operational.

---

# View Container Logs

Inspect logs from all services.

```bash
docker compose logs
```

Inspect logs for a specific service.

```bash
docker compose logs node-app
```

```bash
docker compose logs mongodb
```

```bash
docker compose logs mongo-express
```

Follow logs in real time.

```bash
docker compose logs -f
```

Logs help verify successful startup and diagnose runtime issues.

---

# Access Running Containers

Open an interactive shell inside a running container.

Node.js

```bash
docker exec -it node-app sh
```

MongoDB

```bash
docker exec -it mongodb bash
```

Mongo Express

```bash
docker exec -it mongo-express sh
```

Interactive access is useful for troubleshooting and inspecting the running environment.

---

# Stop the Application

Stop all running services.

```bash
docker compose down
```

This command:

- Stops every container.
- Removes the containers.
- Removes the Docker Compose network.

By default, Docker volumes are preserved.

---

# Restart the Application

Restart all services.

```bash
docker compose restart
```

This command restarts every service defined in the Docker Compose configuration.

---

# Clean Up

Remove the application stack.

```bash
docker compose down
```

Remove unused Docker resources.

```bash
docker system prune
```

> **Note:** Review the resources that will be removed before confirming the command.

---

# Summary

By following this guide, you have:

- Cloned the repository.
- Reviewed the Docker Compose configuration.
- Started the multi-container application.
- Verified container status.
- Confirmed Docker networking.
- Accessed the Node.js application.
- Accessed Mongo Express.
- Viewed container logs.
- Managed the application lifecycle.
- Cleaned up Docker resources.

This setup process provides a repeatable workflow for deploying and managing the application using Docker Compose.