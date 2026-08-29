# Cursor Marketplace

| | |
|---|---|
| Surface | https://cursor.com/marketplace |
| Type | Gated — human-reviewed by the Cursor team |
| Linear | [DEV-3923](https://linear.app/modem-dev/issue/DEV-3923) (child of [DEV-3874](https://linear.app/modem-dev/issue/DEV-3874), Medium) |
| Spot-check | Search the marketplace for Modem / modem.dev / dev.modem / modem-dev. Gated → a hit means someone else published under our name → **escalate**. |

## Why it matters

Dev-ICP marketplace. Remote MCP + OAuth is supported — users get one-click **"Add to Cursor"**
against our existing remote server; the plugin is a thin wrapper.

## Prerequisites

- Square logo assets committed ([DEV-3877](https://linear.app/modem-dev/issue/DEV-3877))
- Draft `.cursor-plugin/plugin.json` in readiness report §5.6

## Steps

1. Package via `cursor/plugin-template`:
   - `.cursor-plugin/plugin.json` (§5.6 draft), **kebab-case name**, committed logos
   - Pass their validator: `scripts/validate-template.mjs`
2. Submit at https://cursor.com/marketplace/publish.
3. Track the human review; respond to feedback.

## Done when

- Listing live with working one-click "Add to Cursor" (OAuth connect + tool call verified)

## See also

- [claude-code-plugin-marketplace.md](claude-code-plugin-marketplace.md) — the sibling thin plugin under the same parent ticket ([DEV-3874](https://linear.app/modem-dev/issue/DEV-3874))
