# 02 - WSL2 Setup

## Installation

WSL was installed from an elevated PowerShell session:

```powershell
wsl --install
```

After rebooting, WSL reported:

```text
WSL version: 3.0.1.0
Default Version: 2
```

Ubuntu was then installed:

```powershell
wsl --install -d Ubuntu
```

A Linux username and password were created during the first-run setup.

## Verification

```powershell
wsl --list --verbose
```

Ubuntu was confirmed as:

```text
Ubuntu    Running    2
```

The important result was **VERSION 2**, confirming WSL2 rather than WSL1.

## Notes

An Ubuntu platform metrics opt-in prompt appeared during setup. Metrics collection was declined because it was not required for the lab.
