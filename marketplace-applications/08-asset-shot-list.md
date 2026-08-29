# Asset shot list — screenshots and demo video

> 📸 **Partially captured as of 2026-08-17.** The core dashboard set (C1, C2, C4, plus
> three Stories shots) exists in the shared Drive folder below, shot by Chrissy against
> the seeded "MerchantRail" demo org. The agent, sources, integrations, automations,
> and all per-integration shots are still missing.

Still the critical path for the remaining listings. Nothing except the Linear email can
be submitted without these, and they are reusable across all seven listings. Capture
once, crop per marketplace.

Links below go straight to the screen to shoot. Replace `{org}` with the demo org's
slug — routes are `apps/dashboard/src/app/[orgSlug]/(dashboard)/…`, served at
`https://app.modem.dev/{org}/…`.

**Where captured files land (decided):** the shared Drive folder
[Modem product shots](https://drive.google.com/drive/folders/11j63eVbF1QA0p_Qt54n77vRkddsZSOJn).
It holds the 10 raw captures (`01`–`10`, 2048×1200 @2×), the standardized marketing
background (`Background`), and the two capture/framing skills used to produce them
(`capture-and-frame-modem-screenshots.md`, `frame-existing-screenshits.md`). Add new
captures there with the same numbered naming, and keep raw masters separate from
framed derivatives.

## Progress

Update as shots are captured, so this doubles as the tracker.

| Shot | Captured? |
| --- | --- |
| C1 hero — topics list | ✅ `01-topics-overview.png` |
| C2 topic detail | ✅ `05-topic-checkout-reliability.png`, `06-topic-fraud-scoring-praise.png` (Slack + Zendesk + Intercom evidence) |
| C3 agent chat | ❌ |
| C4 person/company profile | ✅ `07-people-directory.png`, `08-person-marcus-webb.png`, `09-companies-directory.png`, `10-company-webvan.png` |
| C5 sources | ❌ |
| C6 integrations catalog | ❌ |
| C7 automations | ❌ |
| I-JIRA · I-INTERCOM · I-ZENDESK · I-GITHUB · I-NOTION · I-LINEAR · I-GONG | ❌ all seven — the demo org has no GitHub/Jira/Linear/Gong data seeded yet, so those need seeding before their shots |
| Bonus — Stories (not in original spec) | ✅ `02-stories-overview.png`, `03-story-eu-cdn-latency.png`, `04-story-customer-praise.png` |
| Dark-mode hero variant | ❌ |
| Demo video (30–90s, captioned) | ❌ |

## Capture rules

- **One demo org, realistic data.** Same org across every shot so the listings look
  like one product. Populate it with plausible feedback across Slack, GitHub, Zendesk,
  Intercom, Jira, Linear, and Gong so cross-source topics actually show multiple sources.
- **No real customer data.** Every marketplace listing is public and permanent. Use
  seeded or scrubbed data — never a live customer org.
- **Capture at 2× / retina**, then downscale. Upscaling a 1× capture will read as
  pixelated and Intercom explicitly rejects that.
- **Light mode** as the default set. Capture a dark-mode variant of the hero shot only.
- **Widest capture wins.** Shoot at ~2560×1600 and crop down; several marketplaces want
  different aspect ratios from the same screen, and re-shooting is the expensive part.
- **Strip the browser chrome** unless the marketplace asks for it.

## Core set — shoot these seven once, reuse everywhere

| # | Go here | What must be visible | Used by |
| --- | --- | --- | --- |
| C1 | `app.modem.dev/{org}/topics` | Multiple topics, each showing source icons from several tools. **This is the hero shot** — the one image that explains the product. | All |
| C2 | `app.modem.dev/{org}/topics/{id}` | One topic holding evidence from 3+ different sources, with the people who reported it | All |
| C3 | `app.modem.dev/{org}/agent` | A real question answered with citations back to source messages — e.g. "any open tickets about dark mode?" | All |
| C4 | `app.modem.dev/{org}/people` or `/companies` | A profile showing one person's activity stitched across several tools | Atlassian, Intercom, Zendesk, Gong |
| C5 | `app.modem.dev/{org}/sources` | The connected-sources view showing many integrations live at once | All |
| C6 | `app.modem.dev/{org}/settings/integrations` | The integration catalog | All |
| C7 | `app.modem.dev/{org}/automations` | A configured automation | GitHub, Atlassian |

## Per-integration shots — one each, for that marketplace only

| Shot | Go here | Must show |
| --- | --- | --- |
| I-JIRA | `app.modem.dev/{org}/settings/integrations/jira` + a topic with a Jira issue | Jira issues in Modem; the agent creating or commenting on one |
| I-INTERCOM | `app.modem.dev/{org}/settings/integrations/intercom` + a topic with an Intercom conversation | Conversation captured, **and the admin toggle for agent write access** — that toggle is the privacy story, so make it visible |
| I-ZENDESK | `app.modem.dev/{org}/settings/integrations/zendesk` + a topic with a Zendesk ticket | Ticket comments grouped into a topic |
| I-GITHUB | `app.modem.dev/{org}/settings/integrations/github` + `app.modem.dev/{org}/pull-requests` | Issues as feedback and PRs as shipping context, side by side |
| I-NOTION | `app.modem.dev/{org}/agent` | Agent reading or creating a Notion page from chat |
| I-LINEAR | `app.modem.dev/{org}/agent` | Agent creating a Linear issue from a topic, evidence trail attached |
| I-GONG | `app.modem.dev/{org}/topics/{id}` | A Gong call transcript as a topic, speakers resolved to people |

## Per-marketplace requirements

Verified against live docs where reachable. Several vendor doc sites are blocked from
this environment — those are marked **verify in portal**, and the portal shows exact
specs at upload time.

### Atlassian Marketplace
- **Three highlights required.** Each needs a full screenshot plus a cropped version at
  **580×330 px**
- Highlight title **≤50 chars**, highlight summary **≤220 chars** — three of each
- Formats: .jpg, .png, .gif, .bmp
- Additional screenshots allowed beyond the three highlights
- Suggested highlights: C1 (one backlog from every channel) · I-JIRA (issues in and
  out of Jira) · C3 (ask instead of dig)
- Source: [Atlassian listing docs](https://developer.atlassian.com/platform/marketplace/creating-a-marketplace-listing/), [marketing assets](https://developer.atlassian.com/platform/marketplace/declaring-marketing-assets-for-server-apps/)

### Zendesk Marketplace
- Exact filenames required: `logo.png`, `logo-small.png`, `screenshot-0.png`,
  `screenshot-1.png`, `screenshot-2.png`
- Screenshots **full bleed, no padding**
- **No Zendesk trademarks in the app icon**
- Exact pixel dimensions: **verify in portal** (developer.zendesk.com blocked here)
- Suggested three: I-ZENDESK · C2 · C3
- Source: [Create app brand assets](https://developer.zendesk.com/documentation/marketplace/building-a-marketplace-app/create-app-brand-assets/)

### Intercom App Store
- App icon **512×512 PNG**, not pixelated or stretched, **no Intercom logo in it**
- Icon should be bold and simple — it renders small. Avoid text
- Listing images must be in "marketing format" — a named common rejection reason.
  Check the images section of the listing guide before submitting
- Suggested: I-INTERCOM (lead with the write-access toggle) · C1 · C2 · C3
- Source: [Listing your App](https://developers.intercom.com/docs/publish-to-the-app-store/listing-your-app)

### Slack Marketplace (already live — for the refresh)
- Screenshots **1600×1000 (8:5)**
- Demo video **30–90s**, YouTube, closed captions, no ads
- Source: the Dec 2025 Slack Marketplace Submission review

### GitHub, Notion, Linear, Gong
**Verify in portal.** No published fixed dimensions found. The core set at 2× covers
all four; crop at upload. Linear and Gong are human-reviewed submissions and are the
most forgiving.

## Demo video

Required by Slack, strongly recommended everywhere else. **30–90 seconds**, YouTube,
**closed captions**, no ads.

Suggested beat sheet — one continuous product story, no talking head:

| Time | Beat |
| --- | --- |
| 0:00–0:08 | The problem, one line of on-screen text over C5: feedback arrives in eight places |
| 0:08–0:20 | Connect flow — `settings/integrations`, one OAuth click, connected |
| 0:20–0:40 | The payoff — C1 then C2: scattered reports collapse into one topic with every source attached |
| 0:40–1:00 | C3 — ask the agent a real question, get an answer with citations |
| 1:00–1:15 | Close the loop — create the ticket with evidence attached (I-LINEAR or I-JIRA) |
| 1:15–1:30 | Logo, one-line value prop, modem.dev |

One video serves every listing. Don't cut per-marketplace versions unless a reviewer
asks — the connect step is generic enough to work for all of them.

## Open decision

⚠️ **Which positioning should the listings lead with?** The live homepage now reads
*"Product execution for the AI era"* and describes Modem as an *"AI-native product
workspace where signal becomes action."* The drafts in this folder use the *"AI product
teammate"* framing from the February fact sheet, which still lives at
`modem.dev/ai-product-teammate`, and the GitHub org README uses *"your dev team's
auto-triage Product Manager."*

Three live positionings. Listing copy should match whatever the site leads with, since
buyers click straight through. **Pick one before submitting** — then it's a
find-and-replace across the drafts, not a rewrite.
