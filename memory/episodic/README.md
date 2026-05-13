# memory/episodic/

Time-stamped event memories. **What happened, when, with whom.**

Maps to Tulving's episodic LTM.

## File naming

`YYYY-MM-DD-slug.md` where `slug` is a 2–6 word kebab-case event title.

Examples:
- `2026-05-13-mypersona-phase-a-complete.md`
- `2026-05-13-decided-pure-markdown-architecture.md`

## Frontmatter (required)

```yaml
---
type: episodic
created: YYYY-MM-DD
updated: YYYY-MM-DD
importance: 1-10
tags: [tag, ...]
entities: ["[[entity-slug]]"]
participants: ["[[entity-slug]]"]
location: optional
---
```

See `docs/frontmatter_schema.md` for full spec.

## Source

Episodes are **promoted from `working/session_buffer.md`** at session end (or on explicit `/promote`). They are not authored directly by the user in normal flow.

## What goes here vs. semantic

- "Yewon decided X on 5/13" → episodic
- "Yewon's stance on X is …" → semantic (concept)
- "X happened, and as a consequence Y is now true" → episodic page + linked semantic update
