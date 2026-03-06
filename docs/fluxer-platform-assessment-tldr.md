---
title: "Fluxer Platform Assessment — TLDR"
description: "Why we picked Fluxer. Short version."
category: Research
tags:
  - fluxer
  - platform
  - migration
  - tldr
author: "PapaBearDoes"
version: "v1.1"
last_updated: "2026-03-05"
---
# ✅ Why We Picked Fluxer — The Short Version

> **For the full breakdown:** See `fluxer-platform-assessment.md`
> **Last updated:** March 5, 2026

---

## 🧠 tl;dr

We looked at **every major Discord alternative**. Most had deal-breakers.
Fluxer was the only one that actually fit what we needed.

Here's the short version of why.

---

## ❌ What We Ruled Out (and Why)

- ❌ **Matrix/Synapse** — Federation means child abuse material from other servers can replicate onto ours. Unacceptable.
- ❌ **Rocket.Chat** — Actively markets to the US military and intelligence community. Hard no.
- ❌ **Stoat (Revolt)** — Crashed under load, development too slow
- ❌ **TeamSpeak 6** — Voice only, screen sharing unreliable, no text community features
- ❌ **Discord** — See the other document 😬

---

## ✅ Why Fluxer

### 🇸🇪 It's Swedish — That's a Big Deal

- **US government can't just subpoena a Swedish company**
  - Would require a MLAT treaty process with judicial oversight on both sides
  - Much slower, politically complicated, and publicly visible
  - Confirmed critical: hundreds of DHS subpoenas were sent to Discord, Google, Meta, Reddit — we're not on any of those lists

- **GDPR applies** — EU data protection law, not US surveillance law

### 🔒 No Surveillance Pipeline

- ✅ No age verification
- ✅ No facial scans
- ✅ No ID uploads
- ✅ No Persona, no K-ID, no Palantir connection
- ✅ No behavioral profiling running on our members
- ✅ No government contracts

### 👀 We Can Actually See the Code

- ✅ Fully open source (AGPLv3)
- ✅ Full codebase on GitHub: https://github.com/fluxerapp/fluxer
- ✅ Developer is a real, publicly named person (Hampus Kraft, KTH Stockholm)
- ✅ Company is publicly registered in Sweden (verifiable in their corporate database)

### 💜 Built for Communities Like Ours

- ✅ Community guidelines explicitly protect people based on gender and sexual orientation
- ✅ No advertising, no data selling, no venture capital
- ✅ Revenue from optional subscriptions — not from monetizing your data

### 🎮 It Actually Feels Like Discord

- ✅ Channels, categories, roles — same structure
- ✅ Voice and video with screen sharing
- ✅ Reactions, custom emoji, DMs
- ✅ Full text search
- ✅ Moderation tools
- ✅ Bot API (that's what Bragi is for)

---

## 🤔 What Fluxer Doesn't Have Yet

- ⚠️ **No end-to-end encryption by default**
  - Messages are encrypted in transit and at rest in Sweden
  - For truly sensitive convos, use Signal
  - E2EE "secret chats" are on the roadmap

- ⚠️ **No native mobile app yet**
  - The PWA (progressive web app) works fine
  - Native iOS/Android is the developer's #1 priority

- ⚠️ **Still in beta**
  - Had some growing pains when Discord users flooded in
  - Actively being improved

- ⚠️ **One primary developer**
  - Real risk — mitigated by AGPLv3 license (code can always be forked), new funding, and growing contributor community

---

## 💸 Why Hosted Instead of Self-Hosting

We originally planned to self-host. Fluxer changed that.

- Voice (LiveKit) needs open UDP ports — doesn't work through Cloudflare Tunnel
- Self-hosting = we become responsible for updates, backups, security, GDPR compliance
- Using fluxer.app means Fluxer AB handles all of that
- Our server (Bragi) is better used running **bots** than running a chat backend

### What Bragi does instead:
- 🤖 Hosts all our Fluxer bots (Portia, Prism, Puck, Ratatoskr, and more)
- 🐳 Docker-based, Python bots, Discord-compatible API pointed at Fluxer
- 🔐 All secrets via Docker Secrets — never in config files

---

## 📊 Quick Scorecard

| What We Needed | Got It? |
|---|---|
| Outside US jurisdiction | ✅ Sweden |
| Open source & auditable | ✅ AGPLv3 |
| No age verification / surveillance | ✅ None |
| LGBTQ+ affirming policies | ✅ Explicit |
| Feels like Discord | ✅ Closest we found |
| Bot API | ✅ Discord-compatible |
| No government contracts | ✅ Clean |
| Protected from DHS subpoenas | ✅ MLAT required |
| E2EE | ⚠️ Coming |
| Native mobile app | ⚠️ Coming |
| Production stability | ⚠️ Beta |

---

> **Every concern we had about Discord got worse after we left.**
> DHS subpoenas, behavioral profiling already running, $85 billion ICE surveillance machine, teen restrictions already live.
>
> We made the right call. 🏳️‍🌈
>
> 👉 **https://fluxer.gg/yGJfJH5C**
