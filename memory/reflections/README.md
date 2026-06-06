# memory/reflections/ — INACTIVE (2026-06-06)

> **Inactive under the role-split** (PERSONA.md §1). Auto-derived reflection is now the
> host's native background pass (Claude Code *Auto Dream* / Letta *sleeptime*), which does
> it automatically and better. Mypersona does not run its own reflection trigger.
> Additionally, faulty-memory research (`research/prior_art_synthesis.md §6`) found
> aggressive consolidation/rewrite *corrupts* memory — curated raw episodic beats it.
> The spec below is retained for historical reference only.

---

Higher-level inferences auto-derived from clusters of episodic and semantic pages. **What the persona now believes / notices, given accumulated experience.**

Per Stanford Generative Agents pattern. Without reflections, memory just grows — it doesn't get smarter. Reflections are what turn accumulation into **compounding**.

## File naming

`YYYY-MM-DD-slug.md` where `slug` is a 3–6 word kebab-case summary of the inference.

Examples:
- `2026-05-13-yewon-prefers-prior-art-verification.md`
- `2026-05-15-recurring-trading-system-risk-pattern.md`

## Frontmatter (required)

```yaml
---
type: reflection
created: YYYY-MM-DD
updated: YYYY-MM-DD
importance: 1-10
source: ["[[episodic/YYYY-MM-DD-foo]]", "[[semantic/concepts/bar]]"]
trigger: importance-threshold | manual | scheduled
tags: [tag, ...]
---
```

## Trigger rules

1. **`importance-threshold`** (default): rolling sum of `importance` across recent episodic + semantic additions crosses **30**. Threshold per Stanford pattern; tune after first month.
2. **`manual`**: user invokes `/reflect`.
3. **`scheduled`**: future cron pass (v2 feature, see `prior_art_synthesis.md §3.4`).

## Body structure

```
# Inference Title

## Observation
What pattern was noticed across the source pages?

## Inference
What does this imply about the user / their work / their preferences?

## Confidence
(low / medium / high) — with one sentence justifying

## Implications for the persona
How should this change the persona's default behavior, if at all?

## Sources
- [[source-page-1]] — what was drawn from it
- [[source-page-2]] — what was drawn from it
```

## Important constraint

Reflections may **propose** edits to `subconscious/style.md` or new `memory/semantic/concepts/` pages, but those edits require **user assent** before commit. Reflections themselves are filed automatically — their consequences are not.

`/lint` flags: two reflections within 24h with overlapping `source` arrays (likely redundant).
