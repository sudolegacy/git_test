# Mobile App Opportunity Research — November 2026

**Prepared for:** Usfar (wq)
**Research window:** 12 November 2026 (all web sources accessed on this date)
**Method:** six parallel research streams (market benchmarks, consumer, AI, SMB/vertical, niche/emerging, growth/CAC), three deep-dive verification streams on the finalists, an independent red-team review by a different model family (GPT-6.1), and a scenario financial model built from the stated assumptions.

**Evidence labels used throughout**
- **V** = verified from a primary source (vendor page, regulator, company statement, SEC filing, or named major-outlet reporting)
- **3P** = third-party estimate (app-intelligence sites, competitor blogs, aggregators) — order-of-magnitude only
- **U** = unverified (founder self-reports, podcast claims, anonymous posts)
- **Calc** = my own calculation from stated assumptions — never a forecast

Reddit returned HTTP 403 to every direct fetch during this research; Reddit evidence below is relayed through third parties and labelled accordingly. Several App Store listings, pricing pages and app-intelligence dashboards were fetched directly and are labelled V.

---

## 1. Executive summary

**Recommendation: build a mobile-first "quote-to-cash" app for solo and micro (1–3 person) residential service tradespeople — plumbers, electricians, HVAC, handymen — starting in the US with a UK fast-follow.** Working name candidates: *Jobsheet*, *Quoted*, *Paidly*, *SiteSlip*.

The core loop is: arrive on site → describe the job by voice or photos → AI drafts a priced quote the tradesperson approves → customer accepts and pays a deposit by link or Tap to Pay → job done → quote becomes invoice in one tap → automatic, polite payment-chasing until paid. Pricing: **$19/month or $149/year**, 14-day full trial, written price-lock for as long as the customer stays subscribed, no document caps, true offline mode. Second revenue line: a small platform fee on card payments processed through the app (exempt from Apple/Google commission because it pays for physical services, Apple guideline 3.1.3(e), V).

**Why this wins over 19 alternatives**

1. **Demand is proven at every price point.** Generic mobile invoicing apps have enormous paying bases (Invoice Simple 4.9★/123K US ratings, Invoice Fly 4.8★/111K, Invoice2go 4.8★/56K — all V from App Store pages). Trade-specific platforms show the ceiling: Jobber 100K+ customers and 400K+ daily users (V, May 2026 press), ServiceTitan FY2026 revenue $961M, +24% (V, SEC 10-K).
2. **The addressable base is large and self-employed.** 2.9M US construction businesses with no employees, 1.9M of them specialty-trade contractors (Census NES via NAHB, 3P citing V data); 756K self-employed in UK construction (ONS via Construction News, V); 279K non-employing construction businesses in Australia (ABS, 3P).
3. **Incumbents are actively creating switchers.** Invoice Simple doubled its Plus plan to $14.99 in Oct 2026 and caps Essentials at 3 invoices/month (V/3P); Joist removed its free tier and caps Basics at 5 documents/month, then raised the price twice (V); Housecall Pro Basic went from $49 to $79 (3P); Bending Spoons' acquisitions (MileIQ, Harvest) triggered "outrageous" price-hike coverage (Bloomberg, Aug 2026). Review-mining of 842 US App Store reviews across invoicing apps found price and caps as the dominant 1–2★ themes (3P).
4. **Business users pay monthly and stay.** RevenueCat's 2026 dataset shows business apps take longest to reach $1K MRR (113 days median) but the segment pays $20–100+/month when the tool touches revenue (V/3P). Net LTV per payer in my moderate scenario is ~$564 vs $46–62 for the consumer finalists (Calc).
5. **AI-assisted development is a genuine edge here, not a gimmick.** The product surface (quotes, invoices, customers, scheduling, payments, reminders, PDF, offline sync, two platforms, web portal) is exactly the kind of broad-but-well-understood build that previously needed a 10–20 person team. Unlimited Opus capacity collapses that. In-product AI (voice→quote, photo→line items, reminder drafting) is useful but copyable; the durable advantages are workflow fit, payments, price-lock trust and distribution.

**Runner-up:** a GLP-1 medication companion (oral-pill era, international). Faster to build, strong organic community acquisition (Shotsy: founder claims 1M downloads, 100K+ paying subscribers, zero ad spend — U), but consumer ARPPU is ~3× lower, free competitors are now subsidised by Noom, MyFitnessPal and Novo Nordisk (V), and it carries medical-device declaration and accuracy-claim risk. It is the right **second** app for this operation, not the first.

**Honest framing of the risk:** the red-team's verdict, which I accept, is that "price-lock + no caps + AI quote + auto-chase" is a *credible offer for testing demand, not a moat*. The business is investable only once a repeatable channel delivers paying customers at ≤$50 fully-loaded CAC. The 30-day and 12-month plans below are built around proving exactly that before spending on scale.

---

## 2. Overview of the mobile app market (2025–2026)

### Size and direction
- Global in-app purchase spend reached **$167B in 2025, +10% YoY**; non-game apps grew **21%** and surpassed games for the first time (Sensor Tower State of Mobile 2026, V). Consumers spent 5.3 trillion hours in apps.
- US spend ≈ $59B (eMarketer citing Sensor Tower, 3P). Health & Fitness ≈ $6B, +17% (Business of Apps, 3P).
- Generative-AI apps: >$5B IAP in 2025 (Sensor Tower via Daily Sabah, 3P); AI app downloads +148% (V). ChatGPT was the #3 grossing app of 2025 (V) and ~$301M/month on mobile by April 2026 (Appfigures, 3P).

### Subscription economics (RevenueCat State of Subscription Apps 2026: 115K+ apps, $16B+ revenue, V unless noted)
| Metric | Value |
|---|---|
| Median download→paid (day 35) | 2.0% overall; **10.7% hard paywall vs 2.1% freemium**; top-decile hard paywall 38.7% |
| Day-60 revenue per install | $3.09 hard paywall vs $0.38 freemium |
| Trial→paid | 42.5% for 17–32-day trials vs 25.5% for <4-day trials |
| Day-0 cancellations | 55% of 3-day-trial cancellations happen on day 0 |
| Year-1 retention (2025 edition) | annual 28.4%, monthly 8.6%, weekly 1.6% (3P summary of V report) |
| Annual plan year-1 cancellation (2026) | ~72% (up from ~56%) |
| AI apps | +41% year-1 LTV per payer ($30.16 vs $21.37) but monthly plans retain 36% worse |
| Typical prices | $4.99–6.99/wk, $7.99–9.99/mo, $29.99–39.99/yr; median annual $34.80 |
| High- vs low-priced apps, year-1 LTV/payer | $62.19 vs $10.69 (6×) |
| New-app outcomes | 17.3% reach $1K MRR, 4.6% reach $10K MRR within 2 years; top 10% grew 306% YoY vs 5.3% median |
| Time to $1K MRR | 32 days gaming vs **113 days business apps** |
| Google Play involuntary churn | 31% of cancellations are billing failures vs 14% on iOS |
| Web billing | 3.2% of revenue globally, 4.9% NA; 41% of top-tier apps use it vs 1.3% of bottom tier |

Implication: the market is barbell-shaped — new launches are at a record (~14,700/month) and the median app barely grows, while the top decile compounds. Winning requires (a) a segment that pays above the $30–40 annual median, (b) a hard or near-hard paywall, and (c) a distribution channel the founder controls.

### Store economics (V)
- Apple Small Business Program: **15%** on proceeds ≤ $1M/yr; 30% standard. US link-out commission still unresolved after Ninth Circuit (Dec 2025); Apple proposed 5–15% in Aug 2026. EU from Oct 2026: IAP 15–26%, alt-payments 10–20%.
- Google Play: 15% on first $1M; Epic settlement (Mar 2026) brings subscriptions to 10% + possible 5% billing fee in US/EEA/UK by mid-2026.
- RevenueCat: free to $2.5K MTR then 1%. Supabase Pro $25/mo. Expo EAS from $19/mo. Apple dev $99/yr, Google $25 once.

### Acquisition costs (3P unless noted)
- Apple Ads US median 2025 CPI: Business **$6.86**, Finance $9.65, Health & Fitness $3.77, Productivity $3.58, Education $2.91, Utilities $2.25 (AppTweak, ~2,800 advertisers).
- Meta CPI $2.00–5.50, TikTok $1.75–4.00, Google $1.50–4.50 (Airbridge/Udonis). Cost per trial $20–40 for "healthy" subscription apps.
- Creator "clipping" campaigns: $0.20–6 per 1,000 views (vendor claims, U). Cal AI ran ~250 creators on retainers at mid-six-figures/month (U, founder).
- Organic search still drives most non-game installs (Sensor Tower 2020: 70% of non-game installs from search, V but dated).

---

## 3. The 20 highest-potential app opportunities (scored /100)

Scoring: demand 20 · revenue potential 20 · competition & differentiation 15 · acquisition 15 · retention 10 · feasibility 10 · profitability & scalability 10.

| # | Opportunity | Demand | Rev | Comp | Acq | Ret | Feas | Prof | **Total** |
|---|---|---|---|---|---|---|---|---|---|
| 1 | Solo-trades quote-to-cash (AI voice quote, payments, auto-chase) | 17 | 17 | 9 | 10 | 9 | 7 | 9 | **78** |
| 2 | GLP-1 medication companion (oral-pill era, international) | 17 | 13 | 9 | 13 | 7 | 8 | 8 | **75** |
| 3 | Short-video recipe import + weekly meal planner | 16 | 12 | 8 | 14 | 6 | 8 | 7 | **71** |
| 4 | Co-parenting ledger with one-parent mode | 15 | 14 | 10 | 8 | 9 | 6 | 8 | **70** |
| 5 | Self-employed mileage + receipts + tax set-aside bundle | 15 | 12 | 7 | 9 | 8 | 7 | 8 | **66** |
| 6 | Honest AI calorie tracker for a defined niche | 17 | 13 | 6 | 11 | 5 | 7 | 6 | **65** |
| 7 | Phone-first AI voice notes for field workers (Plaud without hardware) | 13 | 12 | 9 | 9 | 7 | 8 | 6 | **64** |
| 8 | Niche-trade reporting (home inspection / detailing, AI photo→report) | 12 | 14 | 10 | 7 | 9 | 6 | 7 | **65** |
| 9 | Focus / screen-time blocker, Android-first | 14 | 12 | 8 | 10 | 6 | 5 | 7 | **62** |
| 10 | Family organiser with AI school-email→calendar | 14 | 10 | 7 | 9 | 8 | 8 | 6 | **62** |
| 11 | Solo private-pay therapist practice tool | 12 | 14 | 9 | 7 | 9 | 4 | 6 | **61** |
| 12 | Subscription tracker without bank linking | 12 | 8 | 8 | 10 | 6 | 9 | 6 | **59** |
| 13 | Honest storage / photo cleaner (one-time price) | 15 | 11 | 5 | 6 | 4 | 9 | 7 | **57** |
| 14 | Trip & group expense splitting (Splitwise alternative) | 14 | 7 | 7 | 13 | 5 | 8 | 5 | **59** |
| 15 | AI speaking tutor for under-served language pairs | 14 | 12 | 6 | 9 | 6 | 6 | 4 | **57** |
| 16 | TCG collector show-floor tool (offline, trade calculator) | 11 | 9 | 8 | 10 | 6 | 8 | 6 | **58** |
| 17 | Crochet / knitting pattern & row-counter | 10 | 7 | 9 | 10 | 7 | 9 | 7 | **59** |
| 18 | Niche reading tracker (romance / audiobook / book-club) | 11 | 8 | 7 | 11 | 6 | 9 | 6 | **58** |
| 19 | Non-plant identifier (coins / rocks / bugs) | 11 | 9 | 8 | 8 | 4 | 7 | 6 | **53** |
| 20 | Independent running/cycling training plans (post-Runna) | 11 | 8 | 6 | 9 | 6 | 7 | 5 | **52** |

### Score rationale and one-liners

**1. Solo-trades quote-to-cash** — Demand 17: huge paying base at every tier (see §1); Rev 17: $19–39/mo B2B pricing plus payments; Comp 9: crowded, free alternatives (Square/Wave/Zoho) and incumbents shipping AI (Joist AI estimates Aug 2026, Jobber Teammate Sept 2026, V) — but no incumbent combines price-lock, no caps, offline and auto-chase for solos; Acq 10: ASO is hard ("invoice" difficulty 59–77/100, 3P) but trade creators and Facebook groups are proven (Tradify sponsors 106 YouTube deals, 3P); Ret 9: business data lock-in; Feas 7: payments, PDF, offline sync; Prof 9: ~85% gross margin, near-zero marginal AI cost. Biggest risk: "generic invoicing" is a graveyard; must stay vertical.

**2. GLP-1 companion** — Demand 17: 12% of US adults currently on a GLP-1 (KFF Nov 2025, V), 11% for weight loss (Gallup Jul 2026, V); Shotsy 4.8★/35K; Rev 13: $40–60/yr; Comp 9: Shotsy, MeAgain (4.8★/40K) plus free Noom, MFP, Novocare (V); Acq 13: community-driven (r/Zepbound 243K etc.), shareable charts; Ret 7: stops when medication stops; Feas 8; Prof 8. Biggest risk: free subsidised competitors and regulatory drift.

**3. Short-video recipe import + meal planner** — Demand 16: ReciMe #1 grossing Food & Drink (4.8★/333K, est. $480K/mo 3P); 4 of top-10 grossing Food & Drink on 27 Oct 2026 were planners <5 months old (3P); Mealime shut down 21 Oct 2026 (V, mealime.com), Paprika 4 moved to subscription (V); Rev 12: $30–40/yr; Comp 8: Paprika now sells video import at $14.99/yr — brutal price anchor; Acq 14: the most TikTok-native category in this list; Ret 6; Feas 8; Prof 7. Biggest risk: platform ToS and clone saturation.

**4. Co-parenting ledger** — Demand 15: OurFamilyWizard $110–300/yr *per parent* (V), 4.6★/57K; TalkingParents and AppClose both ended free plans in 2026 (3P); 9,598 reviews mined — pricing 1,200+ mentions, failed notifications 450+ (3P); Rev 14; Comp 10: court-recommended incumbents are sticky but hated; Acq 8: family-lawyer referrals are slow; Ret 9: multi-year; Feas 6: admissibility, tamper-evidence; Prof 8. Biggest risk: courts favour incumbents.

**5. Mileage + receipts + tax set-aside** — MileIQ went from ~$60/yr (2023) to $139.92/yr (V pricing page; history 3P), Play rating fell to 2.8★ "recent" (3P); but Stride and TripLog offer free unlimited auto-tracking (V) and Everlance/Hurdlr/Solo overlap the bundle. Differentiation is thin.

**6. Honest AI calorie tracker** — Cal AI: 15M+ downloads, $30M+ revenue, 7 staff, acquired by MyFitnessPal (TechCrunch Mar 2026, V); but growth was bought with ~250 creators (U), billing complaints dominate reviews (3P), Apple pulled it for a week in Apr 2026 (V). A niche (GLP-1 protein, diabetic, South-Asian cuisine) could work; generic is owned.

**7. Phone-first voice notes for field workers** — Plaud ~$250M annualised (Forbes, V as reported), Otter $100M ARR (V), voice-recorder category +2,270% in 2024 (Appfigures, 3P); Apple Notes is free. Angle: structured outputs per trade (site notes → job sheet). Overlaps #1 and is folded into it.

**8. Niche-trade reporting** — Spectora $109/mo for home inspectors (V), Urable $70–110/mo for detailers (V). Highest WTP in the list but tiny markets; strong second vertical once #1 exists.

**9. Focus blocker Android-first** — Opal $10M+ ARR (founder, U), 4.7★/91K; Android parity complaints real; but Android 17 Advanced Protection blocks Accessibility-based blockers (V/press) and Play policy restricts them. Platform risk too high.

**10. Family organiser with AI import** — Cozi 4.8★/403K (V) already sells AI Event Import at $79/yr (V). Space is not empty.

**11. Solo therapist tool** — SimplePractice $49–99/mo and metering claims from Oct 2026 (3P); HIPAA/BAA burden; crowded with cheap entrants.

**12–20.** Smaller or structurally capped: subscription trackers (Rocket Money distrust is real — BBB 1.84/5 — but indie incumbents and low ARPU), cleaners ($197M category, Appfigures 3P, but won by Apple Ads spend), expense splitting (viral but monetises poorly), language tutors (voice inference cost $2.58–18/DAU/month, 3P), hobby verticals (real but ≤$1M/mo categories), identifiers (plants 78% of $27M/mo category; coins 13%), running plans (Strava bought Runna, V).

---

## 4. Competitor analysis — finalists

### 4.1 Trades invoicing / field service (all prices USD, Nov 2026)

| Product | Owner | Free tier / caps | Price | US App Store | Play | Notes |
|---|---|---|---|---|---|---|
| Invoice Simple | EverCommerce (bought 2020, ~$32.5M, 3P citing SEC) | 14-day trial | Essentials $6.99 (3 inv/mo), Plus $14.99 (10), Premium $21.99 (unlimited) (V/3P) | 4.9 / 123K (V) | 10M+ (U) | Plus doubled from $7.49 Oct 2026 (3P); 58% of 1–3★ cite price hikes (3P) |
| Invoice Fly | independent | — | tiered, caps | 4.8 / 111K (V) | 4M+ claimed (V) | "only lets me make 10 invoices a month" (review, 3P) |
| Joist | EverCommerce | Basics capped 5 docs/mo | $10 / $17 / $32 / $100 (V) | 4.7 / 14.5K (V) | 1M+ | AI text/voice estimates rolling out Aug 2026 (V); "just to send 5 invoices a month you have to pay" (review, V) |
| Jobber | VC ($237M raised, 3P); $100M+ ARR (founder podcast, U) | 14-day trial | Core $29 annual / $49 monthly; Connect $99–299; Grow $149–399; +$29/user; cards 2.9%+30¢ (V/3P) | 4.8 / ~22K (V) | 1M+ | 100K+ customers, 400K daily users (V); Teammate AI beta Sept 2026 (V); AI receptionist $29 add-on (3P) |
| Housecall Pro | VC (~$1.1B 2022, 3P) | — | Basic $59 annual / $79 monthly (V) | 4.7 / 32K (V) | 500K+ | Basic was $49 in 2022 (3P); complaints mostly bugs/support |
| ServiceTitan | public | — | enterprise | — | — | FY26 revenue $961M +24% (V); FY27 guide $1.139–1.144B (V) |
| Square Invoices | Block | **Free, unlimited** | Plus $49; cards 3.3%+30¢ on free (V) | — | — | Complaints: held funds |
| Wave / Zoho Invoice | H&R Block / Zoho | Free unlimited / 500 per yr (V) | Wave Pro $19 | — | — | Desktop-first |
| Tradify / ServiceM8 | independent (NZ/AU) | ServiceM8 30 jobs/mo free | $47–61/user; $29–349 (V) | 4.8 / 179 US; 4.6 / 867 US (V) | 100K+ / 50K+ | Tiny in US; Tradify sponsors 106 YouTube deals (3P) |
| SimplyWise Cost Estimator | independent | — | $29.99/mo or $239.99/yr (V) | 4.8 / 41.6K (V) | — | Photo→estimate; largest AI-estimating base found |
| QuoteIQ / Handoff / BuildWell | independent | — | $29.99/mo; $119/mo; $79.99/yr (V) | 4.7/3.4K; 4.8/1.9K; — | — | QuoteIQ built by two contractor-YouTubers with ~1M subs (PR, U) |

**Verbatim pain (sources: App Store review pages V, forums via snippets 3P/U):**
- "Just to send 5 invoices a month you have to pay $8 per month." — Joist review, 2024
- "I can't justify paying for it to only be able to have 5 sales per month." — Joist review, Oct 2026
- "they put way too many pop-up boxes telling you about new features or trying to get you to use their AI." — Joist review
- "Now it only lets me make 10 invoices a month or I have to upgrade for another 300$ to the unlimited." — Invoice Fly review (3P)
- "Was billing a client yesterday and realized I'm paying Invoice2go $25/month just to send PDFs." — r/smallbusiness (U, relayed)
- "It drives me up the wall when customers take forever to pay and come out with excuses." — ElectriciansForums, 2024 (wants to be notified when invoice is viewed)
- "some are too expensive at £34 a month … jobber and servicem8 are the big ones (overkill if you're a side hustle)." — DIYnot, Aug 2026
- "Invoice simple what I use quick and easy… invoice them from your phone before you leave the drive." — PlasterersForum (positive signal for speed)

**Ownership pattern:** the simple apps are PE roll-ups (EverCommerce, Bill.com, team.blue, Bending Spoons) that monetise by raising prices and adding caps; the trade platforms are VC-funded and moving up-market with AI agents. The solo operator is squeezed between the two — that is the gap.

### 4.2 GLP-1 companions
| App | Price | Rating | Notes |
|---|---|---|---|
| Shotsy | $9.99–14.99/mo, $39.99–59.99/yr (V, listing) | 4.8 / ~35K iOS; 4.7 / 13.2K Play (V) | $2M seed (BI, V); founder claims 1M downloads, 100K+ paying, 350K MAU, zero ad spend, 2/3 users from community groups (U) |
| MeAgain | $14.99–119.99 IAPs | 4.8 / 40K (3P) | claims 372K registered (3P) |
| Glowise / Pep AI / GlucoPal | $5.99–69.99 | 4.7–4.8 / 3–7K (3P) | long tail |
| Noom GLP-1 Companion | **free** (Jun 2026, V) | — | dose/side-effect/protein/muscle workouts |
| MyFitnessPal GLP-1 Support | **free** (Apr 2026, V) | — | dose, site, reminders |
| Novocare (Novo Nordisk) | **free** (V) | 4.2 / 10 | pill + injection tracking, coaches |

### 4.3 Recipe / meal planning
ReciMe (4.8★/333K; 5 free imports/wk; Plus $29.99–59.99; #1 grossing Food & Drink; est. $480K/mo 3P), Paprika 4 (4.9★/54K; Premium $14.99/yr incl. TikTok/IG/YouTube import, V), AnyList (4.9★/81K), Plan to Eat ($49/yr, V), Samsung Food (free; Food+ $59.99/yr 3P), Crouton ($24.99 one-time + $14.99/yr AI import), new entrants TapCook ($9.99/mo or $29.99/yr), NeatEat ($7.99/wk), Potto (~$9.99/wk) — all with weekly pricing and billing complaints (31% price, 28% billing/trial, 23% paywall, 20% AI-generated recipes among 143 1–2★ reviews, 3P).

### 4.4 Co-parenting
OurFamilyWizard ($110–299.88/yr per parent, V; 4.6★/57K; owns Cozi; ~$11M revenue 3P), TalkingParents ($7–32/mo per account; free plan ended Mar 2026 3P; "$10M ARR" U), AppClose ($7.99–8.99/mo; free ended Jan 2026 3P; 4.7★/40K), 2houses ($169.99/yr/family), Custody X Change (from $6/mo). Written-review 1–2★ shares: OFW ~58%, TalkingParents ~59%, AppClose ~44% (Civly analysis of 9,598 reviews, 3P).

### 4.5 Mileage
MileIQ $139.92/yr or $13.99/mo, 40 free drives (V), 4.8★/116K iOS but 2.8★ recent on Play (3P); Everlance $89.99–119.99/yr (V); Hurdlr ~$100/yr (3P); Stride free (V); TripLog free unlimited auto-tracking for individuals (V); Driversnote $11/mo (V); Solo $96–180/yr (V).

---

## 5. Monetisation comparison

| Model | Best fit among finalists | Benchmarks | Verdict |
|---|---|---|---|
| Monthly + annual subscription, trial | Trades (B2B), co-parenting | B2B tools $20–100+/mo; 17–32-day trials convert 42.5% | **Primary for the winner** — recurring value is real (every job) |
| Annual-heavy consumer subscription | GLP-1, recipes | median annual $34.80; 72% year-1 cancellation | Works but LTV ~$50–80 |
| Weekly subscription | AI photo/cleaner apps | $4.99–9.99/wk; 1.6% year-1 retention; drives billing complaints and Apple enforcement (Cal AI pulled Apr 2026) | Avoid — reputational and policy risk |
| One-time / lifetime | Recipe managers, hobby tools, cleaners | strong demand signal (Paprika backlash, Fantastical backlash) | Good as an *option* alongside subscription (RevenueCat expects more lifetime plans); not a standalone business |
| Usage credits | AI generation apps | — | Only where marginal AI cost is material; not needed for the winner (voice/photo quoting costs cents) |
| Payments take-rate | Trades | Jobber/Housecall charge 2.9%+30¢ and earn on volume; Stripe Connect allows platform fees (V) | **Secondary for the winner** — outside app-store commission; scales with customer GMV |
| Advertising | Expense splitting, companions | Talkie/Xingye ~60% ad revenue (V) | Not for B2B |
| Web billing | All | 3.2% of revenue; 41% of top-tier apps use it; RevenueCat test: web ≈ 6% worse take-home at 30% fee, worse at 15% | Offer web checkout for annual plans from the marketing site; don't rely on it |

**Winner's monetisation design**
- *Free:* 14-day full trial, no card required to start (removes day-0 friction; B2B trial starts 85% on day 0 per RevenueCat 2025).
- *Paid:* Solo $19/mo or $149/yr (1 user, unlimited everything, payments, auto-chase, offline). Team $39/mo or $349/yr (up to 3 users, shared schedule). Price-lock: your sign-up price never rises while you remain subscribed.
- *Renewal levers:* annual default with "2 months free"; renewal reminders 7 days before (Apple requires for price changes anyway); in-app "year in review" (invoices sent, hours saved, money collected) 30 days before renewal.
- *Cancellation reduction:* exit survey with pause option (1–3 months at $0 — tradespeople have seasonal lulls); data export always available (removes fear of lock-in, paradoxically increases trust); Google Play grace periods and retry to combat 31% involuntary churn.
- *LTV levers:* payments adoption (+$5–15/mo/payer at 0.5% on $1–3K/mo GMV), Team tier upgrade, add-ons later (AI phone answering is $29–79/mo at competitors; supplier price-books; bookkeeping export).

---

## 6. Financial models

All numbers are **Calc** from the assumptions shown. Infra per MAU assumes Supabase/Expo/RevenueCat/Sentry/PostHog scaling; AI cost per payer assumes ~40 voice quotes/month at Haiku-class pricing plus transcription (~$1.20/payer/month for trades; $0.35–0.45 for consumer apps). Store fee 15%. "Net" excludes marketing and salaries.

### 6.1 Winner — solo-trades quote-to-cash ($19.99/mo, $149/yr, 45% annual → blended $16.58 gross, $14.09 net)

| Scenario | % MAU paying | Monthly churn | Payments take & GMV/payer/mo | Lifetime | Net LTV/payer |
|---|---|---|---|---|---|
| Conservative | 6% | 6.0% | 0.3% on $1,500 | 17 mo | $290 |
| Moderate | 10% | 4.5% | 0.5% on $2,500 | 22 mo | $564 |
| Optimistic | 15% | 3.5% | 0.75% on $4,000 | 29 mo | $1,226 |

Moderate scenario (payers = 10% of MAU; "net" before marketing):

| MAU | Payers | Subscription MRR | Payments rev | Gross profit | Infra | Net before marketing |
|---|---|---|---|---|---|---|
| 1,000 | 100 | $1,658 | $1,250 | $2,539 | $420 | $2,119 |
| 5,000 | 500 | $8,291 | $6,250 | $12,697 | $500 | $12,197 |
| 10,000 | 1,000 | $16,582 | $12,500 | $25,395 | $600 | $24,795 |
| 50,000 | 5,000 | $82,910 | $62,500 | $126,974 | $1,400 | $125,574 |
| 100,000 | 10,000 | $165,820 | $125,000 | $253,947 | $2,400 | $251,547 |
| 500,000 | 50,000 | $829,100 | $625,000 | $1,269,735 | $10,400 | $1,259,335 |

Conservative net before marketing: $624 / $4,718 / $9,837 / $50,784 / $101,968 / $511,441 at the same MAU steps. Optimistic: $6,014 / $31,671 / $63,742 / $320,310 / $641,020 / $3,206,702.

Note on MAU: for a B2B tool "MAU" ≈ trial + paying accounts, so payer share is far higher than consumer apps. 10K MAU here means ~1,000 paying tradespeople — roughly 0.03% of the US nonemployer construction base.

Price sensitivity at 10K MAU / 1,000 payers (net of store): $9.99/$79 → $7,188; $14.99/$119 → $10,801; **$19.99/$149 → $14,095**; $29.99/$249 → $21,957; $39.99/$349 → $29,820. RevenueCat's data (higher-priced apps 6× LTV, ~2× trial conversion) argues against going below $19.

CAC: at Apple Ads Business CPI $6.86, 12% install→trial, 40% trial→paid → **~$143 per payer, ~10-month payback** on subscription alone (6 months with payments revenue). At a creator/community blended CPI of $3 → **~$62, ~4-month payback**. The red-team's gate — ≤$50 fully loaded — therefore requires community/creator/partner channels, not Apple Ads, in year one.

Break-even (founder-operated, $1.5K/mo tooling + $2K/mo contractor support, no salary): ~250 payers in the moderate case (~month 5–7 if the 30/90-day gates pass).

### 6.2 Runner-up — GLP-1 companion ($9.99/mo, $49.99/yr, 65% annual → $6.20 gross, $5.27 net)

| Scenario | % paying | Churn | LTV/payer | Net @10K MAU | Net @100K MAU | Net @500K MAU |
|---|---|---|---|---|---|---|
| Conservative | 3% | 10% | $49 | $1,077 | $13,471 | $68,555 |
| Moderate | 6% | 8% | $62 | $2,554 | $28,242 | $142,409 |
| Optimistic | 10% | 6% | $82 | $4,524 | $47,936 | $240,882 |

### 6.3 Recipe/meal planner ($7.99/mo, $39.99/yr, 55% annual → $5.43 gross, $4.61 net)

| Scenario | % paying | Churn | LTV/payer | Net @10K | Net @100K | Net @500K |
|---|---|---|---|---|---|---|
| Conservative | 2.5% | 12% | $35 | $591 | $8,610 | $44,251 |
| Moderate | 5% | 9% | $46 | $1,632 | $19,021 | $96,303 |
| Optimistic | 8% | 7% | $59 | $2,881 | $31,513 | $158,765 |

The consumer finalists need ~10× the audience of the trades app to produce the same profit, and their LTVs ($35–82) cannot support any paid acquisition at measured CPIs — they are organic-only bets.

### 6.4 Cost stack for the winner (year 1, Calc)
- Development: $0 cash for labour (AI-built); ~$2–4K for design assets, icon, store screenshots, legal templates (ToS, privacy, Stripe Connect agreement review).
- Fixed tooling: Apple $99/yr, Google $25, Supabase Pro $25/mo, EAS Starter $19/mo, Sentry $0–26, PostHog free tier, RevenueCat free→1%, domain/email $20/mo, Stripe Connect $0 (Stripe-handled pricing) → **~$150–250/month**.
- Variable: AI ≈ $1.20/payer/month; SMS reminders via Twilio ≈ $0.01–0.05 each (budget $0.50/payer/month); support (AI-first with human escalation) budget $2/payer/month at scale.
- Marketing: $0–1K/month months 1–3 (founder-led), $3–5K/month months 4–12 contingent on gates.

---

## 7. Top five deep-dives

### 7.1 Solo-trades quote-to-cash (winner)

**Market.** US: 2.9M non-employer construction businesses (NAICS 23), 1.9M specialty-trade, average receipts <$70K (Census via NAHB, 3P citing V); plus landscaping/cleaning outside NAICS 23 (not counted). NewView Capital cites 2.5M+ US home-service businesses and $650B annual spend (V, investor). UK 756K self-employed construction (V). Australia 279K non-employing (3P). Field-service software market $5.1B (2025) → $9.2B (2030), 12.5% CAGR (MarketsandMarkets, V as published; other estimates differ 2×). Demographics: owner-operators 25–55, on-site all day, phone-first, often paid by cash/Zelle/bank transfer, chronically chasing invoices.

**Demand.** See §4.1. Additional: DIYnot thread (Aug 2026) asks "quoting on site — what do you actually use?"; ElectriciansForums asks for invoice-viewed notifications; Jobber ran a podcast episode and referral programme (referred customers +5% LTV, vendor case study).

**Product.** Core: customers, quotes, invoices, PDF, send by SMS/email/WhatsApp link, payment links and Tap to Pay, deposits, schedule, job photos, notes, offline-first. AI: voice→quote ("replace the consumer unit, 10-way, Hager, includes certificate, two visits") → structured line items with the tradesperson's own price-book; photo→line items for materials; auto-chase sequences with tone control; "quote assistant" that flags missing items (permit, disposal, travel). Premium/Team: shared schedule, multiple users, CIS/VAT (UK), sales tax (US), QuickBooks/Xero export, review requests, supplier price-books, AI phone answering (later, $29–49 add-on).

**USP (one sentence):** *Quote it on site by talking, get paid before you leave, never pay more than you signed up for.*

**Expansion.** Adjacent trades (cleaning, landscaping, detailing, inspections at higher price points); UK/AU/CA; AI phone answering; embedded financing (invoice factoring) later; marketplace for subcontract overflow.

**Commercial.** Pricing §5; acquisition §12; retention via data gravity (customers, quotes, payment history), price-lock, seasonal pause. Operating costs §6.4. Profitability: 85%+ gross margin; break-even ~250 payers.

**Risks.** Competition (Jobber/Joist AI; Square free); saturation of the "invoice maker" keyword; App Store rules (subscription must use IAP; payments to tradespeople must *not*; AI data-sharing disclosure 5.1.2(i)); acquisition difficulty (business CPI $6.86); retention (side-hustlers churn); technical (offline sync conflicts, PDF fidelity, Stripe Connect onboarding/KYC drop-off, Tap to Pay entitlement); legal/privacy (customer PII, payment data via Stripe only, GDPR for UK, state sales tax display).

### 7.2 GLP-1 companion (runner-up)

**Market.** 12% of US adults currently on a GLP-1, 18% ever (KFF, Nov 2025, V); 11% for weight loss (Gallup Jul 2026, V) up from 3% in 2024; 56% say hard to afford, 14% stopped for cost, 13% for side effects (KFF). Oral Wegovy launched Jan 2026 at $149/mo starter (V); Lilly's Foundayo approved Apr 2026, $149–299 cash (V/3P); MHRA approvals Jun/Aug 2026 (V); NHS coverage limited, UK private from £44–89/mo (3P). Compounding crackdown ongoing (FDA warning letters Mar 2026, V). Subreddits: r/Zepbound 243K, r/Mounjaro 204K, r/semaglutide ~200K, r/Ozempic ~140K (3P).

**Demand.** Shotsy's trajectory (above) and MeAgain's 40K ratings show paying demand for a *tracker with community-shaped features* (shareable charts, injection-site rotation, "medication level" estimate). Medscape notes level-charts use undisclosed pharmacokinetics — accuracy-claim exposure (V).

**Product.** Dose/titration calendar for injections *and pills*, side-effect journal with pattern insights, protein/fibre/hydration targets, strength-training log for muscle retention, weight/measurement trends, shareable progress cards, "questions for your prescriber" summaries, off-ramp/maintenance mode, UK/EU dosing names and NHS/private pathways. AI: photo meal logging with protein emphasis; weekly plain-English summary; never dosing advice.

**Commercial.** $9.99/mo or $49.99/yr, annual-first; organic via community groups and creator testimonials; retention by tying to medication cycles and the off-ramp phase.

**Risks.** Free subsidised competitors (Noom, MFP, Novo); Apple 1.4.1 and the medical-device declaration (Mar 2026, V); FTC Health Breach Notification Rule and Washington MHMDA (V); EU MDR/UK SaMD classification for anything beyond logging (U — needs counsel); churn on discontinuation; dependence on a drug market shaped by pricing politics.

### 7.3 Short-video recipe import + weekly meal planner

**Market/demand.** ReciMe (#1 grossing Food & Drink both stores, 3P), new viral planners in the top 10 (3P), Mealime shutdown (V) and Paprika's subscription switch (V) displace users now. #easyrecipe billions of views (3P, partial counts).

**Product.** Share-sheet import from TikTok/Reels/YouTube using on-device OCR and speech-to-text of the user's own screen capture plus pasted captions (lower ToS risk than server scraping — needs counsel); AI normalisation, scaling, substitutions; weekly plan, grocery list by aisle, household sharing; one-time "Lifetime" alongside annual.

**Commercial.** $7.99/mo, $39.99/yr, $79 lifetime; TikTok-native growth (creators demo importing *their own* recipes — built-in UGC).

**Risks.** Paprika $14.99/yr anchor; platform ToS/API changes; clone flood; "saving ≠ cooking" retention; AI-recipe distrust (20% of complaints).

### 7.4 Co-parenting ledger with one-parent mode

**Market/demand.** 10.24M US one-parent families (upper bound, FRED/Census V); courts and lawyers recommend apps (captive demand); per-parent pricing resentment and failed-notification complaints (3P review mining); AppClose/TalkingParents ending free plans in 2026 pushes price-sensitive parents to look.

**Product.** Tamper-evident message log with read receipts, custody calendar modelled on real orders (alternating weeks, holiday overrides, exceptions), expense ledger with receipts and 50/50 or % splits, court-ready PDF exports, **one-parent mode** (works fully even if the ex never joins — logs SMS screenshots, documents exchanges), AI that drafts the calendar from an uploaded custody order *with mandatory human review*, and a tone-check on outgoing messages.

**Commercial.** $49/yr per parent or $79/yr per family; family-lawyer and mediator referral programme; multi-year retention.

**Risks.** Courts' familiarity with OFW; asymmetric downside of a parsing error; support burden; OFW owns Cozi and can bundle.

### 7.5 Self-employed mileage + receipts + tax set-aside

**Market/demand.** 11.9M US independent contractors (BLS 2023, V); MileIQ's price trajectory and 2.8★ recent Play rating (3P); IRS rate changes mid-year (72.5¢ → 76¢ for Jul–Dec 2026, V) confuse users.

**Product.** Automatic drive detection (Core Motion / Android Activity Recognition), AI receipt capture, quarterly tax set-aside calculator, one-tap IRS/HMRC-ready log. Price-locked $59/yr.

**Commercial/risks.** Free unlimited auto-tracking already exists (Stride, TripLog, V); Everlance/Hurdlr/Solo cover the bundle; battery/missed-drive complaints are a support sink; ranked #5 because differentiation is price alone.

---

## 8. Risk analysis and red-team (self-critique plus independent GPT-6.1 review)

### Winner — why it could fail
1. **"Trades" is not one workflow.** A cleaner's recurring invoice, a plumber's emergency callout and a renovation estimate are different products. *Mitigation adopted:* beachhead = residential service-call trades (plumbing, electrical, HVAC, handyman) where the loop is identical: callout → diagnose → quote on site → do the job → invoice → get paid same day. Cleaning and landscaping come later as "recurring job" mode.
2. **Differentiation is a pricing policy plus copyable features.** Square and Wave are free; Joist and Jobber ship AI quoting. *Mitigation:* the moat has to be built from (a) a payments relationship and data gravity, (b) a trusted distribution channel (creators, supplier counters, bookkeepers), and (c) demonstrated collection outcomes ("paid 9 days faster"), not from feature lists. Price-lock is marketing, not defence.
3. **Switching is work.** Importing customers/templates from Joist/Invoice Simple must be one-tap (CSV import plus AI mapping) and the first quote must be sendable within 3 minutes of install.
4. **CAC could kill it.** Apple Ads yields ~$143/payer (Calc) — 10-month payback. Only community/creator/partner channels at ≤$50 make this fundable. This is the single gating assumption.
5. **Would a mobile website suffice?** For quotes and invoices, largely yes — which is why native must earn its keep with offline mode, camera/voice capture, Tap to Pay, push for "invoice viewed/paid" and a home-screen presence. Also ship a web portal for the office/partner.
6. **Does AI genuinely improve it?** Voice→draft quote: yes (time-to-send). Photo→binding price: dangerous (hidden damage, access, local labour rates) — AI proposes line items, the human prices them; the price-book is theirs. Auto-chase: valuable, copyable.
7. **Recurring value?** Strong for frequent invoicers; weak for side-hustlers. Qualification: target operators issuing ≥5 documents/month; design onboarding to surface that quickly.
8. **Platform/policy.** Subscription must go through IAP (3.1.1); payments to tradespeople must *not* (3.1.3(e)); AI data-sharing requires explicit consent naming the provider (5.1.2(i)); UK VAT/CIS and US sales-tax presentation; Stripe Connect KYC drop-off.

### Runner-up (GLP-1) — why it could fail
Subsidised free competitors; the safe product is undifferentiated and the differentiated product is regulated; treatment transitions cause churn; LTV ($49–82) cannot fund paid acquisition — organic-only; founder-story community growth (Shotsy) may not be repeatable.

### Recipe planner — why it could fail
Price anchor collapse (Paprika $14.99/yr), dependence on platforms for both import and distribution, retention masked by collection growth, AI-recipe distrust.

### Co-parenting — why it could fail
Court-driven demand favours incumbents; one-parent mode removes coordination value; parsing errors have asymmetric downside; lawyer-referral sales are slow.

### Mileage — why it could fail
Free unlimited alternatives; battery/missed-drive support burden; no durable differentiation.

### Market-level risks for all
RevenueCat 2026: the median app grows 5.3% and 72% of annual subscribers cancel in year one. Only hard-paywall, high-price, channel-owning apps escape the "vanishing middle". The plan below is designed for that regime.

---

## 9. The single winning application

**Solo-trades quote-to-cash — residential service trades, US first, UK second.**

It beats the field on the four things that compound: ARPPU (3× consumer), retention (business data gravity + seasonal pause instead of cancel), a second revenue line outside app-store commission (payments), and a buyer who is reachable through communities and creators without a seven-figure UGC budget. It benefits from AI-assisted development more than any other candidate because its surface area is broad and well-specified, and it benefits from in-product AI in a way that is useful without being safety-critical. It does not depend on a drug-pricing cycle, a platform's ToS, or a court's habits.

What it is not: a quick viral hit. The RevenueCat median to $1K MRR for business apps is 113 days. The plan accepts that and front-loads validation.

---

## 10. Complete product blueprint

### A. Product identity
- **Name ideas:** Jobsheet · Quoted · Paidly · SiteSlip · Callout · Tradeslip (check trademarks and App Store name availability; "Jobsheet" has UK resonance, "Quoted" reads well in the US).
- **Positioning:** "The quote-and-get-paid app for one-van trades. Talk the job, send the quote, get paid on site. Your price never goes up."
- **Audience:** owner-operators and 2–3 person crews in plumbing, electrical, HVAC, handyman; US residential; later UK (CIS/VAT), AU/CA.
- **Core problem:** admin after a 10-hour day — writing quotes at the kitchen table, forgetting to invoice, chasing payers, paying more every year for an app that caps documents.
- **USP:** voice-to-quote on site + same-day payment + automatic chasing + price-lock + no caps + works offline.
- **Main competitors:** Invoice Simple, Invoice Fly, Joist, Jobber Core, Housecall Pro Basic, Square Invoices (free), SimplyWise, QuoteIQ.

### B. Product design

**Complete feature list**
- Customers (import from contacts/CSV/Joist/Invoice Simple), job addresses, history
- Quotes: AI voice/text/photo → draft line items; personal price-book with margins; optional items; deposit request; e-signature/acceptance link; expiry; quote-viewed notification
- Jobs/schedule: calendar, job status, photos before/after, notes, checklists, reminders
- Invoices: one-tap from quote; progress/partial; recurring (later); sales tax / VAT; PDF with branding; send by SMS/email/WhatsApp link
- Payments: Stripe Connect Express onboarding; card links; Apple/Google Pay; Tap to Pay on iPhone/Android; ACH/bank; deposits; tips; auto-reconcile; payout tracking
- Auto-chase: configurable sequences (day 1 friendly, day 7 firm, day 14 final), tone presets, pause per customer, "paid" auto-stop, late fee option
- Reports: cash collected, outstanding, aged receivables, tax-ready export (CSV, QuickBooks/Xero)
- Offline-first with conflict-safe sync
- Web portal (office/partner access), customer-facing quote/invoice pages
- Settings: price-lock certificate, data export, pause subscription

**MVP (ship by day 30):** customers, quotes with AI voice draft and price-book, quote→invoice, PDF, send by link, Stripe payment links, basic auto-chase (3-step), offline cache, onboarding import, 14-day trial, RevenueCat paywall.

**Premium/Team (months 3–6):** Tap to Pay, deposits/acceptance, schedule, multi-user, QuickBooks/Xero export, review requests, UK CIS/VAT, AI phone answering add-on (month 9+).

**Onboarding (target: first quote sent in <3 minutes):** 1) trade + country; 2) import contacts/CSV or skip; 3) logo/business name (AI pulls from Google Business if provided); 4) "say your last job out loud" → first quote generated → send to yourself; 5) connect payments (can defer); 6) trial starts, no card.

**Main screens:** Today (jobs, unpaid, actions) · Quotes · Invoices · Customers · Schedule · Money (collected/outstanding/payouts) · New (voice mic FAB).

**User journey:** on-site mic → draft quote → tweak prices → send → customer accepts & pays deposit → job scheduled → photos → finish → invoice auto-created → paid on site via Tap to Pay or chased automatically → "paid" push → weekly summary.

**Subscription experience:** trial countdown shown as "days of unlimited quoting left"; paywall at day 10 and on trial end with price-lock promise; annual default; pause instead of cancel; export always available.

**Retention features:** unpaid-invoice push, "invoice viewed" push, weekly money summary, year-in-review before renewal, seasonal pause, price-book that grows with use, payment history that becomes a credit/ledger asset.

### C. Technical architecture

| Layer | Choice | Why |
|---|---|---|
| Mobile | **Expo SDK 58 / React Native 0.88 (New Architecture)**, TypeScript | one codebase for iOS + Android + web portal; EAS builds/updates; Opus is strongest in TS; large library ecosystem (Stripe, RevenueCat, camera, speech) |
| Native modules | Stripe Terminal SDK (Tap to Pay), expo-speech-recognition / Apple SpeechAnalyzer wrapper, expo-camera, expo-file-system | on-device transcription for privacy and cost; cloud fallback |
| Backend | **Supabase** (Postgres, Auth, Storage, Realtime, Edge Functions) | $25/mo Pro covers 100K MAU; row-level security per business; PostgREST + RPC; pgvector optional for price-book search |
| Offline | local SQLite (expo-sqlite / WatermelonDB) with outbox queue; server-wins for payments, last-write-wins with audit for documents | field reliability |
| PDF | server-side rendering in an Edge Function (HTML→PDF) with cached templates | fidelity across platforms |
| AI | Claude Haiku 5.5 ($0.10/$0.50 per MTok, V) for quote structuring and reminder drafting; Sonnet 5.5 for photo→line items; OpenAI gpt-4o-mini-transcribe ($0.003/min) as cloud STT fallback; strict JSON schemas; price-book grounding; human approval before send | cost ≈ cents per quote; consent screen naming providers (5.1.2(i)) |
| Payments | Stripe Connect Express, Payment Links, Terminal (Tap to Pay); platform fee via `application_fee_amount` | Stripe-handled pricing → no monthly Connect fee |
| Subscriptions | RevenueCat (IAP both stores, Paywalls v2, web billing for annual from site) | 15% store rate under Small Business / Play tiers |
| Messaging | Twilio SMS + Resend email + WhatsApp links; Expo push | chase sequences |
| Analytics | PostHog (events, funnels, session replay), Sentry | free tiers |
| Auth | Supabase Auth (Apple, Google, phone OTP) | tradespeople hate passwords |
| Security/privacy | RLS per tenant; PII minimisation; Stripe holds card data; signed URLs for PDFs; GDPR/UK DPA export & delete; SOC2 not required at launch | |

### D. Growth strategy
- **First 100 users (days 0–30):** 40 founder interviews with owner-operators in one metro (look at their last 10 invoices); 20 hand-onboarded paying pilots at $19; trade Facebook groups (Plumbing Hacks 60K+, ContractorREACH 180K+, 3P) with value posts, not links; local supply-house counters (flyer + QR, buy the counter staff coffee); Reddit r/Plumbing, r/electricians, r/handyman AMAs about quoting ("show me your quote and I'll show you the voice version").
- **First 1,000 (months 2–4):** 10–15 micro-creators (10–100K) in trades on flat-fee + affiliate (Tradify's and Jobber's playbook, 3P); one mid-size YouTube sponsorship test ($2–5K) with a tracked promo; ASO on long-tail terms ("plumber invoice app", "electrician estimate app", "handyman quote") rather than "invoice maker"; referral: give a month, get a month; App Store review prompts after a paid invoice.
- **First 10,000 (months 5–12):** repeatable creator programme (20–40 creators, performance-paid), supplier/bookkeeper partnerships (B2B2C: wholesaler newsletters, accountant referrals), UK launch with CIS/VAT via UK creators (Bald Builders-scale audiences exist, 3P), Apple Ads only on brand + long-tail with ROAS gates, web-to-app landing pages per trade, "paid faster" case studies as content.
- **First 100,000 (year 2+):** adjacent trades (cleaning, landscaping, detailing), AI phone answering as a wedge (a $29–79/mo category today), integrations marketplace (QuickBooks/Xero/supplier catalogues), AU/CA, payments-led upsell, possibly embedded financing. Paid UA at scale only once blended CAC payback <6 months is proven across two channels.

**Shareability:** every quote/invoice page carries "Sent with [Name]"; the "paid in X days" summary card is designed to be screenshot into trade groups; creator content is naturally demo-able (talk → quote appears).

### E. Financial roadmap (Calc; milestones are validation gates, not forecasts)

| Horizon | Spend | Milestones / gates |
|---|---|---|
| 30 days | ≤$1.5K (tooling, legal templates, assets) | MVP in TestFlight/Play internal; 40 interviews done; **gate A:** ≥20 of 40 show ≥2 hrs/week avoidable admin or ≥$500 overdue; 20 paying pilots recruited at real price |
| 90 days | ≤$5K cumulative | Public launch both stores; **gate B:** ≥15 of 20 pilots sent ≥5 real documents in 14 days and ≥15 still paying at day 90; quote-to-send time ≥50% faster than their previous method; ≥50 payers total; first 50 acquired outside founder network at ≤$50 fully-loaded CAC (**gate C**) |
| 6 months | ≤$20K cumulative | 250–400 payers (≈ break-even), payments adoption ≥40% of payers, monthly churn ≤5%, creator programme with ≥3 creators at positive ROAS, UK beta |
| 12 months | ≤$60K cumulative | 1,000–2,000 payers ($15–30K subscription MRR + $5–15K payments revenue in the moderate case), Team tier live, QuickBooks/Xero, AI phone answering beta, UK live; decision point on raising or staying bootstrapped |

If gate A or B fails, pivot within the same build: (1) a *collections overlay* that plugs into existing invoicing tools and only does auto-chase and reconciliation (red-team suggestion — attacks the stated pain without migration), or (2) move to a higher-WTP niche trade (home inspection reports at ~$109/mo incumbents).

---

## 11. Recommended technology stack (summary)
Expo SDK 58 / React Native (New Architecture) + TypeScript · Supabase (Postgres/Auth/Storage/Realtime/Edge Functions) · expo-sqlite offline outbox · Stripe Connect Express + Terminal (Tap to Pay) · RevenueCat (IAP + Paywalls v2 + web billing) · Claude Haiku 5.5 / Sonnet 5.5 for structured drafting; on-device speech with cloud fallback · Twilio/Resend for chase sequences · PostHog + Sentry · EAS Build/Update. Flutter is a reasonable alternative (3.50 stable, V) but React Native's Stripe Terminal and RevenueCat maturity, plus the shared web portal, tip the choice.

**Difficulty:** medium. **Time to MVP:** 3–4 weeks of AI-assisted build with daily device testing. **Backend complexity:** medium (multi-tenant RLS, sync, PDF, webhooks from Stripe). **Platform limits:** Tap to Pay requires Apple entitlement and Stripe Terminal onboarding; background location not needed; iOS/Android share-sheet for photos; Android involuntary billing churn (31%) needs grace-period handling. **Maintenance:** OS updates twice yearly, Stripe/RevenueCat SDK bumps, tax-rule tables.

---

## 12. Customer acquisition strategy (consolidated)
1. **Community-first (months 1–3):** trade Facebook groups, subreddits, supply-house counters, local trade associations; founder answers quoting questions publicly.
2. **Creator programme (months 2–12):** micro-creators on flat fee + affiliate; mid-size YouTube sponsorships only with tracked codes; reuse winning creator videos as paid creatives with usage rights (Quittr/Cal AI pattern, U).
3. **ASO:** trade-specific long-tail, screenshots showing the voice-quote moment, ratings prompts after money is collected.
4. **Referral:** month-for-month; tradespeople talk to each other on site.
5. **Partnerships (B2B2C):** wholesalers, bookkeepers/accountants, trade insurers, van-leasing firms — test one partner for 20 activated customers before investing in more.
6. **Paid:** Apple Ads brand defence and long-tail only; Meta/TikTok once creative is proven; strict payback <6 months.
7. **Web-to-app:** per-trade landing pages ("plumber quote app") with annual web checkout.

---

## 13. First 30-day execution plan

| Days | Fable (research/strategy/review) | Opus (build) | Founder |
|---|---|---|---|
| 1–3 | Interview script; competitor teardown of Joist/Invoice Simple onboarding; price-book taxonomy for plumbing/electrical/HVAC/handyman | Repo, Expo app shell, Supabase schema (tenants, customers, quotes, invoices, payments, chase_jobs), RLS, auth | Recruit 40 interviewees via groups/counters; trademark & name check; Apple/Google accounts; Stripe Connect application |
| 4–10 | Review schema and data model for tax/VAT extensibility; draft ToS/privacy/AI consent copy; define metrics (time-to-first-quote, docs/14 days, chase→paid days) | Customers, quotes, price-book, AI voice→quote (Haiku, JSON schema), PDF function, send-by-link | Run 20 interviews; collect real quotes/invoices (anonymised) as test corpus |
| 11–17 | Red-team the AI quote outputs against the real corpus (accuracy, hallucinated items); paywall copy & pricing test plan | Invoices, quote→invoice, Stripe payment links + webhooks, auto-chase sequences (Twilio/Resend), offline outbox | Finish interviews; **gate A decision**; recruit 20 paying pilots |
| 18–24 | Independent code review (security/RLS/webhook idempotency); onboarding usability review from recordings | Onboarding + import (CSV/contacts), RevenueCat trial/paywall, PostHog events, Sentry, TestFlight/Play internal | Onboard pilots by phone; daily feedback loop |
| 25–30 | Pilot data readout vs gate B leading indicators; ASO keyword set; creator shortlist (15) | Bug-fix, polish, store listings, screenshots/video, submit for review | Store submissions; line up 3 micro-creators for month 2 |

Deliverable at day 30: app in review on both stores, 20 paying pilots using it daily, gate A result, a decision memo.

---

## 14. Twelve-month business roadmap

| Month | Product | Growth | Finance/ops |
|---|---|---|---|
| 1 | MVP, pilots | interviews, groups | gate A |
| 2 | Public launch; chase v2; quote acceptance & deposits | first 3 creators; ASO; referral | first 50 payers |
| 3 | Tap to Pay (iOS/Android); schedule | gate C channel test (≤$50 CAC) | gate B readout; break-even trajectory |
| 4 | Team tier; QuickBooks/Xero export | creator programme 10+; supplier partner pilot | 150–250 payers |
| 5–6 | UK beta (VAT/CIS, GBP, Tap to Pay UK); review requests | UK creators; web-to-app per trade | ~break-even (250–400 payers) |
| 7–8 | Recurring jobs (cleaning/landscaping mode); AI job-photo line items | adjacent-trade communities | 500–800 payers |
| 9–10 | AI phone answering beta (add-on); price-book sharing | paid UA test with proven creatives | payments ≥40% adoption |
| 11–12 | AU/CA localisation; integrations marketplace v1 | partnerships at scale; case-study content | 1,000–2,000 payers; raise-or-bootstrap decision |

Validation targets through the year: day-14 activation (≥5 documents) ≥60% of trials; trial→paid ≥35%; monthly logo churn ≤5%; payments attach ≥40%; blended CAC payback ≤6 months; support ≤15 min/account/month.

---

## 15. How to use Claude Opus and Fable (workflow)

- **Fable (research, strategy, finance, product, critique, independent reviews):** owns the evidence base and the gates. Produces interview guides and synthesises transcripts; maintains the competitor watch (Joist/Jobber AI releases, price changes); runs weekly cohort/retention analysis from PostHog/RevenueCat exports; writes paywall/onboarding experiments with expected effect sizes; performs *adversarial* reviews of every Opus release (security, RLS, webhook idempotency, data-loss paths, AI hallucination on the real quote corpus) and of every founder decision ("what would make this wrong?").
- **Opus (build):** owns the codebase — schema, RLS, sync, PDF, Stripe/RevenueCat integrations, UI, tests (unit + Maestro/Detox E2E on device), performance, release engineering (EAS), crash triage.
- **Mutual challenge, built in:** (1) every spec Fable writes is implemented by Opus with an explicit "assumptions I had to make" list that Fable must accept or reject; (2) every Opus PR is reviewed by Fable *and* a second model family (as done for this report) before merge; (3) Fable's financial and channel claims must cite instrumented data, and Opus must reproduce any metric Fable reports from raw events; (4) weekly "kill criteria" review where each model argues the opposite side of the current plan.
- **Verification layer:** CI with typecheck, unit tests, E2E on real devices, Stripe test-mode webhook replay, RevenueCat sandbox purchases, a golden corpus of 100 real (anonymised) quotes scored for AI extraction accuracy on every model/prompt change, and store-review checklists (3.1.1, 3.1.3(e), 5.1.2(i)).

---

## 16. Sources and supporting evidence

### Market benchmarks
- RevenueCat, *State of Subscription Apps 2026* summary: https://www.revenuecat.com/blog/growth/subscription-app-trends-benchmarks-2026 (V)
- RevenueCat SOSA 2026 report hub: https://www.revenuecat.com/state-of-subscription-apps (V)
- SaaStr, top-10 learnings from SOSA 2026: https://www.saastr.com/the-top-10-learnings-from-revenuecats-state-of-subscription-apps-how-115000-mobile-apps-deliver-16b-in-revenue-whats-working-whats-quietly-killing-growth/ (3P)
- RocketShip HQ summary of SOSA 2025: https://www.rocketshiphq.com/revenuecat-state-of-subscription-apps-2025-summary/ (3P); RevenueCat 2025 PDF: https://www.revenuecat.com/pdf/state-of-subscription-apps-2025.pdf (V)
- RevenueCat Sub Club on SOSA 2025: https://www.revenuecat.com/blog/growth/sosa-2025-launch-sub-club (V)
- Sensor Tower, State of Mobile 2026 press release: https://sensortower.com/press/press-release-boosted-by-gen-ai-services-consumers-spent-more-money-in-apps-than-games-for-first-time (V); blog: https://sensortower.com/blog/state-of-mobile-2026 (V)
- Sensor Tower, AI apps H1 2025: https://sensortower.com/blog/state-of-ai-apps-market-overview-2025 (V); State of AI 2026: https://sensortower.com/report/state-of-ai-2026 (V)
- Appfigures, ChatGPT and rivals revenue: https://appfigures.com/resources/insights/chatgpt-ai-chatbot-revenue-rivals (3P); identifiers category: https://appfigures.com/resources/insights/20250509?f=1 (3P); cleaner apps: https://appfigures.com/resources/this-week-in-apps/20250606 (3P)
- AppTweak Apple Ads benchmarks 2025: https://www.apptweak.com/en/aso-blog/apple-ads-benchmarks (3P)
- Airbridge, cost per trial/subscription: https://www.airbridge.io/en/blog/cost-per-trial-cost-per-subscription-subscription-app-ua-metrics (3P)
- Leapwave CPI by category: https://leapwave.ai/resources/cpi-benchmarks-by-category (3P)
- Sensor Tower download sources (2021 report): https://sensortower.com/blog/app-store-download-sources-report-2021 (V, dated)
- UXCam retention benchmarks compilation: https://uxcam.com/blog/mobile-app-retention-benchmarks/ (3P)
- RevenueCat IAP vs web test: https://www.revenuecat.com/blog/growth/iap-vs-web-purchases-conversion-test (V); Superwall app-to-web data: https://superwall.com/blog/initial-data-is-in-app-to-web-conversion-rates-after-the-app-store-ruling/ (V, vendor)
- Apple Small Business Program: https://developer.apple.com/app-store/small-business-program/ (V); App Review Guidelines: https://developer.apple.com/app-store/review/guidelines/ (V); 5.1.2(i) update: https://developer.apple.com/news/?id=ey6d8onl (V); medical-device declaration: https://developer.apple.com/help/app-store-connect/manage-app-information/declare-regulated-medical-device-status (V)
- Apple EU terms Oct 2026: https://www.apple.com/newsroom/2026/08/apple-announces-changes-for-apps-in-the-european-union/ (V); Ninth Circuit opinion Dec 2025: https://cdn.ca9.uscourts.gov/datastore/opinions/2025/12/11/25-2935.pdf (V); Apple proposed US link-out rates: https://9to5mac.com/2026/08/13/apple-proposes-commissions-of-up-to-15-for-off-app-store-purchases-in-the-us/ (3P)
- Google Play fees: https://support.google.com/googleplay/android-developer/answer/112622 (V); Epic settlement coverage: https://techcrunch.com/2026/03/04/google-settles-with-epic-games-drops-its-play-store-commissions-to-20/ (3P)
- Pricing pages: Anthropic https://platform.claude.com/docs/en/about-claude/pricing (V); OpenAI https://developers.openai.com/api/docs/pricing (V); Supabase https://supabase.com/pricing (V); RevenueCat https://www.revenuecat.com/pricing/ (V); Expo https://expo.dev/pricing (V); Stripe https://stripe.com/pricing and https://stripe.com/connect/pricing (V); Tap to Pay regions https://developer.apple.com/tap-to-pay/regions (V); Expo SDK 58 https://expo.dev/changelog/sdk-58 (V); Flutter 3.50 https://flutter.dev/blog/whats-new-in-flutter-3-50 (V); OneSignal pricing https://onesignal.com/pricing (V); Inworld consumer-AI unit economics https://inworld.ai/resources/unit-economics-of-consumer-ai-apps (3P)

### Trades / field service
- Invoice Simple App Store listing: https://apps.apple.com/us/app/invoice-maker-invoice-simple/id694831622 (V)
- Joist pricing https://joist.com/pricing (V); Joist AI estimates support article: https://support.joistapp.com (article 16760523) (V); Joist App Store reviews: https://apps.apple.com/us/app/joist-estimate-invoice-maker/id592163563?see-all=reviews (V)
- Jobber pricing https://www.getjobber.com/pricing/ (blocked to fetch; 3P readings: https://servicepropicks.com/guides/jobber-core-vs-connect-vs-grow/, https://realcostlabs.com/jobber-pricing/); Jobber $100M Series D: https://techcrunch.com/2023/02/07/jobber-fixes-on-100m-as-its-platform-for-home-services-pros-hits-200k-users/ (V); Jobber ARR podcast: https://www.pmf.show/blog/jobber-forrest-zeisler-100m-arr-startup-growth (U); Contrary Research: https://research.contrary.com/company/jobber (3P)
- Housecall Pro pricing https://www.housecallpro.com/pricing (V)
- ServiceTitan FY2026 results: https://investors.servicetitan.com/news-releases/news-release-details/servicetitan-announces-fiscal-fourth-quarter-and-full-fiscal (V); 10-K: https://www.sec.gov/Archives/edgar/data/1638826/000163882626000028/ttan-20260131.htm (V)
- Square Invoices pricing https://squareup.com/us/en/invoices/pricing (V); Wave https://www.waveapps.com/pricing (V); Zoho Invoice https://www.zoho.com/us/invoice/pricing (V); Tradify https://www.tradifyhq.com/pricing (V); ServiceM8 https://www.servicem8.com/us/pricing (V); Invoice2go https://invoice.2go.com/pricing (V); Billdu https://www.billdu.com/pricing (V); Bookipi https://bookipi.com/pricing (V); SimplyWise, QuoteIQ https://myquoteiq.com, Handoff https://handoff.ai, BuildWell https://buildwellapp.com (V vendor pages)
- Review mining: https://settlejob.com/guides/invoice-app-complaints-app-store-reviews/ (3P); https://opportunitymarket.org/apps/invoice-maker-invoice-simple (3P); https://getwedge.dev/examples/tradesperson-invoicing/ (3P); price history https://settlejob.com/guides/invoice-app-price-history (3P)
- Forums: https://electriciansforums.net/threads/what-invoicing-apps-softwares-do-you-guys-use.212033/ ; https://www.diynot.com/diy/threads/quoting-on-site-what-do-you-actually-use.660164/ ; https://www.contractortalk.com/threads/joist-app.418029/page-3 (snippets, 3P/U)
- Market size: CPWR nonemployer construction https://www.cpwr.com/research/data-center/the-construction-chart-book/interactive-7th/industry-businesses/nonemployer/ (V); Census NES https://www.census.gov/data/developers/data-sets/nonemp-api.2023.html (V); NAHB specialty-trade note (3P); ONS via Construction News (V); NewView Capital on Housecall Pro https://nvc.vc (V); MarketsandMarkets FSM press release (V as published)
- Distribution: vidIQ channel stats for Electrician U / Roger Wakefield / Mikey Pipes (3P); SponsorRadar on Tradify sponsorships (3P); Jobber podcast https://www.getjobber.com/podcast/ep7-paul-jamison-christine-hodge/ (V); SaaSquatch Jobber referral case study https://www.saasquatch.com/blog/how-jobber-strengthens-community-and-increases-ltv-with-saasquatch/ (vendor); PHCP Pros on Plumbing Hacks group (3P)
- Bloomberg on Bending Spoons price hikes (Aug 2026): https://www.bloomberg.com/news/articles/2026-08-13/bending-spoons-customers-decry-outrageous-app-price-hikes (V)

### GLP-1
- KFF poll Nov 2025: https://www.kff.org (GLP-1 tracking poll, V); Gallup Jul 2026: https://news.gallup.com/poll/712157/glp-usage-reaches-new-high.aspx (V)
- Shotsy: App Store https://apps.apple.com/us/app/shotsy-glp-1-tracker/id6499510249 (V); Play https://play.google.com/store/apps/details?id=com.shotsy.app (V); Business Insider funding https://www.businessinsider.com/startup-shotsy-raises-funding-glp1-shot-tracking-app-2025-2 (V); founder interview https://glp1digest.com/p/how-shotsy-grew-to-350000-monthly (U)
- Noom free companion https://www.noom.com/in-the-news/noom-launches-free-version-of-its-powerful-glp-1-companion/ (V); MyFitnessPal GLP-1 support https://news.myfitnesspal.com (V); Novocare app https://apps.apple.com/us/app/novocare/id6751852954 (V); Lose It GLP-1 logging https://loseit.zendesk.com/hc/en-us/articles/50221250242964-GLP-1-Logging (V)
- Oral GLP-1s: FDA Foundayo approval (fda.gov, V); TrumpRx Wegovy pill https://trumprx.gov/p/wegovy-pill (V); MHRA approvals (gov.uk, V); Medscape on GLP-1 apps https://www.medscape.com/viewarticle/glp-1-apps-helpful-companions-or-false-sense-security-2026a1000i9n (V)
- Regulatory: FTC HBNR (federalregister.gov, V); Washington MHMDA RCW 19.373 (V); K&L/King & Spalding summary of FDA wellness policy Jan 2026 (3P)

### Recipes / meal planning
- Mealime shutdown notice https://www.mealime.com/ (V); Paprika 4 news https://paprikaapp.com/news (V); ReciMe App Store https://apps.apple.com/us/app/recime-recipes-meal-planner/id1593779280 (V); Plan to Eat pricing https://www.plantoeat.com/pricing (V); Fledly review analysis https://fledly.app/blog/budget-meal-planner-apps/ (3P); AppStoreTracker ReciMe estimate (3P); TikTok Terms of Service (V); YouTube API developer policies (V); TikTok embed docs https://developers.tiktok.com/doc/embed-videos (V)

### Family / co-parenting
- Cozi plans https://www.cozi.com/compare-plans/ (V); OFW acquires Cozi https://www.prnewswire.com/news-releases/ourfamilywizard-acquires-cozi-1-family-organizing-app-301539136.html (V); OFW pricing https://www.ourfamilywizard.com/plans-and-pricing (V); Civly review study https://www.civly.com/blog/we-read-9600-reviews-of-co-parenting-apps (3P); FRED families with children https://fred.stlouisfed.org/data/TTLFMCU (V) and one-parent families https://fred.stlouisfed.org/series/TTLOPFWCU (V); Skylight subscription https://skylight.zendesk.com/hc/en-us/articles/51833126965019-Subscription (V)

### Mileage
- MileIQ pricing https://www.mileiq.com/pricing (V); MileIQ price-increase support note https://support.mileiq.com/hc/en-us/articles/48521755984788-Update-MileIQ-subscription-price-increase (V); FlatMile price history https://flatmile.com/what-happened-to-mileiq/ (3P, competitor); Willkie on Bending Spoons acquisition (V); Everlance pricing https://www.everlance.com/pricing (V); Driversnote https://www.driversnote.com/pricing (V); Solo https://www.worksolo.com/pricing (V); IRS standard mileage rates https://www.irs.gov/tax-professionals/standard-mileage-rates (V); BLS contingent workers https://www.bls.gov/news.release/conemp.nr0.htm (V); Google Activity Recognition transition API (V); Play background-location policy https://support.google.com/googleplay/android-developer/answer/9799150 (V)

### Consumer AI / growth case studies
- TechCrunch, MyFitnessPal acquires Cal AI: https://techcrunch.com/2026/03/02/myfitnesspal-has-acquired-cal-ai-the-viral-calorie-app-built-by-teens/ (V); Apple pulls Cal AI: https://techcrunch.com/2026/04/21/apples-cal-ai-crackdown-signals-its-still-policing-the-app-store/ (V); CNBC on Cal AI https://www.cnbc.com/make-it/2025/09/06/cal-ai-how-a-teenage-ceo-built-a-fast-growing-calorie-tracking-app.html (V); Latka interview (U) https://getlatka.com/companies/calai.app/interviews/cal-ai-zach-yadegari-2025
- Opal: https://gtmsauce.com/companies/opal (U); Speedinvest https://www.speedinvest.com/knowledge/scaling-smart-how-opal-built-a-10m-arr-business-in-just-2-years (U); RevenueCat Sub Club with Kenneth Schlenker https://www.revenuecat.com/blog/growth/kenneth-schlenker-sub-club-podcast-2026 (V)
- Umax/RizzGPT: Fortune https://fortune.com/2024/07/01/looksmaxxing-apps-rate-teen-boys-faces-mental-health/ (V/U); Forbes https://www.forbes.com/sites/josipamajic/2024/10/07/hacking-the-app-store-gen-zs-15m-arr-bootstrapped-success-story/ (V as reported)
- Quittr founder interview https://boringcashcow.com/interview/interview-with-the-founder-of-quittr (U)
- Otter $100M ARR https://otter.ai/blog/otter-ai-caps-transformational-2025-with-100m-arr-milestone-industry-first-ai-meeting-agents-and-global-enterprise-expansion (V); Plaud profitability (Forbes, Sept 2025, V)
- Speak $100M revenue (Benzinga citing Forbes, V as reported); Duolingo Q3 2026 (Observer, V)
- Locket (TechCrunch Nov 2025, V); StoryGraph 5M users (founder newsletter, V); Strava acquires Runna (The Verge, V)
- Clipping-rate vendor pages: https://markapping.com/apps/clipping-campaigns-for-apps, https://clippertask.com/apps (U)

### What could not be verified (declared)
Reddit threads (403 throughout); Jobber and Housecall Pro actual ARR; Invoice Simple/Invoice Fly revenue; Cal AI deal price and gross margin; Shotsy's paying-subscriber count (conflicting founder claims); every app-intelligence revenue estimate (treated as order-of-magnitude); Apple's own keyword popularity scores; EU MDR/UK SaMD classification of dose-logging apps; Meta/Instagram terms in primary form; Google Play June 2026 billing-flexibility details; exact Claude model names/prices beyond the pricing page as retrieved on the research date.
