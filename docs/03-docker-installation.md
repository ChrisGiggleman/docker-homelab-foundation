# 03 - Docker Desktop Installation

## Installer

Docker Desktop for Windows x86_64 was selected because the GEEKOM uses an Intel x86-64 processor.

## Configuration

The installer was configured with:

```text
Per-user installation                 Enabled
Use WSL 2 instead of Hyper-V          Enabled
Allow Windows Containers              Disabled
Desktop shortcut                      Optional
```

Linux containers were the target for this homelab, so Windows Containers were not enabled.

## Initial CLI Issue

After installation, Docker Desktop showed **Engine running**, but PowerShell initially returned:

```text
docker : The term 'docker' is not recognized...
```

The Docker CLI became available after the environment/path state was refreshed.

## Verification

```powershell
docker --version
docker compose version
```

Docker Compose reported version `v5.5.1` during the lab.

## First Engine Test

```powershell
docker run hello-world
```

Successful result:

```text
Hello from Docker!
```

This validated:

- Docker CLI access
- Docker daemon connectivity
- Docker Hub image pull
- image extraction
- container creation
- container execution
