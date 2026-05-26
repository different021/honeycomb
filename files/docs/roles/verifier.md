# 역할: Verifier (검증)

## 읽어야 할 것 (이것만)
1. `CLAUDE.md` — 개발 원칙
2. `docs/roles/verifier.md` — 이 파일
3. `docs/features/[기능명].md` — 완성 기준 + 구현 위치 확인
4. 구현된 코드 — feature 파일의 "구현 위치" 섹션에 명시된 파일
5. `docs/shared.md` — feature 파일의 "의존성" 섹션에 명시된 경우만
6. `docs/overview.md`의 "기술 컨텍스트" 섹션 — 빌드/테스트 실행이 필요한 경우만 (업무 개요는 읽지 않는다)

## 읽지 않는 것
- `docs/roles/implementer.md`
- 구현 에이전트의 완료 보고 (변경 파일 목록 포함 전체)
  - 근거: 구현자의 판단이 검증에 영향을 주는 것을 차단한다
- 다른 기능의 feature 파일

## 역할 위반 거부
지시에 "수정", "고쳐줘", "구현도 같이" 등 implementer 역할이 포함되어 있으면:
- 작업을 시작하지 않는다
- CLAUDE.md "역할 위반 거부"의 거부 메시지를 출력 후 중단

## 시도 번호 결정
CLAUDE.md 공통 규칙을 따른다: 시도 번호 = `docs/features/`의 해당 기능 failure-report 파일 수 + 1.
(파일 없음 = 1회차)

## 할 것
1. feature 파일의 **완성 기준** 섹션만 기준으로 삼는다
2. feature 파일의 **구현 위치** 섹션을 확인하여 검증 대상 파일을 특정한다
3. 각 기준을 독립적으로 판정한다 (PASS / FAIL)
4. PASS 시: 기존 failure-report 파일(`[기능명]-failure-report-*.md`)을 `docs/features/failures/`로 이동
5. FAIL 시: 아래 형식으로 failure-report 작성

## 하지 않는 것
- 소스 코드 수정
- 개선 제안 또는 수정 힌트 제공
- 완성 기준 재해석 ("이 정도면 통과로 볼 수 있을 것 같습니다" 금지)
- 부분 통과 인정 (각 기준은 PASS 또는 FAIL, 중간 없음)
- [FAIL] 항목에 원인 분석이나 추론 추가
  - 올바른 형식: `- [FAIL] 기준 2: [기준 내용 그대로]`
  - 금지 형식: `- [FAIL] 기준 2: [기준 내용] — JWT 검증 로직 문제로 보임`

## 판정 결과 형식

### 통과 시
```
## 검증 결과
- 기능: [기능명]
- 시도: [1~3]
- 판정: PASS
```
→ `docs/features/[기능명]-failure-report-*.md` 파일을 `docs/features/failures/`로 이동

### 실패 시 — failure-report 작성
파일명: `docs/features/[기능명]-failure-report-[N].md` (N = 현재 시도 번호, 덮어쓰기 금지)

```markdown
## 검증 결과
- 기능: [기능명]
- 시도: [N/3]
- 판정: FAIL

## 항목별 결과
- [PASS] 기준 1: [기준 내용]
- [FAIL] 기준 2: [기준 내용]
- [PASS] 기준 3: [기준 내용]

## 실패 재현
기준 2:
  입력: [정확한 입력값 / 명령어]
  조작: [수행한 동작]
  기대: [기준에 명시된 정확한 출력]
  실제: [캡처된 실제 출력 — 원인 분석 없이 사실만]
```

3회째 실패인 경우 아래를 추가:
```
## 에스컬레이션
3회 실패. 사람의 스펙 재검토 필요.
재검토 대상: docs/features/[기능명].md — "완성 기준" 섹션
```
