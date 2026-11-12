# BUILD PROMPT FOR CLAUDE OPUS 5.5 — GLP-1 Medication Companion — iOS + Android

> Paste everything below this line into Claude Opus 5.5 as the opening message of the build project. Attach `analysis.md` from this folder. Fresh repository.

---

## 0. Role and mission

You are the sole senior engineer building a production iOS + Android companion app for people on GLP-1 medications (semaglutide, tirzepatide, liraglutide, compounded versions, and the 2026 oral pills — Wegovy pill, Foundayo/orforglipron). The founder is non-technical. You own everything from schema to store submission.

The money comes from exactly three things. Prioritise them ruthlessly:

1. **Install → first dose logged and first reminder set in under 90 seconds** (activation).
2. **Free → annual subscription ($49.99/yr; $9.99/mo also offered)** via a well-timed paywall after the user has felt value (first insight, first progress card).
3. **Staying subscribed through titration and into maintenance** (retention features and a maintenance mode instead of cancellation).

Free competitors exist (Noom GLP-1 Companion, MyFitnessPal GLP-1 Support, Novo's Novocare). The paid product must be *better than free* on: pill-era + international coverage, honest side-effect insights, protein/muscle-retention programme, prescriber-ready summaries, off-ramp mode, and privacy. Never ship anything that could be read as medical advice.

## 1. Non-negotiable rules

- **No dosing advice. No titration recommendations. No "medication level" pharmacokinetic charts** unless methodology is disclosed on-screen with a citation (Apple 1.4.1). Default: do not build the level chart in v1.
- Every insight screen carries a short, non-dismissable-once-per-session footer: "Informational only. Talk to your prescriber before changing anything."
- **Medical-device declaration:** the app will be submitted as Health & Fitness with the App Store Connect regulated-medical-device declaration set to "No" — therefore the app must not claim to diagnose, treat, or manage disease. Copy and features must stay inside general wellness (logging, reminders, education, habit support).
- **Health-data privacy:** treat all data as sensitive. Explicit consent on first run; separate consent before any photo leaves the device for AI (Apple 5.1.2(i), name the provider); export and delete account in-app; no third-party ad SDKs; PostHog with no health values in event properties (counts and booleans only).
- No weekly subscriptions. Annual-first. No dark patterns on the paywall or cancellation.
- HealthKit (iOS) and Health Connect (Android) are read/write for weight, steps, workouts only — never store HealthKit data server-side without explicit opt-in.

## 2. Tech stack (fixed)

Expo SDK 58 / React Native 0.88 (New Architecture), TypeScript strict, Expo Router · Supabase (Postgres + RLS, Auth with Apple/Google/email OTP, Storage, Edge Functions) · `expo-sqlite` local cache with outbox for offline logging · RevenueCat (Paywalls v2, Experiments) · Expo Notifications (local scheduled reminders must work with no network and survive reboots; use native local notifications, not push, for dose reminders) · `react-native-health` / Health Connect module · AI via Edge Functions only: Claude Haiku 5.5 for weekly summaries and prescriber questions; Sonnet 5.5 vision for photo meal logging (protein/fibre estimate with explicit ± uncertainty) · PostHog + Sentry · Vitest, RNTL, Maestro E2E · GitHub Actions CI · EAS Build/Submit.

## 3. Data model

Common columns: `id uuid`, `user_id`, `created_at`, `updated_at`, `deleted_at`, `client_updated_at`, `version`.

- `profiles` — `country` (US/GB/CA/AU/EU-*), `units` (metric/imperial), `goal_kind` (weight | maintenance | metabolic_health), `height_cm`, `start_weight`, `target_weight null`, `timezone`, `consents jsonb`.
- `medications` — catalogue (seeded JSON, versioned): `generic_name`, `brand_names[] by country`, `form` (injection | pill), `strengths[]` (with units), `default_schedule` (weekly | daily), `pill_rules` (e.g. empty stomach, water limit, wait minutes), `titration_steps[]` (informational only, as labelled by manufacturer; shown as reference, never recommended).
- `regimens` — user's current plan: `medication_id`, `strength`, `schedule` (cron-like: weekly day/time or daily time), `started_at`, `ended_at null`, `source` (prescriber | compounded | other), `cost_cents_per_fill null`, `fill_interval_days null`.
- `doses` — `regimen_id`, `taken_at`, `strength`, `site` (abdomen_l | abdomen_r | thigh_l | thigh_r | arm_l | arm_r | null for pills), `skipped bool`, `note`.
- `symptoms` — `logged_at`, `kind` (nausea | constipation | diarrhea | fatigue | headache | reflux | injection_site | appetite_loss | dizziness | other), `severity 1-5`, `note`, `linked_dose_id null`.
- `measurements` — `measured_at`, `kind` (weight | waist | hips | body_fat_pct | bp_sys | bp_dia), `value`, `source` (manual | healthkit | health_connect).
- `meals` — `eaten_at`, `description`, `protein_g null`, `fibre_g null`, `calories null`, `photo_path null`, `ai_estimate jsonb null` (with `uncertainty_pct`), `user_confirmed bool`.
- `workouts` — `performed_at`, `kind` (strength | cardio | walk), `minutes`, `source`.
- `hydration` — `logged_at`, `ml`.
- `goals` — `protein_g_per_day`, `fibre_g_per_day`, `water_ml_per_day`, `strength_sessions_per_week`, `steps_per_day`.
- `insights` — generated weekly: `week_start`, `summary_md`, `highlights jsonb`, `prescriber_questions[]`, `model`, `cost_cents`.
- `progress_cards` — `kind`, `image_path`, `created_at`, `shared bool` (opt-in share tracking).
- `reminders` — `kind` (dose | pill_wait | water | protein_checkin | weigh_in), `rule jsonb`, `enabled`.
- `subscriptions_mirror`, `consents`, `exports`.

RLS: `user_id = auth.uid()` everywhere. Insights generated by an Edge Function with service role, scoped to one user per invocation.

## 4. Screens and behaviours

Tabs: **Today · Journey · Log · Insights · More**.

### 4.1 Onboarding (≤ 90 seconds to first reminder; instrument each step)
1. Welcome (what the app is and is not — one line of wellness framing) → consent for health data processing (plain English, link to policy).
2. Sign in (Apple / Google / email OTP) — allow **skip** with local-only mode; sync requires sign-in (prompt at first paywall).
3. "Which medication?" (search with brand names per country; chips for the top 6; "compounded" option; injection vs pill auto-set) → current strength → schedule (day/time or daily time) → **first reminder scheduled** (local notification; confirm with a preview).
4. Goal + units + start weight (optional) → protein target auto-suggested (e.g. 1.2–1.6 g/kg shown as a *range from public guidelines* with source link; user picks).
5. Today screen with "Log your last dose" CTA. Events: `onboarding_*`, `first_regimen_set`, `first_reminder_scheduled`, `first_dose_logged`.

### 4.2 Today
Next dose countdown (or pill timing helper: "wait 30 min before eating" timer where catalogue rules apply), protein/water rings, "How do you feel?" 1-tap symptom chips, weigh-in prompt on weigh-day, quick log buttons. Streak of consistent logging (gentle, never shaming).

### 4.3 Journey
Weight/measurements over time with regimen changes drawn as vertical markers (strength changes, pauses). Dose history with site rotation map (injection) or adherence calendar (pills). Photo timeline (private). "Share progress card" → generates an image (weight change, weeks on treatment, consistency) with no medication name unless the user toggles it; share sheet; `progress_card_shared` event.

### 4.4 Log
Dose (prefilled from regimen; site picker suggests next rotation), symptom (kind + severity + note; optional link to last dose), meal (text or photo → AI estimate with uncertainty; user confirms/edits; protein-first UI), water, workout (manual or HealthKit/Health Connect import), measurement.

### 4.5 Insights (Premium)
Weekly summary (Haiku, markdown) built only from the user's logs: adherence, symptom patterns vs dose timing ("nausea logged within 24h of 4 of the last 5 doses"), protein hit-rate, weight trend, hydration. **Prescriber summary PDF**: last 4 weeks of doses, symptoms, weight, questions. Patterns are descriptive statistics, not recommendations. Footer disclaimer always visible.

### 4.6 Programmes (Premium)
Protein playbook (meal ideas by protein, pantry list), muscle-retention strength programme (3×/week bodyweight/dumbbell, progression logged), hydration and fibre habit tracks, "pill-era" guide (timing rules from the catalogue), **maintenance / off-ramp mode** (when the user marks a regimen as ended or reduced: switches goals to maintenance, keeps habits, adds weekly check-in and "what changed" journaling; never advises how to taper).

### 4.7 More
Profile, medications & regimen history, reminders, goals, HealthKit/Health Connect, data export (CSV + PDF), delete account, subscription (RevenueCat customer center), privacy & consents, about/medical disclaimer.

### 4.8 Paywall
Trigger points: (a) after the first insight preview is generated (day 3–7, soft), (b) on tapping any Premium feature, (c) end of a 7-day trial if the user started one. Content: Insights, prescriber summaries, programmes, photo meal logging, progress cards, cloud sync/multi-device. **Annual preselected** $49.99 ("$4.17/mo"), monthly $9.99. Optional lifetime $129 (toggle via RevenueCat offering experiment). Restore purchases; terms/privacy; no countdowns. Cancellation: offer "maintenance mode at $2.99/mo" and "pause 2 months" before the store's cancel flow (present these in-app, then deep-link to the store management page as required).

## 5. AI specification (Edge Functions only; never client-side keys)

- `weekly_insight`: input = anonymised aggregates (no names), last 28 days of doses/symptoms/measurements/meals/goals; output JSON `{summary_md, highlights: [{kind, text, evidence: {counts...}}], prescriber_questions: [string], safety_flags: [string]}`. System prompt forbids recommendations about dose, frequency, or stopping; must phrase as observations; must include "talk to your prescriber" when `safety_flags` non-empty (e.g. severity-5 symptoms on 3+ days). Validate with Zod; reject on any imperative dosing language (regex deny-list test).
- `meal_estimate` (Sonnet 5.5 vision): output `{items: [{name, grams_est, protein_g, fibre_g, calories, confidence}], total: {...}, uncertainty_pct}`; UI shows "±X%" and requires confirmation; never auto-saves.
- Cost logging per call; alert if monthly AI cost per paying user > $0.60.
- Golden tests: 50 synthetic user months; assert no dosing recommendations, schema validity 100%, safety flags fire on the seeded severe cases.

## 6. Reminders & offline

Dose reminders are **local notifications** scheduled on-device (repeat rules), re-scheduled on app open and after reboot (Android: `RECEIVE_BOOT_COMPLETED`), with "Log now / Snooze 1h / Skipped" actions. All logging works offline via SQLite + outbox; sync on reconnect with last-write-wins per row (`client_updated_at`). E2E test: airplane mode → log dose + symptom + weight → reconnect → server matches.

## 7. Store compliance

- App Store Connect: category Health & Fitness; medical-device declaration "No"; privacy labels (health & fitness, photos, identifiers, usage data); Sign in with Apple; HealthKit usage strings; in-app account deletion; 5.1.2(i) AI consent; disclaimers in listing and in-app; no claims of weight-loss outcomes in listing copy.
- Google Play: Data safety (health data); Health Connect permissions declaration and privacy policy link; POST_NOTIFICATIONS + exact-alarm permission handling (fallback to inexact alarms with user notice); Play Billing via RevenueCat with grace-period banners.
- Listings: title ≤ 30 chars; keywords: "GLP-1 tracker", "Ozempic tracker", "Zepbound", "Mounjaro", "Wegovy pill", "semaglutide", "tirzepatide", UK: "Mounjaro tracker UK"; 6 screenshots per platform (Today, Journey, Insights, Prescriber PDF, Programmes, Progress card); privacy policy/terms drafts flagged for counsel (FTC Health Breach Notification Rule, Washington MHMDA, UK GDPR).

## 8. Analytics (PostHog; booleans/counts only, no health values)

`app_open`, `onboarding_*`, `regimen_set {form}`, `reminder_scheduled`, `dose_logged`, `symptom_logged`, `meal_logged {method}`, `weighin_logged`, `insight_viewed`, `prescriber_pdf_exported`, `progress_card_created/shared`, `paywall_viewed {trigger}`, `trial_started`, `subscription_started {product}`, `renewed`, `cancel_flow_viewed`, `maintenance_mode_selected`, `pause_selected`, `export_requested`, `account_deleted`.
Dashboards: activation (install → first reminder, median seconds), D1/D7/D30 logging retention, paywall conversion by trigger, trial→paid, month-3 payer retention, maintenance-mode uptake, AI cost per payer.

## 9. Build order

**Phase 1 (days 1–3):** repo, design tokens, Supabase schema + RLS + medication catalogue seed (US/UK/CA/AU brands; injections and pills), auth incl. local-only mode, CI.
**Phase 2 (days 3–8):** onboarding, regimen, local reminders (both platforms, reboot-safe), dose/symptom/measurement logging, Today, Journey charts, offline outbox.
**Phase 3 (days 8–12):** HealthKit/Health Connect, meals (text), hydration, workouts, goals.
**Phase 4 (days 12–16):** Insights Edge Function + golden tests, prescriber PDF, progress cards + share.
**Phase 5 (days 16–19):** RevenueCat products, paywall triggers, trial, maintenance-mode and pause offers, subscription mirror, PostHog funnels.
**Phase 6 (days 19–23):** programmes (protein, strength, pill-era guide, off-ramp mode), photo meal logging with consent.
**Phase 7 (days 23–28):** accessibility, empty states, export/delete, privacy labels, listings, screenshots, TestFlight/Play internal → submit.
**Post-launch:** buddy mode (invite + shared streaks), cost/refill tracker, clinic/pharmacy share links (B2B2C), localisation (de/fr/es).

## 10. Definition of done

CI green (typecheck, lint, unit, DB); Maestro E2E for onboarding→reminder→dose log on iOS simulator and Android emulator plus one physical device each; RLS cross-user test; notification reboot test on a physical Android device; golden AI tests passing; no health values in analytics payloads (test asserts); release note with build numbers, what was cut, and the three metrics to watch.

## 11. How to work

One-page plan per phase with acceptance tests before coding; explicit assumptions; pin versions; read and cite current Apple/Google/RevenueCat/HealthKit docs when behaviour is uncertain; never weaken tests; when in doubt between "more features" and "safer wording", choose safer wording — this category gets rejected and sued for the opposite.
