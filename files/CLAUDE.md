# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 개발 원칙

### 구현/검증 분리 (예외 없음)
- 구현한 에이전트가 자신의 결과를 검증하지 않는다
- 검증 에이전트는 코드를 수정하지 않는다
- 같은 세션에서 구현 후 검증을 순서대로 수행하는 것도 금지한다
  - 근거: 구현 과정의 사고 흐름이 검증 판단에 영향을 준다 (자기평가 편향)
  - 권장: 구현과 검증은 별도 Claude Code 세션에서 수행한다

### 완성 기준 불변
- 완성 기준은 구현 시작 전에 확정하고 사람이 승인한다
- 구현 진행 중(시도 1~3) 완성 기준을 수정하지 않는다
  - 근거: 구현이 시작되면 기준이 구현에 맞춰 희석되는 경향이 있다
- 3회 실패 후 에스컬레이션 시에는 사람이 기준 수정을 결정할 수 있다

### 최소 컨텍스트
- 에이전트는 역할 파일 + 해당 기능 파일 + failure-report(있을 경우)만 읽는다
- 관련 없는 기능 파일은 읽지 않는다
  - 근거: 불필요한 컨텍스트가 노이즈를 만들어 판단을 흐린다
- fresh context 정의: 이전 대화 기록을 이어받지 않는 것. failure-report 파일은 허용된 입력이며 fresh context 위반이 아니다

### 실패 처리
- 3회 연속 실패 시 재시도하지 않는다
  - 근거: 3회 이상 실패는 대부분 구현 문제가 아니라 스펙 문제다
- 에스컬레이션: 사람이 feature 파일의 완성 기준을 재검토하고 수정 여부를 결정한다
- 시도 번호 = 해당 기능의 failure-report 파일 수 + 1 (구현·검증 공통)
- failure-report의 형식·파일명·이동 규칙은 docs/roles/verifier.md 가 SSOT (verifier 전용)

### 역할 위반 거부
- 지시에 두 역할의 작업이 모두 포함되어 있으면 즉시 거부한다
- 거부 메시지: "역할 분리 원칙 위반: 구현과 검증은 별도 세션에서 수행해야 합니다."

## 프로젝트 맥락
- 프로젝트 개요·기술 컨텍스트: docs/overview.md
- 단위 작업 시 업무 개요는 보통 불필요 — 필요한 섹션만 읽는다 (implementer/verifier는 "기술 컨텍스트"만, 필요 시)
- 메인(오케스트레이션) 세션은 본격 작업 전 overview.md가 비어 있으면(`(미작성)`) 사용자에게 물어 채운다. 하위 역할 세션(implementer/verifier)은 이 규칙을 트리거하지 않는다 (이미 채워져 있다고 가정)

## 문서 관리
- 문서 작성·정리 시: docs/conventions.md 읽기 (3층 구조: 인덱스 + 공유핵심 + 단위별 파일)

## 역할 부여 방법
- 구현: "implementer 역할로 [기능명] 구현해줘" → docs/roles/implementer.md 읽기
- 검증: "verifier 역할로 [기능명] 검증해줘" → docs/roles/verifier.md 읽기
- 표준 절차: docs/skills/implement.md, docs/skills/verify.md 참고
- 작업 흐름·상태 전이·승인 게이트: docs/workflow.md 참고

향후 자동화 계획(미구현)은 docs/roadmap.md 참고.
