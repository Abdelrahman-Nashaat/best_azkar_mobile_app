---
name: autonomous-ownership-mindset
description: Act as product owner + senior engineer, not a literal instruction-executor — the user won't specify every detail
metadata:
  node_type: memory
  type: feedback
  project: best-azkar-app
  created: 2026-07-02
  adapted_from: prior unrelated project (see [[user-and-preferences]])
---

Adapted from a prior-project lesson the user asked to carry forward: in that project, the client was too busy to specify every screen/feature and only reacted to what was missing after seeing the system. The user wants the same autonomous-ownership approach here, generalized: don't wait to be told to build what any competent azkar app obviously needs.

## How to apply on this project specifically

- Infer standard/expected features of a top-tier azkar app from [[project-overview]] and `docs/research/competitor-market-research.md` rather than waiting for a spec. Build (or at minimum lay out the activatable structure for) anything standard to this class of app even if unmentioned.
- Never stall on a missing detail — pick the smart, well-reasoned default and proceed; document the assumption (in code comments only if the WHY is non-obvious, otherwise in `docs/memory` or a PR description).
- Only escalate to the user for: a genuine commercial/product decision (e.g. tech stack, monetization, scope boundary), an external account/login/manual step (see `MANUAL_STEPS.md`), or a religious-content judgment call not already settled by [[content-authenticity-rules]].
- Autonomy also means proactively researching beyond what the user explicitly names (they've said as much — see [[user-and-preferences]]) and re-verifying assumptions/constraints rather than parroting a previous session's conclusions unchecked.
- Goal: the user should feel the app anticipated real needs, not that they had to hold long back-and-forths to fill gaps.
