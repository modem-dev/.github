# Shared answer bank — reuse across every marketplace form

Every listing form asks the same ~20 questions. Fill these once; copy into each
application. Sourced from the Modem fact sheet, `apps/docs/features/security-privacy.mdx`,
`packages/common/src/billing/plans.ts`, and `packages/common/src/integrations/manifest.ts`
(read at `modem-dev/modem@09d4666`).

⚠️ = needs a human decision or confirmation before submission.

## Company

| Field | Value |
| --- | --- |
| Company name (display) | Modem |
| Legal entity name | ⚠️ **NEEDED** — forms ask for the registered entity, not the brand |
| Headquarters | Toronto, Ontario, Canada |
| Website | https://modem.dev |
| Founded / stage | Pre-seed, $4.4M led by Accel (Dan Levine), with Inovia (Taha Mubashir) |
| Company size | 5 |
| Primary contact | Ben Vinegar, CEO — ben@modem.dev |
| Technical contact | Mike Clarke, CTO |
| Support email | support@modem.dev |
| Security contact | security@modem.dev |
| Support response SLA | 2 business days (matches the commitment already made to Slack) |
| X / Twitter | https://x.com/modemdev |
| Discord | https://discord.gg/WZFjaP6Gt8 |

## URLs

| Field | Value |
| --- | --- |
| Marketing site | https://modem.dev |
| Documentation | https://modem.dev/docs |
| Integrations overview | https://modem.dev/docs/integrations/overview |
| Privacy policy | https://modem.dev/privacy |
| Terms of service | https://modem.dev/terms |
| Security page | https://modem.dev/security |
| Contact | https://modem.dev/contact |
| Support page | ⚠️ Confirm a **public, no-login** support page exists. Slack's review flagged this as unverified and it was never closed out. |

## Positioning copy

**One-liner (≤10 words)**
> Turn scattered user feedback into a triaged product backlog.

**One sentence**
> Modem is an AI product teammate that helps software teams handle triage,
> tickets, and follow-ups so they can ship faster.

**Short description (~50 words)**
> Modem captures every piece of customer feedback your team receives — support
> tickets, group chat, GitHub issues, sales calls, email — and triages it
> automatically. Related reports are grouped into topics, linked to the people and
> companies who raised them, and turned into tickets with real context.

**Long description (~150 words)**
> Product feedback arrives everywhere: a Slack thread, a Zendesk ticket, a GitHub
> issue, a line in a sales call. It rarely arrives as a backlog. Teams ship faster
> than ever and still lose time to the work around the code — reading, sorting,
> deduplicating, and chasing follow-ups.
>
> Modem connects to the tools your team already uses and does that work
> continuously. It groups related feedback into topics, classifies each report
> (bug, feature request, praise, complaint), and links every one back to the person
> and company who raised it. When you're ready to act, Modem creates the ticket
> with the full evidence trail attached. When you ship, it helps you close the loop
> with the people who asked.
>
> The result: engineers and coding agents execute instead of waiting on a PM to
> tell them what matters.

**Category** — Product management / Developer tools / Customer feedback
(pick the closest per marketplace; prefer "Integrations" or "Productivity" where offered)

## Pricing (current as of 2026-08, from `plans.ts`)

| Plan | Price | Events/mo | Credits/mo | Retention | Seats |
| --- | --- | --- | --- | --- | --- |
| Basic | $0 | 2,500 | 1,000 | 30 days | Unlimited |
| Startup | $80/mo | 15,000 | 10,000 | 180 days | Unlimited |
| Scale | $250/mo | 60,000 | highest | 365 days | Unlimited |
| Enterprise | Custom | Unlimited | Unlimited | Unlimited | Unlimited |

- **Not per-seat.** Every plan allows unlimited users. Say this explicitly — it is a
  differentiator and several forms ask for a per-user price.
- **14-day free trial** at Scale limits, no credit card.
- DSL ($144) and Cable ($560) are **legacy and grandfathered** — hidden from new
  customers and rejected at checkout. Do not list them.
- ⚠️ The Notion audit and the June 2026 review both quote the old Dial-Up/DSL/Cable
  ladder. That pricing is stale; use the table above.

## Security & data handling (answers to the questionnaire sections)

- **Encryption in transit:** TLS 1.2+ everywhere.
- **Encryption at rest:** all customer data encrypted at rest. OAuth tokens are
  encrypted with AES-256-GCM using per-token initialization vectors.
- **Tenant isolation:** application-level ORM wrapper enforces organization-scoped
  filtering; PostgreSQL Row-Level Security provides a second enforcement layer at
  the database.
- **Webhook verification:** inbound webhooks verified with HMAC-SHA256 signature
  checks using constant-time comparison.
- **Media handling:** proxied images/files use HMAC-SHA256 signed URLs with
  time-limited expiry; source URLs are never exposed to the browser.
- **Access control:** production access requires MFA and is logged; employees access
  customer data only against a documented business need.
- **Testing:** quarterly vulnerability scans on public-facing systems; annual
  third-party penetration tests.
- **Third-party sharing:** none. Data is not sold or shared for third-party purposes;
  only sub-processors necessary to operate Modem.
- **Retention:** data retained while the organization exists. Deleting an
  organization purges production data; backups purged within 90 days and never
  restored.
- **Deletion requests:** support@modem.dev, subject "Data deletion request".
  Requester authorization verified within 2 business days, deletion completed within
  3 business days of verification, written confirmation of what was deleted.
- **Compliance:** ⚠️ SOC 2 Type II is **in progress, not certified**. Say "pursuing
  SOC 2 Type II" — do not imply certification on any form.
- **Vulnerability disclosure:** security@modem.dev, safe harbour for good-faith
  researchers.

## AI disclosures (asked by Slack, Intercom, Atlassian, Zendesk)

- Modem uses large language models to classify, summarize, and group feedback, and
  to power an agent chat surface.
- ⚠️ **Model vendor and versions must be named** on most forms. Fill in the current
  production model list before submitting.
- Users are shown that responses are AI-generated. ⚠️ Slack's review asked for an
  "AI responses may be inaccurate" disclaimer wherever AI output appears —
  confirm this shipped before repeating the claim.
- Ingested third-party data is processed for topic extraction and analysis. It is
  **not** exported, resold, or used to train third-party models.
- ⚠️ Confirm the current position on customer data and model training, and state it
  identically on every form.

## Assets needed (shared across all listings)

| Asset | Status |
| --- | --- |
| App icon / logo, square, high-res | ✅ `profile/logo-light.svg`, `profile/logo-dark.svg` in this repo — ⚠️ needs raster export at each marketplace's required size |
| Screenshots, 1600×1000 (8:5) | ❌ Not created. Required by Slack, Atlassian, Zendesk, Intercom |
| Demo video, 30–90s, captioned, YouTube | ❌ Not created. Required by Slack; strongly recommended elsewhere |
| Per-integration screenshots | ❌ Each marketplace wants screenshots showing *their* product inside Modem |

The screenshots and video are the single largest blocker across the whole set. Nothing
in P1 can be submitted without them.
