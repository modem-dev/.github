# Zendesk → Zendesk Marketplace

**Program:** Zendesk Marketplace
**Priority:** P1 · **Status:** ⛔ **blocked — do not submit yet**

> ⛔ **Blocker — the only one.** [DEV-2653](https://linear.app/modem-dev/issue/DEV-2653) (Backlog since 2026-05-27, unstarted): Modem must send Zendesk Marketplace
> request headers on outbound calls. Zendesk requires this before it will list.
>
> 📝 **Docs say Beta; not treating it as a blocker.** `zendesk.mdx` carries
> `tag: 'Beta'` while the manifest says `featureFlag: null` (GA). Zendesk has no
> no-beta rule, so we submit as-is once the request-headers issue clears
> (decision, 2026-08-27). Worth fixing on the docs backlog for conversion reasons.
>
> Copy below is drafted now because the character limits are tight and the audit
> explicitly says to draft them early rather than at submission time.

## Copy — within Zendesk's limits

| Field | Limit | Draft | Length |
| --- | --- | --- | --- |
| Title | ≤40 | `Modem` | 5 |
| Summary | ≤80 | `Turn support tickets into a triaged product backlog.` | 52 |

Alternate summaries, all within 80:
- `Every support ticket, grouped into topics and linked to the customer.` (69)
- `Support tickets as product signals, not just a queue.` (53)

### Long description
> Zendesk tickets are some of the richest product signals a team gets — real
> customers describing real problems in their own words. They usually stay in
> support, separate from what's discussed in Slack, reported on GitHub, or raised on
> a sales call.
>
> Modem captures ticket activity as it happens — public replies, internal notes,
> priority, tags — and lands it in the same topics your team already uses for
> feedback. One topic can hold the Zendesk ticket, the Slack thread about it, the
> GitHub issue, and the Linear issue that closed it.
>
> Then you ask. "Any open Zendesk tickets about dark mode? Summarize what customers
> reported and how we responded." Modem reads across every connected source and
> tells you whether it's new or already handled.

## Required data disclosure — what Zendesk data is accessed and why

OAuth scope requested: `read tickets:write webhooks:write`

| Scope | Why |
| --- | --- |
| `read` (global) | Ticket conversations, comments, and metadata are the integration's entire purpose. Global `read` rather than granular `tickets:read` because **attachment downloads 403 under the granular scope** — the granular scope does not cover attachment content (`packages/api/src/utils/zendesk-client.ts:31`). |
| `tickets:write` | Reserved for agent-initiated ticket updates |
| `webhooks:write` | Register the webhooks that deliver real-time ticket activity |

> ⚠️ Global `read` is the scope Zendesk reviewers scrutinize hardest, for the same
> reason Slack pushed back on broad history access. The attachment justification is
> real and documented in code — lead with it. If attachment ingest is not actually
> required for launch, dropping to `tickets:read` would materially de-risk the review.
> **This is a product decision worth making before submitting.**

| Data | Why |
| --- | --- |
| Ticket comments (public + internal) | Core analysis — grouping feedback into topics |
| Ticket metadata (status, priority, tags) | Classification and prioritization |
| Requester identity | Link reports to people and companies |
| Attachments | Screenshots and logs are often the substance of a bug report |

Data is processed for topic extraction and analysis. It is not exported or backed up.

## Packaging requirements

- [ ] Package as a zip: `manifest.json` + `translations/en.json`
- [ ] Authenticate with global OAuth tokens
- [ ] Meet Zendesk branding requirements
- [ ] Logo assets at Zendesk's required dimensions

## Listing metadata

| Field | Value |
| --- | --- |
| Company | Modem |
| Website | https://modem.dev |
| Privacy policy | https://modem.dev/privacy |
| Terms | https://modem.dev/terms |
| Support | support@modem.dev |
| Documentation | https://modem.dev/docs/integrations/zendesk |
| Pricing | Free to install; Modem subscription required |

## Before submitting

- [ ] Close [DEV-2653](https://linear.app/modem-dev/issue/DEV-2653) — **the only real blocker**. Small: three headers across four call sites, fully specified in the ticket.
- [ ] Settle the global-`read` vs `tickets:read` scope question
- [ ] Confirm no Modem listing already exists
- [ ] Re-verify requirements against Zendesk's live developer docs
