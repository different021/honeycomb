# 작업 흐름 (Workflow)

구현/검증 사이클의 운영 규칙. 상태 전이·승인 게이트의 SSOT.

## 상태 전이 (SSOT)

상태 값: `대기` | `구현중` | `검증중` | `완료` | `에스컬레이션`

| 전이 | 시점 | 갱신 책임 |
|------|------|-----------|
| (신규) → `대기` | feature 파일 작성 + 승인 게이트 통과 시 | 사람 |
| `대기` → `구현중` | 구현 착수 시 | 구현을 지시한 사람 |
| `구현중` → `검증중` | 구현 완료 보고 후 | 검증을 지시한 사람 |
| `검증중` → `완료` | 검증 PASS 시 | 검증을 지시한 사람 |
| `검증중` → `구현중` | 검증 FAIL (1~2회) 시 | 다음 시도를 지시한 사람 |
| `검증중` → `에스컬레이션` | 검증 FAIL 3회 시 | 검증을 지시한 사람 |

상태 값은 docs/index.md 기능 테이블의 `상태` 컬럼에 기록한다.

## 승인 게이트 (구현 착수 전 필수)

아래 조건을 모두 충족해야 `대기` 상태로 진입한다:
- [ ] feature 파일의 완성 기준이 작성되어 있는가
- [ ] 각 기준은 구현 없이도 PASS/FAIL 판정이 가능한가
- [ ] 누락된 예외 케이스는 없는가
- [ ] 승인자가 서명했는가 (docs/index.md 기능 테이블 `승인자` 컬럼 기입)

## 추적성 — commit 메시지에 feature scope 의무

모든 feature 작업의 commit 메시지는 **conventional-commits 형식 + scope = feature slug** 로 박는다.

- 형식: `<type>(<feature-slug>): <메시지>`
  - `<type>`: `feat` / `fix` / `refactor` / `test` / `docs` / `chore` 등
  - `<feature-slug>`: 해당 feature의 슬러그 (`docs/features/<slug>.md`의 파일명)
- 예:
  - `feat(health-endpoint): add /health route returning ok`
  - `test(health-endpoint): add /nope 404 case`
  - `refactor(powermonitor): extract list endpoint into module`
- 목적: plan ↔ commit 양방향 자동 추적. `git log --grep="(<slug>)"` 한 줄로 feature의 전체 변경 이력이 나옴.
- 적용 범위: 구현·검증·문서 갱신·해당 feature의 hotfix 전부.
- 무관 변경은 **별 feature·별 commit**으로 분리. 한 commit이 두 feature를 건드리지 않음.
- 위반 시: 이미 머지된 건 amend 비추(history 변경 위험), 다음 commit부터 다시 prefix.

## 보드 거버넌스 — index.md는 보드, 죽으면 전체가 죽는다

`docs/index.md`의 기능 테이블이 **이 프로젝트의 보드**다. 별도 추적 도구 없음.

- 상태 전이는 **즉시** 반영. "나중에 한꺼번에" 금지 — 미루는 순간 보드가 현실과 어긋나기 시작하고, 곧 죽는다.
- 위 갱신 책임 표가 *한 명을 정확히 지목*한다. "누군가 하겠지" 금지.
- **한 트랙이 끝나도 보드는 안 죽는다.** 다음 feature가 곧장 등재된다. 보드 수명 ≠ 트랙 수명.
- 근거 (이전 사례): smart-line2 2026-04~05 시도는 첫 트랙 완료 직후 `board.md` 갱신 정지(22일) → 70+ plans가 가시성 없이 진행 → 외부엔 "사라진 시도"로 보이게 됨. 코드는 50~70% 머지됐는데 보드 사망 때문에 추적 불가. **같은 실패 피하려면 보드를 트랙과 분리 + 즉시 갱신.**

## 전체 흐름

```
1. feature 파일 작성 (docs/features/_template.md 복사) → 승인 게이트 통과 → 상태 "대기"
2. "implementer 역할로 [기능] 구현해줘" (별도 세션 권장) → 상태 "구현중"
   세부 절차: docs/skills/implement.md
3. "verifier 역할로 [기능] 검증해줘" (별도 세션 필수) → 상태 "검증중"
   세부 절차: docs/skills/verify.md
4. PASS → 완료 / FAIL → 2번으로 (최대 3회)
5. 3회 실패 → 에스컬레이션 → 사람이 완성 기준 재검토
   재검토·수정 결정 후 시도 카운터 리셋(failure-report 모두 failures/ 이동) 후 재시작

모든 단계의 commit은 위 "추적성" 규칙을 따른다. 모든 상태 전이는 즉시 index.md에 반영한다.
```
