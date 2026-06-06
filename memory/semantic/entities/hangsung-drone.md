---
type: semantic-entity
created: 2026-05-13
updated: 2026-05-21
importance: 7
tags: [domain, project, hardware, b2b, drone-show]
entities: []
canonical_name: "HangsungDrone"
aliases: ["실내 B2B 드론쇼", "한성드론"]
category: project
related: []
---

# HangsungDrone

실내 B2B 행사(박람회·컨벤션·기업행사) 시장의 **저가 카테고리 신설**형 드론 라이트쇼 사업. AGPL-3.0 public 레포. 본격 시작은 2026 하반기 (휴학 옵션, 창업 트랙).

## 정체성 5개 (락)

| # | 답 |
|---|---|
| WHO | 실내 B2B 행사 (박람회·컨벤션·기업행사·신차 발표회 등) |
| WHAT | 저가 카테고리(시장 신설)의 산업·기업 컨텍스트 시각화 융합형 드론쇼 |
| JTBD | 행사 PR + 부스/무대 임팩트 + 고가 메가쇼 못 부르는 시장 채움 |
| MOAT | 30-50대 단위 가격 효율화 + 산업 도메인 + 융합형 + 운영 안전 패턴 + 반자동 SaaS 즉시 견적·미리보기 경험 |
| MODEL | 행사·부스 단위 + 주기성 + 객단가 200-500만 (추정 미검증) |

**첫 진입(L1.5 beachhead)**: 인터배터리(코엑스, 이차전지전).

## 데뷔 기준 L1.5 (락)

- Crazyflie 2.1+ 30대 + Lighthouse Positioning + 풀 파이프라인 + 반자동 SaaS
- 12-18개월 데뷔 창 — v0.3 풀 자체 결정으로 압박 받음 (재검토 트리거 보존)
- 하드웨어 ≈ $15,316 (충전리그·관세 제외, 메모리 추정 상한 1,800만 초과 가능)
- 안전: 저고도 + 객석 분리 + E-Stop 물리 버튼 + Geofence + 펌웨어 자율 안전

## 설계 4영역 (커밋·푸시 완료, origin main)

- 영역 1: 시스템 아키텍처 5단계 A~E (`docs/design/01~05`) + ADR-0001 DB 보안
- 영역 2 항목 1~4: 드론 사양·BOM·펌웨어 구조 (`docs/design/06`) — 항목 5 L3 BOM은 데뷔 후
- 영역 3: 안전 모델 STPA + FMEA + 위험매트릭스 (`docs/design/07`) — 잔여 🔴 3건 보존(IR·E-Stop·충전화재)
- 영역 4: 운영 모델 R&R·SOP·원가·법무·보험 (`docs/design/08`) — G-OP1~3 게이트

## design-system 락 정정 (v0.3, 2026-05-21)

**"오픈소스 활용 우선" → "풀 자체 구현, Skybrush 완전 탈피".** 사유: 무료 Skybrush Live/Server **10대 캡** + 트랜지션 최적화 **원격 SaaS 의존**이 30대 데뷔·오프라인 운용과 직접 충돌. push back 2회(공학·일정 부담) 등록 후 사용자 확정.

v0.3 델타: `docs/meeting/drone_show_business_summary_v0.3.md`. 자체 범위 = 옵티마이저·안무 포맷·디자인 표면·3D 미리보기. 펌웨어(crazyflie-firmware GPL 의존·app-layer만 자체) 정책은 별개로 유지.

**신규 락 후보 (미확정)**: C1 호스트=Crazyswarm2(MIT, 권고) / C2 옵티마이저=Hungarian+minimum-snap or DMPC / C3 자체 안무 포맷 / C4 MVP 디자인 표면(DSL+웹 뷰어 권고).

**검토 사항 (사전 명문화)**: 일정 락 12-18개월 압박 / 자본 락 R&D 인건비 재산정 / 안전 검증 부담 전이 / MOAT 정합(알고리즘은 MOAT가 아님, 산업 팔레트·SaaS UX가 MOAT).

## Phase 0 상태

- 조달 트랙 보류 (사용자 결정, 2026-05-19) — Wave A 데스크 산출물 보존
- 비조달 트랙 진입: 안무 OSS/AGPL 검증 1차 완료(02) → v0.3 락 정정으로 일부 무효 (배너 처리)
- Phase 0 다음: Pf-1 옵티마이저 알고리즘 결정 / Pf-2 시뮬레이터 / Pf-3 자체 포맷 / Pf-4 디자인 표면 MVP / Pf-5 Crazyswarm2 채택 / Pf-6 일정·자본 재검토

## 자금

자기자본 500만 + 외부투자 유치 계획. 풀 자체 결정으로 R&D 인건비 비중 상승, 외부투자 라운드 시점 재산정 필요.
