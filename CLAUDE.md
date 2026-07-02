# Best Azkar App

Building the best azkar/dhikr/dua mobile app that exists — deliberately **not** an all-in-one Islamic super-app. Depth and polish on one thing beats breadth across ten.

## Scope

**In scope** (own these completely, execute at the highest possible quality):
- Morning/evening azkar, post-prayer azkar, sleep/waking azkar — with counters
- Occasion-based duas from Hisn al-Muslim (travel, illness, distress, gratitude, anxiety, etc.)
- Mood/state-based dua recommendation — inspired by Azkari's "بماذا تشعر" feature, but deepened: cite *why* a dua fits a state (which hadith/ayah), don't just surface a list
- Digital tasbih / dhikr counter with haptic + visual feedback
- Prayer times & Qibla direction (on-device calculation, not a server dependency) — a supporting feature, not the product
- Local reminders/notifications, streaks, reading/progress state — all on-device
- Audio recitation of azkar
- Home screen widgets (iOS + Android) and iOS Live Activities (e.g. countdown to next prayer)
- Arabic (full tashkeel) + English + transliteration at minimum, expandable
- Best-in-class UI/UX: calm, distraction-free, beautiful typography, smooth motion, full accessibility (screen readers, adjustable text size, dyslexia-friendly option)

**Out of scope** (resist scope creep even when "it would be easy to add"):
- Full Quran mushaf/reading/tafsir study tools — that's Quran.com's job, not ours
- Full hadith encyclopedia/search across all books — that's Sunnah.com's job
- Mosque finder, maps, Zakat calculator, Ramadan mega-features, social/community features
- Anything that turns this into "yet another all-in-one Muslim app"

If a feature idea pulls toward "all-in-one," push back or defer it — this boundary is explicit user intent, not a guess. See `docs/memory/project-overview.md`.

## Non-negotiable quality bar

- This ships to real users for real worship. An unverified or wrong dua/hadith string isn't a cosmetic bug — content accuracy is sacred, not an ordinary QA concern (see Content authenticity rules below).
- Never reduce quality because of context limits, `/compact`, session limits, cost, or time — all explicitly waived as constraints by the user. If compaction left gaps, re-derive from `docs/memory/`, `docs/research/`, and git history rather than guessing.
- No prototype-only, demo-only, placeholder, TODO-left, or mock-only work presented as done. No UI disconnected from real logic/persistence.
- Don't declare a feature/phase complete until it's production-ready and actually verified by running it (use the `run` and `verify` skills). Typechecking and unit tests confirm correctness, not that a feature works for a real user.
- Free forever: no ads, no paywalls, no dark patterns. This is a deliberate, direct reaction to the ad and subscription complaints found against competitors — see `docs/research/competitor-market-research.md`.
- **Never let environment-specific limits masquerade as universal constraints.** This project's setup was first drafted inside a heavily sandboxed cloud container (blocked APIs, blocked git access, no GPU/emulator) and then redone on the user's actual local machine, which has almost none of those limits. If you're ever unsure whether a constraint is real or just an artifact of wherever you happen to be running, re-verify — don't assume. See `docs/memory/environment-constraints.md` and `docs/memory/user-and-preferences.md`.

## Content authenticity rules

- Full tashkeel (Arabic diacritics) on every Arabic string, no exceptions. Missing tashkeel was one of the most common complaints found against existing azkar apps — treat any un-voweled Arabic string as a bug.
- Only sahih/hasan-graded narrations ship as azkar content; cite the grading source (commonly Al-Albani's grading, as used in the printed Hisn al-Muslim). Da'if/fabricated content is excluded, not merely labeled.
- Canonical reference: the printed *Hisn al-Muslim* ("Fortress of the Muslim") by Sa'id bin Ali bin Wahf Al-Qahtani. Cross-check every azkar/dua string against it plus at least one independent dataset before shipping — a single scraped source is not sufficient verification for religious text. Candidate datasets are listed in `docs/research/tooling-and-tech-stack.md`.
- Ship a light, non-intrusive disclaimer recommending users consult a qualified scholar for fiqh/creed questions.
- Translations and transliterations need the same rigor as the Arabic source.
- Full detail: `docs/memory/content-authenticity-rules.md`.

## Tech stack (decided during environment setup, 2026-07-02)

- **React Native + Expo**, New Architecture (JSI/Fabric), TypeScript — chosen over Flutter primarily because there's no macOS/Xcode available (true on both the original cloud container and this local Windows machine — this part of the reasoning is a real, permanent constraint, not a sandbox artifact), and Expo's EAS Build gives cloud iOS builds without one. The New Architecture also closes most of the historical RN-vs-Flutter perf gap, and the ecosystem/MCP/plugin tooling coverage is stronger for JS/TS in 2026 (official `expo` Claude Code plugin, etc.).
- Styling: NativeWind (Tailwind for RN) + a custom design-token layer — avoid a generic, default-AI-looking UI. Use the `frontend-design` and `impeccable` skills (both installed, see below) for every UI surface.
- Motion: Reanimated 3 (worklets, UI-thread) + React Native Skia/Skottie for custom drawing and Lottie-quality effects. Respect OS "Reduce Motion".
- Prayer times/Qibla: `adhan` (batoulapps), computed on-device — no network dependency, no rate limits, more private (this remains the right call even though APIs are reachable from this local machine — see `docs/research/tooling-and-tech-stack.md`).
- Notifications: `expo-notifications`, local-only. Widgets: `expo-widgets` (iOS, incl. Live Activities) + `react-native-android-widget` (Android), both via Expo config plugins.
- i18n/RTL: `expo-localization` + `i18next`, `I18nManager`, start/end (not left/right) style props.
- Full rationale, alternatives considered, and sources: `docs/research/tooling-and-tech-stack.md`.

## Environment & tooling

This repo's `.mcp.json` (project-scoped, committed to git) configures:
- **context7** — up-to-date library docs. Say "use context7" when working with any library API. Fully functional here (unlike the original cloud-sandbox draft of this setup, this local machine has normal internet access).
- **sequential-thinking** — structured reasoning for complex planning.
- **basic-memory** — local knowledge graph over `docs/memory/*.md` (project name `best-azkar-app`). Read/search it at the start of any non-trivial session before re-deriving context from scratch.
- **playwright** — browser automation for quick web-preview checks (Expo supports a `web` target) and general browser-driven verification.

Plus these official Claude Code plugins, installed at project scope (`claude-plugins-official` marketplace, see `.claude/settings.json`): **expo** (official Expo skills for building/deploying/debugging), **figma** (design file access, design-to-code), **frontend-design** and **context7**/**playwright**/**sentry** (plugin versions, complementing the raw MCP servers above), **claude-md-management** (keeps this file and `docs/memory/` accurate over time — worth invoking periodically).

Plus the **impeccable** design skill (installed via `npx impeccable install`, not from the marketplace — 23 commands like `/impeccable polish`, `/impeccable critique`, `/impeccable audit`, plus a PostToolUse hook that runs its detector after UI edits). **Run `/impeccable init` as the first step of the actual build phase** (not now — it starts defining product/design context, which crosses into build-phase territory) to set up `PRODUCT.md`/`DESIGN.md`.

### Claude Design (separate product, feeds into Claude Code)

**Claude Design** (claude.ai/design, launched April 2026, research preview) is a *separate* Anthropic product for rapid visual/UX prototyping as live, clickable HTML — not a Claude Code feature. Decided workflow (2026-07-02, see `docs/research/tooling-and-tech-stack.md` for the full comparison): use Claude Design **first**, for fast visual iteration on key screens, then hand off to Claude Code to build the real React Native/Expo implementation. Do not treat this as an either/or with Claude Code — they're sequential phases of the same build.
- Starter brief ready to paste into a new Claude Design project: `docs/design/claude-design-starter-brief.md`.
- Bridge tool: **DesignSync** (this session already has the tool, but it needs one-time interactive authorization — run `/design-login` yourself once; I can't run it non-interactively). Once authorized, `/design-sync` pulls a Claude Design project's design system into this repo, or Claude Design's own "Send to Claude Code Web / local coding agent" button pushes a handoff bundle here directly.

When a needed MCP server/plugin genuinely can't be installed, say so explicitly — but don't assume something is blocked just because an earlier session (possibly in a different, more restricted environment) said so. See `docs/memory/environment-constraints.md`.

Use existing Claude Code skills at the right moments: `run`/`verify` before claiming any feature works, `security-review` before anything touching user data or dependencies, `code-review`/`simplify` on non-trivial diffs, `frontend-design`/`impeccable` for every UI surface.

## User & working style

Full detail: `docs/memory/user-and-preferences.md`. Summary: communicate with the user in Arabic (Egyptian dialect mirrors how they write); cost/time are explicitly not constraints — optimize purely for the best final result; act as an autonomous product owner + senior engineer, not a literal instruction-follower — infer standard features of a top-tier azkar app rather than waiting to be told (see `docs/memory/autonomous-ownership-mindset.md`); only stop to ask about genuinely manual steps or product/commercial decisions (see `MANUAL_STEPS.md`); **never let one environment's limitations quietly become permanent assumptions** — the user has explicitly and repeatedly emphasized this.

## Where to look for more context

- `docs/memory/` — persistent knowledge graph (decisions, preferences, constraints, rules). Read before assuming something hasn't been decided yet.
- `docs/research/competitor-market-research.md` — what's wrong with existing azkar/Muslim apps, what users love, design inspiration.
- `docs/research/tooling-and-tech-stack.md` — full tech stack rationale, content data sources, library choices, MCP/plugin ecosystem, what's actually installed and working.
- `MANUAL_STEPS.md` — everything only the user can do (accounts, installs, optional upgrades) — check this before assuming something is blocked for good.
