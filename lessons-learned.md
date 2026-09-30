# Lessons Learned

## 1. Docker Desktop Can Be Running While the CLI Is Not Immediately Available

Docker Desktop showed that the engine was running, but PowerShell initially could not resolve the `docker` command.

### Lesson

When Docker Desktop appears healthy but the CLI is unavailable, verify the installation path and refresh the shell/environment before assuming the Docker engine itself is broken.

---

## 2. Avoid Port Collisions on Shared Homelab Hosts

The GEEKOM already hosts AMP and game servers. Port `8080` was already in use by AMP, so Nginx was published on `8081`.

### Lesson

Inventory existing listeners before deploying new containers.

---

## 3. Containers Are Disposable; Data Should Not Be

The Nginx container was removed and recreated while the custom page remained because the content was stored on the host through a bind mount.

### Lesson

Application state should live in persistent storage rather than only inside the container filesystem.

---

## 4. Browser Cache Can Look Like a Container Problem

After adding the bind mount, one browser continued showing the default Nginx page. Container inspection proved the correct file was mounted and readable. The site displayed correctly in another browser.

### Lesson

Verify the service from multiple layers before changing a working Docker configuration:

1. verify the host file
2. verify the Compose configuration
3. inspect the mount
4. read the file inside the container
5. test from another client/browser

---

## 5. Docker Service Names Are Better Than Hard-Coded Container IPs

The Curl container reached Nginx using:

```text
http://nginx
```

rather than the internal `172.18.x.x` address.

### Lesson

Use Docker DNS/service discovery for communication between containers on the same Compose network.

---

## 6. Restart Policies Provide Basic Service Resilience

After the Nginx process was intentionally terminated, Docker automatically restarted the container because of:

```yaml
restart: unless-stopped
```

The restart count increased from `0` to `1`.

### Lesson

Restart policies are an important baseline for long-running homelab services.

---

## 7. Logs, Inspect, and Stats Serve Different Troubleshooting Purposes

- `docker logs` shows application/container output
- `docker inspect` shows configuration and runtime state
- `docker stats` shows resource consumption

### Lesson

Use the smallest diagnostic tool that answers the current question instead of relying only on the Docker Desktop GUI.

---

## 8. Resource Planning Matters on a Shared 8 GB Host

The test containers used very little memory, but the host also runs AMP and game servers.

### Lesson

Continue monitoring memory as additional services are deployed. Lightweight services are appropriate now, while heavier platforms such as Wazuh should be evaluated carefully before installation.
