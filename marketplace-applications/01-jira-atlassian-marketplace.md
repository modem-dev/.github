# Jira → Atlassian Marketplace

**Program:** Atlassian Marketplace, Integrations category, Cloud only
**Portal:** https://marketplace.atlassian.com/manage · partner account required
**Priority:** P1 · **Status:** draft ready, blocked on assets + docs de-beta

> 🚧 **Blocker found (not in the Notion audit).** `apps/docs/integrations/jira.mdx`
> still carries `tag: 'Beta'` and an inline "currently in beta" warning, and
> `overview.mdx` line 186 tells readers that Beta integrations are "enabled per
> organization rather than being available to everyone."
> An Atlassian reviewer reads the public docs. Submitting while the docs describe
> the integration as limited-availability invites a rejection. The manifest says
> `featureFlag: null` — it is GA. **This is a stale-docs fix, not an engineering
> one.** Strip the tag and the warning before submitting.

## Account setup

- [ ] Create the Atlassian Marketplace partner account (free)
- [ ] Vendor/partner profile: company name, logo, support contact, website
- [ ] ⚠️ Confirm no Modem listing already exists — the audit inferred absence, never verified it

## Listing form — filled

| Field | Value |
| --- | --- |
| App name | Modem |
| Vendor name | Modem |
| Summary (one line) | Turn Jira issues and every other feedback channel into one triaged backlog. |
| Categories | Integrations · Reporting · Project management |
| Hosting | Cloud (Server / Data Center: skip) |
| Pricing model | Paid via vendor (Modem is billed on modem.dev, not through Atlassian) |
| App type | Integration (OAuth 2.0 3LO, external service) |
| Privacy policy | https://modem.dev/privacy |
| Terms of use | https://modem.dev/terms |
| Support site | https://modem.dev/contact |
| Support email | support@modem.dev |
| Documentation | https://modem.dev/docs/integrations/jira |
| Data residency | ⚠️ **NEEDED** — Atlassian asks where customer data is stored. Confirm region(s). |

### Short description
> Modem connects your Jira site to every other place feedback lives — Slack,
> Zendesk, Intercom, GitHub, email — and keeps them in one triaged view.

### Full description
> **One connection, your whole Jira site.**
> Modem captures Jira issue and comment activity in real time and links it back to
> the people and companies behind each request. One connection covers every project
> on your site, including Jira Service Management request types.
>
> **What it does**
> - Captures issues, comments, and issue metadata as they change, via webhooks
> - Groups related reports across Jira, Slack, Zendesk, Intercom, GitHub, and email
>   into a single topic, so five tickets about one bug read as one problem
> - Resolves reporters to people and companies, so you can see who is affected
> - Lets the Modem Agent search, create, update, and comment on Jira issues from chat
>
> **Ask instead of dig.** "What are customers reporting about billing that isn't
> already in Jira?" The agent reads across every connected source and answers.
>
> Modem does not read your source code and does not export your Jira data.

### Permissions justification
OAuth 2.0 (3LO) scopes requested, from `REQUIRED_JIRA_OAUTH_SCOPES`:

| Scope | Why |
| --- | --- |
| `read:jira-work` | Read issues and comments — the core ingest |
| `write:jira-work` | Agent creates and updates issues on explicit user instruction |
| `read:jira-user` | Resolve reporters and assignees to people profiles |
| `manage:jira-webhook` | Register the webhooks that deliver real-time activity |
| `read:servicedesk-request` | Cover Jira Service Management request types in the same connection |
| `write:servicedesk-request` | ⚠️ **Requested but not yet used** — reserved for future JSM agent replies. Atlassian reviewers challenge unused scopes. Either drop it until the feature ships, or be ready to justify it. |
| `offline_access` | Refresh tokens so the connection survives without re-auth |

Webhook events registered: `jira:issue_created`, `jira:issue_updated`,
`jira:issue_deleted`, `comment_created`, `comment_updated`, `comment_deleted`.

## Assets

- [ ] Logo, square, ≥512×512 PNG
- [ ] Banner / highlight image
- [ ] 3–5 screenshots showing Jira data inside Modem
- [ ] Optional but recommended: 60s demo video

## Before submitting

- [ ] **Strip the Beta tag** from `jira.mdx` and reconcile `overview.mdx` line 186
- [ ] Decide on `write:servicedesk-request`
- [ ] Confirm data residency
- [ ] Verify current requirements against Atlassian's live developer docs — the
      internal source is the June 2026 review, already proven stale on Slack

## Explicitly out of scope
Marketplace Partner Program and Cloud Fortified badges are earned later on traction
and support SLAs. Not applicable to a first listing.
