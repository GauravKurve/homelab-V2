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

**Status:** Selected (Subject to final validation before installation)

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

# Pending Decisions

The following topics remain under active design.

- Filesystem layout
- Directory structure
- Docker architecture
- Backup strategy
- Monitoring stack
- Notification system
- Network architecture
