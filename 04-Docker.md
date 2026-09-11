# Docker CLI for DevOps

## Image Management

List all locally cached Docker images:
```bash
docker images
```

Download an image from Docker Hub or a configured registry:
```bash
docker pull nginx
```

Build a Docker image from a Dockerfile in the current directory and tag it:
```bash
docker build -t myapp:v1 .
```

Build an image using a specific target build stage multi-stage Dockerfiles:
```bash
docker build --target builder -t myapp:v1-builder .
```

Create a new tag reference pointing to an existing local image:
```bash
docker tag myapp:v1 myrepo/myapp:v1
```

Upload a local image tag to a remote container registry:
```bash
docker push myrepo/myapp:v1
```

Delete a locally stored container image by its ID or tag:
```bash
docker rmi myapp:v1
```

Delete all unused, dangling container images on the system:
```bash
docker image prune -f
```

## Container Lifecycle

List all currently running containers:
```bash
docker ps
```

List all local containers regardless of their running status:
```bash
docker ps -a
```

Run a new container in detached background mode with port forwarding:
```bash
docker run -d -p 8080:80 --name my-web-app nginx
```

Start one or more stopped containers:
```bash
docker start container-id
```

Gracefully stop a running container by sending a SIGTERM signal:
```bash
docker stop container-id
```

Restart a running or stopped container:
```bash
docker restart container-id
```

Remove a stopped container from the local host storage:
```bash
docker rm container-id
```

Forcefully remove a running container using a SIGKILL signal:
```bash
docker rm -f container-id
```

## Logging & System Diagnostics

`docker logs` configuration variants:
```bash
docker logs container-id
```
```bash
docker logs -f container-id
```
```bash
docker logs --tail 100 container-id
```
```bash
docker logs --timestamps container-id
```

## Internal Execution & Debugging

Open an interactive terminal inside a running container using Bash:
```bash
docker exec -it container-id bash
```

Open an interactive terminal inside a container using Sh for minimal images:
```bash
docker exec -it container-id sh
```

Execute a single non-interactive command inside a running container without entering it:
```bash
docker exec container-id env
```

## Inspection & Metrics

Return detailed, low-level configuration data on Docker objects in JSON format:
```bash
docker inspect container-id
```

Query a specific property from the configuration payload using Go templates:
```bash
docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' container-id
```

Stream live resource utilization statistics (CPU, memory, network I/O) for containers:
```bash
docker stats
```

View the list of file changes made within a container's writable layer:
```bash
docker diff container-id
```

Display the public-facing ports mapped to a specific container:
```bash
docker port container-id
```

## Storage & Network Components

List all local Docker volumes used for persistent storage:
```bash
docker volume ls
```

Create a named, persistent storage volume separate from container lifecycles:
```bash
docker volume create my-data-vol
```

List all isolated container networks configured on the host machine:
```bash
docker network ls
```

Create a user-defined bridge network for container-to-container communication:
```bash
docker network create my-custom-net
```

## System Cleanup

Display disk space currently consumed by images, containers, volumes, and caches:
```bash
docker system df
```

Wipe out all stopped containers, unused networks, dangling images, and build caches:
```bash
docker system prune -f
```

Deep clean the entire environment including volumes and unused images (destructive):
```bash
docker system prune -a --volumes -f
```
