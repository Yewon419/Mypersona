# consciousness/

The persona's **conscious surface** — what the agent broadcasts about itself every turn (Global Workspace Theory broadcast layer, Letta Core Memory analogue).

## Contents

- `identity.md` (`type: consciousness-identity`) — Who the persona is. Uses SillyTavern V3 fields: `name`, `description`, `personality`, `system_prompt`, `first_mes`, `mes_example`. This is the single most load-bearing file in the repo.
- `active_context.md` (`type: consciousness-active`) — What the persona is currently focused on. Updated turn-by-turn or session-by-session.

## Rules for the agent

- **Always loaded** into the LLM context at the start of every turn.
- Keep concise — these consume token budget on every prompt. Identity ≤ 500 tokens, active context ≤ 300 tokens.
- Edits to `identity.md` require **explicit user assent** (foundational identity is not auto-revised by reflection).
- `active_context.md` may be auto-updated by the agent at session boundaries.

## When does a new conscious-layer file get added?

It doesn't. v1 fixes this folder to two files. Adding a third would dilute the broadcast.
