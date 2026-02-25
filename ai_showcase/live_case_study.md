# Real-World Deployment Case Study
**Date:** 2026-02-25
**Environment:** OpenClaw Internal VPS (Direct Deployment)

---

## The Origin & Context
**Product Details:** An internal AI lipstick try-on app (precise name/brand withheld for security reasons).
**Category:** Beauty/Utility App
**Target Market:** Global (US, UK, Canada, Australia)
**Campaign Objective:** App Installs

## The QA Challenge
To test the skill's ability to handle a regulated product category (health/beauty) according to Meta's strict ad policies, while verifying prompt adherence on a live OpenClaw VPS deployment.

---

## Demonstrated Capabilities

### ✅ Strict Guardrails (BUG-14 Pass)
The agent successfully ingested the product spec and halted execution to ask clarifying questions about the budget and timeline (the Q1-Q4 gate). It correctly refused to hallucinate missing variables and waited for explicit human confirmation before proceeding.

### ✅ Policy Compliance (Gate C Verified)
Upon generation, the agent successfully recognized the beauty app context and applied safe "Lifestyle Upgrade" framing to the Transformation Hook. It strictly avoided any prohibited "before/after body imagery" language often associated with health/beauty ads, ensuring the generated copy was Meta-compliant out of the box.

---

## Live Optimization (Closing BUG-15)

**The Discovery:** 
The initial live run delivered the entire ~1,400 token campaign package as a single monolithic block. While the content was excellent, this "wall of text" degraded readability in the chat UI and occasionally broke complex markdown table rendering (like the 5-slide Carousel).

**The Engineering Fix:** 
We designed and deployed a **Forced 4-Message Protocol** to control the output stream:
- `[Message 1/4]` Executive Summary & Scripts
- `[Message 2/4]` TA Settings
- `[Message 3/4]` Budget Plan
- `[Message 4/4]` Post-Launch Playbook

**The Result:** 
A successful re-deploy and re-test on the VPS confirmed the output is now cleanly chunked. The agent pauses between sections with progress markers (`📋 Scripts done, moving to TA...`), mirroring how a human Creative Producer would present a dense strategy document.

---

**Conclusion:** The skill is not just a theoretical prompt; it has been live-tested on internal OpenClaw systems, iterating on actual chat UI constraints to deliver a production-ready user experience.
