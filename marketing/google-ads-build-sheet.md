# Google Ads Restructure — Build Sheet

**Owner:** talton@modem.dev · **Date:** 2026-08-28 · **Status:** ready to work through in the console

Work top to bottom. Each section is one console task. Est. total time: ~90 min.

## Why this restructure (context)

- 45 days, 13 keywords, ~61 sessions, **0 activated users**. The 4 signups were junk (click-farm pattern on `signup_started`, a CTA-click event).
- No conversion data exists to optimize against, so we optimize against the best measured proxies (Aug 3 analysis):
  - **≥3 pageviews in a session** — 5.6% precision, 5.7× lift
  - **Viewed /pricing** — 3.2% precision, 3.2× lift
- ~90% of spend sits on navigational + category terms. Job-to-be-done and comparison terms — where the content investment went — get zero spend.
- The swap: **kill Tier 4 (navigational), shrink Tier 3 (category), build Tiers 1–2 (job-to-be-done + comparison)**, one ad group per lander.

## Scoreboard (what "working" means)

Success in the next 30 days is **not signups**. It is:

| Metric | Baseline (45d) | Target (30d) |
|---|---|---|
| Sessions with ≥3 pageviews | 5 | ≥8 |
| /pricing views from ads | 2 | ≥5 |
| Spend on Tier 1+2 | ~0% | ≥70% |

---

## Task 0 — GATE: onboarding fix ships first

Free-email signups stall silently at 21.5% (vs 11.2% work email — Jul 6 finding). Cold ad traffic is overwhelmingly personal Gmail. **Do not raise spend until this is fixed**; the restructure below can be built and left paused, but launch is gated on the onboarding fix.

- [ ] Onboarding fix for free-email signups deployed and verified
- [ ] Then, and only then, enable the new campaigns

## Task 1 — Account-level settings

- [ ] **Bidding:** Manual CPC everywhere. No conversion-based bidding until there are ≥30 real conversions to learn from.
- [ ] **Conversion event:** remove `signup_started` (CTA click — click-farm bait) as the account conversion. Create two new conversion actions from analytics imports:
  - `pricing_view` (primary — optimize/report against this)
  - `engaged_session` (≥3 pageviews; secondary/observational)
- [ ] **Networks:** Search only. Uncheck Display Network and Search Partners on every campaign.
- [ ] **Location:** exact targeting ("presence" not "presence or interest").

## Task 2 — Negative keyword list (apply account-wide today)

Create shared negative list `nav-and-junk`, apply to all campaigns:

```
[claude skills]
[claude code skills]
[agent skills]
"skills"
[claude code]
[claude]
[cursor]
[cursor ai]
"free"
"jobs"
"course"
"tutorial pdf"
```

Rationale: navigational terms for other people's products bought us 36 sessions that read one page, and the two junk signups landed through them.

## Task 3 — Pause / kill existing structure

- [ ] **Kill Tier 4 (navigational):** pause every keyword targeting someone else's product name — TODO(list actual account keywords from PostHog pull)
- [ ] **Shrink Tier 3 (category):** keep at most 2 category keywords, phrase match, with a shared low budget cap — TODO(actual keywords)
- [ ] Pause everything else in the legacy ad groups rather than deleting — keeps history readable.

## Task 4 — New campaign structure

One campaign, 3–4 ad groups, **one ad group per lander**, total budget unchanged (~$15/day). Concentration beats coverage: 13 keywords at this budget = 2–3 sessions/day spread too thin to ever read.

TODO(fill from lander inventory + keyword data):

### Ad group 1 — Tier 1: feedback → Linear (JTBD)
### Ad group 2 — Tier 1: feedback MCP / agent context (JTBD)
### Ad group 3 — Tier 2: Productboard alternative (comparison)
### Ad group 4 — Tier 2: Enterpret / Canny (comparison)

For each: keywords (phrase + exact only — no broad match anywhere), final URL = the matching guide/comparison page (not the homepage), 2 RSAs mirroring the query language.

## Task 5 — Tracking

- [ ] Every final URL tagged: `utm_source=google&utm_medium=cpc&utm_campaign={campaign}&utm_term={keyword}&utm_content={adgroup}`
- [ ] Verify `utm_term` lands on PostHog sessions (it's the join key for the scoreboard).

## Task 6 — Weekly review loop

Every Monday, 15 min:
1. PostHog: ad sessions by `utm_term` → sessions, ≥3-page sessions, pricing views.
2. Search terms report: add junk queries to `nav-and-junk`.
3. A keyword with 10+ clicks and zero engaged sessions gets paused. A keyword with an engaged session gets its bid nudged +20%.
4. Do **not** add keywords or switch bidding strategy for 30 days. Let it read.
