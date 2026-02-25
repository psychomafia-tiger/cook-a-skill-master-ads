# DEBUG DIARY — Meta Ads Script & TA Generator

> A log to track bugs found during testing and the progress of fixing them. This file keeps the team aligned and prevents confusion when addressing multiple bugs consecutively.

---

## 📅 [2026-02-24] Debug Session 1: Testlog Review & SKILL.md Logic Holes

### 🔴 Critical Bugs to Fix

- [x] **BUG-02 (Logic):** `Q2 = D (Ongoing)` breaks the daily budget calculation.
  - *Fixed:* Step 6 now handles Q2=D: requires monthly budget, daily = monthly/30, ABO, 30-day review cycle.
- [x] **BUG-03 (Logic):** Revenue Projection (5G) template used wrong flow for Lead Gen and Awareness.
  - *Fixed:* Template 5G now has 3 conditional models: Purchase (Leads→CVR→Purchases), Lead Gen (Leads→Lead-to-Customer Rate→LTV), Awareness (Reach/Impressions/CPM).
- [x] **BUG-04 (Logic):** Budget Split `<X>%` was blank — agent invented random ratios.
  - *Fixed:* Hardcoded default 40% Broad / 35% Interest / 25% LAL in both Step 6 and Template 5F.
- [x] **BUG-05 (Logic):** Small budgets split across 3 ad sets can't exit Learning Phase.
  - *Fixed:* Added two safeguards in Step 6 + Template 5F: (1) IF daily/ad set < CPA×10 → consolidate to 2 ad sets 60/40, (2) IF total < $500/week → force 2 ad sets.
- [x] **BUG-06 (Currency/Market):** CPA benchmark table was VND-only.
  - *Fixed:* Replaced entire table with USD benchmarks. Added fallback rule: if currency mismatch → convert + flag ⚠️ ASSUMPTION.

### 🟡 Test Coverage Gaps — Addressed (Pending Re-simulation)

- [x] **TEST-GAP-01:** `TEST-06` checklist updated — added Gate A (sensitive category: health) check.
- [x] **TEST-GAP-02:** `TEST-01` checklist updated — added Step 2 decision cycle verification + Revenue Projection model check.
- [x] **TEST-GAP-03:** Added `TEST-07` — Q3=B (Raw video available → Skip Production Notes).
- [x] **TEST-GAP-04:** Added `TEST-08` — Q1=A (Awareness → Manual Placements + Reach/CPM projection).
- [x] **TEST-GAP-05:** Added `TEST-09` — Q2=D (Ongoing → monthly budget / 30-day review).

---

## 🕒 Fix History (Done)

### Batch 1 — SKILL.md Logic Patches [2026-02-24]

| Bug | File | Lines Changed | What Changed |
|---|---|---|---|
| BUG-01 | SKILL.md Step 4 | L128 | Added Static Ad differentiation instruction for Q4=B |
| BUG-02 | SKILL.md Step 6 | L153–156 | Added Q2=D → monthly budget / 30-day review cycle |
| BUG-03 | SKILL.md Template 5G | L307–354 | 3 conditional projection models by Q1 (Purchase/Lead Gen/Awareness) |
| BUG-04 | SKILL.md Step 6 + Template 5F | L160–163, L301–305 | Hardcoded 40/35/25 split ratios |
| BUG-05 | SKILL.md Step 6 + Template 5F | L165–167, L308 | Min budget warning + auto-consolidate to 2 ad sets |
| BUG-06 | SKILL.md Step 6 | L170–180 | CPA table VND → USD, added currency mismatch rule |

---

## 📅 [2026-02-24] Debug Session 2: Round 2 Review — 6 Remaining Issues

### Phase Plan

| Phase | Issues | Severity | Target Files |
|---|---|---|---|
| Phase 1 | FIX-07 Playbook adaptive timeline + FIX-08 Q1=D App Install model | High | SKILL.md |
| Phase 2 | TEST-03 budget consolidation gap + TEST-06 budget + CPA mapping gap | Medium | testlog.md |
| Phase 3 | FIX-09 Health/beauty CPA category + TEST-10 partial Q answers | Low | SKILL.md + testlog.md |

---

### Phase 1 — High Severity Fixes [2026-02-24] ✅ DONE

#### FIX-07: Playbook Adaptive Timeline (5H + 5I)

**Problem:** A/B Test Roadmap (5H) and Decision Tree (5I) were hardcoded to 4-week structure. A 7-day campaign gets "Day 14: Scale" advice that doesn't exist. An Ongoing campaign gets a plan that ends at Week 4 with no continuation.

**Root cause:** Templates assumed timeline ≥ 14 days. No conditional branching by Q2.

**Fix applied:**
- **5H (A/B Test Roadmap)** — 3 variants:
  - Sprint (≤7 days): Day 1–2 Hook Test → Day 3 First Kill → Day 4–5 Winner → Day 6–7 All-In
  - Standard (14–30 days): Original Week 1–4 (unchanged)
  - Ongoing (Q2=D): Rolling 30-day cycles + creative refresh + retargeting transition
- **5I (Decision Tree)** — 3 variants:
  - Sprint: Checkpoints at Day 2, 3, 5, 7 only
  - Standard: Original Day 3/7/14/21–30 (unchanged)
  - Ongoing: Standard per cycle + Day 30 cycle review row

**Impact:** All Q2 options produce timeline-appropriate Playbook. Media Buyer no longer receives impossible advice.

---

#### FIX-08: Q1=D App Install Revenue Model (5G) + CPI Benchmark

**Problem:** Q1 has 4 options but 5G only had 3 projection models. App Install uses CPI, D7 retention, ARPU — different from leads or purchases.

**Fix applied:**
- **5G:** Added `IF Q1 = D (App Install)` block with: Installs → D7 Retention → Active Users → ARPU → ROAS
- **Step 6 CPA table:** Added `App Install | $1–$5/install`

**Impact:** All 4 Q1 options now have matching projection models.

---

### Phase 1 Fix History

| Fix | File | Section | What Changed |
|---|---|---|---|
| FIX-07 | SKILL.md | 5H, 5I | 3 timeline-adaptive variants each (Sprint/Standard/Ongoing) |
| FIX-08 | SKILL.md | 5G, Step 6 | App Install projection model + CPI benchmark row |

---

### Phase 2 — Medium Severity Fixes (testlog.md) [2026-02-24] ✅ DONE

#### GAP-R3-01: TEST-03 Missing Budget Consolidation Check

**Problem:** TEST-03 ($500/7d = $71.43/day) has same daily budget as TEST-01 ($1,000/14d = $71.43/day). TEST-01 correctly documents budget consolidation triggering. TEST-03 says "correct budget split ratios (40/35/25)" without mentioning consolidation. Inconsistent — same math, different conclusions.

**Fix applied:** Updated TEST-03 Expected checklist:
- Added: budget consolidation check ($28.57/$25/$17.86 per ad set < CPA×10 $50 → consolidate)
- Added: A/B Roadmap Sprint variant verification (7-day timeline)
- Added: Decision Tree Sprint variant verification
- Updated Actual Output with consolidation math + Sprint Playbook confirmation

---

#### GAP-R3-02: TEST-06 Missing Budget Consolidation + CPA Category Mapping

**Problem:** TEST-06 ($500/14d = $35.71/day, health/beauty) had two gaps:
1. Budget: $250/week < $500/week → low-budget rule triggers. Per-ad-set: $14.29 < $50 → also triggers. Neither mentioned.
2. CPA mapping: "health/beauty" not in CPA benchmark table → agent should map to closest category or flag assumption. Not verified.

**Fix applied:** Updated TEST-06 Expected checklist:
- Added: CPA category mapping check (health/beauty → mapped to closest + `⚠️ ASSUMPTION` flag)
- Added: budget consolidation check (both rules trigger → 2 ad sets)
- Updated Actual Output with both verifications

---

### Phase 2 Fix History

| Gap | File | Test | What Changed |
|---|---|---|---|
| GAP-R3-01 | testlog.md | TEST-03 | Added budget consolidation + Sprint Playbook checklist items |
| GAP-R3-02 | testlog.md | TEST-06 | Added budget consolidation + CPA mapping checklist items |

---

### Phase 3 — Low Severity Fixes [2026-02-24] ✅ DONE

#### FIX-09: Health/Beauty CPA Category in Benchmark Table

**Problem:** CPA benchmark table had no "Health / Beauty / Wellness" row. TEST-06 showed the agent had to guess-map health/beauty to "SaaS/App" — workable but fragile. Every health/beauty campaign would trigger an assumption flag unnecessarily.

**Fix applied:**
- **Step 6 CPA table:** Added `Health / Beauty / Wellness | $3–$10/lead`
- **Step 6 fallback rule:** Added explicit instruction: "IF product_category does not match any row exactly → map to closest category and flag with ⚠️ ASSUMPTION." (Previously only currency mismatch had a fallback rule; now category mismatch also has one.)

**Impact:** Health/beauty products now get a direct CPA benchmark. All other unmapped categories get a clear fallback instruction instead of relying on agent improvisation.

---

#### TEST-10: Partial Q Answers Edge Case

**Problem:** No test verified that the agent refuses to generate output when the user provides only 2 of 4 required Q answers. Two enforcement points exist (Section 3 hard rule + Section 6 constraint), but neither was tested.

**Fix applied:**
- **testlog.md:** Added TEST-10 — user provides Q1 + Q2, skips Q3 + Q4, requests generation. Expected: agent refuses, lists missing Qs, waits. Verified both enforcement points converge.

**Impact:** Confirms the "generate ONLY after ALL answers received" rule is testable and enforceable.

---

### Phase 3 Fix History

| Fix | File | Section | What Changed |
|---|---|---|---|
| FIX-09 | SKILL.md | Step 6 CPA table | Added Health/Beauty/Wellness row + category mismatch fallback rule |
| TEST-10 | testlog.md | New test | Partial Q answers enforcement test (Q1+Q2 only → agent refuses) |

---

## 📅 [2026-02-24] Debug Session 3: Final Deployment Audit — 4 Issues Found

### Context

Full token analysis + logic simulation performed from customer perspective before deployment approval. Token budget: ~10,000 tokens/run (6,800 input + 3,000 output). Fits 32K+ context windows. No rate limit risk for normal use. Cost ~$0.05–0.07/run on Sonnet/GPT-4o.

---

### 🔴 BUG-10 (Logic — Medium): Timeline 8–13 Days Has No Playbook Template

**Problem:** Q2 lists timeline options (A) 7d / (B) 14d / (C) 30d / (D) Ongoing. Nothing prevents a user from entering a freeform timeline like "10 days" or "2 weeks" (14 days is fine, but "12 days" is not). Templates 5H and 5I only cover Sprint (≤7d), Standard (14–30d), and Ongoing. A timeline of 8–13 days has no matching variant. Agent must improvise — output becomes inconsistent.

**Root cause:** Sprint threshold is "≤7 days" with a hard cutoff, leaving an 8–13d gap before Standard begins at 14d.

**Fix applied:**
- **5H (A/B Test Roadmap):** Changed `IF timeline ≤ 7 days (Sprint)` → `IF timeline ≤ 13 days (Sprint)`. Template label updated from "Sprint (≤7 days)" → "Sprint (≤13 days)".
- **5I (Decision Tree):** Changed `IF timeline ≤ 7 days (Sprint)` → `IF timeline ≤ 13 days (Sprint)`.
- Sprint roadmap now covers 8–13d gap without introducing a new variant — simpler and consistent with Sprint logic.

**Status:** ✅ Fixed [2026-02-24]

---

### 🟡 BUG-11 (Content — Medium): output-sample.md Is Outdated — Contradicts Current SKILL.md

**Problem:** The output sample file has 3 incorrect/incomplete points:
1. **Variant A shows "Video 15s"** — TaskFlow Pro is SaaS = considered decision cycle → should be **Video 30s** (per BUG-01 fix applied in Step 4).
2. **Budget table shows 30/40/30 split** — current SKILL.md default is **40/35/25** (per BUG-04 fix).
3. **Variants B, C, Revenue Projection, A/B Roadmap, Decision Tree are all "[placeholder]"** — customer sees an incomplete, non-functional sample on first contact with the repo.

**Root cause:** output-sample.md was written before Batch 1–4 fixes and never updated to reflect changes.

**Impact:** First impression failure. User evaluating the skill before deploying sees contradictions between the sample and the instructions.

**Fix applied:**
- Rewrote entire `output-sample.md` from scratch using Opus 4.6.
- Variant A: Video 15s → **Video 30s** (HOOK/PROBLEM/SOLUTION/CTA structure per 5B-2)
- Budget split: 30/40/30 → **2 ad sets 60/40** (consolidation triggered: $28.57/ad set < CPA $5 × 10 = $50)
- All 4 placeholders filled: Variant B (Static), Variant C (Carousel 5 slides), Revenue Projection (Lead Gen model, LTV $84), A/B Roadmap (Standard), Decision Tree (Standard)
- Added Variant D (Social Proof Hook — Video 15s) since `existing_social_proof` is present in input spec
- All content uses TaskFlow Pro data: pricing, features, social proof, brand colors

**Status:** ✅ Fixed [2026-02-24]

---

### 🟡 BUG-12 (Edge — Low): Q2 Freeform Input Can Be Partially Missing

**Problem:** Q2 asks for both a budget amount AND a timeline in one answer. A user could reply with only one part ("B" for 14 days, missing budget amount) or only the other ("$1,000", missing timeline). SKILL.md has no instruction telling the agent to ask again if either part is absent. Agent may proceed with an assumed value or default to 0.

**Fix applied:**
- **Section 3, Q2:** Added VALIDATION note immediately after Q2 question: "Q2 requires BOTH a budget amount AND a timeline. IF the user's reply contains only one part → ask for the missing part before proceeding. Do not assume or default either value."
- Also fixed missing closing `"` on Q2 question text.

**Status:** ✅ Fixed [2026-02-24]

---

### 🟡 BUG-13 (Clarity — Low): Step 1 Score 8–10 Branch Does Not Mention Flagging

**Problem:** Step 1 defines 3 score branches:
- Score 8–10 → "proceed, generate full output" (no mention of flagging)
- Score 5–7 → "proceed, but flag EVERY assumption" (explicit)
- Score < 5 → hard stop

Section 6 says "ALWAYS flag assumptions wherever data is missing or vague." These are not technically contradictory, but an agent reading Step 1 first may treat "generate full output" as meaning "no special handling needed" — and skip flagging because the 5–7 branch, not the 8–10 branch, is where flagging is described.

**Concrete failure scenario:** 1 required field missing (0 pts) + 5 clear + 1 optional = 8.5 → score 8–10 → agent proceeds without flagging the missing field.

**Fix applied:**
- **Step 1, score 8–10 branch:** Changed from `"proceed, generate full output."` → `"proceed, generate full output. Still apply ⚠️ ASSUMPTION flags wherever any field is missing or vague (per Section 6)."`
- Now explicitly consistent with Section 6 rule — no ambiguity regardless of which branch fires.

**Status:** ✅ Fixed [2026-02-24]

---

### Debug Session 3 — Issue Summary

| Bug | Severity | File | Type | Status |
|---|---|---|---|---|
| BUG-10 | 🔴 Medium | SKILL.md 5H + 5I | Logic gap — no template for 8–13d timeline | ✅ Fixed — Sprint threshold extended to ≤13 days |
| BUG-11 | 🟡 Medium | output-sample.md | Content outdated — wrong format, wrong split, 4 placeholders | ✅ Fixed |
| BUG-12 | 🟡 Low | SKILL.md Section 3 | Edge — Q2 partial answer not handled | ✅ Fixed — VALIDATION note added after Q2 |
| BUG-13 | 🟡 Low | SKILL.md Step 1 | Clarity — flag instruction missing from 8–10 branch | ✅ Fixed — flagging note added to 8–10 branch |

### Debug Session 3 — Fix History

| Fix | File | Section | What Changed |
|---|---|---|---|
| BUG-10 | SKILL.md | 5H, 5I | Sprint threshold ≤7d → ≤13d; template label updated in 5H |
| BUG-12 | SKILL.md | Section 3 (Q2) | VALIDATION note added: Q2 requires both budget + timeline; closes missing closing `"` too |
| BUG-13 | SKILL.md | Step 1 | Score 8–10 branch now includes: "Still apply ⚠️ ASSUMPTION flags per Section 6" |
| BUG-11 | output-sample.md | Entire file | ✅ Fixed — Full rewrite: Video 30s, 40/35/25→2 ad sets 60/40, Lead Gen model, all sections filled |

---

## 📅 [2026-02-25] Debug Session 4: OpenClaw Deployment Testing

### Context

Deployment method: Manual copy via folder transfer to OpenClaw running locally on a VPS (not via github/clawd cli).

---

### 🔴 BUG-14 (Prompt Adherence — High): Agent Skips Q1–Q4 on OpenClaw Deployment

**Problem:** When testing the skill on the actual OpenClaw platform (using `input-sample-ai.md`), the agent ignored the strict instruction to ask questions 1–4 and wait for the user's reply. Instead, it proceeded straight to generating the campaign output using assumed or omitted values.

**Root cause:** The "Ask & Wait" constraint is present in `SKILL.md` (Section 3 and Section 6), but the LLM powering OpenClaw is eagerly completing the task (likely due to seeing a fully-formed, rich spec). The instruction to "STOP and wait" is not strong enough to break the agent's default instruction-following momentum on a rich input.

**Fix applied (2026-02-25):** 3-layer enforcement added to SKILL.md:

- **Layer 1 — CRITICAL INSTRUCTION block** (lines 17–26): Added a blockquote immediately after the file title, before any section. States explicitly: "This skill is a multi-turn conversation, NOT a single-pass generator." Lists 4 steps the agent MUST follow: read spec → ask Q1–Q4 in one message → STOP → wait for all answers → then generate.
- **Layer 2 — Quick Start Example** (lines 28–37): Added a concrete 4-turn conversation flow showing exactly what Turn 1–4 look like. Provides a positive pattern for the agent to mirror instead of relying only on rule-based prohibitions.
- **Layer 3 — Common Mistakes** (lines 39–43): Added a "DO NOT do these" list with 3 specific wrong behaviors labeled **WRONG**: jumping to output on a rich spec, generating partial output while waiting, and assuming budget/timeline from spec data.
- **Reinforcement — STRICT RULE** (line 103): Upgraded existing plain-text rule by adding ⛔ emoji, "STOP and WAIT" phrasing, explicit reference to "Section 4", and the phrase "non-negotiable".

**Root cause addressed:** The original instruction ("STRICT RULE: Generate ONLY after ALL answers are received.") was a single line at the end of Section 3 — too easy to overlook when the agent sees a rich spec and defaults to task completion. The fix repositions enforcement to the very top of the file (highest attention priority) and adds pattern-based guidance to complement the rule-based prohibition.

**Status:** ✅ Fixed [2026-02-25]

---

### 🟡 BUG-15 (UX — Medium): Output Renders as Wall of Text with Broken Tables

**Problem:** When the agent generates the full campaign package in a single message, the output is a monolithic wall of text (~3,000+ tokens). Tables within the output (TA Interest Stack, Budget Plan, Revenue Projection, Decision Tree) render broken or unformatted in most chat UIs. Users cannot parse or copy individual sections easily.

**Root cause:** Step 7 instructed the agent to "Begin the output with the Executive Summary. Then output all applicable sections in order" — implying a single continuous block. No guidance on message splitting or formatting boundaries.

**Fix applied (2026-02-25):**
- **Step 7 — Chunked Format instruction** (lines 225–238): Added mandatory 3-message delivery rule:
  - Message 1: Executive Summary + ALL Ad Script variants (5A → 5B/5C/5D) → ends with `"📋 Scripts done. Sending TA & Budget next..."`
  - Message 2: TA Settings + Budget Plan (5E → 5F) → ends with `"📋 TA & Budget done. Sending Playbook next..."`
  - Message 3: Revenue Projection + A/B Roadmap + Decision Tree (5G → 5H → 5I) → ends with `"✅ Campaign package complete."`
- **Quick Start Example** (lines 36–38): Updated Turn 4 → Turn 4/5/6 to show 3-message output pattern, consistent with chunked delivery.
- **Q3=C handling**: Message 2 skips TA Settings but still sends as separate message (Budget Plan only).

**Root cause addressed:** Single-message output caused chat UI rendering failures. Chunked delivery keeps each message under ~1,000 tokens, allowing tables to render correctly and giving users natural copy boundaries between sections.

**Status:** ✅ Fixed [2026-02-25]

---

### FIX-C (Optimization): Section 6 Consolidated — 10 Duplicate Rules Removed

**Problem:** Section 6 "Strict Constraints" contained 12 rules. 10 of them were exact duplicates of rules already stated in Steps 1–7, Section 3, and templates. Duplication wastes tokens (~150 tokens), creates inconsistency risk (updating one location but not the other), and adds no enforcement value.

**Audit results:**

| Section 6 Rule | Already Stated At | Duplicate? |
|---|---|---|
| Flag ⚠️ ASSUMPTION | Step 1 (L120-121), Step 6 (L214, L216) | ✅ |
| A/B test note per variant | Template 5B (L289) | ✅ |
| 3-angle reasoning for Tier 1 | Step 5 (L168), Template 5E (L326) | ✅ |
| Budget from Q2 only | Step 6 context | ✅ |
| Output after ALL Q1-Q4 | Critical Instruction (L23), STRICT RULE (L105) | ✅ ×3 |
| Readiness Score ≥ 5 | Step 1 (L122) | ✅ |
| Q1 objective = user choice | Section 3 Q1 (L80-85) | ✅ |
| Social Proof Hook conditional | Step 3 (L143) | ✅ |
| Production Notes Q3≠B | Step 7 (L222) | ✅ |
| Health/beauty Lifestyle Upgrade | Step 3 (L146) | ✅ |
| Minors < 18 confirmation | **Unique** | ❌ |
| Sensitive category confirmation | **Unique** | ❌ |

**Fix applied (2026-02-25):**
- Removed all 10 duplicate rules from Section 6.
- Renamed section: "6. Strict Constraints" → "6. Pre-Output Safety Check".
- Retained 2 unique rules (minors + sensitive category) as the only content under Section 6.
- Removed orphaned "per Section 6" reference in Step 1 (L120).
- Net result: **-9 lines** (577 → 568).

**Status:** ✅ Fixed [2026-02-25]

---

### FIX-D (Optimization): SKILL.md Line Reduction — Safe Group

**Problem:** After FIX-A/B/C, SKILL.md was at 568 lines (68 over the 500-line recommendation). Feedback identified bloated sections that could be compacted without losing functional content.

**Fix applied (2026-02-25) — safe-only cuts:**

| ID | Target | Action | Lines Saved |
|---|---|---|---|
| D7 | YAML frontmatter | Removed empty `requires.env: []` | -2 |
| D1 | 5H Ongoing variant | Collapsed 16-line code block → 1-line inline summary (content preserved) | -15 |
| D3 | 5I Ongoing variant | Collapsed 7-line block → 1-line inline (content preserved) | -5 |
| D5 | 5E TA Settings | Removed 1 unnecessary blank line before Phase 2 teaser | -1 |
| D6 | 5F Budget Plan | Merged Learning Phase + Min budget + 7-day rule into 2 compact lines | -3 |
| D8+ | 5G Revenue Projection | Removed blank lines inside code blocks (4 blocks × ~2 each) + merged 2 ⚠️ notes into 1 | -12 |
| | | **Total** | **-40 lines** |

**Result:** 568 → **528 lines** (28 over 500-line target — remaining gap requires medium-risk cuts D2/D4 which were intentionally deferred).

**What was NOT cut (and why):**
- D2 (merge Revenue Projection blocks): agent must parse branching inside a single template — risk of wrong model selection
- D4 (compact Video 15s template): reduces template readability for marginal gain (~8 lines)

**Status:** ✅ Fixed [2026-02-25]

---

### FIX-E (Documentation): README "Why This Skill Exists" Section

**Problem:** README opened with "What It Does" — functional but flat. No business context, no urgency, no reason for a reader to stop scrolling. Feedback: "README nên mở đầu bằng business context."

**Fix applied (2026-02-25):**
- Added "Why This Skill Exists" section (lines 5–33) between tagline and "What It Does"
- **Before/After table**: 4-row comparison showing manual time (2–3 days) vs skill time (< 2 minutes) — anchoring effect
- **Cost per run table**: 5 models with exact token costs ($0.027–$0.263) — specificity builds trust
- **Freelancer price contrast**: "$500–$2,000 for the same scope" vs $0.16 — price anchoring (6,250x cheaper)
- **Loss aversion closer**: "Every campaign you plan manually is time you can't get back."
- Behavioral psychology techniques used: anchoring, loss aversion, ego preservation ("time, not talent"), pattern interrupt ("That's not a typo")

**Status:** ✅ Fixed [2026-02-25]

---

### Debug Session 4 — Issue Summary

| Bug | Severity | File | Type | Status |
|---|---|---|---|---|
| BUG-14 | 🔴 High | SKILL.md | Prompt adherence — agent skips Q1–Q4 on rich spec input | ✅ Fixed — 3-layer enforcement added at top of file |
| BUG-15 | 🟡 Medium | SKILL.md | UX — output wall of text, tables broken in chat | ✅ Fixed — 3-message chunked delivery in Step 7 |
| FIX-C | 🟡 Optimization | SKILL.md | 10 duplicate rules in Section 6 wasting tokens + inconsistency risk | ✅ Fixed — consolidated to 2 unique rules |
| FIX-D | 🟡 Optimization | SKILL.md | File too long (568 lines, target < 500) | ✅ Partial — 528 lines (-40), safe cuts only |
| FIX-E | 🟢 Documentation | README.md | Missing business context + cost transparency | ✅ Fixed — "Why This Skill Exists" + cost table added |

### Debug Session 4 — Fix History

| Fix | File | Lines Changed | What Changed |
|---|---|---|---|
| BUG-14 | SKILL.md | Lines 17–44 (new) | CRITICAL INSTRUCTION block + Quick Start Example + Common Mistakes |
| BUG-14 | SKILL.md | Line 103 (updated) | STRICT RULE strengthened: ⛔ emoji + "STOP and WAIT" + "non-negotiable" |
| BUG-15 | SKILL.md | Lines 225–238 (new) | Chunked output: 3 sequential messages with preview lines |
| BUG-15 | SKILL.md | Lines 36–38 (updated) | Quick Start Turn 4 → Turn 4/5/6 reflecting chunked delivery |
| FIX-C | SKILL.md | Section 6 (rewritten) | 12 rules → 2 unique rules; renamed to "Pre-Output Safety Check"; -9 lines |
| FIX-C | SKILL.md | Line 120 (updated) | Removed orphaned "per Section 6" reference |
| FIX-D | SKILL.md | YAML, 5H, 5I, 5E, 5F, 5G | Safe-group compaction: -40 lines (568 → 528) |
| FIX-E | README.md | Lines 5–33 (new) | "Why This Skill Exists" section: before/after table + cost table + FOMO framing |

---

## 📅 [2026-02-25] Live Test Verification — OpenClaw VPS

### Context

Live deployment tests after Debug Session 4 fixes were applied. Conducted via **Telegram bot interface** on internal VPS. Two specs tested across different product categories.

Evidence: `screenshot_test_openclaw_skill/` · `live_test_on_openclaw_internal.md`

---

### ✅ BUG-14 — Live Verification: PASS (Confirmed across 2 product types, Tests 1 & 2)

**Test 1 — NovaFlow AI (SaaS, fictional, `input-sample-ai.md`):**
- Agent asked Q1–Q4 in one message and STOPPED. No premature output. ✅

**Test 2 — Ai Lipstick Spark App (Beauty App, real internal spec, `spec_lipstick_ai_product.md`, 2.9 KB):**
- BUG-14 holds on a different product category. ✅
- Agent correctly extracted product name + market from spec before asking Q1–Q4.
- **Bonus observation — Q4 domain-aware reframing:** Agent adapted Q4 to *"Team có thể quay video người thật (UGC/Creator) hay chỉ làm motion/MGUK không?"* — not the generic template phrasing. Contextual adaptation working beyond spec.

**Conclusion:** 3-layer enforcement (CRITICAL INSTRUCTION + Quick Start example + Common Mistakes) is robust. BUG-14 officially closed on live.

---

### ✅ BUG-15 — Live Closure: CLOSED (Test 3, patched VPS)

**Test 1 + Test 2 — Pre-fix (regression observed):**
- Full campaign package delivered in one monolithic message. Tables rendered as raw pipe characters. Wall-of-text UX confirmed on both runs.
- Root cause: VPS was running pre-fix SKILL.md (v0.4.0 FIX-B chunk intent but not enforced hard enough).

**Test 3 — Post-redeploy (patched SKILL.md v1.0.0, forced 4-message protocol):**
- Output correctly split into **4 sequential messages** with `[Message X/4]` headers.
- Message boundaries matched spec: M1 = Scripts, M2 = TA Settings, M3 = Budget Plan, M4 = Playbook.
- Progress handoff markers present at end of M1–M3.
- BUG-15 symptom (monolithic wall-of-text) eliminated.
- Screenshot evidence: `ai_showcase/live_test_openclaw_internal/ss3_livetest_output.2.png`

**Status:** ✅ Closed on live [2026-02-25] — patched VPS, 4-message forced protocol verified.

---

### ✅ Gate C — Live Verification: PASS (Beauty product)

**Test 2 — Ai Lipstick Spark App:**
- Transformation Hook in generated output uses lifestyle/confidence framing. No before/after body imagery detected. Meta policy compliance confirmed.

---

### Live Test — Findings Summary (Tests 1 & 2)

| Item | Result | Status |
|---|---|---|
| BUG-14 — SaaS (Test 1) | Q1–Q4 gate holds | ✅ Closed |
| BUG-14 — Beauty App (Test 2) | Q1–Q4 gate holds, Q4 domain-aware | ✅ Closed |
| BUG-15 — Both tests | Wall of text persists on VPS (pre-fix) | ✅ Closed (Test 3) |
| Gate C — Beauty App | Lifestyle Upgrade framing confirmed | ✅ Closed |

---

## 📅 [2026-02-25] Debug Session 5: BUG-15 Live Re-Test on Patched VPS

### Context

Re-deployed patched `SKILL.md` (v1.0.0, 531 lines) to OpenClaw VPS after implementing the **Forced 4-Message Protocol** (P0.0 patch). This session closes BUG-15 on live.

**SKILL.md changes since last VPS deploy:**
- BUG-15 upgrade: 3-message chunked delivery → **forced 4-message protocol** with hard enforcement (P0.0)
  - Added explicit `[Message X/4]` headers per message
  - Added pre-send self-check rule (do NOT merge cross-message content)
  - Added anti-merge rule (do NOT combine M2 + M3 even if short)
  - Added Q3=C conditional skip (skip M2 entirely, send one-line note)
- Version bump: `1.0` → `1.0.0`

---

### ✅ BUG-15 — Live Re-Test: CLOSED

**Evidence:** `ai_showcase/live_test_openclaw_internal/ss3_livetest_output.1.png` + `ss3_livetest_output.2.png`

**Acceptance criteria — all PASS:**

| Check | Result |
|---|---|
| Output split into exactly 4 messages | ✅ |
| `[Message X/4]` headers present on all messages | ✅ |
| M1 = Confirmation + Summary + Scripts boundary | ✅ |
| M2 = TA Settings only boundary | ✅ |
| M3 = Budget Plan only boundary | ✅ |
| M4 = Post-Launch Playbook boundary | ✅ |
| Progress handoff markers (`Scripts done...` / `TA done...` / `Budget done...`) | ✅ |
| BUG-14 gate still holding on patched VPS | ✅ |
| No missing sections after 4-way split | ✅ |

**Final status:** BUG-15 ✅ Closed on live [2026-02-25].

---

### Debug Session 5 — Summary

| Item | Status |
|---|---|
| BUG-15 VPS re-deploy | ✅ Done |
| BUG-15 live smoke test | ✅ PASS |
| BUG-15 evidence captured | ✅ 2 screenshots in ai_showcase/ |
| BUG-14 regression check on patched VPS | ✅ No regression |
| Documentation sync (P0.5) | ✅ Done |
