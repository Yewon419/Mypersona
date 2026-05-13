# subconscious/

The persona's **implicit always-applied background** — tone, style, hard constraints. Always loaded, low salience: shapes behavior without dominating reasoning.

Maps to nondeclarative implicit memory (Squire taxonomy: priming + conditioning) and to SillyTavern's `personality` field plus system-level guardrails.

## Contents

- `style.md` (`type: subconscious-style`) — How the persona expresses itself. Voice, register, sentence rhythm, what it never says.
- `constraints.md` (`type: subconscious-constraints`) — Hard rules. Never-dos. Boundary conditions. Safety / dignity / privacy concerns.

## Rules for the agent

- **Always loaded** alongside `consciousness/` at turn start.
- Each file ≤ 400 tokens. If a constraint or style note doesn't fit, it probably belongs in `memory/procedural/` (specific workflow) or `memory/semantic/` (factual preference).
- `style.md` may be auto-updated by the agent when it observes a stable behavioral pattern from the user over **≥3 episodes** (proposal only — user confirms before commit, per the hybrid rule from `prior_art_synthesis.md §3.3`).
- `constraints.md` is **never** auto-edited. Only the user adds or removes constraints.

## What does NOT go here

- Specific facts about the user → `memory/semantic/`
- One-off events → `memory/episodic/`
- Reusable workflows → `memory/procedural/`
- Self-description the persona surfaces on request → `consciousness/identity.md`
