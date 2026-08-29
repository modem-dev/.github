# MCP Registry Implementation Docs

Implementation docs for getting the Modem MCP server (`https://mcp.modem.dev/mcp`) listed on
every registry in the [MCP Registry Spot-Check](https://app.notion.com/p/3ca2c5842de081629095d7afa5e67205)
(Notion), reconciled against the
[MCP Marketplace Listings](https://linear.app/modem-dev/project/mcp-marketplace-listings-9bf115cf52c4)
Linear project.

**Sources**

- Notion: [MCP Registry Spot-Check](https://app.notion.com/p/3ca2c5842de081629095d7afa5e67205) — row 13 of the Integration Marketplace Audit
- Linear: [MCP Marketplace Listings](https://linear.app/modem-dev/project/mcp-marketplace-listings-9bf115cf52c4) — 44 issues found at reconciliation time (2026-08-29; the Notion page says "45 tickets" — see [Reconciliation notes](#reconciliation-notes))
- Readiness report: [Notion report](https://app.notion.com/p/3c22c5842de081569f54c91fd56b90eb) · [styled artifact](https://claude.ai/code/artifact/24a53777-a050-4fb9-a8c4-5a2fc7950d94). §5.1–§5.6 hold the draft listing copy, `server.json`, portal answers, test cases, demo-org spec, and manifest drafts referenced throughout these docs. *(Not readable by the session that generated these docs — section references are cited, not inlined. Verify against the report before submitting anywhere.)*

## Start here

1. **[Shared prerequisites](00-prerequisites.md)** — the pre-flight work (assets, security/OAuth hardening, public repo, reviewer demo org) that gates most registries. Per the Notion page, the two hard blockers are the private `modem-dev/mcp` repo ([DEV-3869](https://linear.app/modem-dev/issue/DEV-3869)) and the TLS 1.0 `workers.dev` hostname ([DEV-3881](https://linear.app/modem-dev/issue/DEV-3881)) — together they gate roughly half the list.
2. **[Official MCP Registry](official-mcp-registry.md)** — the upstream feed. GitHub's registry (→ VS Code/Copilot gallery), Docker Hub, Smithery, PulseMCP, and Anthropic all ingest it, so this one publish propagates furthest. It is also the only **irreversible** item: `dev.modem` is a first-come DNS-verified namespace. Spot-check it first; if it's claimed by anyone other than us, escalate immediately.
3. Everything else, in the [order of operations](#order-of-operations) below.

## Reconciliation matrix

Every registry on the Notion spot-check list, mapped to its Linear coverage.

| Registry (Notion list) | Type | Linear ticket(s) | Status | Doc |
|---|---|---|---|---|
| Official MCP Registry | Auto-crawled upstream | [DEV-3868](https://linear.app/modem-dev/issue/DEV-3868) (High) + DEV-3884/3885/3886 | Backlog | [official-mcp-registry.md](official-mcp-registry.md) |
| Glama | Auto-crawled | [DEV-3902](https://linear.app/modem-dev/issue/DEV-3902) | Backlog | [glama.md](glama.md) |
| PulseMCP | Auto-ingests official registry | [DEV-3914](https://linear.app/modem-dev/issue/DEV-3914) | Backlog | [pulsemcp.md](pulsemcp.md) |
| Smithery | Auto-ingests official registry | [DEV-3914](https://linear.app/modem-dev/issue/DEV-3914) | Backlog | [smithery.md](smithery.md) |
| mcp.so | Form submission | [DEV-3913](https://linear.app/modem-dev/issue/DEV-3913) | Backlog | [mcp-so.md](mcp-so.md) |
| MCP Market | Form submission | [DEV-3915](https://linear.app/modem-dev/issue/DEV-3915) | Backlog | [mcp-market.md](mcp-market.md) |
| LobeHub | CLI submission + repo verification | [DEV-3915](https://linear.app/modem-dev/issue/DEV-3915) | Backlog | [lobehub.md](lobehub.md) |
| mcpservers.org | Form submission | [DEV-3913](https://linear.app/modem-dev/issue/DEV-3913) | Backlog | [mcpservers-org.md](mcpservers-org.md) |
| awesome-mcp-servers | GitHub PR | [DEV-3903](https://linear.app/modem-dev/issue/DEV-3903) | Backlog | [awesome-mcp-servers.md](awesome-mcp-servers.md) |
| Claude Connectors Directory | Gated (Anthropic review) | [DEV-3873](https://linear.app/modem-dev/issue/DEV-3873) (High) + DEV-3919/3921/3922 + demo-org DEV-3870/3916/3917/3918/3920 | Backlog | [claude-connectors-directory.md](claude-connectors-directory.md) |
| GitHub MCP Registry (+ VS Code/Copilot gallery) | Gated (manual curation) | [DEV-3871](https://linear.app/modem-dev/issue/DEV-3871) (High) + DEV-3886/3887 | Backlog | [github-mcp-registry.md](github-mcp-registry.md) |
| Cline Marketplace | Gated (issue-based review) | [DEV-4051](https://linear.app/modem-dev/issue/DEV-4051) | Backlog | [cline-marketplace.md](cline-marketplace.md) |
| Docker MCP Catalog | Gated (PR review) | [DEV-3904](https://linear.app/modem-dev/issue/DEV-3904) | Backlog | [docker-mcp-catalog.md](docker-mcp-catalog.md) |
| Cursor Marketplace | Gated (human review) | [DEV-3923](https://linear.app/modem-dev/issue/DEV-3923), parent [DEV-3874](https://linear.app/modem-dev/issue/DEV-3874) (Medium) | Backlog | [cursor-marketplace.md](cursor-marketplace.md) |
| OpenAI Plugin Directory (ChatGPT + Codex) | Gated (heaviest review) | [DEV-3875](https://linear.app/modem-dev/issue/DEV-3875) (Medium) + DEV-3925/3926/3927/3928 | Backlog (DEV-3927 In Progress) | [openai-plugin-directory.md](openai-plugin-directory.md) |

### In Linear but *not* on the Notion spot-check list

These have implementation tickets but no spot-check row. Docs are included here for completeness; consider adding rows to the Notion page so they get spot-checked too.

| Surface | Linear ticket(s) | Doc |
|---|---|---|
| Gemini CLI extensions gallery | [DEV-3901](https://linear.app/modem-dev/issue/DEV-3901) | [gemini-cli-extensions.md](gemini-cli-extensions.md) |
| Claude Code plugin marketplace | [DEV-3924](https://linear.app/modem-dev/issue/DEV-3924), parent [DEV-3874](https://linear.app/modem-dev/issue/DEV-3874) | [claude-code-plugin-marketplace.md](claude-code-plugin-marketplace.md) |
| Hermes catalog (NousResearch/hermes-agent) | [DEV-3906](https://linear.app/modem-dev/issue/DEV-3906) | [hermes-agent-catalog.md](hermes-agent-catalog.md) |
| MCP.Directory | [DEV-3915](https://linear.app/modem-dev/issue/DEV-3915) | [mcp-directory.md](mcp-directory.md) |

### Reconciliation notes

- **Ticket count**: the Notion page says the Linear project has 45 tickets; the project returned 44 open/backlog issues on 2026-08-29. Either one was archived/canceled since the page was written, or the page counted [DEV-4051](https://linear.app/modem-dev/issue/DEV-4051) before/after a rename. No registry is left uncovered either way.
- **Cline gap — closed**: the Notion list includes Cline; Linear originally had no submission ticket (only repo-scope coverage under DEV-3869). [DEV-4051](https://linear.app/modem-dev/issue/DEV-4051) was created 2026-08-27 to close that gap. ✅
- **Notion list gap — open**: Gemini CLI extensions, Claude Code plugin marketplace, Hermes catalog, and MCP.Directory are tracked in Linear but missing from the Notion spot-check checklist (see table above).
- **Every Notion registry has a Linear owner path.** No submission on the spot-check list is untracked.
- **Out of scope by project decision** (BD/partnership only, no submit path): Perplexity, Devin, xAI/Grok, Mistral Le Chat, Gemini consumer app, Composio partner program. Microsoft M365 Copilot Agent Store deferred.

## Order of operations

```
Phase 0  Spot-check dev.modem on the official registry (irreversible namespace — escalate if claimed)
Phase 1  Pre-flight: DEV-3866 (assets) ∥ DEV-3867 (security/OAuth) ∥ DEV-3869 (public repo) ∥ DEV-3870 (demo org)
Phase 2  Official registry publish: DEV-3884 → DEV-3885 → DEV-3868 done
Phase 3  Auto-ingest verification: PulseMCP, Smithery (DEV-3914); Glama claim (DEV-3902)
         Repo-triggered: Gemini topic crawl (DEV-3901), Cline same-day (DEV-4051)
Phase 4  Gated galleries: GitHub (DEV-3871), Claude (DEV-3873), OpenAI (DEV-3875),
         Cursor (DEV-3923), Claude Code plugin (DEV-3924), Docker (DEV-3904)
Phase 5  Long tail, one sitting: mcp.so + mcpservers.org (DEV-3913),
         MCP Market + LobeHub + MCP.Directory (DEV-3915), awesome-mcp-servers (DEV-3903),
         Hermes (DEV-3906)
```

## Spot-check protocol (applies to every doc)

From the Notion page — before submitting anywhere, search each registry for **Modem**, **modem.dev**, **dev.modem**, and **modem-dev**:

- **Found, published by Modem** → already listed; don't resubmit. Check the metadata is current.
- **Found, published by someone else** → escalate immediately (don't tick the box).
- **Not found** → proceed with the submission steps in the registry's doc.

`modem-dev/mcp` is still private, so for the auto-crawled registries the expected answer is "nothing" — but check rather than assume, and note any stale or third-party entry.

## Shared server facts

| | |
|---|---|
| Endpoint | `https://mcp.modem.dev/mcp` (remote, streamable-http, POST-only SSE-framed — no GET listening stream, no sessions) |
| Auth | OAuth 2.0 with Dynamic Client Registration (DCR); PKCE supported |
| Registry name | `dev.modem/modem`, publish as `1.0.0` |
| Tools | 11 (9 router write tools + `invoke_modem_agent` + `search_modem`) |
| Docs page | `apps/docs/api/modem-mcp-server.mdx` (monorepo) |
| Policies | `modem.dev/privacy-policy`, `modem.dev/terms-of-service`, `trust.modem.dev` |
| Brand | #079D7D; logo sources `apps/docs/logo/{light,dark}.svg` |
