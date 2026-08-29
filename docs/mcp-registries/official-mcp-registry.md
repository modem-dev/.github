# Official MCP Registry

| | |
|---|---|
| Surface | https://registry.modelcontextprotocol.io |
| Type | Self-service publish, no human review (~1 hour) |
| Linear | [DEV-3868](https://linear.app/modem-dev/issue/DEV-3868) (**High**, Mike Clarke) — subtasks [DEV-3884](https://linear.app/modem-dev/issue/DEV-3884), [DEV-3885](https://linear.app/modem-dev/issue/DEV-3885), [DEV-3886](https://linear.app/modem-dev/issue/DEV-3886) |
| Spot-check | ⚠️ **Check first, before everything else** — see below |

## Why it matters most

The single highest-leverage listing: `registry.modelcontextprotocol.io` is the upstream feed
that GitHub's registry (→ VS Code/Copilot gallery), Docker Hub, Smithery, PulseMCP, and
Anthropic ingest. One `server.json` publish propagates furthest.

## ⚠️ The one that isn't reversible

`dev.modem` is a **first-come DNS-verified namespace**. Everything else on the registry list
can be corrected after the fact; a namespace taken by someone else cannot.

- Spot-check `dev.modem` / `modem` on the registry **before any other registry work**.
- If it's claimed by anyone other than us: **escalate immediately** — do not proceed as if it were a normal stale-listing case.

## Prerequisites

- [DEV-3880](https://linear.app/modem-dev/issue/DEV-3880): GA decision + server version `1.0.0` (we publish as `1.0.0`)
- Control of `modem.dev` DNS (for the TXT verification)
- Nothing else — the public repo and TLS work do **not** gate this publish (it's a `remotes` entry, not a repo listing)

## Steps

1. **Verify the `dev.modem` namespace via DNS** — [DEV-3884](https://linear.app/modem-dev/issue/DEV-3884)
   - Run `mcp-publisher login dns --domain modem.dev`; add the TXT record it asks for, proving control of modem.dev so we can publish under `dev.modem/*`. One-time setup.
2. **Author, validate, publish `server.json`** — [DEV-3885](https://linear.app/modem-dev/issue/DEV-3885)
   - Draft is in readiness report §5.2: name `dev.modem/modem`, `remotes` streamable-http entry for `https://mcp.modem.dev/mcp`, version `1.0.0`.
   - `mcp-publisher validate` against the **current** schema before `mcp-publisher publish`.
   - Verify the listing appears in the registry API.
3. **Gather registry-presence proof** — [DEV-3886](https://linear.app/modem-dev/issue/DEV-3886)
   - `server.json` passing `mcp-registry-validator` + `curl` output proving the server is live in the registry. Both are required by GitHub's onboarding request ([github-mcp-registry.md](github-mcp-registry.md)).

## Done when

- `curl` against the registry API returns the `dev.modem/modem` listing at `1.0.0`
- Validator output + curl proof archived for the GitHub onboarding request
- Downstream: PulseMCP/Smithery ingestion check scheduled ([DEV-3914](https://linear.app/modem-dev/issue/DEV-3914))
