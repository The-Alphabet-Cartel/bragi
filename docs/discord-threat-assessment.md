---
title: "Discord Threat Assessment"
description: "Why The Alphabet Cartel must migrate away from Discord"
category: Research
tags:
  - discord
  - privacy
  - threat-assessment
  - migration
author: "PapaBearDoes"
version: "v3.0"
last_updated: "2026-03-05"
---
# Discord Threat Assessment

============================================================================
**Bragi**: Bot Infrastructure for The Alphabet Cartel
**The Alphabet Cartel** - [The Alphabet Cartel](https://fluxer.gg/yGJfJH5C) | [alphabetcartel.net](https://alphabetcartel.net)
============================================================================

**Document Version**: v3.0
**Created**: 2026-02-20
**Status**: 🚨 Active Concern — Updated with developments through March 5, 2026
**Last Updated**: 2026-03-05

---

## Table of Contents

1. [Purpose](#1-purpose)
2. [Mandatory Age Verification — Now Partially Live](#2-mandatory-age-verification--now-partially-live)
3. [The Persona Exposure — A Surveillance Stack Hiding in Plain Sight](#3-the-persona-exposure--a-surveillance-stack-hiding-in-plain-sight)
4. [Vendor Swap: Persona Out, K-ID In — The Architecture Is Unchanged](#4-vendor-swap-persona-out-k-id-in--the-architecture-is-unchanged)
5. [The 2025 Data Breach](#5-the-2025-data-breach)
6. [The Palantir / ICE Connection — Now an $85 Billion Surveillance Machine](#6-the-palantir--ice-connection--now-an-85-billion-surveillance-machine)
7. [DHS Subpoenas — Discord Named, Hundreds Issued, Targeting Speech Like Ours](#7-dhs-subpoenas--discord-named-hundreds-issued-targeting-speech-like-ours)
8. [Discord's Response — Delay, Not Reversal](#8-discords-response--delay-not-reversal)
9. [Impact on LGBTQIA+ Members Specifically](#9-impact-on-lgbtqia-members-specifically)
10. [Summary: The Threat Model](#10-summary-the-threat-model)
11. [Sources](#11-sources)

---

## 1. Purpose

This document summarizes the concrete, documented threats that Discord's recent policy changes and government entanglements pose to members of [The Alphabet Cartel](https://alphabetcartel.net). It is intended to inform staff and help communicate the urgency of our platform migration to the broader community.

These are not hypothetical risks. Every threat described below is active, documented, and has continued developing since this assessment was first written in February 2026.

**How to read this document:** Each major section follows a consistent structure — *what we assessed originally*, followed by *what has since been confirmed or worsened*. The original arguments were sound when written. The new findings validate them and, in several areas, substantially raise the stakes. We have not replaced our original analysis; we have built on it.

**Version history:**
- **v1.0** (2026-02-20): Original assessment. Documented age verification, Persona/Palantir investment link, 2025 breach, DHS subpoena threat.
- **v2.0** (2026-02-25): Updated with Persona frontend exposure findings, ImmigrationOS/ELITE details, Discord's February 24 delay announcement.
- **v3.0** (2026-03-05): Updated with teen-by-default rollout now live, K-ID as Persona replacement, DHS subpoena surge confirmed (hundreds issued, speech being targeted), ICE surveillance apparatus now documented at $85B scale, behavioral profiling already running on all Discord users.

The situation has materially worsened at each update. The decision to move to Fluxer has been validated at every turn.


---

## 2. Mandatory Age Verification — Now Partially Live

### What We Originally Assessed (v1.0)

In early February 2026, Discord announced that all users would be placed into a "teen-appropriate experience" by default. To escape restrictions — content filtering, limited DMs, no Stage channel access — flagged users would need to submit either a **facial scan** or a **government-issued photo ID** through a third-party verification vendor. We assessed this as an unacceptable surveillance pipeline that TAC members should not be compelled to participate in.

### What Has Since Been Confirmed (v3.0)

**Teen-by-default restrictions are partially live as of March 2026.** The age verification prompt for most users is delayed to H2 2026, but the default restrictions are not. All new and existing Discord accounts are being reclassified into teen-restricted mode in a phased rollout that began in early March 2026. This affects content filters, DM access, Stage channel access, and friend request handling — in public servers and in private group chats alike.

**The behavioral profiling is already running.** Discord's age inference model — the system that decides whether to skip the verification prompt for a given user — is actively analyzing every member's account right now. It uses account tenure, payment methods on file, server membership patterns, activity timing, and behavioral signals to build an age classification. This profiling is not paused pending the H2 2026 rollout. It is live. Every TAC member still on Discord is being profiled today.

**The disproportionate impact on LGBTQIA+ communities is confirmed.** Multiple independent sources have documented that Discord's teen-by-default policy disproportionately impacts LGBTQ+ communities specifically because many of these servers have voluntarily applied age-restricted settings to create safe, adult-only spaces — even when the content itself is not explicitly sexual. Our community structure means our members are more likely to be caught by verification gates than the average Discord user.

### The March Rollout Is Delayed for Prompts — Not for Restrictions or Profiling

Following widespread backlash, Discord's co-founder and CTO Stanislav Vishnevskiy published a blog post on February 24, 2026 acknowledging that Discord had "missed the mark" and announcing a delay of the global verification prompt rollout to the **second half of 2026**. Discord claims approximately 90% of users will not need to verify their age via the explicit prompt flow.

What Discord did not do: reverse the policy, pause the behavioral profiling, or stop rolling out default restrictions. The verification prompts are delayed. The infrastructure and the profiling are not.

### Why "Voluntary" Was Never Reassuring

Discord is not legally required to implement age verification globally. Other major platforms — including Reddit — have fought age verification legislation in court. Discord chose to build this infrastructure ahead of any mandate. The Electronic Frontier Foundation stated there is "no reason for Discord to comply in advance" with laws that have not been passed or enforced against them.

The choice to build a biometric identity pipeline when not required to do so tells us something about the platform's direction of travel. The delay is a response to user revolt. The infrastructure intent remains unchanged — and the behavioral profiling component of that infrastructure is running right now.


---

## 3. The Persona Exposure — A Surveillance Stack Hiding in Plain Sight

### What We Originally Assessed (v1.0/v2.0)

We documented that Persona Identities, Inc. — Discord's age verification vendor for a UK test — was not simply an age-checking tool. It is a comprehensive KYC/AML (Know Your Customer / Anti-Money Laundering) surveillance platform. In February 2026, security researchers found that Persona's frontend code was publicly accessible on a FedRAMP-authorized US government endpoint, exposing the full scope of what the system was doing to users.

### The Full Scope of What Was Confirmed

The exposed code showed Persona performing **269 distinct verification checks** per user, including:

- Facial recognition against watchlists and lists of politically exposed persons (PEPs)
- Adverse media screening across **14 categories including terrorism and espionage**
- Risk and similarity scoring on submitted identities
- Selfie analytics including suspicious-entity detection, pose repeat detection, and age inconsistency flags
- **Data retention of up to three years** for IP addresses, browser fingerprints, device fingerprints, government ID numbers, phone numbers, names, and faces

Discord had told users that biometric data would not leave their device. A deleted UK disclaimer stated that data would leave the device and be stored for up to seven days. The Persona files showed retention of **up to three years** — a direct contradiction of Discord's public reassurances.

The fact that Persona's exposed code sat on a **FedRAMP-authorized endpoint** is not incidental. FedRAMP authorizes cloud services for use by US federal agencies. Persona's CEO confirmed the company is actively pursuing FedRAMP authorization — building the compliance infrastructure to sell identity verification directly to the US federal government. A domain — `withpersona-gov.com` — was identified potentially querying an OpenAI government database. Persona's COO denied partnerships with federal agencies including ICE or DHS. The FedRAMP endpoint tells a more complicated story about where Persona's ambitions lie.

### Why This Still Matters After the Vendor Swap

Faced with this exposure, Discord confirmed it had ended its Persona partnership. Discord's CTO described Persona as failing to meet the platform's privacy bar — specifically that Persona was doing server-side processing rather than on-device processing for facial estimation.

This is better than nothing. But the exposure is what it is. Discord was running users through a full KYC/AML surveillance stack — one with watchlist screening for terrorism and espionage — without disclosing this to those users. That happened. The vendor swap does not change what the exposed code revealed about what was being done to people who went through it. And as we document in the next section, the vendor swap does not eliminate the structural vulnerability.


---

## 4. Vendor Swap: Persona Out, K-ID In — The Architecture Is Unchanged

*This section is new in v3.0.*

### What Changed

Discord has replaced Persona with **K-ID** as its primary global age verification vendor, with Persona retained only for some UK users where it was already deployed. Discord frames this as an improvement — and dropping Persona specifically is a meaningful response to the specific concerns about Persona's surveillance depth and FedRAMP ambitions.

### What Did Not Change

**The structural architecture is identical.** Identity documents still pass through a third-party vendor. Facial estimation still occurs (now on-device for K-ID, which is genuinely better). A human-verified fallback for failed estimations still exists — and it was precisely this fallback pathway that was exploited in the 2025 breach. Switching vendors does not eliminate that attack surface.

**K-ID is not a neutral party.** K-ID is also used by Meta and Snap — it is a major identity data aggregator across multiple large platforms. Users who verify through K-ID are submitting identity data to a company that now holds verification relationships across a significant portion of the major social platform ecosystem.

**The behavioral age inference model is unchanged and already running.** This is the system that profiles every user in the background to decide whether to route them to an explicit verification prompt. It uses account tenure, payment methods, server membership patterns, and behavioral signals. It does not require a verification vendor at all — Discord built and operates it entirely in-house. This profiling is live for every Discord user right now, regardless of vendor changes.

**The Electronic Frontier Foundation's assessment is unchanged.** The EFF noted that the vendor swap is "an improvement" but "doesn't eliminate the underlying potential for data breaches and other harms." Their core concern — that Discord is voluntarily building this infrastructure ahead of any legal requirement — has not been addressed by the vendor change.

### What This Means for TAC

The Persona-specific concerns we raised in v1.0 — the investment chain to Palantir, the FedRAMP government-access ambitions, the 269 surveillance checks — were accurate and are now on the record. Discord has acknowledged them implicitly by ending the relationship. The replacement vendor presents a different but not eliminated risk profile. The decision to leave Discord does not hinge on which vendor Discord is currently using. It hinges on the fact that Discord is building this pipeline at all.


---

## 5. The 2025 Data Breach

### What We Originally Assessed

In late 2024/early 2025, Discord disclosed that attackers had accessed a third-party vendor's systems used for age-related appeals, exposing approximately **70,000 users' government-issued ID photos** and associated sensitive personal data. Discord won the Electronic Frontier Foundation's 2025 "We Still Told You So" Breachies Award for this incident.

### Why This Remains Directly Relevant in v3.0

The breach has not receded into background context — it is the active lens through which every Discord reassurance about identity data security must be evaluated.

**The contested scope.** Discord's official figure is approximately 70,000 affected accounts. Attackers claimed up to 2.1 million ID photos were exfiltrated. Discord disputed the higher figure as an extortion tactic. The underlying point — that centralized identity document handling creates a high-value target — is not in dispute by either party.

**The vendor denial.** The third-party customer support service Discord alleged was responsible for the breach vigorously denied that it had ever handled government-issued IDs for Discord, or that its system had been hacked. This contradiction has never been publicly resolved.

**The architecture persists.** Discord states it no longer routes ID uploads through general support infrastructure. But it has introduced a new vendor (K-ID) for identity verification that includes a human-verified fallback for failed facial estimations. It was precisely the human-verified fallback pathway in the original system that created the breach. A new vendor with a similar architectural pattern does not eliminate that class of risk — it resets the clock on it.

**The trust deficit it created is legitimate.** Discord's announcement of global age verification came while users were still aware of this breach. The backlash to the February 2026 announcement was amplified by the entirely reasonable question: why would users submit identity documents to a platform that just demonstrated it cannot protect them?


---

## 6. The Palantir / ICE Connection — Now an $85 Billion Surveillance Machine

### What We Originally Assessed (v1.0)

We documented the investment relationship between Persona (Discord's age verification vendor), Founders Fund (Peter Thiel's venture firm), and Palantir. We noted that Palantir builds and operates ICE's core investigative infrastructure, that Stephen Miller holds a financial stake in Palantir, and that this created a concerning chain of custody from Discord identity data to immigration enforcement infrastructure.

### What Has Since Been Confirmed — The Scale Is Dramatically Larger (v2.0/v3.0)

The Palantir/ICE relationship has expanded into a surveillance apparatus of a scale that was not fully visible when the original assessment was written.

**ImmigrationOS ($30M contract, active through September 2027).** Palantir built and operates ImmigrationOS — an integrated AI-driven platform for immigration enforcement with three core functions: targeting and enforcement prioritization, self-deportation tracking with near-real-time visibility, and full immigration lifecycle management from identification through removal. The system pulls from passport records, Social Security files, IRS tax data, Medicaid records, DMV files, utility bills, court records, and license-plate reader data.

**ELITE — The Targeting App.** Part of the same $29.9M contract framework, ELITE (Enhanced Leads Identification & Targeting for Enforcement) functions, per its own documentation, like Google Maps populated with people instead of restaurants. ICE agents draw shapes on a map to identify "target-rich areas" for raids. Each person has a dossier with their photo, address, and a **confidence score** predicting whether they are currently at that location — derived in part from Medicaid address updates and other routine government data submissions. During "special operations," per the ELITE user guide, normal safeguards may be turned off.

**The $85 Billion arsenal.** ICE's July 2025 funding expansion, confirmed by multiple investigative outlets, built an interconnected surveillance infrastructure that now includes:
- Palantir ELITE: confidence scores and geospatial targeting from Medicaid and federal databases
- Mobile Fortify: facial recognition against a database of **1.2 billion photos**
- Zignal Labs: monitoring of **8 billion social media posts per day**
- BI2 iris scanners matching against 5 million records
- Cell-site simulators tracking phones in real time
- Drones capable of identifying people from 7.5 miles away

These tools are not siloed. They feed into each other. The database of 1.2 billion faces includes US citizens. The social media monitoring at 8 billion posts per day captures everyone who posts — not only immigrants. The cell-site simulators grab every phone in range of a deployment, not just targeted individuals.

**ICE's AI portfolio expanded 37% in six months.** Palantir appeared in DHS's AI inventory for the first time this cycle. The scale of investment indicates infrastructure being built for permanence, not pilot testing. A civil liberties review noted that an April 2026 deadline for AI risk compliance assessments exists — but the enforcement consequences of missing that deadline are unclear.

**Former Palantir employees condemned the contracts.** In May 2025, 13 former Palantir employees signed a public letter: *"Companies are placating Trump's administration, suppressing dissent, and aligning with his xenophobic, sexist, and oligarchic agenda. Big Tech, including Palantir, is increasingly complicit, normalizing authoritarianism under the guise of a 'revolution' led by oligarchs."*

**Stephen Miller's financial stake in Palantir** — confirmed by the American Immigration Council — means the official most responsible for directing deportation enforcement policy has a direct personal financial interest in Palantir's government contract growth.

### The Chain of Custody, v3.0

The chain we documented in v1.0 has become more concrete at every link:

```
Discord age verification data + behavioral profiling
    → K-ID (current vendor) / Persona (former vendor, Founders Fund–backed)
        → Founders Fund (major investor in both Persona and Palantir)
            → Palantir ($900M+ in federal contracts since Trump took office)
                → ImmigrationOS / ELITE (active ICE targeting platform)
                    → $85B ICE surveillance apparatus
                        → Deportation targeting of individuals identified via AI
```

Palantir has received more than **$900 million in federal contracts** since Trump took office.


---

## 7. DHS Subpoenas — Discord Named, Hundreds Issued, Targeting Speech Like Ours

### What We Originally Assessed (v1.0/v2.0)

We assessed that DHS administrative subpoenas — which require no judicial approval and can be issued directly to tech companies — represented a live threat to TAC members. We noted that Discord had been named among platforms receiving such subpoenas, and that at least three of four named platforms (Google, Meta, Reddit) had complied with some requests.

### What Has Since Been Confirmed — This Is Significantly Worse (v3.0)

The subpoena situation has developed into one of the most significant threats documented in this assessment. What was a stated risk in v1.0 is now a confirmed, ongoing, large-scale operation with specific documented cases.

**Hundreds of subpoenas, no judicial oversight.** The Department of Homeland Security has issued **hundreds of administrative subpoenas** to Google, Meta, Reddit, and Discord in recent months. These subpoenas demand names, email addresses, phone numbers, and other identifying data tied to accounts that criticized ICE, reported ICE agent locations, or tracked immigration enforcement activity. Administrative subpoenas require no judge. DHS writes one up, signs it, and sends it. The only check is whether the company complies or forces DHS to go to court to enforce it.

**Previously reserved for serious crimes — now used against political speech.** Tech employees and government officials told the New York Times this tool was historically used sparingly for serious crimes like child trafficking. It is now being deployed against people posting neighborhood watch alerts and political commentary.

**Google, Meta, and Reddit have complied.** Of the four named platforms, Google, Meta, and Reddit have confirmed compliance with at least some requests. Discord has declined to comment on whether it has complied — which is not the same as refusing.

**The cases are alarming in their specificity.** Documented examples include:
- A Pennsylvania bilingual Facebook page posting ICE checkpoint locations to its 10,000 followers — Meta subpoenaed in September 2025, users given 10-14 days to challenge before disclosure
- A Google retiree who sent a polite email to a publicly listed DHS lawyer asking for "common sense and decency" in an asylum case — subpoenaed within five hours, DHS agents showed up at his home weeks later to question him
- At least one Google subpoena with the "suspected violation" field left entirely blank — Google fulfilled it the same day it notified the user, leaving zero practical time to challenge

**The ACLU pattern.** DHS has withdrawn several subpoenas when legally challenged — before a judge could rule on their validity. The ACLU has characterized this as deliberate: DHS prefers to drop subpoenas under legal pressure rather than establish enforceable precedent against the practice. The pressure is designed to fall on individuals who lack resources to fight back.

**The EFF position is clear.** The Electronic Frontier Foundation has urged all platforms to require a court order before complying with any subpoena for user data. Voluntary compliance varies wildly across platforms. Discord's non-response is not reassuring.

### Why The Alphabet Cartel Is Directly in the Frame

We are an LGBTQIA+ advocacy community. We discuss political issues. We have members who are immigrants, mixed-status household members, or advocates for immigrant communities. We post about immigration enforcement. We have members who have been vocal about trans rights legislation, immigration policy, and other advocacy topics that have drawn DHS attention at other platforms.

We are exactly the profile these subpoenas target. Member usernames, email addresses, IP logs, account creation metadata, and message metadata already exist on Discord's servers and are accessible via this mechanism — with no warrant, no judge, and a 10-14 day window for the targeted person to find a lawyer and get to federal court.

That window, as the Google case demonstrated, can be effectively zero in practice.


---

## 8. Discord's Response — Delay, Not Reversal

### What We Originally Assessed (v2.0)

We assessed Discord's February 24 delay announcement as a response to user revolt that changed the timeline but not the structural situation. Discord's CTO acknowledged earned skepticism while asking users to extend trust the available evidence did not support.

### What Has Since Been Confirmed (v3.0)

The delay has played out exactly as assessed. Discord's commitments from the February 24 blog post:

- ✅ Global verification prompt rollout delayed to H2 2026 — **confirmed**
- ✅ Persona partnership ended — **confirmed, replaced with K-ID**
- ⏳ Vendor transparency list to be published before global launch — **not yet published**
- ⏳ Technical documentation for age inference model — **not yet published**
- ✅ Credit card verification as additional option — **in development**
- 🔴 Behavioral profiling paused during delay — **not done; confirmed running now**
- 🔴 Default restrictions rolled back — **not done; rolling out now**

Discord's CTO wrote: *"Many of you are worried that this is just another big tech company finding new ways to collect your personal data. That we're creating a problem to justify invasive solutions. I get that skepticism. It's earned, not just toward us, but toward the entire tech industry. But that's not what we're doing."*

The acknowledgment that the skepticism is earned is accurate. The claim that Discord is an exception is not supported by the evidence. A platform that:

- Built a biometric identity pipeline before being legally required to
- Used a vendor (Persona) conducting 269 surveillance checks without disclosing this to users
- Allowed a vendor breach that exposed 70,000 users' government IDs
- Deleted a privacy disclaimer it had published
- Has not publicly committed to resisting DHS subpoenas
- Is currently running behavioral profiling on all users during the "delay"
- Is currently rolling out default restrictions affecting LGBTQIA+ spaces

...is asking users to extend trust it has not demonstrated it has earned. The delay changes the timeline. It does not change the structural situation. One independent analysis put it plainly: "The delay to H2 2026 is the most strategically significant concession, because it buys Discord time to execute on these commitments. It also buys time for the story to fade from the news cycle."


---

## 9. Impact on LGBTQIA+ Members Specifically

### What We Originally Assessed (v1.0/v2.0)

We documented four specific vectors of harm for LGBTQIA+ members: trans and nonbinary members misidentified by facial estimation tools; members who rely on pseudonymity; members with immigration concerns; and members engaged in political advocacy.

### What Has Since Been Confirmed and Strengthened (v3.0)

**The disproportionate LGBTQIA+ impact is now independently confirmed.** Multiple sources have documented that Discord's teen-by-default policy disproportionately impacts LGBTQ+ communities because these communities often apply age-restricted settings to create safe adult spaces — even for non-sexual content. This is not our characterization alone. It is a documented pattern recognized by independent researchers and commentators.

**The political advocacy vector is now a live threat, not a theoretical one.** The DHS subpoena surge documented in Section 7 shows that political speech about immigration enforcement is actively being targeted — at the exact platforms where TAC members have been active. This is no longer a risk to model. It is an ongoing operation.

**The immigration concern vector is now more concrete.** The $85 billion surveillance machine documented in Section 6 — including 8 billion social media posts monitored per day via Zignal Labs — means that content our members have posted about immigration, ICE operations, trans rights, and related advocacy topics may already be in surveillance systems. The chain from Discord activity to enforcement action has become demonstrably shorter.

**Trans and nonbinary members face doubled exposure.** Facial estimation tools that misidentify gender-nonconforming presentations push those members into the manual ID verification pathway. In that pathway, government IDs that do not match presented identity create additional points of exposure and potential harm. This pathway is exactly what was compromised in the 2025 breach.

**The EFF has stated the principle clearly:** No one should have to choose between accessing online communities and protecting their privacy. For an LGBTQIA+ community in the current political climate, this is not abstract. It is a material safety concern for specific, identifiable members of our community — and the evidence base for that concern has grown substantially since v1.0.


---

## 10. Summary: The Threat Model

The risks are not theoretical. They are documented, current, and active — and have materially worsened at every update to this document.

| Threat | Status | v3.0 Update |
|--------|--------|-------------|
| Teen-by-default restrictions rolling out globally | 🔴 Live now | Partial rollout began March 2026; not delayed |
| Behavioral age profiling running on all users | 🔴 Active now | Confirmed running during the H2 2026 "delay" |
| Age verification prompts (H2 2026) | 🔴 Coming | Delayed, not cancelled |
| Persona conducted 269 surveillance checks including watchlist screening | 🔴 Confirmed | Discord ended Persona relationship; practices confirmed via code exposure |
| Vendor swap to K-ID does not fix structural vulnerability | 🔴 Confirmed | EFF: "an improvement, but doesn't eliminate the underlying harms" |
| 2025 breach of 70,000 users' government IDs | 🔴 Occurred | Scope disputed; vendor denial unresolved; fallback architecture unchanged |
| Persona code sat on FedRAMP US government endpoint | 🔴 Confirmed | Persona pursuing federal agency contracts; withpersona-gov.com identified |
| Founders Fund investment link (Persona → Palantir) | 🔴 Confirmed | Original chain of custody remains accurate |
| Palantir ImmigrationOS: $30M ICE targeting platform | 🔴 Active through 2027 | AI-driven deportation targeting from Medicaid, SSN, IRS, DMV, license plate data |
| Palantir ELITE: real-time geospatial targeting tool | 🔴 Active | "Google Maps for deportation targets"; confidence scores; safeguards can be disabled |
| $85B ICE surveillance arsenal | 🔴 Confirmed and operational | 1.2B face database; 8B social media posts/day monitored; drones; iris scanners |
| Stephen Miller financial stake in Palantir | 🔴 Confirmed | Policy architect has personal financial interest in contract growth |
| DHS subpoenas targeting political speech | 🔴 Active and escalating | Hundreds issued; Google, Meta, Reddit confirmed compliant; Discord non-responsive |
| Blank-field subpoenas fulfilled same-day | 🔴 Documented | At least one Google subpoena had suspected violation field left blank |
| LGBTQIA+ communities disproportionately impacted | 🔴 Independently confirmed | Age-gated community structure creates higher verification exposure |
| Facial estimation unreliable for trans/nonbinary members | 🔴 Documented | Misidentification routes to manual ID pathway; 2025 breach hit that pathway |
| Discord's response: delay and rebranding, not structural reversal | 🟡 Ongoing | Commitments made; behavioral profiling and restrictions not paused |

**We made the right decision to move to Fluxer.** The situation has worsened at every update to this document. The delay to H2 2026 does not change the calculus — it confirms that Discord is still planning to build exactly what we assessed as unacceptable, while already running the behavioral profiling and rolling out restrictions that affect our community. Our community is on Fluxer. That is where we should be.

---

## 11. Sources

**Age Verification & Persona**
- [Discord Voluntarily Pushes Mandatory Age Verification Despite Recent Data Breach](https://www.eff.org/deeplinks/2026/02/discord-voluntarily-pushes-mandatory-age-verification-despite-recent-data-breach) — EFF, February 12, 2026
- [Age verification vendor Persona left frontend exposed, researchers say](https://www.malwarebytes.com/blog/news/2026/02/age-verification-vendor-persona-left-frontend-exposed) — Malwarebytes, February 20, 2026
- [Hackers Expose Discord Age Verification System Issue After Persona Frontend Code Left Wide Open](https://www.ibtimes.co.uk/discord-age-verification-security-breach-1780591) — IBTimes UK, February 20, 2026
- [Discord distances itself from Peter Thiel–backed verification software after its code was found on a U.S. government server](https://fortune.com/2026/02/24/discord-peter-thiel-backed-persona-identity-verification-breach/) — Fortune, February 24, 2026
- [Discord delays its global age verification after upsetting almost everyone on Earth: 'We've made mistakes'](https://www.pcgamer.com/software/platforms/discord-delays-its-global-age-verification-rollout-and-cuts-ties-with-peter-thiel-backed-verification-vendor-after-upsetting-almost-everyone-on-earth-weve-made-mistakes/) — PC Gamer, February 24, 2026
- [Discord delays global rollout of age verification after backlash](https://techcrunch.com/2026/02/24/discord-delays-global-rollout-of-age-verification-after-backlash/) — TechCrunch, February 24, 2026
- [Getting Global Age Assurance Right: What We Got Wrong and What's Changing](https://discord.com/blog/getting-global-age-assurance-right-what-we-got-wrong-and-whats-changing) — Discord CTO blog, February 24, 2026
- [Discord Delays Global Age Verification to H2 2026: What Changed and What Didn't](https://redact.dev/blog/discord-delays-age-verification-h2-2026-what-changed) — Redact, February 2026

**K-ID & Vendor Architecture**
- [Discord introduces global age verification](https://proton.me/blog/discord-global-age-verification) — Proton, February 2026
- [Discord Age Check Backlash: 70,000 IDs Breached Months Ago](https://www.zyphe.com/news/discord-age-verification-backlash-2026) — Zyphe, 2026

**LGBTQIA+ Community Impact**
- [Discord's New Age Verification Policy: What BL Fans Need to Know](https://www.dramallama.app/post/discord-s-new-age-verification-policy-what-bl-fans-need-to-know) — DramaLlama, February 13, 2026
- [Discord Age Verification March 2026: What Gamers Must Know](https://genelmag.com/article/discord-age-verification-march-2026-changes) — GNL Magazine, 2026

**DHS Subpoenas**
- [DHS Sends Subpoenas to Google, Meta, Reddit, and Discord to Identify Americans Who Criticize ICE](https://www.ibtimes.co.uk/dhs-subpoenas-free-speech-online-privacy-1779372) — IBTimes UK, February 14, 2026
- [US Department of Homeland Security has reportedly demanded personal information about ICE's critics from Discord, Reddit, Google, and Meta](https://www.pcgamer.com/software/platforms/us-department-of-homeland-security-has-reportedly-demanded-personal-information-about-ices-critics-from-discord-reddit-google-and-meta-and-at-least-3-of-those-platforms-have-complied/) — PC Gamer, February 17, 2026
- [Homeland Security reportedly sent hundreds of subpoenas seeking to unmask anti-ICE accounts](https://techcrunch.com/2026/02/14/homeland-security-reportedly-sent-hundreds-of-subpoenas-seeking-to-unmask-anti-ice-accounts/) — TechCrunch, February 14, 2026
- [DHS Orders Tech Giants to Unmask Anti-ICE Accounts](https://www.thedailybeast.com/dhs-orders-tech-giants-to-unmask-anti-ice-accounts/) — The Daily Beast, February 2026
- [Feds Try To Dox Discord And Reddit Users Who Are Mean To ICE](https://kotaku.com/ice-reddit-discord-doxxing-dhs-subpoena-2000670648) — Kotaku, February 2026

**Palantir / ICE Surveillance**
- [ICE to Use ImmigrationOS by Palantir, a New AI System, to Track Immigrants' Movements](https://www.americanimmigrationcouncil.org/blog/ice-immigrationos-palantir-ai-track-immigrants/) — American Immigration Council, 2025
- [ELITE: The Palantir App ICE Uses to Find Neighborhoods to Raid](https://www.404media.co/elite-the-palantir-app-ice-uses-to-find-neighborhoods-to-raid/) — 404 Media, January 2026
- [ICE alleged to use Palantir-developed tool that uses Medicaid data to track arrest targets](https://fortune.com/2026/01/26/ice-allegedly-uses-palantir-tool-tracking-medicaid-data/) — Fortune, January 26, 2026
- [Inside ICE's $85 Billion Arsenal: Every Surveillance Tool and How They Work Together](https://stateofsurveillance.org/news/ice-85-billion-surveillance-arsenal-complete-guide-2026/) — State of Surveillance, February 2026
- [ICE Deploys Palantir, OpenAI Tools for Immigration Enforcement](https://winbuzzer.com/2026/01/30/ice-palantir-openai-immigration-enforcement-ai-tools-xcxwbn/) — WinBuzzer, January 30, 2026

---

**Built with care for chosen family** 🏳️‍🌈
