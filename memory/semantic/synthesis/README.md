# memory/semantic/synthesis/

Derived comparisons, cross-cutting analyses, insights produced by querying the wiki. **The output of thinking, filed back.**

Per Karpathy's pattern: when the user asks "compare X and Y" or "what do my notes say about Z?", the agent's answer is itself valuable — it should not disappear into chat history. File it here.

## File naming

`slug.md` — kebab-case description of the question or comparison.

Examples:
- `memgpt-vs-mem0-architecture.md`
- `recurring-style-preferences.md`
- `autostock-vs-hangsungdrone-risk-profiles.md`

## Frontmatter (required)

```yaml
---
type: synthesis
created: YYYY-MM-DD
updated: YYYY-MM-DD
importance: 1-10
question: "the question that triggered this synthesis"
sources: ["[[page1]]", "[[page2]]"]
tags: [tag, ...]
---
```

## Body structure

```
# Title

## Question
(verbatim or paraphrased)

## Answer
(the synthesis)

## Sources
- [[page1]] — what was drawn from it
- [[page2]] — what was drawn from it

## Caveats
(known limitations, missing perspectives, recency caveats)
```

## When NOT to file as synthesis

- The question was trivial and the answer is in a single existing page → just link to that page in the response, don't synthesize.
- The synthesis is mostly speculation with weak source backing → flag it in body's Caveats section, low `importance` (≤3).
