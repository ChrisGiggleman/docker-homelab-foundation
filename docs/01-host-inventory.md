# 01 - Host Inventory

## Host

- **System:** GEEKOM Air12 Lite
- **OS:** Windows 11 Pro
- **CPU:** Intel N150
- **CPU topology:** 4 cores / 4 logical processors
- **RAM:** approximately 8 GB
- **Primary LAN IP:** `192.168.0.181`
- **Ethernet:** Gigabit
- **Existing platform:** AMP game server platform

## Virtualization

The host inventory confirmed:

- VM Monitor Mode Extensions: supported
- Virtualization enabled in firmware
- Second Level Address Translation: supported
- Data Execution Prevention: supported

This meant no BIOS virtualization change was required before installing WSL2 and Docker.

## Storage

The primary Windows volume had sufficient free space for the Docker foundation lab and future lightweight services.

## Existing Port Awareness

The host already had services listening on ports used by AMP and game servers, including:

- `8080` - AMP web interface
- `25565` - Minecraft
- additional AMP/game service ports

To avoid collisions, the Docker Nginx test used host port `8081`.

## Design Decision

The host's DHCP reservation had already been configured on the router during the earlier AMP setup, so the Docker lab could safely rely on `192.168.0.181` remaining stable.
