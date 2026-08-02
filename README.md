# Homelab V2

## Overview

Homelab V2 is a complete redesign of my existing Linux homelab.

Instead of migrating the current setup, this project focuses on rebuilding the homelab from scratch using a clean architecture, improved storage layout, and a modular Docker-based design.

The primary goal is to create a reliable, low-maintenance home server that can run 24/7 while remaining easy to understand, maintain, and migrate to future hardware.

---

## Project Goals

- Stable 24/7 operation
- Lightweight operating system
- Docker-first architecture
- Organized storage layout
- Simple maintenance
- Easy disaster recovery
- Easy migration to future hardware
- Clear documentation of design decisions

---

## Current Hardware

| Component | Specification |
|-----------|---------------|
| Laptop | Lenovo G50-45 |
| CPU | AMD A8-6410 (4 Cores) |
| Memory | 8 GB DDR3 |
| Storage | 500 GB SSD + 1 TB HDD |
| Graphics | AMD Radeon R5 + Radeon R5 M230 |

Detailed hardware information is available in **HARDWARE.md**.

---

## Planned Services

### Infrastructure

- Docker Engine
- Dockge
- Homepage
- Tailscale
- NoMachine

### Media

- Jellyfin
- Navidrome
- Sonarr
- Radarr
- Lidarr
- Prowlarr
- qBittorrent

### Storage

- Nextcloud

### Smart Home

- Home Assistant
- Matter Server

### Monitoring

- Uptime Kuma
- Lightweight System Monitoring

---

## Storage Philosophy

SSD

- Operating System
- Docker
- Downloads
- Container Configurations

HDD

- Movies
- TV Shows
- Music
- Photos
- Backups

Downloads will be stored on the SSD for maximum performance before being automatically moved to the HDD media library.

---

## Design Philosophy

This project follows a few core principles.

- Design before implementation.
- Document decisions instead of commands.
- Keep the system simple.
- Prefer reliability over bleeding-edge software.
- Build for easy migration to future hardware.

---

## Project Status

Current Phase:

> Planning & Architecture

Completed

- Hardware Audit
- Requirements Gathering
- Operating System Research
- Initial Project Setup

Upcoming

- Storage Architecture
- Docker Architecture
- Backup Strategy
- Fresh Installation
- Service Deployment

---

## Repository Structure

This repository will contain

README.md

HARDWARE.md

DECISIONS.md

Docker Compose files

Scripts

Architecture diagrams

Configuration examples

---

## License

This project is maintained as a personal homelab project and learning resource.
