# 🎯 Meta Ads Script & TA Generator

An OpenClaw skill that turns your product spec into a complete Meta Ads campaign package — ready to execute, no follow-up questions needed.

## Why This Skill Exists

**The problem is time, not talent.**

A competent Media Buyer building a Meta Ads campaign from a product brief typically spends:

| Task | Time (manual) | With this skill |
|------|--------------|-----------------|
| Write 3 ad script variants | 3–5 hours | ~30 seconds |
| Research & set target audience | 2–4 hours | ~20 seconds |
| Build budget plan + CPA benchmarks | 1–2 hours | ~15 seconds |
| Create A/B test roadmap + decision tree | 2–3 hours | ~15 seconds |
| **Total** | **2–3 days** | **< 2 minutes** |

That's not a typo. The same deliverable that takes a team 2–3 business days gets generated in under 2 minutes.

## What It Does

- Reads your product spec `.md` file and asks 4 clarifying questions
- Generates 3+ ad script variants (Video 15s/30s, Static, Carousel) with different psychological hooks
- Builds target audience settings with layered reasoning (demographics, interest stack, placements)
- Creates a budget plan (ABO/CBO), revenue projection, A/B test roadmap, and a 30-day decision tree

## Example Output

See [examples/output-sample.md](examples/output-sample.md) for a full generated campaign package — scripts, TA, budget plan, and playbook.

## What It Costs Per Run

| Model | Input (~45.6k tok) | Output (~1.4k tok) | Total |
|---|---|---|---|
| Gemini 3 Flash | $0.023 | $0.004 | **$0.03** |
| GPT-5.2 Instant | $0.080 | $0.020 | **$0.10** |
| Gemini 3.1 Pro | $0.091 | $0.017 | **$0.11** |
| Claude 4.6 Sonnet | $0.137 | $0.021 | **$0.16** *(recommended)* |
| Claude 4.6 Opus | $0.228 | $0.035 | **$0.26** |

*Token counts measured during internal deployment on OpenClaw VPS. Input = ~45,000 tokens (SKILL.md context) + ~600 tokens (product spec). Output = ~1,400 tokens. API pricing as of Feb 2026.*

For context: a freelance Media Buyer charges **$500–$2,000** for the same scope. Every campaign you plan manually is time you can't get back.

## Installation

**Option 1 — Via GitHub URL:**
Paste this URL in your ClawHub chat:
```
https://github.com/psychomafia-tiger/cook-a-skill-master-ads
```

**Option 2 — Manual install:**
```bash
cp -r . ~/clawd/skills/meta-ads-script-ta-generator/
```

## Usage

Trigger the skill by uploading your product spec and typing:
```
Generate ads for @spec.md
```

## Input spec.md Format

See [spec/spec.md](spec/spec.md) for all required and optional fields.

For a ready-to-use sample input, see [examples/input-sample.md](examples/input-sample.md).

## Requirements

- OpenClaw installed and configured
- A product `spec.md` file with at least 6 required fields filled (see [spec/spec.md](spec/spec.md))

## Roadmap & Vision: The Full-Stack AI Agents Ecosystem

### Current State: MVP (Agent Layer 2)

This skill is **Agent Layer 2** of a planned multi-agent autonomous advertising platform. Today, it handles campaign planning from a written spec. Tomorrow, the entire funnel automates.

### Future: Complete AI Agents Ecosystem

```
                           ┌─────────────────────────────────────────────────────────┐
                           │        USER INPUT: Product Brief (voice/text/pdf)       │
                           └────────────────────┬────────────────────────────────────┘
                                                │
                    ┌───────────────────────────┴───────────────────────────┐
                    │                                                       │
                    ▼                                                       ▼
        ╔═══════════════════════╗                            ╔════════════════════════╗
        ║   AGENT 1: Spec       ║                            ║  OR: Upload spec.md    ║
        ║   Writer              ║                            ║  (skip to Agent 2)     ║
        ║   ─────────────────── ║                            ╚════════════┬═══════════╝
        ║ • Voice → Transcript  ║                                         │
        ║ • Interactive Q&A     ║                                         │
        ║ • Product Details +   ║                                         │
        ║   Target Audience     ║                                         │
        ║ • Gen spec.md         ║                                         │
        ╚═════┬─────────────────╝                                         │
              │                                                           │
              └──────────────────────────┬──────────────────────────────┘
                                        │
                                        ▼
                    ╔═══════════════════════════════════════════╗
                    ║   AGENT 2: Campaign Planner (Current)     ║
                    ║   ─────────────────────────────────────── ║
                    ║ • Analyze product spec                    ║
                    ║ • Generate 3+ ad script variants          ║
                    ║ • Define TA + interest stacks             ║
                    ║ • Build budget plan + CPA benchmarks      ║
                    ║ • Create A/B test roadmap                 ║
                    ║ • Output: Campaign brief (JSON/MD)        ║
                    ╚═════┬───────────────────────────────────┬═╝
                          │                                   │
              ┌───────────┴───────────┐           ┌───────────┴───────────┐
              ▼                       ▼           ▼                       ▼
    ╔═══════════════════╗   ╔═══════════════════╗  ╔═══════════════════╗
    ║   AGENT 3A:       ║   ║   AGENT 3B:       ║  ║   AGENT 4:        ║
    ║   AI Image Gen    ║   ║   AI Video Gen    ║  ║   Campaign        ║
    ║   ─────────────── ║   ║   ─────────────── ║  ║   Executor        ║
    ║ • Script → Images ║   ║ • Script → 15s/30s║  ║   ───────────────  ║
    ║ • 1200x628px +    ║   ║ • Auto B-rolls    ║  ║ • API Integration ║
    ║   mobile variants ║   ║ • Music synthesis ║  ║ • Auto setup ads  ║
    ║ • Per variant: 3x ║   ║ • Per variant: 2x ║  ║ • Budget allocation
    ╚────────┬──────────╝   ╚────────┬──────────╝  ║ • Launch campaign  ║
             │                      │              ╚───────────┬────────┘
             └──────────┬───────────┴────────────────────┬────┘
                        │                               │
                        ▼                               ▼
                ╔═══════════════════════════════════════════════╗
                ║   AGENT 5: Performance Monitor & Optimizer    ║
                ║   ─────────────────────────────────────────── ║
                ║ • Real-time metrics tracking (ROAS, CPA, CTR) ║
                ║ • Daily performance reports                   ║
                ║ • Auto-pause underperforming variants         ║
                ║ • Scale high-ROAS ad sets                     ║
                ║ • Suggest creative/TA pivots                  ║
                ║ • Re-run optimization loop when triggered     ║
                ╚────────────┬──────────────────────────────────╝
                             │
                    ┌────────┴────────┐
                    │                 │
                    ▼                 ▼
            ┌─────────────────┐ ┌─────────────────┐
            │ ROAS > Target?  │ │ CPA < Limit?    │
            │ YES → Scale     │ │ YES → Continue  │
            │ NO → Loop ────┐ │ NO → Pause ───┐ │
            └─────────────────┘ └─────────────────┘
                    │                       │
                    └───────────────┬───────┘
                                    ▼
                    ╔═══════════════════════════════════════╗
                    ║  OPTIMIZATION LOOP (Daily)            ║
                    ║  Until Perfect Scale Achieved         ║
                    ║  ─────────────────────────────────────║
                    ║  • Retest hooks + formats             ║
                    ║  • Pivot audience segments            ║
                    ║  • Adjust budgets automatically       ║
                    ║  • No manual intervention needed      ║
                    ╚═══════════════════════════════════════╝
```

### Key Features of the Ecosystem

| Layer | Agent | Status | Output |
|-------|-------|--------|--------|
| **1** | Spec Writer | 🔄 Q2 2026 | Automated product spec from voice/text |
| **2** | Campaign Planner | ✅ MVP Live | Campaign brief (scripts, TA, budget, playbook) |
| **3A** | Image Generator | 🔄 Q3 2026 | AI-generated ad visuals (3 variants/hook) |
| **3B** | Video Generator | 🔄 Q3 2026 | AI-generated video ads (2 variants/hook) |
| **4** | Campaign Executor | 🔄 Q2 2026 | Automated Meta Ads setup + launch |
| **5** | Performance Monitor | 🔄 Q3 2026 | Daily reporting + auto-optimization loop |

### Multi-Platform Expansion Roadmap

```
Phase 1: Meta Ads Only (Current)
├── Facebook Ads
├── Instagram Ads
└── Audience Network

Phase 2: Google & Social [Q3 2026]
├── Google Search Ads
├── Google Display Network
├── YouTube Ads
├── TikTok Ads
└── TikTok Shop

Phase 3: Premium Channels [Q4 2026]
├── Pinterest Ads
├── LinkedIn Ads
├── Amazon DSP
└── Shopify Native Ads
```

#### Per-Platform Agent Expansion

For each new platform, the ecosystem scales horizontally:

```
AGENT 2 (Campaign Planner)
    ├─ Meta Ads version (current)
    ├─ Google Ads version (Q3)
    ├─ TikTok Ads version (Q3)
    └─ Pinterest Ads version (Q4)
       ↓ All feed into ↓
AGENT 4 (Campaign Executor)
    ├─ Meta Ads Executor
    ├─ Google Ads Executor
    ├─ TikTok Ads Executor
    └─ Pinterest Ads Executor
       ↓ All monitored by ↓
AGENT 5 (Performance Monitor)
    └─ Unified Dashboard (cross-platform metrics)
```

### Why This Architecture?

✅ **No manual intervention** — Users input once, system optimizes forever
✅ **Loop-based optimization** — Daily improvements until target ROAS achieved
✅ **Multi-platform economies of scale** — One spec, multiple channels simultaneously
✅ **AI-native creatives** — Never worry about photographer/videographer delays
✅ **Real-time adaptation** — Pause, scale, pivot without human bottleneck

### Success Metrics (Post-Launch)

- Campaign planning time: **2 days → 2 minutes**
- Creative production: **5–7 days → <1 day**
- Campaign optimization: **weekly manual checks → daily automatic**
- Media Buyer overhead: **60–70% manual work → <10% oversight only**

---

## License

MIT — see [LICENSE](LICENSE).
