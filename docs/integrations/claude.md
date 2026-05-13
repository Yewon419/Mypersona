# Claude Integration (claude.ai Projects)

This guide covers **Claude on the web** (claude.ai Pro). For the CLI tool, see `claude_code.md`.

Highest-capacity paste option among consumer LLM products. Custom Instructions limit is generous; Knowledge accepts files and URLs.

## Steps

1. claude.ai → Projects → Create Project.
2. **Custom Instructions**: paste the entire content of `PERSONA.md` (Claude handles the full file, not just COMPACT).
3. **Project Knowledge**:
   - **Files**: upload key wiki files — `consciousness/identity.md`, `subconscious/style.md`, `subconscious/constraints.md`, `docs/frontmatter_schema.md`, and any `memory/semantic/` or `memory/procedural/` pages you want available.
   - **URLs**: add GitHub raw URLs (e.g. `https://raw.githubusercontent.com/{user}/Mypersona/master/PERSONA.md`). Claude fetches once at add-time.
4. Open any conversation inside the Project. The persona is active.

## Update procedure

- **Custom Instructions**: paste the updated `PERSONA.md` content.
- **Knowledge files**: re-upload the changed file (replaces previous).
- **Knowledge URLs**: re-add to force re-fetch (Claude does not auto-refresh URL knowledge).

## Limitations

- URL knowledge is **fetched once**, not live. Treat it as a snapshot.
- Scoped to the Project — conversations outside don't see the persona.
- No filesystem write. Claude can describe what should go into `memory/episodic/` but can't commit it. Writing back happens via Claude Code on the local clone, or manually.

## Recommendation

claude.ai Projects is the best **consumer-LLM** path for Mypersona. Strong instruction adherence, large knowledge capacity, URL support. If you need write-back to the repo, switch to Claude Code (see `claude_code.md`).
