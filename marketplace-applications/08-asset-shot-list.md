# Asset shot list — screenshots and demo video

The critical path. Nothing except the Linear email can be submitted without these, and
they are reusable across all seven listings. Capture once, crop per marketplace.

Screen names below are real dashboard routes
(`apps/dashboard/src/app/[orgSlug]/(dashboard)/…`).

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

| # | Screen | What must be visible | Used by |
| --- | --- | --- | --- |
| C1 | `topics` list | Multiple topics, each showing source icons from several tools. **This is the hero shot** — it's the one image that explains the product. | All |
| C2 | `topics/[id]` detail | One topic holding evidence from 3+ different sources, with the people who reported it | All |
| C3 | `agent` chat | A real question answered with citations back to source messages — e.g. "any open tickets about dark mode?" | All |
| C4 | `people` or `companies` | A profile showing one person's activity stitched across several tools | Atlassian, Intercom, Zendesk, Gong |
| C5 | `sources` | The connected-sources view showing many integrations live at once | All |
| C6 | `settings/integrations` index | The integration catalog | All |
| C7 | `automations` | A configured automation | GitHub, Atlassian |

## Per-integration shots — one each, for that marketplace only

| Shot | Screen | Must show |
| --- | --- | --- |
| I-JIRA | `settings/integrations/jira` + a topic containing a Jira issue | Jira issues in Modem; the agent creating or commenting on one |
| I-INTERCOM | `settings/integrations/intercom` + a topic with an Intercom conversation | Conversation captured; the admin toggle for agent write access (this is the privacy story — show it) |
| I-ZENDESK | `settings/integrations/zendesk` + a topic with a Zendesk ticket | Ticket comments grouped into a topic |
| I-GITHUB | `settings/integrations/github` + `pull-requests` | Issues as feedback and PRs as shipping context, side by side |
| I-NOTION | `agent` querying Notion | Agent reading/creating a Notion page from chat |
| I-LINEAR | `agent` creating a Linear issue from a topic | Issue created with the evidence trail attached |
| I-GONG | A topic containing a Gong call transcript | Call transcript as a topic, speakers resolved to people |

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
