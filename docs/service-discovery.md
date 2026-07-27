# Docker Compose Service Discovery

## Introduction

One of Docker Compose's most valuable features is **service discovery**.

Service discovery allows containers to locate and communicate with one another automatically without requiring developers to manually configure IP addresses.

When Docker Compose creates a network, it also creates an internal DNS service that maps service names to their corresponding containers.

As a result, services communicate using predictable names rather than temporary IP addresses.

---

# What is Service Discovery?

Service discovery is the process by which one service automatically finds another service on the same network.

Instead of asking:

> "What is the IP address of the MongoDB container?"

the application simply asks:

> "Connect to the **mongodb** service."

Docker Compose resolves the service name to the correct container automatically.

---

# Why IP Addresses Are Not Used

Every Docker container receives an IP address when it starts.

For example:

```text
Node.js      → 172.20.0.3

MongoDB      → 172.20.0.4

Mongo Express → 172.20.0.5
```

These IP addresses are **temporary**.

If a container is recreated, Docker may assign a different IP address.

For example:

```text
Yesterday

MongoDB → 172.20.0.4

Today

MongoDB → 172.20.0.8
```

If an application depends on fixed IP addresses, it may stop working after containers are recreated.

Service discovery solves this problem by allowing applications to use service names instead of IP addresses.

---

# How Docker Compose Provides Service Discovery

When Docker Compose starts an application, it performs several tasks automatically.

```text
Read docker-compose.yml
          │
          ▼
Create Docker Network
          │
          ▼
Create Internal DNS
          │
          ▼
Register Service Names
          │
          ▼
Start Containers
```

Every service defined in the Compose file is automatically registered with Docker's internal DNS server.

---

# Service Names

Consider the following simplified Compose configuration.

```yaml
services:
  node-app:

  mongodb:

  mongo-express:
```

Docker automatically registers the following service names.

```text
node-app

mongodb

mongo-express
```

These names become available to every container connected to the same Docker network.

---

# Example Communication

Instead of writing:

```text
172.20.0.4
```

the Node.js application connects using:

```text
mongodb
```

This is both simpler and more reliable.

The application does not need to know the database container's IP address because Docker resolves the service name automatically.

---

# Communication Flow

The communication process works as follows.

```text
Node.js Application
          │
          ▼
Requests "mongodb"
          │
          ▼
Docker Internal DNS
          │
          ▼
MongoDB Container
```

The DNS lookup occurs entirely within Docker's network.

No external DNS server is involved.

---

# Benefits of Service Discovery

Using service names instead of IP addresses provides several advantages.

- No manual IP management.
- Containers can be recreated without changing application configuration.
- Improved portability.
- Simpler deployments.
- Easier maintenance.
- Reduced configuration errors.
- Better scalability.

These benefits make Docker Compose projects easier to develop and maintain.

---

# Service Discovery in This Project

This project consists of three services.

```text
Browser
    │
    ▼
Node.js
    │
    ▼
MongoDB
    ▲
    │
Mongo Express
```

The Node.js application communicates with MongoDB using the **mongodb** service name.

Mongo Express also connects to the same MongoDB service through Docker's internal network.

Neither service requires knowledge of the database container's IP address.

---

# Common Mistakes

Several common configuration mistakes can prevent service discovery from working correctly.

### Incorrect Service Name

Using:

```text
mongo-db
```

instead of:

```text
mongodb
```

causes connection failures because the service name must exactly match the name defined in the Compose file.

---

### Different Networks

Containers attached to different Docker networks cannot communicate using service discovery.

Always verify that related services belong to the same Docker Compose network.

---

### Using Container IP Addresses

Applications should never depend on container IP addresses.

Containers are frequently recreated, and their IP addresses can change.

Service names provide a stable method of communication.

---

### Containers Not Running

A service cannot be discovered if its container is not running.

Verify service status using:

```bash
docker compose ps
```

or

```bash
docker ps
```

---

# Verifying Service Discovery

Several Docker commands can help verify service discovery.

Display Compose services.

```bash
docker compose ps
```

List running containers.

```bash
docker ps
```

Inspect the Docker network.

```bash
docker network inspect <network-name>
```

View application logs.

```bash
docker compose logs
```

These commands confirm that services are running and connected to the same network.

---

# Best Practices

To ensure reliable service discovery:

- Use descriptive service names.
- Reference services by name instead of IP address.
- Keep related services on the same Docker network.
- Verify service names before deployment.
- Inspect Docker networks during troubleshooting.
- Avoid hardcoding network information in application code.

Following these practices makes Docker Compose applications easier to manage and more resilient to change.

---

# Summary

Docker Compose service discovery simplifies communication between containers by automatically providing internal DNS resolution.

Instead of relying on temporary IP addresses, applications communicate using stable service names defined in the `docker-compose.yml` file.

In this project, service discovery enabled the Node.js application, MongoDB database, and Mongo Express interface to communicate seamlessly, demonstrating one of Docker Compose's most powerful features for building reliable and maintainable multi-container applications.