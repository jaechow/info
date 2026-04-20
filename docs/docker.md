# Docker

Build, run, ship. The commands you reach for daily.

## Build

Build an image from the current directory:

```shell
docker build -t myapp:latest .
```

Build with a specific Dockerfile and build arg:

```shell
docker build -f Dockerfile.prod --build-arg NODE_ENV=production -t myapp:prod .
```

---

## Run

Run a container interactively with port mapping:

```shell
docker run -it -p 3000:3000 myapp:latest
```

Run detached with a name and auto-remove on exit:

```shell
docker run -d --rm --name myapp -p 8080:8080 myapp:latest
```

Run with a volume mount (bind mount for development):

```shell
docker run -v $(pwd)/src:/app/src -p 3000:3000 myapp:latest
```

---

## Exec

Open a shell in a running container:

```shell
docker exec -it myapp /bin/sh
```

Run a one-off command:

```shell
docker exec myapp cat /app/config.json
```

---

## Compose

Start all services defined in `docker-compose.yml`:

```shell
docker compose up -d
```

Rebuild and start:

```shell
docker compose up -d --build
```

View logs for a specific service:

```shell
docker compose logs -f api
```

Stop and remove everything (containers, networks):

```shell
docker compose down
```

Stop and remove everything including volumes:

```shell
docker compose down -v
```

---

## Inspect & Debug

List running containers:

```shell
docker ps
```

List all containers (including stopped):

```shell
docker ps -a
```

View container logs:

```shell
docker logs -f --tail 100 myapp
```

Inspect a container's network, mounts, config:

```shell
docker inspect myapp
```

---

## Cleanup

Remove all stopped containers:

```shell
docker container prune
```

Remove all unused images:

```shell
docker image prune -a
```

Nuclear option — reclaim all unused space:

```shell
docker system prune -a --volumes
```

!!! warning
    `docker system prune -a --volumes` removes **all** unused images, containers, networks, and volumes. Make sure you don't need any of them.

Show disk usage:

```shell
docker system df
```

---

## Podman (Rootless Alternative)

Most Docker commands work identically with `podman`:

```shell
podman build -t myapp .
podman run -it -p 3000:3000 myapp
podman compose up -d
```

> Install: `brew install podman` · `apt install podman` · `winget install RedHat.Podman`
