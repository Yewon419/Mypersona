---
type: semantic-entity
created: 2026-05-13
updated: 2026-05-23
importance: 7
tags: [domain, project]
entities: []
canonical_name: "AutoStock"
aliases: []
category: project
related: ["[[2026-05-23-autostock-frontend-design-unification]]"]
---

# AutoStock

키움 API 기반 한국 주식 자동매매 플랫폼. FastAPI + Vue 3 + Docker.

## 정체성

- 봇 ↔ strategy 1:1 모델 (5/15~)
- 모드: mock(시뮬) / paper(KIS 모의) / real(실계좌)
- 브로커: Kiwoom API + KIS (Korea Investment & Securities)
- 봇 타입: 스윙(일봉·5분 주기) / 단타(분봉·1분 주기)

## 디자인 시스템 (2026-05-23 통일)

- 톤: 트레이딩 터미널 HUD — 다크 베이스 `#050507` + 골드 액센트 `#f59e0b`
- 폰트 듀얼: Inter (콘텐츠) + JetBrains Mono (HUD·숫자·티커)
- Korean PnL 컨벤션: profit=red / loss=blue
- AI/LLM 표식: violet
- 한국 캔들: up=red / down=blue (lightweight-charts)
- 단일 출처: `frontend/src/assets/main.css` (CSS 변수 100+)
- 관련 이력: [[2026-05-23-autostock-frontend-design-unification]]

## 부모님 시연 임계

거래 30건/봇 + 수익>0 + Sharpe≥0.8 + MDD<10% + KOSPI초과 + gap<5%p, 손실선 10% 절대.
