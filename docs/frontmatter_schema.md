# Frontmatter Schema

Every page under `memory/`, `consciousness/`, `subconscious/` carries YAML frontmatter
conforming to this schema. Kept minimal — after the role-split (PERSONA.md §1, see
`../research/prior_art_synthesis.md §6`) Mypersona is a portable persona layer + a thin
curated KB, not a self-growing wiki, so the retrieval/reflection/lint machinery is gone.

## Universal fields (all page types)

```yaml
---
type: <one of the type values below>
created: YYYY-MM-DD            # the day this page was first written
updated: YYYY-MM-DD            # last meaningful edit
importance: 1-10              # curation priority (see below)
tags: [tag1, tag2]           # kebab-case freeform tags
entities: ["[[entity-slug]]"] # wiki-links to entities this page references
---
```

## Per-type required additions

### `type: consciousness-identity`
The persona's broadcast identity. Single file: `consciousness/identity.md`. SillyTavern V3 fields.
```yaml
name: "Persona Name"
description: "one-paragraph self-description"
personality: "trait list"
system_prompt: "the broadcast instruction"
first_mes: "default greeting"
mes_example: |
  example exchange showing voice
```

### `type: subconscious-style` / `type: subconscious-constraints`
Voice/expression (`subconscious/style.md`) and hard rules (`subconscious/constraints.md`).
No extra fields beyond universal.

### `type: semantic-entity`
A person, organization, project, tool, product. Filename: `slug.md` in `memory/semantic/entities/`.
```yaml
canonical_name: "Full Name"
aliases: ["alt1", "alt2"]
category: person | org | project | tool | product | place
related: ["[[other-entity]]"]
```

### `type: procedural`
A portable workflow or rule. Filename: verb-phrase `slug.md` in `memory/procedural/`.
```yaml
trigger: "when this rule applies"
```

### `type: episodic`
A dated past milestone. Filename: `YYYY-MM-DD-slug.md` in `memory/episodic/`.
**Static archive only** — new session memory goes to the host's native auto-memory, not here.

---

## Importance (1–10)

Curation priority — how much this page matters when deciding what to keep or surface.

| Score | Meaning |
|---|---|
| 1–2 | Trivial / utility |
| 3–4 | Useful context |
| 5–6 | Meaningful pattern or event |
| 7–8 | Strong identity / commitment, major decision |
| 9–10 | Defining / foundational |
