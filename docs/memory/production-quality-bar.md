---
name: production-quality-bar
description: Absolute top priority = best final production-ready result; never let compact/limits/cost/time reduce quality
metadata:
  node_type: memory
  type: feedback
  project: best-azkar-app
  created: 2026-07-02
  adapted_from: prior unrelated project (see [[user-and-preferences]])
---

Adapted from a working philosophy the user explicitly asked to carry over from a prior project (originally a soil/building-materials testing-lab system — the domain is irrelevant here, the philosophy is not).

**Why it matters more here, not less:** that prior project was "just" a business system. This one ships azkar, duas, and hadith that real Muslims will read, trust, and share for worship. An unverified or poorly-sourced string isn't a cosmetic bug — see [[content-authenticity-rules]].

## How to apply

- Do not optimize for speed, token usage, session limits, or convenience at the expense of quality. Do not reduce quality because of time/cost/limit/compact concerns — the user has repeatedly and explicitly waived all of those as constraints.
- If a `/compact` or context summarization left gaps, re-derive from [[project-overview]], `docs/research/*`, and git history — don't let compaction silently degrade the work.
- Every feature ships complete end-to-end: no prototype-only, demo-only, placeholder, TODO-leftover, fake-data, or mock-only work; no UI disconnected from real logic/persistence.
- Don't declare a phase done until it's production-ready and verified by actually running it (the `run`/`verify` skills exist for this) — typechecking and unit tests confirm correctness, not that the feature works for a real user.
- If a plugin/MCP/tool is needed and can't be added without a manual step from the user, say so directly rather than quietly working around it or skipping the capability. See `MANUAL_STEPS.md`.
- Quality bar applies to *environment setup* too, not just app code — see [[environment-constraints]] for what happens when that gets shortcut (conclusions drawn from a restrictive sandbox nearly became permanent, incorrect assumptions).
