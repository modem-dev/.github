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
| [06](06-linear-integration-directory.md) | Linear Integration Directory | P2 | ✅ **Send today** — email is drafted, only assets missing |
| [05](05-notion-integration-gallery.md) | Notion Integration Gallery | P2 | ✅ Copy complete; one token-refresh answer to prepare |
| [01](01-jira-atlassian-marketplace.md) | Atlassian Marketplace | P1 | 🚧 Docs de-beta + one scope decision |
| [02](02-intercom-app-store.md) | Intercom App Store | P1 | ❓ Blocked on a decision: which OAuth app to list |
| [07](07-gong-collective.md) | Gong Collective | P2 | 🚧 Docs de-beta; confirm program with Gong directly |
| [03](03-zendesk-marketplace.md) | Zendesk Marketplace | P1 | ⛔ Request-headers issue + docs de-beta |
| [04](04-github-marketplace.md) | GitHub Marketplace | P1 | ⛔ Plan-change webhook not implemented |

Not drafted: **Salesforce/AppExchange** — the audit correctly re-scoped it to a
listing-type decision, not a form. Nothing to fill until that question is answered.
**Sentry** is already in a publishing review. P3/P4 are queued or skipped per the audit.

## Three findings that change the plan

**1. Three integrations are publicly documented as Beta while being GA in code.**
`jira.mdx`, `zendesk.mdx`, and `gong.mdx` all carry `tag: 'Beta'` plus an inline
warning, and `overview.mdx:186` tells readers Beta integrations are "enabled per
organization rather than being available to everyone." All three have
`featureFlag: null` in the manifest — they serve to everyone.

This matters because reviewers read the public docs. GitHub Marketplace explicitly
rejects apps that aren't publicly available, and Atlassian, Zendesk, and Gong will all
read "not available to everyone" as limited release. DEV-3748 checked the overview
cards and found them accurate; it did not check the per-page frontmatter tags.

It's a stale-docs fix, not engineering — and it unblocks three of seven listings.

**2. GitHub Marketplace's plan-change webhook is not implemented.**
No `marketplace_purchase` handler exists anywhere in the repo. The audit carries this
as a checkbox; it's the only P1 blocker that copy and docs can't clear. It may be
avoidable entirely with a free listing — worth confirming before building anything.

**3. Pricing in the audit is stale.** Current plans are Basic $0 / Startup $80 /
Scale $250. Dial-Up, DSL ($144), and Cable ($560) are legacy and grandfathered — DSL
and Cable are hidden from new customers and rejected at checkout. Gong additionally
requires Scale, so its pricing answer differs from every other form here.

## The real critical path

Not the P1/P2 ordering. It's **assets** — no marketplace in this set accepts a
submission without screenshots, and Slack also required a 30–90s captioned demo video.
None exist. Both are reusable across all seven listings, and both block everything
except the Linear email.

Suggested order:
1. Produce screenshots + demo video (unblocks everything)
2. Send the Linear email — fastest listing, existing relationship
3. Fix the three Beta doc tags — one small PR, unblocks Jira, Zendesk, Gong
4. Submit Notion (5–10 business day clock, start it early)
5. Resolve the Intercom OAuth-app decision, then submit
6. Submit Jira and Gong
7. Zendesk and GitHub once their blockers clear

## Open questions

These need answers before the affected forms can be submitted.

1. **Legal entity name.** Every form asks for the registered entity, not "Modem".
2. **Intercom: which OAuth app do we list** — the approved read-only one, or the
   full-access one? Listing read-only would undercut the "bidirectional integration"
   rationale that made Intercom a P1.
3. **GitHub: free or paid listing?** Free avoids publisher verification and probably
   the billing webhook. Recommend free.
4. **Zendesk: is attachment ingest required at launch?** Global `read` is only needed
   for attachments. Dropping to `tickets:read` would materially de-risk that review.
5. **Jira: keep `write:servicedesk-request`?** It's requested but unused — Atlassian
   challenges unused scopes.
6. **AI model disclosure.** Several forms require naming model vendors and versions,
   and stating the position on customer data and model training. Needs one answer used
   consistently everywhere.
7. **Data residency.** Atlassian asks where customer data is stored.
8. **Public support page.** Slack's review flagged that this was never verified. Several
   forms require a no-login support page.
9. **Did the Slack AI disclaimers ship?** Slack's review asked for an "AI responses may
   be inaccurate" disclaimer wherever AI output appears. Other marketplaces ask the same
   question, and the answer should be true before it's given.

## Also worth a look

The audit lists **Stripe** as P4 "listable", but `stripe/router.ts:51` says *"The app
is published, so every org installs through the public marketplace authorize URL."*
Modem may already have a live Stripe Marketplace listing. Worth checking before anyone
spends an afternoon on it — and it means the audit's "not submitted" statuses are
unreliable in at least one direction, which is exactly what its own open item warned.
