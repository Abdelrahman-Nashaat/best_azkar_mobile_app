---
name: project-overview
description: What this project is, its scope boundary, and where things stand
metadata:
  node_type: memory
  type: project
  project: best-azkar-app
  created: 2026-07-02
---

The goal: the best azkar/dhikr/dua mobile app that exists — deliberately **not** an all-in-one Islamic super-app (the user's own words: "هذا افضل تطبيق للاذكار وليس ALL in ONE"). See CLAUDE.md at the repo root for the canonical in-scope/out-of-scope list — keep that list in sync with this note if scope ever changes.

Repo: `best_azkar_mobile_app` on GitHub (`Abdelrahman-Nashaat/best_azkar_mobile_app`), working locally at `C:\Users\abdel\Projects\web_best_azkar_mobile` on the user's Windows machine. As of 2026-07-02, only environment-setup work exists — no app code yet.

## Two-environment history (important context, not noise)

This environment-setup phase was actually done **twice**: first in a heavily sandboxed Claude Code "on the web" cloud container (couldn't push to GitHub, couldn't reach most external APIs/MCP endpoints, couldn't `git clone` the plugin marketplace), then redone here, locally, once the user opened the conversation on their own Windows machine and pointed out that cloud-sandbox limitations shouldn't be assumed to apply everywhere. They were right — almost none of them applied locally. See [[environment-constraints]] for specifics. The lesson (see [[user-and-preferences]]) generalizes: re-verify constraints per environment, don't carry them over as universal.

## Approach

Competitor apps (Azkari, Muslim Pro, Hisn al-Muslim variants, Pillars, etc.) were researched in depth *before* writing any code — see [[competitor-market-research]] (full doc: `docs/research/competitor-market-research.md`). Their most common complaints (missing tashkeel, ads, privacy violations, dark-pattern subscriptions, reliability bugs, no progress-saving) become explicit anti-goals here. Their best-loved features (Azkari's mood-based "بماذا تشعر" recommendation, Hisn al-Muslim's multi-language + transliteration, iOS widgets) become a floor to build above, not just match.

## Development sequence intended by the user

1. Environment-setup phase (tooling/MCP/plugins/docs, explicitly no app code) — 2026-07-02, done twice (cloud draft, then local for-real).
2. A build phase run by a different/successor model the user refers to as "Fable 5".
3. Iterative feature build-out, tested end-to-end each phase, git-committed at stable points.

## Related notes

[[tech-stack-decision]], [[environment-constraints]], [[content-authenticity-rules]], [[user-and-preferences]], [[production-quality-bar]], [[autonomous-ownership-mindset]].
