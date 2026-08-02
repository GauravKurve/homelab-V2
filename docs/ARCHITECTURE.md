# Homelab V2 Architecture

## System Overview

```
                    Internet
                        │
                        ▼
                     Router
                        │
                ┌───────┴────────┐
                │                │
           Local Network     Tailscale
                │                │
                └───────┬────────┘
                        │
                   Debian 13
                        │
                 Docker Engine
                        │
      ┌─────────┬─────────┬─────────┬─────────┐
      │         │         │         │
Infrastructure Media  Smart Home Storage Monitoring
```

---

## Storage Layout

```
500 GB SSD
│
├── Debian OS
├── Docker
├── Downloads
└── AppData

↓

1 TB HDD
│
├── Movies
├── TV
├── Music
├── Photos
├── Documents
└── Backups
```

---

## Docker Architecture

```
Docker

├── Infrastructure
│   ├── Homepage
│   ├── Dockge
│   ├── Tailscale
│   └── NoMachine
│
├── Media
│   ├── Jellyfin
│   ├── Navidrome
│   ├── Sonarr
│   ├── Radarr
│   ├── Lidarr
│   ├── Prowlarr
│   └── qBittorrent
│
├── Smart Home
│   ├── Home Assistant
│   └── Matter
│
├── Storage
│   └── Nextcloud
│
└── Monitoring
    ├── Homepage Widgets
    └── Uptime Kuma
```

---

## Media Workflow

```
Internet
    │
    ▼
qBittorrent
    │
    ▼
Downloads (SSD)
    │
    ▼
Sonarr / Radarr / Lidarr
    │
    ▼
Automatic Rename
    │
    ▼
Media Library (HDD)
    │
    ▼
Jellyfin
```

---

## Backup Strategy

```
GitHub
│
├── Documentation
├── Compose Files
├── Scripts
└── Templates

↓

SSD
│
├── Running Infrastructure

↓

HDD
│
└── Infrastructure Backups
```

---

## Disaster Recovery

```
Install Debian

↓

Clone Repository

↓

Run bootstrap.sh

↓

Restore Infrastructure Backup

↓

docker compose up -d

↓

System Restored
```
