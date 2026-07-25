# Docker Compose Commands Reference

This document contains the Docker Compose commands used throughout this project, along with explanations of their purpose and common use cases.

---

# Table of Contents

- Verify Docker Compose
- Validate Compose File
- Start Services
- Stop Services
- Restart Services
- View Running Services
- View Logs
- Build Services
- Pull Images
- Remove Services
- Inspect Networks
- Inspect Volumes
- Execute Commands Inside Containers
- Monitor Containers
- Cleanup Commands
- Command Summary

---

# Verify Docker Compose Installation

Verify Docker Compose is installed correctly.

```bash
docker compose version
```

Example Output

```text
Docker Compose version v2.x.x
```

---

# Validate the Compose File

Check that the docker-compose.yml file is valid.

```bash
docker compose config
```

Purpose

- Validates syntax
- Merges configuration
- Displays final configuration
- Detects YAML errors

---

# Start the Application Stack

Start every service defined in docker-compose.yml.

```bash
docker compose up
```

Docker Compose automatically:

- Creates the network
- Pulls images
- Creates containers
- Starts services

---

# Start in Detached Mode

```bash
docker compose up -d
```

Runs every service in the background.

---

# Stop the Application

```bash
docker compose stop
```

Stops every running service while preserving containers.

---

# Restart the Application

```bash
docker compose restart
```

Restarts all services.

Restart a single service.

```bash
docker compose restart mongodb
```

---

# Shut Down the Stack

```bash
docker compose down
```

Removes:

- Containers
- Networks

Volumes remain unless explicitly removed.

---

# Remove Everything

```bash
docker compose down -v
```

Removes:

- Containers
- Networks
- Volumes

---

# View Running Services

```bash
docker compose ps
```

Displays:

- Service names
- Container names
- Ports
- Current status

---

# View Docker Containers

```bash
docker ps
```

Lists every running container.

---

# View Logs

Display logs from every service.

```bash
docker compose logs
```

---

# View Logs for One Service

MongoDB

```bash
docker compose logs mongodb
```

Mongo Express

```bash
docker compose logs mongo-express
```

Node.js

```bash
docker compose logs node-app
```

---

# Follow Logs

```bash
docker compose logs -f
```

Displays log output in real time.

---

# Build Images

Rebuild every service.

```bash
docker compose build
```

Rebuild one service.

```bash
docker compose build node-app
```

---

# Pull Latest Images

```bash
docker compose pull
```

Downloads the latest images defined in the Compose file.

---

# Execute Commands Inside a Container

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

Useful for:

- Debugging
- File inspection
- Running commands
- Verifying configuration

---

# List Docker Networks

```bash
docker network ls
```

---

# Inspect Docker Network

```bash
docker network inspect <network-name>
```

Displays:

- Connected containers
- IP addresses
- Network driver
- Subnet

---

# List Docker Volumes

```bash
docker volume ls
```

---

# Inspect Docker Volume

```bash
docker volume inspect <volume-name>
```

---

# Inspect a Service

```bash
docker inspect node-app
```

Shows detailed configuration including:

- Environment variables
- Ports
- Networks
- Mounts
- Labels

---

# Display Resource Usage

```bash
docker stats
```

Monitor:

- CPU usage
- Memory usage
- Network traffic
- Disk I/O

---

# View Running Processes

```bash
docker top node-app
```

Displays running processes inside the container.

---

# Remove Unused Containers

```bash
docker container prune
```

---

# Remove Unused Images

```bash
docker image prune
```

---

# Remove Unused Volumes

```bash
docker volume prune
```

---

# Remove Unused Networks

```bash
docker network prune
```

---

# Remove Everything Unused

```bash
docker system prune
```

Remove all unused resources.

```bash
docker system prune -a
```

---

# Typical Workflow

```bash
docker compose up -d

docker compose ps

docker compose logs

docker compose logs -f

docker compose restart

docker compose down
```

This represents the standard operational workflow used throughout this project.

---

# Command Summary

| Command | Purpose |
|----------|---------|
| docker compose version | Verify Compose installation |
| docker compose config | Validate Compose file |
| docker compose up | Start services |
| docker compose up -d | Start services in background |
| docker compose stop | Stop services |
| docker compose restart | Restart services |
| docker compose down | Stop and remove services |
| docker compose down -v | Remove services and volumes |
| docker compose ps | View services |
| docker compose logs | View logs |
| docker compose logs -f | Follow logs |
| docker compose build | Build images |
| docker compose pull | Pull images |
| docker network ls | List networks |
| docker network inspect | Inspect network |
| docker volume ls | List volumes |
| docker volume inspect | Inspect volume |
| docker stats | Monitor resource usage |
| docker system prune | Clean Docker resources |

---

# Conclusion

Docker Compose simplifies the deployment and management of multi-container applications by providing a single interface for building, starting, monitoring, and maintaining interconnected services. Mastering these commands is essential for developing, troubleshooting, and operating containerized application stacks efficiently.
