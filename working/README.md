# working/ — DEPRECATED (2026-06-06)

> **Inactive under the role-split** (PERSONA.md §1). Short-term session memory now
> belongs to the host's native auto-memory (Claude Code `~/.claude/.../memory/`), which
> runs an automatic background consolidation pass. The agent **no longer maintains
> `session_buffer.md`** and no longer promotes from it. Past contents were archived to
> `memory/episodic/2026-05-23_2026-05-30-session-archive.md`. The rules below describe
> the retired contract, kept for historical reference only.

---

**Per-session volatile scratch.** Gitignored. Baddeley's episodic buffer analogue + Letta's Recall Memory pre-promotion area.

## Contents

- `session_buffer.md` — the current session's running log. Observations, decisions, partial reflections, things to consider promoting.

## Rules for the agent

- Read at the start of every session if it exists. Treat as continuity from the prior unconsolidated session.
- Append observations during the session (timestamps optional but recommended at major shifts).
- At session end (or on explicit `/promote`), the agent:
  1. Extracts the day's events → writes one or more `memory/episodic/YYYY-MM-DD-*.md` pages with `importance` scored
  2. If new stable facts emerged → writes/updates `memory/semantic/` pages
  3. If a behavioral pattern was observed ≥3 times → proposes `subconscious/style.md` edit (user confirms)
  4. Appends one line per promotion to `log.md`
  5. **Clears `session_buffer.md`** (truncates to empty header)

## Why gitignored

Working memory is volatile by nature. Committing every session's raw scratch would pollute history without preserving anything that wasn't already promoted to long-term storage. The promotion *is* the durable record.

## What goes here vs. memory/

- Did it happen? Was it observed? → working buffer first, then promoted to `memory/episodic/`
- Was it explicitly stated as a stable fact? → directly to `memory/semantic/`, skip working
