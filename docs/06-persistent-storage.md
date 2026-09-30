# 06 - Persistent Storage

## Goal

Demonstrate that application content can survive container deletion and recreation.

## Host Content Directory

```powershell
mkdir html
notepad .\html\index.html
```

The custom page contained:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Docker Homelab</title>
</head>
<body>
    <h1>Docker Homelab is Working</h1>
    <p>This page is being served from persistent storage on the GEEKOM homelab server.</p>
</body>
</html>
```

## Bind Mount

The Compose file was updated with:

```yaml
volumes:
  - ./html:/usr/share/nginx/html:ro
```

This mapped:

```text
C:\Docker-Lab\nginx-test\html
        ->
/usr/share/nginx/html
```

The `:ro` option mounted the host content read-only inside the container.

## Validation

The mount was verified with:

```powershell
docker exec nginx-compose-test ls -l /usr/share/nginx/html
docker exec nginx-compose-test cat /usr/share/nginx/html/index.html
```

The container showed the same custom HTML stored on the Windows host.

## Persistence Test

```powershell
docker compose down
docker ps -a
docker compose up -d
docker compose ps
```

After the Nginx container was removed and recreated, the custom page was still present.

## Troubleshooting Note

The browser initially continued displaying the default Nginx page even though the bind mount was correct. Inspection inside the container proved the custom file was mounted properly. Opening the page in another browser confirmed the issue was browser cache rather than Docker configuration.
