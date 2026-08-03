# Homelab v2 Migration Guide

> **Project Goal**
>
> Build a clean, documented, maintainable homelab from scratch on the new SSD. Only migrate important data and configurations—not years of accumulated system changes.

---

# Project Overview

## Current Hardware

### Server
- Laptop: Lenovo IdeaPad 80E3
- RAM:
- CPU:
- SSD: 500 GB (System + Docker + Downloads)
- HDD: 1 TB (Media Library)

### Client Devices
- Windows PC
- Fire TV Stick
- Android Phone
- Other:

---

# Target Architecture

## SSD

```
/
├── Ubuntu
├── Docker
├── /home/gaurav
│   ├── homelab
│   └── Downloads
```

---

## HDD

```
/media
├── Movies
├── TV Shows
├── Music
├── Photos
├── Anime
└── Other Media
```

---

# Directory Structure

```
~/homelab
│
├── compose/
│
├── config/
│   ├── jellyfin/
│   ├── qbittorrent/
│   ├── sonarr/
│   ├── radarr/
│   ├── lidarr/
│   ├── bazarr/
│   ├── prowlarr/
│   ├── homepage/
│   ├── homeassistant/
│   ├── navidrome/
│   ├── nextcloud/
│   ├── uptime-kuma/
│   └── netdata/
│
├── media/
│
├── downloads/
│
├── backups/
│
├── scripts/
│
├── docs/
│
├── .env
│
├── docker-compose.yml
│
└── README.md
```

---

# Services

## Media

- [ ] Jellyfin
- [ ] qBittorrent
- [ ] Sonarr
- [ ] Radarr
- [ ] Lidarr
- [ ] Bazarr
- [ ] Prowlarr
- [ ] FlareSolverr
- [ ] Navidrome

---

## Infrastructure

- [ ] Homepage
- [ ] Uptime Kuma
- [ ] Netdata

---

## Smart Home

- [ ] Home Assistant
- [ ] Matter Server

---

## Cloud

- [ ] Nextcloud
- [ ] MariaDB

---

# Base System

- [ ] Ubuntu Installed
- [ ] SSD Optimized
- [ ] Docker Installed
- [ ] Docker Compose Installed
- [ ] SSH Configured
- [ ] SSH Keys Installed
- [ ] VS Code Remote SSH
- [ ] Tailscale Installed
- [ ] UFW Configured

---

# Remote Access

## Keep

- [ ] SSH
- [ ] VS Code Remote SSH
- [ ] NoMachine (Optional)

## Do NOT Reinstall

- [ ] TigerVNC
- [ ] XRDP

---

# Data to Preserve

## Jellyfin

- [ ] Library
- [ ] Metadata
- [ ] Watch History
- [ ] Users
- [ ] Collections
- [ ] Plugins

---

## qBittorrent

- [ ] Configuration
- [ ] Torrent List
- [ ] Categories
- [ ] Resume Data
- [ ] Fast Resume Files

---

## Sonarr

- [ ] Configuration
- [ ] Indexers
- [ ] Download Client
- [ ] Root Folders

---

## Radarr

- [ ] Configuration
- [ ] Movies
- [ ] Quality Profiles

---

## Lidarr

- [ ] Configuration

---

## Bazarr

- [ ] Configuration

---

## Prowlarr

- [ ] Indexers

---

## Homepage

- [ ] Services
- [ ] Widgets
- [ ] Icons
- [ ] Bookmarks

---

## Home Assistant

- [ ] configuration.yaml
- [ ] Automations
- [ ] Integrations
- [ ] Backups

---

## Nextcloud

- [ ] Database
- [ ] User Data
- [ ] Configuration

---

## Navidrome

- [ ] Configuration

---

# Docker

Backup:

- [ ] docker-compose.yml
- [ ] .env
- [ ] Config Folders
- [ ] Docker Volumes
- [ ] Networks (if required)

---

# Scripts

Move to

```
~/homelab/scripts/
```

Scripts

- [ ] update-containers.sh
- [ ] backup.sh
- [ ] restore.sh
- [ ] cleanup.sh
- [ ] healthcheck.sh
- [ ] notifications.sh

---

# Documentation

Create

```
~/homelab/docs/
```

Documents

- [ ] README.md
- [ ] Network Diagram
- [ ] Docker Architecture
- [ ] Backup Guide
- [ ] Restore Guide
- [ ] Storage Layout
- [ ] Service Documentation
- [ ] Troubleshooting
- [ ] Port Reference

---

# Backup Checklist

## Verify

- [ ] Docker Configs
- [ ] Docker Volumes
- [ ] Jellyfin Metadata
- [ ] qBittorrent Resume Data
- [ ] Homepage Config
- [ ] Home Assistant Backup
- [ ] Nextcloud Database
- [ ] Media Paths
- [ ] Scripts
- [ ] SSH Keys

---

# Migration Checklist

## Before Installation

- [ ] Backup Verified
- [ ] SSD Installed
- [ ] HDD Verified
- [ ] Installation Media Ready

---

## After Ubuntu Installation

- [ ] Updates Installed
- [ ] SSH Working
- [ ] VS Code Remote SSH Working
- [ ] Tailscale Connected
- [ ] Docker Installed
- [ ] Docker Compose Installed

---

## Restore

- [ ] Copy Homelab Folder
- [ ] Restore Configurations
- [ ] Restore Docker Volumes
- [ ] Restore Databases
- [ ] Restore Media Mounts

---

## Verification

- [ ] Homepage Opens
- [ ] Jellyfin Works
- [ ] Watch History Preserved
- [ ] qBittorrent Resumes Torrents
- [ ] Sonarr Working
- [ ] Radarr Working
- [ ] Lidarr Working
- [ ] Bazarr Working
- [ ] Prowlarr Working
- [ ] Navidrome Working
- [ ] Home Assistant Working
- [ ] Nextcloud Working
- [ ] Uptime Kuma Working
- [ ] Netdata Working

---

# Improvements for Homelab v2

- [ ] Single Docker Compose Project
- [ ] Clean Folder Structure
- [ ] Named Docker Volumes
- [ ] Automatic Backups
- [ ] Health Monitoring
- [ ] Update Automation
- [ ] Documentation
- [ ] Notification System
- [ ] Git Repository
- [ ] Disaster Recovery Guide

---

# Things NOT to Migrate

- [ ] Native Jellyfin Installation
- [ ] Native qBittorrent Installation
- [ ] Old Docker Compose Project
- [ ] Anonymous Docker Volumes
- [ ] TigerVNC
- [ ] XRDP
- [ ] Old Experimental Files
- [ ] Obsolete Configurations

---

# Future Ideas

- [ ] Immich
- [ ] Paperless-ngx
- [ ] Grafana
- [ ] Prometheus
- [ ] Portainer
- [ ] Cloudflare Tunnel
- [ ] Automated Backups to External Drive
- [ ] WhatsApp/Telegram Notifications
- [ ] AI Assistant for Homelab
- [ ] UPS Integration

---

# Notes

Use this section to record decisions, observations, and lessons learned during the migration.

---

_Last Updated:_
_Date:_

_Status:_ Planning