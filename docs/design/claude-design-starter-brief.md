# Claude Design starter brief — paste this to begin Phase 1 (visual/UX exploration)

Researched 2026-07-02. See `docs/research/tooling-and-tech-stack.md` → "Claude Design ↔ Claude Code workflow" for why this two-phase approach was chosen. This file is meant to be copy-pasted (or summarized) as the opening message in a new Claude Design project at claude.ai/design.

---

I'm designing **the best azkar/dhikr/dua mobile app that exists** — deliberately not an all-in-one Islamic app (no Quran reader, no hadith encyclopedia, no maps/mosque-finder, no social features). Depth on one thing, executed better than anyone else, beats breadth.

**Design it as a native mobile app** (phone-frame viewport, touch-sized targets, thumb-reachable primary actions) — not a website or a responsive web page.

## Brand feeling
Calm, sincere, unhurried — this is for private worship and remembrance, not a productivity app. Avoid every current "AI-generated design" default: no purple-to-blue gradients, no glassmorphism, no generic icon-tile-above-every-heading cards, no Inter/Roboto-only typography. The design bar across existing azkar apps is low (dated, generic) — that's the opening to take.

## Typography
Pair a modern Arabic UI sans-serif (**Cairo**, from Google Fonts) for chrome/labels/navigation with a classical Naskh-style face (**Amiri** or **Noto Naskh Arabic**) for the actual azkar/Quran/hadith text itself — Naskh is the conventional, respectful register for religious text, distinct from UI chrome. Arabic-first (RTL), with English as a fully supported second language — design both directions, not just RTL-mirrored-from-English.

## Core screens/flows to prototype (in priority order)
1. **Morning/evening azkar reading screen** — the primary daily-use surface. Needs: Arabic text with full tashkeel (diacritics) prominently legible, a repeat counter per dhikr (many azkar repeat 3x/7x/10x/33x/100x), smooth progress through the list, a sense of calm pacing rather than a checklist grind.
2. **Digital tasbih/dhikr counter** — likely the single most-used interaction in the app. Deserves a genuinely delightful, tactile-feeling interaction (this is a strong candidate for the app's "signature element" per the `frontend-design` skill's own advice) — think about what large tap target, haptic-implying visual feedback, and counter-reset/target-count affordance feels best.
3. **Mood/state-based dua flow** ("How do you feel?") — inspired by a competitor feature called "بماذا تشعر", but deepened: the user picks an emotional/spiritual state (anxious, grieving, grateful, fearful, seeking guidance, etc.), and the app surfaces specific authentic duas for that state *with a brief, visible citation of which hadith/ayah it's from and why it fits* — not just a bare list. Design how that rationale is shown without breaking the calm reading experience.
4. **Prayer times + Qibla** — a supporting utility screen, not the main event. Should feel like a clean, glanceable companion (today's five prayer times, countdown to next, Qibla compass), not compete visually with the azkar content.
5. **Onboarding** — first-run experience. No forced account/login (the app is offline-first and private by design — no data leaves the device by default). Should establish the calm tone immediately.
6. **Settings** — language (Arabic/English + transliteration toggle), appearance (light/dark), text size (accessibility), notification/reminder scheduling, prayer calculation method.
7. **Home-screen widget concepts** (iOS + Android) — a small daily-azkar or next-prayer-countdown widget, and an iOS Live Activity concept for a prayer countdown on the Lock Screen/Dynamic Island.

## Explicit anti-goals (from direct competitor research — see `docs/research/competitor-market-research.md`)
- No ads, no paywalls, no "remove ads for $X/month" — everything is free, always.
- No account required, nothing implying data collection/tracking — this app's whole positioning is a privacy-respecting alternative to apps like Muslim Pro (which had a real data-selling scandal).
- Nothing that reads as "generic Islamic app" — most existing apps in this category look dated; this should look like it belongs next to the best-designed apps of any category, not just the best-designed *Islamic* app.

## When the design feels right
Hand it off to Claude Code (`Send to Claude Code Web` / `Send to local coding agent`, or `/design-sync` from the Claude Code side) — the receiving project already has: the full competitor/content/tech research this brief is based on, the React Native + Expo stack decision, the `frontend-design` and `impeccable` design skills installed, and the content-authenticity rules that govern the real azkar/Quran/hadith text. It should continue from the validated design, not start over from a screenshot.
