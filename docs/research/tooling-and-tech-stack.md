# Tooling & tech stack research

Researched 2026-07-02 during environment setup (done twice: a cloud-sandbox draft, then redone locally — see `docs/memory/environment-constraints.md`). Decisions summarized in `docs/memory/tech-stack-decision.md` and CLAUDE.md; this doc holds the fuller rationale, alternatives, and sources.

## Framework choice: React Native + Expo vs Flutter

- React Native's 2024–2025 New Architecture (JSI + Fabric) closes most of the historical performance gap with Flutter; Expo on the New Architecture measures close to bare RN (~267–341ms cold start in 2026 benchmarks).
- Flutter (Impeller renderer, default since 3.27+) still has an edge for heavy custom animation / pixel-identical cross-platform UI, achieving 120fps in complex scenes more consistently.
- Deciding factor for this project: no macOS/Xcode available (true on the original cloud container *and* the user's local Windows machine — a real, permanent constraint either way). Expo's **EAS Build** provides cloud-based iOS builds without a local Mac.
- Verdict: **React Native + Expo**, New Architecture, TypeScript. Flutter is the documented fallback if animation needs later outgrow Reanimated + Skia.
- Sources: [RN vs Flutter vs Expo 2026 comparison](https://dev.to/krunal_groovy/react-native-vs-flutter-vs-expo-vs-lynx-2026-which-to-choose-for-your-app-30h6), [RN performance benchmarks 2026](https://www.applighter.com/blog/react-native-performance-benchmarks-expo-vs-bare-vs-flutter-vs-native-2026)

## Motion / premium UI

- **Reanimated 3**: worklets run on the UI thread, eliminating bridge-related jank — use for all interactive/gesture-driven animation.
- **React Native Skia** + **Skottie** (`react-native-skottie` / Shopify's `react-native-skia`): GPU-accelerated custom drawing; Skottie renders After-Effects/Lottie exports with reportedly +63% frame-rate over `lottie-react-native` on low-end Android in one benchmark.
- Respect the OS "Reduce Motion" accessibility setting; avoid motion-heavy effects on essential flows.
- Sources: [Skia in RN 2026](https://medium.com/@expertappdevs/skia-game-changer-for-react-native-in-2026-f23cb9b85841), [react-native-skottie](https://github.com/margelo/react-native-skottie)

## Design skills & tooling — installed and working locally

This is the section that changed most between the cloud draft and the local redo. All of the following are now actually installed in this repo (`.claude/settings.json` for plugins, `.mcp.json` for MCP servers) — not just researched:

- **`frontend-design`** (official Anthropic plugin, `claude-plugins-official` marketplace): guidance for distinctive, intentional visual design — ground every screen in the actual subject matter (Islamic remembrance: calm, sincere, unhurried), pair typefaces deliberately, avoid the current "AI-generated design" clusters (cream+serif+terracotta / near-black+single-accent / broadsheet-hairline-grid), work in two passes (plan a compact token system, critique it against the brief before coding).
- **Impeccable** (`pbakaus/impeccable`, installed via `npx impeccable install`, **not** from the marketplace — a separate npm-distributed tool): a widely-used (35k+ stars), explicit upgrade on top of Anthropic's own `frontend-design`, purpose-built against "AI slop" (Inter-everywhere, purple-blue gradients, cards-in-cards, icon-tile-above-every-heading). Ships as `.claude/skills/impeccable/` with 23 `/impeccable <command>` commands (`init`, `craft`, `shape`, `critique`, `audit`, `polish`, `bolder`, `quieter`, `distill`, `harden`, `onboard`, `animate`, `colorize`, `typeset`, etc.) plus 45 deterministic detector rules and a `PostToolUse` hook (in the gitignored `.claude/settings.local.json`) that runs its detector after any UI file edit. **Run `/impeccable init` as the very first step of the actual build phase** — not now, since it starts writing `PRODUCT.md`/`DESIGN.md` product context, which is build-phase work.
- Blocked in the cloud sandbox, works fine locally: this whole category was previously unavailable because `npx impeccable install` executes a third-party installer, and the cloud session's Auto Mode classifier correctly declined to run that without explicit authorization, and the marketplace plugin required `git clone`-ing a repo outside that session's GitHub scope. Neither restriction exists locally.
- **Arabic typography pairing recommendation**: **Cairo** (Google Fonts, modern sans-serif, described as the current gold-standard for digital Arabic UI text) for interface chrome/labels, paired with **Amiri** or **Noto Naskh Arabic** (classical Naskh-style, the conventional register for religious/Quranic text) for the actual azkar/Quran/hadith text itself.
- **Islamic geometric pattern resources** (for subtle background textures/decorative elements, not as a crutch): [TheBeachLab/islamic-geometry](https://github.com/TheBeachLab/islamic-geometry) (generative/computational design), a CodePen Islamic SVG pattern generator, and Taprats (older open-source Java tool). Use sparingly and intentionally per the `frontend-design` restraint principle.
- **Figma** (official plugin, installed): design file access, extract components/tokens, design-to-code. Needs a Figma account + one-time OAuth login when actually used — see `MANUAL_STEPS.md`.
- **Higgsfield CLI** (`higgsfield-ai/cli`, higgsfield.ai/cli): AI image/video/audio generation, useful for **marketing assets, app store screenshots, and app icon exploration** — explicitly **not** for the azkar audio recitation itself, which must come from an authentic, respected human Qari/reciter per `docs/memory/content-authenticity-rules.md`, not synthetic TTS. Requires its own account; revisit only when we reach app-store-asset/marketing work.

## Claude Design ↔ Claude Code workflow (researched 2026-07-02)

The user asked directly: run "Fable 5" in Claude Code, or in Claude Design first? Researched both rather than guessing.

**What Claude Design is**: a separate Anthropic Labs product (claude.ai/design, launched 2026-04-17, research preview, Pro/Max/Team/Enterprise), built on Claude Opus 4.7. Chat-driven canvas that produces live, clickable HTML prototypes (not static images) — describe a screen, refine via conversation/inline comments/direct edits/sliders. Can import an existing design system from a GitHub repo, design files, or a local codebase via `/design-sync`, and validates its own output against that system once imported. Explicitly positioned as feeding into Claude Code: "When a design is ready to become software, you can hand it off to Claude Code, which continues from your existing work instead of starting over from a screenshot" — via "Send to local coding agent" or "Send to Claude Code Web".
- Sources: [Anthropic announcement](https://www.anthropic.com/news/claude-design-anthropic-labs), [Claude Help Center: Get started with Claude Design](https://support.claude.com/en/articles/14604416-get-started-with-claude-design), [VentureBeat coverage](https://venturebeat.com/technology/anthropic-just-launched-claude-design-an-ai-tool-that-turns-prompts-into-prototypes-and-challenges-figma)

**Verdict: not either/or — sequenced.** Claude Design is for fast visual/UX exploration (screens, flows, the design system itself); Claude Code (this repo, with expo/figma/frontend-design/context7/impeccable already installed) is for the real, production React Native/Expo implementation. Use Claude Design first to nail "best UI/UX ever" through cheap iteration on live HTML mockups, then hand off.
- The docs describe Claude Design as "available on web and desktop only" and give no explicit React Native/Expo guidance — this refers to *where you access the Claude Design tool itself* (browser/desktop app), not a restriction on designing *for* a mobile target. Phone-frame/mobile-viewport prototyping in an HTML canvas is standard practice; the starter brief (`docs/design/claude-design-starter-brief.md`) explicitly asks for a native-mobile-app framing, not a web page.
- **DesignSync** is the concrete bridge tool on the Claude Code side (already available in this session). It needs one-time interactive authorization via `/design-login`, which only the user can run (not callable non-interactively). Once authorized: `list_projects`/`get_project`/`list_files`/`get_file` to read a Claude Design project, `create_project` → `finalize_plan` → `write_files`/`delete_files` to push a local component library into one, incrementally (never a wholesale replace).
- Practical flow: (1) user opens claude.ai/design, pastes/adapts `docs/design/claude-design-starter-brief.md`, iterates on the priority screen list in that brief; (2) once a screen/flow feels right, hand off via the button or `/design-sync`; (3) Claude Code implements it for real, using the existing content/tech decisions in this repo rather than re-deriving them.

## Prayer times & Qibla — on-device, not API-dependent

- **`adhan`** (batoulapps, MIT license) — high-precision astronomical calculation (Jean Meeus' "Astronomical Algorithms"), works fully offline, ships for JS/TS, Swift, Kotlin, Python. Still the right architecture even though `api.aladhan.com` is reachable from this local machine (unlike the cloud sandbox) — no network dependency, no rate limits, more private, and it's a stronger privacy story to point to (see competitor research on the Muslim Pro scandal).
- Source: [batoulapps/adhan-js](https://github.com/batoulapps/adhan-js)

## Content data sources (for sourcing + cross-verification)

Per `docs/memory/content-authenticity-rules.md`, the core azkar/dua text should be **bundled locally** (verified once, shipped as an asset), not fetched live:
- [wafaaelmaandy/Hisn-Muslim-Json](https://github.com/wafaaelmaandy/Hisn-Muslim-Json) — Hisn al-Muslim in Arabic + English JSON
- [ahegazy/muslimKit JSON files](https://ahegazy.github.io/muslimKit/json/) — azkar JSON (text, repeat count, virtue/fadl) for morning/evening/post-prayer azkar
- [mhashim6/Open-Hadith-Data](https://github.com/mhashim6/Open-Hadith-Data) — 9 hadith books incl. the Six Books, with tashkeel
- [my-prayers/muslim-data-android](https://github.com/my-prayers/muslim-data-android) — categorized azkar library (Category/Chapter/Item), multiple languages
- [01walid/awesome-arabic](https://github.com/01walid/awesome-arabic) — curated list of Arabic computational resources

For supplementary Quran/Hadith lookup (not the core azkar set) — **now directly reachable and testable from this machine**, unlike the cloud sandbox: [Quran.com developer APIs](https://quran.com/developers) / [QuranFoundation API docs](https://api-docs.quran.com/), [Sunnah.com developers](https://sunnah.com/developers) (API key requested via GitHub issue), [Al Quran Cloud](https://alquran.cloud/api) (free, no key).

## Notifications & platform-native extras

- **`expo-notifications`** for local scheduled reminders. Must handle Android 12+ `SCHEDULE_EXACT_ALARM` permission; foreground notification handling differs on iOS; **must test on a real device** — Expo Go and simulators don't fully replicate background/killed-app behavior.
- **Widgets**: `@bittingz/expo-widgets` (iOS home-screen widgets + Live Activities) and `react-native-android-widget` (Android, via Expo config plugin) — both keep us in the Expo/EAS build pipeline.
- **iOS Live Activities**: good fit for a "time until next prayer" or "azkar streak" countdown. Max 8h active in the Dynamic Island, up to 12h total on the Lock Screen.
- **Apple Watch companion app**: possible via RN bare workflow + `react-native-watch-connectivity`, but EAS Build doesn't support Watch app targets out of the box — needs occasional actual macOS/Xcode access regardless of local vs cloud. Later nice-to-have.
- Sources: [Expo widgets](https://docs.expo.dev/versions/latest/sdk/widgets/), [react-native-android-widget](https://saleksovski.github.io/react-native-android-widget/), [iOS Live Activities guide](https://newly.app/guides/ios-live-activities)

## i18n / RTL

- `expo-localization` + `i18next` + `I18nManager`; use `start`/`end` style properties instead of `left`/`right`; extra line-height for Arabic; let the localization library handle Arabic's multiple plural forms. Test with real RTL-reading users before shipping.

## Testing/verification strategy — updated for the local environment

- **Android**: install Android Studio + SDK (manual step, see `MANUAL_STEPS.md`) to get a real, likely hardware-accelerated emulator — this machine already has WSL2/Docker Desktop running, implying virtualization support that the original cloud container (no `/dev/kvm`) simply didn't have.
- **iOS**: still no local simulator option — Windows can never run Xcode. Use Expo Go on a physical iPhone, or EAS-built installable IPAs.
- **EAS Build**: reachable from this machine (`api.expo.dev` returns 200 here, unlike the blocked cloud sandbox) — should work once logged into an Expo account. Free tier: 15 iOS + 15 Android builds/month, 45-min build timeout.
- **Maestro** (free, local, open-source) for scripted E2E flows once there's a real app to test; Maestro Cloud is a paid device farm, not needed yet.
- Sources: [Maestro](https://maestro.dev/), [EAS Build limitations](https://docs.expo.dev/build-reference/limitations/)

## Claude Code MCP / plugin ecosystem — final state

**MCP servers** (`.mcp.json`, project-scoped): `context7` (now fully functional — real network access), `sequential-thinking`, `basic-memory` (knowledge graph over `docs/memory/`, project name `best-azkar-app`), `playwright`.

**Official plugins** (`claude-plugins-official` marketplace, project scope, see `.claude/settings.json`): `expo`, `figma`, `frontend-design`, `context7`, `playwright`, `sentry`, `claude-md-management`. All installed cleanly with zero errors once run from a normal (non-sandboxed) environment.

**Non-marketplace design tooling**: `impeccable` (via `npx impeccable install`).

**Still deliberately not installed** (needs an account first, not a technical blocker): `supabase`/`firebase` plugins (pending the backend/sync decision), any App Store Connect / Google Play Console MCP (deployment phase, needs paid developer accounts).
