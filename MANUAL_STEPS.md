# Manual steps — things only you can do

Everything here is a step the assistant genuinely cannot complete — either because it needs your account/login, a commercial decision, or a one-time interactive approval. This list got dramatically shorter once the environment setup moved from the cloud sandbox to this local machine — see `docs/memory/environment-constraints.md` for why. Nothing below is urgent (no app code exists yet); grouped by when it actually matters.

## Right now / next session start

1. **Approve the 2 project MCP servers.** `sequential-thinking` and `basic-memory` are in this repo's `.mcp.json` (context7 and playwright are already connected via their official plugins, so they were removed from here to avoid duplicate/confusing entries). Type `/mcp` in Claude Code and approve/connect each — one-time, first-run behavior.
2. **Run `/design-login` once** to authorize the DesignSync bridge between Claude Design and this repo — needed for the design workflow below (item 3). This is an interactive command only you can run.

## To start the design phase (Claude Design → Claude Code handoff)

3. **Open [claude.ai/design](https://claude.ai/design)** (or the Claude Desktop sidebar) and start a new project. Paste/adapt `docs/design/claude-design-starter-brief.md` as your opening message — it already encodes the app's scope, anti-goals, priority screens, and typography direction from this repo's research, so you don't need to re-explain any of it. Iterate there on the visual design and key flows.
4. **When a screen/flow feels right**, hand it off back here — either click "Send to Claude Code Web" / "Send to local coding agent" inside Claude Design, or (once `/design-login` above is done) run `/design-sync` from Claude Code to pull the design system in. Full reasoning for this two-phase approach: `docs/memory/design-workflow-decision.md`.

## Already resolved (no longer on this list)

- ~~GitHub push access~~ — works. `git push` succeeded on the first try locally (Windows already had cached GitHub credentials), no PAT or permission-fixing needed. The commit is live on `main` at `github.com/Abdelrahman-Nashaat/best_azkar_mobile_app`.
- ~~Network policy blocking APIs/MCP endpoints~~ — this machine has normal internet access. Not an issue here.
- ~~Plugin marketplace blocked~~ — installed cleanly: `expo`, `figma`, `frontend-design`, `context7`, `playwright`, `sentry`, `claude-md-management`, plus `impeccable` (separate installer). See `docs/research/tooling-and-tech-stack.md`.

## Before real device/emulator testing

5. **Install Android Studio + Android SDK** (free) if you want a local Android emulator — this machine has WSL2/Docker Desktop already running, which implies virtualization is enabled, so the emulator should get hardware acceleration once set up. Not required to start building — Expo Go on your phone works without it — but it's a smoother loop for iteration. Get it from developer.android.com/studio.
6. **Install "Expo Go" on your phone(s)** — lets you scan a QR code and see the app live on a real device while the dev server runs here, without any build step. iOS still has no local-simulator option on Windows (Xcode is macOS-only) — Expo Go or an EAS-built install is the way to test iOS regardless.
7. **Log into an Expo account** (`npx expo login`, free) when we're ready to use EAS Build for real installable binaries — reachable from this machine now, unlike the cloud sandbox. Free tier: 15 iOS + 15 Android builds/month.

## Optional, whenever convenient

8. **Context7 API key (free)** — works without one at a lower rate limit; a free key at context7.com/dashboard raises the limit. Tell me if you want it added.
9. **`gh auth login`** — only if you want to use the GitHub CLI directly for things like PR creation; not required for anything covered so far (plain `git push`/`pull` already works).

## Later — design phase

10. **Figma account (free tier is fine)** — only if you want a Figma-based design workflow in addition to Claude Design. I'll ask for the one-time OAuth login when we get there.

## Later — production-hardening phase

11. **Sentry account (free tier)** — for crash/error monitoring before real users get the app.
12. **Supabase or Firebase account — only if/when we decide the app needs backend sync.** Current default is fully offline-first with no account (see `docs/memory/tech-stack-decision.md`).

## Later — deployment phase

13. **Apple Developer Program ($99/year) + Google Play Developer account ($25 one-time).** Required to publish to the App Store / Play Store.

## About the GitHub token you shared earlier

Since it never actually got used (the classifier blocked embedding it in a command, and it turned out to be unnecessary once we moved local), it's your call whether to revoke/regenerate it — no urgency, just flagging that it's sitting in the chat history unused.

---

Nothing above blocks the build phase from starting. Items 1–4 are quick one-time setup; 5–7 make the *testing loop* smoother but Expo Go alone is enough to get moving.
