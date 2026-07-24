# Troubleshooting Guide

This document provides a structured approach to diagnosing and resolving common issues encountered while deploying and managing the multi-container application using Docker Compose.

The project consists of:

- Node.js Application
- MongoDB Database
- Mongo Express
- Docker Compose
- Docker Networking

---

# Table of Contents

- Troubleshooting Workflow
- Docker Compose Installation Issues
- Compose File Validation Errors
- Service Startup Failures
- Container Restart Loops
- Docker Network Issues
- Service Discovery Problems
- MongoDB Connectivity Issues
- Mongo Express Issues
- Node.js Application Issues
- Port Mapping Problems
- Viewing Logs
- Interactive Debugging
- Volume Issues
- Cleanup Problems
- Troubleshooting Checklist
- Best Practices

---

# Troubleshooting Workflow

Always follow a systematic troubleshooting process.

```text
Issue Detected
      │
      ▼
Read Error Message
      │
      ▼
Validate docker-compose.yml
      │
      ▼
Verify Docker Engine
      │
      ▼
Check Running Services
      │
      ▼
Review Logs
      │
      ▼
Inspect Network
      │
      ▼
Verify Service Connectivity
      │
      ▼
Apply Resolution
      │
      ▼
Restart Services
```

Avoid making multiple configuration changes simultaneously. Resolve one issue at a time.

---

# Issue 1 — Docker Compose Command Not Found

## Symptoms

```text
docker: 'compose' is not a docker command
```

## Possible Causes

- Docker Compose is not installed.
- Docker installation is incomplete.
- Incorrect Docker version.

## Verify Installation

```bash
docker compose version
```

If the command fails, install or update Docker Compose before continuing.

---

# Issue 2 — Invalid Compose File

## Symptoms

```text
services.xxx contains an invalid type
```

## Possible Causes

- YAML indentation errors.
- Missing required fields.
- Incorrect syntax.

## Verify Configuration

```bash
docker compose config
```

This validates the Compose file and identifies configuration errors before deployment.

---

# Issue 3 — Services Fail to Start

## Symptoms

Containers exit immediately or fail during startup.

## Possible Causes

- Incorrect image name.
- Missing environment variables.
- Invalid configuration.
- Application startup failure.

## Diagnostic Commands

```bash
docker compose ps

docker compose logs
```

Review the logs for the affected service and correct the reported issue.

---

# Issue 4 — Container Restart Loop

## Symptoms

The container repeatedly starts and stops.

## Possible Causes

- Application crash.
- Missing dependencies.
- Incorrect startup command.
- Configuration error.

## Resolution

Inspect the service logs.

```bash
docker compose logs node-app
```

Resolve the application error before restarting the stack.

---

# Issue 5 — Docker Network Issues

## Symptoms

Containers cannot communicate with each other.

## Possible Causes

- Containers are not attached to the same network.
- Incorrect service names.
- Network creation failure.

## Verify Networks

```bash
docker network ls
```

Inspect the project network.

```bash
docker network inspect <network-name>
```

Confirm that all services are attached to the same Docker Compose network.

---

# Issue 6 — Service Discovery Failure

## Symptoms

The Node.js application cannot locate MongoDB.

## Possible Causes

- Incorrect hostname.
- Incorrect service name.
- Configuration mismatch.

## Resolution

Verify the service names defined in the Compose file.

Docker Compose automatically provides DNS-based service discovery.

The application should reference:

```text
mongodb
```

instead of an IP address.

---

# Issue 7 — MongoDB Connection Errors

## Symptoms

The application cannot connect to the database.

## Possible Causes

- MongoDB container not running.
- Invalid credentials.
- Incorrect environment variables.
- Database initialization incomplete.

## Diagnostic Commands

```bash
docker compose logs mongodb

docker compose ps
```

Verify MongoDB is healthy before starting dependent services.

---

# Issue 8 — Mongo Express Not Accessible

## Symptoms

The browser cannot load Mongo Express.

## Possible Causes

- Container stopped.
- Incorrect host port.
- Security group restrictions.
- MongoDB unavailable.

## Resolution

Verify:

```bash
docker compose ps

docker compose logs mongo-express
```

Also confirm the AWS Security Group allows access to the configured host port.

---

# Issue 9 — Node.js Application Not Accessible

## Symptoms

Browser displays:

- Connection refused
- Timeout
- Unable to reach the application

## Possible Causes

- Node.js container stopped.
- Incorrect port mapping.
- Application startup failure.
- Security group configuration.

## Diagnostic Commands

```bash
docker compose logs node-app

docker compose ps
```

Verify:

- Application is running.
- Host port is exposed.
- AWS inbound rules allow traffic.

---

# Issue 10 — Port Already in Use

## Symptoms

```text
Bind for 0.0.0.0 failed
```

## Possible Causes

Another application is already using the requested port.

## Resolution

Identify the conflicting process or update the host port mapping in the Compose file.

Redeploy the stack.

---

# Issue 11 — Changes Not Reflected

## Symptoms

Application updates do not appear after modifying the source code.

## Possible Causes

- Containers were restarted without rebuilding the image.

## Resolution

Rebuild the application image.

```bash
docker compose build
```

Restart the application.

```bash
docker compose up -d
```

---

# Issue 12 — Inspecting Running Containers

Access an interactive shell.

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

Interactive debugging is useful for verifying configuration, files, and runtime behavior.

---

# Issue 13 — Persistent Data Issues

## Symptoms

Expected data is missing after restarting services.

## Possible Causes

- Volumes were removed.
- Incorrect volume configuration.
- Data stored only inside the container filesystem.

## Diagnostic Commands

```bash
docker volume ls

docker volume inspect <volume-name>
```

Verify that persistent storage is configured correctly.

---

# Issue 14 — Viewing Logs

Display logs for every service.

```bash
docker compose logs
```

View a single service.

```bash
docker compose logs mongodb

docker compose logs mongo-express

docker compose logs node-app
```

Follow logs continuously.

```bash
docker compose logs -f
```

Logs provide valuable insight into startup, connectivity, and runtime issues.

---

# Issue 15 — Cleaning Up Resources

Remove the application stack.

```bash
docker compose down
```

Remove associated volumes.

```bash
docker compose down -v
```

Remove unused Docker resources.

```bash
docker system prune
```

Use cleanup commands carefully, especially when working with persistent data.

---

# Useful Diagnostic Commands

| Command | Purpose |
|----------|---------|
| `docker compose config` | Validate Compose configuration |
| `docker compose ps` | View running services |
| `docker compose logs` | View service logs |
| `docker compose build` | Rebuild images |
| `docker network inspect` | Verify networking |
| `docker volume inspect` | Inspect persistent storage |
| `docker inspect` | View detailed container configuration |
| `docker stats` | Monitor resource usage |
| `docker exec -it` | Interactive debugging |

---

# Troubleshooting Checklist

Before concluding deployment is successful, verify the following:

- Docker Engine is running.
- Docker Compose is installed.
- Compose configuration validates successfully.
- All services are running.
- Docker network exists.
- Node.js communicates with MongoDB.
- Mongo Express loads successfully.
- Required ports are exposed.
- AWS Security Group allows inbound traffic.
- Service logs contain no critical errors.

---

# Best Practices

- Validate the Compose file before deployment.
- Use meaningful service names.
- Prefer service names over IP addresses for inter-service communication.
- Review logs after every deployment.
- Keep configuration in environment variables.
- Test one change at a time.
- Rebuild images after modifying application code.
- Document recurring issues and their resolutions.

---

# Conclusion

Troubleshooting Docker Compose applications requires understanding not only individual containers but also the relationships between services. By validating the Compose configuration, inspecting networks, reviewing logs, and confirming service discovery, most deployment issues can be resolved quickly and systematically. Following a structured troubleshooting workflow leads to more reliable deployments and a stronger operational understanding of multi-container applications.
