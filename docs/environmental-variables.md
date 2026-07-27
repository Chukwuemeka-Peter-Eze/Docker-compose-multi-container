# Environment Variables in Docker Compose

## Introduction

Environment variables provide a flexible way to configure applications without modifying their source code.

Instead of hardcoding configuration values such as database credentials, ports, or application settings, Docker Compose injects these values into containers at runtime.

This separation of configuration from application code improves portability, security, and maintainability.

---

# What Are Environment Variables?

Environment variables are key-value pairs made available to an application while it is running.

For example:

```text
DATABASE_HOST=mongodb

DATABASE_PORT=27017

DATABASE_NAME=my-db

DATABASE_USER=admin

DATABASE_PASSWORD=password123
```

Applications read these values during startup and use them to configure their behavior.

---

# Why Use Environment Variables?

Without environment variables, configuration values would need to be written directly into the application source code.

For example:

```javascript
const database = {
    host: "mongodb",
    port: 27017,
    username: "admin",
    password: "password123"
}
```

This approach creates several problems:

- Configuration changes require modifying source code.
- Sensitive information may be exposed.
- Different environments require different code changes.
- Maintaining multiple configurations becomes difficult.

Environment variables solve these issues by separating configuration from the application itself.

---

# Environment Variables in Docker Compose

Docker Compose allows environment variables to be defined for each service.

A simplified example:

```yaml
services:
  mongodb:
    environment:
      MONGO_INITDB_ROOT_USERNAME: admin
      MONGO_INITDB_ROOT_PASSWORD: password123

  mongo-express:
    environment:
      ME_CONFIG_MONGODB_ADMINUSERNAME: admin
      ME_CONFIG_MONGODB_ADMINPASSWORD: password123
```

When Docker Compose creates the containers, these values become available inside the running services.

---

# Environment Variables Used in This Project

The application requires configuration values for communication between services.

Typical examples include:

| Variable | Purpose |
|----------|---------|
| Database Host | Location of MongoDB service |
| Database Port | MongoDB listening port |
| Database Username | Database authentication |
| Database Password | Database authentication |
| Application Port | Port exposed by the Node.js application |

These variables allow each service to locate and communicate with the others correctly.

---

# Database Configuration

The Node.js application connects to MongoDB using environment variables.

Instead of specifying an IP address, the application references the MongoDB service name provided by Docker Compose.

```text
DATABASE_HOST=mongodb
```

Because Docker Compose provides automatic service discovery, the application always connects to the correct container.

---

# Runtime Configuration

Environment variables are read when a container starts.

The general process is:

```text
Docker Compose
        │
        ▼
Reads docker-compose.yml
        │
        ▼
Injects Environment Variables
        │
        ▼
Container Starts
        │
        ▼
Application Reads Configuration
```

This allows the same application image to run in different environments with different configuration values.

---

# Advantages of Environment Variables

Using environment variables provides several important benefits.

### Separation of Configuration

Application code remains independent of deployment-specific settings.

---

### Improved Portability

The same container image can be used across multiple environments simply by changing the configuration values.

---

### Easier Maintenance

Configuration updates do not require rebuilding or modifying application code.

---

### Better Security

Sensitive information is separated from the application source code.

In production environments, secrets management tools should be used instead of storing sensitive values directly in a Compose file.

---

# Best Practices

The following practices improve the management of environment variables.

- Avoid hardcoding configuration values inside application code.
- Use descriptive variable names.
- Keep development and production configurations separate.
- Never commit sensitive credentials to public repositories.
- Use Docker Secrets or dedicated secret management tools for production deployments.
- Document required environment variables for future users.

---

# Common Mistakes

Several common issues can occur when working with environment variables.

### Missing Variables

Applications may fail to start if required variables are not provided.

---

### Typographical Errors

Incorrect variable names prevent applications from reading the expected configuration.

---

### Incorrect Values

Using an incorrect database host, port, username, or password may prevent successful communication between services.

---

### Hardcoding Secrets

Placing passwords directly in source code reduces security and makes configuration difficult to manage.

---

# Verifying Environment Variables

To inspect a running container's environment variables:

```bash
docker inspect <container-name>
```

or access the container and display its environment:

```bash
docker exec -it <container-name> sh
```

Then run:

```bash
env
```

These commands help verify that Docker Compose supplied the expected configuration.

---

# Summary

Environment variables provide a reliable method for configuring containerized applications without modifying their source code.

In this project, Docker Compose supplied the configuration required for the Node.js application, MongoDB, and Mongo Express services to communicate correctly.

By separating configuration from application logic, environment variables make deployments more portable, maintainable, and secure while supporting consistent behavior across different environments.