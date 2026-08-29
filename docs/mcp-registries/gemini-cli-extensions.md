# Gemini CLI Extensions Gallery

> Not on the Notion spot-check list — tracked in Linear only. Consider adding a spot-check row.

| | |
|---|---|
| Surface | Gemini CLI extensions gallery |
| Type | Auto-crawled — Google indexes GitHub repos tagged `gemini-cli-extension` daily; no submission form |
| Linear | [DEV-3901](https://linear.app/modem-dev/issue/DEV-3901) |
| Spot-check | Search the gallery for Modem / modem.dev / dev.modem / modem-dev. Expected: nothing until the public repo exists. |

## Prerequisites

- **[DEV-3869](https://linear.app/modem-dev/issue/DEV-3869)** public `modem-dev/mcp` repo — hard blocker (the manifest and topic live on it)

## Steps

1. Add `gemini-extension.json` at the repo root declaring the remote server via `httpUrl: https://mcp.modem.dev/mcp` (draft in readiness report §5.6).
2. Add the GitHub topic `gemini-cli-extension` to the repo.
3. Wait for the daily crawl; verify the listing appears in the Gemini CLI extensions gallery.

## Done when

- Listing visible in the gallery and installable from Gemini CLI
