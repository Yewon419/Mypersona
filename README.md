# Mypersona

An **LLM-agnostic persona layer**: a portable, downloadable identity that any LLM
(Claude / ChatGPT / Gemini / Claude Code / Codex / Cursor) can adopt — plus a thin,
deliberately curated knowledge base. Plain markdown + git. No runtime.

Pattern derived from Andrej Karpathy's [LLM Wiki idea-file](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) (Apr 2026)
and brain-inspired layering (`consciousness/` identity, `subconscious/` style + hard
constraints). It started as a self-growing wiki; in 2026-06 it was **deliberately narrowed**
— short-term session memory is now handled by the host's native memory (e.g. Claude Code
auto-memory / Letta sleeptime), which does background consolidation automatically and better.
Mypersona keeps only what native, host-locked memory can't provide. See
[`research/prior_art_synthesis.md §6`](research/prior_art_synthesis.md).

## What it is (and isn't)

- **Is**: a portable persona (identity / voice / hard constraints) that pastes into any LLM,
  plus a small curated KB of facts worth carrying across hosts.
- **Isn't**: a session memory engine. Per-session observations, work logs, and project status
  belong to the host's native memory — Mypersona does not duplicate that.

## Quick start (5 minutes)

### Option A — Claude Code (recommended)

```bash
git clone https://github.com/{your-username}/Mypersona
cd Mypersona
claude
```

Then ask: *"read bootstrap.md and run the 5-question setup."* The agent fills `PERSONA.md`
and the persona files. Commit + push when done.

### Option B — Consumer LLM (ChatGPT / Claude.ai / Gemini)

1. Fork/clone, run `bootstrap.md` (via Claude Code) or fill the 5 answers manually.
2. Open `PERSONA.md`, copy its COMPACT section.
3. Paste into your LLM's instruction slot — per-tool guides:
   - ChatGPT: [`docs/integrations/chatgpt.md`](docs/integrations/chatgpt.md)
   - Claude Projects: [`docs/integrations/claude.md`](docs/integrations/claude.md)
   - Gemini Gems: [`docs/integrations/gemini.md`](docs/integrations/gemini.md)
4. (Optional) Always-latest sync: [`docs/integrations/url_fetch_addon.md`](docs/integrations/url_fetch_addon.md).

## File map

| | |
|---|---|
| `PERSONA.md` | Canonical entry. Contract + portable identity broadcast. |
| `bootstrap.md` | First-run 5-question setup (for forks). |
| `CLAUDE.md` / `AGENTS.md` / `.cursorrules` | Tool-specific entry files → redirect to `PERSONA.md`. |
| `consciousness/identity.md` | Always-broadcast identity. |
| `subconscious/` | Always-broadcast style + hard constraints. |
| `memory/semantic/entities/` | Curated KB pages. |
| `memory/procedural/` | Portable rules. |
| `memory/episodic/` | Static archive of past milestones (no new writes). |
| `docs/frontmatter_schema.md` | Page schema. |
| `docs/integrations/` | Per-tool setup guides. |
| `research/` | Design rationale (cognitive architecture + prior art audit). |

## Cost

Bring your own LLM (API key or subscription). Mypersona itself is markdown + git — free.

## License

MIT. Fork and adapt freely.

## Credits

- Andrej Karpathy — original LLM Wiki idea-file
- SillyTavern V3 — persona schema fields
- Squire, Tulving, Baddeley, Baars — cognitive architecture foundations
- Letta / MemGPT (sleeptime) & Claude Code (Auto Dream) — native background consolidation, the reason short-term memory was ceded
