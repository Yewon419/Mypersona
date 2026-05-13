# memory/semantic/concepts/

Ideas, frameworks, methodologies, beliefs, principles. **Named abstractions.**

## File naming

`slug.md` — kebab-case of canonical name.

Examples:
- `compounding-knowledge.md`
- `scope-discipline.md`
- `pre-report-principle.md`

## Frontmatter (required)

```yaml
---
type: semantic-concept
created: YYYY-MM-DD
updated: YYYY-MM-DD
importance: 1-10
canonical_name: "Concept Name"
tags: [tag, ...]
related: ["[[other-concept]]"]
entities: ["[[entity-slug]]"]
---
```

## Body structure (recommended)

```
# Concept Name

## Definition
One paragraph.

## Why it matters to the user
Connection to user's work or worldview.

## Operating rules / heuristics
- bullet

## Related episodes
- [[episodic/YYYY-MM-DD-slug]]
```

## Entity vs concept — disambiguation

- Has a proper name and exists in the world? → entity
- Is an abstraction the user invokes or applies? → concept
- Edge case (e.g., "AutoStock" — both a project and a methodology): create an entity page, and a separate concept page if the *idea* of it is reused beyond the project.
