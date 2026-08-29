# LobeHub

| | |
|---|---|
| Surface | https://lobehub.com/mcp |
| Type | CLI submission with GitHub ownership verification |
| Linear | [DEV-3915](https://linear.app/modem-dev/issue/DEV-3915) (long-tail batch with MCP Market, MCP.Directory) |
| Spot-check | Search Modem / modem.dev / dev.modem / modem-dev. Expected: nothing. Escalate any third-party entry. |

## How it works

Submit via LobeHub's CLI: `lhm plugin submit <repo-url>`, which verifies GitHub ownership of
the submitted repo.

## Prerequisites

- **[DEV-3869](https://linear.app/modem-dev/issue/DEV-3869)** public `modem-dev/mcp` repo — hard blocker (the submission *is* the repo URL, and ownership verification runs against it)
- Shared listing copy (readiness report §5.1); logos committed to the repo ([DEV-3888](https://linear.app/modem-dev/issue/DEV-3888))

## Steps

1. Once the public repo exists, run `lhm plugin submit https://github.com/modem-dev/mcp`.
2. Complete the GitHub ownership verification as someone with admin on `modem-dev`.
3. Verify the listing renders with the repo's metadata/logos; batch alongside [MCP Market](mcp-market.md) and [MCP.Directory](mcp-directory.md).

## Done when

- Listing live on lobehub.com/mcp under Modem's verified ownership
