# 10 - Resource Management

## Docker Capacity

```powershell
docker info | Select-String "CPUs|Total Memory"
```

Observed:

```text
CPUs: 4
Total Memory: 3.716 GiB
```

## Ubuntu / WSL View

```powershell
wsl -d Ubuntu free -h
```

Observed approximately:

```text
Mem total:      3.7 GiB
Mem available:  2.9 GiB
Swap:           1.0 GiB
```

## WSL Configuration

```powershell
Test-Path "$env:USERPROFILE\.wslconfig"
```

Result:

```text
False
```

No custom `.wslconfig` existed, so the default WSL resource configuration was retained.

## Container Usage During Testing

Approximate observed usage:

```text
docker-network-test   ~340 KiB RAM
nginx-compose-test    ~5 MiB RAM
CPU                   ~0%
```

## Decision

No additional WSL/Docker resource cap was added during the foundation lab because the current Docker workload was extremely light.

This will be reevaluated as heavier services are added, particularly Wazuh.
