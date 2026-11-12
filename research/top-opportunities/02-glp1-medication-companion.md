# 02 — GLP-1 Medication Companion (Score 75/100) — RUNNER-UP

**Concept:** consumer companion app for people on GLP-1 medications (Ozempic/Wegovy/Zepbound/Mounjaro, compounded semaglutide/tirzepatide, and the 2026 oral pills): dose/titration calendar for injections *and* pills, side-effect journal with pattern insights, protein/fibre/hydration targets, strength-training log for muscle retention, weight/measurement trends, shareable progress cards, "questions for your prescriber" summaries, off-ramp/maintenance mode, UK/EU dosing names and pathways. AI for photo meal logging (protein emphasis) and weekly plain-English summaries — never dosing advice.

**Pricing:** $9.99/month or $49.99/year, annual-first. Organic community-led acquisition.

**Position in the portfolio:** the right *second* app for this operation — faster to build and cheaper to grow than the winner, but ~3× lower ARPPU, now facing free subsidised competitors, and carrying medical-device-declaration and accuracy-claim risk.

Evidence labels: **V** verified (primary/press), **3P** third-party estimate, **U** unverified, **Calc** own calculation. Research date 12 Nov 2026.

---

## 1. Score breakdown

| Criterion | Score | Rationale |
|---|---|---|
| Demonstrated market demand | 17/20 | 12% of US adults currently on a GLP-1, 18% ever (KFF Nov 2025, V); 11% for weight loss (Gallup Jul 2026, V) up from 3% in 2024; Shotsy 4.8★/~35K iOS ratings, MeAgain 4.8★/40K |
| Revenue potential | 13/20 | $40–60/yr consumer pricing; Shotsy founder claims 100K+ paying subscribers (U) |
| Competition & differentiation | 9/15 | Shotsy and MeAgain lead the indie field; Noom, MyFitnessPal and Novo Nordisk now give trackers away free (V) |
| Customer acquisition | 13/15 | Community-driven: r/Zepbound 243K, r/Mounjaro 204K, r/semaglutide ~200K, r/Ozempic ~140K (3P); shareable charts; Shotsy reports 2/3 of users from community groups and zero ad spend (U) |
| Retention | 7/10 | Strong during active treatment; stops when medication stops (14% stop for cost, 13% for side effects — KFF) |
| Development feasibility | 8/10 | Simple data model; HealthKit/Health Connect integration; photo logging |
| Profitability & scalability | 8/10 | Low AI cost (~$0.35/payer/month); organic-only economics |
| **Total** | **75** | |

**Biggest risk:** free subsidised competitors and regulatory drift (anything beyond logging may be a medical device).

---

## 2. Market

- **US prevalence:** KFF (fielded 27 Oct–2 Nov 2025, n=1,350): 12% currently take a GLP-1, 18% ever; 56% of users say hard to afford; 14% stopped for cost, 13% for side effects; use is 22% among ages 50–64 (V). A later KFF poll (Feb–Mar 2026) is cited at 12% again (3P). Gallup (Jul 2026, updated Sep): 11% take a GLP-1 for weight loss, 15% have ever (V).
- **Oral GLP-1s (expanding the market in 2026):** Novo's Wegovy pill launched 5 Jan 2026 at $149/month starter (V); Lilly's Foundayo (orforglipron) FDA-approved 1 Apr 2026 (V); cash prices $149 (2.5 mg), $199 (5.5 mg), $299 (9 mg+) via LillyDirect/TrumpRx (3P); Wegovy pill $149/$199/$299 on TrumpRx at 78–89% off list (V).
- **UK/EU:** MHRA approved semaglutide tablet 11 Jun 2026 and Foundayo 10 Aug 2026 (V); NHS covers Mounjaro/Wegovy injections for limited groups; pills private-only; UK private starter prices Mounjaro 2.5 mg from £89, Wegovy 0.25 mg from £44, Wegovy pill from £52.99 (3P); EU access lags (Politico, V).
- **Compounding crackdown:** 30 FDA warning letters to telehealth firms 4 Mar 2026 (V); FDA proposed excluding semaglutide/tirzepatide/liraglutide from the 503B bulks list 30 Apr 2026 (V; final status U); Import Alert 66-80 revised 9 Oct 2026 (V).
- **Communities:** r/Zepbound 243K, r/Mounjaro 204K, r/semaglutide 183–207K, r/Ozempic 138–145K (3P). GummySearch notes r/Semaglutide discussions frequently mention "app" and "provider" (3P). Shotsy's founder says the product came from a Reddit post and chart screenshots circulate on Reddit and Facebook (U).
- **Adjacent programmes:** Omada GLP-1 Care Track 150K+ members, Voy 85K+ (3P); Ro $39 first month then $149/mo (3P); Noom Med $129/mo after month one (3P); WW Med+ billed separately from meds (V).

---

## 3. Customer problem

1. **Who:** adults on GLP-1 therapy for weight loss or diabetes, increasingly self-paying and on oral pills; 50–64 is the heaviest-using cohort.
2. **Frequency:** daily (pills, side effects, protein) and weekly (injections, weigh-ins, titration).
3. **Importance:** medication is expensive ($149–299/mo cash) and side effects drive discontinuation — people want to protect the investment and manage the journey.
4. **What they use now:** Shotsy, MeAgain, Glowise, Pep AI; free Noom/MFP/Novocare; spreadsheets; Reddit threads.
5. **Cost of current solutions:** $0 (big-player free tiers) to $39.99–119.99/yr (indies).
6. **Why insufficient:** free tools are generic trackers inside weight-loss funnels; indie trackers rely on "medication level" charts with undisclosed pharmacokinetics (Medscape, V); pill users are under-served by injection-centric apps; off-ramp/maintenance support is thin.
7. **Will they pay:** yes — Shotsy's and MeAgain's ratings volumes and paid tiers prove it; the question is whether a second-mover can carve a segment (pill-era, international, off-ramp) that the free tiers ignore.

---

## 4. Competitor analysis

| App | Price | Rating | Notes |
|---|---|---|---|
| Shotsy | IAPs $9.99 / $14.99 monthly, $39.99 / $49.99 / $59.99 yearly (V listing) | 4.8 / ~35K iOS; 4.7 / 13.2K Play, 100K+ installs (V) | $2M seed, Springbank Collective (Business Insider, V); 6 staff (3P); founder claims 1M+ downloads with zero ad spend, 100K+ paying subscribers, 25K five-star reviews (Jun 2026 podcast, U), 350K MAU, cash-flow positive, ~2/3 of new users from community groups (U); Medscape cites >250K MAU (3P); AppGazers Play revenue $20–97K/mo (3P); #75 US Health & Fitness grossing (3P); earlier BI report: $1M run rate in ~8 months, launched via a Zepbound subreddit (V) |
| MeAgain | $14.99–119.99 IAPs | 4.8 / 40.1K (3P) | claims 372K registered users (3P) |
| Glowise | $5.99–69.99 | 4.8 / 6.7K (3P) | |
| Pep AI / Pep (Shred) | $9.99–49.99 | 4.7 / 4.0K; 4.7 / ~970 (3P) | lists retatrutide and compounded semaglutide/tirzepatide (V) |
| GlucoPal / DreamMe / Glapp | free + Pro / — / — | 4.7–4.8 / 1–3K (3P) | long tail; also Regimen, Mingo (lifetime), Lumi, Glippy, JabKeeper, Dozify |
| Off-ramp/maintenance apps | — | — | OffRamp, Leanos, Cove Maintain, Sharpy already exist |
| **Noom GLP-1 Companion** | **free** (launched 24 Jun 2026, V) | — | dose and side-effect tracking, protein targets, AI photo meal logging, "Muscle Defense" workouts; open to any GLP-1 user regardless of provider |
| **MyFitnessPal GLP-1 Support** | **free** for all users (28 Apr 2026, V) | — | dose, time, injection site, reminders, side effects |
| Lose It | Premium-only GLP-1 logging with estimated medication levels (V) | — | |
| MyNetDiary | Premium GLP-1 Companion (3P) | — | |
| **Novocare (Novo Nordisk)** | **free** (V) | 4.2 / 10 | Wegovy pill + injection, dose tracking, reminders, live coaches |
| Lilly | support via "Lilly Health app" + email/text (V) | — | no dedicated dose tracker found |

**Ownership:** Shotsy is seed-funded; MeAgain and the long tail are indie; the free tier is now owned by a coaching company (Noom), a nutrition incumbent (MFP) and a drug manufacturer (Novo) — each subsidising tracking to support another revenue stream.

---

## 5. Distribution and viral potential

- **Community-first:** subreddits (800K+ combined subscribers), Facebook GLP-1 groups, Discords; Shotsy's founder-reported growth was entirely community-driven (U) and the product's charts are screenshot-shared.
- **Short-form video:** "my GLP-1 journey" content is abundant; the app's progress cards and side-effect timelines are naturally shareable; creator testimonials from people documenting their journey.
- **ASO:** "GLP-1 tracker", "Ozempic tracker", "Zepbound tracker", "Mounjaro app", "Wegovy pill" — pill-era terms are new and less contested.
- **Paid:** Apple Ads Health & Fitness US median CPI $3.77 (AppTweak 2025, 3P). At 2% download-to-paid, payer CAC ≈ $189; at 10.7% (hard paywall) ≈ $35 — against ≈ $42.49 net first-year revenue on a $49.99 annual plan (red-team Calc). **Paid acquisition is untenable; this is an organic-only bet.**
- **Referral:** invite a "buddy" on the same medication; shared accountability features.

---

## 6. Monetisation design

- **Model:** freemium with annual-first subscription ($9.99/mo, $49.99/yr); consider a lifetime option (Mingo does this) for the maintenance phase.
- **Free:** dose calendar and reminders (table stakes now that Noom/MFP/Novo are free).
- **Paid:** side-effect pattern insights, protein/muscle programme, AI photo logging, weekly summaries, prescriber-question reports, progress cards, off-ramp mode, HealthKit/Health Connect sync.
- **Trial:** 7–14 days (longer trials convert better: 42.5% for 17–32 days vs 25.5% for <4 days, RevenueCat V).
- **Renewals:** tie the annual plan to the treatment cycle ("your titration year"); pre-renewal progress recap.
- **Cancellation reduction:** maintenance mode at a lower price when medication stops; pause option; export always available.
- **Why subscription is justified:** value recurs weekly through the titration and maintenance phases, but it ends with treatment — expect a natural lifetime of 10–17 months (Calc).
- **Store rules:** Apple 1.4.1 (accuracy-claim disclosure; "consult a doctor" reminders) (V); medical-device declaration required for Health & Fitness/Medical apps in EEA/UK/US from 26 Mar 2026 (V); 5.1.2(i) consent for sending photos to third-party AI (V).

---

## 7. Financial model (Calc — assumptions, not forecasts)

Blended: $9.99/mo, $49.99/yr, 65% annual → $6.20 gross ARPPU/month, $5.27 net of 15% store fee. AI ≈ $0.35/payer/month. Infra fixed $300 + $0.01/MAU. "Net" excludes marketing and salaries.

| Scenario | % MAU paying | Monthly churn | Lifetime | Net LTV/payer |
|---|---|---|---|---|
| Conservative | 3% | 10% | 10 mo | $49 |
| Moderate | 6% | 8% | 12 mo | $62 |
| Optimistic | 10% | 6% | 17 mo | $82 |

**Moderate scenario**

| MAU | Payers | MRR | Gross profit | Infra | Net before marketing |
|---|---|---|---|---|---|
| 1,000 | 60 | $372 | $295 | $310 | −$15 |
| 5,000 | 300 | $1,861 | $1,477 | $350 | $1,127 |
| 10,000 | 600 | $3,723 | $2,954 | $400 | $2,554 |
| 50,000 | 3,000 | $18,613 | $14,771 | $800 | $13,971 |
| 100,000 | 6,000 | $37,226 | $29,542 | $1,300 | $28,242 |
| 500,000 | 30,000 | $186,129 | $147,709 | $5,300 | $142,409 |

**Conservative** net before marketing at the same steps: −$162 / $389 / $1,077 / $6,585 / $13,471 / $68,555.
**Optimistic:** $182 / $2,112 / $4,524 / $23,818 / $47,936 / $240,882.

Implication: needs ~10× the audience of the trades app for the same profit, and LTV ($49–82) cannot fund paid acquisition at measured CPIs. Shotsy's claimed 100K+ payers (U) would imply roughly $0.5M+/month gross at these prices — consistent with the glp1digest estimate of ~£3.5M/yr (3P, derived) but unaudited.

**Cost stack:** same tooling as the winner (~$150–250/mo); AI photo logging via Haiku-class vision; no payments infrastructure; counsel review for health-data compliance (budget $2–5K).

---

## 8. Product blueprint

**Positioning:** "The companion for your GLP-1 journey — injections or pills, titration to maintenance — built with the community, not a weight-loss funnel."

**USP:** pill-era and international coverage (US/UK/EU names, pathways, prices), honest side-effect insights without pseudo-pharmacokinetic charts, muscle-retention focus, and a genuine off-ramp mode.

**Core functionality**
- Dose/titration calendar (injection sites with rotation; pill schedule with food/water rules); reminders
- Side-effect journal with pattern insights (what, when, severity, relation to dose changes)
- Protein/fibre/hydration targets; AI photo meal logging with protein emphasis
- Strength-training log and muscle-retention programme
- Weight/measurements/photos; trends; HealthKit/Health Connect
- Shareable progress cards (opt-in, privacy-safe)
- "Questions for your prescriber" weekly summary (PDF)
- Off-ramp/maintenance mode (dose tapering tracking as logged by the user's clinician; habit retention)
- Medication cost tracker (cash-pay prices, refill reminders)

**Premium:** insights, AI logging, programmes, exports, multi-device, buddy mode.

**Onboarding:** medication + form (injection/pill) → current dose + schedule → goals → optional HealthKit → first reminder set in <90 seconds; consent screen for AI photo processing naming the provider.

**Main screens:** Today (next dose, protein, water, how do you feel) · Journey (weight/dose timeline) · Log (food/side effects/workouts) · Insights · Community/Share · Settings.

**Expansion:** diabetes-specific mode, caregiver sharing, clinic/pharmacy white-label (B2B2C), UK/EU localisation first (less competition from US free tiers), pharmacy partnership for refill reminders.

---

## 9. Technical architecture

- Expo / React Native (New Architecture) + TypeScript; Supabase (Postgres, Auth, Storage); RevenueCat; PostHog + Sentry; Expo push.
- HealthKit (iOS) and Health Connect (Android) for weight/steps/workouts.
- AI: Claude Haiku 5.5 ($0.10/$0.50 per MTok, V) for summaries and structured side-effect insights; Sonnet 5.5 vision for meal photos; strict JSON; explicit consent (5.1.2(i)).
- Privacy: PII minimisation; data export/delete; FTC Health Breach Notification Rule and Washington My Health My Data Act apply to consumer health apps (V); HIPAA generally does not (consumer app is not a covered entity).
- **Difficulty:** low–medium. **Time to MVP:** 2–3 weeks. **Backend complexity:** low. **Platform limits:** medical-device declaration in App Store Connect; Apple 1.4.1 scrutiny of any accuracy claims. **Maintenance:** medication catalogue updates (new drugs, doses, countries).

---

## 10. Risks and red-team

1. **Free competitors have structural subsidies.** Noom, MyFitnessPal and Novo can give tracking away to feed coaching, nutrition or drug sales. A paid tracker must be *better than free* on something those players won't do (pill-era international coverage, honest side-effect analytics, off-ramp).
2. **The safe product may be undifferentiated; the differentiated product may be regulated.** Logging and reminders are generic. Personalised titration or side-effect recommendations introduce clinical risk. Medscape notes "medication level" charts use simplified, undisclosed pharmacokinetics — avoid them or disclose methodology (Apple 1.4.1).
3. **Treatment transitions cause churn.** Stopping medication, switching providers or reaching a stable routine removes the habit. "Off-ramp" is a graduation feature, not permanent retention.
4. **Incumbent success ≠ unmet need.** Shotsy's ratings prove willingness to buy *Shotsy*; a second-mover needs a segment.
5. **Founder-story growth may not repeat.** Shotsy's zero-ad-spend community growth is self-reported; assume you must earn community trust the slow way.
6. **CAC:** untenable for paid channels (≈$189/payer at 2% conversion vs $42 net first-year revenue; even $35 leaves little).
7. **Mobile web would suffice** for logging and education; native earns its keep via notifications, widgets, HealthKit/Health Connect.
8. **AI genuinely helps** with summaries and prescriber questions; unnecessary for basic tracking; hazardous if it drifts into treatment decisions.
9. **Regulatory:** Apple medical-device declaration (26 Mar 2026, V); FDA general-wellness policy revision 6 Jan 2026 — disease-specific claims, clinical thresholds and disease-management alerts can take a product outside the policy (3P law-firm summary); EU MDR / UK MHRA SaMD classification of dose logging is unresolved (U) — turns on intended purpose, so never recommend doses.
10. **Market dependence:** pricing politics (TrumpRx, NHS decisions), compounding crackdown, and drug-maker apps shape the user base.

**Red-team (GPT-6.1) verdict:** would not switch to this merely because the market is fashionable; its safety constraints and subsidised competitors are a worse fit for a small budget. It becomes preferable only with an existing trusted patient-distribution channel (clinic, pharmacy, telehealth partner, or a large community).

---

## 11. Execution outline (if pursued as app #2)

- **Weeks 1–2:** build MVP (dose calendar for pills + injections, side-effect journal, protein target, weekly summary); counsel review of health-data posture; medical-device declaration prepared.
- **Weeks 3–4:** soft-launch in UK/EU-focused communities where US free tiers are weakest; recruit 50 beta users from one subreddit/Facebook group with explicit permission from moderators; collect shareable-card feedback.
- **Months 2–3:** public launch; creator testimonials from journey-documenting users; ASO on pill-era terms; gate: ≥5% of installs paying within 35 days and month-3 retention ≥60% of payers, or stop.
- **Months 4–6:** off-ramp mode, buddy mode, pharmacy/clinic partnership pilot (B2B2C), localisation.

---

## 12. Sources

- KFF GLP-1 tracking poll (Nov 2025) https://www.kff.org (V); Gallup https://news.gallup.com/poll/712157/glp-usage-reaches-new-high.aspx (V)
- Shotsy App Store https://apps.apple.com/us/app/shotsy-glp-1-tracker/id6499510249 (V); Play https://play.google.com/store/apps/details?id=com.shotsy.app (V); Business Insider funding https://www.businessinsider.com/startup-shotsy-raises-funding-glp1-shot-tracking-app-2025-2 (V); founder interview https://glp1digest.com/p/how-shotsy-grew-to-350000-monthly (U); AppGazers https://appgazers.com/reports/apps/android-com.shotsy.app (3P); AppInsider https://appinsider.io/app/shotsy-glp-1-tracker-6499510249 (3P)
- Medscape on GLP-1 apps https://www.medscape.com/viewarticle/glp-1-apps-helpful-companions-or-false-sense-security-2026a1000i9n (V)
- Indie tracker comparison (competitor-authored) dozify.app (3P)
- Noom free companion https://www.noom.com/in-the-news/noom-launches-free-version-of-its-powerful-glp-1-companion/ (V); MyFitnessPal GLP-1 support https://news.myfitnesspal.com (V); Lose It https://loseit.zendesk.com/hc/en-us/articles/50221250242964-GLP-1-Logging (V); Novocare https://apps.apple.com/us/app/novocare/id6751852954 (V); Lilly https://zepbound.lilly.com/support-resources (V); WW https://www.weightwatchers.com/us/weight-loss-medication (V)
- Oral GLP-1s: Fierce Pharma on Wegovy pill launch (V); FDA Foundayo approval press release (fda.gov, V); TrumpRx https://trumprx.gov/p/wegovy-pill (V); LillyDirect/TrumpRx Foundayo prices via telehealthgraded.com, glp1picks.com (3P); MHRA approvals (gov.uk, V); Politico EU (V); UK private prices doseclub.co.uk (3P)
- Compounding: FDA warning letters (Fierce Pharma, V); FDA 503B proposal 30 Apr 2026 (fda.gov, V); Import Alert 66-80 (accessdata.fda.gov, V)
- Subreddit sizes: redditli.st, redpulse.io, reddifier.com, semaglutides.org (3P); GummySearch r/Semaglutide (3P)
- Regulatory: Apple App Review Guidelines https://developer.apple.com/app-store/review/guidelines/ (V); medical-device declaration https://developer.apple.com/help/app-store-connect/manage-app-information/declare-regulated-medical-device-status (V); FTC HBNR (federalregister.gov, V); Washington MHMDA RCW 19.373 (V); FDA general-wellness summary (kslaw.com, 3P); MDCG 2019-11 rev.1 and MHRA SaMD guidance 6 Nov 2026 (found, not extracted)
- Apple Ads benchmarks https://www.apptweak.com/en/aso-blog/apple-ads-benchmarks (3P); RevenueCat SOSA 2026 https://www.revenuecat.com/blog/growth/subscription-app-trends-benchmarks-2026 (V)

**Not verified:** Reddit thread text (403); IQVIA user counts; Form Health / Found / Sequence pricing; Lilly dedicated tracker; 503B exclusion final status; EU MDR / UK SaMD classification of dose logging; Shotsy's conflicting payer counts (100K vs ~117K derived).
