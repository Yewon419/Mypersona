# Claude Code Integration

The reference implementation environment. Claude Code reads `CLAUDE.md` automatically on session start, which redirects to `PERSONA.md`. Filesystem access means the agent both **reads** and **writes** the wiki during conversation — full self-edit per the Letta pattern.

## Setup

```bash
git clone <your-fork-url> Mypersona
cd Mypersona
claude
```

That's it. Claude Code will:
- Read `CLAUDE.md` → redirect → load `PERSONA.md`
- Load `consciousness/*` and `subconscious/*` per the operating contract
- Append to `working/session_buffer.md` during reasoning
- Create new `memory/` pages as entities/concepts come up
- Promote at session end

## First run

If `PERSONA.md` still contains `{{slot}}` placeholders, ask Claude Code:

> *"Read `bootstrap.md` and run the 5-question setup."*

Claude Code will walk through the 5 questions, fill `PERSONA.md` + create `consciousness/identity.md`, `subconscious/style.md`, `subconscious/constraints.md`, and stub `memory/semantic/concepts/` pages for your domains. Commit + push when done.

## Why this is the canonical path

- **Write-back**: every other consumer-LLM integration is read-only. Claude Code is the only one where the persona actually grows during conversation without manual repo edits.
- **Reflection module fully active**: rolling importance sum is computed and reflections are written automatically when the threshold trips.
- **Git native**: commits and pushes happen from inside the session.
- **Schema authority**: `docs/frontmatter_schema.md` lint rules are enforced by the agent.

## Equivalent setups (same pattern)

- **Codex** — reads `AGENTS.md` (redirects to `PERSONA.md`)
- **Cursor** — reads `.cursorrules` (compressed version of `PERSONA.md`)

All three honor the same persona. Choose by tool preference; switching tools doesn't change the persona.

## After bootstrap

```bash
git add .
git commit -m "bootstrap: initial persona seeded"
git push
```

Every subsequent session starts from a populated persona.
