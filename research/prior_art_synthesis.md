# Prior Art Synthesis — what we missed in Phase A

> **Purpose.** Audit Phase A's design conclusions against existing implementations of (a) academic agent-memory architectures, (b) production memory frameworks, (c) consumer persona formats, and (d) personal-AI / digital-twin projects on GitHub. Identify what to **add**, what to **revise**, and what's **validated as-is**.
>
> Read `cognitive_architecture.md` first. This doc only annotates deltas.

---

## 1. The four reference categories

| Category | Flagship | Year | Relevance |
|---|---|---|---|
| Academic foundation | **Stanford Generative Agents** (Park et al.) | 2023 | Highest-cited prior work on LLM agents with episodic-style memory + emergent persona behavior |
| Production infra | **Letta** (formerly MemGPT) | 2024–26 | OS-inspired tiered memory; closest mature framework |
| Production infra (lightweight) | **Mem0**, **Cognee**, **Zep** | 2024–26 | Extraction-based or graph-based memory layers |
| Consumer persona | **SillyTavern Character Card V2/V3** | 2023–25 | De facto standard for distributable AI personas |
| LLM Wiki community | **NicholasSpisak/second-brain** (Karpathy pattern) | 2026 | Reference implementation of Karpathy's original idea-file |
| **Closest analog** | **Jason-Cyr/ai-shared-brain** | 2025–26 | Persona + memory in plain markdown; **same pattern Mypersona is converging on** |

---

## 2. Concrete patterns from each — and what they imply for Mypersona

### 2.1 Stanford Generative Agents
- **Memory stream**: append-only natural-language record. Every observation gets stored, nothing is deleted.
- **Reflection**: when accumulated *importance score* of recent events crosses a threshold (~2–3×/day), agent generates **higher-level inferences** from clusters of memories. Reflections are themselves memories, stored alongside observations.
- **Retrieval**: scored by weighted sum of **relevance + recency + importance**. Top-k retrieved per query.

→ **Implication:** Our Phase A has consolidation (working → episodic), but **no Reflection step**. Reflection is what produces *compounding* — without it, episodic memory just grows, it doesn't get smarter.

### 2.2 Letta / MemGPT — OS-inspired tiered memory
- **Core Memory** (small, in-context, always present) — like RAM
- **Recall Memory** (searchable conversation history, out of context, retrieved by tool calls) — like disk cache
- **Archival Memory** (long-term storage, queried via tools) — like cold storage
- Agent **self-edits** memory by calling memory functions inside its reasoning loop.

→ **Implication:** Our `PERSONA.md` + `consciousness/` ≈ Core. Our `working/` + `memory/episodic/` ≈ Recall. Our `memory/semantic/` + `memory/procedural/` + `subconscious/` ≈ Archival. **Mapping is clean.** What we missed: the **self-edit behavioral contract** — `PERSONA.md` should explicitly instruct the agent "you write to these folders during your own reasoning, not as a post-hoc step."

### 2.3 Mem0 / Cognee / Zep
- All three use **vector embeddings** for retrieval, not pure markdown.
- All three converged on the same memory scopes: **episodic / semantic / procedural**.

→ **Implication:** Three-way LTM split is **industry standard, not just our cognitive-science derivation**. Validates Phase A folder structure.
→ **Open trade-off:** pure markdown (LLM-agnostic claim intact, retrieval quality degrades past ~hundreds of pages) vs. optional vector index (faster retrieval, compromises portability). See §4.

### 2.4 SillyTavern Character Card V2/V3
Standard distributable persona schema. Fields:
```
name, description, personality, scenario,
first_mes, mes_example, system_prompt,
post_history_instructions, alternate_greetings,
tags, creator, creator_notes, character_version,
character_book  (a lorebook of facts about the persona's world)
```

→ **Implication:** We have no frontmatter schema for `consciousness/identity.md`. SillyTavern's fields are battle-tested for "persona that runs anywhere." Borrow **at minimum**: `name, description, personality, system_prompt, first_mes, mes_example`. `character_book` ≈ our `memory/semantic/`.

### 2.5 NicholasSpisak/second-brain (Karpathy reference impl)
Wiki sub-structure:
```
wiki/
├── sources/     — ingest summaries
├── entities/    — people, orgs, tools
├── concepts/    — ideas, frameworks
├── synthesis/   — comparisons, theme work
├── index.md
└── log.md
```

→ **Implication:** This is for *knowledge* wikis, not persona. But the `entities/ concepts/ synthesis/` triplet is a useful sub-structure for our `memory/semantic/` — too flat currently.

### 2.6 Jason-Cyr/ai-shared-brain (closest analog)
Three-file core:
- `SOUL.md` — personality customization (what the agent *is*)
- `USER.md` — facts about the user (what the agent *knows about them*)
- `MEMORY.md` — LLM-curated long-term memory filled over time

Agent reviews daily notes, **promotes** important items to long-term memory.

→ **Implication:** Our split is nearly identical (`consciousness/identity.md` ≈ SOUL.md, plus broader memory layering). The **explicit "promote" verb** is more concrete than our "consolidation." Worth adopting the vocabulary.

### 2.7 gbrain (YC / Garry Tan)
- Markdown + git repo
- **Overnight enrichment**: scans conversations/emails/transcripts while user sleeps, builds knowledge graph
- Auto cross-references entities

→ **Implication:** The "background pass" pattern matters for compounding. Our Phase A has consolidation at session end, but a separate **scheduled enrichment pass** is a different operation (cross-references, dedup, lint).

---

## 3. Delta against Phase A

### 3.1 What's validated as-is
- ✅ **Episodic / semantic / procedural** LTM split (industry standard, all major frameworks agree)
- ✅ **Always-broadcast core layer** (`PERSONA.md` + `consciousness/`) — matches Letta Core Memory
- ✅ **`subconscious/` for tone/style** — non-standard naming but covers ground that SillyTavern's `personality` field and ai-shared-brain's `SOUL.md` both target; the brain metaphor justifies the divergence
- ✅ **Session-end consolidation** (`working/` → `memory/episodic/`) — matches ai-shared-brain's daily review
- ✅ **Pure markdown choice** for LLM-agnostic portability — see trade-off in §4

### 3.2 What's missing (must add)
1. **Reflection module** (from Stanford). Periodic synthesis that produces *derived* memories — not "move working to episodic" but "given last 30 episodes, what does the persona now believe/notice?" Without this, no compounding. → add `memory/reflections/` folder + reflection trigger spec in `PERSONA.md`.
2. **Importance scoring on memories** (from Stanford). Frontmatter field `importance: 1–10`. Affects retrieval weighting and triggers reflection.
3. **Three-factor retrieval spec** in `PERSONA.md` — relevance + recency + importance.
4. **Self-edit behavioral contract** in `PERSONA.md` — explicit "agent writes to its own memory during reasoning."

### 3.3 What's worth revising
5. **Frontmatter schema** for `consciousness/identity.md` — borrow SillyTavern fields: `name, description, personality, system_prompt, first_mes, mes_example`. Improves portability and distributability.
6. **Sub-structure inside `memory/semantic/`** — apply Karpathy wiki sub-pattern (`entities/ concepts/ synthesis/`). Current "flat .md files" doesn't scale past dozens of facts.
7. **Vocabulary**: `consolidation` → `promotion` (ai-shared-brain terminology, more concrete and recurring in literature).

### 3.4 What to defer (not v1)
- **Scheduled background enrichment pass** (gbrain pattern). Adds an extra mode of operation. Can be a v2 feature; v1 ships with session-end consolidation + on-demand `/reflect` only.
- **Vector embeddings layer** — see §4.

---

## 4. The pure-markdown vs vector-index trade-off

The single biggest architectural decision left.

| Approach | Pro | Con |
|---|---|---|
| **Pure markdown only** (Phase A default) | LLM-agnostic claim fully intact. Git-friendly. Human-readable. Works with `grep`. | Retrieval degrades past ~hundreds of pages. Whole-folder reads waste tokens. |
| **Optional vector sidecar** (e.g., `.index/` folder, regenerable) | Fast semantic retrieval at scale. | Requires embedding model; agent now depends on more than just markdown. Mitigated if the index is *regenerable from markdown* and *not required* — agents without it fall back to grep. |
| **Hybrid: tags + frontmatter, no vectors** | Stays pure markdown. Tagged retrieval is faster than full grep. Frontmatter-driven retrieval is deterministic. | Less semantic — exact-match tags only, no synonym matching. |

**Recommendation:** Start with **hybrid**. Frontmatter fields (`importance`, `tags`, `date`, `entities`) give us deterministic filtered retrieval. If retrieval quality becomes a real bottleneck after months of use, add optional regenerable `.index/` sidecar. Keep the LLM-agnostic claim as a v1 commitment.

---

## 5. Revised Phase B input

Apply changes 1–6 from §3.2–3.3 before drafting the directory tree. Specifically:

```
Mypersona/
├── PERSONA.md                # entry point + behavioral contract (Letta self-edit + 3-factor retrieval spec)
├── CLAUDE.md                 # → redirect to PERSONA.md
├── AGENTS.md                 # → redirect to PERSONA.md
├── consciousness/
│   ├── identity.md           # SillyTavern-style frontmatter + body
│   └── active_context.md
├── subconscious/
│   ├── style.md
│   └── constraints.md
├── working/                  # gitignored
│   └── session_buffer.md
├── memory/
│   ├── episodic/             # YYYY-MM-DD-*.md, frontmatter w/ importance
│   ├── semantic/
│   │   ├── entities/         # ← NEW: borrowed sub-structure
│   │   ├── concepts/
│   │   └── synthesis/
│   ├── procedural/
│   └── reflections/          # ← NEW: derived memories from reflection module
├── index.md
├── log.md
└── research/                 # cognitive_architecture.md + prior_art_synthesis.md
```

**Frontmatter schema (memory pages):**
```yaml
---
type: episodic | semantic-entity | semantic-concept | procedural | reflection
created: YYYY-MM-DD
importance: 1-10
tags: [...]
entities: [[link1]] [[link2]]
source: episodic/YYYY-MM-DD-foo.md  # for reflections, what they were derived from
---
```

---

## Sources

- Park et al., *Generative Agents: Interactive Simulacra of Human Behavior* (2023). https://arxiv.org/abs/2304.03442
- Letta / MemGPT memory tiers — https://forum.letta.com/t/agent-memory-letta-vs-mem0-vs-zep-vs-cognee/88
- Mem0 vs Letta industry comparison — https://vectorize.io/articles/mem0-vs-letta
- SillyTavern Character Card V2 spec — https://github.com/malfoyslastname/character-card-spec-v2
- NicholasSpisak/second-brain — https://github.com/NicholasSpisak/second-brain
- Jason-Cyr/ai-shared-brain — https://github.com/Jason-Cyr/ai-shared-brain
- Copana (personal AI in markdown) — https://copana.ai/
