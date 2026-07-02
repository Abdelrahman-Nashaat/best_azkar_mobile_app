---
name: design-workflow-decision
description: Claude Design (visual prototyping) feeds into Claude Code (real implementation) — not either/or
metadata:
  node_type: memory
  type: decision
  project: best-azkar-app
  created: 2026-07-02
---

The user asked directly whether to run "Fable 5" in Claude Code or in Claude Design first, given the "best UI/UX ever" goal. Researched rather than guessed — see `docs/research/tooling-and-tech-stack.md` → "Claude Design ↔ Claude Code workflow" for full detail and sources.

**Decision: both, sequenced, not either/or.**
1. **Claude Design** (claude.ai/design — a separate Anthropic product, not part of Claude Code) for fast visual/UX exploration: live HTML prototypes, conversational refinement, cheap to iterate. Starter brief ready at `docs/design/claude-design-starter-brief.md` — covers the priority screen list (azkar reading, tasbih counter, mood-based dua flow, prayer times/Qibla, onboarding, settings, widgets), the anti-goals from [[competitor-market-research]], and the Cairo+Amiri/Noto-Naskh type pairing from [[tech-stack-decision]].
2. **Claude Code** (this repo) for the real, production React Native/Expo build — picks up the validated design via the **DesignSync** tool / `/design-sync` command / Claude Design's own "Send to Claude Code Web" handoff, and implements it using everything already set up here (plugins, content-sourcing plan, on-device prayer-time calculation, etc.) rather than re-deriving decisions.

**Outstanding**: DesignSync needs one-time interactive authorization via `/design-login` — only the user can run this (not callable non-interactively). Until then, the bridge exists but isn't connected. See `MANUAL_STEPS.md`.

Related: [[tech-stack-decision]], [[project-overview]].
