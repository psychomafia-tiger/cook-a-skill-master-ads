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

## License

MIT — see [LICENSE](LICENSE).
