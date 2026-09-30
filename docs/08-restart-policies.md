# 08 - Restart Policies

## Policy

The Nginx service used:

```yaml
restart: unless-stopped
```

Verification:

```powershell
docker inspect nginx-compose-test --format '{{.HostConfig.RestartPolicy.Name}}'
```

Expected result:

```text
unless-stopped
```

The same restart policy was later added to the network test container.

## Recovery Test

The current restart count was checked:

```powershell
docker inspect nginx-compose-test --format '{{.RestartCount}}'
```

Initial result:

```text
0
```

Nginx was then gracefully terminated inside the container:

```powershell
docker exec nginx-compose-test nginx -s quit
```

Docker automatically restarted the container.

The restart count was checked again:

```text
1
```

## Key Lesson

`unless-stopped` allows Docker to recover a service after an unexpected process exit while still respecting an intentional manual stop.
