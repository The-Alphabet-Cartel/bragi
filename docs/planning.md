---
title: "Bragi - Planning"
description: "Planning for Bragi — Bot Infrastructure for The Alphabet Cartel's Fluxer Community"
category: Planning
tags:
  - planning
  - Bragi
  - fluxer
  - bots
  - python
author: "PapaBearDoes"
version: "v2.0"
last_updated: "2026-02-22"
---
# Bragi: Planning

============================================================================
**Bragi**: Bot Infrastructure Host for The Alphabet Cartel's Fluxer Community
**Community**: [The Alphabet Cartel](https://fluxer.gg/yGJfJH5C) | [alphabetcartel.net](https://alphabetcartel.org)
============================================================================

**Document Version**: v1.0
**Created**: 2026-02-22
**Phase**: Bot Infrastructure
**Status**: 🔄 Pivoted — Bot Infrastructure Host
**Last Updated**: 2026-02-22

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Why We Pivoted](#2-why-we-pivoted)
3. [Platform Decision — Fluxer](#3-platform-decision--fluxer)
4. [Infrastructure](#4-infrastructure)
5. [Bot Architecture](#5-bot-architecture)
6. [Authentication Stack](#6-authentication-stack)
7. [Networking & Proxy](#7-networking--proxy)
8. [Known Issues & Decisions Log](#8-known-issues--decisions-log)
9. [Open Questions](#9-open-questions)
10. [Next Steps](#10-next-steps)

---

## 1. Project Overview

**Bragi** is the bot infrastructure host for [The Alphabet Cartel](https://discord.gg/alphabetcartel), named for the Norse god of eloquence and poetry.

Bragi runs the Python-based bots that serve our community on [Fluxer](https://fluxer.app) — our chosen community chat platform. The Alphabet Cartel's chat platform itself is hosted at fluxer.app and does not require self-hosting infrastructure.

### Community Profile

The Alphabet Cartel is an LGBTQIA+ community with approximately 500 members focused on:

- Gaming (primary focus — safe space for queer gamers)
- Mental health support and peer advocacy
- Political discourse and activism
- Societal advocacy and lifestyle

### Current State

| Component | Status | Details |
|-----------|--------|---------|
| Bragi hardware | ✅ Complete | Debian Trixie, Docker ready |
| Fluxer community | ✅ Active | Hosted at fluxer.app |
| Bot infrastructure | 🔄 In progress | Architecture defined, viability testing next |
| Discord decommission | ⏳ Planned | Timing TBD by staff |

---

## 2. Why We Pivoted

Bragi was originally provisioned to self-host a community chat platform as a privacy-respecting alternative to Discord. After extensive research, we identified Fluxer as a platform that makes self-hosting unnecessary — and in fact, the hosted fluxer.app instance offers protections our self-hosted instance could not.

**Key factors that drove the pivot:**

Self-hosting a chat platform was always a stop-gap measure while we searched for a viable long-term solution. Fluxer is that solution. The hosted instance at fluxer.app sits in Sweden under GDPR and EU law, completely outside US jurisdiction. Our member data is protected by legal frameworks that meaningfully resist the kind of government surveillance we documented in our Discord Threat Assessment.

Redirecting Bragi toward bot infrastructure is a better use of the hardware. Bots need a reliable, always-on host. Bragi is exactly that.

See [fluxer-platform-assessment.md](fluxer-platform-assessment.md) for the full research findings presented to staff.

---

## 3. Platform Decision — Fluxer

**Platform:** [Fluxer](https://fluxer.app)
**Deployment:** Hosted at fluxer.app (not self-hosted)
**Company:** Fluxer Platform AB, Sweden (AGPLv3, GDPR)

### Why Fluxer

- Swedish legal jurisdiction — DHS subpoenas cannot reach fluxer.app
- No age verification, no facial scan pipeline, no Palantir connections
- AGPLv3 open source — auditable, cannot go closed-source
- Discord-compatible API — our Python bots can connect using adapted Discord libraries
- Closest feature parity to Discord of any alternative evaluated
- No advertising, no data selling, no venture capital
- Our members' Plutonium subscriptions directly fund independent privacy-respecting development

### What We Deprecated

| Platform Considered | Reason Rejected |
|--------------------|----------------|
| Matrix/Synapse | Federation CSAM replication risk |
| Rocket.Chat | Active DoD/IC government marketing + mandatory workspace registration |
| Stoat (Revolt) | E2EE not implemented; unstable under load |
| TeamSpeak 6 | Voice/text only; screen sharing unreliable on self-hosted |

---

## 4. Infrastructure

### Server Inventory

| Server | IP | Role | OS | Key Services |
|--------|-----|------|----|--------------|
| **Bragi** | 10.20.30.242 | Bot Infrastructure Host | Debian Trixie | Python bots, Docker |
| **Lofn** | 10.20.30.253 | Primary Homelab Host | Debian 12 | Docker, dnsmasq, NAS |
| **Talia** | 10.20.30.200 | Reverse Proxy | Debian (VM on Odin) | SWAG/NGINX, CrowdSec |
| **Odin** | 10.20.30.240 | Hypervisor | Windows 11 Pro | Hyper-V |
| **Bacchus** | 10.20.30.14 | AI Rig | Windows 11 Pro | AI workloads, dev |

### Bragi Hardware

- CPU: AMD Ryzen 7 6800U
- RAM: 24GB LPDDR5
- Storage:
  - OS: 512GB NVMe — Debian Trixie
  - Data: 2TB NVMe — mounted at `/opt/bragi`
- NIC: Realtek RTL8125B 2.5Gb (r8125-dkms driver)
- Location: Garage (AI-Mesh node ethernet backhaul)

### Docker Environment

- Docker Engine: 29.2.1 (official Docker repo)
- Docker Compose: v5.0.2
- Base directory: `/opt/bragi/`
- All secrets via Docker Secrets — never plaintext in compose files or `.env`

### Directory Structure

```
/opt/bragi/
├── bots/                       ← One subdirectory per bot
│   ├── <bot-name>/
│   │   ├── docker-compose.yml
│   │   ├── Dockerfile
│   │   ├── src/                ← Python bot source
│   │   └── data/               ← Persistent bot state
├── secrets/                    ← Docker secret files (chmod 600, never committed)
└── shared/                     ← Shared utilities / base images
```

### Known Hardware Notes

- RTL8125B NIC requires `r8125-dkms` — autoloads via `/etc/modules-load.d/r8125.conf`
- IP assigned via dnsmasq DHCP reservation on Lofn (MAC: `78:55:36:06:59:3A`)
- ACPI warning on boot is non-fatal — suppressed via `acpi=relaxed` in GRUB

---

## 5. Bot Architecture

### Python Viability

Fluxer's official quickstart uses Node.js (`@discordjs/core`), but **Fluxer's API is intentionally Discord-compatible** — same Gateway protocol, same REST event model, just pointed at `api.fluxer.app` instead of Discord's endpoints.

Python Discord libraries that allow custom base URL configuration can connect to Fluxer. Primary candidates to evaluate:

- **discord.py** — dominant Python library; base URL overridable via HTTP client config
- **hikari** — async-first, clean REST/Gateway separation; may be simplest to redirect
- **interactions.py** — modern slash-command library; note slash commands not yet on Fluxer

**Current limitation:** Fluxer does not yet have slash commands or interactions. Bots will use prefix commands (e.g., `!ping`) until that feature ships. This is on the Fluxer roadmap.

### Bot Token Management

Each bot gets its own application registered in Fluxer:

1. User Settings → Applications → Create Application
2. Regenerate bot token
3. Store token as a Docker Secret in `/opt/bragi/secrets/<bot-name>-token`
4. Inject via Docker Secrets into the container at runtime

Bot tokens are never stored in compose files, Dockerfiles, or source code.

### Bot Container Pattern

Each bot runs as an isolated Docker container with:

- Python 3.12+ slim base image
- Docker Secret injection for the bot token
- A named volume for any persistent state
- Restart policy: `unless-stopped`
- No exposed ports (bots initiate outbound connections to Fluxer's Gateway; they do not receive inbound)

### Network Requirements

Bots on Bragi need outbound access to:

- `api.fluxer.app` (HTTPS/443) — REST API
- `gateway.fluxer.app` (WSS/443) — WebSocket Gateway

No inbound ports required. No Cloudflare Tunnel needed for bot operation. Standard outbound internet access from Bragi's LAN IP is sufficient.

---

## 6. Authentication Stack

Bot tokens are the only authentication mechanism bots use — they do not go through Pocket ID or TinyAuth.

Pocket ID and TinyAuth remain on Lofn serving their existing roles (staff/admin authentication for other services). They are not involved in bot infrastructure.

| Service | Auth Method | Host |
|---------|-------------|------|
| Fluxer bots | Docker Secret (bot token) | Bragi |
| Pocket ID | Passkey/OIDC | Lofn |
| TinyAuth | Forward-auth | Lofn |

---

## 7. Networking & Proxy

Bots on Bragi do not require reverse proxy configuration. They are outbound-only services connecting to Fluxer's hosted API.

If we eventually expose any bot-adjacent web services (dashboards, webhooks), those would route through Talia as with all other web services. That is not a current requirement.

### Internal Network

| Device | IP | Role |
|--------|-----|------|
| Bragi | 10.20.30.242 | Bot infrastructure host |
| Lofn | 10.20.30.253 | dnsmasq, Docker, NAS |
| Talia | 10.20.30.200 | SWAG reverse proxy |
| Gateway | 10.20.30.1 | ASUS ZenWifi ET12 |

### Firewall

Bragi's UFW rules for bot infrastructure:

- SSH: LAN only (10.20.30.0/24)
- All other inbound: deny
- Outbound: unrestricted (bots need outbound internet)

---

## 8. Known Issues & Decisions Log

| Date | Decision / Finding | Outcome |
|------|-------------------|---------|
| Feb 2026 | RTL8125B NIC not detected on fresh Trixie install | Resolved: r8125-dkms + linux-headers |
| Feb 2026 | DHCP not working — dnsmasq listen-address restricted | Resolved: AI-Mesh node reboot |
| Feb 2026 | ACPI error on boot | Non-fatal, suppressed via acpi=relaxed |
| Feb 2026 | Matrix federation CSAM risk identified | Rejected Matrix |
| Feb 2026 | Rocket.Chat government entanglement confirmed | Rejected Rocket.Chat |
| Feb 2026 | Stoat unstable, no E2EE | Discovery layer only, not primary platform |
| Feb 2026 | Fluxer identified and evaluated | Selected as primary platform |
| Feb 2026 | Hosted fluxer.app chosen over self-hosting | Swedish jurisdiction; eliminates LiveKit/UDP complexity |
| Feb 2026 | Bragi repurposed — chat platform → bot host | Better use of hardware; self-hosting no longer needed |
| Feb 2026 | Python bot viability confirmed in principle | Fluxer API is Discord-compatible; testing needed to confirm library behavior |

---

## 9. Open Questions

- [ ] **Python library:** Which library works best with Fluxer's API? (discord.py vs hikari vs interactions.py)
- [ ] **Bot viability test:** Can we successfully connect a Python bot to Fluxer's Gateway and receive events?
- [ ] **Prefix vs slash commands:** Slash commands not yet on Fluxer — confirm prefix command approach for initial bots
- [ ] **Discord decommission:** What is the timeline and communication plan for the Discord → Fluxer migration?
- [ ] **Bot roster:** What bots does the community actually need? (welcome bot, moderation, mental health resources, etc.)
- [ ] **Backup strategy:** Define backup schedule for bot data volumes on Bragi

---

## 10. Next Steps

### Immediate (Bot Viability Testing)

1. Set up a test bot application in Fluxer
2. Write a minimal Python bot using discord.py pointed at api.fluxer.app
3. Confirm Gateway connection, event receipt, and message sending
4. Test with hikari if discord.py presents friction
5. Document which library works and why — write up findings

### Bot Infrastructure Setup

6. Create `/opt/bragi/bots/` directory structure on Bragi
7. Define base Python Dockerfile for bot containers
8. Create Docker Secrets scaffolding for bot tokens
9. Stand up first real bot in a container

### Community Migration

10. Work with staff to define bot requirements for the Fluxer community
11. Build and deploy bots in priority order
12. Plan Discord decommission timeline with staff
13. Communicate migration plan to community members

---

**Built with care for chosen family** 🏳️‍🌈
