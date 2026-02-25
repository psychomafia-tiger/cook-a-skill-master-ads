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

| Model | Input cost | Output cost | Total |
|-------|-----------|-------------|-------|
| Gemini 3 Flash | $0.0228 | $0.0042 | **$0.027** |
| GPT-5.2 Instant | $0.0798 | $0.0196 | **$0.099** |
| Gemini 3.1 Pro | $0.0912 | $0.0168 | **$0.108** |
| Claude 4.6 Sonnet | $0.1368 | $0.0210 | **$0.158** |
| Claude 4.6 Opus | $0.2280 | $0.0350 | **$0.263** |

*Token breakdown per run: ~45,000 input tokens (SKILL.md runtime) + ~600 tokens (product spec) + ~1,400 output tokens. Prices as of Feb 2026.*

For context: a freelance Media Buyer charges $500–$2,000 for the same scope of work. This skill runs unlimited times for the cost of a single API call.

Every campaign you plan manually is time you can't get back.

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
