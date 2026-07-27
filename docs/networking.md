# Docker Compose Networking

## Introduction

Networking is one of Docker Compose's most powerful features. It enables multiple containers to communicate securely without requiring manual network configuration.

When Docker Compose starts an application, it automatically creates a dedicated network and connects every service defined in the `docker-compose.yml` file to that network.

This allows containers to communicate reliably while remaining isolated from unrelated containers running on the host machine.

---

# Why Networking Matters

In a multi-container application, services rarely operate independently.

For example:

- A web application needs to communicate with a database.
- A backend API may connect to a cache.
- Monitoring services collect metrics from application containers.
- Administrative interfaces connect to backend databases.

Without networking, these services cannot exchange data or work together as a complete application.

Docker Compose automates this process.

---

# Network Architecture

The application deployed in this project consists of three services connected through a shared Docker network.

```text
                 Web Browser
                      │
                      ▼
             Node.js Application
                      │
                      ▼
                  MongoDB
                      ▲
                      │
              Mongo Express

          Docker Compose Bridge Network
```

Each service runs inside its own isolated container while communicating through the Docker network.

---

# Automatic Network Creation

When the following command is executed:

```bash
docker compose up -d
```

Docker Compose automatically:

- Creates a dedicated bridge network.
- Connects every service to that network.
- Configures internal DNS.
- Enables communication using service names.

No additional networking commands are required.

---

# Listing Available Networks

Display all Docker networks.

```bash
docker network ls
```

Example output:

```text
NETWORK ID     NAME                    DRIVER    SCOPE
a1b2c3d4e5f6   bridge                  bridge    local
d7e8f9g0h1i2   host                    host      local
j3k4l5m6n7o8   none                    null      local
p9q0r1s2t3u4   docker-compose_default  bridge    local
```

The project network is automatically created using the project name followed by `_default`.

---

# Inspecting the Network

Inspect the Docker Compose network.

```bash
docker network inspect <network-name>
```

Replace `<network-name>` with the name of your project's network.

The inspection output provides information such as:

- Connected containers
- Network driver
- Subnet configuration
- Gateway
- Internal IP addresses

Inspecting the network is useful for verifying that all required services are connected correctly.

---

# Bridge Network

By default, Docker Compose creates a **bridge network**.

A bridge network:

- Connects related containers.
- Isolates the application from other Docker networks.
- Allows secure communication between services.
- Supports automatic DNS resolution.

This default behavior is sufficient for most local development projects.

---

# Internal DNS Resolution

Docker Compose automatically provides an internal DNS service.

Instead of locating another container by its IP address, a service simply references the other service by name.

Example:

```text
Node.js
    │
    ▼
mongodb
```

Docker automatically resolves the service name to the correct container.

This makes the application easier to configure and maintain.

---

# Service Communication

The services in this project communicate as follows.

```text
User
 │
 ▼
Browser
 │
 ▼
Node.js Application
 │
 ▼
MongoDB
 ▲
 │
Mongo Express
```

The Node.js application stores and retrieves data from MongoDB.

Mongo Express connects to the same MongoDB instance to provide a browser-based administration interface.

Because all services belong to the same Docker network, communication occurs without exposing internal traffic to the host machine.

---

# Host-to-Container Communication

External users access services through published ports.

Example:

```text
Host Machine

localhost:3000
        │
        ▼
Node.js Container
```

```text
Host Machine

localhost:8081
        │
        ▼
Mongo Express Container
```

Docker forwards incoming traffic from the host machine to the appropriate container.

---

# Container-to-Container Communication

Communication between containers does not require published ports.

Instead, Docker routes traffic internally through the bridge network.

Example:

```text
Node.js

↓

mongodb:27017
```

The Node.js application communicates directly with MongoDB using the database service name.

This communication remains entirely inside Docker's virtual network.

---

# Benefits of Docker Compose Networking

Automatic networking provides several advantages.

- Secure communication between services.
- Automatic DNS resolution.
- Simplified application configuration.
- Reduced manual network management.
- Improved portability.
- Easier troubleshooting.
- Better separation between applications.

These features allow developers to focus on application development rather than network configuration.

---

# Common Networking Issues

Although Docker Compose simplifies networking, configuration problems can still occur.

Common issues include:

- Incorrect service names.
- Containers attached to different networks.
- Incorrect port mappings.
- Firewall restrictions.
- Application configuration errors.

Most networking problems can be diagnosed using Docker inspection and logging commands.

---

# Useful Networking Commands

List Docker networks.

```bash
docker network ls
```

Inspect a network.

```bash
docker network inspect <network-name>
```

List running containers.

```bash
docker ps
```

Display Docker Compose services.

```bash
docker compose ps
```

View service logs.

```bash
docker compose logs
```

These commands are commonly used when verifying container communication.

---

# Best Practices

The following practices help maintain reliable Docker networking.

- Use Docker Compose service names instead of IP addresses.
- Keep related services on the same network.
- Publish only the ports that require external access.
- Verify network connectivity after deployment.
- Inspect networks during troubleshooting.
- Document network architecture for future reference.

Following these practices results in more maintainable and portable applications.

---

# Summary

Docker Compose networking provides a simple yet powerful mechanism for connecting multiple containers into a cohesive application.

By automatically creating a dedicated bridge network, configuring internal DNS, and enabling service-to-service communication through service names, Docker Compose removes much of the complexity traditionally associated with container networking.

In this project, Docker Compose successfully connected the Node.js application, MongoDB database, and Mongo Express interface into a single application stack, demonstrating how containerized services can communicate securely and reliably while remaining isolated from the host system and other Docker applications.