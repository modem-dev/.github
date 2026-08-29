# Notion Marketplace listing — requirements review

**Source:** https://developers.notion.com/guides/get-started/marketplace-listing
**Reviewed:** 2026-08-29
**Verdict:** Modem is eligible and the application copy already drafted in
`marketplace-applications/05-notion-integration-gallery.md` (branch
`claude/integration-marketplace-partnerships-efme0o`) still holds up. The submission
*process* has changed since the June 2026 internal review — Notion replaced the old
"Integration Gallery" email/invite flow with a self-serve Marketplace listing dashboard —
so there are a few new process steps, but no new product blockers beyond the known
assets gap.

> Note on sourcing: `developers.notion.com` is blocked by the research environment's
> egress proxy, so this review reconstructs the live guide from search-indexed content
> rather than a direct page read. Field-level specifics (image dimensions, character
> limits) could not be verified and are flagged below. Whoever opens the portal sees
> the exact specs on the form itself.

## What changed vs. the June 2026 internal review

The internal checklist (Notion page "Notion → Integration Gallery" and the audit) was
built on the old doc, `publishing-integrations-to-notions-integration-gallery`. The live
guide is now "List on the Marketplace" and the flow is:

1. **Creator profile** — set up at https://app.notion.com/profile. Separate from a
   personal Notion profile; carries profile photo, cover photo, and company blurb.
   *New requirement — not in our checklist.*
2. **Marketplace listing dashboard** — Listings → **Connections** → "Start a new
   connection listing". Listings save as drafts and are editable until submitted.
3. **Listing draft** — listing name, brief + full description, category and tags,
   listing images + logo, and the public connection to associate with the listing.
   A custom listing URL can be set.
4. **Submit for review** — moves to the "Submitted" section; status trackable in the
   dashboard. Decision in **5–10 business days** by email (unchanged). Rejections
   come with a reason (brand/trademark issues, quality concerns, baseline criteria
   not met).

## Eligibility (Modem status)

| Requirement (live docs) | Modem status |
| --- | --- |
| Public API integration or Link Preview integration | ✅ Public API integration |
| Public connection using OAuth 2.0 | ✅ OAuth 2.0, GA (unflagged in manifest) |
| Installation scope **"Any workspace"** — "Selected workspaces only" and internal connections are not Marketplace-eligible | ⚠️ **Verify in the integration settings** — new explicit requirement, not in the June checklist |
| Tagline, privacy policy, terms, support email, company name + website | ✅ All drafted (modem.dev/privacy, modem.dev/terms, support@modem.dev) |
| Security & privacy review | Expected; data-handling answers drafted in `05-notion-integration-gallery.md` |

## Blockers before submitting

1. **Assets** — the known cross-marketplace blocker. Screenshots + logo + listing
   images; capture spec already exists at `marketplace-applications/08-asset-shot-list.md`.
   Nothing else on this list matters until these exist.
2. **Creator profile** — decide which account owns it and set it up (company identity,
   not personal). New step; small.
3. **Installation scope check** — confirm the Notion integration is set to
   "Any workspace" at notion.so/my-integrations. Two minutes; hard eligibility gate.
4. **Token-refresh answer** — refresh tokens stored but refresh flow not wired
   (`tokenRefresh: 'none'`). Have a written credential-lifecycle answer ready for the
   security review, or wire the refresh first. (Carried over from the drafted app.)
5. **Listing search** — confirm no Modem listing exists at notion.com/integrations/all
   (blocked for the research environment; needs a human spot-check).

## Could not verify (egress-blocked)

- Exact image dimensions and description character limits for connection listings.
- Whether the security review is a questionnaire, a form section, or a follow-up email.
- Whether Link Preview-specific requirements apply (they don't for us — Public API path).

## Suggested order

Unchanged from the audit: assets → creator profile + scope check → submit Notion early
(it has the 5–10 day external clock) alongside Linear.
