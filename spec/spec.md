# Skill Spec: Meta Ads Script & TA Generator
Version: 0.1 | Owner: Tiger
Platform: Meta Ads (Facebook / Instagram)
Status: Supervisor Approved

---

## 1. Problem Statement

Every time a new product campaign is prepared, Creative Producers
must brainstorm scripts from scratch and set up target audience (TA) based on intuition.

Consequences:
- 1–3 days wasted just to produce an ads brief
- TA settings lack logic → budget burn in early phase
- Scripts lack diversity → insufficient variants for A/B testing from day one
- Inaccurate briefs → team asks back multiple times → delayed go-live

---

## 2. Skill Overview

Input: product spec .md file
→ Clarifying questions → Generate detailed ad scripts
(multiple formats) + TA settings with reasoning + budget plan
+ post-launch playbook
→ Output: 1 complete markdown block, ready for team execution immediately.

---

## 3. Target Users

Creative Producer / Marketing Manager / Growth team.
Prerequisite: User already has a product spec .md file.

---

## 4. Input Requirements

### 4.1 File spec .md — Required Fields

| Field | Description | Usage in Skill |
|---|---|---|
| product_name | Product name | Appears in all outputs |
| value_proposition | Core benefit (1–2 sentences) | Foundation for all script bodies |
| target_persona | Target user description | Derive TA settings |
| product_category | Product type (SaaS/ecom/app...) | Select correct campaign objective |
| key_features | 3–5 main features | Raw material for benefit hooks |
| market | Market (NA / EU / Global) | Calibrate cultural context in TA |

### 4.2 Optional Fields

| Field | Description | Impact When Missing |
|---|---|---|
| pricing | Product pricing | Cannot derive income bracket in TA |
| competitors | Competitors | Cannot use Contrast Hook |
| tone_of_voice | Brand tone | Defaults to neutral-professional |
| existing_social_proof | Reviews, user count, awards... | Cannot use Social Proof Hook |
| visual_direction | Visual direction | Production notes left blank |

### 4.3 Clarifying Questions (Mandatory)

Before generating any output, the skill MUST ask
4 core (mandatory) questions below. If spec.md is missing
landing_page_url or brand_name, the skill may ask up to
2 additional questions bundled with the 4 core questions.

**Q1 — Objective:**
> "What is the primary objective of this campaign?
> (A) Awareness
> (B) Lead Generation
> (C) Conversion / Purchase
> (D) App Install"

**Q2 — Budget & Timeline:**
> "What budget can you allocate for this campaign?
> And how long do you plan to run it?
> (A) 7 days  (B) 14 days  (C) 30 days  (D) Ongoing
> (USD accepted)"
→ Q2 data feeds directly into Section 8
  Budget Plan: Daily budget = total budget / Q2 days.

**Q3 — Existing Assets:**
> "What does your team currently have?
> (A) Nothing — need the most complete output
> (B) Raw video available — only need script + TA
> (C) TA already set — only need ad scripts"
→ Affects output scope (see Step 7 conditional).

**Q4 — Production Capability:**
> "Can your team shoot video?
> (A) Yes — video + static + carousel all feasible
> (B) No — only need static + carousel"
→ Affects format selection in Step 4.

→ Generation begins only after all answers are received.

---

## 5. Processing Logic (Mandatory Sequence)

### Step 1: Spec Quality Check

Scan spec .md → score Readiness Score using the following rubric:

**Scoring Method:**
- Each required field (Section 4.1) complete + clear:
  **+1.5 points** (6 fields × 1.5 = max 9 points)
- Each required field present but vague (e.g.,
  value_proposition just says "good"): **+0.5 points**
- At least 1 useful optional field (Section 4.2):
  **+1 point** (max 1 bonus point)
- **Total scale: 10**

**Actions by Score:**
- 8–10: Generate full output
- 5–7: Generate but clearly mark all assumptions
  where data is missing
- < 5: Stop, list specific fields that are missing/vague
  with per-field scores, request additions before proceeding

### Step 2: Product Analysis

Skill determines:
- B2B vs B2C → affects tone and TA logic
- Emotional vs Functional product → affects hook priority
- Price sensitivity: budget / premium / luxury
- Purchase decision cycle:
  impulse (<1 day) / considered (1–7 days)
  / high-involvement (>7 days)

### Step 3: Hook Generation

Generate **3 mandatory hook variants**, each using a
different psychological trigger.
If data quality is sufficient → add up to 2 bonus hooks (max 5 total).

**Mandatory (always generate):**

| Hook Type | Psychological Trigger | Prioritize When |
|---|---|---|
| Pain Hook | Loss aversion | Functional product, B2B |
| Curiosity Hook | Information gap | All types |
| Transformation Hook | Lifestyle Upgrade framing | Lifestyle product |

**Note:** Transformation Hook describes life AFTER using
the product. Do NOT use Before/After body image
for health/beauty products (violates Meta policy).

**Conditional (only generate when data available):**

| Hook Type | Psychological Trigger | Condition |
|---|---|---|
| Social Proof Hook | Herd behavior | Only when spec includes existing_social_proof |
| Controversy Hook | Cognitive dissonance | Only when category has common misconceptions |

### Step 4: Script Assembly

For EACH hook from Step 3, assemble a complete script.
Each hook is assigned exactly 1 format per the table below:

| Hook Type | Required Format | Rationale |
|---|---|---|
| Pain Hook | Video 15s or 30s (per Step 2 decision cycle) | Loss aversion needs facial expression + urgency |
| Curiosity Hook | Static Ad | Information gap works best with short headlines |
| Transformation Hook | Carousel 5 slides | Lifestyle Upgrade needs multi-step storytelling |
| Social Proof Hook (if applicable) | Video 15s | Testimonials need facial expression |
| Controversy Hook (if applicable) | Static Ad | Cognitive dissonance needs strong headlines |

**Exception:** If Q4 = (B) team cannot shoot video
→ replace all Video formats with Static Ad.

See Section 6 for detailed templates per format.

### Step 5: TA Derivation

Derive TA settings from product analysis + persona,
with specific reasoning for EACH choice based on:
behavioral psychology / local culture insight /
target lifestyle / product use case (see Section 7).

### Step 6: Budget Planning

Use budget from Q2 → recommend budget allocation structure
following Meta 2026 best practices (see Section 8).

### Step 7: Output Assembly

Compile everything into 1 markdown block following
standard Output Format (see Sections 6–9).
Clearly note all assumptions used.

**Begin output with Executive Summary:**
- Product name + campaign objective
- Budget + timeline
- Number of variants generated
- Core TA (age, location, interest layer 1)
- Readiness Score assigned

**Conditional output based on Q3:**

| Q3 Answer | Skip | Keep |
|---|---|---|
| (A) Nothing available | No skip | Full output: Scripts + TA + Budget |
| (B) Raw video available | Skip detailed Production Notes | Scripts (structure only) + TA + Budget |
| (C) TA already set | Skip Step 5 TA Derivation | Scripts + Budget only |

### Step 8: Post-Launch Playbook

Use data from all previous steps → generate:
- Revenue Projection with 3 scenarios (see Section 9A)
- A/B Test Roadmap for 4 weeks (see Section 9B)
- Decision Tree by day (see Section 9C)

This step always runs, never skipped by Q3.

---

## 6. Output: Ad Scripts — Standard Format

Each script must be detailed enough for production team
and copywriter to execute immediately.

**Universal Creative Specs (mandatory in every script):**
- Video: Aspect ratio 9:16 (Reels/Stories) or 1:1 (Feed)
- Image: 1080×1080px (Square) or 1200×628px (Landscape)
- Carousel: Max 10 slides, recommend 5
- Text on image: Max 20% area to pass Meta review

### 6A. Video Script 15s (Full Template — Other Formats Follow Similar Structure)

[VARIANT A — Pain Hook — Video 15s]
Platform: Facebook Feed / Instagram Reels | Objective: [from Q1]

HOOK (0–3s): Visuals: [...] | Voiceover: "[...]" | Text overlay: "[...]" | Emotion trigger: [...]
BODY (3–12s): Visuals: [...] | Voiceover: "[...]" | Key message: [...] | Supporting proof: [...]
CTA (12–15s): Visuals: [...] | Voiceover: "[...]" | Button text: "[...]" | Landing page: [...]

PRODUCTION NOTES:
Tone: [...] | Casting: [...] | Music vibe: [...]
Caption: Mandatory (85% watch without sound)
A/B TEST NOTE: Test variable: Hook vs [Variant B hook]

### 6A-2. Video Script 30s (Skeleton)

Used when Purchase Decision Cycle is considered/high-involvement.
Structure: HOOK (0–5s) → PROBLEM (5–15s) → SOLUTION (15–25s) → CTA (25–30s)
Each section includes: Visuals + Voiceover + Key message.
Production Notes: same format as 6A.

### 6B. Static Ad Copy

[VARIANT B — Curiosity Hook — Static]
Primary text (first 125 characters most critical): "[...]"
Headline (max 40 chars): "[...]" | Description (max 30 chars): "[...]"
CTA Button: [Learn More / Shop Now / Sign Up / Get Quote...]
Image Direction: Concept [...] | Composition [...] | Colour mood [...]
Do NOT include: [e.g., before/after for health products]

### 6C. Carousel (5 Slides)

[VARIANT C — Transformation Hook — Carousel]

| Slide | Name | Content | Intent |
|---|---|---|---|
| 1 | Hook | Image + Headline (max 40 chars) | Stop scroll, spark curiosity |
| 2 | Problem | Image + Headline | Empathize, mirror pain point |
| 3 | Solution | Image + Headline | Introduce product as hero |
| 4 | Proof | Screenshot/data + Headline | Build trust, overcome objections |
| 5 | CTA | Product visual + CTA Button | Convert |

---

## 7. Output: TA Settings — Standard Format

Every setting MUST include reasoning. Detail level
is split into 2 tiers:

**Tier 1 — Core Settings (full 3-angle reasoning):**
Age, Gender, Location, Interest Stack → reasoning based on:
behavioral psychology / cultural insight / use case fit.

**Tier 2 — Standard Settings (1-line reasoning):**
Placements, Lookalike size → only 1 rationale sentence needed
(universal best practice, no 3-angle analysis required).

TA SETTINGS — [Product Name] — Phase 1

**Demographics (Tier 1 — 3-angle reasoning):**
Age: [e.g., 25–34] → Psychology: [...] | Use case: [...] | Cultural: [...]
Gender: [All / Male skew / Female skew] → Rationale: [...]
Location: [e.g., HCM + HN + Da Nang] → Rationale: [...]

**Interest Stack (3 Layers — Tier 1):**

| Layer | Description | Example | Rationale |
|---|---|---|---|
| 1 — Core | Direct use case mapping | [Interest A], [Interest B] | Maps to product |
| 2 — Adjacent | Expand reach, maintain relevance | [Interest C], [Interest D] | Core users also interested |
| 3 — Behavioral | Purchase intent signals | [Engaged Shoppers], [...] | Decision-making power |

**Lookalike Audiences (Tier 2):**
If website/app data available: Source 1 [...] + Source 2 [...], size 1–2%
If not yet launched: replace with Broad Interest using Layer 3 behavioral.

**Placements (Tier 2):** Advantage+ Placements (Phase 1 needs fast data).
Exception: Awareness → manual Feed + Reels.

**Negative Targeting (mandatory):**
Exclude: existing customers | competitors' employees | age < 18 | unserviceable locations

Phase 2 teaser: After 14 days of data, transition to retargeting
custom audiences (outside MVP scope).

---

## 8. Output: Budget Plan — Standard Format

BUDGET PLAN — [Product Name] — [timeline from Q2]
Total budget: [from Q2]
Daily budget: [total / days from Q2]

**Campaign Type (selected by timeline):**
- Timeline ≥ 14 days → ABO (Ad Set Budget Optimization)
  → Rationale: ABO enables even spend control
  across ad sets for clean data
- Timeline < 14 days → CBO (Campaign Budget Optimization)
  → Rationale: Insufficient learning phase time for ABO,
  CBO lets Meta optimize faster

Budget Split

| Ad Set | Audience | Budget/Day | Purpose |
|---|---|---|---|
| Broad Test | [age range], [market], No interest | 40% | Let Meta find audiences |
| Interest Stack | Layer 1+2 | [X]% | Validate hypothesis |
| Lookalike 1% / Broad Interest 2 | Website visitors (if available) or Layer 3 behavioral (if not launched) | [X]% | Warm-ish cold audience |

Learning Phase Note:
Each ad set needs ~50 conversions/week to exit learning phase

Minimum budget/ad set = target CPA × 2 / day

Do NOT modify ad sets in the first 7 days
→ avoid resetting the learning phase

Scale Trigger:
When 1 ad set achieves CPA ≤ target for
3 consecutive days → increase budget max 20%/day,
never increase more than 20% at once to avoid resetting learning

CPA Benchmark Reference (USD, 2025–2026):

| Product Category | Estimated CPA (USD) | Notes |
|---|---|---|
| SaaS / App | $2–$8/lead | Depends on pricing tier |
| E-commerce (orders) | $1–$4/purchase | Depends on product price |
| Service / Booking | $3–$12/lead | Depends on complexity |
| Education / Course | $4–$20/lead | High-involvement |

→ Skill suggests appropriate CPA range based on product_category.

---

## 9. Output: Post-Launch Playbook

This section transforms the output from a "static brief"
into a "30-day playbook". All calculations are based on
data already collected from Q1–Q4 + spec, no additional input needed.

### 9A. Revenue Projection

Based on: budget (Q2), CPA benchmark (Section 8),
pricing (spec), estimated conversion rate by
product_category → calculate 3 scenarios:

| Scenario | Assumptions | Formula |
|---|---|---|
| Best case | CPA = benchmark low, CVR = 5% | Leads = budget / CPA → Revenue = leads × CVR × pricing |
| Expected | CPA = benchmark mid, CVR = 3% | Same |
| Worst case | CPA = benchmark high, CVR = 1% | Same |

**Mandatory output includes:**
- Estimated leads/purchases within [Q2 timeline]
- Revenue projection for each scenario
- **Breakeven point** for Expected scenario
- Projected ROAS (Return on Ad Spend)
- Clear assumption note: "Figures are estimates based on
  industry benchmarks; actual results depend on
  creative quality and landing page."

**Example format:**
```
REVENUE PROJECTION — [Product Name] — [timeline]
Budget: $1,000 USD | CPL target: $6.67
Estimated leads: 150 (expected)

| Scenario | Leads | CVR | Purchases | Revenue | ROAS |
|---|---|---|---|---|---|
| Best     | 200   | 5%  | 10        | $2,990  | 2.99 |
| Expected | 150   | 3%  | 4–5       | $1,194  | 1.19 |
| Worst    | 75    | 1%  | 0–1       | $299    | 0.30 |

Breakeven: ~Day 18 (Expected case)
⚠️ Note: Phase 1 typically runs at a loss; the goal is
   to buy audience data, not achieve positive ROI.
```

### 9B. A/B Test Roadmap

Generate a scientific weekly testing roadmap based on
created variants and budget.

**Week 1 — Hook Test:**
- Run 3 variants (3 different hooks) in parallel
- Each variant with same audience, same budget
- Decision metric: CTR (Click-Through Rate)
- Decision: After 3–5 days, pick winner hook
  (highest CTR with sufficient statistical significance)

**Week 2 — CTA Test:**
- Winner hook × 3 different CTA variants
  (e.g., "Buy Now" vs "Learn More" vs "Start Free Trial")
- Decision metric: Conversion Rate
- Decision: Pick best CTA combo

**Week 3 — Audience Test:**
- Winner hook + CTA × 3 different audiences
  (Broad vs Interest Stack vs Lookalike)
- Decision metric: CPA
- Decision: Pick best audience

**Week 4 — Scale:**
- Winner combo (hook + CTA + audience) → increase budget
- Kill all losers
- Increase budget 20%/day for winner
- Begin planning Phase 2 (retargeting)

**Kill Criteria:**
Each week, any ad set NOT meeting threshold → turn off:
- CTR < 1% after 3 days → kill
- CPA > 2× target after 5 days → kill
- Frequency > 3.0 → audience saturated, kill or expand

### 9C. Decision Tree (By Day)

| Day | Check | If... | Action |
|---|---|---|---|
| 1–3 | Do nothing | — | Learning phase, observe only |
| 3 | CTR | < 1% | Swap hook, keep audience |
| 3 | CPA | CTR ok but CPA high | Fix Landing Page, don't touch ads |
| 3 | Both ok | CTR ok + CPA ok | Continue, no changes |
| 7 | CPA | 1 ad set ≤ target | Potential winner, run 3 more days to confirm |
| 7 | CPA | All > target | Review creative/audience/LP |
| 7 | Frequency | > 2.5 | Audience saturated, expand or swap creative |
| 14 | CPA | ≤ target for 3 consecutive days | Scale 20%/day, kill losers |
| 14 | CPA | No winner | Pause, review product-market fit |
| 14 | CPA | Fluctuating | Run 7 more days with same setup |
| 21–30 | Scale | Winners identified | Scale + build retargeting audiences (Phase 2 prep) |

---

## 10. Business Rules

### Always Do:
- Clearly note assumptions wherever spec data is missing
- Include A/B test note for each variant pair
- Provide reasoning for EVERY TA setting — no setting
  without a rationale
- Ask about budget first, never suggest a budget
  without knowing the user's constraints

### Never Do:
- Do NOT generate output when Readiness Score < 5
- Do NOT choose campaign objective for the user (always ask Q1)
- Do NOT use before/after body imagery for health/beauty
  products (violates Meta policy). Transformation Hook
  for health/beauty MUST use Lifestyle Upgrade framing.
- Do NOT leave scripts without Production Notes —
  team cannot execute without this section
- Do NOT generate Social Proof Hook when spec lacks
  existing_social_proof — avoid fabricating data

### Ask First:
- When spec indicates product is for minors
  (< 18 years old) → ask for confirmation before applying TA rules
- When product category is sensitive (finance, health,
  politics) → ask for confirmation before selecting targeting

---

## 11. Success Criteria

Output is considered successful when:
- [ ] Creative Producer can take the output → brief
      the production team immediately,
      without asking any additional questions
- [ ] Media Buyer can take the output → set up
      a complete campaign in Meta Ads Manager
      without further research
- [ ] Exactly 3 mandatory variants with different hook types
      and formats for A/B testing from day one
- [ ] Revenue Projection with 3 scenarios for stakeholders
      to evaluate risk/reward before spending
- [ ] A/B Test Roadmap + Decision Tree enabling team
      to self-operate for the entire month without a consultant

---

## 12. MVP Boundary (Minimum Viable — 2 Days)

### In Scope:
- 3 mandatory ad scripts (video 15s/30s + static + carousel),
  plus up to 2 bonus if data is sufficient
- Complete TA settings with reasoning (2 tiers)
- Budget plan based on user's actual budget + timeline
- Readiness Score check with rubric
- **Post-Launch Playbook: Revenue Projection + A/B Test
  Roadmap + Decision Tree**

### Out of Scope (for later):
- Retargeting campaigns
- Dynamic Creative
- Multi-language output
- Direct integration with Meta Ads Manager API
