---
type: episodic
created: 2026-05-21
updated: 2026-05-21
importance: 8
tags: [hangsung-drone, architecture-decision, lock-change, skybrush]
entities: ["[[hangsung-drone]]"]
participants: ["[[hangsung-drone]]"]
location: null
---

# HangsungDrone design-system 락 정정 — 풀 자체 구현

## 무엇이 결정됐는가

design-system 락이 **"오픈소스(Skybrush) 활용 우선" → "풀 자체 구현, Skybrush 완전 탈피"** 로 정정. 사용자가 두 차례 push back을 받은 뒤 명시 확정. v0.3 회의록 신설 (`docs/meeting/drone_show_business_summary_v0.3.md`).

## 트리거된 사유

Phase 0 안무 OSS + AGPL 검증 데스크 리서치(`docs/design/phase0/02_choreography_oss_license.md`)에서 두 발견:

1. **무료 Skybrush Live/Server 10대 캡** — L1.5 데뷔 30대 불가
2. **자동 트랜지션 최적화 = Skybrush 공개 원격 Studio Server 의존** — 오프라인 운용 가정 충돌

정체성 락 MOAT(반자동 SaaS 견적·미리보기 경험)가 외부 SaaS에 종속되는 구조였음.

## Push back 등록 (peer 의무, 사후 미보고 회피용 사전 명문화)

1. **공학 부담**: 30대급 트랜지션 옵티마이저는 Hungarian goal assignment + minimum-snap polynomial trajectory + RVO/ORCA 또는 DMPC 충돌회피. 학술→실용 갭 큼. arXiv 1909.05150 DMPC 30 agent 90%+ 성공률이 2019년 = 비교적 최근
2. **일정 충돌**: 12-18개월 데뷔 락 + 자기자본 500만 + 외부투자 미확보 단계에서 풀 자체는 정직하게 빠듯함
3. **MOAT 정합**: 정체성 락 MOAT는 산업 팔레트·운영 안전·반자동 SaaS UX이지 **알고리즘 자체가 MOAT가 아님**. 풀 자체는 알고리즘 통제권은 되지만 MOAT 강화 효과는 산업 팔레트·SaaS UX에서 더 큼

사용자 응답: 풀 자체로 진행. 권고는 등록·기록됨, 결정 존중.

## 의존 변경 — 자체 vs 활용

| 레이어 | v0.2 | v0.3 |
|---|---|---|
| 디자인 표면 (Blender/웹) | Skybrush Studio for Blender | 자체 (MVP는 DSL+웹 뷰어 권고) |
| 트랜지션 옵티마이저 | Skybrush 원격 Studio Server | 자체 (Hungarian + minimum-snap or DMPC) |
| 물리 검증 | Skybrush 내장 | 자체 |
| 안무 바이너리 포맷 | libskybrush `.skyb` 호환 | 자체 포맷 |
| GCS / 호스트 스웜 제어 | Skybrush Live | Crazyswarm2 (MIT, 권고 — 풀자체는 design-system만, 호스트 라이브러리는 별개) |
| 펌웨어 app-layer | 자체 (락 η″·θ″) | 유지 — crazyflie-firmware GPL 의존·app-layer만 자체 |

## 영향받지 않는 락

정체성 5개, L1.5 데뷔 30대, L3 자체 BOM 후순위, 시스템 아키텍처 5단계, 펌웨어 코어 정책(포크 금지), 안전 모델, 운영 모델 — v0.2 그대로 유효.

## 보존된 검토 트리거 (별도 결정으로 이어짐)

- 일정 락 12-18개월 정정 필요 여부 → Phase 0 Pf-6
- 자본 락 R&D 인건비 재산정 → G-OP1 연동
- 안전 검증 부담 전이 → GS1~5 게이트에 자체 옵티마이저 검증 항목 추가 가능성
- MOAT 정합 트레이드 → 자원 배분 시 재참조

## 후속 작업 (R1만 즉시, R2~R5는 신규 락 확정 후)

- ✅ R1: `02_choreography_oss_license.md` 상단 v0.3 부분 무효 배너 추가
- R2: `01_system_architecture.md` 모듈 3 `design-system` 책임 범위 확장
- R3: `02_interface_catalog.md` Skybrush 인터페이스 제거
- R4: `06_drone_specification.md` §2 펌웨어 자체 포맷 정렬
- R5: `08_operations_model.md` G-OP1 원가 — Skybrush 라이선스비 제거, R&D 인건비 신설
