# GitHub → GitHub Marketplace

**Program:** GitHub Marketplace (GitHub App listing)
**Priority:** P1 · **Status:** ⛔ **blocked on engineering**
**Listing type:** Free (decided 2026-08-27) · **Blocker ticket:** [DEV-4050](https://linear.app/modem-dev/issue/DEV-4050)

> ⛔ **Blocker: the plan-change webhook is required, and a free listing does not
> avoid it.** GitHub Marketplace requires the app to handle `marketplace_purchase`
> events (purchased, changed, cancelled, pending_change). A search of
> `apps/github/src` and `packages/` finds **no handler anywhere in the repo**.
>
> This was checked against GitHub's live docs on 2026-08-27, because the free-listing
> route looked like it might sidestep it. It does not:
>
> - *"Apps must have webhook events set up to notify the publisher of any plan
>   changes or cancellations using the GitHub Marketplace API"* — stated as applying
>   to all listings, free or paid
>   ([Requirements for listing an app](https://docs.github.com/en/apps/github-marketplace/creating-apps-for-github-marketplace/requirements-for-listing-an-app))
> - *"When a customer purchases a paid plan, free trial, **or the free version** of
>   your GitHub Marketplace app, you'll receive the `marketplace_purchase` event
>   webhook with the `purchased` action"*
>   ([Handling new purchases and free trials](https://docs.github.com/en/apps/github-marketplace/using-the-github-marketplace-api-in-your-app/handling-new-purchases-and-free-trials))
>
> Free installs still generate purchase events, so the handler is needed either way.
> This is the only P1 blocker that copy cannot clear. Size it before committing to a date.

## Free vs paid — decided: free

| Option | Requirement | |
| --- | --- | --- |
| **Free listing** | Plan-change webhook + general requirements | ✅ **Chosen.** Modem bills on modem.dev via Stripe. A free listing is distribution, not billing — and it avoids publisher verification. |
| Paid listing | Publisher verification + full Marketplace billing flow | Rejected — meaningful lead time for no gain |

The free route still saves the publisher-verification lead time. It just doesn't save
the webhook.

## Requirements check

| Requirement | Status |
| --- | --- |
| Integrates beyond authentication, provides real value | ✅ Ingests issues and PRs, powers agent tools, drives automations |
| Publicly available — no invite-only or preview | ✅ `github` is unflagged in the manifest (GA by construction); docs carry no Beta tag |
| Contact information | ✅ support@modem.dev |
| Description | ✅ below |
| Pricing plan | ✅ Free |
| Privacy policy | ✅ https://modem.dev/privacy |
| Support link | ✅ https://modem.dev/contact |
| Webhook events for plan changes | ⛔ **Not implemented** — required even for free listings, see blocker |
| 2FA on the publishing account/org | ✅ Confirmed enabled on `modem-dev` (Talton, 2026-08-29). This is the GitHub org setting at [org security settings](https://github.com/organizations/modem-dev/settings/security), unrelated to Modem's own magic-link login |

## Listing form — filled

| Field | Value |
| --- | --- |
| App name | Modem |
| Publisher | modem-dev |
| Tagline | Turn GitHub issues into a triaged product backlog. |
| Categories | Project management · Support |
| Pricing | Free (Modem subscription billed separately at modem.dev) |
| Website | https://modem.dev |
| Privacy policy | https://modem.dev/privacy |
| Terms | https://modem.dev/terms |
| Support | https://modem.dev/contact |
| Documentation | https://modem.dev/docs/integrations/github |
| Installation | GitHub App install, per-repository selection |

### Short description
> Modem treats GitHub issues as user feedback and pull requests as shipping context,
> then connects both to everything your customers say elsewhere.

### Full description
> **Two jobs, one integration.**
>
> **Issues as user feedback.** Modem treats GitHub issues as public submissions —
> bug reports, feature requests, questions — and categorizes and groups them
> alongside feedback from Slack, Zendesk, Intercom, sales calls, and email. Five
> issues describing one bug become one topic.
>
> **Pull requests as shipping context.** Modem syncs PR metadata so it understands
> what your team is building. That's what lets it connect a customer complaint to
> the change that fixed it — and tell you when something a customer asked for has
> actually shipped.
>
> **Modem does not read your source code.** It syncs metadata only: issue and PR
> titles, descriptions, comments, labels, and review discussions. No file contents,
> no diffs, no repository browsing.
>
> Ask the agent "what did we ship this week that customers were asking for?" and it
> answers from GitHub, Linear, Jira, and every support channel at once.

### Permissions justification
GitHub App installation (not user OAuth). Metadata-only access:

| Permission | Why |
| --- | --- |
| Issues (read) | Issues are the feedback signal — the core of the integration |
| Pull requests (read) | PR metadata gives shipping context linking feedback to changes |
| Metadata (read) | Repository listing for the repo-selection UI |
| Webhooks | Real-time issue and PR activity |

**No `contents` permission.** Modem never reads source code. Say this prominently —
it is the single most reassuring thing on the listing.

## Assets

Core product shots now exist — see the
[shared Drive folder](https://drive.google.com/drive/folders/11j63eVbF1QA0p_Qt54n77vRkddsZSOJn)
and the tracker in `08-asset-shot-list.md` (C1, C2, C4 + Stories captured 2026-08-17;
capture and framing skills included in the folder).

- [ ] Logo, square, ≥512×512 PNG (export from brand kit; SVGs in `profile/`)
- [x] General product screenshots (topics, topic detail, people/companies — in Drive)
- [ ] **I-GITHUB shot**: GitHub issues as feedback + PRs as shipping context, side by
      side — blocked on seeding GitHub data into the MerchantRail demo org
- [ ] Feature cards / listing images at GitHub's current dimensions (crop from raws
      with the framing skill at upload time)

## Before submitting

- [ ] **Implement the `marketplace_purchase` webhook handler** — [DEV-4050](https://linear.app/modem-dev/issue/DEV-4050)
- [x] Confirm 2FA on the publishing org — confirmed enabled (Talton, 2026-08-29)
- [ ] Re-verify requirements against GitHub's live developer docs
