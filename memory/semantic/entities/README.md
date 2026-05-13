# memory/semantic/entities/

People, organizations, projects, tools, products, places.

## File naming

`slug.md` — kebab-case of canonical name. Use the most common short form.

Examples:
- `yewon.md` (the user)
- `karpathy.md`
- `autostock.md`
- `claude-code.md`

## Frontmatter (required)

```yaml
---
type: semantic-entity
created: YYYY-MM-DD
updated: YYYY-MM-DD
importance: 1-10
canonical_name: "Full Name"
aliases: ["alt1", "alt2"]
category: person | org | project | tool | product | place
tags: [tag, ...]
related: ["[[other-entity]]"]
---
```

## Body structure (recommended)

```
# Canonical Name

One-line characterization.

## What
(2–4 sentences)

## Relationship to user
(why the persona tracks this entity)

## Key facts
- bullet
- bullet

## Related episodes
- [[episodic/YYYY-MM-DD-slug]]
```

Sections are not enforced — adapt to what's useful. But include backlinks to episodes that mention this entity.
