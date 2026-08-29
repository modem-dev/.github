# Gong → Gong Collective

**Program:** Gong Collective (marketplace inside the Gong Partner Network)
**Technology partner request:** https://integrations.gong.io/partner/request
**Priority:** P2 · **Status:** ready to submit once assets exist
**Why it matters:** highest buyer-relevance of the P2 set. Gong's ecosystem points at
customer-facing and revenue teams, which overlaps Modem's buyer. ~280–300 apps in the
integrations category, roughly a third AI-positioned — established but not saturated.

> 📝 **Note, not a blocker.** `gong.mdx` carries `tag: 'Beta'` and the overview card
> reads "Gong (Beta)", while the manifest says `featureFlag: null` — Gong is GA.
> Submitting as-is (decision, 2026-08-27). Gong's partner request is human-reviewed
> and has no no-beta rule; if a reviewer raises it, the answer is that it is GA and
> the docs label is stale.

> ⚠️ **Gong requires Modem's Scale plan ($250/mo).** Per `INTEGRATION_MINIMUM_PLAN`,
> Gong moved to the Scale tier on 2026-08-17. It is not available on Basic or Startup.
> Every other integration in this batch is available from the free tier. The pricing
> answer on this form is therefore different from all the others — do not copy-paste
> it. Orgs that connected Gong before the change keep their connection.

## Sequence

1. **Technology partner** → gets the integration listed in the Collective
2. **GTM partner** → co-marketing motion, **requires a live integration first**

Do them in that order. The GTM application is not submittable until the listing is live.

## Technology partner request — filled

| Field | Value |
| --- | --- |
| Company name | Modem |
| Website | https://modem.dev |
| Contact | Ben Vinegar, CEO — ben@modem.dev |
| Technical contact | Mike Clarke, CTO |
| Support | support@modem.dev |
| Integration type | Data consumer — reads calls, transcripts, and participants via OAuth |
| Integration status | Live and generally available |
| Documentation | https://modem.dev/docs/integrations/gong |
| Privacy policy | https://modem.dev/privacy |
| Terms | https://modem.dev/terms |
| Pricing | Requires Modem Scale plan, $250/mo (14-day trial includes it) |

### What the integration does
> Modem captures transcripts from recorded Gong calls and feeds them into the same
> feedback pipeline as Slack, Zendesk, Intercom, GitHub, and email. Each call becomes
> a conversation that's grouped into topics, classified by type (bug, feature
> request, praise, complaint), and linked to the people and companies who spoke on it.
>
> The point is cross-channel: what a customer says on a Gong call and what the same
> customer files as a support ticket land in the same topic. A product team can see
> that the objection raised in three sales calls is the same issue support has been
> fielding for a month — and that it's already in the backlog, or isn't.

### Customer value
> Revenue teams generate the highest-signal product feedback a company gets, and it
> is the hardest to act on because it lives in call recordings nobody outside sales
> replays. Modem makes Gong calls queryable alongside every other customer channel,
> so product and engineering can act on what customers actually said — and so the
> revenue team can see what happened to it.

### Data accessed
OAuth scopes from `GONG_OAUTH_SCOPES`:

| Scope | Why |
| --- | --- |
| `api:calls:read:basic` | Call metadata — when, who, which workspace |
| `api:calls:read:extensive` | Call detail needed for accurate attribution |
| `api:calls:read:transcript` | The transcript is the feedback signal |
| `api:users:read` | Resolve speakers to people |
| `api:workspaces:read` | Scope ingest to the subscribed workspaces |

Transcripts are processed for topic extraction and analysis. Not exported, not resold,
not used to train third-party models. Encrypted at rest; organization-scoped isolation
with PostgreSQL Row-Level Security.

## Assets

- [ ] Logo, square, high-res PNG
- [ ] Screenshots showing Gong call transcripts as Modem topics
- [ ] One-page solution brief (Gong partner listings typically want one)

## Before submitting

- [ ] **Confirm current requirements directly with Gong** — partner program structures
      change and public documentation is thin. Recommend emailing before filling the form.
- [ ] Queue the GTM partner application for after the listing goes live
