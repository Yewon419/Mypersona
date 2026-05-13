# Cognitive Architecture Reference — for Mypersona Wiki

> **Purpose.** This is a working reference for the agent (Claude Code or any LLM dev tool) that will design Phases B/C/D of the Mypersona persona-wiki. It compresses four standard cognitive models into a single mapping table from **brain construct → persona-wiki layer candidate**, surfaces the open design decisions that follow from that mapping, and ends with concrete recommendations for the next phases.
>
> Not a literature survey. Not for end users. Optimized for grep-and-map by a coding agent.

---

## 1. The four axes that matter

Any persona-wiki design needs to position each piece of stored content on these axes. Everything below is a compression of the literature into these axes — if a psych concept doesn't help us locate content on one of them, it's omitted.

| Axis | Values | Why it matters for the wiki |
|---|---|---|
| **Duration** | sensory · short-term/working · long-term | Decides which files are volatile (per-session scratch) vs persistent (committed to repo). |
| **Consciousness** | conscious/declarative · preconscious · unconscious/implicit | Decides what the LLM should surface to the user on demand vs apply silently as background flavoring. |
| **Content kind** | episodic (events) · semantic (facts) · procedural (how-to) | Decides folder partitioning inside long-term memory. |
| **Access pattern** | broadcast (always on) · cued retrieval · implicit influence | Decides which files are injected into every prompt vs loaded by query vs only influence tone. |

---

## 2. Standard models — compressed

### 2.1 Atkinson-Shiffrin multi-store (1968)
Linear pipeline: **Sensory → STM → LTM**. Information moves by attention (in) and rehearsal (consolidation). Forgetting = decay or displacement.

- **Useful contribution:** the duration axis. STM ≠ LTM ≠ raw input.
- **Where it breaks for us:** treats STM as a single store. For an LLM agent we need structure inside the working layer.

### 2.2 Baddeley & Hitch working memory (1974, +episodic buffer 2000)
Replaces Atkinson's monolithic STM with **4 components**:

| Component | Function | LLM analogue |
|---|---|---|
| Central executive | Attention allocation, control | The agent's reasoning loop / system prompt |
| Phonological loop | Verbal/auditory scratch | Token stream / chat history |
| Visuospatial sketchpad | Visual/spatial scratch | Image/diagram context (multimodal) |
| Episodic buffer | Binds modalities + connects LTM | The "what just happened in this session" summary |

- **Useful contribution:** working memory is structured; an "episodic buffer" is a real construct, not a metaphor — it's the bridge between in-session scratch and long-term episodic memory. That bridge needs an explicit file in our wiki.

### 2.3 Squire / Tulving taxonomy of long-term memory
The most load-bearing model for us. LTM splits into:

```
LTM
├── Declarative (explicit, conscious recall)
│   ├── Episodic   — "I did X on date Y with Z"
│   └── Semantic   — "X is a Y" / facts, concepts, preferences as statements
└── Nondeclarative (implicit, non-conscious)
    ├── Procedural — skills, workflows ("how to do X")
    ├── Priming    — exposure-shaped biases
    └── Conditioning / nonassociative — reflexive associations
```

- **Useful contribution:** this is the cleanest decomposition of long-term content. Maps almost 1:1 to folder structure.
- **Note:** Priming + conditioning collapse into "implicit influence" for our purposes — we don't need three separate folders for tone/style biases. One `subconscious/` folder suffices.

### 2.4 Global Workspace Theory (Baars 1988, Dehaene)
Consciousness = a **broadcast hub** that selects which content from many specialized unconscious modules gets globally distributed across the whole system. Only broadcasted content is "conscious"; the rest runs in parallel below threshold.

- **Useful contribution:** explains *how* the system decides what to surface. For us this is the **entry-point file** (`PERSONA.md` / `AGENTS.md`) — the one file every agent reads first, which broadcasts the active persona configuration to the LLM each turn.
- **Recent work** ("Theater of Mind" arxiv 2604.08206; Global Workspace Agents) confirms this is a viable architecture for LLM agents specifically, not just human cognition.

---

## 3. Mapping table — brain construct → wiki layer

This is the table the next phase consumes directly.

| Brain construct | Persona-wiki layer | Folder/file candidate | Volatile? | In every prompt? |
|---|---|---|---|---|
| Sensory input | (n/a — LLM's input is itself sensory) | — | — | — |
| Working memory: phonological loop | Chat history | (handled by host LLM tool) | yes | yes |
| Working memory: episodic buffer | In-session bridge to LTM | `working/session_buffer.md` | yes (gitignored) | yes (session-scoped) |
| Working memory: central executive | The reasoning contract | `PERSONA.md` (entry point) | no | **yes — always** |
| Declarative · episodic LTM | Logged events, conversations, milestones | `memory/episodic/YYYY-MM-DD-*.md` | no | retrieved by cue |
| Declarative · semantic LTM | Facts, preferences, identity statements | `memory/semantic/*.md` | no | partial (top-level always) |
| Nondeclarative · procedural | Workflows, "how I work" rules | `memory/procedural/*.md` | no | retrieved by task context |
| Nondeclarative · implicit (priming/conditioning) | Tone, style, aesthetic bias | `subconscious/*.md` | no | **yes — always (low salience)** |
| Conscious surface (GWT broadcast) | What the persona says about itself | `consciousness/identity.md` | no | yes |
| Conscious surface (current focus) | What the persona is currently working on | `consciousness/active_context.md` | semi-volatile | yes |

**Key design moves baked into this table:**

1. **Three "always-broadcast" files**: `PERSONA.md`, `consciousness/identity.md`, `subconscious/*` (concatenated). These define the persona regardless of which LLM is hosting.
2. **Episodic and procedural are cue-retrieved**, not always broadcast — too large, and most aren't relevant to a given turn.
3. **The `subconscious/` layer is always-on but low-salience** — this is what produces persona consistency across sessions even when no specific episodic memory is being recalled.
4. **`working/` is gitignored.** Per-session scratch. The episodic buffer file gets *consolidated* into `memory/episodic/` at session end (see §5).

---

## 4. Mapping the user's three terms

The user phrased the goal as separating "표면에서 드러나는 지식 / 잠재의식 / 기억". Mapped to the architecture above:

| User term | Maps to | Folder |
|---|---|---|
| 표면에서 드러나는 지식 | Conscious / declarative surface (GWT broadcast + semantic LTM) | `consciousness/` + `memory/semantic/` |
| 잠재의식 | Nondeclarative implicit (priming/conditioning) | `subconscious/` |
| 기억 | Declarative episodic + procedural | `memory/episodic/` + `memory/procedural/` |

This is a clean fit. The three folksy terms cover the full taxonomy.

---

## 5. Design implications for Phases B / C / D

### For Phase B (directory structure)
Adopt the folder layout in §3 verbatim. One deviation worth considering: **flatten `memory/` into `episodic/`, `semantic/`, `procedural/` at the top level** for visibility — the wiki is the persona, so the structure should be readable at a glance.

Recommendation: keep `memory/` as the grouping container. The triple subdivision (episodic/semantic/procedural) is a real cognitive distinction; surfacing all three at top level would clutter the root.

### For Phase C (LLM-agnostic bootstrap)

**Entry point file naming.** Two relevant conventions exist:
- `CLAUDE.md` — Claude Code specific
- `AGENTS.md` — emerging cross-tool standard (Codex, Cursor, Cline)

Both are read-on-startup. Recommendation: write `PERSONA.md` as the canonical source, then commit `CLAUDE.md` and `AGENTS.md` as **one-line redirects** to it (`See PERSONA.md`). This keeps a single source of truth while satisfying every tool's discovery convention.

**Bootstrap dialogue.** The first-run guided Q&A the user mentioned maps to **initializing the conscious-surface layer** before any episodic memories exist. Suggested initial questions (the persona asks the user):
1. *Consciousness level* — How surfaced should the persona be? (silent assistant ↔ explicit co-presence)
2. *Constraints* — What must the persona never do? (hard rules → `subconscious/constraints.md`)
3. *Identity seed* — In one paragraph, who is the user? (→ `consciousness/identity.md`)
4. *Working style* — How does the user like to be addressed, corrected, paced? (→ `subconscious/style.md`)
5. *Domains* — What topics will this persona accumulate around? (→ creates initial `memory/semantic/<domain>.md` stubs)

These five seed the always-broadcast layer. Everything else accumulates through normal conversation.

### For Phase D (auto-classification rules)

The agent needs a decision procedure for "what folder does this new piece of information go in?" Proposed rule order (apply top-down, first match wins):

1. **Is it time-stamped and event-shaped?** → `memory/episodic/`
2. **Is it a workflow or rule the user wants enforced?** → `memory/procedural/`
3. **Is it a fact, preference, or identity claim the user stated explicitly?** → `memory/semantic/`
4. **Is it a pattern the agent inferred from behavior, not explicitly stated?** → `subconscious/`
5. **Is it self-description the persona should surface on request?** → `consciousness/`

**Consolidation rule (working → long-term).** At session end (or on explicit `/consolidate`), the agent:
- Promotes `working/session_buffer.md` events into a new dated `memory/episodic/` page
- Updates `memory/semantic/` if any new facts were stated
- Updates `subconscious/` if a stable new pattern was observed (≥3 occurrences threshold suggested)
- Appends one line to `log.md`
- Clears `working/session_buffer.md`

This mirrors **biological memory consolidation** (hippocampus → neocortex during sleep). The metaphor is load-bearing, not decorative: it tells us when to write and when to defer.

---

## 6. Open decisions — to resolve before / during Phase B

1. **Should `working/` be in git at all, or pure local?**
   - In-git: cross-machine session continuity, but noisy history.
   - Local-only: clean history, but losing a machine loses scratch.
   - *Default suggestion: gitignored. Consolidation runs at session end anyway.*

2. **How does `subconscious/` get populated — agent-inferred or user-asserted?**
   - Agent-inferred: more authentic to the construct (implicit memory isn't consciously stated), but error-prone.
   - User-asserted: safer, but then it's really just semantic memory with a different label.
   - *Default suggestion: hybrid. Agent proposes patterns at session end, user confirms before commit.*

3. **Promotion threshold from episodic → semantic.**
   - When does "I prefer X" (stated once in an episode) become a stable semantic fact?
   - *Default suggestion: explicit promotion only. Episodic pages can link to semantic ones, but auto-promotion produces drift.*

4. **Entry-point naming.** `PERSONA.md` canonical + `CLAUDE.md`/`AGENTS.md` redirects (recommended) vs picking one and committing.

5. **Multi-persona support.** Is this strictly one-persona-per-repo, or should the structure allow multiple personas as siblings? Affects whether `consciousness/`, `subconscious/`, `memory/` are top-level or nested under `personas/<name>/`.
   - *Default suggestion: single-persona at v1. Multi-persona is a v2 concern that would otherwise over-engineer the initial release.*

---

## 7. Out of scope for this document

- **Phase E (interactive node-graph visualization).** Data schema must stabilize first. Note for later: the cross-folder link graph defined by `[[wikilink]]` references is the natural graph data source. Libraries to evaluate when Phase E starts: `react-force-graph`, `d3-force`, `cytoscape.js`. Spline/Motion are aesthetic layers on top, not graph engines.
- **Sync/multi-device strategy.** Git handles this.
- **Encryption / privacy gating of public repo.** User accepted public; if `memory/episodic/` ever contains sensitive content, revisit.

---

## Sources

- Squire LR. *Memory systems of the brain: A brief history and current perspective.* Neurobiol Learn Mem 2004. http://whoville.ucsd.edu/PDFs/384_Squire_%20NeurobiolLearnMem2004.pdf
- Atkinson & Shiffrin (1968) multi-store model — overview: https://www.simplypsychology.org/multi-store.html
- Baddeley working memory — overview: https://en.wikipedia.org/wiki/Baddeley's_model_of_working_memory
- Global Workspace Theory — overview: https://en.wikipedia.org/wiki/Global_workspace_theory
- "Theater of Mind" — GWT architecture for LLMs: https://arxiv.org/abs/2604.08206
- AI agent memory taxonomy (industry mapping): https://atlan.com/know/types-of-ai-agent-memory/
