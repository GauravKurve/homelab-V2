# Homelab V2

A complete redesign of my self-hosted homelab built around simplicity, reliability and Infrastructure as Code.

Rather than upgrading an existing installation, Homelab V2 is being rebuilt from the ground up using a clean architecture, modular Docker stacks and a documented design process.

The goal is to build a lightweight, maintainable and easily recoverable home server that can evolve with future hardware.

---

# Project Status

| Property | Value |
|----------|-------|
| Version | v2.0.0-alpha |
| Status | 🟡 Architecture Complete |
| Current Phase | Infrastructure Bootstrap |
| Next Milestone | Debian Installation |

---

# Objectives

- Stable 24/7 operation
- Lightweight and reliable operating system
- Docker-first architecture
- Modular service deployment
- Clean storage organization
- Infrastructure as Code
- Fast disaster recovery
- Easy migration to future hardware
- Well-documented design decisions

---

# Hardware

| Component | Specification |
|-----------|---------------|
| Laptop | Lenovo G50-45 |
| CPU | AMD A8-6410 (4 Cores) |
| Memory | 8 GB DDR3 |
| Primary Storage | 500 GB SSD |
| Secondary Storage | 1 TB HDD |
| Graphics | AMD Radeon R5 + Radeon R5 M230 |

Detailed hardware specifications are available in **docs/HARDWARE.md**.

---

# Planned Service Architecture

## Infrastructure

- Docker Engine
- Dockge
- Homepage
- Tailscale
- NoMachine

## Media

- Jellyfin
- Navidrome
- Sonarr
- Radarr
- Lidarr
- Prowlarr
- qBittorrent

## Storage

- Nextcloud

## Smart Home

- Home Assistant
- Matter Server

## Monitoring

- Uptime Kuma
- Lightweight System Monitoring
- Notifications

---

# Storage Architecture

## SSD (500 GB)

- Debian Operating System
- Docker Engine
- Docker AppData
- Active Downloads
- Infrastructure

## HDD (1 TB)

- Movies
- TV Shows
- Music
- Personal Files
- Infrastructure Backups

Downloads are stored on the SSD for performance and automatically moved to the HDD after processing.

---

# Architecture Principles

Homelab V2 follows several core principles.

- Design before implementation.
- Infrastructure as Code.
- Containers never own user data.
- Services are grouped into independent Docker stacks.
- Only irreplaceable data is backed up.
- The operating system is disposable.
- Keep the system simple.
- Build for future migration.

---

# Documentation

| Document | Purpose |
|----------|---------|
| docs/HARDWARE.md | Hardware inventory |
| docs/DECISIONS.md | Architecture Decision Records |
| docs/ARCHITECTURE.md | System architecture and diagrams |
| BUILD.md | Build and deployment plan |

---

# Repository Structure

```text
homelab-V2/

├── README.md
├── BUILD.md
├── docs/
├── compose/
├── scripts/
├── bootstrap/
├── templates/
├── diagrams/
└── .github/
```

---

# Roadmap

## ✅ Completed

- Hardware Audit
- Requirements Analysis
- Operating System Selection
- Storage Architecture
- Docker Architecture
- Backup Strategy
- Infrastructure as Code
- Build Planning
- Repository Structure

## 🚧 In Progress

- Infrastructure Bootstrap

## 📋 Upcoming

- Debian Installation
- Base System Configuration
- Docker Platform
- Infrastructure Stack
- Media Stack
- Storage Stack
- Smart Home Stack
- Monitoring Stack
- Backup Validation
- Production Release (v2.0.0)

---

# Design Philosophy

Homelab V2 is not just a server.

It is an engineering project where every architectural decision is documented, version-controlled and reproducible.

The GitHub repository is the source of truth, while the running server is considered a deployed instance of that repository.

---

# License

This repository is maintained as a personal homelab project, learning resource and long-term infrastructure blueprint.
