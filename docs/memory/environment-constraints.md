---
name: environment-constraints
description: What this dev environment can and can't do — now the LOCAL Windows machine, previously a restrictive cloud sandbox
metadata:
  node_type: memory
  type: constraint
  project: best-azkar-app
  created: 2026-07-02
  updated: 2026-07-02
---

**Read this note's date/environment carefully before trusting it — this is exactly the kind of note that goes stale across environment switches. See [[user-and-preferences]] for why that matters here specifically.**

## Current environment (2026-07-02): local, Windows, unrestricted

Working directory `C:\Users\abdel\Projects\web_best_azkar_mobile` on the user's own Windows 10 machine (hostname `DESKTOP-5K6RSHA`). Confirmed via direct testing:
- **Full outbound internet access** — `api.expo.dev`, `api.quran.com`, `github.com`, `mcp.sentry.dev` all reachable (unlike the cloud sandbox, see below). EAS Build, live content-API integration/testing, and OAuth-based MCP servers (Sentry, Figma, Supabase) all become genuinely usable here, not just configurable-but-inert.
- **`git clone` of arbitrary repos works** — the plugin marketplace install (`claude plugin marketplace add anthropics/claude-plugins-official`) succeeded here on the first try, unlike the cloud session. Full plugin ecosystem is usable.
- Toolchain present: Node 24, npm 11, git 2.52, `uv`/`uvx` 0.11, Java 17 (Microsoft OpenJDK), GitHub CLI (`gh`, not yet authenticated — see `MANUAL_STEPS.md`), Docker Desktop with WSL2 backend already set up (implies virtualization is enabled, which matters for Android emulator acceleration).
- **Not present yet**: Android SDK/Studio (`ANDROID_HOME` unset) — installing it would unlock a real local Android emulator, unlike the cloud container which had no `/dev/kvm` at all. See `MANUAL_STEPS.md`.
- **Still not present, and never will be locally**: Xcode/macOS — this is a genuine, permanent constraint (Windows cannot run Xcode), not a sandbox artifact. The EAS-Build-for-iOS reasoning in [[tech-stack-decision]] holds for this reason alone, independent of local-vs-cloud.
- `npx impeccable install` and the plugin marketplace installs were **not** blocked by any safety classifier here (contrast the cloud session, where `npx impeccable install` was explicitly denied as unverified third-party code execution). Whatever permission/classifier system is active locally is evidently less restrictive for this kind of action — don't assume the cloud session's specific denials still apply.

## Historical: the original cloud sandbox (2026-07-02, first pass, superseded)

Kept for reference only — **do not apply these to the current environment**. A Claude Code "on the web" cloud container had: a strict network allowlist (only npm/PyPI/Anthropic domains; blocked `api.quran.com`, `api.aladhan.com`, `api.expo.dev`, all remote MCP endpoints), GitHub access scoped to a single repo with `git clone` blocked for anything else, and a GitHub App integration that turned out to be read-only (both direct `git push` and the GitHub MCP server's `push_files` failed with permission errors) — never actually resolved there; superseded by moving to local instead. An Auto Mode safety classifier also actively blocked embedding a live secret in a shell command and running an unverified third-party npm installer — both reasonable, unrelated to the network/git restrictions.

**The generalizable lesson, not the specific facts:** a sandboxed cloud container and a user's own local machine can have almost entirely different capabilities. When a future session (this one or "Fable 5") hits a wall, identify *why* before writing it down as a rule — inherent to the task, or an artifact of this particular execution environment? Only the former belongs in [[tech-stack-decision]] or CLAUDE.md as a hard constraint.

See `MANUAL_STEPS.md` for what's still genuinely outstanding (GitHub auth locally, Android Studio install, etc.) — much shorter list now than the cloud pass had.
