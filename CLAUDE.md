# CLAUDE.md — Context Reset File
> Read this first if you sense the context is long or you're unsure what we're building.

---

## What We're Building

An **OpenClaw Skill** named **"Meta Ads Script & TA Generator"**.

**One-line purpose:** Takes a product spec `.md` file as input → asks 4 clarifying questions → outputs a complete Meta Ads campaign package in 1 markdown block, ready to execute without further questions.

---

## Key Files in This Repo

| File | Purpose |
|---|---|
| `SKILL.md` | Runtime instructions — ClawHub reads this ✅ |
| `spec/spec.md` | Design spec — Supervisor Approved ✅ |
| `CLAUDE.md` | This file — context reset anchor |
| `README.md` | GitHub-facing documentation |
| `logs/CHANGELOG.md` | Project tracking + roadmap |

---

## System Architecture

```
╔══════════════════════════════════════════════════════════════════╗
║                    LAYER 1: TRIGGER                             ║
╠══════════════════════════════════════════════════════════════════╣
║                                                                  ║
║   [User]──▶ Upload product spec.md ──▶ Invoke Skill             ║
║                                                                  ║
╠══════════════════════════════════════════════════════════════════╣
║                    LAYER 2: OPENCLAW RUNTIME                    ║
╠══════════════════════════════════════════════════════════════════╣
║                                                                  ║
║   ┌─────────────┐    ┌──────────────┐    ┌───────────────────┐  ║
║   │  SKILL.md   │───▶│ LLM Context  │◀───│ User spec.md      │  ║
║   │(instructions)│    │   Window     │    │ (product data)    │  ║
║   └─────────────┘    │  ≤128K tokens│    └───────────────────┘  ║
║                      └──────┬───────┘                            ║
║                             │                                    ║
║         ┌───────────────────┼──────────────────────┐             ║
║         ▼                   ▼                      ▼             ║
║   No file write      No web access         Text-only output     ║
║   (output in chat)   (no API calls)        (Markdown block)     ║
║                                                                  ║
╠══════════════════════════════════════════════════════════════════╣
║                    LAYER 3: PROCESSING PIPELINE                 ║
╠══════════════════════════════════════════════════════════════════╣
║                                                                  ║
║   ┌──────────┐         ┌──────────────────────────┐             ║
║   │ CLARIFY  │◀───────▶│ GATE A: Sensitive         │             ║
║   │ Q1–Q4   │         │ category? → Ask confirm   │             ║
║   │(+2 bonus)│         │ before proceeding         │             ║
║   └────┬─────┘         └──────────────────────────┘             ║
║        ▼                                                         ║
║   ┌──────────┐                                                   ║
║   │ STEP 1   │                                                   ║
║   │ Spec     │                                                   ║
║   │ Quality  │                                                   ║
║   │ Check    │                                                   ║
║   └────┬─────┘                                                   ║
║        │                                                         ║
║   [GATE 1: Readiness Score]                                      ║
║        ├── Score 8–10 ──▶ Continue (full confidence)             ║
║        ├── Score 5–7  ──▶ Continue + FLAG all assumptions        ║
║        └── Score < 5  ──▶ STOP → list missing fields, ask user  ║
║                                                                  ║
║   ┌──────────┐    ┌──────────┐    ┌──────────┐                  ║
║   │ STEP 2   │───▶│ STEP 3   │───▶│ STEP 4   │                  ║
║   │ Product  │    │ Hook     │    │ Script   │                  ║
║   │ Analysis │    │Generation│    │ Assembly │                  ║
║   └──────────┘    └──────────┘    └──────────┘                  ║
║        │               │               │                         ║
║   [GATE B]         [GATE C]        [GATE D]                     ║
║   B2B/B2C?         Health/beauty?  Q4=No video?                 ║
║   → tone +         → Lifestyle     → all Video                  ║
║     TA logic         Upgrade only    formats → Static           ║
║                    [GATE E]                                      ║
║                    No social proof?                              ║
║                    → skip Social                                 ║
║                      Proof Hook                                  ║
║                                                                  ║
║   ┌──────────┐    ┌──────────┐                                  ║
║   │ STEP 5   │───▶│ STEP 6   │                                  ║
║   │ TA       │    │ Budget   │                                  ║
║   │Derivation│    │ Planning │                                  ║
║   └──────────┘    └──────────┘                                  ║
║        │               │                                         ║
║   [GATE F]         [GATE G]                                     ║
║   Not launched?    Timeline<14d?                                 ║
║   → Broad Int.     → CBO not ABO                                ║
║     not LAL                                                      ║
║                                                                  ║
║   ┌──────────┐    ┌──────────┐                                  ║
║   │ STEP 7   │───▶│ STEP 8   │                                  ║
║   │ Output   │    │ Playbook │                                  ║
║   │ Assembly │    │(always)  │                                  ║
║   └──────────┘    └──────────┘                                  ║
║        │                                                         ║
║   [GATE H]                                                       ║
║   Q3 answer? → conditionally skip output sections               ║
║                                                                  ║
╠══════════════════════════════════════════════════════════════════╣
║                 LAYER 4: DECISION GATES (pipeline order)        ║
╠══════════════════════════════════════════════════════════════════╣
║                                                                  ║
║  ┌──────────────────────────────────────────────────────────┐   ║
║  │ GATE A │ Sensitive category ──▶ ASK confirm (pre-Q1)    │   ║
║  │ GATE 1 │ Score 8–10 ──▶ full output                     │   ║
║  │        │ Score 5–7  ──▶ continue + FLAG assumptions      │   ║
║  │        │ Score < 5  ──▶ HARD STOP, request missing data  │   ║
║  │ GATE B │ B2B vs B2C ──▶ affects tone + TA (Step 2)      │   ║
║  │ GATE C │ Health/beauty ──▶ Lifestyle Upgrade only (Step 3)│  ║
║  │ GATE D │ Q4 no video ──▶ Video → Static (Step 4)        │   ║
║  │ GATE E │ No social proof ──▶ skip hook (Step 3)          │   ║
║  │ GATE F │ Not launched ──▶ Broad Interest not LAL (Step 5)│   ║
║  │ GATE G │ Timeline < 14d ──▶ CBO not ABO (Step 6)        │   ║
║  │ GATE H │ Q3 answer ──▶ conditional output skip (Step 7)  │   ║
║  └──────────────────────────────────────────────────────────┘   ║
║                                                                  ║
╠══════════════════════════════════════════════════════════════════╣
║                    LAYER 5: OUTPUT                              ║
╠══════════════════════════════════════════════════════════════════╣
║                                                                  ║
║   ┌─────────────────────────────────────────────────────────┐   ║
║   │                   OUTPUT .md BLOCK                      │   ║
║   │  ┌─ 1. Executive Summary ─────────────────────────┐    │   ║
║   │  ├─ 2. Ad Script: Variant A (Pain → Video)        │    │   ║
║   │  ├─ 3. Ad Script: Variant B (Curiosity → Static)  │    │   ║
║   │  ├─ 4. Ad Script: Variant C (Transform → Carousel)│    │   ║
║   │  ├─ 5. TA Settings (2-tier reasoning)      [Q3↓]  │    │   ║
║   │  ├─ 6. Budget Plan (ABO/CBO + split + scale)      │    │   ║
║   │  ├─ 7. Revenue Projection (3 scenarios)           │    │   ║
║   │  ├─ 8. A/B Test Roadmap (4-week plan)             │    │   ║
║   │  └─ 9. Decision Tree (day-by-day actions)         │    │   ║
║   │  * Sections 2–4: up to 2 bonus variants           │    │   ║
║   │  * [Q3↓] = may be skipped per Q3 answer           │    │   ║
║   │  * Sections 7–9 (Playbook) NEVER skipped          │    │   ║
║   └─────────────────────────────────────────────────────────┘   ║
║                                                                  ║
╚══════════════════════════════════════════════════════════════════╝
```

## Architecture Notes

- **Single-pass, no external calls:** The skill runs entirely within the LLM context window (≤128K tokens). No API calls, no file writes, no web access — all output is a single Markdown block in chat.
- **Gate 1 has 3 branches, not 2:** Score 8–10 (full output), Score 5–7 (generate but flag all assumptions at every gap), Score < 5 (hard stop). The 5–7 branch is the most common real-world case.
- **Q3 controls output scope, not internal processing:** When Q3=C, the agent leverages TA knowledge already in context but skips generating the TA output section. No hidden internal processing — the skip is purely about output generation.
- **Gates are ordered by pipeline position:** Gate A fires before Q1–Q4; Gate 1 at Step 1; Gates B–E during Steps 2–4; Gates F–G at Steps 5–6; Gate H at Step 7. Only Gate 1 is a hard stop; all others are branching.
- **Post-Launch Playbook (Step 8) never skips:** Revenue Projection + A/B Test Roadmap + Decision Tree always generate regardless of Q3. This is the skill's key differentiator.

---

## The Output This Skill Produces

When a user runs the skill, the agent generates **1 markdown block** containing:

1. **Executive Summary** — product, objective, budget, TA core, Readiness Score
2. **Ad Scripts** — 3 mandatory variants (different hook × format combos):
   - Variant A: Pain Hook → Video 15s or 30s
   - Variant B: Curiosity Hook → Static Ad
   - Variant C: Transformation Hook → Carousel 5 slides
   - (Up to 2 bonus hooks if data quality allows)
3. **TA Settings** — Demographics + Interest Stack (3 layers) + Lookalike/Placements + Negative Targeting, all with reasoning
4. **Budget Plan** — ABO or CBO based on timeline, split across 3 ad sets, CPA benchmarks, scale trigger rules
5. **Post-Launch Playbook** ← the "wow" feature:
   - **9A. Revenue Projection** — Best/Expected/Worst cases with breakeven day + ROAS
   - **9B. A/B Test Roadmap** — Week 1 Hook → Week 2 CTA → Week 3 Audience → Week 4 Scale
   - **9C. Decision Tree** — Day-by-day if/then actions table (Day 3, 7, 14, 21–30)

---

## Processing Flow (8 Steps)

```
Step 1: Spec Quality Check (Readiness Score rubric)
Step 2: Product Analysis (B2B/B2C, emotional/functional, decision cycle)
Step 3: Hook Generation (3 mandatory + up to 2 conditional)
Step 4: Script Assembly (each hook → assigned format per mapping table)
Step 5: TA Derivation (see Section 7 of spec.md)
Step 6: Budget Planning (see Section 8 of spec.md)
Step 7: Output Assembly (with Executive Summary + Q3 conditional skip logic)
Step 8: Post-Launch Playbook (always runs, never skipped)
```

---

## Critical Design Decisions (Don't Revisit Without Good Reason)

| Decision | What Was Decided | Why |
|---|---|---|
| Number of variants | **3 mandatory** (+ max 2 bonus) | Prevents context overflow; matches Success Criteria |
| Hook ↔ Format mapping | Fixed table in Step 4 | Eliminates ambiguity about which hook gets which format |
| Clarifying questions | 4 core questions (Q1–Q4); up to +2 bonus if spec missing `landing_page_url` or `brand_name` | Replaces original rigid "exactly 4" rule |
| Q2 combines budget + timeline | Single question | Old Q2+Q3 were separate but budget plan hardcoded 30 days — merged to fix |
| Q3 = existing assets → conditional skip | Step 7 has conditional table | Old spec collected data but didn't use it |
| Q4 = production capability | Affects format selection | If no video → all Video formats → Static |
| Readiness Score rubric | 6 required fields × 1.5pt + 1pt optional bonus = 10 max | Replaces vague "score it somehow" instruction |
| TA reasoning 2-tier | Core settings: 3-angle; Standard settings: 1-line | Old rule required 4-angle on everything including auto-placement |
| Transformation Hook for health/beauty | Use **Lifestyle Upgrade framing**, NOT before/after | Meta policy compliance |
| Social Proof Hook | **Conditional only** — skip if no `existing_social_proof` | Prevents fabricating data |
| Budget plan dynamic | `timeline from Q2`, not hardcoded 30 days | |
| ABO vs CBO | ≥ 14 days → ABO; < 14 days → CBO | Learning phase feasibility |
| Lookalike conditional | If not yet launched → Broad Interest + Layer 3 behavioral | No website visitors to create lookalike from |
| Post-Launch Playbook | Section 9 (9A Revenue, 9B A/B Roadmap, 9C Decision Tree) | "Wow" differentiator — turns brief into 30-day playbook |

---

## What This Spec Is NOT

- This is **NOT** the SKILL.md that the AI agent reads at runtime.
- This is the **design spec for Supervisor review** — human-readable, explains intent and logic.
- The SKILL.md (for the agent to actually run) will be written later, after spec is approved.

---

## Scope Boundaries

**In MVP:**
- 3 mandatory ad scripts (+ up to 2 bonus)
- TA settings with 2-tier reasoning
- Budget plan (dynamic timeline, CPA benchmarks)
- Readiness Score check
- Post-Launch Playbook (Revenue Projection + A/B Roadmap + Decision Tree)

**Out of MVP (build later):**
- Retargeting campaigns
- Dynamic Creative
- Meta Ads Manager API integration

---

## Repo Structure

```
spec-build-for-master-ads/
├── SKILL.md              ← Runtime instructions (ClawHub reads this)
├── CLAUDE.md             ← Context reset anchor (this file)
├── logs/
│   ├── CHANGELOG.md       ← Project tracking + roadmap
│   ├── debug_log.md       ← Debug sessions + fixes
│   ├── testlog.md         ← Test results
│   └── live_test_on_openclaw_internal.md ← Live deployment evidence
├── README.md             ← GitHub-facing documentation
├── LICENSE               ← MIT 2026
├── .gitignore
├── spec/
│   └── spec.md           ← Supervisor-approved design spec
├── examples/
│   ├── input-sample.md   ← Sample product spec (fictional)
│   └── output-sample.md  ← Sample skill output
└── scripts/
    └── .gitkeep          ← Reserved for future automation
```

## File Ownership Rules

| File | Who Can Edit | How |
|---|---|---|
| `SKILL.md` | Claude proposes via PR, human reviews and merges | Never commit directly to main |
| `spec/spec.md` | Human only | — |
| `CLAUDE.md` | Human only | — |
| `README.md` | Claude may update when major changes occur | Human review before merge |
| `logs/CHANGELOG.md` | Claude updates after each work session | — |
| `logs/debug_log.md` | Claude updates as bugs are found/fixed | — |
| `logs/testlog.md` | Claude updates as tests are run | — |
| `logs/live_test_on_openclaw_internal.md` | Claude updates with live test evidence | — |
| `examples/` | Claude may create new files | Human review before merge |

