# Claude Code Plugin Marketplace

> Not on the Notion spot-check list (only the Claude Connectors Directory is) — tracked in
> Linear only. Distinct surface: `/plugin` Discover in Claude Code and Cowork, not claude.ai.

| | |
|---|---|
| Surface | `/plugin` Discover in Claude Code and Cowork |
| Type | Gated — automated security scan → Anthropic approval |
| Linear | [DEV-3924](https://linear.app/modem-dev/issue/DEV-3924) (child of [DEV-3874](https://linear.app/modem-dev/issue/DEV-3874), Medium) |
| Spot-check | Search `/plugin` Discover for Modem / modem.dev / dev.modem / modem-dev. Gated → a hit means someone else published under our name → **escalate**. |

## How it works

A thin plugin wrapping the remote server:

- `.claude-plugin/plugin.json`
- Bundled MCP config pointing at `https://mcp.modem.dev/mcp`
- Optionally a skill with Modem usage guidance

Submit at https://clau.de/plugin-directory-submission.

## ⚠️ Naming is immutable

Plugin names cannot be changed once published — pick carefully before submitting.

## Prerequisites

- Draft `plugin.json` in readiness report §5.6; logos ([DEV-3877](https://linear.app/modem-dev/issue/DEV-3877))
- Name decision recorded on [DEV-3924](https://linear.app/modem-dev/issue/DEV-3924)

## Steps

1. Build the plugin package (`plugin.json` + MCP config + optional skill).
2. Submit; pass the automated security scan; await Anthropic approval.
3. Verify it surfaces in `/plugin` Discover and the bundled config connects (OAuth + tool call).

## Done when

- Plugin discoverable and installable in Claude Code and Cowork

## See also

- [cursor-marketplace.md](cursor-marketplace.md) — sibling thin plugin under [DEV-3874](https://linear.app/modem-dev/issue/DEV-3874)
- [claude-connectors-directory.md](claude-connectors-directory.md) — the claude.ai consumer surface (separate submission, separate review)
