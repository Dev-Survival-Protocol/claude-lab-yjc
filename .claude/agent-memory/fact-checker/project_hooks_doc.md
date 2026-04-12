---
name: hooks.md 팩트체크 결과
description: 2026-04-12 수행한 공식 docs 대비 hooks.md 오류 검토 기록
type: project
---

2026-04-12, building-with-claude-code/hooks.md를 code.claude.com/docs/en/hooks 및 ko/hooks와 대조 검토.

**확인된 오류:**
- HTTP hook 기본 타임아웃(30초) 누락 — 공통 필드 표에 http:30 추가 필요
- Stop 이벤트 주요 이벤트 요약 테이블에서 중복 행 존재 (153행, 161행)
- $CLAUDE_ENV_FILE의 사용 가능 범위 미표기 — SessionStart/CwdChanged/FileChanged 전용
- InstructionsLoaded 매처 패턴에서 path_glob_match, compact 누락
- SessionEnd 매처 패턴에서 bypass_permissions_disabled, other 누락
- Notification 매처 패턴에서 auth_success, elicitation_dialog 누락
- ConfigChange 매처 패턴에서 local_settings, policy_settings, skills 누락
- StopFailure 매처 패턴에서 invalid_request, server_error, max_output_tokens, unknown 누락
- additionalContext가 공통 출력 필드임에도 PreToolUse 전용 블록에만 표기됨

**확인 완료 (정확):**
- 훅 타입 4종, 설정 위치 6곳, 종료 코드, 이벤트 26개 목록, 기본 타임아웃(http 제외), shell 기본값 bash, allowedEnvVars, permissionDecision 4종 값, 경로 변수 5종, /hooks 명령, disableAllHooks, SessionEnd 1.5초 타임아웃

**패턴:**
- 매처 패턴 테이블의 값 목록이 공식 문서보다 일관되게 불완전함 — 여러 이벤트에서 반복
- 공통 출력 필드와 이벤트 전용 필드 구분이 불명확

**Why:** 공식 문서의 상세 매처 값이 로컬 문서 작성 시점에 업데이트되었거나 의도적으로 축약된 것으로 보임
**How to apply:** hooks.md 검토 시 매처 패턴 테이블의 완전성을 우선 확인할 것
