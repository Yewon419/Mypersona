# memory/semantic/

Facts, preferences, identity claims. **What is true.**

Maps to Tulving's semantic LTM. Sub-divided per Karpathy wiki convention to prevent flat-folder collapse past dozens of pages.

## Sub-folders

- `entities/` — people, organizations, projects, tools, products, places the persona knows about
- `concepts/` — ideas, frameworks, methodologies, beliefs, principles
- `synthesis/` — derived insights, comparisons, cross-cutting analyses (often produced by user queries that get filed back)

## Promotion source

- From `memory/episodic/`: explicit `/promote` only, no auto-promotion. (Per `prior_art_synthesis.md §3.3` — prevents drift.)
- Directly from user statements during conversation: "I prefer X" → semantic.
- From synthesis triggered by user query.

## Linking discipline

Every semantic page should be referenced from at least one other page (episodic that mentions it, another semantic page, or a synthesis). Orphan semantic pages are flagged by `/lint`.

`[[wikilink]]` syntax for cross-references. Match the target's filename slug.
