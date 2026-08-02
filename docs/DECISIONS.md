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

---

# Decision 010 - Docker Architecture

## Decision

Homelab V2 will follow a modular Docker architecture.

Services are grouped into independent stacks rather than maintaining one large Docker Compose file.

Each stack contains its own Compose file, environment file and documentation.

Example structure:

/opt/docker/stacks/

- infrastructure/
- media/
- smart-home/
- storage/
- monitoring/

Each stack contains:

- compose.yaml
- .env
- README.md

---

## Design Principles

- One logical Compose file per stack.
- One configuration directory per application.
- Shared data remains outside containers.
- Containers are replaceable.
- User data is independent of applications.

---

## Reason

Grouping services by function improves maintainability, simplifies troubleshooting and allows individual stacks to be deployed, upgraded or migrated independently.

The architecture also scales naturally as additional services are introduced.

---

# Decision 011 - Backup & Disaster Recovery

## Decision

Homelab V2 follows a tiered backup strategy based on the value and recoverability of data.

### Tier 0

Operating System

The operating system is considered disposable.

Recovery is achieved through a fresh installation followed by infrastructure restoration.

---

### Tier 1

Infrastructure

Includes:

- Docker Compose files
- Container configurations
- Homepage
- Home Assistant configuration
- Scripts
- Environment templates

Daily backup.

Retain the two most recent versions.

---

### Tier 2

Personal Data

Includes:

- Nextcloud files
- Personal documents
- Photos

Protected independently and intended for future expansion to a NAS.

---

### Tier 3

Reproducible Media

Includes:

- Movies
- TV Shows
- Music

No backup is maintained.

Media can be downloaded again if required.

---

## Recovery Goals

- Docker container failure: Restore in minutes.
- SSD failure: Restore infrastructure within one hour.
- HDD failure: Replace storage and rebuild media library.
- Operating system failure: Fresh installation followed by infrastructure restoration.

---

## Reason

Backup resources should be focused on data that is expensive or impossible to recreate.

Media libraries are replaceable, whereas infrastructure configuration is not.

---

# Decision 012 - Infrastructure as Code

## Decision

The GitHub repository is the primary source of truth for Homelab V2.

The running server is considered a deployed instance of the repository.

---

## Repository Responsibilities

The repository contains:

- Documentation
- Docker Compose files
- Bootstrap scripts
- Homepage configuration
- Templates
- Automation scripts

The repository does not contain:

- Media
- Downloads
- Databases
- Personal files
- Docker volumes

---

## Update Strategy

The repository is updated whenever infrastructure changes occur.

Examples include:

- New services
- Configuration changes
- Compose updates
- Homepage modifications
- Architectural decisions

Routine scheduled commits are intentionally avoided.

---

## Disaster Recovery

Recovery procedure:

1. Install Debian.
2. Clone the repository.
3. Run bootstrap automation.
4. Restore infrastructure backup.
5. Start Docker stacks.

---

## Reason

Treating infrastructure as code ensures every configuration change is version controlled, documented and reproducible.

The repository becomes both documentation and the deployment blueprint for future hardware.

# Project Decision Status

## Completed

- Project philosophy
- Documentation strategy
- Operating system (Preferred: Debian 13 + Xfce)
- Display server (X11)
- Container platform (Docker Engine)
- Storage philosophy
- Server philosophy
- Storage & directory architecture
- Docker architecture
- Backup & disaster recovery
- Infrastructure as Code (GitHub-first)

## Pending

- Network architecture
- Monitoring & alerting
- Installation blueprint
- Bootstrap automation
