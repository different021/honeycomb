---
name: honeycomb
description: "구현/검증 분리 + 최소 컨텍스트 + 문서 3층 구조의 에이전트 작업 프레임(honeycomb)을 현재 프로젝트에 스캐폴딩한다. 새 프로젝트에서 이 프레임을 도입하거나 재사용할 때 사용."
user-invocable: true
---

# Honeycomb

구현/검증을 분리하고 최소 컨텍스트로 운영하는 **에이전트 작업 프레임**을 현재 프로젝트에 설치한다.
단위 작업은 자족적 셀로, 공통 규약은 공유 셀로 — 벌집처럼 가볍게 결합하는 구조.
smart-link에서 검증된 프레임(구현/검증 역할 분리, 완성 기준 불변, 문서 3층 구조, 독립 검증 루프)을 재사용한다.

## 구성
- `files/CLAUDE.md` — 개발 원칙(역할 분리·완성기준 불변·최소 컨텍스트·실패 처리·역할 위반 거부) + 포인터. 프로젝트 특정 내용 0.
- `files/docs/` — conventions(문서 3층 규칙), workflow(상태 전이·승인 게이트), roles/(implementer·verifier), skills/(implement·verify 절차), features/_template, shared(빈), overview(빈), index(빈)

## References
- @procedure.md — 설치 절차 (복사 → CLAUDE.md 충돌 처리 → overview 채우기 → 워크플로우 안내)
- `files/` — 스캐폴딩할 템플릿 트리
