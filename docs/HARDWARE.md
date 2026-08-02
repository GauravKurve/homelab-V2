# Hardware Profile

## Overview

Homelab V2 is built on a repurposed Lenovo G50-45 laptop.

Rather than purchasing dedicated server hardware, this project is designed around existing hardware with the goal of achieving reliable 24/7 operation while keeping power consumption low.

The hardware profile directly influences every architectural decision made throughout this project.

---

# System Specifications

| Component | Details |
|----------|---------|
| Model | Lenovo G50-45 |
| CPU | AMD A8-6410 APU |
| CPU Cores | 4 |
| Memory | 8 GB DDR3 |
| Maximum Supported Memory | 16 GB |
| Graphics | AMD Radeon R5 + AMD Radeon R5 M230 |
| Primary Storage | 500 GB Crucial BX500 SSD |
| Secondary Storage | 1 TB Western Digital HDD |
| Network | Gigabit Ethernet + Wi-Fi + Bluetooth |

---

# Hardware Strengths

The existing hardware provides several advantages for a home server.

- Low power consumption
- Dual-drive storage (SSD + HDD)
- Built-in battery acts as a small UPS
- AMD-V virtualization support
- Reliable Linux compatibility
- Quiet operation
- Dedicated Gigabit Ethernet

These strengths make the laptop well suited for Docker containers, media streaming, file storage, home automation and remote administration.

---

# Hardware Limitations

Like every homelab, this one is designed around certain constraints.

## CPU

The AMD A8-6410 is sufficient for running multiple Docker containers simultaneously but is not intended for heavy virtualization or multiple real-time video transcodes.

## Memory

Current memory capacity is limited to 8 GB.

Maximum supported memory is 16 GB.

The architecture should therefore prioritize lightweight services and avoid unnecessary overhead.

## Graphics

The laptop uses legacy AMD Radeon graphics.

The system prioritizes stability over cutting-edge graphics technologies.

## Wake Capabilities

This laptop does not support Wake-on-LAN (WoL) or Wake-on-WiFi.

As a result, the homelab is designed to remain powered on continuously rather than being powered on remotely after shutdown.

## Battery

Battery health is reduced compared to its original capacity.

For homelab usage, the battery primarily serves as short-term protection against brief power interruptions.

---

# Design Implications

The hardware profile leads to several important architectural decisions.

- Lightweight operating system
- Minimal desktop environment
- Docker-based services
- SSD dedicated to operating system, Docker and downloads
- HDD dedicated to long-term media storage
- Simple monitoring instead of enterprise monitoring solutions
- Low maintenance design
- Easy migration to future hardware

---

# Future Upgrade Path

Homelab V2 is intentionally designed to be hardware independent.

When future hardware becomes available, the objective is to migrate the existing Docker stack and storage layout with minimal changes.

The software architecture should outlive the hardware.
