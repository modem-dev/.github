# Google Ads Restructure — Build Sheet

**Owner:** talton@modem.dev · **Date:** 2026-08-28 · **Status:** ready to work through in the console

Work top to bottom. Each section is one console task. Est. total time: ~90 min.

## Why this restructure (context)

- 45 days (Jul 14–Aug 28), **19 named keywords + 1 keywordless DSA/PMax bucket, 83 sessions** (`utm_source=google, utm_medium=cpc` in PostHog), **0 activated users**. The 4 signups were junk (`claude code` ×2, `cursor` ×1, `ai code assistant` ×1 — click-farm pattern).
- No conversion data exists to optimize against, so we optimize against the best measured proxies (Aug 3 analysis):
  - **≥3 pageviews in a session** — 5.6% precision, 5.7× lift
  - **Viewed /pricing** — 3.2% precision, 3.2× lift
- ~90% of spend sits on navigational + category terms. Job-to-be-done and comparison terms — where the content investment went — get zero spend.
- The swap: **kill Tier 4 (navigational), shrink Tier 3 (category), build Tiers 1–2 (job-to-be-done + comparison)**, one ad group per lander.

## Scoreboard (what "working" means)

Success in the next 30 days is **not signups**. It is:

| Metric | Baseline (45d, PostHog-verified) | Target (30d) |
|---|---|---|
| Sessions with ≥3 pageviews | 4 | ≥8 |
| Sessions viewing /pricing | 4 | ≥8 |
| Spend on Tier 1+2 | ~0% | ≥70% |

PostHog definitions (join key is `$entry_utm_term` on the `sessions` table): engaged session = `$pageview_count >= 3`; pricing view = any `/pricing` URL in the session's `$urls`; signup = `user_signed_up` event joined via `$session_id`.

---

## Task 0 — GATE: onboarding fix ships first

Free-email signups stall silently at 21.5% (vs 11.2% work email — Jul 6 finding). Cold ad traffic is overwhelmingly personal Gmail. **Do not raise spend until this is fixed**; the restructure below can be built and left paused, but launch is gated on the onboarding fix.

- [ ] Onboarding fix for free-email signups deployed and verified
- [ ] Then, and only then, enable the new campaigns

## Task 1 — Account-level settings

- [ ] **Bidding:** Manual CPC everywhere. No conversion-based bidding until there are ≥30 real conversions to learn from.
- [ ] **Conversion event:** remove the CTA-click conversion (click-farm bait) as the account conversion. Note: the real PostHog signup event is `user_signed_up` — `signup_started` does not exist in the taxonomy; check what the Google Ads conversion action is actually wired to. Create two new conversion actions:
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
"code assistant"
"coding assistant"
"free"
"jobs"
"course"
"tutorial pdf"
```

Rationale: navigational terms for other people's products bought us 36 sessions that read one page, and all 4 junk signups arrived through them (`claude code` ×2, `cursor`, `ai code assistant`).

## Task 3 — Pause / kill existing structure

Actual account keywords, 45-day performance from PostHog (`$entry_utm_term`):

**Kill — Tier 4 navigational (36 sessions, 0 pricing views, all 3 junk-signup keywords):**

| Keyword | Sessions | ≥3-pg | Pricing | Action |
|---|---|---|---|---|
| claude code | 15 | 2 | 0 | pause (2 junk signups) |
| claude skills | 12 | 0 | 0 | pause |
| cursor | 6 | 1 | 0 | pause (1 junk signup) |
| claude code skills | 2 | 0 | 0 | pause |
| cursor ai | 1 | 0 | 0 | pause |
| ai code assistant | 1 | 0 | 0 | pause (1 junk signup) |
| ai coding assistant | 1 | 0 | 0 | pause |

**Kill — DSA/PMax bucket:** campaign `search-ca-aitools-2026q3` produces keywordless sessions (6 in 45d, all landing on `/unfair-advantage`, 0 engaged, 0 pricing). Pause it — unattributable exploration spend on this budget.

**Shrink — Tier 3 category (keep the 2 that produced signal, pause the rest):**

| Keyword | Sessions | ≥3-pg | Pricing | Action |
|---|---|---|---|---|
| ai product management tool | 4 | 1 | 1 | **keep** — best keyword in the account (13 pageviews on 4 sessions) |
| product feedback tool | 3 | 0 | 1 | **keep** |
| customer feedback software | 7 | 0 | 0 | pause |
| conversation intelligence software | 6 | 0 | 1 | pause — 1 pricing view but expensive CPC territory; revisit if Tier 1–2 underdelivers |
| user feedback software | 4 | 0 | 0 | pause |
| customer insights software | 4 | 0 | 0 | pause |
| sales call insights software | 1 | 0 | 0 | pause |
| product discovery tool | 1 | 0 | 0 | pause |

**Fold into Tier 1 (already JTBD-shaped — move, don't kill):** `context for ai agents` (1 pricing view), `mcp context server`, `ai agent context`, `ai agent memory` → these move into the Tier 1 ad groups below with proper landers instead of `/unfair-advantage`.

- [ ] Pause (don't delete) everything marked pause — keeps history readable.

## Task 4 — New campaign structure

One campaign (`search-tiered-2026q3`), 4 ad groups + 1 legacy holdover, **one ad group per lander**, total budget unchanged. Concentration beats coverage: 19 keywords at this budget = 2–3 sessions/day spread too thin to ever read.

All keywords **phrase + exact only — no broad match anywhere**. Final URLs are PostHog-confirmed live pages. Append tracking template from Task 5 to every final URL.

### Ad group 1 — `feedback-mcp-server` (Tier 1) — ~25% of budget

**Final URL:** `https://modem.dev/guides/best-mcp-servers-for-customer-feedback`

| Keyword | Match |
|---|---|
| customer feedback mcp server | phrase + exact |
| mcp server for customer feedback | exact |
| feedback mcp server | phrase |
| mcp context server | exact *(moved from legacy — had 1 session on `/missing-context`)* |

RSA angles: H "MCP Server for Customer Feedback" / "Give Your Agents Customer Context" / "Feedback, Triaged for Claude & Cursor" · D "Pipe every ticket, thread, and issue into your coding agent via MCP. Set up in minutes."

### Ad group 2 — `feedback-to-coding-agents` (Tier 1) — ~25% of budget

**Final URL:** `https://modem.dev/guides/best-tools-route-feedback-to-coding-agents`

| Keyword | Match |
|---|---|
| route customer feedback to coding agents | phrase |
| send customer feedback to coding agent | phrase |
| customer feedback for ai agents | phrase |
| context for ai agents | phrase + exact *(moved — 1 pricing view in 45d)* |
| ai agent context | exact *(moved)* |
| ai agent memory | exact *(moved)* |
| auto triage customer feedback | phrase *(lander alt: `/guides/best-ai-triage-tools-for-engineering-teams` — split into its own ad group in phase 2 if it gets clicks)* |

RSA angles: H "Route Feedback to Your Coding Agents" / "Auto-Triage Customer Feedback" / "From Support Ticket to Agent Task" · D "Modem captures feedback from chat, tickets, and GitHub — triaged and ready for agents to execute."

### Ad group 3 — `productboard-alternative` (Tier 2) — ~20% of budget

**Final URL:** `https://modem.dev/productboard-alternative`

| Keyword | Match |
|---|---|
| productboard alternative | phrase + exact |
| productboard alternatives | exact |
| productboard competitors | exact |
| productboard vs | phrase |

RSA angles: H "The Productboard Alternative for Devs" / "Feedback Triage Without the PM Overhead" · D "Auto-triage feedback straight to Linear and your coding agents. See why teams switch."

### Ad group 4 — `canny-alternative` (Tier 2) — ~20% of budget

**Final URL:** `https://modem.dev/canny-alternative` *(most-visited comparison page — 11 views)*

| Keyword | Match |
|---|---|
| canny alternative | phrase + exact |
| canny alternatives | exact |
| canny vs productboard | exact *(lander alt: none live yet — the vs-pages have no traffic; point at `/canny-alternative` until a vs page is confirmed)* |

RSA angles: H "Canny Alternative for Dev Teams" / "Beyond the Feedback Board" · D "Feedback boards collect; Modem triages. Every request routed, deduped, and agent-ready."

### Ad group 5 — `category-survivors` (Tier 3 holdover) — ~10% of budget, bid-capped

The two legacy keywords that produced signal, kept on their existing landers:

| Keyword | Match | Final URL |
|---|---|---|
| ai product management tool | phrase + exact | `https://modem.dev/ai-product-manager` |
| product feedback tool | exact | `https://modem.dev/guides/which-feedback-tool-for-which-bottleneck` *(upgrade from `/modem-for-discord`, which produced 0 engagement on 3 sessions)* |

### Phase 2 bench (add only by swapping out a 30-day loser)

Confirmed-live comparison landers with no ad group yet: `/enterpret-alternative`, `/buildbetter-alternative`, `/pylon-alternative`, `/unwrap-alternative`, `/pendo-alternative`, `/feedback-board-alternative`. Each is a ready-made ad group on the Tier 2 pattern above.

## Task 5 — Tracking

- [ ] Every final URL tagged: `utm_source=google&utm_medium=cpc&utm_campaign={campaign}&utm_term={keyword}&utm_content={adgroup}`
- [x] `utm_term` capture verified working — PostHog `sessions` table records it as `$entry_utm_term` (19 keywords currently attributed; only DSA/PMax traffic lacks it, and that campaign is being killed in Task 3).

## Task 6 — Weekly review loop

Every Monday, 15 min:
1. PostHog: ad sessions by `utm_term` → sessions, ≥3-page sessions, pricing views.
2. Search terms report: add junk queries to `nav-and-junk`.
3. A keyword with 10+ clicks and zero engaged sessions gets paused. A keyword with an engaged session gets its bid nudged +20%.
4. Do **not** add keywords or switch bidding strategy for 30 days. Let it read.

---

## Appendix — data provenance & open items

- Keyword and session data: PostHog `sessions` table, Jul 14–Aug 28 2026, filter `$entry_utm_source='google' AND $entry_utm_medium='cpc'` (83 sessions — includes the 6-session DSA bucket; the earlier ~61 figure likely excluded it).
- Lander inventory: enumerated from PostHog `$pageview` pathnames (modem.dev is egress-blocked from the analysis environment, so the sitemap couldn't be fetched). **Only pages with ≥1 recorded pageview are listed** — roughly 21 guides, 1 alternative page, and 3 vs pages exist but have zero traffic and couldn't be confirmed. Before launch, sanity-check each final URL loads.
- The only live vs-style page found is `/modem-vs-claude-tag`; no competitor-vs-competitor pages (e.g. canny-vs-productboard) have traffic yet. If those pages are live, they're better final URLs for the vs-keywords than the alternative pages.
- Junk-signup spot check pending: 4 `user_signed_up` events from ad sessions (`claude code` ×2, `cursor`, `ai code assistant`) — confirm these are the known junk accounts before treating navigational as strictly zero-value.
