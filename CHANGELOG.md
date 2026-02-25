# CHANGELOG — Meta Ads Script & TA Generator

---

## PART 1 — PROJECT SNAPSHOT

**Project:** Meta Ads Script & TA Generator — an OpenClaw skill that converts a product spec `.md` into a complete, execution-ready Meta Ads campaign package in a single Markdown output block.

**End goal:** Any Creative Producer or Media Buyer invokes the skill → gets ad scripts (3+ variants), TA settings with reasoning, budget plan, and a 30-day post-launch playbook — no follow-up questions needed.

**Current stage:** Spec Approved ✅ · Architecture Documented ✅ · SKILL.md Complete ✅ · 10/10 Tests Passing ✅ · Deployed on OpenClaw VPS ✅ · Debug Session 4–5 Complete ✅ · Live Test Session 3 Complete ✅ (BUG-14 Closed · BUG-15 Closed · Gate C Closed) · Skill Card Created ✅ · **Pending: AI Showcase Curation**

---

## PART 2 — CHANGELOG

### [v0.6.0] - 2026-02-25

#### ✅ Bug Closed (Live Verified)
- **BUG-15: ✅ CLOSED on live** — Forced 4-Message Protocol (P0.0 patch) re-deployed to VPS. Test 3 confirmed: output splits into exactly 4 sequential messages with `[Message X/4]` headers, correct section boundaries (M1=Scripts, M2=TA, M3=Budget, M4=Playbook), and progress handoff markers. Wall-of-text symptom eliminated.

#### 🛠 Updated
- `SKILL.md` — BUG-15 fix upgraded from "3-message chunked delivery" to **Forced 4-Message Protocol**: explicit `[Message X/4]` headers, pre-send self-check rule, anti-merge rule, Q3=C conditional skip. Version remains 1.0.0. Line count: 528 → 531.
- `live_test_on_openclaw_internal.md` — Test 3 section added: pre-fix vs post-redeploy comparison table, acceptance check results table, final status for all items.
- `debug_log.md` — BUG-15 status updated (regression → closed). Debug Session 5 appended with closure evidence, acceptance criteria table, summary.
- `CHANGELOG.md` — Current stage line updated; BUG-15 VPS Re-deploy moved from Pending → Recently Completed.

#### 🧪 Live Test Results (Test 3 — OpenClaw VPS, patched v1.0.0)
- **BUG-14: ✅ No regression** — Q1–Q4 gate still holds on patched VPS.
- **BUG-15: ✅ CLOSED** — 4-message forced protocol verified in runtime behavior. `[Message 2/4]`, `[Message 3/4]`, `[Message 4/4]` markers visible in screenshots.
- **Evidence:** `ai_showcase/live_test_openclaw_internal/ss3_livetest_output.1.png` + `ss3_livetest_output.2.png`

#### 💡 Decisions Made
- Forced 4-Message Protocol uses 5 enforcement mechanisms: NON-NEGOTIABLE label, explicit `[Message X/4]` headers, pre-send self-check, anti-merge rule, Q3=C conditional skip — stronger than original 3-message chunked delivery.
- Line count accepted at 531 (31 over 500 target) — hard enforcement mechanisms justify the overhead; medium-risk cuts deferred.

---

### [v0.5.0] - 2026-02-25

#### ✅ Added
- `skill-card.md` — Mandatory BGK deliverable created. Sections: Problem, Before/After, What Gets Generated, What Makes This Different, How It Works, Quality Engineering, Input Requirements, Tools & AI Used, Limitations, Cost Per Run, Roadmap, Quick Start.

#### 🛠 Updated
- `skill-card.md` — Post-review fixes (P1/P2 issues): line count corrected (252→251), "0 revisions" softened to "Minimal — structured template", A/B roadmap labelled "timeline-adaptive: Sprint / Standard / Ongoing" (not "4-week plan"), Q3=C exception noted in Message 2 table. Cost table expanded with Input/Output columns + token methodology note. Proof links added to Quality Engineering section.
- `README.md` — Cost table expanded with Input/Output columns + token methodology note (mirrors skill-card.md).
- `SKILL.md` — Version bumped `"1.0"` → `"1.0.0"`.
- `live_test_on_openclaw_internal.md` — Test 2 (Ai Lipstick Spark App) documented: BUG-14 ✅, Gate C ✅, BUG-15 regression 🔴 noted.

#### 🧪 Live Test Results (OpenClaw VPS)
- **BUG-14: ✅ PASS** — Q1–Q4 gate confirmed on both SaaS (NovaFlow AI) and Beauty App (Ai Lipstick Spark App). Q4 domain-aware reframing observed as bonus behavior.
- **BUG-15: 🔴 Regression** — Wall of text still present on VPS (running pre-fix SKILL.md). Re-deployment pending.
- **Gate C: ✅ PASS** — Lifestyle Upgrade framing confirmed in beauty product output.

#### 💡 Decisions Made
- skill-card.md cost table uses 4-column format (Model / Input / Output / Total) with methodology note — provides verifiable evidence for BGK, not just a number.
- Token counts sourced from actual VPS deployment measurement (not estimate): 45k input (SKILL.md context) + 600 (spec) + 1,400 output.

---

### [v0.4.0] - 2026-02-25

#### ✅ Bugs Fixed (Debug Session 4)

| Bug | Fix | Root Cause | Fix Applied |
|---|---|---|---|
| BUG-14 | FIX-A | Agent defaulted to single-pass generation even on rich specs | 3-layer enforcement: CRITICAL INSTRUCTION block at top of file + Quick Start positive example + Common Mistakes negative reinforcement. STRICT RULE strengthened with ⛔ emoji + "non-negotiable" language |
| BUG-15 | FIX-B | Single-block output caused wall-of-text + broken table rendering in chat UIs | Chunked 3-message delivery in Step 7: Message 1 (Scripts) → Message 2 (TA + Budget) → Message 3 (Playbook), each ending with a progress marker |

#### 🛠 Improvements

| Fix | Area | Description | Line Δ |
|---|---|---|---|
| FIX-C | Section 6 | Audited 12 rules — 10 were duplicates of Step constraints. Replaced entire section with "Pre-Output Safety Check" containing only 2 unique rules (minors <18, sensitive category) | −9 lines |
| FIX-D | SKILL.md | Safe-group optimization: D1 (5H Ongoing inline), D3 (5I Ongoing inline), D5 (5E blank line), D6 (5F budget rules compact), D7 (YAML `requires.env` removed), D8 (5G code block blank lines + ⚠️ notes merged) | −40 lines |
| FIX-E | README.md | Full restructure to conversion funnel order: Why → What → Example → Cost → Install → Usage → Format → Requirements → License. Added "Why This Skill Exists" with before/after time table, FOMO psychology (anchoring, loss aversion, pattern interrupt), and 5-model cost-per-run pricing table | +28 lines |

**SKILL.md net result:** 533 → 528 lines (−5 net: +35 from FIX-A/B additions, −40 from FIX-C/D cuts)

#### 💡 Decisions Made
- 3-layer behavioral enforcement chosen for BUG-14 over single-rule approach — position + positive example + negative example cover all known LLM failure modes
- Chunked 3-message delivery splits natural content boundaries (Scripts / TA+Budget / Playbook) rather than arbitrary line counts
- FIX-D medium-risk cuts (D2: Revenue block merge; D4: Video 15s template compact) intentionally deferred — 28 lines over 500-line target accepted as tradeoff for FIX-A/B additions
- README conversion funnel: Awareness (Why) → Interest (What It Does) → Desire (Example Output) → Conviction (Cost) → Action (Install) — matches standard reader journey for developer tools

---

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
| Curate `ai_showcase/` — add `prompt_highlights/` + index/captions | Medium | 🔴 Pending |

### ✅ Recently Completed

| Task | Completed In | Notes |
|---|---|---|
| BUG-15 closed on live (4-message protocol verified) | v0.6.0 Live Test 3 | Forced 4-message protocol deployed + runtime verified |
| SKILL.md Forced 4-Message Protocol (P0.0 patch) | v0.6.0 | 5 enforcement mechanisms, 528→531 lines |
| Create `skill-card.md` (mandatory BGK deliverable) | v0.5.0 | Created + reviewed + overclaim fixes applied |
| BUG-14 live verified — PASS | v0.5.0 Live Test | Confirmed on SaaS + Beauty App product types |
| Gate C live verified — PASS | v0.5.0 Live Test | Lifestyle Upgrade framing confirmed on beauty output |
| Cost table methodology added (skill-card + README) | v0.5.0 | Token counts from real VPS measurement |
| Fix BUG-14: Agent skips Q1–Q4 gate on OpenClaw | v0.4.0 FIX-A | 3-layer enforcement |
| Fix BUG-15: Wall-of-text output | v0.4.0 FIX-B | 3-message chunked delivery (upgraded to forced protocol in v0.6.0) |
| Consolidate duplicate constraints (Section 6) | v0.4.0 FIX-C | 12 rules → 2 unique |
| Optimize SKILL.md size | v0.4.0 FIX-D | 533 → 528 lines |
| Rewrite README with FOMO psychology | v0.4.0 FIX-E | Conversion funnel structure |

### 🟡 Upcoming (Presentation Prep)

| Task | Complexity | Depends On |
|---|---|---|
| Curate ai_showcase/ with prompt_highlights/ + captions index | Medium | BUG-15 closed ✅ |
| Prepare real-data demo (internal product spec) | Medium | ai_showcase curated |
| Submit Skill Card + AI Showcase before presenting | Easy | Both ready |
| Present to Judge: introduce skill, live demo, Q&A | Medium | All above done |

### 🟢 Backlog

| Task | Complexity | Depends On |
|---|---|---|
| Phase 2 Retargeting skill | Hard | Phase 1 live |
| Meta Ads Manager API integration | Hard | — |
