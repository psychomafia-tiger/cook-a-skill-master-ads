# 🎯 SKILL CARD — Meta Ads Script & TA Generator

> **One product spec in. One complete Meta Ads campaign out.**
> 3 ad scripts. Targeting with reasoning. Budget plan. 30-day launch playbook.
> One conversation. Zero guesswork.
>
> **For:** Creative Producers, Media Buyers, and Startup Founders running Meta Ads.

```
Version: 1.0.0 | License: MIT | Tests: 10/10 Passing | Bugs: 15 found & fixed
```

---

## The Problem

**This skill replaces 2–3 days of campaign planning with a 2-minute conversation.**

Every new campaign starts the same way: a Creative Producer stares at a blank doc, a Media Buyer guesses at targeting, and the team burns 2–3 business days assembling a brief that still needs revisions. The A/B test strategy is "we'll figure it out after launch." Nobody knows what to do on Day 7 if CPA is 2x target.

**This skill eliminates that entire cycle.**

---

## Before → After

| | ❌ Without This Skill | ✅ With This Skill |
|---|---|---|
| **Ad Scripts** | Brainstorm from scratch. 1 format, maybe 2. **3–5 hours** | 3+ variants (Video + Static + Carousel) with psychological triggers. **~30s** |
| **Target Audience** | Gut feeling + copy-paste from last campaign. **2–4 hours** | 3-layer Interest Stack with reasoned justification per setting. **~20s** |
| **Budget Plan** | "Split it evenly" + no CPA benchmarks. **1–2 hours** | ABO/CBO auto-selected, consolidation logic, CPA by category. **~15s** |
| **Post-Launch Plan** | "We'll optimize as we go." **2–3 hours** *(if at all)* | Revenue projection + A/B roadmap + decision tree. **~15s** |
| **Total** | **2–3 business days** | **< 2 minutes** |
| **Revisions needed** | 2–4 rounds of back-and-forth | Minimal — output follows a tested, structured template |

---

## What Gets Generated

The skill outputs a campaign package in **3 sequential messages**:

| Message | Contains |
|---|---|
| 📦 **Message 1** | Executive Summary + 3–5 Ad Script variants (Video 15s/30s, Static, Carousel — each with visuals, voiceover, hooks, production notes) |
| 📦 **Message 2** | TA Settings (Demographics + 3-layer Interest Stack + Placements + Negatives) + Budget Plan (ABO/CBO + ad set split + CPA benchmarks) *(TA section skipped if user has existing TA — Q3=C)* |
| 📦 **Message 3** | Revenue Projection (3 scenarios) + A/B Test Roadmap (timeline-adaptive: Sprint / Standard / Ongoing) + Decision Tree (day-by-day if/then actions) |

See [output-sample.md](examples/output-sample.md) for a fully realized 251-line example.

---

## What Makes This Different

| Feature | Typical Ad Generator | This Skill |
|---|---|---|
| Multiple format-aware variants | ❌ or 1 variant, text only | ✅ 3–5 variants across Video/Static/Carousel |
| Psychological hook strategy | ❌ | ✅ Pain / Curiosity / Transformation / Social Proof |
| Target audience with reasoning | ❌ | ✅ 3-layer stack, every setting justified |
| Budget + revenue projection | ❌ | ✅ CPA benchmarks, 3 scenarios, breakeven calc |
| 30-day post-launch playbook | ❌ | ✅ A/B roadmap + decision tree |
| Input quality gate | ❌ | ✅ Readiness Score — blocks bad inputs, flags assumptions |

---

## How It Works

```
User uploads spec.md
  ──▶ Skill reads spec + checks sensitive category (Gate A)
  ◀── Asks Q1–Q4 (objective, budget, assets, video)
User answers Q1–Q4
  ──▶ 8-step pipeline:
       1. Readiness Score (< 5 = STOP)
       2. Product Analysis  →  3. Hook Generation
       4. Script Assembly   →  5. TA Derivation
       6. Budget Planning   →  7. Output Assembly
       8. Post-Launch Playbook
  ◀── 3 messages delivered sequentially
  ✅ Execute.
```

**8 Decision Gates** ensure quality: Readiness Score threshold, B2B/B2C detection, health/beauty compliance, no-video fallback, social proof conditional, pre-launch audience swap, timeline-based campaign type, and Q3 section skip logic.

---

## Quality Engineering

```
📊 Test cases: 10/10 passing | Bugs: 15 found & fixed | Debug sessions: 4
   Edge cases: health/beauty, no-video, partial answers, ongoing budget,
   incomplete spec, awareness objective, app install, sprint timeline
```

Evidence: [testlog.md](testlog.md) · [debug_log.md](debug_log.md)

---

## Input Requirements

**6 required fields** in a `.md` file: `product_name`, `value_proposition`, `target_persona`, `product_category`, `key_features`, `market`

**5 optional fields** (enrich output): `pricing` · `competitors` · `tone_of_voice` · `existing_social_proof` · `visual_direction`

**4 clarifying questions** asked before generation:

| # | Question | Controls |
|---|---|---|
| Q1 | Objective (Awareness / Lead Gen / Purchase / App Install) | Revenue model, CPA benchmarks |
| Q2 | Budget + timeline | Daily budget, ABO vs CBO, playbook variant |
| Q3 | Existing assets (Nothing / Raw video / TA set) | Which sections to generate vs skip |
| Q4 | Video capability (Yes / No) | Format selection (Video → Static fallback) |

---

## Tools & AI Used

| Tool | Role |
|---|---|
| **Claude** (Anthropic) | Spec design, architecture, SKILL.md authoring, debugging, test design |
| **OpenClaw** | Runtime platform — SKILL.md runs as a skill |
| **ClawHub** | Distribution via marketplace |
| **Meta Ads Best Practices 2025–2026** | CPA benchmarks, ABO/CBO rules, budget split ratios *(internal benchmark assumptions)* |

---

## Limitations

| What This Skill Does NOT Do | Why |
|---|---|
| Retargeting campaigns | Requires Phase 1 data first |
| Dynamic Creative Optimization | Requires Meta API integration |
| Direct Meta Ads Manager setup | Output is a brief, not API calls |
| Guarantee specific ROAS | Projections are benchmark-based estimates |
| Multi-language in single run | One language per run (matches spec language) |

---

## Cost Per Run

| Model | Input (~45.6k tok) | Output (~1.4k tok) | Total |
|---|---|---|---|
| Gemini 3 Flash | $0.023 | $0.004 | **$0.03** |
| GPT-5.2 Instant | $0.080 | $0.020 | **$0.10** |
| Gemini 3.1 Pro | $0.091 | $0.017 | **$0.11** |
| Claude 4.6 Sonnet | $0.137 | $0.021 | **$0.16** *(recommended)* |
| Claude 4.6 Opus | $0.228 | $0.035 | **$0.26** |

*Token counts measured during internal deployment on OpenClaw VPS (direct install, not via ClawHub). Input = ~45,000 tokens (SKILL.md context) + ~600 tokens (product spec). Output = ~1,400 tokens. API pricing as of Feb 2026.*

A freelance Media Buyer charges **$500–$2,000** for the same scope.

---

## Roadmap

| Phase | What | Status |
|---|---|---|
| ✅ Phase 1 | Core skill: scripts + TA + budget + playbook | **Deployed (internal)** |
| 🔜 Phase 2 | Retargeting campaign module | Planned |
| 🔜 Phase 3 | Meta Ads Manager API integration | Planned |
| 🔜 Phase 4 | Multi-language + regional CPA benchmarks | Planned |

---

## Quick Start

```
1. Install:  Paste https://github.com/psychomafia-tiger/cook-a-skill-master-ads in ClawHub
2. Prepare:  Create product spec.md with 6 required fields
3. Run:      Upload spec → Answer 4 questions → Receive campaign package
4. Execute:  Scripts → Creative Producer | TA + Budget → Media Buyer | Playbook → Team Lead
```

---

<div align="center">

**Built by Tiger** · **Powered by OpenClaw** · **Distributed via ClawHub**

*Every campaign you plan manually is time you can't get back.*

</div>
