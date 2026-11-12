# BUILD PROMPT FOR CLAUDE OPUS 5.5 — Co-Parenting Ledger with One-Parent Mode — iOS + Android

> Paste everything below this line into Claude Opus 5.5 as the opening message of the build project. Attach `analysis.md` from this folder. Fresh repository.

---

## 0. Role and mission

You are the sole senior engineer building a production iOS + Android co-parenting app: tamper-evident messaging, a custody calendar that models real court orders, a shared expense ledger with receipts and settlements, court-ready PDF exports, and a **one-parent mode that delivers full value even if the other parent never joins**. Priced **per family ($79/yr) or per parent ($49/yr)** — the direct attack on incumbents that bill each parent $110–300/yr. The founder is non-technical; you own everything.

Revenue depends on:

1. **First parent gets value alone in under 5 minutes** (one-parent mode: calendar from their order, first logged exchange, first export) — so they subscribe even before the ex joins.
2. **Second parent joins** (invite flow with zero-friction read-only entry, then upgrade to full participation) — raises retention and justifies the per-family price.
3. **Multi-year retention**: reliability (notifications that actually arrive, with receipts), records that grow in value, multi-year plans, and read-only archive instead of deletion on downgrade.

This product is used in conflict and sometimes in court. Reliability, immutability and careful wording matter more than feature count.

## 1. Non-negotiable rules

- **Immutable records.** Messages, calendar changes and expenses are append-only. Edits create new versions; deletions are tombstones; every record carries a server timestamp and a SHA-256 hash chained to the previous record for that family (`prev_hash`). Exports include the chain so tampering is detectable. Never offer "delete message".
- **Never claim "court-admissible" or "legally binding".** Use "court-ready export" and "timestamped, tamper-evident record". Admissibility is jurisdiction-specific; copy must say so.
- **AI drafts, humans decide.** The custody-order parser produces a *proposed* calendar with every rule linked to the clause it came from; nothing is applied until the parent reviews each rule. Tone-check *suggests* rewording; it never modifies or blocks a message.
- **No legal advice.** AI outputs and UI copy must not interpret law or predict outcomes. A deny-list test enforces this on AI output.
- **Minors' data.** Children are represented by first name/initial and birth year only by default; no photos of children required; data minimisation throughout; explicit consent; export and delete (delete = cryptographic erasure of content while preserving hash chain integrity for the other parent's copy as required — implement content encryption per family with per-parent key escrow; document the design).
- **Notifications are a core feature, not plumbing.** Every message and schedule change must produce a delivery record (`delivered_at`, `read_at`) visible to both parents. Push + in-app + optional SMS/email fallback for undelivered after 2 hours.
- No weekly billing, no countdowns, no per-parent double-billing surprises (price shown per family up front).

## 2. Tech stack (fixed)

Expo SDK 58 / RN 0.88 (New Architecture), TypeScript strict, Expo Router · Supabase (Postgres + RLS, Auth Apple/Google/email OTP, Storage with signed URLs, Edge Functions, Realtime, cron) · `expo-sqlite` cache + outbox (read offline; writes queue and are timestamped server-side on receipt — record both `client_sent_at` and `server_received_at`) · RevenueCat (per-family and per-parent products; Paywalls v2) · Expo Notifications with delivery tracking + Twilio/Resend fallback · PDF via Edge Function (HTML→PDF with embedded hash chain and page numbering) · AI via Edge Functions only: Claude Sonnet 5.5 for custody-order parsing (document → rule schema with clause citations), Haiku 5.5 for tone suggestions and summaries · OCR on-device (Vision/ML Kit) for screenshot logging in one-parent mode · PostHog (no message content in events) + Sentry · Vitest, RNTL, Maestro · GitHub Actions · EAS.

## 3. Data model

Common: `id uuid`, `family_id`, `created_at` (server), `client_sent_at`, `hash`, `prev_hash`, `actor_user_id`.

- `families` — `name`, `plan` (free | premium_family | premium_parent | archive), `jurisdiction` (country + state/province), `timezone`, `created_by`, `encryption_meta jsonb`.
- `parents` — `family_id`, `user_id null` (null until joined), `display_name`, `role` (parent_a | parent_b), `status` (active | invited | never_joined | read_only), `invite_token`, `invited_at`, `joined_at`.
- `children` — `family_id`, `label` (first name/initial), `birth_year`, `notes_encrypted`.
- `messages` — `family_id`, `thread_id`, `body_encrypted`, `attachments[]`, `sent_by`, `delivered_to jsonb` (`{parent_b: {delivered_at, read_at, channel}}`), `tone_suggestion_shown bool`, `tone_suggestion_accepted bool`, `kind` (message | system | external_log).
- `external_logs` — one-parent mode: `source` (sms_screenshot | email_paste | call_note | handover_note), `occurred_at` (user-entered), `logged_at` (server), `ocr_text_encrypted`, `attachment_path`, `note_encrypted`.
- `custody_rules` — `family_id`, `kind` (alternating_weeks | 2-2-3 | 2-2-5-5 | weekdays_weekends | custom_cron), `anchor_date`, `params jsonb`, `holiday_set_id`, `source_clause text null`, `ai_proposed bool`, `approved_by[]`, `effective_from`, `effective_to null`.
- `holiday_overrides` — `rule_id`, `holiday_key`, `year_parity` (even | odd | all), `parent`, `start_rule`, `end_rule`, `source_clause`.
- `schedule_exceptions` — `date_range`, `parent`, `reason`, `proposed_by`, `status` (proposed | accepted | declined | unilateral_logged), `responded_at`.
- `calendar_events` — derived cache per day: `date`, `parent`, `source` (rule | override | exception).
- `expenses` — `amount_cents`, `currency`, `category`, `paid_by`, `split jsonb` (`{parent_a: 50, parent_b: 50}` or amounts), `receipt_paths[]`, `status` (logged | requested | accepted | disputed | settled), `settled_at`, `notes_encrypted`.
- `settlements` — `from_parent`, `to_parent`, `amount_cents`, `method`, `reference`, `confirmed_by[]`.
- `documents` — vault: `kind` (order | school | medical | other), `path`, `name`, `uploaded_by`, `shared bool`.
- `exports` — `requested_by`, `range`, `sections[]`, `pdf_path`, `hash_root`, `created_at`.
- `audit_events` — every read of exports and documents (`who`, `what`, `when`) — shown to both parents.
- `notification_deliveries` — `message_id`, `parent`, `channel`, `attempted_at`, `delivered_at null`, `error`.
- `professionals` — optional: lawyer/mediator read-only share links (`token`, `scope`, `expires_at`).
- `subscriptions_mirror`, `consents`.

RLS: both parents in a family can read family rows; writes restricted by role; `external_logs` visible to the logging parent only until the other parent joins *and* the logger chooses to share (default: private, because one-parent mode is for the user's own records). Document the privacy rules in-app.

## 4. Screens and behaviours

Tabs: **Calendar · Messages · Expenses · Records · More**.

### 4.1 Onboarding (≤ 5 minutes to first value alone)
1. Welcome: "Works even if your co-parent never joins." → sign in (Apple/Google/email) → jurisdiction + timezone → children (label + birth year).
2. "Do you have a custody order or parenting plan?" → **Upload/scan** (PDF/photos → on-device OCR → `parse_order` Edge Function → proposed rules with clause citations) or **Choose a template** (alternating weeks, 2-2-3, 2-2-5-5, weekdays/weekends, custom) → **Review each rule** (accept/edit) → calendar renders for 12 months.
3. "Invite your co-parent" (SMS/email/link; can skip; persistent, non-nagging prompt later). Explain what they will and won't see.
4. First action prompt: log an exchange, add an expense, or export a sample record. Events: `onboarding_*`, `rules_applied {source: ai|template}`, `first_value_action`.

### 4.2 Calendar
Month/week/agenda; colour per parent; holidays and exceptions marked with their source; "propose a swap" (creates `schedule_exception` → other parent accept/decline with timestamps; if the other parent hasn't joined, log as `unilateral_logged` with a note); handover reminders; "who has the kids today" widget (iOS WidgetKit, Android app widget); conflicts flagged (overlapping rules). Export month/year to PDF/ICS; subscribe URL (read-only ICS) for Google/Apple Calendar.

### 4.3 Messages
Single thread per family (plus optional per-child topics); composer with **tone suggestion** (Haiku; appears only when heuristics flag hostility; shows a neutral alternative; user picks); send → delivery/read receipts visible to both; attachments; search; **no edit/delete**; system messages for calendar/expense actions. Message delivery: push with retry; after 2 h undelivered → SMS/email fallback (if the other parent opted in); each attempt recorded.

### 4.4 Expenses
Add expense (amount, category, who paid, split, receipt photo), request reimbursement, accept/dispute, settle (record method/reference), running balance per parent, monthly statement PDF. One-parent mode: expenses log with "not yet acknowledged" state.

### 4.5 Records (one-parent mode lives here)
- **Exchange log:** screenshot of SMS/email → on-device OCR → extract sender/date (editable) → stored as `external_log`; call notes; handover notes with time/location.
- **Vault:** orders, school, medical documents; share toggles.
- **Export:** choose range + sections (messages, calendar, expenses, exchange log, documents) → PDF with cover page, index, timestamps (client-sent and server-received), hash chain root, page numbers; also CSV; audit entry created; share sheet / email to professional.
- **Professional share:** read-only link with expiry for a lawyer/mediator (Premium).

### 4.6 More
Family & co-parent status (invite management), children, notifications (channels, quiet hours — but never suppress delivery records), subscription (RevenueCat customer center; per-family vs per-parent explained), privacy & encryption explainer, consents, export all, delete account (with clear explanation of what remains for the other parent).

### 4.7 Paywall and pricing logic
Free: one-parent documentation mode with 90-day history, template calendar, basic expenses, watermarked exports. Premium: unlimited history, AI order parsing, holiday/exception engine, tone suggestions, delivery fallbacks, full exports, vault sharing, professional links, multi-year archive. Products: `family_annual_7900` (covers both parents; purchaser's store account), `parent_annual_4900`, `family_2year_13900`. If parent B joins a family with an active family plan, they are entitled automatically (server-side entitlement, not RevenueCat per-device). Triggers: after first export preview; on AI parsing; on history limit. Restore; terms/privacy; no dark patterns. Downgrade → **read-only archive**, never data loss.

## 5. AI specification (Edge Functions only)

- `parse_order` (Sonnet 5.5): input = OCR text of the order/plan (+ page refs) → output
```json
{"rules": [{"kind": "alternating_weeks", "params": {}, "anchor_hint": "", "source_clause": "exact quoted text", "page": 3, "confidence": 0.8}],
 "holidays": [{"holiday_key": "thanksgiving", "year_parity": "even", "parent": "parent_a", "start_rule": "", "end_rule": "", "source_clause": "", "confidence": 0.7}],
 "exchange_logistics": [{"text": "", "source_clause": ""}],
 "unparsed_sections": ["quoted text the model could not map"],
 "warnings": []}
```
System prompt: extract only what is written; quote source text for every item; never infer unstated rules; never give legal interpretation; if ambiguous, put it in `unparsed_sections`. Zod validation; deny-list regex test for advice language ("you should", "the court will", "you are entitled").
- `tone_suggest` (Haiku): input = draft message; output `{flagged: bool, reason: string|null, suggestion: string|null}`; must preserve factual content; never adds claims.
- `summarise_period` (Haiku, Premium): neutral factual summary of a date range for exports (counts, dates); no characterisations of either parent.
- Golden corpus: 40 synthetic orders (US states + UK child-arrangements orders) with known rules; assertions: every extracted rule has a source clause that exists verbatim in the input; recall of seeded rules ≥ 0.85; zero advice-language violations.

## 6. Reliability & offline

- Reads offline; writes queue with `client_sent_at` and are hashed on the server at receipt; the UI shows "queued — not yet delivered" states truthfully.
- Delivery pipeline: insert → Realtime → push (Expo) → delivery receipt from the client → `notification_deliveries`; cron every 10 min retries undelivered and triggers SMS/email fallback at 2 h; weekly digest of anything unread.
- Calendar engine is pure TypeScript with exhaustive unit tests (DST transitions, leap years, year-parity holidays, exceptions overriding overrides); shared between app and Edge Functions.
- E2E: two devices/accounts in one family; message sent → delivered/read receipts on both; swap proposed and accepted; export hash chain verifies.

## 7. Store compliance

- iOS: privacy labels (contacts optional, photos, identifiers, user content); Sign in with Apple; account deletion with explanation; AI consent (5.1.2(i)) before uploading order text; WidgetKit extension; no "legal advice" claims in listing; subscription disclosures; family plan explained as covering a second user (allowed — it is your server-side entitlement, not Apple Family Sharing).
- Android: Data safety; POST_NOTIFICATIONS; app widget; Play Billing via RevenueCat; grace-period handling.
- Listings: "co-parenting app", "custody calendar", "co-parent messages", "parenting plan", "child expense tracker", "ourfamilywizard alternative" (as a search term, not in the title); screenshots: calendar from order, delivery receipts, expense balance, court-ready export, one-parent mode.
- Legal drafts flagged for counsel: privacy policy (minors' data, encryption, retention), terms (no legal advice; export disclaimer), jurisdiction notes.

## 8. Analytics (PostHog; no content, no names)

`onboarding_*`, `rules_applied {source}`, `invite_sent`, `coparent_joined`, `message_sent`, `delivery_confirmed {channel, minutes}`, `fallback_triggered`, `tone_suggestion_shown/accepted`, `exception_proposed/accepted`, `expense_logged`, `settlement_recorded`, `external_log_created {source}`, `export_created {sections}`, `professional_link_created`, `paywall_viewed {trigger}`, `subscription_started {product}`, `renewed`, `downgraded_to_archive`.
Dashboards: time-to-first-value (alone), second-parent join rate and time, delivery success rate and median latency (the trust KPI), exports per family, paywall conversion by trigger, 12-month retention, per-family vs per-parent mix.

## 9. Build order

**Phase 1 (days 1–4):** repo, tokens, schema + RLS + hash chain + per-family encryption design doc, auth, family/parents/children, CI.
**Phase 2 (days 4–11):** calendar engine (pure TS, exhaustive tests), templates, holidays, exceptions/swaps, ICS, widgets.
**Phase 3 (days 9–15):** messages with delivery pipeline, receipts, fallback cron, Realtime, offline queue.
**Phase 4 (days 15–20):** expenses, settlements, statements; Records: external logs with OCR, vault, exports with hash chain + PDF; audit events.
**Phase 5 (days 20–24):** `parse_order` + review UI + golden tests; tone suggestions; consent screens.
**Phase 6 (days 24–27):** RevenueCat products, server-side family entitlement, paywalls, archive downgrade, professional links, PostHog.
**Phase 7 (days 27–32):** accessibility, empty states, privacy labels, listings, screenshots, TestFlight/Play internal → submit.
**Post-launch:** lawyer/mediator dashboard (web), payment rails for settlements, UK/AU jurisdiction packs, per-child info sharing (medical/school).

## 10. Definition of done

CI green; calendar engine 100% branch coverage on rule logic; Maestro two-account E2E on iOS + Android (physical devices for push delivery); RLS tests (parent outside family cannot read; parent B cannot read parent A's private external logs); hash-chain verification test on exports; deny-list test on AI outputs; delivery success ≥ 99% in a 200-message test run; release note with build numbers, cuts, risks, KPIs.

## 11. How to work

One-page plan per phase with acceptance tests; explicit assumptions; pin versions; cite current docs for push delivery, WidgetKit, RevenueCat entitlements and Apple family-plan rules in code comments; never weaken tests; when choosing between a feature and a stronger guarantee of delivery/immutability, choose the guarantee — that is what this audience pays for.
