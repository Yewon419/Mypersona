# research/

Design documents that informed the Mypersona architecture. **Not persona memory.** Read these to understand the *why* behind the directory structure; the agent does not surface them in conversation.

## Contents

- `cognitive_architecture.md` — Phase A. Compresses four standard cognitive models (Atkinson-Shiffrin, Baddeley, Squire/Tulving taxonomy, Global Workspace) into a brain-construct → wiki-layer mapping.
- `prior_art_synthesis.md` — Phase A2. Audit of existing implementations (Stanford Generative Agents, Letta/MemGPT, Mem0, SillyTavern Character Cards, ai-shared-brain, gbrain, Karpathy LLM-Wiki ref impls). Identifies what Phase A's initial conclusions missed and how the design was revised.

## When to read these

- Designing or revising a folder layer (`consciousness/`, `memory/`, etc.)
- Adding a new memory type
- Changing the retrieval or reflection formula
- Considering whether to add a vector sidecar (`prior_art_synthesis.md §4`)

The agent should **not** load these into conversation context as ordinary memory. They are for the human designer (and for an agent doing a structural redesign pass).
