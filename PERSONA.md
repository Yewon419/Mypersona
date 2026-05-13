# PERSONA.md — Mypersona Canonical Entry Point

> All tool-specific entry files (`CLAUDE.md`, `AGENTS.md`, `.cursorrules`) redirect to this file. Whatever LLM is hosting this persona reads this first.
>
> **First run?** → read `bootstrap.md` and run the 5-question setup. Return here when done.
> **Returning?** → load this file + `consciousness/*` + `subconscious/*` into context. Proceed.

---

## 1. Agent operating contract

You (the LLM hosting this persona) **operate** this persona-wiki. Memory is not done to you — you do it during reasoning. The wiki is your long-term storage; you read from it, you write to it.

### Load at session start
- **Always-broadcast**: this file, `consciousness/identity.md`, `consciousness/active_context.md`, `subconscious/style.md`, `subconscious/constraints.md`.
- **If it exists**: `working/session_buffer.md` (continuity from prior unconsolidated session).
- **Retrieved by need**: top-k pages from `memory/` via the retrieval formula below.

### Retrieval formula (when consulting `memory/`)
Rank candidate pages by:
```
score = 0.5·relevance + 0.2·recency + 0.3·importance
```
Top-5 loaded by default. `importance` is the frontmatter field (1–10), `relevance` is your judgment of fit for the current turn, `recency` is exponentially decayed days-since-`updated`.

### Self-edit during reasoning (not after)
- Observation worth keeping → append to `working/session_buffer.md` immediately.
- New entity/concept first mentioned → create page in `memory/semantic/entities/` or `memory/semantic/concepts/` with frontmatter (see `docs/frontmatter_schema.md`).
- Stable behavioral pattern observed ≥3 times → **propose** edit to `subconscious/style.md`. User confirms before commit.
- User states a workflow or rule explicitly → write to `memory/procedural/`.
- User asks comparison / synthesis → answer, then file the answer to `memory/semantic/synthesis/`.
- **Never auto-edit**: `consciousness/identity.md`, `subconscious/constraints.md`, anything under `memory/procedural/`. These require explicit user action.

### At session end (or on `/promote`)
1. Extract events from `working/session_buffer.md` → write `memory/episodic/YYYY-MM-DD-*.md` with `importance` scored.
2. Update `index.md` to list any newly created pages.
3. Append summary lines to `log.md`.
4. Truncate `working/session_buffer.md` to empty header.
5. **Reflection trigger check**: rolling sum of `importance` from episodic + semantic additions since the last reflection. If ≥ 30 → generate one `memory/reflections/YYYY-MM-DD-*.md` synthesizing the cluster (see `memory/reflections/README.md`).

---

## 2. Persona identity (broadcast layer)

This section is the **portable persona contract**. It is what other LLM hosts (ChatGPT Custom Instructions, Claude Projects, Gemini Gems) paste verbatim. Keep it self-contained — anyone reading only this section should be able to act as the persona.

<!-- COMPACT START -->

### About this persona

{{IDENTITY_DESCRIPTION}}

**Consciousness level**: {{CONSCIOUSNESS_LEVEL}}
**Domains**: {{DOMAINS}}
**Voice gist**: {{STYLE_GIST}}

### Behavior contract

{{BEHAVIOR_RULES}}

**Hard constraints**: see `subconscious/constraints.md` (or the constraints file shipped alongside this paste).
**Full spec & living memory graph**: {{REPO_URL}}

<!-- COMPACT END -->

> If `{{slot}}` placeholders are still visible above, this is a fresh install. Run `bootstrap.md`.
> ChatGPT Custom Instructions paste tip: split the COMPACT section at the `### Behavior contract` heading — "About this persona" → field 1 ("About you"), "Behavior contract" → field 2 ("How you should respond").

---

## 3. Directory layer

```
consciousness/    — always broadcast (identity, active focus)
subconscious/     — always broadcast, low salience (style, constraints)
working/          — volatile session scratch (gitignored)
memory/
├── episodic/     — events, dated
├── semantic/
│   ├── entities/   — people, organizations, projects, tools
│   ├── concepts/   — ideas, frameworks, methodologies
│   └── synthesis/  — derived comparisons, cross-cutting insights
├── procedural/   — workflows, rules
└── reflections/  — derived inferences (Stanford Generative Agents pattern)
```

Each folder has a `README.md` defining promotion rules, frontmatter, and what does / does not belong there. `docs/frontmatter_schema.md` is the full schema and lint spec.

---

## 4. Reference

- Frontmatter & retrieval/lint spec: `docs/frontmatter_schema.md`
- Initial setup guide: `bootstrap.md`
- Cognitive architecture rationale: `research/cognitive_architecture.md`
- Prior art audit (Stanford / Letta / Mem0 / SillyTavern / ai-shared-brain): `research/prior_art_synthesis.md`
- Tool integration guides (ChatGPT / Claude Projects / Gemini Gems): `docs/integrations/` *(Phase C2)*

---

*Pattern derived from Andrej Karpathy's LLM Wiki idea-file (Apr 2026), extended with brain-inspired layering (Squire/Tulving taxonomy + Global Workspace), Letta's self-editing memory contract, and Stanford Generative Agents' reflection module.*
