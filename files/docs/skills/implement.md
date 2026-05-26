# 스킬: 기능 구현 (Implement)

구현 워크플로우의 표준 진입점. 매번 동일한 절차로 시작하기 위해 사용한다.

## 사전 조건 (사람이 확인)
- [ ] feature 파일이 존재하고 완성 기준이 작성되어 있는가
- [ ] docs/index.md에서 해당 기능의 승인자 컬럼이 기입되어 있는가
- [ ] feature 파일의 "구현 위치" 섹션이 있는가 (첫 시도면 비어있어도 됨)
- [ ] 이전 시도가 있다면 failure-report 파일(`[기능명]-failure-report-N.md`)이 존재하는가

## 시작 방법
```
새 Claude Code 세션을 열고 다음을 입력:
"implementer 역할로 [기능명] 구현해줘"
```

## (참고) 에이전트 수행 순서
에이전트는 역할 파일(implementer.md)의 지시에 따라 아래 순서로 수행한다.
이 섹션은 사람이 흐름을 파악하기 위한 참고용이며, 에이전트가 이 파일을 읽지 않아도 된다.

1. CLAUDE.md 읽기
2. docs/roles/implementer.md 읽기
3. docs/index.md에서 승인자 확인
4. docs/features/[기능명].md 읽기
5. docs/features/[기능명]-failure-report-*.md 읽기 (있을 경우)
6. docs/shared.md 읽기 (의존성 명시된 경우)
7. 구현
8. shared.md 갱신 (스키마/타입 변경 시)
9. feature 파일의 "구현 위치" 섹션 작성/갱신
10. 완료 보고

## 완료 후
구현 완료 보고 후 상태 전이는 docs/workflow.md 가 SSOT (요약: → 검증중).
검증은 반드시 별도 새 세션에서 시작한다 (docs/skills/verify.md).
