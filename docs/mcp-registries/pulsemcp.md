# PulseMCP

| | |
|---|---|
| Surface | https://www.pulsemcp.com/servers |
| Type | Auto-ingests the official MCP registry |
| Linear | [DEV-3914](https://linear.app/modem-dev/issue/DEV-3914) (shared with Smithery) |
| Spot-check | Search Modem / modem.dev / dev.modem / modem-dev. Expected: nothing until the official-registry publish. Escalate any third-party entry. |

## How it works

PulseMCP ingests the official MCP registry — after the [official registry publish](official-mcp-registry.md),
our listing should appear automatically. The play is **verify → claim → enrich**, not a cold submission.

## Prerequisites

- [Official MCP Registry publish](official-mcp-registry.md) ([DEV-3868](https://linear.app/modem-dev/issue/DEV-3868)) completed

## Steps

1. After the registry publish, wait for ingestion and verify the `dev.modem/modem` listing appears.
2. Claim the listing and enrich it with the §5.1 listing copy and logos.
3. **Known wrinkle**: PulseMCP submissions were reportedly paused during an ingestion rework ("until mid-August") — that window has now passed (today ≥ 2026-08-29); confirm current status when picking this up. If ingestion doesn't surface the listing, check whether their submission lane has reopened.

## Done when

- Listing visible on pulsemcp.com, claimed, with current metadata (title, description, logo, docs link)
