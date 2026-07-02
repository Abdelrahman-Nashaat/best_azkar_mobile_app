---
name: tech-stack-decision
description: Chosen stack for the app and why, decided during environment setup
metadata:
  node_type: memory
  type: decision
  project: best-azkar-app
  created: 2026-07-02
  updated: 2026-07-02
---

Decided 2026-07-02 (recommended by the assistant; user has an open invitation to override — see [[user-and-preferences]]). Re-confirmed after moving from the cloud sandbox to the local machine — see [[environment-constraints]] — nothing here changed as a result, because the reasoning that mattered (no Xcode/macOS) is a real constraint on Windows too, not a sandbox artifact.

- **React Native + Expo**, New Architecture (JSI/Fabric), TypeScript — over Flutter. Reasoning: no macOS/Xcode available on this machine either, and Expo's EAS Build gives cloud iOS builds without one (and EAS itself is actually reachable from here, unlike the cloud sandbox — see [[environment-constraints]]); the New Architecture closes most of the historical RN-vs-Flutter perf gap; bigger ecosystem and better 2026 MCP/tooling coverage (official `expo` Claude Code plugin, now actually installed). Flutter remains the documented fallback if custom-animation needs later outgrow Reanimated+Skia.
- NativeWind + custom design tokens for styling; Reanimated 3 + React Native Skia/Skottie for motion; `adhan` (batoulapps) for on-device prayer times/Qibla (no network dependency — still the right call for privacy/reliability even though the Aladhan API is reachable from here); `expo-notifications` for local reminders; `expo-widgets`/`@bittingz/expo-widgets` + `react-native-android-widget` for home-screen widgets and iOS Live Activities; `expo-localization` + `i18next` for Arabic/English/transliteration + RTL.
- Backend: offline-first, no forced account, nothing leaves the device by default (deliberate contrast to the Muslim Pro data-selling scandal found in research — see [[competitor-market-research]]). Optional account + cloud sync is a later, additive feature, not a day-one requirement. Supabase/Firebase MCP still deliberately not installed — revisit when the build phase actually needs sync/push infra.
- **Testing/verification strategy — updated now that this runs locally**: install Android Studio + SDK to get a real, hardware-accelerated Android emulator (this machine has WSL2/virtualization already enabled, so acceleration should work — unlike the cloud container, which had no `/dev/kvm` at all). iOS still has no local simulator option (Windows can never run one) — Expo Go on a physical iPhone, or an EAS-built installable IPA, remain the way to test iOS. EAS Build itself is reachable from here and should just work once the user is logged into an Expo account (manual step, see `MANUAL_STEPS.md`).

Full rationale and sources: `docs/research/tooling-and-tech-stack.md`.
