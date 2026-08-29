# Claude Connectors Directory

| | |
|---|---|
| Surface | https://claude.ai/directory (Claude.ai / Desktop / mobile) |
| Type | Gated — portal submission, Anthropic policy scan + review (~2–3 weeks, free) |
| Linear | [DEV-3873](https://linear.app/modem-dev/issue/DEV-3873) (**High**, Mike Clarke) — subtasks [DEV-3919](https://linear.app/modem-dev/issue/DEV-3919), [DEV-3921](https://linear.app/modem-dev/issue/DEV-3921), [DEV-3922](https://linear.app/modem-dev/issue/DEV-3922); demo-org track [DEV-3870](https://linear.app/modem-dev/issue/DEV-3870) → DEV-3916/3917/3918/3920 |
| Spot-check | Search the directory for Modem / modem.dev / dev.modem / modem-dev. Gated by review, so a hit means someone else published under our name → **escalate**. |
| Escalation | mcp-review@anthropic.com |

## Why it matters

The biggest consumer-assistant MCP surface: one-click connect for Claude.ai / Desktop / mobile
users. Our OAuth (DCR) already meets the technical bar. Listings enter as a "community
connector" after Anthropic's policy scan.

## Prerequisites

- **Org access** — [DEV-3919](https://linear.app/modem-dev/issue/DEV-3919): the submission portal lives inside Claude.ai org settings and requires a **Team or Enterprise org** with Owner/Directory permission for whoever clicks submit. Confirm or create this before any other Claude submission work.
- **Assets & metadata** ([00-prerequisites.md §3](00-prerequisites.md)): tool/server titles ([DEV-3876](https://linear.app/modem-dev/issue/DEV-3876)) — Claude's checklist requires titles on every tool; 1:1 SVG logo ([DEV-3877](https://linear.app/modem-dev/issue/DEV-3877)); policy links on docs ([DEV-3878](https://linear.app/modem-dev/issue/DEV-3878)); **privacy policy must explicitly describe data retention** ([DEV-3879](https://linear.app/modem-dev/issue/DEV-3879)); destructive annotations ([DEV-3927](https://linear.app/modem-dev/issue/DEV-3927)).
- **Test account valid ≥30 days with seeded data** ([00-prerequisites.md §4](00-prerequisites.md)): demo org ([DEV-3916](https://linear.app/modem-dev/issue/DEV-3916)), seeded data ([DEV-3917](https://linear.app/modem-dev/issue/DEV-3917)), reviewer connect instructions ([DEV-3918](https://linear.app/modem-dev/issue/DEV-3918)), screenshots ([DEV-3920](https://linear.app/modem-dev/issue/DEV-3920)).
- Security hardening ([DEV-3867](https://linear.app/modem-dev/issue/DEV-3867)) de-risks the policy scan.

## Steps

1. **Re-read the primary doc + finalize portal answers** — [DEV-3921](https://linear.app/modem-dev/issue/DEV-3921). Draft answers in readiness report §5.3 (server URL, auth method, listing copy, logo, policies, test account, tool inventory note). The primary doc — https://claude.com/docs/connectors/building/submission — was corroborated **second-hand** during research; reconcile field-by-field before submitting.
2. **Submit via the in-product portal + track** — [DEV-3922](https://linear.app/modem-dev/issue/DEV-3922). Track status in the submissions dashboard. Expect the automated policy scan first; listing lands as a "community connector"; review timeline ~2–3 weeks. Escalate via mcp-review@anthropic.com if stuck.

## Done when

- Listing live in the Claude Connectors Directory as a community connector, one-click connect working end-to-end against `https://mcp.modem.dev/mcp`
