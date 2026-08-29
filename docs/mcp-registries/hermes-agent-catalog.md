# Hermes Catalog (NousResearch/hermes-agent)

> Not on the Notion spot-check list — tracked in Linear only. Consider adding a spot-check row.

| | |
|---|---|
| Surface | `optional-mcps/` in https://github.com/NousResearch/hermes-agent |
| Type | GitHub PR — merged = approved; no other process |
| Linear | [DEV-3906](https://linear.app/modem-dev/issue/DEV-3906) |
| Spot-check | Search the repo for Modem / modem.dev / dev.modem / modem-dev. Expected: nothing. |

## Why it's easy

Our OAuth works zero-config there: Hermes uses Client ID Metadata Documents and falls back to
Dynamic Client Registration, which we support openly.

## Prerequisites

- None hard; a public repo/docs link target helps ([DEV-3869](https://linear.app/modem-dev/issue/DEV-3869))

## Steps

1. Fork `NousResearch/hermes-agent`.
2. Add a Modem manifest under `optional-mcps/`, mirroring an existing entry's shape, pointing at `https://mcp.modem.dev/mcp`.
3. Open the PR; merged = listed.

## Done when

- PR merged; Modem connectable from Hermes with zero OAuth config
