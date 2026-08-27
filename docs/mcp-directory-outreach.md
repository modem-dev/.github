# MCP Directory Outreach — Modem MCP Server

Target list, submission mechanics, and outreach copy for getting the Modem MCP server
listed and verified across the MCP ecosystem.

**Last researched:** 2026-08-27

---

## How the ecosystem actually works

The directory landscape is not 30 independent submissions. It is a small number of
**sources of truth** plus a large number of **downstream mirrors** that scrape them:

1. **Official MCP Registry** (`registry.modelcontextprotocol.io`) — canonical metadata.
   Several directories ingest from it directly.
2. **GitHub** — Glama, mcp.so, awesome-lists and most SEO directories crawl public repos.
3. **Client galleries** (Claude, Cline, Docker, VS Code, Cursor) — the only ones with real
   install intent. These have human review and are where outreach effort actually pays.

**Practical consequence:** publish to the official registry and a public GitHub repo first.
That alone gets Modem into a large fraction of the long tail passively. Then spend real
effort on the four or five gated client galleries, and treat the SEO directories as a
30-minute batch of form fills.

---

## Prerequisites — assemble once, reuse everywhere

Every directory asks for the same ~15 fields. Fill this in before submitting anywhere;
each submission then takes minutes instead of an hour.

| Field | Value |
|---|---|
| Server name (registry namespace) | `dev.modem/modem` (requires DNS auth — see Tier 0.1) |
| Display name | Modem |
| One-liner (≤ 100 chars) | Your dev team's auto-triage Product Manager |
| Short description (≤ 250 chars) | *TBD — see draft below* |
| Transport | Remote, Streamable HTTP *(confirm)* |
| Server URL | `https://mcp.modem.dev` *(confirm)* |
| Auth | OAuth 2.0 + DCR *(confirm)* |
| Public repo | *needed for Glama / mcp.so / Cline / awesome-lists* |
| Docs URL | `https://modem.dev/docs/mcp` *(confirm)* |
| Privacy policy URL | **Required. Missing = automatic Claude rejection.** |
| Support contact | `support@modem.dev` *(confirm)* |
| Icon | 400×400 PNG **and** SVG; light + dark variants (`profile/logo-*.svg` exists) |
| Category | Developer Tools / Productivity |
| Tags | `product-management`, `feedback`, `triage`, `issues`, `agents` |
| Tool list | Every tool needs a `title` + `readOnlyHint` or `destructiveHint` |
| Test account | Pre-populated demo workspace + credentials for reviewers |

**Draft short description (reuse verbatim everywhere for brand consistency):**

> Modem captures customer feedback from Slack, Discord, support tickets, and GitHub issues,
> auto-triages it into prioritized topics, and exposes it to your coding agent. Ask for the
> top issues affecting a customer, pull the context behind a topic, and turn triaged feedback
> into work without a PM in the loop.

**Blocking gate:** annotate every tool with `readOnlyHint` / `destructiveHint` and publish a
privacy policy *before* submitting anywhere. These are the two most common rejection reasons
at Anthropic, and fixing them post-rejection costs a full review cycle.

---

## Tier 0 — Self-serve, no human to email (do this week)

No outreach needed. These are forms and CLIs. Doing them first makes the Tier 1 pitches
credible ("we're already in the official registry").

### 0.1 Official MCP Registry ⭐ highest leverage
- **URL:** https://registry.modelcontextprotocol.io · docs: https://modelcontextprotocol.io/registry/quickstart
- **Method:** `mcp-publisher` CLI (Homebrew or prebuilt binary), publishes a `server.json`.
- **Namespace:** GitHub auth gives you `io.github.modem-dev/*`. **Use DNS auth instead** to
  claim `dev.modem/*` — it is the branded namespace and it is first-come.
- **Effort:** ~1 hour. **Outreach:** none.
- **Why first:** downstream registries ingest from here, and the namespace is a land grab.

### 0.2 Glama
- **URL:** https://glama.ai/mcp · methodology: https://glama.ai/mcp/methodology
- **Method:** auto-indexes public GitHub repos; maintainer claims the listing via GitHub OAuth
  (verifies write/admin access on the repo).
- **Notes:** ranks on quality signals — real README, working install instructions, examples.
  Provides an in-browser inspector, so tool schemas and annotations are publicly visible.
- **Effort:** ~30 min once a public repo exists. **Outreach:** only if indexing stalls or
  metadata is wrong (template E).

### 0.3 Smithery
- **URL:** https://smithery.ai
- **Method:** `smithery mcp publish <url> -n modem/modem` (CLI: `smithery-ai/cli`).
- **Effort:** ~20 min. **Outreach:** none.

### 0.4 PulseMCP
- **URL:** https://www.pulsemcp.com · submit: https://www.pulsemcp.com/submit
- **Method:** submission form, plus automated crawling and official-registry ingestion.
- **⚠️ Verify:** a 2025 notice paused manual submissions during an ingestion rework. Check the
  submit page is live; if not, email `hello@pulsemcp.com` (template D).
- **Why it matters more than its size:** founded by Tadas Antanavicius (MCP Steering Committee)
  and Mike Coughlin; runs the *Weekly Pulse* newsletter — the ecosystem's main editorial
  surface. This is the one Tier 0 target that is also a Tier 3 relationship.

### 0.5 mcp.so
- **URL:** https://mcp.so · submit: https://mcp.so/submit
- **Method:** submit form / GitHub issue. **Public GitHub repo required.**
- **Effort:** ~10 min. Largest raw catalog (20k+); mostly SEO value.

### 0.6 MCP Market
- **URL:** https://mcpmarket.com · submit: https://mcpmarket.com/submit
- **Method:** form, submit GitHub repo, they review. **Effort:** ~10 min.

---

## Tier 1 — Gated client galleries (highest install intent; real review)

These are where users actually install from. Each needs a genuine submission and, in some
cases, a human nudge.

### 1.1 Claude Connectors Directory ⭐ highest value
- **Submit via:** the submission portal in your **organization settings on claude.ai**
  (not a public form). Docs: https://claude.com/docs/connectors/building/submission
- **Free.** Portal is always open. Passing servers typically enter as a *community connector*.
- **Hard requirements:**
  - Remote MCP server over **HTTPS**
  - **OAuth 2.0** for authenticated services
  - Every tool: `title` + applicable `readOnlyHint` / `destructiveHint`
  - **Public privacy policy** — incomplete or missing is an immediate rejection
  - Reviewer test-account instructions detailed enough to exercise the server end to end:
    every link, every credential, every step, against a *populated* workspace
  - Docs URL, support contact, icon
- **Outreach:** the "outreach" here is the reviewer notes field. Use **template A**.
- **Sequencing:** do not submit until the annotation + privacy-policy gate is closed.

### 1.2 Cline MCP Marketplace
- **URL:** https://github.com/cline/mcp-marketplace
- **Method:** open an issue using the `mcp-server-submission.yml` template.
- **Needs:** GitHub repo URL, **400×400 PNG logo**, short rationale, and confirmation you
  tested install in Cline from your README (optionally add `llms-install.md` for complex setups).
- **Review:** "within a couple of days"; weighs community adoption, maturity, security.
- **Outreach:** the issue body itself. Use **template B**.

### 1.3 Docker MCP Catalog / MCP Toolkit
- **URL:** https://github.com/docker/mcp-registry · CONTRIBUTING.md
- **Method:** PR adding `servers/modem/` with `server.yaml`, `tools.json`, `readme.md`.
- **Remote servers are accepted** — no container required. Use `task remote-wizard` to
  generate config. `type: remote`, plus `remote` (transport, URL) and `oauth` blocks.
- **Review:** Docker team review on every PR; live within 24h of merge, surfaced in Docker
  Desktop + Docker Hub. Test credentials shared via their form.
- **Outreach:** the PR description. Use **template C**.

### 1.4 VS Code / GitHub Copilot MCP gallery
- **URL:** https://github.com/mcp
- **Method:** currently sourced from GitHub's curated registry; VS Code surfaces it via `@mcp`
  in the Extensions view. Ingestion is tied to the official registry and GitHub curation.
- **Action:** publish to the official registry first (0.1), then check for inclusion. If absent
  after a few weeks, raise it in `github/community` discussions. Use **template E**.

### 1.5 Cursor
- **URL:** https://cursor.com/directory (community: cursor.directory)
- **Method:** community-maintained submission. Lower ceremony than the above.

### 1.6 Second-wave clients (batch, ~2 hours total)
Goose (Block) extensions · Continue Hub (`hub.continue.dev`) · Zed · Windsurf · Raycast ·
LM Studio. Each has its own small submission path. Worth doing once Tier 1.1–1.3 are live.

---

## Tier 2 — Community lists and SEO directories (batch in one sitting)

Low individual value, meaningful in aggregate for search. All are PR-or-form; none need a
relationship. Budget one focused afternoon.

| Target | URL | Method |
|---|---|---|
| awesome-mcp-servers (punkpeye) | github.com/punkpeye/awesome-mcp-servers | PR (template F) |
| modelcontextprotocol/servers | github.com/modelcontextprotocol/servers | PR to community list |
| mcpservers.org | mcpservers.org | Form / PR |
| awesome-mcp (abordage) | github.com/abordage/awesome-mcp | Auto-updated daily from crawl |
| LobeHub MCP | lobehub.com/mcp | Submit form |
| OpenTools | opentools.com | Submit form |
| mcp-get | mcp-get.com | CLI registry PR |
| explainx.ai | explainx.ai/mcp | Form |
| zPlatform | zplatform.ai/mcp-servers | Form |

---

## Tier 3 — Editorial and relationship outreach (after listings are live)

Only worth doing once Modem is actually installable. A "we exist" email lands better when it
links to a live listing.

| Target | Who | Angle |
|---|---|---|
| PulseMCP Weekly Pulse | Tadas Antanavicius, Mike Coughlin — `hello@pulsemcp.com` | New server feature; Tadas is on the MCP Steering Committee |
| Glama editorial | Frank Fiegel | "Alternatives to" / featured server placement |
| MCP community Discord | — | Show-and-tell channel post |
| Docker / Anthropic devrel | — | Post-listing co-marketing, once a community connector |

---

## Sequencing

1. **Week 1 — close the gates.** Annotate every tool (`title`, `readOnlyHint`/`destructiveHint`),
   publish the privacy policy, stand up the public repo + README, produce the icon set, create
   the reviewer demo workspace.
2. **Week 1 — Tier 0.** Claim `dev.modem/*` via DNS auth on the official registry. Then
   Smithery, mcp.so, MCP Market, PulseMCP. Glama should auto-index; claim it.
3. **Week 2 — Tier 1.** Claude Connectors portal, Cline issue, Docker PR. These run in parallel
   and all have multi-day review.
4. **Week 3 — Tier 2 batch** + second-wave clients.
5. **Week 4 — Tier 3 editorial,** now linking to live listings.

**Tracking:** one row per target — status, submitted date, reviewer contact, listing URL,
follow-up date. Nudge at 7 days, once, then move on.

---

# Outreach copy

Placeholders in `[brackets]`. Every template assumes the sender is a named human at Modem,
not a generic marketing alias — these are small teams and a real person gets a real reply.

---

## Template A — Claude Connectors Directory reviewer notes

*Not an email. This goes in the submission portal's notes/test-instructions field. It is the
single highest-value piece of copy here, because a reviewer who cannot reach a populated
workspace rejects the submission.*

> **What Modem is**
>
> Modem is an auto-triage product manager for engineering teams. It ingests customer feedback
> from Slack, Discord, support tickets, and GitHub issues, clusters it into prioritized topics
> with user and company context, and exposes that triaged view to agents and engineers.
>
> **What the MCP server does**
>
> The Modem MCP server gives Claude read and write access to a Modem workspace so a developer
> can work directly from triaged feedback:
>
> - `[list_topics]` — prioritized feedback topics (read-only)
> - `[get_topic]` — full context behind a topic: source messages, affected users, companies (read-only)
> - `[search_feedback]` — search raw feedback across all connected sources (read-only)
> - `[create_issue]` — turn a topic into a tracked issue (destructive: creates external state)
>
> Every tool carries a `title` and the applicable `readOnlyHint` / `destructiveHint`.
>
> **Test account**
>
> 1. Go to `[https://app.modem.dev/login]`
> 2. Sign in with `[reviewer@example.com]` / `[password]` — this account is pre-populated with a
>    demo workspace containing `[N]` feedback sources and `[N]` triaged topics, so every tool
>    returns non-empty results.
> 3. Connect the server at `[https://mcp.modem.dev]`. Auth is OAuth 2.0; the consent screen
>    requests `[scopes]`.
> 4. Suggested exercises: "What are the top feedback topics this week?" → `[list_topics]`;
>    "Show me everything behind the `[topic]` topic" → `[get_topic]`; "Create an issue for it"
>    → `[create_issue]`.
>
> **Links**
> Docs: `[https://modem.dev/docs/mcp]` · Privacy policy: `[https://modem.dev/privacy]` ·
> Support: `[support@modem.dev]`
>
> Happy to provide additional accounts or walk through anything — reach me directly at `[email]`.

---

## Template B — Cline MCP Marketplace issue

**Title:** `Add Modem MCP server — auto-triaged customer feedback for coding agents`

> **GitHub repo:** `[https://github.com/modem-dev/mcp-server]`
> **Logo:** attached (400×400 PNG)
>
> **What it does**
>
> Modem captures customer feedback from Slack, Discord, support tickets, and GitHub issues and
> auto-triages it into prioritized topics. The MCP server exposes that to Cline, so instead of
> reading a backlog someone else groomed, a developer can ask "what are users actually blocked
> on in `[area]`?" and get clustered feedback with the affected customers attached — then act on
> it in the same session.
>
> **Why Cline users specifically**
>
> Cline users are already doing the execution half of this loop. The missing half is knowing
> what to execute. This closes it without a round trip through a PM or a ticket tracker.
>
> **Install verification**
>
> Tested end to end in Cline using the repo README. Setup is `[remote server URL + OAuth /
> npx one-liner]`; no manual config file editing required. `[llms-install.md included for
> the OAuth step.]`
>
> **About us**
>
> Modem is built by Ben Vinegar (ex-VP Eng, Sentry) and Mike Clarke (ex-VP Eng, Treasury Prime),
> backed by Accel and Inovia. We also maintain `[hunk](https://github.com/modem-dev/hunk)`
> (8.8k stars) and `[slop-scan](https://github.com/modem-dev/slop-scan)`, so we're familiar with
> the bar for tools in this workflow.

---

## Template C — Docker MCP Registry pull request

**Title:** `Add Modem remote MCP server`

> Adds `servers/modem/` — a remote MCP server (`type: remote`, Streamable HTTP, OAuth 2.0).
> Config generated with `task remote-wizard`.
>
> **What it is:** Modem auto-triages customer feedback from Slack, Discord, support tickets,
> and GitHub issues into prioritized topics, and exposes them to coding agents so engineers can
> work from real user demand instead of a hand-groomed backlog.
>
> **Files:** `server.yaml` (remote transport + OAuth), `tools.json`, `readme.md`.
> **Category:** `[productivity]` · **Tags:** `[product-management, feedback, issues]`
>
> Server URL is publicly reachable and returns a valid MCP handshake. Tools are annotated with
> `readOnlyHint` / `destructiveHint`. Test credentials submitted via the credentials form —
> happy to re-send or provision a dedicated reviewer workspace.
>
> Maintainer contact: `[name, email]`.

---

## Template D — Directory maintainer email (cold, listing ask)

*Use for PulseMCP, mcp.so, MCP Market, LobeHub, and any directory where the form is broken,
paused, or absent. Keep it this short — these are one- and two-person teams triaging a lot of
mail, and the ask is transactional.*

**Subject:** `Listing the Modem MCP server on [Directory]`

> Hi `[name]`,
>
> I'm `[name]` from Modem. We've just shipped an MCP server and I'd like to get it listed on
> `[Directory]`.
>
> Modem auto-triages customer feedback — from Slack, Discord, support tickets, and GitHub
> issues — into prioritized topics. The MCP server exposes those topics to coding agents, so a
> developer can ask what users are actually blocked on and act on it in the same session,
> without a PM in the middle.
>
> - Server: `[https://mcp.modem.dev]` (remote, Streamable HTTP, OAuth 2.0)
> - Repo: `[https://github.com/modem-dev/mcp-server]`
> - Docs: `[https://modem.dev/docs/mcp]`
> - Official registry: `[dev.modem/modem]`
> - Icon + full metadata: `[link]`
>
> `[I tried the submit form at <url> but it looks like submissions are paused — happy to wait,
> just wanted to be in the queue.]`
>
> Anything else you need from me, say the word.
>
> `[Name]`
> `[title]`, Modem — `[email]`

---

## Template E — Metadata correction / claim request

*For directories that already scraped Modem and got it wrong, or where auto-indexing stalled.*

**Subject:** `Correcting the Modem listing on [Directory]`

> Hi `[name]`,
>
> Modem is listed at `[listing URL]`, but `[the description is out of date / the icon is missing
> / the install command is wrong / it hasn't picked up our latest release]`.
>
> Correct metadata:
>
> - Name: Modem
> - Description: `[one-liner]`
> - Server URL: `[url]` · Repo: `[url]` · Docs: `[url]`
> - Icon: `[url]`
> - Registry entry: `[dev.modem/modem]`
>
> I'm `[name]`, `[title]` at Modem — happy to verify ownership however you prefer `[GitHub
> OAuth / DNS TXT record / a note from our domain]`.
>
> Thanks,
> `[Name]`

---

## Template F — awesome-mcp-servers PR

**Title:** `Add Modem`

> Adds Modem under `[category]`.
>
> `- [modem-dev/mcp-server](https://github.com/modem-dev/mcp-server) 🎖️ ☁️ - Auto-triaged
> customer feedback from Slack, Discord, support tickets, and GitHub issues, exposed to coding
> agents as prioritized topics.`
>
> Server is published to the official MCP registry as `[dev.modem/modem]`. Follows the list's
> existing format and alphabetical ordering.

---

## Template G — Newsletter / editorial pitch (Tier 3, after listings are live)

*For PulseMCP's Weekly Pulse and similar. This is the one template that is not transactional —
it needs a reason to write about you beyond existing.*

**Subject:** `Modem MCP server — feedback triage as an agent primitive`

> Hi Tadas, Mike,
>
> `[Name]` from Modem. Our MCP server went live on `[date]` — it's in the official registry as
> `[dev.modem/modem]` and listed on `[Glama / Smithery / Docker]`.
>
> The angle I think is interesting for Weekly Pulse, beyond the launch: most MCP servers give
> agents access to *systems* — a database, a tracker, a repo. This one gives an agent access to
> *demand*. Modem clusters raw customer feedback into prioritized topics, so the agent's input
> is "here's what users are blocked on, with the affected companies attached" rather than "here's
> a ticket someone already wrote." In practice that moves the agent one step earlier in the
> product loop.
>
> `[Optional: an early number — "in the first N weeks, X% of issues our users' agents opened
> came straight from a triaged topic rather than a hand-written ticket."]`
>
> Happy to give you a demo workspace to poke at, or write up how we handle `[the interesting
> technical bit — clustering, OAuth scoping, whatever's genuinely novel]` if that's more useful
> than a listing blurb.
>
> `[Name]`
> `[title]`, Modem

---

## Template H — Follow-up nudge (7 days, once)

**Subject:** `Re: [original subject]`

> Hi `[name]` — following up on the Modem listing below. No rush if you're backed up; just let
> me know if anything's missing on my end and I'll get it over.
>
> `[Name]`

---

## Open items to confirm before sending anything

These could not be verified from here (`modem.dev` is unreachable from this environment) and
change which directories Modem is eligible for:

1. **Does the Modem MCP server exist and ship publicly yet?** All copy above is written as if
   it does.
2. **Remote or local?** Remote HTTPS + OAuth 2.0 is required for the Claude Connectors
   Directory and unlocks the Docker `type: remote` path. A local `npx` server is ineligible
   for the former.
3. **Public repo?** Glama, mcp.so, Cline, and the awesome-lists all require one. Without it,
   roughly half this list is closed.
4. **Privacy policy live?** Hard gate at Anthropic.
5. **Tool annotations shipped?** Hard gate at Anthropic; visible publicly via Glama's inspector.
6. **Named sender + reply-to address** for the email templates.
7. **PulseMCP submissions reopened?** Verify the submit page before emailing.
