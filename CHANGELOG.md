# CHANGELOG — Meta Ads Script & TA Generator

---

## PART 1 — PROJECT SNAPSHOT

**Project:** Meta Ads Script & TA Generator — an OpenClaw skill that converts a product spec `.md` into a complete, execution-ready Meta Ads campaign package in a single Markdown output block.

**End goal:** Any Creative Producer or Media Buyer invokes the skill → gets ad scripts (3+ variants), TA settings with reasoning, budget plan, and a 30-day post-launch playbook — no follow-up questions needed.

**Current stage:** Spec Approved ✅ · Architecture Documented ✅ · SKILL.md Complete ✅ · 10/10 Tests Passing ✅ · Deployed on OpenClaw VPS ✅ · **Pending: Skill Card · AI Showcase · BUG-14 Fix (Q enforce on OpenClaw)**

---

## PART 2 — CHANGELOG

### [v0.3.0] - 2026-02-25

#### ✅ Added
- `examples/input-sample-ai.md` — Sample spec for a new AI SaaS product (NovaFlow AI), US market, $1,500/30d budget, team 3–4 people
- `examples/input-sample-incomplete.md` — Intentionally incomplete spec (Readiness Score ~3.5) to test Gate 1 HARD STOP behavior
- `feedback.md` — BGK competition feedback (private, gitignored)
- `debug_log.md` — Debug Session 4: BUG-14 recorded (agent skips Q1–Q4 on OpenClaw)

#### 🐛 Bugs Recorded
- **BUG-14 (🔴 Pending):** Agent ignores Q1–Q4 "Ask & Wait" gate when input spec is fully complete. Discovered during OpenClaw VPS deployment test with `input-sample-ai.md`. Fix strategy TBD.

---

### [v0.2.0] - 2026-02-24

#### ✅ Added
- `testlog.md` — 10 test cases (Round 1, 2, and 3) — all 10 passed
- `debug_log.md` — 3 debug sessions, 13 bugs tracked (BUG-01 through BUG-13), all fixed
- `examples/output-sample.md` — Full rewrite: Video 30s, 40/35/25→2 ad sets (60/40), Lead Gen revenue model, 4 variants complete, A/B Roadmap + Decision Tree Standard
- `examples/input-sample.md` — TaskFlow Pro sample input spec

#### 🐛 Bugs Fixed (Debug Session 1–3 / Batch 1–4)

| Bug | Severity | Fix Summary |
|---|---|---|
| BUG-01 | 🔴 Logic | Step 4: Video format selection now checks decision cycle (Q4=B → Static/Carousel) |
| BUG-02 | 🔴 Logic | Step 6: Q2=D (Ongoing) → monthly budget / 30-day review / ABO |
| BUG-03 | 🔴 Logic | Template 5G: 3 revenue models conditional on Q1 (Purchase / Lead Gen / Awareness) |
| BUG-04 | 🔴 Logic | Template 5F + Step 6: Hardcoded 40/35/25 budget split (was blank `<X>%`) |
| BUG-05 | 🔴 Logic | Budget consolidation: IF daily/ad set < CPA×10 OR total < $500/wk → 2 ad sets 60/40 |
| BUG-06 | 🔴 Currency | CPA table: VND → USD. Added currency mismatch fallback rule |
| BUG-07 | 🟡 Content | Removed all VND/Vietnam references from SKILL.md + spec/spec.md |
| FIX-07 | 🔴 Logic | Templates 5H + 5I: 3 timeline-adaptive variants (Sprint ≤13d / Standard 14–30d / Ongoing) |
| FIX-08 | 🔴 Logic | Template 5G + Step 6: Added Q1=D (App Install) → CPI/D7 Retention/ARPU model |
| FIX-09 | 🟡 Content | Step 6 CPA table: Added "Health / Beauty / Wellness $3–$10/lead" row + unmapped category fallback |
| BUG-10 | 🔴 Logic | Templates 5H + 5I: Sprint threshold extended from ≤7d → ≤13d to close the 8–13d gap |
| BUG-11 | 🟡 Content | output-sample.md: Full rewrite (Video 30s, 2 ad sets, Lead Gen model, all placeholders filled) |
| BUG-12 | 🟡 Edge | Section 3 Q2: VALIDATION note added — requires both budget amount AND timeline |
| BUG-13 | 🟡 Clarity | Step 1 score 8–10 branch: Added explicit ⚠️ ASSUMPTION flag instruction |

#### 💡 Decisions Made
- Sprint threshold extended to ≤13 days (not ≤7) to eliminate dead zone between Sprint and Standard
- Health/Beauty added as explicit CPA benchmark category (was previously forcing `⚠️ ASSUMPTION` on every health product)
- Q4=D (App Install) now has its own projection model — all 4 Q1 options are fully covered
- Constraint on Q2 partial answers formalized (previously undocumented)

---

### [v0.1.0] - 2026-02-24

#### ✅ Added
- `spec/spec.md` — Skill specification (English, Supervisor Approved)
- `SKILL.md` — Runtime instruction file for OpenClaw agent
- `CLAUDE.md` — Context reset anchor + System Architecture diagram (5 layers, 8 decision gates)
- `CHANGELOG.md` — This file

#### 💡 Decisions Made
- Separated `spec.md` (human-readable design doc) from `SKILL.md` (LLM-executable instructions)
- Used IF/THEN pseudo-code + stripped rationale columns in SKILL.md to conserve character budget
- Converted "Never Do" rules into positive-constraint form (`ONLY generate IF...`)
- Added explicit merge guardrail: agent must unify Q1–Q4 answers + spec.md before Step 1
- ASCII architecture diagram → `CLAUDE.md` only (saves ~3,500 chars from SKILL.md budget)

---

## PART 3 — ROADMAP

### 🔴 Immediate (Pending)

| Task | Complexity | Status |
|---|---|---|
| Fix BUG-14: Agent skips Q1–Q4 gate on OpenClaw | Hard | 🔴 Pending |
| Create `skill-card.md` (mandatory BGK deliverable) | Easy | 🔴 Pending |
| Create `ai-showcase/` folder with 3–5 screenshots | Medium | 🔴 Pending |

### 🟡 Upcoming (Presentation Prep)

| Task | Complexity | Depends On |
|---|---|---|
| Prepare real-data demo (internal product spec) | Medium | BUG-14 fixed |
| Compact SKILL.md: extract templates → `references/output-templates.md` | Medium | — |
| Consolidate duplicate constraints (Step 3 vs Section 6) | Easy | — |
| Submit Skill Card + AI Showcase before presenting | Easy | Both ready |
| Present to Judge: introduce skill, live demo, Q&A | Medium | All above done |

### 🟢 Backlog

| Task | Complexity | Depends On |
|---|---|---|
| Phase 2 Retargeting skill | Hard | Phase 1 live |
| Meta Ads Manager API integration | Hard | — |
