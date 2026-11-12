# BUILD PROMPT FOR CLAUDE OPUS 5.5 — Short-Video Recipe Import + Weekly Meal Planner — iOS + Android

> Paste everything below this line into Claude Opus 5.5 as the opening message of the build project. Attach `analysis.md` from this folder. Fresh repository.

---

## 0. Role and mission

You are the sole senior engineer building a production iOS + Android recipe manager and weekly meal planner whose hook is **importing recipes from TikTok, Instagram Reels and YouTube via the share sheet**, with AI normalisation, scaling and substitutions, a weekly plan, an aisle-sorted grocery list and household sharing. The founder is non-technical; you own everything.

Revenue depends on three flows — build for them first:

1. **Share a video → structured recipe saved in under 20 seconds** (the "wow" that creators will demo on camera). Reliability of this single flow is the product.
2. **Free → paid ($39.99/yr annual-first; $7.99/mo; $79 Lifetime one-time)** when the user hits the import limit or opens the planner.
3. **Weekly planning habit** (Sunday plan → list → cook) because people who plan renew; people who only hoard recipes churn.

The price anchor is harsh (Paprika sells video import at $14.99/yr). The paid tier must bundle planner + household + unlimited imports + AI, and the **Lifetime** option must exist because this audience hates subscriptions.

## 1. Non-negotiable rules

- **Import is user-initiated and on-device first.** Never run server-side scrapers or download video files. Pipeline order: (1) user shares a URL/caption via share sheet → (2) read only what the platform exposes publicly for that URL without automation beyond a single fetch of the share target's public page metadata/caption, if and only if the platform's terms permit it (gate behind a server-side `platform_policy` table the founder can flip per platform after counsel review; default **off** for TikTok and Instagram, **on** for generic web/blogs) → (3) if nothing usable, ask the user to paste the caption or **screen-record/screenshot the video**; run **on-device OCR** (Vision / ML Kit) and **on-device speech-to-text** (Apple SpeechAnalyzer / Android SpeechRecognizer; whisper.cpp fallback) over the user's own capture → (4) send extracted *text* only to the AI Edge Function for structuring. Never upload the user's video.
- **AI never invents a recipe.** If the extracted text contains ingredients/steps, use them verbatim-ish with normalisation; if it does not, return `insufficient_source: true` and the UI asks for more (paste caption, add screenshot) instead of generating. Every AI field carries confidence; quantities below 0.6 confidence are highlighted for review.
- **No weekly billing.** Annual-first, monthly available, Lifetime available. No countdowns, no second paywall after decline.
- **Consent before text leaves the device for AI** (Apple 5.1.2(i)), naming the provider.
- Export (JSON + Paprika-compatible format + printable PDF) always available, free tier included.
- Respect creators: store the source URL and creator handle on every imported recipe and show it; never strip attribution; provide "open original".

## 2. Tech stack (fixed)

Expo SDK 58 / RN 0.88 (New Architecture), TypeScript strict, Expo Router · **iOS Share Extension** (native target via Expo config plugin) and **Android share intent** receiving text/URLs/images · Supabase (Postgres + RLS, Auth Apple/Google/email, Storage, Edge Functions) · `expo-sqlite` offline cache + outbox (recipes must be readable offline in the kitchen) · RevenueCat (subscriptions + non-consumable Lifetime; Paywalls v2; Experiments) · On-device OCR: iOS Vision `VNRecognizeTextRequest`, Android ML Kit Text Recognition · On-device STT as above · AI via Edge Functions: Claude Haiku 5.5 for structuring/scaling/substitutions, Sonnet 5.5 vision only for screenshot cases where OCR fails · PostHog + Sentry · Vitest, RNTL, Maestro · GitHub Actions · EAS.

## 3. Data model

Common: `id uuid`, `household_id`, `created_by`, `created_at`, `updated_at`, `deleted_at`, `client_updated_at`, `version`.

- `households` — `name`, `plan` (free | premium | lifetime), `owner_user_id`, `invite_code`.
- `household_members` — `user_id`, `role`.
- `recipes` — `title`, `source_url null`, `source_platform` (tiktok | instagram | youtube | web | manual | paprika_import | mealime_import), `creator_handle null`, `servings_base numeric`, `prep_min`, `cook_min`, `tags[]`, `cover_image_path null`, `notes`, `nutrition jsonb null` (approximate, labelled), `ai_meta jsonb` (`{method, confidence_avg, insufficient_source}`), `favorite bool`, `times_cooked int`, `last_cooked_at`.
- `ingredients` — `recipe_id`, `position`, `raw_text`, `name`, `qty numeric null`, `unit text null`, `prep_note`, `aisle` (produce | dairy | meat | seafood | bakery | pantry | frozen | spices | other), `confidence`.
- `steps` — `recipe_id`, `position`, `text`, `timer_seconds null`.
- `plans` — `household_id`, `week_start date`.
- `plan_entries` — `plan_id`, `day`, `slot` (breakfast | lunch | dinner | snack), `recipe_id`, `servings numeric`, `cooked bool`, `cooked_at`.
- `lists` — `household_id`, `plan_id null`, `name`.
- `list_items` — `list_id`, `name`, `qty`, `unit`, `aisle`, `checked bool`, `from_recipe_ids[]`, `manual bool`.
- `pantry_items` — `name`, `always_have bool`.
- `imports` — `user_id`, `source_url`, `platform`, `method` (metadata | caption_paste | ocr | stt | vision), `status`, `error`, `duration_ms`, `ai_cost_cents`.
- `collections` — `name`, `recipe_ids[]`, `creator_handle null`, `public bool`.
- `platform_policy` — `platform`, `metadata_fetch_enabled bool`, `notes`, `updated_at` (server-only).
- `subscriptions_mirror`, `consents`, `exports`.

RLS by household membership. Public collections served via Edge Function with a token.

## 4. Screens and behaviours

Tabs: **Saved · Plan · List · Cook · More**. The share extension is the real front door.

### 4.1 Share-sheet import (the core flow; target ≤ 20 s to saved recipe)
- iOS Share Extension receives URL/text/image → writes to an App Group container → opens the main app via URL scheme to a full-screen **Import** sheet (keep the extension itself tiny: show "Sending to [App]…" and hand off; respect extension memory limits).
- Android: `ACTION_SEND` intent filter for text/plain and image/* → Import screen.
- Import screen states: *Fetching caption* (only if platform policy allows) → *Found a recipe / Need a bit more*. "Need a bit more" offers: **Paste caption** (big text field, auto-reads clipboard with permission prompt), **Add screenshots** (OCR runs on-device, shows extracted text), **Screen recording** (STT on-device over the audio track; show progress). Then AI structuring → review screen (title, servings, ingredients with confidence highlighting, steps) → **Save** (auto-tag, cover image from screenshot if any) → toast "Saved. Plan it?" with a one-tap "Add to this week".
- Free tier: 5 imports/week (counter visible, resets Monday). Hitting the limit opens the paywall with the import still queued so it completes on purchase.

### 4.2 Saved
Grid/list of recipes, search (title/ingredient/tag), filters (time, tags, creator), collections, favourites, "not cooked yet", source badges. Recipe detail: ingredients with a **servings stepper** (scaling via AI-normalised quantities; unit conversion metric/imperial), **substitutions** (AI, on demand, Premium), steps with timers, **Cook mode** (screen stays on, large text, step-by-step, voice "next" optional), original link + creator attribution, "I cooked this" button (feeds retention metrics), notes.

### 4.3 Plan (Premium)
Week view; drag or tap-to-add recipes to day/slot; leftovers ("eat again Thursday"); servings per entry; "Plan my week" suggestion (AI picks from Saved by tags/time; never invents recipes); Sunday 17:00 local reminder (opt-in) "Plan your week in 2 minutes". Generates list in one tap.

### 4.4 List
Aisle-grouped; merges duplicate ingredients across recipes (normalised names/units); pantry "always have" items auto-unchecked; check-off with haptics; shared live across household (Realtime); manual items; share/print; "Send to Instacart/Amazon Fresh" later (behind flag).

### 4.5 Cook
Today's planned meals with cook mode shortcuts; timers; "cooked" check → streak of weeks with ≥3 cooked meals (no shaming).

### 4.6 More
Household (invite link/QR; members), import tools (Paprika/Mealime/CSV/JSON importers), export, units, reminders, subscription (RevenueCat customer center), consents, delete account.

### 4.7 Paywall
Triggers: import limit reached; opening Plan or Substitutions; day 7 soft prompt if ≥5 recipes saved. Content: unlimited imports, weekly planner + list, household sharing, AI scaling/substitutions, cook mode extras, sync. Options: **Annual $39.99 preselected**, Monthly $7.99, **Lifetime $79** (non-consumable; shown as "one payment, forever"). Restore; terms/privacy. Cancellation flow: offer Lifetime upgrade credit and pause before store cancel.

## 5. AI specification (Edge Functions only)

- `structure_recipe`: input `{text_sources: [{kind: caption|ocr|stt|web, text}], locale, units_pref}` → output
```json
{"insufficient_source": false, "title": "", "servings": 4, "prep_min": 10, "cook_min": 20,
 "ingredients": [{"raw_text": "", "name": "", "qty": 1, "unit": "cup", "prep_note": "", "aisle": "produce", "confidence": 0.9}],
 "steps": [{"text": "", "timer_seconds": null}], "tags": [], "warnings": []}
```
Rules in the system prompt: use only provided text; keep original wording where possible; normalise units; if ingredients or steps are missing set `insufficient_source: true` and list what is missing in `warnings`; never add ingredients not present. Zod-validate; retry once; log cost.
- `scale_recipe` and `substitute` (Haiku): pure transformations with explicit constraints; substitutions flag allergens.
- `plan_week` (Haiku): choose from provided recipe IDs only.
- Golden corpus: 150 real-world caption/OCR/STT samples (messy, multi-language, emoji, "recipe in comments" cases). Assertions: zero ingredients not traceable to source text; `insufficient_source` precision ≥ 0.9; schema validity 100%. Run on every prompt/model change.

## 6. Offline, sync, household realtime

Recipes/plan/list cached in SQLite; outbox for writes; last-write-wins per row except list check-offs (merge by item). Realtime channel per household for list and plan. E2E: airplane mode → open saved recipe in cook mode → check list items → reconnect → household member sees state.

## 7. Store compliance

- iOS: Share Extension entitlements + App Group; Speech/Photos/Clipboard usage strings; privacy labels; Sign in with Apple; account deletion; AI consent; Lifetime as non-consumable; subscription disclosures on paywall.
- Android: share intent filters; READ_MEDIA_IMAGES scoped; Data safety; Play Billing via RevenueCat (grace period handling); no background scraping services.
- Listing keywords: "recipe keeper", "meal planner", "save tiktok recipes", "grocery list", "recipe organizer", "paprika alternative", "mealime"; screenshots lead with the share-sheet import moment; preview video shows share → saved → planned → list in 15 s.
- Legal: ship with a `platform_policy` default that disables metadata fetching for TikTok and Instagram until counsel approves; document the on-device approach in the privacy policy; attribution always shown.

## 8. Analytics (PostHog)

`share_received {platform, kind}`, `import_started`, `import_method {method}`, `import_succeeded {duration_ms, confidence_avg}`, `import_insufficient`, `import_failed {error}`, `recipe_saved {platform}`, `recipe_cooked`, `plan_entry_added`, `list_generated`, `list_item_checked`, `household_invited/joined`, `paywall_viewed {trigger}`, `trial_started`, `subscription_started {product}`, `lifetime_purchased`, `renewed`, `cancel_flow_viewed`, `export_requested`.
Dashboards: share→saved success rate and median duration (the product KPI), weekly "cooked" rate per household, import-limit→paywall conversion, annual vs lifetime mix, D7/D30 retention of planners vs non-planners.

## 9. Build order

**Phase 1 (days 1–3):** repo, tokens, Supabase schema/RLS, auth, household creation, CI.
**Phase 2 (days 3–9):** manual recipe CRUD, detail, scaling (deterministic first), cook mode, offline cache, Saved tab.
**Phase 3 (days 7–13):** share extension (iOS) + share intent (Android), Import screen, caption paste, on-device OCR, on-device STT, `structure_recipe` + golden tests, consent screen, free-tier counter.
**Phase 4 (days 13–17):** Plan, list generation with merge/aisle logic, pantry, household invites + Realtime.
**Phase 5 (days 17–20):** RevenueCat products (annual/monthly/lifetime), paywall triggers, customer center, subscription mirror, PostHog funnels.
**Phase 6 (days 20–24):** AI substitutions, plan-my-week, Paprika/Mealime importers, export, collections.
**Phase 7 (days 24–28):** accessibility, empty states, privacy labels, listings, screenshots/preview, TestFlight/Play internal → submit.
**Post-launch:** creator collections/storefronts, grocery-delivery integration, nutrition goals mode, tablet layout.

## 10. Definition of done

CI green; Maestro E2E for share→save→plan→list on iOS simulator + Android emulator + one physical device each (share extension must be tested on a physical iPhone); RLS cross-household test; golden AI tests passing; share→saved success ≥ 90% on the golden set with median ≤ 20 s on device; no video bytes ever uploaded (test asserts upload paths are text/image only); release note with build numbers, cuts, and KPIs to watch.

## 11. How to work

Plan each phase in one page with acceptance tests; state assumptions; pin versions; cite current Apple Share Extension, Android intent, RevenueCat and platform-policy docs in code comments; never weaken tests; when the import can't find a recipe, prefer asking the user for more over generating — trust is the moat in this category.
