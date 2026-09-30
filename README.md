# Docker Homelab Foundation

A hands-on Docker homelab project built on a GEEKOM Air12 Lite running Windows 11 Pro.

The goal of this project was to establish a reliable container platform for future self-hosted services including Nginx Proxy Manager, Uptime Kuma, Vaultwarden, and Wazuh.

## Project Goals

- Install and validate WSL2 and Ubuntu
- Install Docker Desktop using the WSL2 backend
- Verify Docker CLI and Docker Compose
- Deploy and manage Linux containers
- Practice port mapping and container lifecycle management
- Deploy services with Docker Compose
- Configure persistent storage with bind mounts
- Validate Docker bridge networking and service-name DNS
- Configure and test restart policies
- Practice container logs, inspection, and resource monitoring
- Perform final HTTP service validation

## Skills Demonstrated

- Windows 11 and WSL2 administration
- Docker Desktop installation and configuration
- Linux container deployment
- Docker Compose
- Port mapping
- Bind mounts and persistent storage
- Docker bridge networking
- Container DNS/service discovery
- Restart policies
- Container logging and inspection
- Resource monitoring
- Basic HTTP service validation
- Troubleshooting Docker CLI access and browser caching

## Lab Environment

| Component | Configuration |
|---|---|
| Host | GEEKOM Air12 Lite |
| CPU | Intel N150, 4 cores / 4 threads |
| RAM | 8 GB |
| OS | Windows 11 Pro |
| Virtualization | Enabled in firmware |
| WSL | WSL2 with Ubuntu |
| Docker | Docker Desktop using WSL2 backend |
| Host LAN IP | `192.168.0.181` |
| Existing platform | AMP game server platform |
| Test web service | Nginx |
| Test host port | `8081` |

## Architecture

```text
GEEKOM Air12 Lite
192.168.0.181
│
├── Windows 11 Pro
│
├── AMP
│   └── Existing game servers
│
└── WSL2
    └── Docker Desktop
        │
        ├── nginx-compose-test
        │   ├── nginx:latest
        │   ├── Host port 8081 -> Container port 80
        │   └── Bind mount:
        │       C:\Docker-Lab\nginx-test\html
        │       -> /usr/share/nginx/html
        │
        └── docker-network-test
            ├── curlimages/curl:latest
            └── Internal DNS test using http://nginx
```

## Key Validation Results

### Docker Engine

The first validation container completed successfully:

```powershell
docker run hello-world
```

Result:

```text
Hello from Docker!
```

### Docker Compose

Compose was validated with:

```powershell
docker compose version
```

The lab then recreated the Nginx service using `compose.yaml` rather than a long `docker run` command.

### Persistent Storage

A host bind mount was configured:

```yaml
volumes:
  - ./html:/usr/share/nginx/html:ro
```

The container was removed and recreated with:

```powershell
docker compose down
docker compose up -d
```

The custom web page remained available after recreation, proving the content was stored outside the disposable container layer.

### Container Networking

A second container was added to the same Compose project. Container-to-container communication was tested with:

```powershell
docker exec docker-network-test curl http://nginx
```

The request successfully returned the custom Nginx page by service name, demonstrating Docker's internal DNS and bridge networking.

### Restart Policy

Both test containers were configured with:

```yaml
restart: unless-stopped
```

The Nginx process was deliberately stopped inside the container:

```powershell
docker exec nginx-compose-test nginx -s quit
```

Docker automatically restarted the container. The restart counter changed from `0` to `1`.

### Logs and Inspection

Common troubleshooting commands practiced included:

```powershell
docker logs nginx-compose-test
docker logs --tail 20 nginx-compose-test
docker inspect nginx-compose-test
docker stats
```

The inspection output confirmed:

- container state: running
- restart policy: `unless-stopped`
- restart count: `1`
- network: `nginx-test_default`
- bind mount source: `C:\Docker-Lab\nginx-test\html`
- bind mount destination: `/usr/share/nginx/html`
- host port `8081` mapped to container port `80`

### Resource Usage

The test containers used very little memory:

```text
docker-network-test   ~340 KiB
nginx-compose-test    ~5 MiB
```

Docker/WSL reported approximately:

```text
CPUs: 4
Total Memory: ~3.7 GiB
```

No custom `.wslconfig` was present, so the default WSL resource configuration was retained.

### Final HTTP Validation

The final validation used PowerShell:

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

## Repository Structure

```text
docker-homelab-foundation/
│
├── README.md
├── docs/
│   ├── 01-host-inventory.md
│   ├── 02-wsl2-setup.md
│   ├── 03-docker-installation.md
│   ├── 04-container-basics.md
│   ├── 05-docker-compose.md
│   ├── 06-persistent-storage.md
│   ├── 07-docker-networking.md
│   ├── 08-restart-policies.md
│   ├── 09-logs-and-inspection.md
│   ├── 10-resource-management.md
│   └── 11-final-validation.md
├── compose/
│   └── nginx-test/
│       ├── compose.yaml
│       └── html/
│           └── index.html
├── screenshots/
└── lessons-learned.md
```

## Future Expansion

This Docker foundation will support future homelab projects including:

- Nginx Proxy Manager
- Uptime Kuma
- Vaultwarden
- Wazuh
- Future monitoring and security tooling

## Status

**Project 1 - Docker Foundation: Complete**
