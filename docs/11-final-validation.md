# 11 - Final Validation

## Compose Status

```powershell
docker compose ps
```

Both lab containers were running.

## Network Status

```powershell
docker network ls
```

The Compose bridge network remained present and active.

## One-Shot Resource Check

```powershell
docker stats --no-stream
```

Resource use remained minimal.

## HTTP Validation

The final web service test used:

```powershell
Invoke-WebRequest http://192.168.0.181:8081/index.html -UseBasicParsing
```

Result:

```text
StatusCode        : 200
StatusDescription : OK
```

The response content included:

```text
Docker Homelab is Working
```

## Final Result

The Docker foundation lab successfully demonstrated:

- working WSL2 + Ubuntu
- working Docker Desktop engine
- Docker CLI and Compose
- image pulls and container execution
- port publishing
- container lifecycle management
- Docker Compose deployment
- persistent host bind mounts
- container-to-container networking
- Docker service-name DNS
- automatic restart policies
- log and inspection workflows
- resource monitoring
- HTTP service validation

**Project status: Complete**
