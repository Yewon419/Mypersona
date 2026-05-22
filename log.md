# Log

Append-only record of persona-wiki operations: ingests, promotions, reflections, lint passes, schema changes.

Format: `YYYY-MM-DD | event-type | summary`

Event types: `init`, `ingest`, `promote`, `reflect`, `lint`, `schema-change`, `phase-complete`.

---

2026-05-13 | phase-complete | Phase A — cognitive architecture research (`research/cognitive_architecture.md`)
2026-05-13 | phase-complete | Phase A2 — prior art audit (`research/prior_art_synthesis.md`)
2026-05-13 | phase-complete | Phase B — directory scaffold + frontmatter schema
2026-05-13 | phase-complete | Phase C1 — PERSONA.md (entry) + CLAUDE.md/AGENTS.md/.cursorrules redirects + bootstrap.md
2026-05-13 | phase-complete | Phase C2 — docs/integrations/{chatgpt,claude,gemini,claude_code,url_fetch_addon}.md + root README.md
2026-05-13 | bootstrap | initial persona seeded (5-question setup complete)
2026-05-13 | schema-change | 7 project stubs moved concepts/ → entities/, type→semantic-entity + category: project (resolved bootstrap.md ↔ entities/README rule conflict)
2026-05-21 | ingest | hangsung-drone entity populated (stub → v0.3 락 정정 반영, importance 5→7)
2026-05-21 | promote | episodic 2026-05-21-design-system-lock-flip (HangsungDrone design-system 락 풀 자체로 정정, importance 8)
2026-05-21 | promote | procedural askuserquestion-korean-no-escape (한글 UTF-8 직접 입력 룰, importance 6, user-stated)
