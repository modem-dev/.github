# Integration marketplace applications

Filled application drafts for the marketplaces identified in
[Integration Marketplace Audit — All 25](https://app.notion.com/p/3c92c5842de08178b4e7e8dfb2b11d9e).

Each file is the vendor's actual form with Modem's answers filled in. Copy the values
into the portal. `⚠️` marks a field needing a human decision; `⛔` marks a hard blocker.

Facts were read from `modem-dev/modem@09d4666` (integration manifest, billing plans,
OAuth scope constants, published docs) rather than the June 2026 review, which is
eight months old and has already proven stale.

## Status

| # | Marketplace | Priority | Status |
| --- | --- | --- | --- |
| [06](06-linear-integration-directory.md) | Linear Integration Directory | P2 | ✅ **Send today** — email drafted, only assets missing |
| [05](05-notion-integration-gallery.md) | Notion Integration Gallery | P2 | ✅ Copy complete; one token-refresh answer to prepare |
| [01](01-jira-atlassian-marketplace.md) | Atlassian Marketplace | P1 | ✅ Ready once assets exist; one scope decision |
| [02](02-intercom-app-store.md) | Intercom App Store | P1 | ✅ Ready once assets exist — full-access app |
| [07](07-gong-collective.md) | Gong Collective | P2 | ✅ Ready once assets exist; confirm program with Gong |
| [03](03-zendesk-marketplace.md) | Zendesk Marketplace | P1 | ⛔ [DEV-2653](https://linear.app/modem-dev/issue/DEV-2653) — small, stalled in Backlog since May |
| [04](04-github-marketplace.md) | GitHub Marketplace | P1 | ⛔ [DEV-4050](https://linear.app/modem-dev/issue/DEV-4050) — `marketplace_purchase` handler |
| [08](08-asset-shot-list.md) | *Asset shot list* | — | 📸 The critical path for all seven |

Not drafted: **Salesforce/AppExchange** — the audit correctly re-scoped it to a
listing-type decision, not a form. Nothing to fill until that question is answered.
**Sentry** is already in a publishing review. P3/P4 are queued or skipped per the audit.

## Decisions taken 2026-08-27

- **Submit with the Beta doc labels in place.** Not a blocker — see below.
- **Intercom: list the full-access OAuth app**, not the approved read-only one.
- **GitHub: free listing.** Avoids publisher verification. Does *not* avoid the webhook.

## Findings

**1. GitHub's plan-change webhook is required, and a free listing doesn't avoid it.**
Filed as [DEV-4050](https://linear.app/modem-dev/issue/DEV-4050).
No `marketplace_purchase` handler exists anywhere in the repo. Checked against
GitHub's live docs: the requirement is stated as applying to all listings, free or
paid, and `marketplace_purchase` fires on *"the free version"* too
([requirements](https://docs.github.com/en/apps/github-marketplace/creating-apps-for-github-marketplace/requirements-for-listing-an-app),
[purchase events](https://docs.github.com/en/apps/github-marketplace/using-the-github-marketplace-api-in-your-app/handling-new-purchases-and-free-trials)).
The audit carries this as a checkbox. It is the only P1 blocker copy cannot clear.

**2. Pricing in the audit is stale.** Current plans are Basic $0 / Startup $80 /
Scale $250. Dial-Up, DSL ($144), and Cable ($560) are legacy and grandfathered — DSL
and Cable are hidden from new customers and rejected at checkout. Gong additionally
requires Scale, so its pricing answer differs from every other form here.

**3. Three integrations are documented as Beta while being GA in code — cosmetic.**
`jira.mdx`, `zendesk.mdx`, and `gong.mdx` carry `tag: 'Beta'` plus an inline warning,
and `overview.mdx:186` says Beta integrations are "enabled per organization rather
than being available to everyone." All three are `featureFlag: null` in the manifest.

I initially called this a submission blocker on the grounds that GitHub Marketplace
rejects apps that aren't publicly available. **That was wrong** — `github.mdx` carries
no Beta tag, and GitHub reviews the GitHub app, not the Jira/Zendesk/Gong pages. None
of Atlassian, Zendesk, or Gong has a no-beta rule. Submitting as-is.

Still worth fixing on the docs backlog: a buyer who clicks from a listing into docs
saying "features and behavior may change" is less likely to install. Conversion nit,
not a launch dependency.

## The real critical path

**Assets.** No marketplace in this set accepts a submission without screenshots, and
Slack also required a 30–90s captioned demo video. None exist. Both are reusable
across all seven listings, and both block everything except the Linear email.

Full capture spec, per-marketplace dimensions, and a video beat sheet:
**[08-asset-shot-list.md](08-asset-shot-list.md)**.

1. Produce screenshots + demo video per the shot list (unblocks everything)
2. Send the Linear email — fastest listing, existing relationship
3. Submit Notion (5–10 business day review clock, start it early)
4. Submit Jira, Intercom, and Gong
5. Zendesk once the request-headers issue closes
6. GitHub once the `marketplace_purchase` handler ships

## Open questions

Still needed before the affected forms can go out.

1. **Legal entity name.** Every form asks for the registered entity, not "Modem".
2. **Zendesk: is attachment ingest required at launch?** Global `read` is only needed
   for attachments. Dropping to `tickets:read` would materially de-risk that review.
3. **Jira: keep `write:servicedesk-request`?** Requested but unused — Atlassian
   challenges unused scopes.
4. **AI model disclosure.** Several forms require naming model vendors and versions,
   and stating the position on customer data and model training. Needs one answer used
   consistently everywhere.
5. **Data residency.** Atlassian asks where customer data is stored.
6. **Which positioning do the listings lead with?** The live homepage reads "Product
   execution for the AI era"; the drafts use the February fact sheet's "AI product
   teammate"; the GitHub org README says "auto-triage Product Manager". Three live
   positionings. Pick one — it's a find-and-replace, not a rewrite. Detail in the shot list.
7. **Public support page.** Slack's review flagged this as unverified and it was never
   closed out. Several forms require a no-login support page.
8. **Did the Slack AI disclaimers ship?** Slack's review asked for an "AI responses may
   be inaccurate" disclaimer wherever AI output appears. Other marketplaces ask the same
   question, and the answer should be true before it's given.

## Spot-check: do listings already exist?

The audit flags this as an open item — absence was inferred, never confirmed. Checked
2026-08-27. **Caveat: both marketplace search pages are blocked by this environment's
egress proxy, so these are web-search results, not direct portal checks.** Treat as
supporting evidence, not proof. Someone should confirm in the portals.

| Marketplace | Result |
| --- | --- |
| Atlassian | No Modem listing surfaced. Consistent with "not submitted". |
| Stripe | No Modem listing surfaced. |

On **Stripe** specifically: `stripe/router.ts:51` says *"The app is published, so every
org installs through the public marketplace authorize URL."* Read alongside a search
that finds no listing, the likely reconciliation is that the Stripe **OAuth app** is
published — which is what makes the public authorize URL work — while no **Marketplace
listing** exists. Those are different things and the code comment only evidences the
first. Worth five minutes in the Stripe dashboard to settle, but it no longer looks
like the audit is wrong here.

What did surface in search: `modem.dev/integrations` is live and indexed, as is
`modem.dev/ai-product-teammate`. Both are usable as listing URLs.
