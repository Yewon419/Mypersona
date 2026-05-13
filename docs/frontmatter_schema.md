# Frontmatter Schema

Every persistent persona-wiki page (everything under `memory/`, `consciousness/`, `subconscious/`) MUST carry YAML frontmatter conforming to this schema. The agent reads these fields for retrieval scoring, reflection triggering, and lint.

## Universal fields (all page types)

```yaml
---
type: <one of the type values below>
created: YYYY-MM-DD            # ISO date, the day this page was first written
updated: YYYY-MM-DD             # last meaningful edit (auto-bump on agent edits)
importance: 1-10                # see §Importance scoring
tags: [tag1, tag2]              # kebab-case freeform tags
entities: ["[[entity-slug]]"]   # wiki-links to entities this page references
---
```

## Per-type required additions

### `type: episodic`
A time-stamped event memory. Filename: `YYYY-MM-DD-slug.md` inside `memory/episodic/`.
```yaml
participants: ["[[entity-slug]]"]   # who was involved (incl. the user themselves)
location: optional-string            # where, if relevant
```

### `type: semantic-entity`
A person, organization, project, tool, product. Filename: `slug.md` inside `memory/semantic/entities/`.
```yaml
canonical_name: "Full Name"
aliases: ["alt1", "alt2"]
category: person | org | project | tool | product | place
related: ["[[other-entity]]"]
```

### `type: semantic-concept`
An idea, framework, methodology, belief. Filename: `slug.md` inside `memory/semantic/concepts/`.
```yaml
canonical_name: "Concept Name"
related: ["[[other-concept]]"]
```

### `type: synthesis`
Derived insight, comparison, cross-cutting analysis. Filename: `slug.md` inside `memory/semantic/synthesis/`.
```yaml
sources: ["[[page1]]", "[[page2]]"]   # what this synthesis was built from
question: "the question that triggered this synthesis"
```

### `type: procedural`
A workflow, work rule, repeated pattern. Filename: verb-phrase `slug.md` inside `memory/procedural/`.
```yaml
trigger: "when does this procedure apply"
```

### `type: reflection`
Higher-level inference auto-derived from clusters of episodes/semantic pages. Filename: `YYYY-MM-DD-slug.md` inside `memory/reflections/`.
```yaml
source: ["[[episodic/2026-05-13-foo]]", "[[episodic/2026-05-14-bar]]"]
trigger: importance-threshold | manual | scheduled
```

### `type: consciousness-identity`
The persona's broadcast identity. Single file: `consciousness/identity.md`. Borrows SillyTavern V3 fields.
```yaml
name: "Persona Name"
description: "one-paragraph self-description"
personality: "trait list"
system_prompt: "the broadcast instruction"
first_mes: "default greeting"
mes_example: |
  example exchange showing voice
```

### `type: consciousness-active`
What the persona is currently focused on. Single file: `consciousness/active_context.md`. No extra fields beyond universal.

### `type: subconscious-style`
Tone, voice, expression patterns. File: `subconscious/style.md`.

### `type: subconscious-constraints`
Hard rules, never-dos. File: `subconscious/constraints.md`.

---

## Importance scoring (1–10)

Used for retrieval weighting and as the trigger for the Reflection module.

| Score | Meaning | Examples |
|---|---|---|
| 1–2 | Trivial / utility | mundane scheduling, one-off facts |
| 3–4 | Useful context | preferences, working details |
| 5–6 | Meaningful pattern or event | repeated workflows, notable interactions |
| 7–8 | Strong identity / commitment | core beliefs, major decisions, stable preferences |
| 9–10 | Defining / foundational | life-shaping events, foundational identity claims |

**Reflection trigger:** when the **rolling sum of `importance` across recent episodic+semantic additions** crosses **30**, the agent generates one reflection. (Threshold per Stanford pattern; adjust after first month of use.)

---

## Retrieval scoring formula

When the agent needs to load supporting memory for the current turn, it ranks candidate pages by:

```
score = α·relevance + β·recency + γ·importance
```

with defaults `α=0.5, β=0.2, γ=0.3` (relevance dominates, but importance pulls foundational pages forward; recency only as tie-breaker). Top-k retrieved (default k=5).

This is the **deterministic hybrid retrieval** referenced in `prior_art_synthesis.md §4`. Pure markdown — no vector embeddings required.

---

## Lint rules

The `/lint` command (Phase C) checks:
1. Every page has valid frontmatter conforming to its type.
2. No orphan entity/concept pages (each must be referenced from ≥1 other page).
3. No broken `[[wikilink]]` references.
4. `index.md` contains every persistent page.
5. No two reflections within 24h with overlapping sources.
6. `updated` date never precedes `created`.

Violations are logged to `log.md` with event-type `lint`.
