# Docker Compose Multi-Container Application Walkthrough

## Introduction

Hello everyone!

Welcome to my Docker Compose Multi-Container Application project.

In this project, I built and deployed a containerized application consisting of multiple services managed with Docker Compose.

The application includes:

- A Node.js backend application
- A MongoDB database
- A Mongo Express web interface

The objective of this project was to understand how Docker Compose simplifies the deployment and management of multi-container applications by defining all services in a single configuration file.

---

# Repository Overview

Let's begin by looking at the repository.

The repository contains:

- README.md
- docker-compose.yml
- Node.js application
- Documentation
- Architecture diagrams
- Project screenshots
- Command reference

The README explains the project at a high level, while the documentation folder contains detailed explanations of networking, service discovery, environment variables, troubleshooting, and lessons learned.

---

# Project Architecture

This application consists of three containers.

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

Each service has a single responsibility.

The Node.js application handles requests.

MongoDB stores the application's data.

Mongo Express provides a browser-based interface for viewing and managing the database.

Docker Compose connects all three services through a shared network.

---

# Docker Compose Configuration

The entire application is defined in a single `docker-compose.yml` file.

Within this file, I configured:

- Services
- Images
- Environment variables
- Port mappings
- Networks
- Restart policies

Rather than starting each container individually, Docker Compose manages the complete application stack.

---

# Deploying the Application

To start the application, I ran:

```bash
docker compose up -d
```

Docker Compose automatically:

- Created the Docker network
- Pulled required images
- Created the containers
- Connected every service
- Started the application

This demonstrates one of Docker Compose's greatest strengths: repeatable deployments with a single command.

---

# Verifying the Deployment

After deployment, I verified the running services using:

```bash
docker compose ps
```

and

```bash
docker ps
```

I confirmed that:

- The Node.js application was running.
- MongoDB was running.
- Mongo Express was running.

I also inspected the Docker network to verify that every service belonged to the same network.

---

# Accessing the Application

Next, I opened the Node.js application in the browser.

Successful access confirmed that:

- The application was running correctly.
- Port mapping worked as expected.
- The application could communicate with MongoDB.

I also opened Mongo Express to verify database connectivity.

---

# Networking and Service Discovery

One of the most important concepts demonstrated in this project is service discovery.

Instead of using container IP addresses, the Node.js application connects to MongoDB using the service name defined in the Compose file.

Docker Compose automatically provides internal DNS, allowing services to discover each other without manual network configuration.

This makes the application more portable and easier to maintain.

---

# Environment Variables

Configuration values such as database credentials and application settings are supplied through environment variables.

Separating configuration from application code improves portability and allows the same application image to be used in different environments with different settings.

---

# Troubleshooting

During the project, I used Docker commands to troubleshoot and verify the deployment.

These included:

- Viewing logs
- Inspecting containers
- Inspecting Docker networks
- Validating the Compose configuration

Using these commands helped identify and resolve issues in a structured way.

---

# Key Skills Demonstrated

This project strengthened my practical understanding of:

- Docker Engine
- Docker Compose
- Multi-container applications
- Container networking
- Service discovery
- Environment variables
- Container lifecycle management
- Troubleshooting
- Technical documentation
- Git and GitHub

---

# Lessons Learned

One of the biggest lessons from this project is that Docker Compose allows infrastructure to be defined declaratively.

Instead of managing containers one by one, the entire application can be described in a single configuration file and recreated consistently whenever needed.

I also gained a deeper understanding of how containers communicate, how Docker networking works, and why automation is an important principle in modern DevOps practices.

---

# Next Steps

The next technologies I plan to explore include:

- Docker volumes
- Building custom Docker images
- Docker Compose profiles
- Reverse proxy configuration with Nginx
- CI/CD pipelines
- Kubernetes

These technologies build naturally on the concepts introduced in this project.

---

# Conclusion

Thank you for taking the time to review this project.

This repository represents another step in my journey toward becoming a DevOps and Cloud Engineer.

If you have any feedback, suggestions, or questions, I would be happy to connect and discuss the project.

Thank you for watching!