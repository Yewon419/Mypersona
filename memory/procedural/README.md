# memory/procedural/

Workflows, work rules, repeated patterns. **How to do things.**

Maps to Squire's nondeclarative procedural memory.

## File naming

`slug.md` — verb-phrase preferred (action-oriented).

Examples:
- `start-new-coding-task.md`
- `commit-and-push.md`
- `respond-to-ambiguous-scope.md`

## Frontmatter (required)

```yaml
---
type: procedural
created: YYYY-MM-DD
updated: YYYY-MM-DD
importance: 1-10
trigger: "when does this procedure apply"
tags: [tag, ...]
related: ["[[other-procedural]]"]
---
```

The `trigger` field is critical — it's what the agent matches against the current situation to decide whether to load this procedure.

## Body structure (recommended)

```
# Procedure Name

## When to apply
(restatement / elaboration of trigger)

## Steps
1. …
2. …

## Edge cases
- bullet

## Anti-patterns
- bullet
```

## Promotion source

**User-triggered only.** Procedural memory is rule-shaped — auto-extracting rules from observed behavior is error-prone. When the user says "from now on, always do X" or "the way to do Y is …", that's the cue to write here.

Compare with `subconscious/style.md`: style patterns are inferred (with user confirmation); procedural rules are stated.
