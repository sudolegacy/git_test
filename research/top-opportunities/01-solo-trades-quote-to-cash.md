# 01 — Solo-Trades Quote-to-Cash (Score 78/100) — WINNER

**Concept:** mobile-first quoting, invoicing and get-paid app for one-van residential service tradespeople (plumbers, electricians, HVAC, handymen; 1–3 person crews). Arrive on site → describe the job by voice or photos → AI drafts a priced quote from the tradesperson's own price-book → customer accepts and pays a deposit by link or Tap to Pay → job done → quote becomes invoice in one tap → automatic, polite payment-chasing until paid.

**Pricing:** $19/month or $149/year (Solo), $39/month or $349/year (Team, up to 3 users). 14-day full trial, no card. Written price-lock for as long as the customer stays subscribed. No document caps. Offline-first. Secondary revenue: small platform fee on card payments processed through the app (exempt from app-store commission under Apple guideline 3.1.3(e), V).

**Working names:** Jobsheet · Quoted · Paidly · SiteSlip · Callout · Tradeslip

Evidence labels: **V** verified (primary/press), **3P** third-party estimate, **U** unverified, **Calc** own calculation. Research date 12 Nov 2026.

---

## 1. Score breakdown

| Criterion | Score | Rationale |
|---|---|---|
| Demonstrated market demand | 17/20 | Enormous paying bases at every tier: Invoice Simple 4.9★/123K US ratings, Invoice Fly 4.8★/111K, Invoice2go 4.8★/56K (V); Jobber 100K+ customers, 400K+ daily users (V); ServiceTitan FY26 revenue $961M +24% (V) |
| Revenue potential | 17/20 | B2B pricing $19–39/mo plus payments take-rate; net LTV/payer ≈ $564 moderate (Calc) — ~3× the consumer finalists |
| Competition & differentiation | 9/15 | Crowded; Square/Wave/Zoho offer free invoicing; Joist (Aug 2026) and Jobber Teammate (Sept 2026) shipping AI quoting (V). No incumbent combines price-lock + no caps + offline + auto-chase for solos, but that is an offer, not a moat |
| Customer acquisition | 10/15 | ASO hard ("invoice" keyword difficulty 59–77/100, 3P); trade creators and Facebook groups are proven channels (Tradify 106 YouTube sponsorships, 3P); Apple Ads Business CPI $6.86 (3P) |
| Retention | 9/10 | Business data gravity (customers, quotes, payment history); seasonal pause instead of cancel |
| Development feasibility | 7/10 | Payments (Stripe Connect KYC), PDF fidelity, offline sync, Tap to Pay entitlements |
| Profitability & scalability | 9/10 | ~85% gross margin; AI cost ≈ cents per quote; break-even ≈ 250 payers (Calc) |
| **Total** | **78** | |

**Biggest risk:** "generic invoicing" is a graveyard; the product must stay vertical and prove a channel at ≤$50 fully-loaded CAC.

---

## 2. Market

- **US:** 2.9M construction (NAICS 23) businesses with no employees; 1.9M are specialty-trade contractors averaging <$70K receipts (Census NES via NAHB, 3P citing V data). 78.2% of construction establishments are non-employer (CPWR, V). BLS CPS ≈ 1.6M unincorporated self-employed in construction (3P). NAICS 23 excludes landscaping and cleaning, so the real base is larger.
- **UK:** 756K self-employed in construction, Q3 2025 (ONS via Construction News, V).
- **Australia:** 278,687 non-employing construction businesses of 462,939 total, June 2025 (ABS, 3P).
- **Home services:** 2.5M+ US home-service businesses, $650B annual spend (NewView Capital, V investor statement).
- **Software market:** field-service management $5.10B (2025) → $9.17B (2030), 12.5% CAGR (MarketsandMarkets, V as published; other estimates differ ~2×).
- **Demographics:** owner-operators 25–55, on-site all day, phone-first, often paid by cash/Zelle/bank transfer, chronically chasing invoices.

---

## 3. Customer problem

1. **Who:** 1–3 person residential service trades.
2. **Frequency:** every job — multiple quotes/invoices per week; admin after a 10-hour day.
3. **Importance:** directly tied to cash flow; late payers are the #1 emotional complaint.
4. **What they use now:** Invoice Simple, Invoice Fly, Joist, Jobber Core, Housecall Pro Basic, Square Invoices, paper/WhatsApp.
5. **Cost of current solutions:** $6.99–21.99/mo (generic apps), $29–79/mo (platforms), free (Square/Wave) but desktop-first.
6. **Why insufficient:** document caps, repeated price hikes, pop-ups, paywalled basics (logo, photos), no auto-chase, overkill platforms for solos.
7. **Will they pay:** yes — already paying at every tier; the question is switching cost, not willingness.

**Verbatim pain (App Store review pages V; forums via snippets 3P/U):**
- "Just to send 5 invoices a month you have to pay $8 per month." — Joist review, 2024
- "I can't justify paying for it to only be able to have 5 sales per month." — Joist review, Oct 2026
- "they put way too many pop-up boxes telling you about new features or trying to get you to use their AI." — Joist review
- "Now it only lets me make 10 invoices a month or I have to upgrade for another 300$ to the unlimited." — Invoice Fly review (3P)
- "Descent app but after I subscribed it sent me an email of a price increase for my subscription about 2 weeks later, not cool." — Joist review (3P)
- "Was billing a client yesterday and realized I'm paying Invoice2go $25/month just to send PDFs." — r/smallbusiness (U, relayed)
- "It drives me up the wall when customers take forever to pay and come out with excuses." — ElectriciansForums, Mar 2024 (also wants invoice-viewed notifications)
- "some are too expensive at £34 a month … jobber and servicem8 are the big ones (overkill if you're a side hustle)." — DIYnot, Aug 2026
- "Invoice simple what I use quick and easy… invoice them from your phone before you leave the drive." — PlasterersForum (positive signal for speed)

Review mining of 842 US App Store reviews (Nov 2025–Nov 2026, 3P): Invoice Simple 49 1–2★ reviews, 22 on price, 9 on invoice limits; Joist 13 of 31 on price; Jobber 12 of 60; Housecall Pro mostly bugs/support; Square Invoices mostly held funds. Another tracker: 58% of Invoice Simple 1–3★ cite "frequent and aggressive price increases", 47% cite invoice limits mid-subscription (3P).

---

## 4. Competitor analysis (USD, Nov 2026)

| Product | Owner | Free tier / caps | Price | US App Store | Play | Notes |
|---|---|---|---|---|---|---|
| Invoice Simple | EverCommerce (acq. 2020, ~$32.5M, 3P citing SEC) | 14-day trial | Essentials $6.99 (3 inv/mo), Plus $14.99 (10), Premium $21.99 (unlimited) (V/3P) | 4.9 / 123K (V) | 10M+ (U) | Plus doubled from $7.49 Oct 2026 (3P); est. iOS rev $2.0M/mo (3P, low confidence) |
| Invoice Fly | independent | — | tiered, caps | 4.8 / 111K (V) | 4M+ claimed (V) | est. $0.85–2M/mo (3P) |
| Joist | EverCommerce (acq. 2019, V) | Basics capped 5 docs/mo | $10 / $17 / $32 / $100 (V) | 4.7 / 14.5K (V) | 1M+ | free tier removed; price $8 (Nov 2024) → $10 (2026); AI text/voice estimates rolling out Aug 2026 (V) |
| Invoice2go | Bill.com (acq. ~$625M 2021, V) | 30-day trial, card required | $7.99 / $11.99 / $44.99; 30/100/unlimited invoices per yr; card 3.5%/3.0%/2.9% (V/3P) | 4.8 / 56K (V) | — | |
| Jobber | VC ($237M raised, 3P); $100M+ ARR (founder podcast, U); "$250M ARR" (U, modelled) | 14-day trial | Core $29 annual / $49 monthly; Connect $99–299; Grow $149–399; Plus $399–529; +$29/user; cards 2.9%+30¢, Tap to Pay 2.7%+30¢, ACH 1% (V/3P) | 4.8 / ~22K (V) | 1M+ | 100K+ customers, 400K daily users, 70+ countries (V, May 2026); Teammate AI beta 23 Sept 2026 (V); AI receptionist $29 add-on (3P); affiliate + ambassador programmes (V) |
| Housecall Pro | VC (~$1.1B 2022, 3P); NewView tender Sept 2025 (V) | none | Basic $79 monthly / $59 annual; Essentials $189/$149; Max $329/$299; card from 2.59%, ACH 1% (V) | 4.7 / 32K (V) | 500K+ | Basic was $49 in 2022 (3P); 200K+ pros |
| ServiceTitan | public (TTAN) | — | enterprise | — | — | FY26 revenue $961M +24% (V, 10-K); FY27 guide $1.139–1.144B (V) |
| Square Invoices | Block | **Free, unlimited** | Plus $49, Premium $149; free-plan card 3.3%+30¢, ACH 1% (V) | — | — | complaints: held funds |
| Wave | H&R Block | Free unlimited | Pro $19; card 2.9%+60¢ (V) | — | — | desktop-first |
| Zoho Invoice | Zoho | Free: 500 invoices/yr, 2 users (V) | none | — | — | |
| QuickBooks | Intuit | 2 invoices/mo free (unlimited with QB Payments) | Solopreneur $20, Simple Start $38 (V) | — | — | |
| Tradify | independent (NZ) | 14-day trial | $47 / $51 / $61 per user/mo (V) | 4.8 / 179 US (V) | 100K+ | 106 tracked YouTube sponsorships (3P), Bald Builders partnership (V) |
| ServiceM8 | independent (AU) | 30 jobs/mo free | $29 (50 jobs) → $349 (V) | 4.6 / 867 US (V) | 50K+ | tiny in US |
| Bookipi | independent | 3 docs/mo rolling | ~$7.60–9.99/mo; iOS $129.99/yr (V/3P) | 4.9 / 16K (V) | ~1.7M (3P) | 1M+ businesses claimed; ships Tap to Pay |
| Billdu | team.blue (majority Nov 2023, V) | 3 invoices/yr | Lite $4.99 annual, Standard $9.99, Premium $19.99 (V) | 4.8 / 26K (V) | 500K+ | 200K+ customers |
| SimplyWise Cost Estimator | independent | — | $29.99/mo or $239.99/yr (V) | 4.8 / 41.6K (V) | — | photo→estimate; largest AI-estimating base found |
| QuoteIQ | independent | — | from $29.99/mo (V) | 4.7 / ~3.4K | — | built by two contractor-YouTubers (~1M subs combined, PR/U); claims 40K+ contractors |
| Handoff | VC ($5.8M Jul 2025, V) | — | from $119/mo | 4.8 / 1.9K | — | voice/text/plan-set estimates |
| BuildWell | independent | — | $7.99/wk or $79.99/yr (V) | — | — | voice, text, photos |
| Contractor+ | independent | 5 docs/mo | Pro $49 ($29 annual) (3P) | — | — | |

**Pattern:** the simple apps are PE roll-ups (EverCommerce, Bill.com, team.blue) monetising via caps and price hikes; the platforms are VC-funded and moving up-market with AI agents. Bending Spoons' acquisitions (MileIQ, Harvest) drew "outrageous price hike" coverage (Bloomberg, Aug 2026, V). The solo operator is squeezed between the two — that is the gap.

**AI quoting is no longer unique:** Joist "Estimate with AI" (text/voice, all plans, limited rollout Aug 2026, no taxes/deposits/markups, no photo input); Jobber Teammate drafts quotes; SimplyWise and QuoteIQ do photo-to-estimate; a long tail of tiny voice-to-quote indies (Kvota, Priced, VanBoss, Quinvo, InstaQuotes, FieldFrame). No competitor was found marketing automatic late-payment chasing as a core feature (not exhaustively searched).

---

## 5. Distribution and viral potential

- **YouTube trade creators:** Electrician U 957K subs, Roger Wakefield 733K (1.7M+ cross-platform), Mikey Pipes 208K (vidIQ, 3P).
- **TikTok:** @lextheelectriciann 1.1M+ (3P), Brian Ridge 450K (U), The Bald Builders (UK) 1M+ TikTok / 291K Instagram (U).
- **Facebook groups:** Plumbing Hacks 60K+ (3P), ContractorREACH 180K+ across state groups (U), ServiceTitan Hacks 11.5K (U).
- **Competitor tactics:** Tradify sponsorships (106 deals/5 channels, 3P); Jobber affiliate + ambassador programme (V), 23 sponsored creators (3P); Jobber podcast (V); referred customers +5% LTV (SaaSquatch case study, vendor).
- **App Store search:** "invoice maker" difficulty 59–73/100; "invoice" 77/100, ~3,600 searches/day (3P/U); top-10 apps average ~42K reviews; no app launched in the last 6–12 months reached 50 ratings (3P). Organic search drove 70% of non-game installs (Sensor Tower 2020, V but dated).
- **Paid:** Apple Ads US 2025 median Business CPI $6.86, CPT $3.33, conversion 55.6% (AppTweak, 3P).
- **Shareability:** every quote/invoice page carries "Sent with [Name]"; "paid in X days" summary card designed for screenshotting into trade groups; creator content is naturally demo-able (talk → quote appears). Referral: month-for-month.

**Growth ladder**
- *First 100 (days 0–30):* 40 founder interviews in one metro (inspect last 10 invoices); 20 hand-onboarded paying pilots at $19; value posts in trade Facebook groups; supply-house counters (flyer + QR); r/Plumbing, r/electricians, r/handyman quoting AMAs.
- *First 1,000 (months 2–4):* 10–15 micro-creators (10–100K) flat fee + affiliate; one mid-size YouTube sponsorship test ($2–5K) with tracked promo; long-tail ASO ("plumber invoice app", "electrician estimate app"); review prompts after a paid invoice.
- *First 10,000 (months 5–12):* repeatable creator programme (20–40, performance-paid); supplier/bookkeeper B2B2C partnerships (test one partner for 20 activated customers first); UK launch with CIS/VAT via UK creators; Apple Ads brand + long-tail with ROAS gates; per-trade web-to-app landing pages; "paid faster" case studies.
- *First 100,000 (year 2+):* adjacent trades (cleaning, landscaping, detailing), AI phone answering wedge ($29–79/mo category), integrations marketplace, AU/CA, payments-led upsell, embedded financing; paid UA at scale only once blended CAC payback <6 months across two channels.

---

## 6. Monetisation design

- **Free:** 14-day full trial, no card (B2B trials start 85% on day 0 per RevenueCat 2025; 17–32-day trials convert 42.5% vs 25.5% for <4 days, V).
- **Paid:** Solo $19/mo or $149/yr (unlimited everything, payments, auto-chase, offline). Team $39/mo or $349/yr (3 users, shared schedule). Price-lock certificate in settings.
- **Renewals:** annual default ("2 months free"); reminder 7 days before; in-app "year in review" (invoices sent, hours saved, money collected) 30 days before renewal.
- **Cancellation reduction:** pause 1–3 months at $0 (seasonal lulls); data export always available; Google Play grace periods + retries (31% of Play cancellations are billing failures vs 14% iOS, V).
- **LTV levers:** payments adoption (+$5–15/mo/payer at 0.5% on $1–3K/mo GMV), Team upgrade, add-ons later (AI phone answering, supplier price-books, bookkeeping export).
- **Store rules:** subscription must use IAP (3.1.1, V); payments to the tradesperson must not (3.1.3(e), V); AI data-sharing needs explicit consent naming the provider (5.1.2(i), V). Apple Small Business 15%; Google Play 15% first $1M (V).
- **Why subscription is justified:** recurring value on every job; not a one-off utility.

---

## 7. Financial model (Calc — assumptions, not forecasts)

Blended: $19.99/mo, $149/yr, 45% annual → $16.58 gross ARPPU/month, $14.09 net of 15% store fee. AI ≈ $1.20/payer/month (≈40 voice quotes at Haiku-class pricing + transcription). Infra fixed $400 + $0.02/MAU. "Net" excludes marketing and salaries. For a B2B tool, MAU ≈ trial + paying accounts.

| Scenario | % MAU paying | Monthly churn | Payments take & GMV/payer/mo | Lifetime | Net LTV/payer |
|---|---|---|---|---|---|
| Conservative | 6% | 6.0% | 0.3% on $1,500 | 17 mo | $290 |
| Moderate | 10% | 4.5% | 0.5% on $2,500 | 22 mo | $564 |
| Optimistic | 15% | 3.5% | 0.75% on $4,000 | 29 mo | $1,226 |

**Moderate scenario**

| MAU | Payers | Subscription MRR | Payments rev | Gross profit | Infra | Net before marketing |
|---|---|---|---|---|---|---|
| 1,000 | 100 | $1,658 | $1,250 | $2,539 | $420 | $2,119 |
| 5,000 | 500 | $8,291 | $6,250 | $12,697 | $500 | $12,197 |
| 10,000 | 1,000 | $16,582 | $12,500 | $25,395 | $600 | $24,795 |
| 50,000 | 5,000 | $82,910 | $62,500 | $126,974 | $1,400 | $125,574 |
| 100,000 | 10,000 | $165,820 | $125,000 | $253,947 | $2,400 | $251,547 |
| 500,000 | 50,000 | $829,100 | $625,000 | $1,269,735 | $10,400 | $1,259,335 |

**Conservative** net before marketing at the same MAU steps: $624 / $4,718 / $9,837 / $50,784 / $101,968 / $511,441.
**Optimistic:** $6,014 / $31,671 / $63,742 / $320,310 / $641,020 / $3,206,702.

**Price sensitivity** (10K MAU, 1,000 payers, net of store): $9.99/$79 → $7,188; $14.99/$119 → $10,801; **$19.99/$149 → $14,095**; $29.99/$249 → $21,957; $39.99/$349 → $29,820. RevenueCat: higher-priced apps show 6× year-1 LTV and ~2× trial conversion — do not go below $19.

**CAC:** Apple Ads Business CPI $6.86 × (12% install→trial × 40% trial→paid) → ≈ **$143/payer, ~10-month payback** on subscription alone (≈6 months incl. payments). Creator/community blended CPI $3 → ≈ **$62/payer, ~4-month payback**. Red-team gate: ≤$50 fully loaded — requires community/creator/partner channels in year one, not Apple Ads.

**Break-even:** ~250 payers (founder-operated, ~$1.5K/mo tooling + ~$2K/mo contractor support, no salary), ≈ month 5–7 if gates pass.

**Cost stack, year 1:** labour $0 cash (AI-built); ~$2–4K design/store assets/legal templates; tooling ~$150–250/mo (Apple $99/yr, Google $25, Supabase Pro $25/mo, EAS Starter $19/mo, Sentry $0–26, PostHog free, RevenueCat free→1%, domain/email ~$20); SMS ≈ $0.50/payer/mo; support budget $2/payer/mo at scale; marketing $0–1K/mo months 1–3, $3–5K/mo months 4–12 contingent on gates.

---

## 8. Product blueprint

**Positioning:** "The quote-and-get-paid app for one-van trades. Talk the job, send the quote, get paid on site. Your price never goes up."

**USP:** voice-to-quote on site + same-day payment + automatic chasing + price-lock + no caps + works offline.

**Complete feature list**
- Customers (import from contacts/CSV/Joist/Invoice Simple with AI column mapping), job addresses, history
- Quotes: AI voice/text/photo → draft line items; personal price-book with margins; optional items; deposit request; acceptance link/e-signature; expiry; quote-viewed notification
- Jobs/schedule: calendar, status, before/after photos, notes, checklists, reminders
- Invoices: one-tap from quote; progress/partial; recurring (later); sales tax / VAT; branded PDF; send by SMS/email/WhatsApp link
- Payments: Stripe Connect Express onboarding; card links; Apple/Google Pay; Tap to Pay on iPhone/Android; ACH/bank; deposits; tips; auto-reconcile; payout tracking
- Auto-chase: sequences (day 1 friendly, day 7 firm, day 14 final), tone presets, pause per customer, auto-stop on payment, optional late fee
- Reports: collected, outstanding, aged receivables, tax-ready export (CSV, QuickBooks/Xero)
- Offline-first with conflict-safe sync; web portal; customer-facing quote/invoice pages
- Settings: price-lock certificate, data export, pause subscription

**MVP (day 30):** customers, quotes with AI voice draft + price-book, quote→invoice, PDF, send by link, Stripe payment links, 3-step auto-chase, offline cache, onboarding import, 14-day trial, RevenueCat paywall.

**Premium/Team (months 3–6):** Tap to Pay, deposits/acceptance, schedule, multi-user, QuickBooks/Xero export, review requests, UK CIS/VAT, AI phone answering add-on (month 9+).

**Onboarding (first quote sent in <3 minutes):** trade + country → import contacts/CSV or skip → logo/business name (AI pulls from Google Business if given) → "say your last job out loud" → first quote generated → send to yourself → connect payments (deferrable) → trial starts, no card.

**Main screens:** Today (jobs, unpaid, actions) · Quotes · Invoices · Customers · Schedule · Money (collected/outstanding/payouts) · New (voice mic FAB).

**User journey:** on-site mic → draft quote → tweak prices → send → customer accepts & pays deposit → scheduled → photos → finish → invoice auto-created → paid on site via Tap to Pay or chased automatically → "paid" push → weekly summary.

**Subscription experience:** trial countdown as "days of unlimited quoting left"; paywall at day 10 and trial end with price-lock promise; annual default; pause instead of cancel; export always available.

**Retention features:** unpaid-invoice push, "invoice viewed" push, weekly money summary, year-in-review before renewal, seasonal pause, price-book that grows with use, payment history as a ledger asset.

**Expansion:** adjacent trades (cleaning, landscaping, detailing, home inspection at higher price points); UK/AU/CA; AI phone answering; embedded financing (invoice factoring); subcontract-overflow marketplace.

---

## 9. Technical architecture

| Layer | Choice | Why |
|---|---|---|
| Mobile | Expo SDK 58 / React Native 0.88 (New Architecture), TypeScript | one codebase for iOS + Android + web portal; EAS builds/updates; strongest ecosystem for Stripe/RevenueCat/camera/speech |
| Native modules | Stripe Terminal SDK (Tap to Pay), expo-speech-recognition / Apple SpeechAnalyzer wrapper, expo-camera, expo-file-system | on-device transcription for privacy and cost; cloud fallback |
| Backend | Supabase (Postgres, Auth, Storage, Realtime, Edge Functions) | $25/mo Pro covers 100K MAU; row-level security per business; pgvector optional |
| Offline | expo-sqlite / WatermelonDB outbox; server-wins for payments, last-write-wins with audit for documents | field reliability |
| PDF | Edge Function HTML→PDF with cached templates | cross-platform fidelity |
| AI | Claude Haiku 5.5 ($0.10/$0.50 per MTok, V) for quote structuring and reminder drafting; Sonnet 5.5 for photo→line items; OpenAI gpt-4o-mini-transcribe ($0.003/min) cloud STT fallback; strict JSON schemas; price-book grounding; human approval before send | cents per quote; consent screen naming providers |
| Payments | Stripe Connect Express, Payment Links, Terminal; platform fee via `application_fee_amount` | Stripe-handled pricing → no monthly Connect fee; cards 2.9%+30¢, in-person 2.7%+5¢ (+10¢ Tap to Pay), ACH 0.8% capped $5 (V) |
| Subscriptions | RevenueCat (IAP both stores, Paywalls v2, web billing for annual from site) | 15% store rate |
| Messaging | Twilio SMS + Resend email + WhatsApp links; Expo push | chase sequences |
| Analytics | PostHog (events, funnels, replay), Sentry | free tiers |
| Auth | Supabase Auth (Apple, Google, phone OTP) | tradespeople hate passwords |
| Security/privacy | RLS per tenant; PII minimisation; Stripe holds card data; signed PDF URLs; GDPR/UK DPA export & delete | |

Tap to Pay on iPhone supported in US, UK, CA, AU, NZ with Stripe/Square/Adyen (V). Flutter 3.50 is a reasonable alternative; React Native's Stripe Terminal/RevenueCat maturity and the shared web portal tip the choice.

**Difficulty:** medium. **Time to MVP:** 3–4 weeks AI-assisted with daily device testing. **Backend complexity:** medium (multi-tenant RLS, sync, PDF, Stripe webhooks). **Platform limits:** Tap to Pay entitlement + Stripe Terminal onboarding; Android involuntary-billing handling. **Maintenance:** OS updates twice yearly, SDK bumps, tax-rule tables.

---

## 10. Risks and red-team

1. **"Trades" is not one workflow.** Cleaner's recurring invoice ≠ plumber's callout ≠ renovation estimate. *Mitigation:* beachhead = residential service-call trades where the loop is identical (callout → diagnose → quote on site → job → invoice → paid same day); cleaning/landscaping later as "recurring job" mode.
2. **Differentiation is a pricing policy plus copyable features.** Square/Wave free; Joist/Jobber ship AI. *Mitigation:* build the moat from payments relationship + data gravity, a trusted distribution channel, and demonstrated collection outcomes ("paid 9 days faster"). Price-lock is marketing, not defence; it constrains future economics.
3. **Switching is work.** One-tap import from Joist/Invoice Simple; first quote sendable within 3 minutes.
4. **CAC could kill it.** ~$143/payer via Apple Ads = 10-month payback. Only community/creator/partner channels at ≤$50 make this fundable — the single gating assumption.
5. **Mobile website would largely suffice** for quotes/invoices — native must earn its keep with offline, camera/voice capture, Tap to Pay, push for viewed/paid, home-screen presence; also ship a web portal.
6. **Does AI genuinely improve it?** Voice→draft: yes (time-to-send). Photo→binding price: dangerous (hidden damage, access, local labour rates) — AI proposes line items, the human prices them. Auto-chase: valuable, copyable.
7. **Recurring value** strong for frequent invoicers, weak for side-hustlers — qualify on ≥5 documents/month.
8. **Platform/policy:** IAP for subscription; no IAP for service payments; AI consent; UK VAT/CIS and US sales-tax presentation; Stripe Connect KYC drop-off; Android 31% involuntary churn.
9. **Market regime:** RevenueCat 2026 — median app grows 5.3%, 72% of annual subs cancel in year one, business apps take 113 days to $1K MRR. Plan accepts a slow start and front-loads validation.

**Red-team (GPT-6.1) verdict:** fund a small experiment restricted to one frequent-invoicing trade and one geography; the biggest condition is proving a repeatable channel acquiring genuinely paying customers for ≤$50. Suggested falsification gates:
- Interview 40 owner-operators in one trade, inspecting real invoices: pass if ≥20 show ≥2 hrs/week avoidable admin or ≥$500 overdue.
- Recruit 20 users at the real $19 price: pass if ≥15 send ≥5 real documents within 14 days and ≥15 still paying at day 90.
- Demonstrate ≥50% faster quote-to-send without worse correction rates; measure actual collection improvement, not reminders sent.
- Acquire 50 paying customers outside the founder's network at ≤$50 fully-loaded CAC.
- Support <15 min/account/month; contribution payback <4 months.

**Hidden opportunities the red-team surfaced:** (a) a *collections overlay* that plugs into existing invoicing tools and only does auto-chase + reconciliation (attacks the stated pain without migration) — the designated pivot; (b) B2B2C via trade suppliers or bookkeepers (test one partner for 20 activated customers); (c) payments-led model is small per user at 0.5% ($20K GMV → $100/yr) — measure adoption and fee resistance before underwriting it.

---

## 11. Execution plan

### First 30 days

| Days | Fable (research/strategy/review) | Opus (build) | Founder |
|---|---|---|---|
| 1–3 | Interview script; Joist/Invoice Simple onboarding teardown; price-book taxonomy for plumbing/electrical/HVAC/handyman | Repo, Expo shell, Supabase schema (tenants, customers, quotes, invoices, payments, chase_jobs), RLS, auth | Recruit 40 interviewees; trademark/name check; Apple/Google accounts; Stripe Connect application |
| 4–10 | Review schema for tax/VAT extensibility; ToS/privacy/AI-consent copy; define metrics (time-to-first-quote, docs/14 days, chase→paid days) | Customers, quotes, price-book, AI voice→quote (Haiku, JSON schema), PDF function, send-by-link | 20 interviews; collect anonymised real quotes/invoices as test corpus |
| 11–17 | Red-team AI quote outputs vs real corpus; paywall copy & pricing test plan | Invoices, quote→invoice, Stripe payment links + webhooks, auto-chase (Twilio/Resend), offline outbox | Finish interviews; **gate A decision**; recruit 20 paying pilots |
| 18–24 | Independent code review (security/RLS/webhook idempotency); onboarding usability review | Onboarding + import, RevenueCat trial/paywall, PostHog, Sentry, TestFlight/Play internal | Onboard pilots by phone; daily feedback |
| 25–30 | Pilot readout vs gate B indicators; ASO keyword set; creator shortlist (15) | Bug-fix, polish, store listings, screenshots/video, submit | Store submissions; line up 3 micro-creators |

Deliverable: app in review on both stores, 20 paying pilots using it daily, gate A result, decision memo.

### Financial roadmap

| Horizon | Spend | Milestones / gates |
|---|---|---|
| 30 days | ≤$1.5K | MVP in TestFlight/Play internal; 40 interviews; **gate A** passed; 20 paying pilots |
| 90 days | ≤$5K cum. | Public launch; **gate B** (≥15/20 pilots active and paying at day 90; ≥50% faster quoting); ≥50 payers; **gate C** (50 acquired outside network at ≤$50 CAC) |
| 6 months | ≤$20K cum. | 250–400 payers (≈ break-even); payments adoption ≥40%; churn ≤5%; ≥3 creators at positive ROAS; UK beta |
| 12 months | ≤$60K cum. | 1,000–2,000 payers ($15–30K subscription MRR + $5–15K payments, moderate case); Team tier; QuickBooks/Xero; AI phone answering beta; UK live; raise-or-bootstrap decision |

If gate A or B fails: pivot to the collections overlay, or to a higher-WTP niche trade (home inspection reports; incumbents ~$109/mo).

### 12-month roadmap

| Month | Product | Growth | Finance/ops |
|---|---|---|---|
| 1 | MVP, pilots | interviews, groups | gate A |
| 2 | Public launch; chase v2; acceptance & deposits | first 3 creators; ASO; referral | first 50 payers |
| 3 | Tap to Pay; schedule | gate C channel test | gate B readout |
| 4 | Team tier; QuickBooks/Xero export | 10+ creators; supplier partner pilot | 150–250 payers |
| 5–6 | UK beta (VAT/CIS, GBP, Tap to Pay UK); review requests | UK creators; per-trade web-to-app | ~break-even (250–400) |
| 7–8 | Recurring jobs mode; AI job-photo line items | adjacent-trade communities | 500–800 payers |
| 9–10 | AI phone answering beta; price-book sharing | paid UA test with proven creatives | payments ≥40% attach |
| 11–12 | AU/CA; integrations marketplace v1 | partnerships at scale; case studies | 1,000–2,000 payers; decision point |

Validation targets: day-14 activation (≥5 docs) ≥60% of trials; trial→paid ≥35%; monthly logo churn ≤5%; payments attach ≥40%; blended CAC payback ≤6 months; support ≤15 min/account/month.

### AI workflow (Opus + Fable)
- **Fable:** evidence base and gates; interview guides and synthesis; competitor watch (Joist/Jobber AI, price changes); weekly cohort/retention analysis; paywall/onboarding experiments; adversarial review of every Opus release (security, RLS, webhook idempotency, data-loss, AI hallucination on the real quote corpus) and of founder decisions.
- **Opus:** codebase — schema, RLS, sync, PDF, Stripe/RevenueCat, UI, tests (unit + device E2E), performance, EAS releases, crash triage.
- **Mutual challenge:** every spec implemented with an explicit "assumptions I made" list Fable must accept/reject; every PR reviewed by Fable *and* a second model family; metrics reproduced from raw events; weekly kill-criteria review where each model argues the opposite side.
- **Verification layer:** CI typecheck/unit/E2E, Stripe test-mode webhook replay, RevenueCat sandbox purchases, golden corpus of 100 anonymised quotes scored on every prompt/model change, store-review checklists (3.1.1, 3.1.3(e), 5.1.2(i)).

---

## 12. Sources

- Invoice Simple App Store listing: https://apps.apple.com/us/app/invoice-maker-invoice-simple/id694831622 (V)
- Joist pricing https://joist.com/pricing (V); Joist AI estimates support article 16760523 at support.joistapp.com (V); Joist reviews https://apps.apple.com/us/app/joist-estimate-invoice-maker/id592163563?see-all=reviews (V)
- Jobber pricing https://www.getjobber.com/pricing/ (blocked; 3P readings https://servicepropicks.com/guides/jobber-core-vs-connect-vs-grow/, https://realcostlabs.com/jobber-pricing/); Jobber Series D https://techcrunch.com/2023/02/07/jobber-fixes-on-100m-as-its-platform-for-home-services-pros-hits-200k-users/ (V); ARR podcast https://www.pmf.show/blog/jobber-forrest-zeisler-100m-arr-startup-growth (U); Contrary Research https://research.contrary.com/company/jobber (3P)
- Housecall Pro pricing https://www.housecallpro.com/pricing (V); NewView Capital https://nvc.vc (V)
- ServiceTitan FY2026 results https://investors.servicetitan.com/news-releases/news-release-details/servicetitan-announces-fiscal-fourth-quarter-and-full-fiscal (V); 10-K https://www.sec.gov/Archives/edgar/data/1638826/000163882626000028/ttan-20260131.htm (V)
- Square Invoices https://squareup.com/us/en/invoices/pricing; Wave https://www.waveapps.com/pricing; Zoho Invoice https://www.zoho.com/us/invoice/pricing; Tradify https://www.tradifyhq.com/pricing; ServiceM8 https://www.servicem8.com/us/pricing; Invoice2go https://invoice.2go.com/pricing; Billdu https://www.billdu.com/pricing; Bookipi https://bookipi.com/pricing; QuoteIQ https://myquoteiq.com; Handoff https://handoff.ai; BuildWell https://buildwellapp.com (all V vendor pages)
- Review mining: https://settlejob.com/guides/invoice-app-complaints-app-store-reviews/ ; https://settlejob.com/guides/invoice-app-price-history ; https://opportunitymarket.org/apps/invoice-maker-invoice-simple ; https://getwedge.dev/examples/tradesperson-invoicing/ (3P)
- Forums: https://electriciansforums.net/threads/what-invoicing-apps-softwares-do-you-guys-use.212033/ ; https://www.diynot.com/diy/threads/quoting-on-site-what-do-you-actually-use.660164/ ; https://www.contractortalk.com/threads/joist-app.418029/page-3 (3P/U snippets)
- Market size: CPWR https://www.cpwr.com/research/data-center/the-construction-chart-book/interactive-7th/industry-businesses/nonemployer/ (V); Census NES https://www.census.gov/data/developers/data-sets/nonemp-api.2023.html (V); ONS via Construction News (V); ABS via bookkeepingpros.com.au (3P); MarketsandMarkets FSM press release (V as published)
- Distribution: vidIQ channel stats (3P); SponsorRadar on Tradify (3P); Jobber podcast https://www.getjobber.com/podcast/ep7-paul-jamison-christine-hodge/ (V); SaaSquatch case study https://www.saasquatch.com/blog/how-jobber-strengthens-community-and-increases-ltv-with-saasquatch/ (vendor); PHCP Pros on Plumbing Hacks (3P); AppTweak Apple Ads benchmarks https://www.apptweak.com/en/aso-blog/apple-ads-benchmarks (3P)
- Bloomberg on Bending Spoons price hikes https://www.bloomberg.com/news/articles/2026-08-13/bending-spoons-customers-decry-outrageous-app-price-hikes (V)
- Apple App Review Guidelines https://developer.apple.com/app-store/review/guidelines/ (V); 5.1.2(i) https://developer.apple.com/news/?id=ey6d8onl (V); Small Business Program https://developer.apple.com/app-store/small-business-program/ (V); Tap to Pay regions https://developer.apple.com/tap-to-pay/regions (V)
- Stripe https://stripe.com/pricing and https://stripe.com/connect/pricing (V); Supabase https://supabase.com/pricing (V); RevenueCat https://www.revenuecat.com/pricing/ (V); Expo https://expo.dev/pricing and https://expo.dev/changelog/sdk-58 (V); Anthropic pricing https://platform.claude.com/docs/en/about-claude/pricing (V); OpenAI pricing https://developers.openai.com/api/docs/pricing (V)
- RevenueCat SOSA 2026 https://www.revenuecat.com/blog/growth/subscription-app-trends-benchmarks-2026 (V); SaaStr summary https://www.saastr.com/the-top-10-learnings-from-revenuecats-state-of-subscription-apps-how-115000-mobile-apps-deliver-16b-in-revenue-whats-working-whats-quietly-killing-growth/ (3P)

**Not verified:** Jobber and Housecall Pro actual ARR; Invoice Simple / Invoice Fly / Bookipi / Saldo revenue; any Reddit thread directly (403); Apple's own keyword popularity scores; landscaping/cleaning solo-business counts; absence of any competitor offering auto-chase as a core feature (not exhaustively searched).
