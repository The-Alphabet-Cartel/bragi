# Bragi

Bot orchestration platform for [The Alphabet Cartel](https://fluxer.gg/yGJfJH5C)'s Fluxer community.

Named for the Norse god of poetry and music — the voice of the gods who welcomed fallen warriors to Valhalla — Bragi is the backbone that brings every bot in the family to life.

---

## What Bragi Does

Bragi is not a bot itself. It is the **deployment hub** — a unified Docker Compose stack that orchestrates every bot serving The Alphabet Cartel. Each bot lives in its own repository as a Git submodule, built and published independently via GitHub Actions. Bragi pulls their container images, wires up secrets, networks, and volumes, and brings the whole family online with a single command.

**Single source of truth.** One `docker-compose.yml` defines every bot, every secret mount, every volume, and every network connection. No scattered configs across the server.

**Submodule architecture.** Each bot is a standalone repository with its own Dockerfile, CI/CD pipeline, and README. Bragi references them as Git submodules for development access while deploying from pre-built container images.

**Shared secrets directory.** All bot tokens and API credentials live in one `secrets/` directory on the host, mounted into containers via Docker Secrets. Nothing sensitive touches source control.

---

## The Bot Family

| Bot | Role | Description |
|-----|------|-------------|
| [**Portia**](https://github.com/the-alphabet-cartel/portia) | Voice Channel Manager | Creates private temp voice channels when users join the lobby. Cleans up automatically when empty. Named for Shakespeare's advocate in *The Merchant of Venice*. |
| [**Prism**](https://github.com/the-alphabet-cartel/prism) | Member Onboarding | Assigns the base member role when someone posts in `#introductions`. Named for how light through a prism reveals every color. |
| [**Puck**](https://github.com/the-alphabet-cartel/puck) | Stream Monitor | Watches Twitch and YouTube for community members going live, toggling a "Live" role for visibility. Named for Shakespeare's mischievous herald in *A Midsummer Night's Dream*. |

All bots follow the same architectural patterns defined in the [Clean Architecture Charter](docs/standards/charter.md): factory functions, dependency injection, three-layer config, Docker Secrets for credentials, and Python entrypoints with tini.

---

## Architecture

```
┌─────────────────────────────────────────────────────────┐
│                     Bragi (Host)                        │
│                                                         │
│  docker-compose.yml ─── single stack, all bots          │
│                                                         │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐         │
│  │   Portia   │  │   Prism    │  │    Puck    │         │
│  │  (voice)   │  │ (welcome)  │  │ (streams)  │         │
│  └─────┬──────┘  └─────┬──────┘  └─────┬──────┘         │
│        │               │               │                │
│        └───────────┬───┘───────────────┘                │
│                    │                                    │
│              bragi-net (Docker network)                 │
│                                                         │
│  secrets/          ← Docker Secrets (gitignored)        │
│  /opt/bragi/       ← Persistent volumes (logs + data)   │
└─────────────────────────────────────────────────────────┘
```

### Config Stack

Every bot in the family uses the same three-layer configuration pattern:

```
bot_config.json       ← structural defaults (committed)
      ↓
.env                  ← runtime overrides (not committed)
      ↓
Docker Secrets        ← sensitive values (never in source)
```

---

## Repository Structure

```
bragi/
├── docker-compose.yml            ← Unified bot stack
├── .env.template                 ← Shared environment reference
├── .gitmodules                   ← Submodule declarations
├── secrets/
│   ├── README.md                 ← Credential setup guide (committed)
│   ├── portia_fluxer_token      ← (gitignored)
│   ├── prism_fluxer_token       ← (gitignored)
│   ├── puck_fluxer_token        ← (gitignored)
│   ├── twitch_client_id         ← (gitignored)
│   ├── twitch_client_secret     ← (gitignored)
│   └── youtube_api_key          ← (gitignored)
├── docs/
│   └── standards/
│       ├── charter.md            ← Clean Architecture Charter
│       └── fluxer-py_quirks.md   ← Platform API reference
├── portia/                       ← Git submodule → the-alphabet-cartel/portia
├── prism/                        ← Git submodule → the-alphabet-cartel/prism
└── puck/                         ← Git submodule → the-alphabet-cartel/puck
```

---

## Deployment

### Prerequisites

- **Server:** Debian Linux with Docker Engine 29.x + Compose v5
- Fluxer bot tokens for each bot (see [`secrets/README.md`](secrets/README.md))
- Twitch and YouTube API credentials for Puck (see [`secrets/README.md`](secrets/README.md))

### Setup

```bash
# 1. Clone with submodules
git clone --recurse-submodules https://github.com/the-alphabet-cartel/bragi.git
cd bragi

# 2. Create the Docker network
docker network create bragi-net

# 3. Create host directories for persistent data
mkdir -p /opt/bragi/bots/portia/{logs,data}
mkdir -p /opt/bragi/bots/prism/{logs,data}
mkdir -p /opt/bragi/puck/{logs,data}

# 4. Configure environment
cp .env.template .env
# Edit .env — set GUILD_ID and bot-specific channel/role IDs

# 5. Create secrets (see secrets/README.md for detailed instructions)
printf 'token' > secrets/portia_fluxer_token
printf 'token' > secrets/prism_fluxer_token
printf 'token' > secrets/puck_fluxer_token
printf 'client-id' > secrets/twitch_client_id
printf 'client-secret' > secrets/twitch_client_secret
printf 'api-key' > secrets/youtube_api_key
chmod 600 secrets/*_token secrets/twitch_* secrets/youtube_*

# 6. Deploy the full stack
docker compose up -d
```

### Managing the Stack

```bash
# View all bot logs
docker compose logs -f

# Restart a single bot
docker compose restart portia

# Pull latest images and redeploy
docker compose pull && docker compose up -d

# Update submodules (for development)
git submodule update --remote --merge
```

---

## Adding a New Bot

1. Create the bot repository under [The-Alphabet-Cartel](https://github.com/The-Alphabet-Cartel) org following the [Charter](docs/standards/charter.md)
2. Add it as a submodule:
   ```bash
   git submodule add https://github.com/the-alphabet-cartel/new-bot.git
   ```
3. Add the service definition to `docker-compose.yml` following the existing pattern
4. Add any required secrets to `secrets/` and update `secrets/README.md`
5. Add the bot's environment variables to `.env.template`
6. Create host directories: `mkdir -p /opt/bragi/bots/new-bot/{logs,data}`

---

## Platform

Bragi's bots run on [Fluxer](https://fluxer.gg), a Discord-alternative platform, using the [fluxer-py](https://github.com/akarealemil/fluxer.py) library. Fluxer-py is under active development with limited documentation — see the [fluxer-py Quirks & API Reference](docs/standards/fluxer-py_quirks.md) for known behaviors, workarounds, and patterns discovered during bot development.

---

## Standards & Documentation

| Document | Description |
|----------|-------------|
| [Clean Architecture Charter](docs/standards/charter.md) | Immutable development rules for all Bragi bots |
| [fluxer-py Quirks & API Reference](docs/standards/fluxer-py_quirks.md) | Platform library behaviors and workarounds |
| [`secrets/README.md`](secrets/README.md) | Step-by-step credential setup for all APIs |

---

## Infrastructure

| Component | Details |
|-----------|---------|
| **Server** | Bragi (Beelink SER5 Max), Debian Trixie |
| **Container Runtime** | Docker Engine 29.x + Compose v5 |
| **Bot Language** | Python 3.12 |
| **Bot Library** | [fluxer-py](https://github.com/akarealemil/fluxer.py) |
| **CI/CD** | GitHub Actions → GHCR container images |
| **Network** | `bragi-net` Docker bridge network |
| **Persistence** | `/opt/bragi/` on host (logs + data volumes) |

---

## Naming

In Norse mythology, Bragi is the god of poetry and music — the skald of the gods who welcomed heroes to the halls of Valhalla with song. As the orchestration layer, Bragi welcomes every bot into the stack and gives them the stage to serve the community. The bot family draws from Shakespeare and symbolism: **Portia** (the advocate), **Prism** (the spectrum), and **Puck** (the herald).

---

**Built with care for chosen family** 🏳️‍🌈
