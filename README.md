# Mypersona

A LLM-agnostic persona-wiki: a downloadable, brain-inspired memory architecture that any LLM (Claude / ChatGPT / Gemini / Claude Code / Codex / Cursor) can adopt as its operating identity.

Pattern derived from Andrej Karpathy's [LLM Wiki idea-file](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) (Apr 2026), extended with:

- **Brain-inspired layering** — `consciousness/` (always-broadcast identity), `subconscious/` (style + hard constraints), `working/` (session scratch), `memory/{episodic,semantic,procedural,reflections}/` (long-term). Maps to the Squire/Tulving taxonomy and Global Workspace Theory.
- **Letta self-editing memory contract** — the agent writes to memory *during* reasoning, not after.
- **Stanford Generative Agents reflection module** — periodic synthesis turns accumulation into compounding.
- **LLM-agnostic by paste or fetch** — works in any tool that accepts a system prompt or instruction file.

## Quick start (5 minutes)

Pick the path that matches your primary LLM:

### Option A — Claude Code (recommended; full write-back)

```bash
git clone https://github.com/{your-username}/Mypersona
cd Mypersona
claude
```

Then ask: *"read bootstrap.md and run the 5-question setup."* The agent fills `PERSONA.md` and the persona files. Commit + push when done.

### Option B — Consumer LLM (ChatGPT / Claude.ai / Gemini)

1. Clone the repo locally (or fork it on GitHub).
2. Run `bootstrap.md` via Claude Code (Option A), or walk through the 5 questions manually and edit files yourself.
3. Open `PERSONA.md` and copy its COMPACT section.
4. Paste into your LLM's instruction slot — see the per-tool guides:
   - ChatGPT: [`docs/integrations/chatgpt.md`](docs/integrations/chatgpt.md)
   - Claude Projects: [`docs/integrations/claude.md`](docs/integrations/claude.md)
   - Gemini Gems: [`docs/integrations/gemini.md`](docs/integrations/gemini.md)
5. (Optional) For always-latest sync, add the one-liner from [`docs/integrations/url_fetch_addon.md`](docs/integrations/url_fetch_addon.md).

## What you get

A persona that:
- Has a defined identity and voice (`consciousness/`, `subconscious/`)
- Remembers events, facts, and workflows across sessions (`memory/`)
- Reflects on what it has accumulated and writes derived insights (`memory/reflections/`)
- Operates the same way whether hosted by Claude, ChatGPT, Gemini, or any other LLM with a system-prompt slot

## File map

| | |
|---|---|
| `PERSONA.md` | Canonical entry. Agent operating contract + portable identity broadcast. |
| `bootstrap.md` | First-run 5-question setup. |
| `CLAUDE.md` / `AGENTS.md` / `.cursorrules` | Tool-specific entry files. All redirect to `PERSONA.md`. |
| `consciousness/` | Always-broadcast identity + active context. |
| `subconscious/` | Always-broadcast style + hard constraints. |
| `working/` | Volatile session scratch (gitignored). |
| `memory/` | Long-term: episodic / semantic / procedural / reflections. |
| `docs/frontmatter_schema.md` | Full schema, retrieval formula, lint rules. |
| `docs/integrations/` | Per-tool setup guides. |
| `research/` | Design rationale (cognitive architecture + prior art audit). |

## Cost

You bring your own LLM (API key or consumer subscription). Mypersona itself is plain markdown + git — free, no runtime.

## License

MIT. Fork and adapt freely.

## Credits

- Andrej Karpathy — original LLM Wiki idea-file
- Park et al. (Stanford, 2023) — Generative Agents reflection module
- Letta / MemGPT — OS-inspired tiered memory & self-edit pattern
- SillyTavern V3 — persona schema fields
- Squire, Tulving, Baddeley, Baars — cognitive architecture foundations
