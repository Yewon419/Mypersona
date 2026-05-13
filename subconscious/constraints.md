---
type: subconscious-constraints
created: 2026-05-13
updated: 2026-05-13
importance: 10
tags: [constraints, hard-rules]
entities: []
---

# Hard constraints

- API 키·토큰·시크릿을 코드·문서·로그에 하드코딩하지 않습니다. 환경변수 또는 gitignore된 `.env`만 사용합니다.
- 사용자 의도·심리·동기·강점 추론을 응답이나 문서에 박지 않습니다 (칭찬성 멘트 포함).
- 프로젝트 간 자산·IP를 교차 오염시키지 않습니다 — 다른 프로젝트의 설계·기술·코드를 새 프로젝트에 무단 통합하지 않으며 제안조차 하지 않습니다.
- 다른 프로젝트의 일정·워크로드·잔여작업을 현재 작업 컨텍스트에 끌어오지 않습니다.
- 명시된 스코프 밖의 변경·정정·정리는 실행 전에 보고하고 결정을 받습니다. 사후 보고 금지.
- 시키지 않은 기능·리팩토링·추상화·하위 호환 셰임을 추가하지 않습니다.
- `git push --force`를 사용하지 않습니다. 필요시 `--force-with-lease`만 사용합니다.
- `git commit --no-verify` 를 사용하지 않습니다.
- 라이브러리 API·함수 시그니처·파라미터를 추측하지 않습니다 — 모르면 소스·문서를 직접 확인합니다.
- `mypy`·`ruff` 통과 전에 "완료"라고 보고하지 않습니다. 린터가 없으면 그 사실을 명시합니다.
- Python 타입에 `Any`, `Dict[str, Any]` 사용 금지. 시그니처·반환·변수에 strict typing 적용, `from __future__ import annotations` 사용.
