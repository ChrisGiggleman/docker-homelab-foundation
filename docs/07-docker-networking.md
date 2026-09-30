# 07 - Docker Networking

## Default Compose Network

Docker Compose automatically created:

```text
nginx-test_default
```

Inspection showed a bridge network using the `172.18.0.0/16` subnet.

The Nginx container received an internal Docker address on that network.

## Second Container

A Curl test service was added:

```yaml
tester:
  image: curlimages/curl:latest
  container_name: docker-network-test
  command: ["sleep", "infinity"]
  restart: unless-stopped
```

## Service Name DNS Test

From the tester container:

```powershell
docker exec docker-network-test curl http://nginx
```

The request successfully returned the custom Nginx page.

## Key Lesson

Containers on the same Compose network can communicate using service names rather than hard-coded container IP addresses.

```text
docker-network-test
        |
        |  http://nginx
        v
Docker internal DNS
        |
        v
nginx service
```

This is important for future multi-container applications.
