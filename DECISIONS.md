# Architecture Decisions

This document records the major design decisions made during the development of Homelab V2.

The purpose is to explain **why** a decision was made, not simply **what** was installed.

---

# Decision 001 - Project Philosophy

## Decision

Homelab V2 will be built using a **design-first** approach.

## Reason

The previous homelab evolved organically over time.

While functional, the architecture became increasingly difficult to understand and maintain.

Homelab V2 prioritizes planning before implementation.

Every major architectural decision is documented before installation begins.

---

# Decision 002 - Documentation Strategy

## Decision

Document decisions instead of implementation steps.

## Reason

Commands can always be reproduced.

The reasoning behind architectural decisions is much more valuable in the long term.

Documentation should remain concise and useful instead of becoming a step-by-step installation guide.

---

# Decision 003 - Operating System

## Current Decision

Debian 13 with Xfce Desktop

**Status:** Status: Preferred (Final validation during installation)

## Requirements

The operating system must provide:

- Long-term stability
- Lightweight desktop environment
- Excellent Docker compatibility
- Reliable remote administration
- Low resource usage
- Strong Linux community support

## Alternatives Considered

### Linux Mint

Advantages

- Familiar desktop
- Excellent hardware support
- Beginner friendly

Reason not selected

Although Linux Mint remains an excellent distribution, Debian provides a cleaner foundation for a dedicated home server while still supporting a lightweight desktop environment.

---

### Fedora

Advantages

- Latest kernel
- Latest desktop technologies
- Excellent Wayland support

Reason not selected

The faster release cycle introduces more maintenance than desired for a 24/7 home server.

---

# Decision 004 - Display Server

## Current Decision

X11

**Status:** Selected

## Reason

The primary goals are stability and compatibility.

Current remote access tools (NoMachine) and existing hardware are well supported under X11.

Wayland will be revisited when future hardware is introduced.

---

# Decision 005 - Container Platform

## Current Decision

Docker Engine

**Status:** Selected

## Reason

The existing homelab already uses Docker successfully.

Remaining within the Docker ecosystem minimizes migration effort while maintaining excellent compatibility with the required services.

Container management will remain Compose-first.

---

# Decision 006 - Container Management

## Current Decision

Dockge

**Status:** Under Evaluation

## Reason

A lightweight management interface is preferred.

The management solution should preserve Docker Compose files rather than hiding them behind a database.

---

# Decision 007 - Storage Philosophy

## Decision

SSD

- Operating System
- Docker Engine
- Container Configurations
- Downloads

HDD

- Movies
- TV Shows
- Music
- Photos
- Backups

## Reason

Downloads benefit from SSD performance.

Completed media is automatically transferred to the HDD where large storage capacity is more important than performance.

---

# Decision 008 - Server Philosophy

## Decision

The laptop is treated as a dedicated home server rather than a personal laptop.

## Reason

The machine does not support Wake-on-LAN or Wake-on-WiFi.

The preferred operational model is continuous uptime.

Power management will therefore prioritize reliability over aggressive sleep or shutdown behaviour.

---

---

# Decision 009 - Storage & Directory Architecture

## Decision

The storage layout will be designed around the role of each drive rather than treating all storage equally.

### SSD (Performance Tier)

The SSD will be dedicated to active workloads.

```
/
└── opt
    └── docker
        ├── compose
        ├── appdata
        ├── scripts
        └── backups

/srv
└── downloads
    ├── incomplete
    ├── complete
    ├── watch
    └── manual
```

Primary responsibilities

- Operating System
- Docker Engine
- Docker Compose files
- Container configuration
- Downloads
- Temporary working data

---

### HDD (Storage Tier)

The HDD will be dedicated to long-term storage.

```
/srv
├── media
│   ├── Movies
│   ├── TV
│   ├── Music
│   ├── Photos
│   └── Documents
│
└── backup
    ├── Docker
    ├── Compose
    ├── Configurations
    ├── Databases
    └── Nextcloud
```

Primary responsibilities

- Media Library
- Backups
- Long-term file storage

---

## Storage Workflow

```
Internet
    │
    ▼
qBittorrent
    │
    ▼
SSD Downloads
    │
    ▼
Sonarr / Radarr / Lidarr
    │
    ▼
Rename & Organize
    │
    ▼
HDD Media Library
    │
    ▼
Jellyfin Library Scan
```

---

## Design Principles

### Separate Applications from Data

Application files and user data must never be mixed.

Container configurations remain inside `/opt/docker/appdata`, while user-generated files remain under `/srv`.

---

### Predictable Layout

Every service should have an obvious location.

Examples

| Item | Location |
|-------|----------|
| Docker Compose | `/opt/docker/compose` |
| Container Configurations | `/opt/docker/appdata` |
| Downloads | `/srv/downloads` |
| Movies | `/srv/media/Movies` |
| TV Shows | `/srv/media/TV` |
| Music | `/srv/media/Music` |
| Backups | `/srv/backup` |

---

### Future Migration

The architecture is intentionally hardware-independent.

Migrating to future hardware should only require:

1. Install the operating system.
2. Install Docker.
3. Restore `/opt/docker`.
4. Restore `/srv`.
5. Start the Docker Compose stack.

---

## Reason

The previous homelab evolved organically, resulting in configuration files, downloads and application data being distributed across multiple locations.

Homelab V2 adopts a predictable, Linux-standard directory structure that improves maintainability, simplifies backups and significantly reduces migration effort.

The design also aligns with the different strengths of the available storage devices by using the SSD for performance-sensitive workloads and the HDD for long-term storage.

# Project Decision Status

## Completed

- Project philosophy
- Documentation strategy
- Operating system selection
- Display server
- Container platform
- Storage philosophy
- Server philosophy
- Storage & directory architecture

## Pending

- Docker architecture
- Backup strategy
- Monitoring stack
- Notification system
- Network architecture
