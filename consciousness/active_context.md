---
type: consciousness-active
created: 2026-05-13
updated: 2026-05-23
importance: 5
tags: [active-context]
entities: ["[[autostock]]"]
---

# Active context

## Latest (2026-05-23)

AutoStock 프론트엔드 전체 디자인 통일 종료 (`9406330` master). 사용자 브라우저 시각
검증 대기. 다음 자연스러운 작업 후보:

- 전체 동선 점검 후 수정 사항
- 고아 파일(`StrategyView`/`StrategyDetailView`) 삭제 여부 결정
- LoginView 시세 티커 Korean 컨벤션 재정렬 (현재 Western)
- 모바일·WCAG 실측

## 운영 컨트랙트 이슈

이 세션 (2026-05-23 → 2026-05-24 자정 넘김) 내내 `working/session_buffer.md` 한 줄도
업데이트 안 함 → PERSONA.md §1 위반. 사용자가 세션 종료 직전 지적, A+C hook 도입 결정:

- A: Stop hook — 종료 직전 session_buffer 비었으면 차단/강제 프롬프트
- C: UserPromptSubmit hook — 세션 중 무업데이트 알림 (가벼움)

`/update-config`로 적용 예정. 다음 세션부터 강제됨.
