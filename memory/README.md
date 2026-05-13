# memory/

Long-term persistent storage. Four-way split mirroring the Squire/Tulving taxonomy plus the Stanford Reflection module.

```
memory/
├── episodic/      — events, dated, what-happened-when
├── semantic/      — facts, what-is-true
│   ├── entities/  — people, orgs, projects, tools, products
│   ├── concepts/  — ideas, frameworks, methodologies
│   └── synthesis/ — derived comparisons, cross-cutting insights
├── procedural/    — workflows, how-to, repeated patterns
└── reflections/   — higher-level inferences derived from clusters of the above
```

## Retrieval

Three-factor scoring (`relevance + recency + importance`) — see `docs/frontmatter_schema.md`. Default top-k = 5 candidates loaded per turn that needs supporting memory.

## Promotion paths

- **Episode → Semantic-entity**: when a new person/org/tool is mentioned by name for the first time, an entity page is created and linked from the episode.
- **Episode → Semantic-concept**: when an idea is articulated and named, a concept page is created.
- **Episode → Procedural**: when a workflow is observed and explicitly extracted (user-triggered, no auto-promotion).
- **Cluster → Reflection**: when rolling importance sum crosses 30, the agent surveys recent additions and writes one reflection.
- **Semantic ⇄ Synthesis**: synthesis pages cite semantic pages and may, with user approval, update their parent pages.

## What does NOT go here

- Tone / style / constraints → `subconscious/`
- Self-description for broadcast → `consciousness/identity.md`
- Current focus → `consciousness/active_context.md`
- Volatile session scratch → `working/`
