# Linear → Integration Directory

**Program:** Linear Integration Directory
**Submission:** email integrations@linear.app via Linear's submission form
**Priority:** P2 · **Status:** ✅ **fastest path to a live listing** — send the email
**Advantage:** Modem's own team runs on Linear (`modem-dev` workspace). There is a
real relationship to lean on if the submission stalls.

## Requirements check

| Requirement | Status |
| --- | --- |
| Built on OAuth | ✅ OAuth 2.0 |
| Dedicated app workspace | ⚠️ Confirm the OAuth app lives in a dedicated workspace, not a personal one |
| Formal company, useful to the community | ✅ Modem qualifies |
| Publicly available | ✅ `linear` is unflagged in the manifest (GA); no Beta tag in docs |

## Draft submission email

**To:** integrations@linear.app
**Subject:** Integration Directory submission — Modem

> Hi,
>
> I'd like to submit Modem for the Linear Integration Directory.
>
> **What Modem is.** Modem is an AI product teammate that captures customer feedback
> from everywhere it lands — Slack, Discord, Zendesk, Intercom, GitHub, Gong, email —
> and triages it into a clear backlog. It groups related reports into topics,
> classifies them, and links each one to the people and companies who raised it.
>
> **What the integration does.** Once a workspace connects Linear via OAuth, the
> Modem Agent can search issues, create new ones directly from clustered user
> feedback, update existing issues, and add comments — from chat. It's fetch-based:
> Modem doesn't continuously sync or store Linear data, it queries on demand.
>
> The practical shape of it: five customers report the same bug across three
> channels, Modem collapses that into one topic with the evidence attached, and the
> agent files one Linear issue that already contains who reported it and what they
> said. When it ships, Modem helps close the loop with those customers.
>
> **Details**
> - Company: Modem — https://modem.dev
> - Docs: https://modem.dev/docs/integrations/linear
> - Privacy: https://modem.dev/privacy · Terms: https://modem.dev/terms
> - Support: support@modem.dev
> - Pricing: free tier available; paid plans from $80/mo, unlimited users on every plan
> - Contact: Ben Vinegar, CEO — ben@modem.dev
>
> Listing copy and assets are attached. Happy to adjust to fit the directory's format.
>
> Thanks,
> [NAME]

## Listing copy

**Tagline:** Turn customer feedback into Linear issues, with the evidence attached.

**Description:**
> Modem captures customer feedback from across your team's tools and groups it into
> topics. Connect Linear and the Modem Agent can search your issues, create new ones
> from clustered feedback, update them, and comment — all from chat. Modem doesn't
> sync or store your Linear data; it queries on demand.

### Scopes requested
From `REQUIRED_LINEAR_OAUTH_SCOPES`: `read`, `write`, `issues:create`,
`comments:create`, `app:assignable`, `app:mentionable`, `customer:read`,
`customer:write`.

> ⚠️ `customer:read` / `customer:write` touch Linear's Customer Requests feature.
> Be ready to explain the use — mapping Modem's people/company records onto Linear
> customers is a *good* story and worth stating proactively rather than being asked.

## Assets — per Linear's live docs (verified 2026-08-28)

Submit via the form at [linear.app/docs/integration-directory#submit-your-integration](https://linear.app/docs/integration-directory#submit-your-integration); assets to integrations@linear.app or linked in the form. Linear provides a Figma template.

- [x] Color icon, 320×320 — `assets/linear/modem-icon-color.svg` (built from the org logo)
- [x] Monochrome white icon, 320×320 — `assets/linear/modem-icon-white.svg`
- [ ] Showcase images, 1–3, **1600×1000** — ❌ and note: Linear says to **"defer away from simple screenshots"** and design them. This is design work, not capture work — the shot list's raw captures are an input, not the deliverable, for this one.

## Before submitting

- [ ] Confirm the dedicated app workspace
- [ ] Confirm no Modem listing already exists
- [ ] Re-verify the submission path against Linear's live docs
