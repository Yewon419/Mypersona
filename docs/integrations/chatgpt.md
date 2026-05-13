# ChatGPT Integration

Two paths: **Custom Instructions** (free tier compatible) and **Projects** (Plus/Pro).

## Path 1 — Custom Instructions

The fastest setup. Works on free tier. Applies globally to every ChatGPT conversation.

**Hard limit**: 1500 characters per field × 2 fields = 3000 chars total. The persona must fit in this budget.

### Steps

1. ChatGPT → Settings → Personalization → Custom Instructions.
2. Open `PERSONA.md` and locate the COMPACT section (between `<!-- COMPACT START -->` and `<!-- COMPACT END -->`).
3. **Field 1** ("What would you like ChatGPT to know about you?"): copy the **About this persona** subsection — everything from `### About this persona` up to (but not including) `### Behavior contract`.
4. **Field 2** ("How would you like ChatGPT to respond?"): copy the **Behavior contract** subsection — from `### Behavior contract` through the end of the COMPACT block.
5. If either overflows 1500 chars, trim non-essential bullets. Save.

### Update procedure

When PERSONA.md changes (e.g. after a reflection or identity edit), repeat steps 2–5. There is no auto-sync.

### Limitations

- Applies globally — affects every ChatGPT conversation, including unrelated ones.
- No access to wiki files. ChatGPT only sees the pasted COMPACT content.
- No write-back. ChatGPT cannot grow the persona during conversation; promotion is manual.

## Path 2 — Projects (Plus / Pro)

Higher capacity, scoped to a Project workspace.

### Steps

1. ChatGPT → New Project.
2. **Project Instructions**: paste the entire COMPACT section from PERSONA.md (no field-splitting needed).
3. **Project Knowledge** (drag-drop, up to 20 files): upload
   - `PERSONA.md`
   - `consciousness/identity.md` (after bootstrap)
   - `subconscious/style.md`, `subconscious/constraints.md`
   - `docs/frontmatter_schema.md`
   - Top `memory/semantic/` and `memory/procedural/` pages relevant to the Project's topic
4. Use the Project for any work where this persona should be active.

### Update procedure

When wiki files change, re-upload them to Project Knowledge (replaces existing). Manual.

### Limitations

- Scoped to this Project. Conversations outside don't see the persona.
- No live sync with the GitHub repo.
- No MCP support (as of 2026) — no filesystem access from inside ChatGPT.

## Recommendation

- One-shot try / casual use → **Custom Instructions**.
- Sustained topic-specific work → **Projects** with carefully chosen memory pages.
- Maximum capability with write-back → use **Claude Code** instead (see `claude_code.md`).
