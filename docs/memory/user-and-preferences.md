---
name: user-and-preferences
description: Who the user is and how they want work done on this project
metadata:
  node_type: memory
  type: user
  project: best-azkar-app
  created: 2026-07-02
---

The user (Abdelrahman Nashaat; GitHub `Abdelrahman-Nashaat`; git email `emara01111@gmail.com` locally, `reakosan1@gmail.com` on the account used for the cloud session — same person, two emails seen) is building [[project-overview]] — the best azkar/dhikr mobile app, not an all-in-one Islamic app. Communicates in Egyptian Arabic; reply to them in Arabic in conversation. Documentation/code/CLAUDE.md itself stay in English (matches the convention of the prior project's files this user provided as a template).

Also runs other, unrelated projects on this machine (`alardan-platform`, `sahmai`, a Hajj-algorithm project) — don't confuse those with this one.

## Working preferences (stated explicitly, 2026-07-02, during environment-setup phase)

- Cost, time, and effort are **not** constraints — optimize purely for the best final result. Explicitly said "مش مهتم بالتكلفة ولا الوقت" (not concerned with cost or time) and "المهم عندي النتيجة النهائية" (what matters is the final result).
- Wants the **best UI/UX ever** and wants every feature done to the highest standard, not just "done": "عايزين نعمل كل حاجة وبافضل كل حاجة" (we want to do everything, and the best of everything).
- Explicitly invites questions ("تقدر تسالني اي سؤال براحتك") but also clearly wants autonomy — don't over-ask; use good judgment and escalate only genuinely blocking/manual/commercial decisions. See [[autonomous-ownership-mindset]].
- Brought 3 memory-style instruction files from a prior, unrelated project (a soil/building-materials testing-lab system built for "Eng. Hamza" / Jhood Ltd) and asked to adapt their spirit here. See [[production-quality-bar]] and [[autonomous-ownership-mindset]] for the adapted versions — only the working philosophy carries over, no domain specifics from that project apply here.
- **Critical, repeated instruction: "لا تقم ابدا بتقييد Fable 5" (never restrict Fable 5).** Concretely: when a limitation is discovered (a blocked API, a missing tool, a permission denial), pin down *why* before encoding it as a rule — is it inherent to the task/domain, or just an artifact of the specific sandbox/machine this session happened to run in? Only the former belongs in a durable decision. This surfaced concretely on 2026-07-02: the first pass of this setup ran in a restrictive cloud container and concluded several things were impossible (plugin marketplace installs, GitHub push, Context7, live API access); redone locally, all of those worked fine. See [[environment-constraints]] for the corrected picture. Don't repeat that mistake — when in doubt, re-test rather than assume.
- Actively finds and shares external tools/links unprompted (Impeccable, Higgsfield CLI) and explicitly wants proactive research beyond only what they name: "لا مانع انك تبحث مرة اخرى... ليس فقط المصطلحات التي ذكرتها" (no objection to you researching again — not just the terms I mentioned). Keep scanning for relevant tooling even without being pointed at it.
- This environment-setup work was explicitly **not** a coding/build phase — scoped to preparing tooling, MCP servers, plugins, and documentation so a subsequent model (the user calls it "Fable 5") can build with maximum context and capability. See [[environment-constraints]] and [[tech-stack-decision]] for what was actually configured.

## Decisions defaulted this session

An interactive confirmation round-trip (AskUserQuestion) failed twice with a tool/connection error during the cloud pass, so the following were applied as clearly-flagged recommendations rather than left blocking — none contradicted since:
- Tech stack: React Native + Expo (see [[tech-stack-decision]])
- Backend: offline-first, optional account sync later
- Languages: Arabic + English + transliteration

If the user corrects any of these, update this note **and** the more specific note it points to.
