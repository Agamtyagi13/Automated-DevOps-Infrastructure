# Phase 3 – Docker Containerization

## Objective

The objective of this phase is to containerize a static NGINX web application using Docker. The application is packaged into a Docker image and executed inside an isolated container with proper networking, health checks, restart policies, and resource limits.

---

## Prerequisites

- Ubuntu (WSL2)
- Docker Engine installed
- Git
- Basic Linux knowledge

---

## Project Structure

```
docker/
├── Dockerfile
└── html/
    └── index.html
```

---

## Dockerfile

```dockerfile
FROM nginx:1.27-alpine

LABEL maintainer="Agam Tyagi"
LABEL project="Automated DevOps Infrastructure"

COPY html/ /usr/share/nginx/html/

EXPOSE 80

HEALTHCHECK --interval=30s \
  --timeout=5s \
  --start-period=10s \
  --retries=3 \
  CMD wget --spider http://localhost || exit 1

CMD ["nginx", "-g", "daemon off;"]
```

---

## Dockerfile Explanation

### Base Image

```dockerfile
FROM nginx:1.27-alpine
```

Uses the lightweight Alpine Linux version of the official NGINX image.

---

### Labels

```dockerfile
LABEL maintainer="Agam Tyagi"
LABEL project="Automated DevOps Infrastructure"
```

Adds metadata to the Docker image.

---

### Copy Application

```dockerfile
COPY html/ /usr/share/nginx/html/
```

Copies the website files into NGINX's default web directory.

---

### Expose Port

```dockerfile
EXPOSE 80
```

Documents that the application listens on port 80.

---

### Health Check

```dockerfile
HEALTHCHECK --interval=30s \
  --timeout=5s \
  --start-period=10s \
  --retries=3 \
  CMD wget --spider http://localhost || exit 1
```

Docker checks every 30 seconds whether the NGINX server is responding.

---

### Start Command

```dockerfile
CMD ["nginx", "-g", "daemon off;"]
```

Starts the NGINX server in the foreground.

---

# Build Docker Image

```bash
docker build -t xqora-nginx:v1 .
```

Verify the image:

```bash
docker images
```

---

# Create Docker Network

```bash
docker network create devops-network
```

Verify:

```bash
docker network ls
```

---

# Create Docker Volume

```bash
docker volume create nginx-data
```

Verify:

```bash
docker volume ls
```

---

# Run Container

```bash
docker run -d \
--name nginx-server \
--network devops-network \
-p 8080:80 \
--restart unless-stopped \
--memory="256m" \
--cpus="0.5" \
xqora-nginx:v1
```

---

## Command Breakdown

### Detached Mode

```bash
-d
```

Runs the container in the background.

---

### Container Name

```bash
--name nginx-server
```

Assigns a custom container name.

---

### Custom Network

```bash
--network devops-network
```

Connects the container to a user-defined Docker network.

---

### Port Mapping

```bash
-p 8080:80
```

Maps:

- Host Port → 8080
- Container Port → 80

Application URL:

```
http://localhost:8080
```

---

### Restart Policy

```bash
--restart unless-stopped
```

Automatically restarts the container if Docker restarts or the container crashes.

---

### Memory Limit

```bash
--memory="256m"
```

Limits the container to 256 MB RAM.

---

### CPU Limit

```bash
--cpus="0.5"
```

Limits the container to half of one CPU core.

---

## Verify Running Container

```bash
docker ps
```

---

## Verify Logs

```bash
docker logs nginx-server
```

---

## Verify Health Status

```bash
docker inspect nginx-server
```

or

```bash
docker inspect --format='{{json .State.Health}}' nginx-server
```

Expected output:

```
healthy
```

---

## Verify Network

```bash
docker network inspect devops-network
```

---

## Verify Resource Usage

```bash
docker stats
```

---

## Stop Container

```bash
docker stop nginx-server
```

---

## Start Container

```bash
docker start nginx-server
```

---

## Restart Container

```bash
docker restart nginx-server
```

---

## Remove Container

```bash
docker rm -f nginx-server
```

---

## Remove Image

```bash
docker rmi xqora-nginx:v1
```

---

## Learning Outcomes

- Built a custom Docker image.
- Containerized an NGINX web application.
- Created and managed Docker networks.
- Created Docker volumes.
- Configured Docker health checks.
- Applied restart policies.
- Applied CPU and memory limits.
- Verified container status, logs, health, and resource usage.
- Exposed the application on localhost using port mapping.

---

## Screenshots to Include

- Docker image (`docker images`)
- Running container (`docker ps`)
- Docker network (`docker network ls`)
- Docker volume (`docker volume ls`)
- Health check (`docker inspect`)
- Docker stats (`docker stats`)
- Application running in browser (`http://localhost:8080`)

---

## Conclusion

In this phase, the application was successfully containerized using Docker. The container was configured with networking, resource limits, health monitoring, and automatic restart policies, providing a production-oriented Docker setup that serves as the foundation for the next phase, where the same application will be deployed to Kubernetes.

Developer
     │
     │ writes
     ▼
Dockerfile
     │
     │ git push
     ▼
GitHub
     │                               Relationship between docker and jenkins (jenkins uses dockerfile build the image)
     ▼
Jenkins
     │
docker build
     │
(uses Dockerfile)
     ▼
Docker Image
     │
docker push
     ▼
Docker Hub
     │
kubectl apply
     ▼
Kubernetes
     │
docker pull
     ▼
Running Pod
