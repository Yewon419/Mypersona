# Claude Code Integration

The reference environment. Claude Code reads `CLAUDE.md` automatically on session start, which redirects to `PERSONA.md`. Filesystem + git access means it can curate the KB directly (commit + push from inside the session) when you ask it to.

## Setup

```bash
git clone <your-fork-url> Mypersona
cd Mypersona
claude
```

That's it. Claude Code will:
- Read `CLAUDE.md` → redirect → load `PERSONA.md`
- Broadcast `consciousness/identity.md` + `subconscious/{style,constraints}.md`
- Curate `memory/` only on explicit intent (PERSONA.md §1)

> **Short-term memory note**: Claude Code has its own native auto-memory (`~/.claude/.../memory/`) that records session work and consolidates in the background. Mypersona deliberately does **not** duplicate that — it holds the portable persona + a thin curated KB. See `../../research/prior_art_synthesis.md §6`.

## First run

If `PERSONA.md` still contains `{{slot}}` placeholders, ask Claude Code:

> *"Read `bootstrap.md` and run the 5-question setup."*

It will walk through the 5 questions, fill `PERSONA.md`, and create `consciousness/identity.md`, `subconscious/style.md`, `subconscious/constraints.md`, and stub `memory/semantic/entities/` pages for your domains. Commit + push when done.

## Equivalent setups (same pattern)

- **Codex** — reads `AGENTS.md` (redirects to `PERSONA.md`)
- **Cursor** — reads `.cursorrules` (redirects to `PERSONA.md`)

All three honor the same persona. Switching tools doesn't change it.

## After bootstrap

```bash
git add .
git commit -m "bootstrap: initial persona seeded"
git push
```

Every subsequent session starts from a populated persona.
