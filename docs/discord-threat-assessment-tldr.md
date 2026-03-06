---
title: "Discord Threat Assessment — TLDR"
description: "The short version. Major issues only. No walls of text."
category: Research
tags:
  - discord
  - privacy
  - threat-assessment
  - tldr
author: "PapaBearDoes"
version: "v3.0"
last_updated: "2026-03-05"
---
# 🚨 Why We Left Discord — The Short Version

> **For the full breakdown:** See `discord-threat-assessment.md`
> **Last updated:** March 5, 2026

---

## 🧠 What's Actually Happening Right Now

- 🔴 **Discord is restricting accounts by default — starting NOW (March 2026)**
  - Not waiting for the "big rollout" — it's already rolling out
  - Limited DMs, filtered content, no Stage channels until you verify
  - LGBTQ+ communities hit harder because we use age-restricted settings for *safety*, not just explicit content

- 🔴 **Discord is already profiling every single user in the background**
  - Tracking: account age, payment methods, server memberships, activity patterns
  - No verification prompt needed — the surveillance is already running
  - You don't know your score. You can't opt out.

---

## 🪪 The ID / Face Scan Problem

- 🔴 **To get your account back to normal, Discord wants a government ID or facial scan**
  - Delayed until late 2026 — but still coming
  - The vendor they originally used (Persona) was running **269 background checks on each person**
    - Watchlist screening ✔️
    - Terrorism/espionage flags ✔️
    - Data kept for **up to 3 years** ✔️
  - Discord told users data "wouldn't leave their device" — **that was false**

- 🔴 **They swapped vendors (now using K-ID) — but didn't fix the problem**
  - Same architecture: third-party vendor + human fallback = same breach risk
  - K-ID is also used by Meta and Snap — it's a major data aggregator
  - The profiling running *right now* doesn't need any vendor at all

- 🔴 **This already went wrong once**
  - 2025: ~70,000 users' government IDs were leaked through a vendor breach
  - The exact pathway that was breached still exists in the new system

---

## 🏛️ The Government Connection

- 🔴 **Discord's original ID vendor had ties to a US federal surveillance system**
  - Persona's code was found sitting on a US government-authorized server
  - Persona is building tools to sell identity checks directly to federal agencies

- 🔴 **The money trail goes: Discord → Persona → Founders Fund → Palantir → ICE**
  - Palantir built ICE's deportation targeting system (ImmigrationOS)
  - It uses Medicaid records, DMV files, IRS data, Social Security numbers, utility bills
  - There's also a tool called ELITE that works like "Google Maps but for finding people to deport"
  - 1.2 billion faces in the facial recognition database
  - 8 billion social media posts monitored every single day
  - Stephen Miller — the person running deportation policy — has a personal financial stake in Palantir

---

## 🚔 The Government Is Already Coming For Accounts Like Ours

- 🔴 **Hundreds of subpoenas sent to Discord, Google, Meta, and Reddit**
  - No judge required — DHS just sends them directly
  - Targeting: people who criticized ICE, reported ICE locations, tracked immigration enforcement
  - Google, Meta, and Reddit have confirmed they complied with some requests
  - **Discord has not said whether they complied**

- 🔴 **The cases are scary specific**
  - A Facebook page posting ICE checkpoint locations → Meta subpoenaed
  - A retired person who sent a *polite email* to a DHS lawyer → subpoenaed within 5 hours, agents at their door weeks later
  - One Google subpoena had the "suspected violation" field **left blank** — Google fulfilled it same-day anyway

- 🔴 **TAC is exactly the kind of community being targeted**
  - We're LGBTQ+
  - We talk about immigration
  - We do advocacy
  - Our members' account data (usernames, emails, IPs) is sitting on Discord's servers right now

---

## 🏳️‍🌈 Why This Hits Our Community Harder

- 🔴 **Trans and nonbinary members**
  - Facial age estimation tools are bad at reading gender-nonconforming faces
  - Getting flagged = forced into the ID upload path
  - Government IDs may not match how someone presents — outing risk

- 🔴 **Members who use a pseudonym**
  - Youth, survivors, people in unsupportive families or workplaces
  - Forced choice: hand over your real identity or lose access to your community

- 🔴 **Members with immigration concerns**
  - The surveillance machine is specifically built to find them
  - Medicaid data, DMV records, and utility bills are already being used

- 🔴 **Anyone who's ever posted about politics or advocacy**
  - That's literally what the subpoenas are targeting

---

## ✅ Why We Moved to Fluxer

- ✅ **Swedish company — US government subpoenas can't touch it directly**
  - Would require a MLAT treaty process with judicial oversight on both sides
  - Much slower, politically complicated, and publicly visible

- ✅ **No age verification, no facial scans, no ID uploads, no vendor pipeline**

- ✅ **No Palantir connection, no government contracts**

- ✅ **Open source (AGPLv3) — we can read every line of the code**

- ✅ **GDPR-protected — EU data law applies**

- ✅ **Same channels/roles/voice/reactions UX you already know**

---

## 🟡 What Fluxer Doesn't Have Yet

- ⚠️ No end-to-end encryption by default (use Signal for truly private convos)
- ⚠️ No native mobile app yet (PWA works, native in progress)
- ⚠️ Still in beta — occasional hiccups

---

> **Bottom line:** Discord is building surveillance infrastructure, the government is actively using it against communities like ours, and it's already started. We got out at the right time. Come join us on Fluxer. 🏳️‍🌈
>
> 👉 **https://fluxer.gg/yGJfJH5C**
