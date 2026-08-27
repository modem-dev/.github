# Notion → Integration Gallery

**Program:** Notion Integration Gallery (public API integration)
**Priority:** P2 · **Status:** ✅ **closest to submittable** — copy complete, needs assets
**Review:** security and privacy review, 5–10 business days

## Requirements check

| Requirement | Status |
| --- | --- |
| Public API integration | ✅ OAuth 2.0 public integration |
| Publicly available via OAuth | ✅ `notion` is unflagged in the manifest (GA); no Beta tag in docs |
| Tagline | ✅ below |
| Privacy policy | ✅ https://modem.dev/privacy |
| Terms of service | ✅ https://modem.dev/terms |
| Support email | ✅ support@modem.dev |
| Company name + website | ✅ Modem — https://modem.dev |

## Listing form — filled

| Field | Value |
| --- | --- |
| Integration name | Modem |
| Tagline | Bring your Notion workspace to your product feedback agent. |
| Company name | Modem |
| Company website | https://modem.dev |
| Category | Product management · Productivity |
| Privacy policy | https://modem.dev/privacy |
| Terms of service | https://modem.dev/terms |
| Support email | support@modem.dev |
| Documentation | https://modem.dev/docs/integrations/notion |
| Integration type | Public OAuth integration, fetch-based |

### Description
> Modem is an AI product teammate that captures customer feedback from across your
> team's tools and triages it into a clear backlog. Connecting Notion lets the Modem
> Agent work with the documents your team already keeps there.
>
> Once connected, the agent can search your pages and databases, read content,
> create new pages, update properties, and add comments — from chat, in the flow of
> the work. Ask it to draft a spec from a cluster of customer reports, update a
> roadmap page with what actually shipped, or pull the PRD for the feature a
> customer is asking about.
>
> **Modem does not sync or store your Notion data.** The integration is fetch-based:
> the agent queries your workspace on demand when you ask, and only ever sees pages
> and databases you have explicitly shared with it in Notion.

### Data handling — for the security & privacy review
This is the section the review actually turns on. Lead with the architecture:

- **No sync, no storage.** `sourceName: null`, `events: 'none'`, `worker: null` in
  the integration manifest — Modem runs no ingest pipeline for Notion. Content is
  fetched on demand to answer a user request and is not persisted as Modem content.
- **Explicit sharing only.** The integration can access only pages and databases a
  user has shared with it in Notion. Modem cannot enumerate the workspace.
- **Token storage.** OAuth tokens encrypted at rest with AES-256-GCM, per-token IVs.
- **Tenant isolation.** Organization-scoped ORM wrapper plus PostgreSQL Row-Level
  Security.
- **Retention.** No Notion content retained. Disconnecting revokes the token.
- **Third-party sharing.** None.
- **AI processing.** Fetched content is passed to the model serving the user's
  request and is not used to train third-party models. ⚠️ Confirm this matches the
  current vendor terms before submitting.

> ⚠️ **One thing to get ahead of.** The manifest notes that Notion refresh tokens are
> stored but **the refresh flow is not wired** (`tokenRefresh: 'none'`, see the
> `notion_oauth_refresh` note). A privacy reviewer asking about credential lifecycle
> will get an answer that sounds worse than it is. Either wire the refresh before
> submitting, or have a clear written answer about token expiry and re-auth
> behaviour ready.

## Assets

- [ ] Logo, square, high-res PNG
- [ ] Screenshots showing the agent working with Notion pages
- [ ] Cover image at Notion's current dimensions

## Before submitting

- [ ] Resolve the token-refresh answer (above)
- [ ] Confirm no Modem listing already exists
- [ ] Re-verify requirements against Notion's live developer docs
