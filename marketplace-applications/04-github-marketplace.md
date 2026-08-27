# GitHub → GitHub Marketplace

**Program:** GitHub Marketplace (GitHub App listing)
**Priority:** P1 · **Status:** ⛔ **blocked on engineering**

> ⛔ **Blocker found (not in the Notion audit).** GitHub Marketplace requires the app
> to **handle Marketplace webhook events for plan changes** (`marketplace_purchase`:
> purchased, changed, cancelled, pending_change). A search of `apps/github/src` and
> `packages/` finds **no `marketplace_purchase` handler anywhere in the repo**.
>
> The audit lists this as a checkbox. It is an engineering task, and it is the only
> hard blocker in the P1 set that cannot be cleared by writing copy or fixing docs.
> Size it before committing to a submission date.
>
> ⚠️ **This requirement may be avoidable.** It applies to apps *sold through* GitHub
> Marketplace. A **free** listing that bills entirely on modem.dev may not need
> Marketplace billing events at all. **Confirm against GitHub's current docs before
> building anything** — the answer decides whether this is a one-line listing or a
> sprint.

## Free vs paid — decide first

| Option | Requirement | Recommendation |
| --- | --- | --- |
| **Free listing** | General requirements only | ✅ **Recommended.** Modem bills on modem.dev via Stripe. A free GitHub listing is a distribution channel, not a billing one, and avoids publisher verification entirely. |
| Paid listing | Publisher verification + Marketplace billing flow | Adds meaningful lead time for no obvious gain |

## Requirements check

| Requirement | Status |
| --- | --- |
| Integrates beyond authentication, provides real value | ✅ Ingests issues and PRs, powers agent tools, drives automations |
| Publicly available — no invite-only or preview | ✅ `github` is unflagged in the manifest (GA by construction); docs carry no Beta tag |
| Contact information | ✅ support@modem.dev |
| Description | ✅ below |
| Pricing plan | ⚠️ Decide free vs paid (above) |
| Privacy policy | ✅ https://modem.dev/privacy |
| Support link | ✅ https://modem.dev/contact |
| Webhook events for plan changes | ⛔ **Not implemented** — see blocker |
| 2FA on the publishing account/org | ⚠️ Confirm enabled on `modem-dev` |

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

- [ ] Logo, square, ≥512×512 PNG
- [ ] Screenshots showing GitHub issues and PRs inside Modem
- [ ] Feature cards / listing images at GitHub's current dimensions

## Before submitting

- [ ] **Resolve the plan-change webhook question** — is it required for a free listing?
- [ ] Decide free vs paid
- [ ] Confirm 2FA on the publishing org
- [ ] Re-verify requirements against GitHub's live developer docs
