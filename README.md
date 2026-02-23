# 🎯 Meta Ads Script & TA Generator

An OpenClaw skill that turns your product spec into a complete Meta Ads campaign package — ready to execute, no follow-up questions needed.

## What It Does

- Reads your product spec `.md` file and asks 4 clarifying questions
- Generates 3+ ad script variants (Video 15s/30s, Static, Carousel) with different psychological hooks
- Builds target audience settings with layered reasoning (demographics, interest stack, placements)
- Creates a budget plan (ABO/CBO), revenue projection, A/B test roadmap, and a 30-day decision tree

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

Your `spec.md` must follow the required format — see [spec/spec.md](spec/spec.md) for the full field reference.

## Input spec.md Format

See [spec/spec.md](spec/spec.md) for all required and optional fields.

For a ready-to-use sample input, see [examples/input-sample.md](examples/input-sample.md).

## Example Output

See [examples/output-sample.md](examples/output-sample.md) for what the generated campaign package looks like.

## Requirements

- OpenClaw installed and configured
- A product `spec.md` file with at least 6 required fields filled (see [spec/spec.md](spec/spec.md))

## License

MIT — see [LICENSE](LICENSE).
