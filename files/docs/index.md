# 프로젝트 인덱스

## 프로젝트 맥락
- [overview.md](overview.md) — 프로젝트 개요(업무) + 기술 컨텍스트. 단위 작업 시 필요한 섹션만 읽는다 (보통 업무 개요는 스킵)

## 규칙
- [문서 관리 규칙](conventions.md) — 문서 작성 시 따르는 3층 구조 (인덱스 + 공유핵심 + 단위별 파일)
- [작업 흐름](workflow.md) — 구현/검증 사이클, 상태 전이, 승인 게이트
- [향후 계획](roadmap.md) — 미구현 자동화 항목

## 설계 스펙
| 스펙 | 파일 | 상태 |
|------|------|------|
| (추가 예정) | | |

## 역할 파일
| 역할 | 파일 | 설명 |
|------|------|------|
| 구현 | [docs/roles/implementer.md](roles/implementer.md) | 기능 구현 담당 |
| 검증 | [docs/roles/verifier.md](roles/verifier.md) | 완성 기준 판정 담당 |

## 공유핵심
- [shared.md](shared.md) — 기능 간 공유 의존성 (feature 파일의 "의존성" 섹션에 명시된 경우만 읽는다)

## 기능 파일
상태 정의: `대기` | `구현중` | `검증중` | `완료` | `에스컬레이션` (전이 규칙은 [workflow.md](workflow.md))
신규 작성: [features/_template.md](features/_template.md) 복사 → 승인 게이트([workflow.md](workflow.md)) 통과

| 기능 | 파일 | 상태 | 승인자 |
|------|------|------|--------|
| (추가 예정) | | | |
