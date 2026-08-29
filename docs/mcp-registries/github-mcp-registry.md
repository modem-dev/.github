# GitHub MCP Registry (+ VS Code / Copilot gallery)

| | |
|---|---|
| Surface | https://github.com/mcp (~220 curated servers) — also feeds the in-product `@mcp` gallery in VS Code / GitHub Copilot |
| Type | Gated — manual curation by GitHub's product team, no SLA |
| Linear | [DEV-3871](https://linear.app/modem-dev/issue/DEV-3871) (**High**) — subtasks [DEV-3886](https://linear.app/modem-dev/issue/DEV-3886), [DEV-3887](https://linear.app/modem-dev/issue/DEV-3887) |
| Spot-check | Search github.com/mcp for Modem / modem.dev / dev.modem / modem-dev. Gated → a hit means someone else published under our name → **escalate**. |

## Why it matters

One manual onboarding request unlocks two surfaces: the curated github.com/mcp registry and
the VS Code / Copilot in-product gallery it feeds. Once onboarded, new registry versions sync
automatically from the official MCP registry.

## Prerequisites

- **[Official MCP Registry publish](official-mcp-registry.md)** ([DEV-3868](https://linear.app/modem-dev/issue/DEV-3868)) — hard prerequisite, confirmed by GitHub staff: publish upstream first
- **Proof pack** — [DEV-3886](https://linear.app/modem-dev/issue/DEV-3886): `server.json` passing `mcp-registry-validator` + `curl` output proving the server is live in the official registry
- Curation favors: stability, security practices, active maintenance, clear utility, comprehensive docs — the [pre-flight work](00-prerequisites.md) is indirect ammunition here

## Steps

1. Prepare the validator output and registry-presence `curl` proof ([DEV-3886](https://linear.app/modem-dev/issue/DEV-3886)).
2. **Post the onboarding request** — [DEV-3887](https://linear.app/modem-dev/issue/DEV-3887) — in the github-mcp-server discussion: https://github.com/github/github-mcp-server/discussions/1257. Include: registry name/namespace (`dev.modem/modem`), version, repo + docs links, validator/curl proof.
3. Track the thread until listed. Initial inclusion is manual curation (no SLA); after onboarding, version syncs are automatic.
4. Verify the listing appears both on github.com/mcp and in the VS Code / Copilot `@mcp` gallery.

## Done when

- `dev.modem/modem` visible on github.com/mcp and installable from the VS Code / Copilot gallery
