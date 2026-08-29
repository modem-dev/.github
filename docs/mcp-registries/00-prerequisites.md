# Shared Prerequisites (Pre-flight)

Cross-cutting work that gates the registry submissions. Nothing in this doc is a listing
itself — but per the Notion spot-check page, two items here (the private repo and the TLS 1.0
hostname) gate roughly half the registry list.

## 1. Public `modem-dev/mcp` repo — [DEV-3869](https://linear.app/modem-dev/issue/DEV-3869) (Medium, Ben Vinegar)

The monorepo is private; a small public repo unlocks every repo-based directory in one move:
Gemini CLI extensions (crawled daily via topic), Cline, Glama auto-indexing, LobeHub, and a
canonical link target for the awesome-lists.

Contents (drafts in readiness report §5.6):

- README with per-client install docs, mirroring `apps/docs/api/modem-mcp-server.mdx` — [DEV-3888](https://linear.app/modem-dev/issue/DEV-3888)
- `llms-install.md` at repo root so Cline can self-install (helps its auto-install through the OAuth step) — [DEV-3888](https://linear.app/modem-dev/issue/DEV-3888)
- `gemini-extension.json` (remote server via `httpUrl: https://mcp.modem.dev/mcp`) + GitHub topic `gemini-cli-extension` — [DEV-3901](https://linear.app/modem-dev/issue/DEV-3901)
- `glama.json` controlling Glama's auto-indexed listing metadata — [DEV-3902](https://linear.app/modem-dev/issue/DEV-3902)
- Committed square logo assets so directories have a stable raw URL — [DEV-3888](https://linear.app/modem-dev/issue/DEV-3888)

**Unblocks:** Cline ([DEV-4051](https://linear.app/modem-dev/issue/DEV-4051)), Gemini, Glama claim, LobeHub, awesome-mcp-servers link target.

## 2. Security & OAuth hardening — [DEV-3867](https://linear.app/modem-dev/issue/DEV-3867) (High, Mike Clarke)

Fixes a security reviewer would flag. Blocks the OpenAI submission (automated tool scan) and
de-risks Anthropic's policy scan.

- **Retire the TLS 1.0 `workers.dev` twin** — [DEV-3881](https://linear.app/modem-dev/issue/DEV-3881). `modem-agent-gateway.modem-dev.workers.dev` serves the identical `/mcp` endpoint and accepts TLS 1.0/1.1 (the `workers.dev` zone floor isn't ours to set) — byte-for-byte the finding that failed Slack's review ([DEV-3668](https://linear.app/modem-dev/issue/DEV-3668)). `workers_dev: true` is load-bearing for internal traffic, so: migrate internal consumers to a custom services domain (e.g. `agent-gateway.services.modem.dev`), then disable `workers.dev`. Verify with the forced-TLS-1.0 handshake from `.agents/rules/cloudflare.md`.
- **Tighten OAuth defaults** — [DEV-3882](https://linear.app/modem-dev/issue/DEV-3882). DCR default scope currently grants anonymous self-registered clients `agent:invoke` (full write + agent-run; `packages/auth/src/auth.ts:1351`) → default to `data:read`. Enforce PKCE (`requirePkce` unset today; MCP's OAuth spec mandates it for public clients).
- **OAuth discovery cheap wins** — [DEV-3883](https://linear.app/modem-dev/issue/DEV-3883). Bare `/.well-known/oauth-protected-resource` and `/.well-known/oauth-authorization-server` both 404 (legacy-client fallback paths); protected-resource metadata omits `resource_name`/`resource_documentation` (directories surface both). A few lines each in `apps/agent-gateway/src/routes/mcp/`.

**Unblocks:** OpenAI tool scan ([DEV-3875](https://linear.app/modem-dev/issue/DEV-3875)); de-risks Claude ([DEV-3873](https://linear.app/modem-dev/issue/DEV-3873)).

## 3. Listing assets & metadata — [DEV-3866](https://linear.app/modem-dev/issue/DEV-3866) (High, Mike Clarke)

Everything the directories render or check before any submission. Reference: readiness report §1 blockers 3–4, §4 step 1.

- **Tool/server titles** — [DEV-3876](https://linear.app/modem-dev/issue/DEV-3876). No tool (or the server) declares a `title`, so listings render raw `snake_case`. Claude's checklist requires titles on every tool. Sites: `apps/agent-gateway/src/routes/mcp/server.ts`, `packages/api/src/agent-tools/mcp-router-tools.ts`.
- **Explicit `destructiveHint` on every tool** — [DEV-3927](https://linear.app/modem-dev/issue/DEV-3927) (**In Progress**, Talton Figgins). `invoke_modem_agent` and `search_modem` are missing it (`apps/agent-gateway/src/routes/mcp/server.ts:314,411`). Required by OpenAI's tool scan; satisfies Claude's annotation checklist.
- **Square logo exports** — [DEV-3877](https://linear.app/modem-dev/issue/DEV-3877). Needed: 1:1 SVG (Claude), 64×64 PNG < 5KB (OpenAI), 400×400 PNG (Cline). Brand #079D7D. Only `apps/docs/logo/{light,dark}.svg` + favicon exist today.
- **Policy links on docs site** — [DEV-3878](https://linear.app/modem-dev/issue/DEV-3878) (**In Progress**, Talton Figgins). Pages exist but aren't linked from `apps/docs` (`docs.json` has no policy links). Add footer links + a policies row on `apps/docs/api/modem-mcp-server.mdx`.
- **Data-retention language** — [DEV-3879](https://linear.app/modem-dev/issue/DEV-3879). Claude's review requires the privacy policy to explicitly describe retention. Legal check; amend if missing.
- **Beta→GA + version 1.0.0** — [DEV-3880](https://linear.app/modem-dev/issue/DEV-3880). MCP surface is badged "Beta" and reports `version: 0.1.0`; directories generally want GA. Product decision + trivial code change.

**Unblocks:** every gated gallery; listing quality everywhere else.

## 4. Reviewer demo org + credentials — [DEV-3870](https://linear.app/modem-dev/issue/DEV-3870) (Medium, Mike Clarke)

Both reviewed directories require working demo credentials: Claude wants a test account valid
≥30 days with seeded data; OpenAI wants OAuth demo credentials for review + the demo recording.
One seeded demo org serves both.

- **Create `modem-review-demo` org + dedicated login** — [DEV-3916](https://linear.app/modem-dev/issue/DEV-3916). E.g. `mcp-review@modem.dev`, password in the vault, valid ≥30 days, not tied to a personal account, isolated from production customer data.
- **Seed demo data so every tool is demonstrable** — [DEV-3917](https://linear.app/modem-dev/issue/DEV-3917). ~15 topics across priorities/statuses (incl. one about "CSV export errors", several with recent activity), ~10 companies (one obvious duplicate pair), ~20 people (a "Jane Doe" duplicate pair), messages from ≥2 sources so `search_modem` cites sources. Spec: readiness report §5.5; also backs OpenAI's 5/3 test cases (§5.4).
- **Write reviewer connect instructions** — [DEV-3918](https://linear.app/modem-dev/issue/DEV-3918). Server URL, OAuth consent screen walkthrough, org-selection step, scopes to grant, one example prompt per tool family, note that writes are destructive-annotated and rate-limited.
- **Capture 3–5 listing screenshots** — [DEV-3920](https://linear.app/modem-dev/issue/DEV-3920). Shot list (readiness report §5.1): ① agent answering "what are customers saying about X" with cited topics ② topic updated from chat, shown in dashboard ③ OAuth consent screen with org selection ④ `search_modem` results in Claude ⑤ company 360° view. Use the demo org.

**Unblocks:** Claude ([DEV-3873](https://linear.app/modem-dev/issue/DEV-3873)) and OpenAI ([DEV-3875](https://linear.app/modem-dev/issue/DEV-3875)) submissions.

## Dependency summary

| Prerequisite | Gates |
|---|---|
| DEV-3869 public repo | Cline, Gemini, Glama, LobeHub, awesome-lists, Hermes link target |
| DEV-3881 TLS 1.0 retirement | OpenAI (hard), Claude (risk), every security-reviewed gallery |
| DEV-3877 logos | Claude (SVG), OpenAI (64×64), Cline (400×400), Cursor (committed logos) |
| DEV-3876/3927 titles + hints | Claude checklist, OpenAI tool scan |
| DEV-3878/3879 policies | Claude, OpenAI, most gated galleries |
| DEV-3880 GA + 1.0.0 | Official registry publish (`1.0.0`), gated galleries |
| DEV-3870 demo org | Claude, OpenAI |
| DEV-3884 DNS namespace | Official registry → GitHub, Docker, Smithery, PulseMCP |
