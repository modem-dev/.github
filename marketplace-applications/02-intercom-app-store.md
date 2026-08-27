# Intercom → App Store + App Partner Program

**Program:** Intercom App Store; publishing auto-enrols in the App Partner Program
**Portal:** Intercom Developer Hub → your app → App Listing + App Partner Program
**Priority:** P1 · **Status:** draft ready, blocked on a decision (below) + assets

> ❓ **Decision required before anything else: which OAuth app gets listed?**
> Modem runs **two** Intercom OAuth apps (`packages/api/.../intercom/router.ts`):
> - **read-only** (`INTERCOM_READONLY_CLIENT_ID`) — a separate, already
>   Intercom-approved app whose scopes physically cannot write
> - **full access** (`INTERCOM_CLIENT_ID`) — supports agent replies, tagging, and
>   conversation management. Per the docs, write access is **disabled by default**
>   and an admin opts in via Settings → Integrations → Intercom
>
> These are different submissions with different review burdens. The read-only app
> is the easy approval; the full-access app is the one that earns the "bidirectional
> integration" framing the Notion audit is counting on. **Listing the read-only app
> would undercut the entire rationale for prioritizing Intercom.** Recommend
> submitting the full-access app and disclosing the default-off write behaviour as a
> privacy feature.

## Listing form — filled

| Field | Value |
| --- | --- |
| App name | Modem |
| Tagline | Every piece of customer feedback, triaged into one backlog. |
| Category | Product management · Reporting & analytics |
| App type | Public app, OAuth |
| Pricing | Free to install; Modem subscription required (Basic $0 / Startup $80 / Scale $250) |
| Website | https://modem.dev |
| Privacy policy | https://modem.dev/privacy |
| Terms of service | https://modem.dev/terms |
| Support email | support@modem.dev |
| Documentation | https://modem.dev/docs/integrations/intercom |
| Data handled | Conversations, conversation parts, contacts, admins, tags, CSAT |

### Short description
> Modem pulls your Intercom conversations into the same feedback pipeline as Slack,
> Zendesk, GitHub, and email — grouped into topics, linked to the people who raised
> them, and ready to become tickets.

### Full description
> **Support conversations are product signals. Most teams treat them as a queue.**
>
> Modem captures Intercom conversation activity in real time — new conversations,
> user and admin replies, internal notes, state changes, tags, CSAT ratings, and
> whether Fin participated — and analyses it alongside every other channel your team
> uses.
>
> **What you get**
> - Related reports across Intercom, Slack, Zendesk, GitHub, Linear, Jira, and email
>   collapse into one topic, so the fifth person asking for the same thing in
>   different words shows up as one signal, not five tickets
> - Intercom contacts sync to Modem people profiles by email, giving a unified view
>   of each customer across every tool
> - The Modem Agent can search conversations and — when an admin enables write
>   access — reply, tag, and manage conversations directly
> - Historical backfill on connect, so the picture is complete from day one
>
> **Ask instead of dig.** "Any open Intercom conversations about the new onboarding
> flow? Summarize what customers reported and whether it's fixed." The agent reads
> across Intercom, GitHub, and Linear and tells you.

### Start Guide (required by Intercom's listing guidelines)
> 1. In Modem, go to **Settings → Integrations → Intercom** and click **Connect Intercom**.
> 2. Authorize the Modem app in Intercom. You'll need admin access to the workspace.
> 3. Modem begins a historical backfill of past conversations and starts receiving
>    new activity via webhooks. No further configuration is required.
> 4. *(Optional)* To let the Modem Agent reply to and tag conversations, an admin
>    enables write access from **Settings → Integrations → Intercom**. This is off by
>    default.

### Data access disclosure
| Data | Why |
| --- | --- |
| Conversations and parts | Core analysis — grouping feedback into topics |
| Internal notes | Team context on a report; treated identically to replies |
| Contacts (users, leads, visitors) | Link reports to people; matched on email |
| Admins | Attribute replies to the right teammate |
| Tags, state, CSAT | Classification and prioritization signal |

Data is processed for topic extraction and analysis. It is not exported, resold, or
used to train third-party models.

## App Partner Program page

Publishing auto-enrols Modem. Prepare:
- [ ] Partner description (reuse the long description above)
- [ ] Co-marketing contact: ben@modem.dev
- [ ] ⚠️ Target-customer and joint-value statement — needs a GTM decision, not a copy edit

## Before submitting

- [ ] **Decide read-only vs full-access app** (above) — everything else depends on it
- [ ] Screenshots showing Intercom conversations inside Modem
- [ ] Confirm no Modem listing already exists
- [ ] Re-verify requirements against Intercom's live developer docs
