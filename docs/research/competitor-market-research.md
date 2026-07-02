# Competitor & market research — azkar/dhikr/dua apps

Researched 2026-07-02, before any app code was written, to inform (not yet implement) the feature/design plan. See `docs/memory/project-overview.md` for how this feeds into scope.

## App-by-app findings

### Azkar - اذكار : Athan & Prayer
- 4.7/5 across ~42,950 reviews (safety/review analysis via justuseapp).
- Complaints: some ads feature women / aren't Muslim-appropriate; some users report only the Quran section working while other categories stop responding (reliability bug); **many azkar entries lack proper tanween/tashkeel marks**, making pronunciation hard for non-Arabic-fluent readers.
- Liked: iOS home-screen widgets; ad removal for $1.99/month.
- Links: [App Store](https://apps.apple.com/us/app/azkar-%D8%A7%D8%B0%D9%83%D8%A7%D8%B1-athan-prayer/id1454509502), [review analysis](https://justuseapp.com/en/app/1454509502/%D8%A7%D8%B0%D9%83%D8%A7%D8%B1-%D8%A7%D9%84%D8%B5%D8%A8%D8%A7%D8%AD-%D9%88%D8%A7%D9%84%D9%85%D8%B3%D9%80%D8%A7%D8%A1/reviews)

### Azkari (اذكاري)
- ~4.95/5 on Aptoide. Free.
- **Unique feature**: "بماذا تشعر" ("How do you feel") — asks about the user's psychological/emotional state (joy, sadness, weakness, anxiety, etc.) and surfaces azkar/ayat/hadith tailored to that state. Described in coverage as the only Islamic app with this feature.
- Includes Asma-ul-Husna, azkar sabah/masaa, sleep azkar, ruqyah shariah, editable/custom reminders, share via social apps.
- Opportunity: the mood feature is praised but (per the user's own read of it) not fully realized — richer emotional-state coverage and an explicit "why this dua" rationale per state would meaningfully improve on it (see `docs/memory/content-authenticity-rules.md` on requiring a checkable rationale).
- Links: [Aptoide](https://azkari.ar.aptoide.com/app), [App Store](https://apps.apple.com/us/app/%D8%A7%D8%B0%D9%83%D8%A7%D8%B1%D9%8A-%D8%B7%D9%85%D8%A6%D9%86-%D9%82%D9%84%D8%A8%D9%83-%D8%A8%D8%B0%D9%83%D8%B1-%D8%A7%D9%84%D9%84%D9%87/id1109857175)

### Muslim Pro
- Major **privacy scandal**: sold/brokered location data via third-party broker X-Mode, reportedly reaching US military buyers; company disputes the "sold to military" framing but confirmed the broker relationship.
- Heavy ads historically (ads over duas, prayer times, community chat, hadith-of-the-day); 2025 reviews note improvement to ~3 ads/day.
- **Dark-pattern subscriptions**: 2025 reviews report users charged for 3 years after a 7-day free trial with no visible cancel button.
- Reliability complaints: Qibla compass getting stuck; app doesn't save reading/listening progress.
- This is the single clearest "what not to be" reference for this project — see `docs/memory/tech-stack-decision.md`'s offline-first/no-account default and CLAUDE.md's "free forever" rule.
- Links: [review analysis](https://justuseapp.com/en/app/388389451/muslim-pro-quran-athan-azan/reviews), [privacy scandal writeup](https://muslimadnetwork.com/muslim-pro-user-data-scandal-lesson/), [App Store](https://apps.apple.com/xk/app/muslim-pro-quran-azkar/id388389451)

### Hisn al-Muslim / Hisnul Muslim apps (multiple publishers)
- Digital versions of the book *Hisn al-Muslim* ("Fortress of the Muslim") by Sa'id bin Ali bin Wahf Al-Qahtani — Arabic + English/French/German/Dutch translation + transliteration, offline per-hadith audio, autocomplete search.
- This is the **canonical content reference**, not necessarily a UI/UX benchmark — see `docs/memory/content-authenticity-rules.md`.
- Praised for helping parents teach children duas via the transliteration + translation combo.
- Links: [App Store](https://apps.apple.com/us/app/hisnul-muslim-%D8%AD%D8%B5%D9%86-%D8%A7%D9%84%D9%85%D8%B3%D9%84%D9%85/id684520441), [Google Play](https://play.google.com/store/apps/details?id=com.quanticapps.hisnalmuslim&hl=en_US), [printed text PDF](https://mjc.org.za/wp-content/uploads/2018/11/HISN-AL-MUSLIM-FORTRESS-OF-THE-MUSLIM.pdf), [abdurrahman.org edition](https://abdurrahman.org/hisn-al-muslim/), [ahadith.co.uk edition](https://ahadith.co.uk/fortressofthemuslim.php)

### Pillars
- Ad-free, privacy-driven prayer app; location data stays fully on-device. Multiple calculation methods (Moonsighting Committee, ISNA, MWL). Direct evidence that a privacy-first positioning is viable and valued in this market.
- Link: [thepillarsapp.com](https://www.thepillarsapp.com/)

### Community sentiment
- A Privacy Guides community thread specifically asks for privacy-friendly Muslim app recommendations (Azan/Quran/Athkar) — signal that privacy-conscious users are actively searching for alternatives to the mainstream apps.
- Link: [privacyguides.net thread](https://discuss.privacyguides.net/t/muslims-recommend-privacy-friendly-muslim-apps-azan-quran-athkar-etc/30714)

### Design-quality context
- UX case-study commentary (e.g. the "Daily Muslim" app case study) explicitly notes that Islamic apps have historically shipped basic, dated UI relative to mainstream consumer apps — i.e. **the design bar in this category is currently low**, which is exactly the opening for a "best UI/UX ever" azkar app.
- Design inspiration sources to revisit during the actual UI build phase (not now): [Behance: Quran app projects](https://www.behance.net/search/projects/quran%20app), [Behance: Islamic app projects](https://www.behance.net/search/projects/islamic%20app), [Dribbble: islamic-app tag](https://dribbble.com/tags/islamic-app), [Dribbble: azkar tag](https://dribbble.com/tags/azkar), ["Daily Muslim" UX case study](https://www.themeaningofislam.org/blog/daily-muslim-habits-app-a-ux-case-study)

## Synthesis: gaps → anti-goals, loved features → floor to beat

| Competitor problem found | Our anti-goal / rule |
|---|---|
| Missing tashkeel on Arabic text | Full tashkeel mandatory, no exceptions ([[content-authenticity-rules]]) |
| Ads (incl. inappropriate imagery), paywalled ad-removal | Free forever, zero ads, zero paywalls |
| Muslim Pro data-selling scandal | Offline-first, no forced account, nothing leaves device by default |
| Dark-pattern subscriptions / hard-to-cancel trials | No subscriptions at all |
| Reliability bugs (sections freezing, Qibla stuck) | End-to-end verification before declaring any feature done ([[production-quality-bar]]) |
| No reading/progress persistence | Local streaks/progress persistence is a baseline feature, not a nice-to-have |
| Dated, generic UI across the category | Treat this as the biggest open differentiation opportunity — see `docs/research/tooling-and-tech-stack.md` for the design tooling (frontend-design, Impeccable) installed to support this |

| Competitor feature users loved | Our floor (must at least match, ideally exceed) |
|---|---|
| Azkari's mood-based dua recommendation | Same idea, deepened with an explicit "why this dua fits this state" rationale |
| Hisn al-Muslim's translation + transliteration | Arabic + English + transliteration minimum (see CLAUDE.md language decision) |
| Azkar app's iOS widgets | Widgets on both iOS and Android, plus iOS Live Activities for prayer-time countdowns |
| Pillars' on-device privacy | Match or exceed — no location/usage data leaves the device by default |
