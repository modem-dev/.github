# OpenAI Plugin Directory (ChatGPT + ChatGPT Work + Codex)

| | |
|---|---|
| Surface | https://developers.openai.com/plugins — since July 2026 one unified directory covers ChatGPT, ChatGPT Work, and Codex: one submission, all three surfaces |
| Type | Gated — heaviest first-party lift (identity verification, domain challenge, automated tool scan, demo review) |
| Linear | [DEV-3875](https://linear.app/modem-dev/issue/DEV-3875) (Medium) — subtasks [DEV-3925](https://linear.app/modem-dev/issue/DEV-3925), [DEV-3926](https://linear.app/modem-dev/issue/DEV-3926), [DEV-3927](https://linear.app/modem-dev/issue/DEV-3927) (**In Progress**, Talton Figgins), [DEV-3928](https://linear.app/modem-dev/issue/DEV-3928) |
| Spot-check | Search the directory for Modem / modem.dev / dev.modem / modem-dev. Gated → a hit means someone else published under our name → **escalate**. |

## Hard blockers

- ⚠️ **Automated tool scan is blocked until the TLS 1.0 `workers.dev` twin is retired** — [DEV-3881](https://linear.app/modem-dev/issue/DEV-3881) under [DEV-3867](https://linear.app/modem-dev/issue/DEV-3867). Same class of finding that failed the Slack review.
- Explicit `readOnlyHint` / `openWorldHint` / `destructiveHint` on **every** tool — [DEV-3927](https://linear.app/modem-dev/issue/DEV-3927) (in progress; `invoke_modem_agent` and `search_modem` are missing `destructiveHint` at `apps/agent-gateway/src/routes/mcp/server.ts:314,411`).

## Prerequisites

- **Live transport confirmation first** — [DEV-3925](https://linear.app/modem-dev/issue/DEV-3925): add `mcp.modem.dev` as a custom connector in **ChatGPT developer mode** and run the full flow (OAuth connect, search, write, agent invoke). Our transport is POST-only SSE-framed (no GET listening stream, no sessions) — legal per spec but needs live confirmation against OpenAI's client. Also sanity-check Codex via `codex mcp add`.
- **Verified business identity + domain challenge** — [DEV-3926](https://linear.app/modem-dev/issue/DEV-3926): verified developer/business identity on the OpenAI platform (identity must match listing name, website, support contact, privacy policy, ToS) plus a completed domain-verification challenge for `mcp.modem.dev`. First figure out who holds the OpenAI org.
- **Demo org + OAuth demo credentials** ([00-prerequisites.md §4](00-prerequisites.md)); 64×64 PNG icon **under 5KB** ([DEV-3877](https://linear.app/modem-dev/issue/DEV-3877)); policy pages linked ([DEV-3878](https://linear.app/modem-dev/issue/DEV-3878)).

## Steps

1. Clear the blockers above (TLS retirement, annotations, dev-mode verification, identity/domain).
2. **Assemble the submission pack** — [DEV-3928](https://linear.app/modem-dev/issue/DEV-3928):
   - Demo recording URL. Take: OAuth connect → search query → topic update shown live in dashboard → disconnect.
   - **Exactly 5 positive + 3 negative test cases** with expected outcomes (drafts in readiness report §5.4; backed by the §5.5 demo data).
   - OAuth demo credentials (the demo org), release notes, the 64×64 icon.
3. Submit at https://developers.openai.com/plugins/deploy/submission — one submission covers ChatGPT, ChatGPT Work, and Codex.
4. Re-read the primary doc at submission time (research was partly second-hand).

## Done when

- Listing approved and live across ChatGPT, ChatGPT Work, and Codex; connector verified end-to-end in production ChatGPT
