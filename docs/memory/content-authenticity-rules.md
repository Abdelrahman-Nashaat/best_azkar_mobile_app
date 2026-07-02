---
name: content-authenticity-rules
description: Non-negotiable rules for sourcing and verifying religious text in this app
metadata:
  node_type: memory
  type: rule
  project: best-azkar-app
  created: 2026-07-02
---

These rules exist because this app's entire value proposition is trustworthy religious content, delivered beautifully — get the content wrong and nothing else matters. See [[production-quality-bar]] for why this is treated as more than an ordinary QA concern.

- Full tashkeel (Arabic diacritics) on every Arabic string, no exceptions. Missing tashkeel was one of the most common complaints found against existing azkar apps in [[competitor-market-research]].
- Only sahih/hasan-graded narrations ship as azkar content; cite the grading source (commonly Al-Albani's grading, as used in the printed Hisn al-Muslim). Da'if/fabricated content is excluded, not merely labeled.
- Canonical reference: the printed *Hisn al-Muslim* ("Fortress of the Muslim") by Sa'id bin Ali bin Wahf Al-Qahtani. Cross-check every azkar/dua string against it plus at least one independent dataset before shipping (candidates in `docs/research/tooling-and-tech-stack.md` — e.g. `wafaaelmaandy/Hisn-Muslim-Json`, `ahegazy/muslimKit`, `mhashim6/Open-Hadith-Data`). A single scraped source is not sufficient verification for religious text. Now that this machine has normal internet access, actually cross-check against live Quran.com/Sunnah.com APIs too (unlike the cloud-sandbox pass, which couldn't reach them at all) — see [[environment-constraints]].
- Ship a light, non-intrusive disclaimer recommending users consult a qualified scholar for fiqh/creed questions — standard practice among reputable Islamic apps, and appropriate humility given this is software, not a mufti.
- Translations and transliterations need the same rigor as the Arabic source — don't let translation quality lag behind visual polish.
- The mood/state-based dua feature (see [[project-overview]]) must map states to duas using an explicit, checkable rationale (which hadith/ayah, why it fits) — not vibes-based matching.
