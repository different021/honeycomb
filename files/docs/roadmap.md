# 향후 적용 계획 (미구현)

현재 텍스트 원칙으로만 존재하며, settings.json 훅으로 자동화 예정인 항목.

## 역할/완성기준 강제 훅
- PreToolUse(Edit/Write): feature 파일의 "완성 기준" 섹션 수정 감지 시 중단
- failure-report 파일 3개 감지 시 자동 에스컬레이션 알림
- 두 역할 파일(implementer.md + verifier.md) 동시 읽기 감지 시 경고
