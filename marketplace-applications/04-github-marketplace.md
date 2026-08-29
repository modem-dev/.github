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

> ⚠️ **Open question on the free plan (found re-verifying against live docs,
> 2026-08-29):** GitHub's pricing-plans page states *"you can't list your app with a
> free pricing plan if you offer a paid service outside of GitHub Marketplace"* — and
> once a free-listed app meets the paid-app requirements, GitHub expects at least one
> paid plan. Modem bills on modem.dev via Stripe, which reads as exactly that "paid
> service outside Marketplace." Options: (a) position the GitHub App itself as free
> (the integration costs nothing; a Modem subscription is a separate product) and see
> if review accepts it — some free-with-external-SaaS listings do exist; (b) plan for
> publisher verification + a paid plan. **Decide before submitting; this could
> invalidate the free-listing strategy.**

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
| 2FA on the publishing account/org | ✅ Confirmed enabled on `modem-dev` (Talton, 2026-08-29). Note: per the live docs this is only *required* for publisher verification (paid plans / verified badge), not for a plain free listing — so we're covered either way. Unrelated to Modem's own magic-link login |
| Setup URL on the GitHub App | ⚠️ Required for Marketplace even though App settings call it optional — *"you will not be able to handle purchases"* without it. Confirm it's set |
| App identifies users via OAuth flow | ⚠️ Verify the app implements the OAuth authorization flow and provisions accounts via `GET /user/marketplace_purchases` |
| App is public + org owner submits | ⚠️ Draft listings require a public app; only an **org owner** can submit (App-manager role is not enough). Accept the Marketplace Developer Agreement at submission |

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

Image specs verified against the live docs source (2026-08-29): logo ≥200×200 (cropped
square; transparent background and no text recommended), feature-card background image
**exactly 965×482**, screenshots ≥1200px wide with one consistent aspect ratio, up to
five, content-window only (no browser chrome required by GitHub).

Ready-made files in this repo:

- [x] Logo — `assets/github/modem-logo-512.png` and `modem-logo-1024.png` (rasterized
      from the brand icon SVG; teal mark, transparent margins)
- [x] Feature card — `assets/github/feature-card-965x482.png` (brand gradient
      cover-cropped to spec; pick a light text color for the app name in the portal)
- [x] General product screenshots — `assets/product-shots/01`–`10` (framed 2304×1440
      derivatives mirrored from the
      [shared Drive folder](https://drive.google.com/drive/folders/11j63eVbF1QA0p_Qt54n77vRkddsZSOJn),
      captured 2026-08-17 against the MerchantRail demo org; capture + framing skills
      alongside)
- [ ] **I-GITHUB shot**: GitHub issues as feedback + PRs as shipping context, side by
      side — blocked on seeding GitHub data into the MerchantRail demo org

## Before submitting

- [ ] **Implement the `marketplace_purchase` webhook handler** — [DEV-4050](https://linear.app/modem-dev/issue/DEV-4050)
- [x] Confirm 2FA on the publishing org — confirmed enabled (Talton, 2026-08-29);
      per live docs only strictly required for publisher verification anyway
- [x] Re-verify requirements against GitHub's live developer docs — done 2026-08-29
      against the `github/docs` source repo (docs.github.com is egress-blocked from
      the work env). Confirmed: webhook must be configured **and active** on the
      listing before submitting; free-plan floor is handling `purchased` +
      `cancelled` (implement all five anyway — deliveries are **not retried**);
      publisher verification not needed for free. New items folded into the
      requirements table above (Setup URL, OAuth identify flow, org-owner
      submission, Developer Agreement, public app). One open flag: the
      free-plan-with-external-paid-service restriction — see the warning at the top
- [ ] Resolve the free-plan ⚠️ (free listing vs. paid service on modem.dev) before
      submitting
