# Cline MCP Marketplace

| | |
|---|---|
| Surface | https://github.com/cline/mcp-marketplace (issues) |
| Type | Gated — issue-based review (~a couple of days) |
| Linear | [DEV-4051](https://linear.app/modem-dev/issue/DEV-4051) (child of [DEV-3872](https://linear.app/modem-dev/issue/DEV-3872)) |
| Spot-check | Search the marketplace for Modem / modem.dev / dev.modem / modem-dev. Gated → a hit means someone else published under our name → **escalate**. |

## Why it matters

Cheapest of the gated client galleries — no portal, no PR review, just a GitHub issue. Cline
weighs community adoption, developer credibility, project maturity, and security. **Worth doing
the same day the repo flips public.**

## Prerequisites

- **[DEV-3869](https://linear.app/modem-dev/issue/DEV-3869)** public `modem-dev/mcp` repo URL — hard blocker
- **[DEV-3877](https://linear.app/modem-dev/issue/DEV-3877)** 400×400 PNG logo — hard blocker
- `llms-install.md` at the repo root (part of [DEV-3888](https://linear.app/modem-dev/issue/DEV-3888)) — helps Cline's auto-install through the OAuth step
- Short "why Cline users want it" rationale — draft in `modem-dev/mcp` `submissions/LISTING-COPY.md`

## Steps

1. Install the server end-to-end **in Cline, from the repo README** — the submission requires confirming this was done.
2. Open an issue on `cline/mcp-marketplace` using the `mcp-server-submission.yml` template with: public repo URL, 400×400 PNG logo, the rationale, and the end-to-end-install confirmation.
3. Track the issue; review typically lands within a couple of days.

## Done when

- Submission issue accepted; Modem appears in the Cline marketplace and auto-install works from `llms-install.md`
