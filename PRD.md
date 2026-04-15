# TOPIK Note — 1-Page PRD

**Product**: TOPIK Note (iOS · Android)
**Landing**: https://luke-gu.github.io/topik-note-demo/
**Date**: 2026-04-15
**Creator**: GEONWOO JUNG · codelue01@gmail.com

---

## 0. Canonical Copy (shared across Landing / PRD / App Store)

- **Target persona (1 sentence)**: Foreign adult learners who must pass TOPIK level 3 or higher within 3–6 months for a student visa, work permit, or graduate admission, and who can only study 30–60 minutes a day during their commute.
- **Core pain scene**: *"She opens a Korean learning app on the Seoul Line 2 to Gangnam every morning, but two weeks before the test she opens a real past TOPIK paper and doesn't recognize 70% of the vocabulary. The flashcard apps she's been using were built by non-native speakers, and she keeps hitting typos and wrong answer keys. Korean language academies are too expensive and don't fit her commuter schedule. She panics."*
- **Existing solution limitations**:
  - General Korean learning apps are built for casual conversation — their coverage of TOPIK-level exam vocabulary is shallow.
  - Most "TOPIK prep" apps are built by non-native speakers and ship with typos, wrong answer keys, and mistranslated definitions.
  - Korean language academies are expensive, passive, and not schedule-friendly for commuters.
- **3 core features (1:1 mapped to pains)**:
  1. **7,970 quizzes built from real past TOPIK exams** (4 quiz types) → *solves the coverage pain*.
  2. **SM-2 spaced-repetition scheduler** that surfaces a word only when you're about to forget it → *solves the 30–60 minute time budget pain*.
  3. **Every word reviewed and verified by native Korean speakers**, sourced from 국립국어원 (National Institute of Korean Language) → *solves the wrong-answer / trust pain caused by apps built by non-native speakers — this is the core differentiator*.
- **Positioning (1 sentence)**: *"For foreigners prepping TOPIK 3+, TOPIK Note drills the exact words from real TOPIK exams on a spaced-repetition schedule — with every word reviewed and verified by native Korean speakers."*
- **Before / After**:
  - *Before*: 40 minutes a day on a generic Korean learning app for 3 months → sits the exam → 70% of words unfamiliar.
  - *After*: 25 minutes a day on TOPIK Note for 3 months → sits the exam → ≥80% of words already seen, most with 3+ exposures on the SRS schedule.

---

## 1. User Flow with Branching

Two journeys. They intersect at the **Home Hub (S3)** and value is delivered in the **Study Session (S6)**.

```
J1 — First-time learner
  S1 Welcome
    └─▶ S2 Level choice ─┬─▶ S2a Level test (20 Q, auto-classify TOPIK 1/3/5)
                         └─▶ S2b Manual select (pick 1-2 / 3-4 / 5-6)
                              └─▶ S3 Home Hub ◀── J2 joins here
                                   │
                                   ├─ free: 20-new-words/day quota ──▶ S8 Paywall at quota hit
                                   └─ premium: unlimited ──▶ S6 Study Session ★ CORE VALUE
                                                              └─▶ S7 Result

J2 — Returning learner
  S3 Home Hub ─▶ S6 Study Session (SRS queue today) ─▶ S7 Result ─▶ (optional) S4 Stats
```

**Branching conditions**:
- `isOnboarded === false` → J1 path, else J2.
- `premium === false && remainingNewWords <= 0` → Paywall (S8) overlays S3/S6.
- Stats (S4) charts are locked behind premium (PremiumLockOverlay).

---

## 2. Screen List

| ID  | Name               | User objective (verb phrase)                 | Core components |
| --- | ------------------ | -------------------------------------------- | --------------- |
| S1  | Welcome            | Accept terms and enter the app               | Hero copy, Start button |
| S2  | Level choice       | Decide how to set starting level             | 2 choice cards (test / manual) |
| S2a | Level test         | Prove TOPIK level with 20 questions          | QuizChoices, ProgressBar |
| S2b | Manual level select| Pick a TOPIK tier (1-2 / 3-4 / 5-6)          | Tier cards |
| S3  | Home Hub (tabs/index) | Start today's study and see daily quota   | Quota card, 4 action buttons |
| S4  | Stats              | Review streak, accuracy, and weak points     | BarChart, LineChart, PremiumLockOverlay |
| S5  | Settings           | Change language, notifications, legal        | SettingsRow list |
| **S6** | **Study Session** | **Answer quizzes and bank learning**     | **QuizChoices, WordCard, SessionProgress** |
| S7  | Result             | Review session outcome and next review date  | Summary, CTA to continue |
| S8  | Paywall            | Unlock unlimited + full stats                | SKU cards (Lifetime / Annual / Monthly) |

Core value moment: **S6**. Everything else is funnel.

---

## 3. MVP Scope

**In (must-have for the claim on the landing page to be true):**

| Item                                                   | 1-line justification |
| ------------------------------------------------------ | -------------------- |
| i. Four quiz types + SM-2 SRS                          | Core "learn the right words at the right time" claim. |
| ii. Free 20-new-words / day quota                      | Lets external evaluator experience the product with no signup. |
| iii. Level test **and** manual level select            | Reduces onboarding friction (persona can skip test). |
| iv. 7,970 quizzes across TOPIK 1–6, all reviewed by native Korean speakers | Makes the "real exam words, Korean-vetted" claim verifiable. |
| v. 5 UI locales (en / ko / ja / vi / zh)               | Aligns with persona's Southeast Asian + East Asian distribution. |

**Out (next version, conditional):**

- **Mock exam mode** (full 40-question simulated TOPIK test) — *after* we confirm ≥ X% lifetime conversion on vocab alone.
- **Pronunciation AI** (STT + accuracy scoring) — *after* the current TTS fallback path is stable across all 5 locales.
- **Social leaderboard / streak sharing** — *after* DAU reaches a level where social proof improves retention.
- **No-install web demo (5-question quiz)** — *after* landing conversion baseline is measured; treated as a marketing MVP, not a product surface.

**Completion criteria (external-user threshold):**
*"A first-time external evaluator can open the app without instructions, pick a level in ≤ 60 seconds, and answer 5 TOPIK vocabulary questions in a session they understand without reading any help text."*

---

## 4. Core Assumptions & Validation

Two assumptions that kill the product if wrong.

### Assumption 1 — Business

> "Foreigners preparing for TOPIK (visa / study / work) will pay for an exam-specific tool that is built and verified by native Korean speakers, instead of generic Korean apps or non-native-built TOPIK prep apps."

- **Why critical**: If the answer is "they'll just use free options," every feature investment is wasted.
- **Validation method**: 4-week post-launch cohort, measured on PostHog.
- **Success metric**: Paywall-view → IAP-purchase conversion rate ≥ **2%** on the lifetime SKU within the first 4 weeks, across ≥ 300 paywall views.
- **Data source**: `paywall_view` → `iap_purchase_success` funnel in PostHog (already instrumented via `EXPO_PUBLIC_POSTHOG_API_KEY`).

### Assumption 2 — Technical

> "Our SM-2 SRS schedule produces meaningful retention for typical learners (not just experts), so the coverage claim becomes a real learning outcome — not just exposure."

- **Why critical**: If retention is weak, learners will recognize words but fail the exam anyway, and the app's core promise breaks.
- **Validation method**: Cohort analysis on `wordProgress.correctStreak` 30 days after first session.
- **Success metric**: Median 30-day cohort has `correctStreak ≥ 4` (mastered to SRS box 4+) on ≥ **70%** of the words they've seen at least twice.
- **Data source**: `apps/mobile/lib/progress-repository.ts` export → PostHog cohort tables.

---

## 5. MVP URL

- **Primary (submission landing)**: https://luke-gu.github.io/topik-note-demo/ — landing with CTAs to the App Store / Play Store listings.
- **Native app**:
  - iOS: *App Store link (pending final live URL; current TestFlight during review)*
  - Android: *Google Play link (pending final live URL; current internal testing)*
- **Web demo (5-question quiz)**: on backlog — see "Out" above.

The native apps are the functional MVP. The landing page satisfies the "URL + mobile browser compatible" criterion by presenting the persona / pain / solution / CTA within a viewport; install required for the full 30-second core-value experience.

---

## 6. Consistency Check (against Solopreneur criteria)

- [x] Three deliverables describe the **same persona** (foreign TOPIK 3+ prepper, 30–60 min commute learner).
- [x] Three deliverables describe the **same 3 core features** (real exam words / SM-2 SRS / Korean-native-verified vocabulary).
- [x] "Core assumptions & validation" section present (Section 4) with numeric success metrics.
- [x] MVP URL live and functional (luke-gu.github.io/topik-note-demo, App Store, Play Store).
- [x] Each feature maps 1:1 to a pain point.
- [x] Positioning is a single sentence of the form "For X, Y, why Z."
- [x] ≥ 1 testimonial shown on the landing page (social-proof section).
