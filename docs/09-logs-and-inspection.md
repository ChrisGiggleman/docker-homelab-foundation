# 09 - Logs and Inspection

## Log Commands

```powershell
docker logs nginx-compose-test
docker logs --tail 20 nginx-compose-test
```

The logs showed:

- Nginx initialization
- worker process startup
- the Curl request from the second container
- the deliberate SIGQUIT shutdown
- automatic restart and fresh Nginx startup

## Container Inspection

```powershell
docker inspect nginx-compose-test
```

Important values observed:

```text
State.Status: running
RestartCount: 1
NetworkMode: nginx-test_default
RestartPolicy: unless-stopped
HostPort: 8081
ContainerPort: 80
```

The mount configuration showed:

```text
Source:
C:\Docker-Lab\nginx-test\html

Destination:
/usr/share/nginx/html

Mode:
read-only
```

## Targeted Inspection

Examples:

```powershell
docker inspect nginx-compose-test --format '{{.State.Status}}'
docker inspect nginx-compose-test --format '{{.HostConfig.RestartPolicy.Name}}'
docker inspect nginx-compose-test --format '{{.RestartCount}}'
docker inspect nginx-compose-test --format '{{json .Mounts}}'
```

## Resource Monitoring

```powershell
docker stats
```

This provided live CPU, RAM, network, block I/O, and process usage for each container.
