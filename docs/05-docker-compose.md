# 05 - Docker Compose

## Working Directory

```powershell
mkdir C:\Docker-Lab
cd C:\Docker-Lab
mkdir nginx-test
cd nginx-test
```

## Initial Compose File

```yaml
services:
  nginx:
    image: nginx:latest
    container_name: nginx-compose-test
    ports:
      - "8081:80"
    restart: unless-stopped
```

The stack was launched with:

```powershell
docker compose up -d
```

Verification:

```powershell
docker compose ps
docker ps
```

## Result

Docker Compose created:

- the Nginx container
- the Compose default bridge network
- the requested host-to-container port mapping

The same Nginx page was reachable at:

```text
http://192.168.0.181:8081
```

## Why Compose Matters

Compose stores desired state in a file, making services easier to reproduce, review, version, and redeploy than long one-off `docker run` commands.
