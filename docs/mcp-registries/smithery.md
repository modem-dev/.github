# Smithery

| | |
|---|---|
| Surface | https://smithery.ai |
| Type | Auto-ingests the official MCP registry; optional external-MCP lane |
| Linear | [DEV-3914](https://linear.app/modem-dev/issue/DEV-3914) (shared with PulseMCP) |
| Spot-check | Search Modem / modem.dev / dev.modem / modem-dev. Expected: nothing until the official-registry publish. Escalate any third-party entry. |

## How it works

Smithery ingests the official MCP registry, so after the [official registry publish](official-mcp-registry.md)
our listing should appear automatically — verify, claim, and enrich rather than submitting cold.

Separately, Smithery's **external-MCP lane** wants a `/.well-known/mcp-config` served at our
domain (`mcp.modem.dev`). That's an open decision.

## Prerequisites

- [Official MCP Registry publish](official-mcp-registry.md) ([DEV-3868](https://linear.app/modem-dev/issue/DEV-3868)) completed

## Steps

1. After the registry publish, verify the ingested listing appears on smithery.ai.
2. Claim and enrich it (listing copy §5.1, logos from [DEV-3877](https://linear.app/modem-dev/issue/DEV-3877)).
3. **Decide**: add `/.well-known/mcp-config` at `mcp.modem.dev` for their external-MCP lane, or rely on the ingested listing. If added, it lives next to the other well-known endpoints being touched in [DEV-3883](https://linear.app/modem-dev/issue/DEV-3883) (`apps/agent-gateway/src/routes/mcp/`) — cheap to bundle into that change.

## Done when

- Listing visible on smithery.ai, claimed, metadata current
- `/.well-known/mcp-config` decision recorded on [DEV-3914](https://linear.app/modem-dev/issue/DEV-3914) (and implemented if yes)
