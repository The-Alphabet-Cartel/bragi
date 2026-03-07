# Bragi

Bot orchestration platform for [The Alphabet Cartel](https://fluxer.gg/yGJfJH5C) and [Joint Task Force Draugr](https://fluxer.gg) Fluxer communities.

Named for the Norse god of poetry and music — the voice of the gods who welcomed fallen warriors to Valhalla — Bragi is the backbone that brings every bot in the family to life.

---

## What Bragi Does

Bragi is not a bot itself. It is the **top-level orchestration hub** — a monorepo that owns shared standards, the bot skeleton template, and references each community deployment as a Git submodule. Each community (TAC, JFTD) manages its own bot stack independently, while all bots share the same architectural standards defined here.

**Two-tier submodule architecture.** Bragi references community repos (`tac`, `jftd`) as submodules. Each community repo in turn references its individual bots as submodules. This allows each layer to be developed, deployed, and permissioned independently.

**Shared standards.** The [Clean Architecture Charter](docs/standards/charter.md) and [fluxer-py Quirks reference](docs/standards/fluxer-py_quirks.md) live here and apply to every bot across all communities.

**Skeleton template.** The `skeleton/` directory provides a standardized starting point for any new bot, regardless of which community it serves.

**Shared infrastructure home.** The `shared/` directory is reserved for any utilities or configuration that span multiple community deployments.

---

## Community Deployments

| Repo | Community | Bots |
|------|-----------|------|
| [**tac**](https://github.com/the-alphabet-cartel/tac) | The Alphabet Cartel | Portia, Prism, Puck |
| [**jtfd**](https://github.com/the-alphabet-cartel/jtfd) | Joint Task Force Draugr | Frigg, Ratatoskr |

---

## Repository Structure

```
bragi/
├── tac/                          ← Git submodule → the-alphabet-cartel/tac
│   ├── portia/                   ← Git submodule → the-alphabet-cartel/portia
│   ├── prism/                    ← Git submodule → the-alphabet-cartel/prism
│   ├── puck/                     ← Git submodule → the-alphabet-cartel/puck
│   ├── docker-compose.yml        ← TAC bot stack
│   └── secrets/
│       └── README.md             ← TAC credential setup guide (committed)
├── jtfd/                         ← Git submodule → the-alphabet-cartel/jtfd
│   ├── frigg/                    ← Git submodule → the-alphabet-cartel/frigg
│   ├── ratatoskr/                ← Git submodule → the-alphabet-cartel/ratatoskr
│   ├── docker-compose.yml        ← JTFD bot stack
│   └── secrets/
│       └── README.md             ← JFTD credential setup guide (committed)
├── docs/
│   └── standards/
│       ├── charter.md            ← Clean Architecture Charter (all bots)
│       └── fluxer-py_quirks.md   ← Platform API reference
├── skeleton/                     ← Standardized new bot template
└── shared/                       ← Shared infrastructure (future use)
```

---

## Setup

```bash
# Clone with all submodules (both tiers)
git clone --recurse-submodules https://github.com/the-alphabet-cartel/bragi.git
cd bragi

# Or, if already cloned without submodules
git submodule update --init --recursive
```

> **Note:** The `--recursive` flag is required to initialize both the community repos *and* the bot submodules nested within them.

---

## Deployment

Each community manages its own Docker stack independently. See the respective community repo for deployment instructions:

- **TAC:** [`tac/README.md`](tac/README.md)
- **JFTD:** [`jftd/README.md`](jftd/README.md)

---

## Adding a New Bot

1. Create the bot repository under [The-Alphabet-Cartel](https://github.com/The-Alphabet-Cartel) org following the [Charter](docs/standards/charter.md)
2. Add it as a submodule inside the appropriate community repo (`tac/` or `jftd/`)
3. Add the service definition to that community's `docker-compose.yml`
4. Add any required secrets to the community's `secrets/` directory and update its `README.md`

---

## Standards & Documentation

| Document | Description |
|----------|-------------|
| [Clean Architecture Charter](docs/standards/charter.md) | Immutable development rules for all Bragi bots |
| [fluxer-py Quirks & API Reference](docs/standards/fluxer-py_quirks.md) | Platform library behaviors and workarounds |

---

## Platform

Bragi's bots run on [Fluxer](https://fluxer.gg), a Discord-alternative platform, using the [fluxer-py](https://github.com/akarealemil/fluxer.py) library. Fluxer-py is under active development — see the [fluxer-py Quirks & API Reference](docs/standards/fluxer-py_quirks.md) for known behaviors, workarounds, and patterns discovered during development.

---

## Infrastructure

| Component | Details |
|-----------|---------|
| **Server** | Bragi (Beelink SER5 Max), Debian Trixie |
| **Container Runtime** | Docker Engine 29.x + Compose v5 |
| **Bot Language** | Python 3.12 |
| **Bot Library** | [fluxer-py](https://github.com/akarealemil/fluxer.py) |
| **CI/CD** | GitHub Actions → GHCR container images |

---

## Naming

In Norse mythology, Bragi is the god of poetry and music — the skald of the gods who welcomed heroes to the halls of Valhalla with song. As the orchestration layer, Bragi welcomes every bot into the stack and gives them the stage to serve their communities.

---

**Built with care for chosen family** 🏳️‍🌈
