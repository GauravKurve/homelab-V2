============================================================
HOMELAB HEALTH CHECK
Version: 1.0
Status: IN PROGRESS
Started: 2026-08-04

============================================================
PHASE 1 - SYSTEM HEALTH
============================================================

Status:
✅ PASSED

Objective:
Verify that the operating system, hardware, storage, and base Docker platform are healthy before validating homelab services.

------------------------------------------------------------
Checks Performed
------------------------------------------------------------

Operating System
✓ Linux Mint 22.3
✓ Kernel: 6.17.0-40-generic
✓ Hostname: Gaurav-Lab

System Resources
✓ System uptime verified
✓ Memory usage normal
✓ No swap configured (intentional - review during SSD migration)
✓ Root filesystem healthy
✓ Home filesystem healthy

Storage
✓ Root partition (/dev/sda2) healthy
✓ Home partition (/dev/sda3) healthy
✓ EFI partition healthy
✓ SMART self-test: PASSED
✓ Filesystem mounts verified
✓ /etc/fstab verified (UUID based)

Hardware
✓ CPU temperature normal (~55°C)
✓ GPU temperature normal (~54°C)

Docker Foundation
✓ Docker Root Directory:
  /var/lib/docker

Filesystem Permissions
✓ /home
✓ /home/gaurav
✓ /home/gaurav/media
✓ /home/gaurav/media/downloads

------------------------------------------------------------
Observations
------------------------------------------------------------

• Temporary high CPU load observed immediately after Jellyfin migration.
• Investigation confirmed it was caused by Jellyfin library scan and Docker activity.
• CPU usage returned to normal after scan completed.

• Docker daemon healthy.
• Container runtime healthy.
• Disk I/O within expected range.

------------------------------------------------------------
Issues Found
------------------------------------------------------------

Priority: LOW

1.
Home partition currently around 80% utilized.
Approximately 120+ GB remains free.
No immediate action required.
Will be addressed during SSD migration.

2.
No swap configured.
Not considered an issue at present.
Will be reviewed during SSD migration planning.

------------------------------------------------------------
Actions Taken
------------------------------------------------------------

✓ Verified SMART health.
✓ Verified filesystem integrity.
✓ Verified Docker storage location.
✓ Verified system temperatures.
✓ Verified mount configuration.
✓ Verified permissions.

------------------------------------------------------------
Decision
------------------------------------------------------------

Phase 1 approved.

Proceed to:
PHASE 2 - Docker Platform Validation.
Status:
✅ PASSED

Objective:
Verify that the Docker Engine, Docker Compose environment, and container runtime are healthy before validating individual homelab services.

Checks Performed

Docker Platform
✓ Docker Engine version verified
✓ Docker API compatibility verified
✓ containerd version verified
✓ Docker Compose version verified

Container Runtime
✓ All expected containers running
✓ No restarting containers
✓ No unhealthy containers
✓ Restart counts verified (all containers: 0)

Container Health
✓ Jellyfin healthy
✓ Homepage healthy
✓ Netdata healthy
✓ Remaining services running normally

Docker Daemon
✓ No daemon warnings detected
✓ No daemon errors detected
✓ Runtime operating normally

Observations

• Docker Engine operating normally.
• Docker Compose functioning correctly.
• Container runtime stable.
• No crash loops detected.
• No unexpected container restarts detected.
• All monitored services remained available throughout validation.

Notes

• qBittorrent is currently outside the intended Compose-managed deployment.
• Restart policy validation was not applied to qBittorrent during this health check.
• This configuration will be reviewed during the SSD migration and Docker consolidation project.

Issues Found

None.

Actions Taken

✓ Verified Docker Engine.
✓ Verified Docker Compose.
✓ Verified running containers.
✓ Verified container health.
✓ Verified restart counts.
✓ Verified Docker daemon stability.

Decision

Phase 2 approved.

Proceed to:
PHASE 3 - STORAGE VALIDATION.
============================================================
PHASE 3 - STORAGE VALIDATION
============================

Status:
✅ PASSED

Objective:
Validate the storage layout, filesystem health, media directories, Docker bind mounts, and cache locations to ensure a reliable foundation for all homelab services.

---

## Checks Performed

Filesystem Health
✓ Root filesystem verified
✓ Home filesystem verified
✓ EFI partition verified
✓ Mount points validated
✓ Filesystem types verified

Storage Devices
✓ HDD detected and operating normally
✓ SSD detected and available for future migration
✓ Disk usage reviewed

Homelab Directory Structure
✓ Cache directory verified
✓ Compose directory verified
✓ Data directory verified
✓ Service configuration directories verified

Media Library
✓ Movies library verified
✓ Series library verified
✓ Music library verified
✓ Downloads directory verified

Docker Storage
✓ Docker bind mounts validated
✓ Jellyfin configuration directory verified
✓ Jellyfin cache separation verified
✓ Service configuration directories verified

---

## Observations

• Homelab directory structure is clean and well organized.
• Jellyfin cache has been successfully separated from configuration data.
• Media library layout is consistent across services.
• All required bind-mounted host paths exist and are accessible.
• SSD is connected and ready for the planned operating system migration.

---

## Notes

• The `jellyfin.docker-backup` directory is intentionally retained until the SSD migration has been completed and verified.

• Jellyfin currently exposes the media library through both `/home/gaurav/media` and `/media`. This is a temporary compatibility configuration and will be simplified during the SSD migration project.

• FlareSolverr and qBittorrent currently use Docker-managed named volumes for their configuration. These are operating normally and are outside the scope of this storage validation.

---

## Issues Found

None.

---

## Actions Taken

✓ Verified filesystem health.
✓ Verified storage layout.
✓ Verified Docker bind mounts.
✓ Verified media directory structure.
✓ Verified Jellyfin cache separation.
✓ Verified SSD detection for future migration.

---

## Decision

Phase 3 approved.

Proceed to:
PHASE 4 - MEDIA STACK VALIDATION.
============================================================
PHASE 4 - MEDIA STACK VALIDATION
================================

Status:
✅ PASSED

Objective:
Validate the operational health of all media services, verify media library configuration, confirm hardware acceleration availability, and ensure media storage remains accessible after the Jellyfin migration.

---

## Checks Performed

Media Services
✓ Jellyfin
✓ Sonarr
✓ Radarr
✓ Bazarr
✓ Prowlarr
✓ Lidarr
✓ qBittorrent
✓ Navidrome

Service Availability
✓ All services responding over HTTP
✓ No unhealthy containers
✓ No service startup failures

Jellyfin
✓ Database verified
✓ Configuration verified
✓ Hardware acceleration devices detected
✓ Media library accessible

Media Library
✓ Movies root folder verified
✓ Series root folder verified
✓ Music root folder verified
✓ Media directory permissions verified

Application Logs
✓ No critical service failures detected
✓ No database corruption detected
✓ No filesystem permission errors detected

---

## Observations

• Hardware acceleration devices are successfully available inside the Jellyfin container.
• Media root folders remain correctly configured after the migration.
• All media services are operational and responding normally.
• Media directory permissions are consistent.
• Minor informational log messages were observed (metadata refreshes, RSS synchronization, temporary indexer rate limiting) but no operational issues were identified.

---

## Issues Found

None requiring corrective action.

---

## Actions Taken

✓ Verified service availability.
✓ Verified HTTP responsiveness.
✓ Verified media library accessibility.
✓ Verified Jellyfin hardware acceleration.
✓ Verified root folder configuration.
✓ Reviewed application logs.

---

## Decision

Phase 4 approved.

Proceed to:
PHASE 5 - SERVICE INTEGRATION VALIDATION.
============================================================
PHASE 5 - SERVICE INTEGRATION VALIDATION
========================================

Status:
✅ PASSED

Objective:
Verify that the media ecosystem is functioning as an integrated platform and that core service APIs and storage paths remain operational.

---

## Checks Performed

Docker Networking
✓ Docker networks verified
✓ Container networking operational

Application APIs
✓ Jellyfin Public API verified
✓ Netdata API verified
✓ Homepage service reachable

Media Integration
✓ Jellyfin database accessible
✓ Media library available
✓ Movies directory verified
✓ Series directory verified
✓ Music directory verified
✓ Downloads directory verified

Media Configuration
✓ Sonarr root folder verified
✓ Radarr root folder verified
✓ Lidarr root folder verified

---

## Observations

• Jellyfin database contains the expected media records following migration.
• Netdata reports no warning or critical system alarms.
• Media libraries remain accessible to all services.
• Docker networking is operating normally.
• Application APIs are responding correctly.

---

## Issues Found

None.

---

## Actions Taken

✓ Verified Docker networking.
✓ Verified application API responses.
✓ Verified Jellyfin database accessibility.
✓ Verified media directory accessibility.
✓ Verified root folder configuration.
✓ Verified monitoring service health.

---

## Decision

Phase 5 approved.

Proceed to:
PHASE 6 - NETWORK & REMOTE ACCESS VALIDATION.
============================================================
PHASE 6 - NETWORK & REMOTE ACCESS VALIDATION
============================================

Status:
✅ PASSED

Objective:
Validate local networking, remote access services, network connectivity, time synchronization, and remote management components to ensure reliable access to the homelab.

---

## Checks Performed

Host Identity
✓ Hostname verified
✓ LAN IP address verified
✓ Tailscale IPv4 address verified
✓ Tailscale IPv6 address verified

Network Services
✓ SSH service listening
✓ Jellyfin service listening
✓ Sonarr service listening
✓ Radarr service listening
✓ Bazarr service listening
✓ Prowlarr service listening
✓ Lidarr service listening
✓ Navidrome service listening
✓ Netdata service listening
✓ Uptime Kuma service listening

Remote Access
✓ Tailscale connectivity verified
✓ NoMachine service verified
✓ Home Assistant service verified

Time Synchronization
✓ System clock synchronized
✓ NTP service active
✓ Timezone correctly configured (Asia/Kolkata)

---

## Observations

• All expected network services are listening on their designated ports.
• Tailscale successfully established IPv4 and IPv6 connectivity.
• UDP traversal, UPnP, and NAT-PMP are functioning correctly.
• Nearest Tailscale DERP relay is Bengaluru with excellent latency.
• NoMachine has remained continuously operational throughout the validation period.
• Home Assistant is reachable and responding normally.
• System time synchronization is healthy.

---

## Informational Notes

• Tailscale reported a DNS server health warning during validation.
• A subsequent network diagnostic confirmed successful UDP connectivity, port mapping, DERP connectivity, and Internet reachability.
• The DNS warning has been classified as informational and will be reviewed during the future network configuration audit.

---

## Issues Found

None requiring corrective action.

---

## Actions Taken

✓ Verified network identity.
✓ Verified listening services.
✓ Verified SSH accessibility.
✓ Verified Tailscale connectivity.
✓ Verified NoMachine operation.
✓ Verified Home Assistant availability.
✓ Verified system time synchronization.

---

## Decision

Phase 6 approved.

Proceed to:
PHASE 7 - MONITORING & ALERTING VALIDATION.
============================================================
PHASE 7 - MONITORING & ALERTING VALIDATION
==========================================

Status:
✅ PASSED

Objective:
Validate that monitoring services, health checks, system logging, and hardware health monitoring are functioning correctly.

---

## Checks Performed

Monitoring Services
✓ Netdata API verified
✓ Uptime Kuma verified

Container Health
✓ Docker health checks verified
✓ All monitored containers healthy

System Health
✓ No failed systemd services
✓ No recent error-level journal entries
✓ System load within expected range
✓ Memory availability verified

Hardware Health
✓ SMART disk health verified
✓ No storage health issues detected

---

## Observations

• Netdata reports only normal alarms with no warnings or critical events.
• Uptime Kuma is responding normally.
• Docker health checks are passing for all monitored containers.
• No failed system services remain.
• No error-level events were recorded during the post-migration validation period.
• Disk SMART status is healthy.
• Memory usage and system load are within acceptable operating limits.

---

## Issues Found

None.

---

## Actions Taken

✓ Verified monitoring platform.
✓ Verified Docker health status.
✓ Verified system logs.
✓ Verified SMART health.
✓ Verified memory usage.
✓ Verified system load.

---

## Decision

Phase 7 approved.

Proceed to:
PHASE 8 - BACKUP & RECOVERY READINESS.
============================================================
PHASE 8 - BACKUP & RECOVERY READINESS
=====================================

Status:
✅ PASSED

Objective:
Verify that configuration, application data, documentation, backups, and scheduled maintenance are available to support full system recovery.

---

## Checks Performed

Configuration
✓ Docker Compose configuration verified
✓ Homelab configuration directory verified
✓ Application configuration directories verified

Backups
✓ Native Jellyfin backup verified
✓ Docker Jellyfin backup verified

Documentation
✓ Git repository accessible
✓ Health check documentation maintained

Automation
✓ Scheduled container update cron job verified
✓ Systemd maintenance timers verified

Recovery Assets
✓ Application configuration available
✓ Media library available
✓ Docker Compose available
✓ Backup data available

---

## Observations

• All critical application configuration directories are present.
• Native and Docker Jellyfin backups are retained.
• Docker Compose configuration is available for service restoration.
• Scheduled maintenance tasks are active.
• Git repository is synchronized apart from current documentation updates.

---

## Issues Found

None requiring corrective action.

---

## Actions Taken

✓ Verified backup availability.
✓ Verified recovery configuration.
✓ Verified scheduled maintenance.
✓ Verified documentation repository.

---

## Decision

Phase 8 approved.

Proceed to:
PHASE 9 - SSD MIGRATION READINESS.
============================================================
PHASE 9 - SSD MIGRATION READINESS

Status:
✅ PASSED

Objective:
Confirm that all assets required for rebuilding the homelab on a fresh operating system have been identified, documented, and verified.

Checks Performed

Operating System
✓ Linux Mint version recorded
✓ Kernel version recorded

Docker Platform
✓ Docker Engine version recorded
✓ Docker Compose version recorded

Storage
✓ Existing HDD layout documented
✓ Target SSD detected
✓ Filesystem layout verified

Recovery Assets
✓ Docker Compose configuration verified
✓ Homelab configuration verified
✓ Jellyfin backup verified
✓ Git repository verified
✓ SSH keys verified
✓ Custom maintenance scripts verified
✓ Tailscale identity verified

Data Inventory
✓ Homelab configuration size recorded
✓ Media library size recorded
✓ Backup size recorded
✓ Repository size recorded

Observations

• All critical recovery assets are available.
• Migration target SSD is detected by the operating system.
• Current storage layout is fully documented.
• Container-owned directories generate expected permission warnings during non-root size calculations.
• Tailscale connectivity is healthy despite an informational DNS warning.

Issues Found

None requiring corrective action.

Actions Taken

✓ Verified migration assets.
✓ Verified storage inventory.
✓ Verified recovery configuration.
✓ Recorded software versions.
✓ Recorded baseline storage usage.

Decision

Phase 9 approved.

Proceed to:
PHASE 10 - FINAL ACCEPTANCE & BASELINE SNAPSHOT.
============================================================
PHASE 10 - FINAL ACCEPTANCE & BASELINE SNAPSHOT
===============================================

Status:
✅ PASSED

Objective:
Establish the official pre-migration baseline for the Homelab V2 environment before migrating the operating system to the SSD.

---

## Overall Validation Summary

Phase 1 - System Health
✓ PASSED

Phase 2 - Docker Platform
✓ PASSED

Phase 3 - Storage Validation
✓ PASSED

Phase 4 - Media Stack Validation
✓ PASSED

Phase 5 - Service Integration
✓ PASSED

Phase 6 - Network & Remote Access
✓ PASSED

Phase 7 - Monitoring & Alerting
✓ PASSED

Phase 8 - Backup & Recovery Readiness
✓ PASSED

Phase 9 - SSD Migration Readiness
✓ PASSED

---

## Baseline Snapshot

Operating System
• Linux Mint 22.3 (Zena)
• Kernel 6.17.0-40-generic

Docker Platform
• Docker Engine 29.1.3
• Docker Compose 2.40.3

Core Services
✓ Jellyfin
✓ Sonarr
✓ Radarr
✓ Bazarr
✓ Prowlarr
✓ Lidarr
✓ qBittorrent
✓ Homepage
✓ Home Assistant
✓ Netdata
✓ Uptime Kuma
✓ Navidrome
✓ Nextcloud
✓ Matter Server

Storage Inventory
• Homelab configuration: ~2.0 GB
• Media library: ~499 GB
• Jellyfin backup: ~1.4 GB

Recovery Assets
✓ Docker Compose
✓ Application configuration
✓ Media library
✓ Jellyfin backups
✓ GitHub documentation
✓ SSH keys
✓ Custom scripts
✓ Scheduled maintenance

Outstanding Items
• Tailscale DNS warning (informational only)
• Container-owned directories produce expected permission warnings when inspected without elevated privileges.

---

## Acceptance Decision

The Homelab V2 environment has successfully completed all validation phases.

No critical issues preventing migration were identified.

The system is approved as the reference baseline for the SSD migration project.

This document shall be used as the comparison checklist after the migration to confirm that all services, configurations, integrations, and recovery assets have been restored successfully.

============================================================
END OF PRE-MIGRATION BASELINE
=============================

