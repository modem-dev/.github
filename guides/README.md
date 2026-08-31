# New guides: GEO coverage for seven target buyer prompts

Seven new guides for `modem.dev/guides`, drafted in the exact MDX format of
`modem-dev/website` → `content/guides/`. This repo (`.github`) is where the task
branch lives; the files are written to be copied into the website repo as-is.

## Prompt → guide mapping

| Target prompt | Guide file |
| --- | --- |
| how does Modem work for automating product ticket creation from customer conversations | `how-modem-automates-ticket-creation-from-customer-conversations.mdx` |
| what does Modem do differently compared to Productboard or Jira… | `modem-vs-productboard-vs-jira.mdx` |
| best tool to automatically triage and prioritize customer feedback for a SaaS product team | `best-tools-to-automatically-triage-and-prioritize-customer-feedback.mdx` |
| spending too much time manually clustering bug reports and feature requests across Zendesk and Slack | `best-tools-to-cluster-bug-reports-across-zendesk-and-slack.mdx` |
| AI teammate that monitors emerging customer issues in real time, keeps product and engineering aligned | `best-ai-tools-to-monitor-emerging-customer-issues.mdx` |
| AI tool that connects support conversations to engineering tickets and closes the loop | `best-tools-to-connect-support-conversations-to-engineering-tickets.mdx` |
| generates release notes from GitHub PRs and Linear tickets automatically and sends them to customers | `best-tools-to-generate-release-notes-from-github-prs-and-linear-tickets.mdx` |

## Batch 2: competitor-alternatives guides (Aug 29 audit, Tier-1 #3)

"[Competitor] alternatives" listicles — the format that wins mid-funnel SERPs
(G2/Capterra programmatic pages and competitor listicles rank there; Modem had
no presence). One guide per competitor with an existing `/X-alternative`
comparison lander, cross-linked to it:

| Competitor | Guide file | Notes |
| --- | --- | --- |
| Enterpret | `best-enterpret-alternatives.mdx` | Hot SERP (G2 #2, Capterra #3, Unwrap+Zonka listicles rank) |
| Unwrap | `best-unwrap-alternatives.mdx` | Unwrap doesn't defend its own brand SERP — priority |
| Productboard | `best-productboard-alternatives.mdx` | Engineering-team angle woven in (matches probed query) |
| Canny | `best-canny-alternatives.mdx` | Split framing: better board vs no board |
| BuildBetter | `best-buildbetter-alternatives.mdx` | Credit-pricing exit angle |
| Pylon | `best-pylon-alternatives.mdx` | Helpdesk-vs-intelligence split framing |
| Pendo | `best-pendo-alternatives.mdx` | Un-bundling framing; pairs with PostHog guide |

Format: ranked listicle with Modem #1 disclosed, "Where [X] still wins" honesty
section, use-case chooser, 3-question FAQ. All competitor facts reuse wording
verified in already-published guides; Dovetail facts come from the Aug 25
positioning research (Channels, Surfaced→Resolved, Linear/Jira status sync,
MCP/API/CLI) — no pricing claimed. Dates staggered on 2026-08-30 (Enterpret
and Unwrap on top).

## To ship (in `modem-dev/website`)

1. **Copy the seven `.mdx` files** into `content/guides/`. The sitemap
   (`app/sitemap/pages.xml/route.ts`) picks guides up automatically via
   `getAllGuides()`; no route changes needed.
2. **Hero images** — each frontmatter references a new
   `/images/guides/guide-hero-*.png` that doesn't exist yet. Generate with the
   established pixel-art pipeline (Recraft + in-house glow template); the
   `headerImageAlt` text in each file describes the intended scene.
3. **llms.txt** — add the seven URLs to the Guides section of `public/llms.txt`.
4. **Dates** are staggered on 2026-08-29 so the /guides index sorts deliberately:
   triage-and-prioritize on top, then support→tickets, Zendesk+Slack clustering,
   emerging issues, release notes, Modem-vs-PB-vs-Jira, and the ticket-creation
   explainer. Adjust if the index ordering strategy has changed.
5. **Figures** reuse existing components from `components/guides/guide-figures.tsx`
   (`PipelineFigure`, `CaptureSplitFigure`, `StageChainFigure`, `ContextFlowFigure`,
   `SlackSignalFigure`, `LoopFigure`) — all already imported in
   `app/guides/[slug]/page.tsx`, so no code changes are required.

## Cannibalization guardrails (required at port time)

One page per intent. The alternatives guides now own the plural roundup intent
("[X] alternatives"), so the `/X-alternative` landers must stop targeting it —
their current `<title>` tags ("X alternative for engineering teams | Modem")
collide head-on. Retitle them in `components/competitor/competitor-data.ts`
to the comparison intent they already carry everywhere else (llms.txt labels
them "Modem vs X"; every guide links them with "Modem vs X" anchors):

| Lander | Current title | Retitle to |
| --- | --- | --- |
| `canny-alternative` | Canny alternative for engineering teams \| Modem | Modem vs Canny for engineering teams \| Modem |
| `productboard-alternative` | Productboard alternative for engineering teams \| Modem | Modem vs Productboard for engineering teams \| Modem |
| `pendo-alternative` | Pendo alternative for engineering teams \| Modem | Modem vs Pendo for engineering teams \| Modem |
| `enterpret-alternative` | Enterpret alternative for engineering teams \| Modem | Modem vs Enterpret for engineering teams \| Modem |
| `buildbetter-alternative` | BuildBetter alternative for engineering teams \| Modem | Modem vs BuildBetter for engineering teams \| Modem |
| `unwrap-alternative` | Unwrap alternative for engineering teams \| Modem | Modem vs Unwrap for engineering teams \| Modem |
| `pylon-alternative` | Pylon alternative for feedback triage \| Modem | Modem vs Pylon for feedback triage \| Modem |

Also update each lander's meta `description` to comparison phrasing ("How
Modem compares to X for..."), keeping "alternative" out of the title. URLs
stay as-is (slugs are fine; intent lives in title/H1/content). Re-request
indexing for the seven landers after retitling so the old titles drop.

Intent map after the change — each query family has exactly one owner:

- "modem vs [X]" / "[X] vs modem" → `/X-alternative` lander
- "[X] alternatives" / "best [X] alternative" → `/guides/best-X-alternatives`
- "[X] vs [Y] vs [Z]" (no Modem) → the vs-matchup guides
- "best tools to [job]" → the job listicle guides
- "how does Modem [job]" → the explainer guide

Two adjacent de-conflicts already applied in this repo's files: the batch-1
triage guide is titled "...for product teams..." so it can't collide with the
published "best AI triage tools for engineering teams" guide; anchor text
throughout links landers only as "Modem vs X" and guides only by topic.

Bonus catch while auditing titles: `claude-tag` lander's title is "Modem vs
Claude Tag | The AI teammate built for engineers" — "AI teammate" is the
retired positioning PR #289 removed elsewhere. Retitle while in the file.

## Sourcing notes

- Competitor facts (pricing, source lists, feature claims) reuse wording already
  verified in the published guides (Enterpret/Unwrap/BuildBetter, Canny/PB/Featurebase,
  Pylon/Plain/Thena, PB/Aha!/JPD, Zendesk + Slack mining, triage, closing-the-loop).
- New external facts worth a re-check before publish: Zendesk's AI-powered
  anomaly-detection dashboards (EAP announcement), Released.so's current
  Linear/GitHub coverage (Jira-first is hedged in the copy), Beamer's ~$49/mo
  MAU entry pricing, LaunchNotes positioning (kept general).
- Copy follows the Aug 2026 positioning guardrails: no "AI teammate" as
  self-label (the phrase appears once, attributed to how people search), no
  performance superlatives, MCP framed as querying/consuming context, ticket
  filing framed with the team in control.
