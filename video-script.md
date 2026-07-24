# Project Demonstration Video Script

**Project:** Docker Compose Multi-Container Application on AWS

**Target Duration:** 8–10 Minutes

**Audience**

- Recruiters
- Hiring Managers
- DevOps Engineers
- Cloud Engineers
- Platform Engineers
- Software Engineers

---

# Video Objective

The purpose of this demonstration is to showcase the deployment and management of a complete multi-container application using Docker Compose on AWS.

Unlike a single-container deployment, this project demonstrates how Docker Compose orchestrates multiple services—including a Node.js application, MongoDB database, and Mongo Express interface—into a unified application stack.

The video highlights architecture, service orchestration, networking, deployment, verification, troubleshooting, and key engineering lessons.

---

# Scene 1 — Introduction (45 seconds)

### Screen

Open the GitHub repository homepage.

### Narration

> Hello everyone, and welcome to this project demonstration.

> In this project, I deployed a multi-container application using Docker Compose on an AWS EC2 instance.

> The stack consists of a Node.js application, a MongoDB database, and Mongo Express, all orchestrated through a single Docker Compose configuration.

> Throughout the project, I documented the implementation process, architecture, deployment workflow, troubleshooting techniques, and lessons learned.

---

# Scene 2 — Repository Overview (1 minute)

### Screen

Scroll through the repository.

Highlight:

- README
- docker-compose.yml
- Commands Guide
- Setup Guide
- Troubleshooting Guide
- Lessons Learned
- Architecture Diagram

### Narration

> This repository is organized to make the deployment reproducible and easy to understand.

> It includes comprehensive documentation covering architecture, deployment steps, Docker Compose commands, troubleshooting procedures, and engineering reflections.

---

# Scene 3 — Architecture Diagram (1 minute)

### Screen

Display:

```text
images/architecture.png
```

Zoom into the architecture.

### Narration

> The application consists of three services managed by Docker Compose.

> The Node.js application communicates with MongoDB for data storage.

> Mongo Express provides a web-based interface for interacting with the database.

> Docker Compose automatically creates a shared network, allowing services to communicate securely using service names.

---

# Scene 4 — Docker Compose Configuration (1 minute)

### Screen

Open `docker-compose.yml`.

Highlight:

- Services
- Environment Variables
- Port Mappings
- Networks
- Container Names

### Narration

> The docker-compose.yml file defines the entire application stack.

> Rather than starting each container individually, every service is declared in one configuration file.

> This approach improves consistency, repeatability, and simplifies deployments.

---

# Scene 5 — Deploy the Application Stack (1 minute)

### Screen

Run:

```bash
docker compose up -d
```

Show:

```bash
docker compose ps
```

### Narration

> With a single command, Docker Compose creates the required network, starts MongoDB, Mongo Express, and the Node.js application, and connects them together automatically.

> The `docker compose ps` command confirms that all services are running successfully.

---

# Scene 6 — Verify Service Communication (1 minute)

### Screen

Run:

```bash
docker network inspect <network-name>
```

Display the connected containers.

### Narration

> Docker Compose automatically creates a dedicated bridge network for the project.

> Each service is attached to this network, enabling secure communication without manually configuring IP addresses.

> Services communicate using their Compose service names, simplifying application configuration.

---

# Scene 7 — Demonstrate the Application (1 minute)

### Screen

Open the Node.js application in a web browser.

Then open Mongo Express.

### Narration

> The successful loading of the application confirms that the backend, database, and networking are functioning correctly.

> Mongo Express also verifies that the database is running and accessible within the application stack.

---

# Scene 8 — Logs and Troubleshooting (1 minute)

### Screen

Run:

```bash
docker compose logs
```

Then:

```bash
docker compose logs -f
```

Access the Node.js container.

```bash
docker exec -it node-app sh
```

### Narration

> Docker Compose provides centralized logging across all services.

> This makes it easier to identify startup issues, monitor runtime behavior, and troubleshoot connectivity problems.

> Interactive container access is also useful for inspecting files and verifying configurations.

---

# Scene 9 — Key Lessons Learned (1 minute)

### Screen

Return to the README and scroll to the "Lessons Learned" section.

### Narration

> This project strengthened my understanding of multi-container application design, service orchestration, Docker networking, and cloud deployments.

> It also reinforced the importance of documentation, automation, and structured troubleshooting in modern DevOps workflows.

---

# Scene 10 — Conclusion (30–45 seconds)

### Screen

Return to the GitHub repository homepage.

### Narration

> Thank you for watching this demonstration.

> This repository represents a practical implementation of Docker Compose for deploying and managing a complete application stack on AWS.

> Feedback and suggestions are always appreciated. Thank you for your time.

---

# Recording Checklist

Before recording, verify the following:

- Terminal font size is readable.
- The Docker Compose stack starts without errors.
- The Node.js application is accessible.
- Mongo Express loads successfully.
- Architecture diagram is complete.
- README and documentation are up to date.
- Sensitive information (credentials, keys, tokens, private IPs) is hidden.
- Screenshots have been added to the repository.
- Desktop notifications are disabled.

---

# Suggested Repository Assets

To strengthen the repository, include:

- `architecture.png` exported from Draw.io
- Screenshot of `docker-compose.yml`
- Screenshot of `docker compose up`
- Screenshot of running containers
- Screenshot of Docker network
- Screenshot of Mongo Express
- Screenshot of the Node.js application
- Screenshot of Docker logs
- Short animated GIF showing the deployment process
- Video thumbnail image

---

# Estimated Timeline

| Section | Approximate Duration |
|----------|----------------------|
| Introduction | 0:45 |
| Repository Overview | 1:00 |
| Architecture | 1:00 |
| Compose Configuration | 1:00 |
| Deploy Stack | 1:00 |
| Networking | 1:00 |
| Application Demo | 1:00 |
| Troubleshooting | 1:00 |
| Lessons Learned | 1:00 |
| Conclusion | 0:30 |

**Total Duration:** Approximately **9–10 minutes**

---

# Final Notes

This video should demonstrate not only that the application works, but also your understanding of Docker Compose concepts such as service orchestration, networking, configuration management, and operational troubleshooting. A clear explanation of the architecture and deployment process will help viewers understand the engineering decisions behind the implementation and showcase practical DevOps skills beyond simply running containers.
