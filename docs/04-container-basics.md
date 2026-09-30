# 04 - Container Basics

## First Persistent Service

A basic Nginx container was launched with:

```powershell
docker run -d --name docker-test -p 8081:80 nginx
```

### Command Breakdown

```text
docker run
    Create and start a container

-d
    Run in detached/background mode

--name docker-test
    Assign a friendly container name

-p 8081:80
    Map host port 8081 to container port 80

nginx
    Use the nginx image
```

The test site was accessed at:

```text
http://192.168.0.181:8081
```

## Lifecycle Management

Commands practiced:

```powershell
docker ps
docker ps -a
docker stop docker-test
docker start docker-test
docker rm docker-test
docker images
```

## Key Lesson

Stopping a container does not delete it.

Removing a container deletes the container instance, but the downloaded image remains available until the image itself is removed.
