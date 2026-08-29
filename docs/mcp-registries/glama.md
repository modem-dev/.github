# Glama

| | |
|---|---|
| Surface | https://glama.ai/mcp/servers |
| Type | Auto-crawled (indexes public GitHub repos) + claimable listing |
| Linear | [DEV-3902](https://linear.app/modem-dev/issue/DEV-3902) |
| Spot-check | Search Modem / modem.dev / dev.modem / modem-dev. Repo is private, so expected result: nothing. Note any stale or third-party entry; escalate if published by someone else. |

## How it works

Glama auto-indexes public GitHub repos — no submission needed once `modem-dev/mcp` is public.
A `glama.json` at the repo root controls the auto-indexed listing's metadata. Run by the same
founder as [awesome-mcp-servers](awesome-mcp-servers.md), which feeds Glama visibility.

## Prerequisites

- **[DEV-3869](https://linear.app/modem-dev/issue/DEV-3869)** public `modem-dev/mcp` repo — hard blocker; Glama has nothing to index until it exists

## Steps

1. Add `glama.json` to the public repo root (listing metadata; use the shared listing copy from readiness report §5.1).
2. Wait for auto-indexing to pick up the repo; verify the listing renders with our metadata.
3. **Claim the listing** for admin control.
4. For the curated **"remote MCP services"** list (closed-source hosted endpoints — our actual category), reach out on Glama's Discord.

## Done when

- Listing live with `glama.json`-controlled metadata, claimed by a Modem admin
- Remote-services curated-list request posted on Discord
