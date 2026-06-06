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
2026-05-23 | promote | episodic 2026-05-23-autostock-frontend-design-unification (AutoStock 프론트엔드 14커밋 전체 디자인 통일, importance 8, post-hoc catch-up — 컨트랙트 위반 인지)
2026-05-23 | ingest | autostock entity populated (stub → 디자인 시스템 통일 반영, importance 5→7)
2026-06-06 | schema-change | 역할 분할 (role-split) — PERSONA.md §1 재작성: self-edit/reflection 컨트랙트 은퇴, 단기 작업메모리를 호스트 네이티브 auto-memory에 양보. Mypersona = 휴대용 persona 레이어 + 큐레이션 KB. 근거: prior_art_synthesis.md §6 (Letta sleeptime / Claude Code Auto Dream / faulty-memory)
2026-06-06 | promote | episodic 2026-05-23_2026-05-30-session-archive (구 session_buffer 460줄 원본 보존, lossy rewrite 금지 — faulty-memory 교훈, importance 4)
2026-06-06 | schema-change | working/·active_context·synthesis/·reflections/ inactive 처리. 글로벌 Stop/UserPromptSubmit buffer hook 제거 + 고아 .ps1 2개 삭제. SessionStart hook은 active_context 로드만 제외하고 유지
