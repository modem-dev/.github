# Docker MCP Catalog

| | |
|---|---|
| Surface | https://hub.docker.com/u/mcp (Docker Desktop MCP Toolkit) |
| Type | Gated — PR review on `docker/mcp-registry`; live ~24h after approval |
| Linear | [DEV-3904](https://linear.app/modem-dev/issue/DEV-3904) |
| Spot-check | Search the catalog for Modem / modem.dev / dev.modem / modem-dev. Gated → a hit means someone else published under our name → **escalate**. |

## How it works

Fork `docker/mcp-registry` and run `task remote-wizard`, which generates `server.yaml`,
`tools.json`, and a README from the remote URL — no container image needed for a remote server.

## Prerequisites

- Listing copy (§5.1) and logos ([DEV-3877](https://linear.app/modem-dev/issue/DEV-3877))
- **Open question to resolve before submitting**: how Docker's license preference applies to a closed-source hosted service. Settle this first so the PR isn't bounced on policy.
- [Official registry publish](official-mcp-registry.md) helps (Docker Hub ingests the official registry) — check after that publish whether an ingested entry already exists before opening the PR

## Steps

1. Resolve the license-preference question for closed-source hosted services.
2. Fork `docker/mcp-registry`; run `task remote-wizard` against `https://mcp.modem.dev/mcp`.
3. Test the generated entry in Docker Desktop's MCP Toolkit (OAuth connect + a tool call).
4. Open the PR; respond to review. Listing goes live ~24h after approval.

## Done when

- Modem live under hub.docker.com/u/mcp and connectable from Docker Desktop's MCP Toolkit
