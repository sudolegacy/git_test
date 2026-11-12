# BUILD PROMPT FOR CLAUDE OPUS 5.5 — "Jobsheet" (solo-trades quote-to-cash) — iOS + Android

> Paste everything below this line into Claude Opus 5.5 as the opening message of the build project. Attach `analysis.md` from this folder as context. Work in a fresh repository.

---

## 0. Who you are and what you are building

You are the sole senior engineer building **Jobsheet** (working name), a production mobile app for iOS and Android used by one-van residential service tradespeople (plumbers, electricians, HVAC techs, handymen). The founder has no engineering team; you own architecture, code, tests, release engineering and store submission. You have unlimited effort budget. You do not ask the founder to write code.

The business lives or dies on four flows. Everything else is secondary:

1. **Install → first quote sent in under 3 minutes** (activation).
2. **Trial → paid subscription** ($19/mo or $149/yr via in-app purchase, 14-day trial, price-lock promise).
3. **Quote → invoice → customer pays through the app** (Stripe Connect; platform fee on volume — revenue outside app-store commission).
4. **Automatic payment chasing until paid** (the feature tradespeople talk about to each other).

If a task does not move one of those four flows, it is lower priority. Build in the order given in §9. Ship a TestFlight / Play internal build at the end of every phase.

## 1. Non-negotiable product rules

- **No document caps, ever.** Unlimited quotes, invoices, customers on every plan.
- **Price-lock:** the price a customer subscribes at is the price they keep while continuously subscribed. Show a "Price-lock certificate" in Settings with the date and price. (Implementation: RevenueCat entitlement + stored `locked_price` on the tenant; new price points are new product IDs, never price changes on existing products.)
- **Offline-first:** every core action (create customer, quote, invoice, add line items, take photos) works with no network and syncs later. Payments and sending require network and must say so clearly.
- **Data export always available** (CSV + PDFs zip) from Settings, free tier included, no dark patterns.
- **Human approves every AI output before it is sent.** AI drafts; it never sends, never prices without a price-book basis, never invents line items the tradesperson didn't say. Confidence must be visible.
- **Physical-service payments must NOT use Apple/Google in-app purchase** (Apple guideline 3.1.3(e)); **the app subscription MUST use in-app purchase** (3.1.1). Never mix these.
- **AI data-sharing consent** (Apple 5.1.2(i)): before any audio/photo leaves the device, show a consent screen naming the third-party AI providers (Anthropic; OpenAI for transcription fallback). Store consent timestamp.
- No weekly subscriptions. No fake countdown timers. No "decline → second paywall" pattern (Apple pulled Cal AI for exactly this).

## 2. Tech stack (fixed — do not substitute without a written reason)

| Layer | Choice |
|---|---|
| App | Expo SDK 58 (React Native 0.88, New Architecture), TypeScript strict, Expo Router, EAS Build/Update/Submit |
| UI | React Native core + a small design system you write (tokens, Button, Input, Sheet, ListRow, Money, Badge). No heavy UI kit. Large tap targets (min 48dp), high contrast, usable with gloves/sun. |
| State/data | TanStack Query for server state; local SQLite via `expo-sqlite` with a write-ahead **outbox** table for offline mutations; Zustand for ephemeral UI state |
| Backend | Supabase: Postgres + Row Level Security, Auth (Apple, Google, phone OTP), Storage (photos, PDFs), Edge Functions (Deno/TS) for PDF rendering, AI calls, Stripe webhooks, chase scheduler |
| Payments to tradesperson's customers | Stripe Connect **Express** accounts; Payment Links / Checkout for remote pay; Stripe Terminal SDK for **Tap to Pay on iPhone and Android**; `application_fee_amount` for platform fee |
| App subscription | RevenueCat (iOS + Android) with Paywalls v2; products: `solo_monthly_1999`, `solo_annual_14900`, `team_monthly_3900`, `team_annual_34900` |
| AI | Anthropic Claude: Haiku 5.5 for quote structuring, line-item extraction from text, reminder drafting; Sonnet 5.5 for photo→line items. Transcription: on-device first (Apple SpeechAnalyzer/SpeechTranscriber on iOS 26+, iOS Speech framework fallback; Android SpeechRecognizer), cloud fallback OpenAI `gpt-4o-mini-transcribe`. All AI calls go through Edge Functions (never ship API keys in the app). Strict JSON schemas, temperature 0, retries with validation. |
| Messaging | Twilio (SMS), Resend (email), WhatsApp via `wa.me` deep links; Expo Notifications for push |
| Analytics / errors | PostHog (events, funnels, session replay opt-in), Sentry |
| Testing | Vitest (unit), React Native Testing Library, Maestro for E2E on real devices/simulators, Supabase local for DB tests, Stripe CLI for webhook replay |
| CI | GitHub Actions: typecheck, lint, unit, DB migration check, EAS build on tag |

## 3. Data model (Postgres; write the migration first)

All tables carry `id uuid pk default gen_random_uuid()`, `tenant_id uuid not null`, `created_at`, `updated_at`, `deleted_at` (soft delete), `client_updated_at` (for sync conflict resolution), `version int`.

- `tenants` — business: `name`, `trade` (enum: plumbing, electrical, hvac, handyman, other), `country` (US/GB/CA/AU), `currency`, `tax_mode` (none | sales_tax | vat), `tax_rate_default`, `logo_path`, `address`, `phone`, `email`, `locked_price_cents`, `locked_price_product_id`, `price_locked_at`, `payment_account_status`, `stripe_account_id`, `chase_defaults jsonb`, `brand_color`.
- `users` — `tenant_id`, `auth_user_id`, `role` (owner | member), `display_name`.
- `customers` — `name`, `phone`, `email`, `address jsonb`, `notes`, `source` (manual | import | contacts), `external_ref`.
- `price_book_items` — `name`, `category`, `unit` (each | hour | m | ft | sqft | visit), `unit_cost_cents`, `unit_price_cents`, `markup_pct`, `taxable bool`, `usage_count`, `last_used_at`, `embedding vector(1024) null` (pgvector; optional for fuzzy match).
- `documents` — single table for quotes and invoices: `kind` (quote | invoice), `number` (per-tenant sequential; generated server-side via `tenant_counters`), `status` (draft | sent | viewed | accepted | declined | scheduled | done | unpaid | partially_paid | paid | overdue | void), `customer_id`, `source_quote_id` (invoice created from quote), `title`, `notes_customer`, `notes_internal`, `subtotal_cents`, `tax_cents`, `total_cents`, `deposit_cents`, `amount_paid_cents`, `due_at`, `expires_at`, `accepted_at`, `sent_at`, `viewed_at`, `paid_at`, `public_token` (unguessable, for customer page), `pdf_path`, `ai_draft_id`.
- `line_items` — `document_id`, `position`, `description`, `qty numeric`, `unit`, `unit_price_cents`, `taxable`, `optional bool`, `selected bool`, `price_book_item_id null`, `ai_confidence numeric null`.
- `photos` — `document_id null`, `customer_id null`, `storage_path`, `taken_at`, `caption`, `kind` (before | after | receipt | other).
- `payments` — `document_id`, `provider` (stripe_link | stripe_terminal | cash | bank | other), `amount_cents`, `fee_cents`, `platform_fee_cents`, `stripe_payment_intent_id`, `status`, `received_at`, `payout_id`.
- `chase_sequences` — tenant templates: `name`, `steps jsonb` (array of `{day_offset, channel: sms|email|both, tone: friendly|firm|final, template}`).
- `chase_jobs` — `document_id`, `sequence_id`, `step_index`, `scheduled_for`, `channel`, `status` (pending | sent | skipped | cancelled | failed), `sent_at`, `message_body`, `paused bool`.
- `events` — append-only audit (`document_id`, `type`, `actor`, `payload jsonb`) — drives the activity timeline and "viewed" notifications.
- `ai_drafts` — `input_kind` (voice | text | photo), `transcript`, `raw_response jsonb`, `model`, `tokens_in`, `tokens_out`, `cost_cents`, `accepted bool`, `edits_count`.
- `subscriptions_mirror` — RevenueCat webhook mirror: `entitlement`, `product_id`, `status`, `expires_at`, `store`, `is_trial`, `original_purchase_at`.
- `tenant_counters`, `consents` (`kind`, `granted_at`, `version`), `imports` (`source`, `status`, `mapping jsonb`, `rows_ok`, `rows_failed`).

RLS: every table policy `tenant_id = (select tenant_id from users where auth_user_id = auth.uid())`. Customer-facing public pages read through an Edge Function using `public_token`, never through RLS bypass in the app.

## 4. Screens and exact behaviours

Bottom tabs: **Today · Quotes · Invoices · Customers · Money**. Floating mic/plus button on every tab → "New quote (voice)", "New quote (type)", "New invoice", "New customer", "Take payment".

### 4.1 Onboarding (target ≤ 3 minutes to first quote sent; instrument every step)
1. Welcome → Sign in with Apple / Google / phone.
2. "What's your trade?" (4 big tiles + Other) → "Where do you work?" (US/GB/CA/AU; sets currency, tax mode, date format, phone format, Tap to Pay availability).
3. Business name + optional logo (camera/gallery) — skippable.
4. Import customers: from phone contacts (select-all or pick), or CSV (Joist / Invoice Simple / generic — AI column mapping via Haiku, show mapping for confirmation), or skip.
5. **"Say your last job out loud."** Full-screen mic, live transcript, 60-second cap. On stop → AI draft quote appears with line items, prices from a trade-default starter price-book (ship starter price-books per trade/country as JSON seeds), confidence chips. User edits prices inline → "Send to myself" (SMS/email) → sees the customer page and PDF.
6. "Connect payments to get paid on site" → Stripe Connect Express onboarding (can defer; show persistent banner later).
7. Trial starts automatically (no card). Show "14 days of unlimited quoting — your price if you stay: $19/mo or $149/yr, locked".
Events: `onboarding_step_viewed/completed {step}`, `first_quote_drafted`, `first_quote_sent`, `payments_connected`, with timestamps so time-to-first-quote is measurable.

### 4.2 Today
Cards: "Unpaid — $X across N invoices" (tap → list), "Quotes awaiting answer", "Jobs today", "Payouts on the way", "Connect payments" banner if not connected, "Trial: N days left" pill (tap → paywall). Pull-to-refresh. Empty states push toward creating a quote.

### 4.3 New quote (voice)
Full-screen record; on-device transcription streams text; cloud fallback if on-device unavailable. After stop: Edge Function `ai_draft_quote` returns JSON (schema in §5). Render editable draft: title, customer (match existing by name/phone; else create), line items with qty/unit/price, optional items, deposit %, notes. Each AI-generated item shows a confidence chip (green ≥0.8, amber 0.5–0.8, red <0.5) and "from your price-book" badge when matched. Buttons: **Send**, Save draft, Add photo, Add item from price-book. On Send: choose SMS / email / WhatsApp / copy link; generate PDF; create `events: sent`; set `expires_at` default 30 days.

### 4.4 Quote (customer web page, served by Edge Function, mobile-first HTML)
Branding, line items, optional items with checkboxes that update total, deposit request, **Accept** (name + typed signature + timestamp + IP → `accepted_at`), **Pay deposit** (Stripe Checkout). Viewing fires `events: viewed` → push to tradesperson "Dave viewed your quote". Declined → optional reason.

### 4.5 Convert to invoice
One tap from an accepted/done quote: copies line items (selected optional items only), carries deposit as paid, sets `due_at` (default: on receipt / 7 / 14 / 30 days per tenant setting), number from counter, PDF, send. Partial invoices (progress) allowed.

### 4.6 Take payment
Sheet: amount (prefilled balance), method: **Tap to Pay** (Stripe Terminal; show availability per device/country), **Send pay link**, **Cash**, **Bank transfer** (mark as paid manually with reference). On success: `payments` row, document status → paid/partially_paid, chase jobs cancelled, receipt sent to customer, confetti-free but clear "Paid $X" state. Platform fee: `application_fee_amount` = round(amount × fee_bps / 10000) with `fee_bps` from tenant config (default 50 bps). Show the customer-facing fee transparently (tradesperson chooses whether to pass processing fees where legal).

### 4.7 Auto-chase
Per-tenant default sequence (editable): day +1 friendly SMS+email ("Hi {first}, here's the invoice for {title} — pay here {link}. Thanks! — {business}"), day +7 firm, day +14 final with late-fee notice if enabled. Per-invoice: pause/resume, skip next, edit message. Scheduler: Supabase cron → Edge Function `run_chase_jobs` every 15 min, idempotent (claim with `update ... where status='pending' and scheduled_for <= now() returning`), respects quiet hours (no sends 20:00–08:00 local), stops on paid/void. Every send logged in `events`. AI (Haiku) may **draft** tone variants; the stored template is what sends.

### 4.8 Customers, Price-book, Money, Settings
Customers: list/search, detail with timeline (quotes, invoices, payments, photos), call/SMS/WhatsApp buttons, map link. Price-book: list grouped by category, usage-sorted, quick add from any line item ("save to price-book"), bulk edit margins. Money: collected this week/month, outstanding by age (0–7, 8–30, 31+), payouts (Stripe balance/transfers), export. Settings: business profile, tax, numbering, chase defaults, payments (Stripe dashboard link), subscription (RevenueCat customer center: manage, pause, restore), price-lock certificate, data export, consents, delete account.

### 4.9 Paywall (RevenueCat Paywalls v2; A/B via Experiments)
Triggered: day 10 of trial (soft, dismissible), trial end (hard: app usable read-only + export until subscribed), and from the Today pill. Content: "Unlimited quotes & invoices · Get paid on site · Auto-chase · Your price locked at $149/yr". Annual preselected ("2 months free"). Monthly visible. Team toggle. Restore purchases. Terms/privacy links. No countdowns, no second paywall after decline.

## 5. AI specification (Edge Function `ai_draft_quote`)

Input: `{tenant_id, transcript | text | photo_paths[], locale, currency, trade, price_book: [{id,name,unit,unit_price_cents,category}] (top 300 by usage), tax_mode, tax_rate}`.

System prompt essentials: "You convert a tradesperson's spoken job description into a quote. Use ONLY the provided price-book for prices when an item matches (fuzzy match on name/synonyms); otherwise set `unit_price_cents: null` and `needs_price: true`. Never invent work not described. Mark anything inferred (e.g. 'disposal', 'travel') as `optional: true` with `inferred: true`. Output JSON only."

Output schema (validate with Zod; reject and retry once on failure):
```json
{
  "title": "string",
  "customer": {"name": "string|null", "phone": "string|null", "address": "string|null"},
  "line_items": [{
    "description": "string",
    "qty": "number",
    "unit": "each|hour|m|ft|sqft|visit",
    "unit_price_cents": "number|null",
    "price_book_item_id": "string|null",
    "needs_price": "boolean",
    "optional": "boolean",
    "inferred": "boolean",
    "confidence": "number 0-1"
  }],
  "deposit_pct": "number|null",
  "notes_customer": "string|null",
  "questions_for_tradesperson": ["string"]
}
```
Photo→line items (`ai_items_from_photos`, Sonnet 5.5 vision): returns materials/quantities visible with confidence; never prices without price-book match. Log every call to `ai_drafts` with token counts and cost; alert if cost/draft > $0.05.

Golden corpus: create `/ai/golden/` with 100 realistic transcripts (US and UK phrasing across the four trades; include messy speech, prices said aloud, corrections mid-sentence). Write a test that runs the function against the corpus and asserts: no hallucinated items (items must trace to transcript spans), price-book match precision ≥ 0.9, schema validity 100%. Run on every prompt/model change.

## 6. Offline & sync

- All reads from SQLite; background sync via TanStack Query + outbox. Outbox rows: `{op, table, row_id, payload, client_updated_at, attempts}`; push in order; on 409 (server `version` newer) apply **last-write-wins per field** for documents/customers using `client_updated_at`, but **server-wins** for `status`, `amount_paid_cents`, `payments`, `number`.
- Document numbers: assigned by server on first sync; show "Draft" locally until then. Never send a document that has no server number (sending requires network anyway).
- Photos: stored locally, uploaded in background with resumable uploads; PDF generation waits for photo upload.
- Show a persistent, honest offline indicator; never silently drop writes. Write an E2E test: airplane mode → create customer + quote with 5 items + photo → reconnect → verify server state and PDF.

## 7. Store compliance & release

- iOS: Sign in with Apple required (you offer Google); Tap to Pay entitlement request (document the steps for the founder); Speech/mic/camera/contacts/photos usage strings that explain the benefit; App Privacy nutrition labels (financial info, contacts, photos, usage data; identifiers for Sentry/PostHog); Account deletion in-app; 5.1.2(i) consent flow; subscription disclosure text and links on the paywall; Restore Purchases.
- Android: Play Billing via RevenueCat; Data safety form; background work via WorkManager for sync; POST_NOTIFICATIONS runtime permission; handle Play billing grace period / account hold (RevenueCat statuses) with an in-app banner; target current API level.
- Both: deep links for customer pages (`https://<domain>/q/<token>`), universal links to open paid-status in app; crash-free sessions ≥ 99.5% before public release.
- Produce: store listings (title ≤ 30 chars, subtitle, keyword list for US/GB: "plumber invoice app", "electrician estimate", "handyman quote", "invoice maker", "get paid"), 6 screenshots per platform showing the voice→quote moment first, a 20-second preview video script, privacy policy and terms drafts (flag for lawyer review), support email auto-responder.

## 8. Analytics & money dashboards (PostHog)

Events (with properties): `app_open`, `onboarding_*`, `quote_created {input: voice|text|photo}`, `ai_draft_accepted {edits_count, items, confidence_avg}`, `quote_sent {channel}`, `quote_viewed`, `quote_accepted`, `invoice_created {from_quote}`, `invoice_sent`, `payment_connected`, `payment_received {method, amount, fee}`, `chase_sent {step, channel}`, `chase_paused`, `paywall_viewed {trigger}`, `trial_started`, `subscription_started {product}`, `subscription_renewed`, `subscription_cancelled {reason}`, `pause_selected`, `export_requested`.
Dashboards: activation funnel (install → first quote sent, median minutes), trial→paid by cohort, documents per account per 14 days, payments attach rate, chase→paid days, churn with reasons, AI cost per draft. These are the numbers the founder uses to decide whether the business works; they are not optional.

## 9. Build order (phases; each ends with a device build and a written release note)

**Phase 1 — Skeleton (days 1–3):** repo, Expo app, design tokens, Supabase project + migrations + RLS + seed price-books, auth, tenant creation, CI.
**Phase 2 — Core documents (days 4–10):** customers, price-book, quotes (type), line items, totals/tax, PDF Edge Function, send-by-link, customer web page, quote→invoice, offline outbox + sync, E2E for the full loop.
**Phase 3 — Voice & AI (days 8–14, overlaps):** on-device STT + cloud fallback, consent screen, `ai_draft_quote`, draft editor with confidence, golden-corpus test, onboarding "say your last job".
**Phase 4 — Money (days 12–18):** Stripe Connect Express onboarding, pay links/Checkout, webhooks (idempotent), payments table, statuses, receipts, Money tab, platform fee; Tap to Pay (iOS first, then Android) behind a feature flag.
**Phase 5 — Auto-chase (days 16–21):** sequences, scheduler, Twilio/Resend, quiet hours, pause/skip, events timeline, "viewed" push.
**Phase 6 — Monetisation (days 19–24):** RevenueCat products/entitlements, trial logic, paywalls (day-10 soft, trial-end hard), price-lock certificate, customer center, pause flow, subscription mirror webhook, PostHog funnels.
**Phase 7 — Polish & submit (days 24–30):** empty states, accessibility (VoiceOver/TalkBack labels, dynamic type), haptics, error states, import flows (contacts/CSV), export, privacy labels, listings, screenshots, TestFlight + Play internal → submit for review.
**Post-launch backlog (in order):** Team tier (multi-user, shared schedule), QuickBooks/Xero CSV export, review requests after paid, UK VAT/CIS specifics, recurring jobs mode, AI photo→items, AI phone answering add-on.

## 10. Definition of done (for every phase)

- Typecheck + lint + unit + DB tests green in CI; Maestro E2E for the phase's critical path passing on an iOS simulator and an Android emulator, and manually on one physical device of each.
- No API keys in the app bundle; RLS verified with a test that a second tenant cannot read the first tenant's rows.
- Stripe webhooks replayed twice produce no duplicate payments (idempotency keys on `stripe_payment_intent_id`).
- Chase scheduler run twice concurrently sends each job once.
- Activation path measured: a fresh install reaches "quote sent" in ≤ 3 minutes in a scripted run.
- Release note lists: what shipped, what was cut and why, known risks, the exact TestFlight/Play build numbers, and the top 3 metrics the founder should look at this week.

## 11. How to work

- Before coding each phase, write a one-page plan with the data flows and the acceptance tests, then implement. State assumptions explicitly in the plan; don't silently decide product questions — pick the option that best serves the four money flows and flag it.
- Prefer boring, well-documented libraries. Pin versions. Write migrations as forward-only SQL files.
- When Apple/Google/Stripe/RevenueCat behaviour is uncertain, read the current official docs and cite the page in the code comment.
- Every PR description includes: what changed, how it was tested (with the actual commands and device), and which metric it affects.
- Never weaken a test to make it pass. Never ship a paywall pattern you would be embarrassed to defend to Apple review.
