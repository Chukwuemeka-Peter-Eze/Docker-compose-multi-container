# Troubleshooting Guide

## Introduction

Troubleshooting is an essential skill when working with containerized applications. Although Docker Compose simplifies the deployment of multi-container applications, configuration errors, networking issues, and runtime failures can still occur.

This guide documents common issues encountered during Docker Compose deployments, their possible causes, and recommended solutions.

---

# Verify Docker Installation

Before troubleshooting the application itself, verify that Docker is installed and running.

Check the Docker version.

```bash
docker --version
```

Check the Docker Compose version.

```bash
docker compose version
```

Verify that the Docker daemon is running.

```bash
docker info
```

If Docker is not running, start Docker Desktop or the Docker service before continuing.

---

# Containers Fail to Start

## Symptoms

- Containers exit immediately after starting.
- Services remain in the **Exited** state.
- `docker compose up` reports errors.

Verify container status.

```bash
docker ps -a
```

---

## Possible Causes

- Invalid Docker Compose syntax.
- Missing environment variables.
- Incorrect image name.
- Invalid port mapping.
- Application startup failure.

---

## Resolution

Validate the Compose configuration.

```bash
docker compose config
```

Review service logs.

```bash
docker compose logs
```

Restart the application.

```bash
docker compose down

docker compose up -d
```

---

# Docker Compose Configuration Errors

## Symptoms

Deployment fails before any containers are created.

Example:

```text
ERROR: Invalid Compose file
```

---

## Possible Causes

- YAML indentation errors.
- Incorrect property names.
- Unsupported Compose options.

---

## Resolution

Validate the Compose file.

```bash
docker compose config
```

Correct any reported syntax errors before redeploying.

---

# Image Download Failures

## Symptoms

Docker cannot download an image.

Example:

```text
pull access denied
```

---

## Possible Causes

- Incorrect image name.
- Invalid image tag.
- Internet connectivity issues.
- Docker Hub availability.

---

## Resolution

Verify the image names.

Pull the image manually.

```bash
docker pull mongo

docker pull mongo-express

docker pull node
```

If the images download successfully, redeploy the application.

---

# Port Already in Use

## Symptoms

Deployment fails with a port binding error.

Example:

```text
Bind for 0.0.0.0:3000 failed
```

---

## Possible Causes

- Another application is already using the required port.
- Another Docker container is publishing the same port.

---

## Resolution

List running containers.

```bash
docker ps
```

Stop the conflicting container.

```bash
docker stop <container-name>
```

Alternatively, modify the port mapping in the `docker-compose.yml` file and redeploy.

---

# Service Communication Problems

## Symptoms

The Node.js application cannot connect to MongoDB.

---

## Possible Causes

- Incorrect service name.
- Containers attached to different networks.
- MongoDB not fully initialized.
- Incorrect application configuration.

---

## Resolution

Display Compose services.

```bash
docker compose ps
```

Inspect the network.

```bash
docker network inspect <network-name>
```

Verify that:

- Every service is running.
- All services belong to the same network.
- The application references the MongoDB service by its Compose service name.

---

# MongoDB Connection Errors

## Symptoms

Application reports database connection failures.

---

## Possible Causes

- MongoDB container still starting.
- Invalid credentials.
- Incorrect connection string.
- Incorrect environment variables.

---

## Resolution

Review MongoDB logs.

```bash
docker compose logs mongodb
```

Wait until MongoDB has fully initialized before restarting the application if necessary.

---

# Mongo Express Cannot Connect

## Symptoms

Mongo Express loads but cannot display the database.

---

## Possible Causes

- MongoDB service unavailable.
- Incorrect credentials.
- Incorrect service name.

---

## Resolution

Verify the MongoDB container.

```bash
docker compose ps
```

Review Mongo Express logs.

```bash
docker compose logs mongo-express
```

Confirm that the environment variables match the MongoDB configuration.

---

# Application Not Accessible from Browser

## Symptoms

The browser cannot reach the Node.js application.

---

## Possible Causes

- Incorrect port mapping.
- Container not running.
- Application startup failure.

---

## Resolution

Verify running containers.

```bash
docker ps
```

Confirm that the application port is published.

Review logs.

```bash
docker compose logs node-app
```

---

# Docker Network Issues

## Symptoms

Containers cannot communicate.

---

## Possible Causes

- Containers connected to different networks.
- Incorrect service names.
- Network creation failure.

---

## Resolution

List Docker networks.

```bash
docker network ls
```

Inspect the project network.

```bash
docker network inspect <network-name>
```

Verify that all services are attached to the same network.

---

# Viewing Logs

Logs provide valuable information during troubleshooting.

Display logs for all services.

```bash
docker compose logs
```

Display logs for a single service.

```bash
docker compose logs node-app

docker compose logs mongodb

docker compose logs mongo-express
```

Follow logs continuously.

```bash
docker compose logs -f
```

---

# Inspecting Containers

Inspect container configuration.

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

Inspection commands reveal detailed runtime information, including networking, mounted volumes, and environment variables.

---

# Restarting the Application Stack

Sometimes the simplest solution is to recreate the application.

Stop all services.

```bash
docker compose down
```

Start the application again.

```bash
docker compose up -d
```

This recreates the containers using the current Docker Compose configuration.

---

# Useful Troubleshooting Commands

| Command | Purpose |
|----------|---------|
| `docker ps -a` | Display all containers |
| `docker compose ps` | Display Compose services |
| `docker compose logs` | View service logs |
| `docker compose logs -f` | Follow logs |
| `docker inspect` | Inspect a container |
| `docker network ls` | List networks |
| `docker network inspect` | Inspect a network |
| `docker compose config` | Validate Compose configuration |
| `docker compose down` | Stop and remove the application |
| `docker compose up -d` | Redeploy the application |

---

# Troubleshooting Workflow

A structured troubleshooting process helps identify issues efficiently.

```text
Identify the Problem
          │
          ▼
Review Error Messages
          │
          ▼
Inspect Running Containers
          │
          ▼
Review Logs
          │
          ▼
Inspect Networks
          │
          ▼
Verify Configuration
          │
          ▼
Apply Fix
          │
          ▼
Redeploy and Verify
```

---

# Summary

Most Docker Compose issues can be resolved through a systematic troubleshooting approach. Reviewing logs, validating the Compose configuration, inspecting networks, and verifying container status provide valuable insight into deployment problems.

Developing these troubleshooting skills is essential for managing containerized applications in both development and production environments.