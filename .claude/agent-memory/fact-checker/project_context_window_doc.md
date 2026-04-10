---
name: context-window.md 팩트체크 결과
description: 2026-04-11 수행한 공식 docs 대비 오류 검토 기록 (Hook 가시성 오류, ENABLE_TOOL_SEARCH 설명/누락 오류 발견)
type: project
---

context-window.md 팩트체크 결과 (2026-04-11, 재검토 포함)

**Why:** 공식 문서(https://code.claude.com/docs/en/context-window, /en/memory, /en/mcp, /en/hooks)와 교차 검증.

**오류 발견:**
1. Hook 출력 가시성이 `full`로 기재되었으나 공식 EVENTS 배열에서 `vis: 'hidden'`으로 명시됨.
2. ENABLE_TOOL_SEARCH=auto 설명 방향 모호: "10% 이내 범위에서 미리 로드"는 오해 소지. 정확한 의미는 "모든 MCP 도구 스키마 합이 컨텍스트 윈도우의 10% 이내면 전부 미리 로드, 초과면 지연".
3. ENABLE_TOOL_SEARCH=true 값이 누락됨 (비공식 ANTHROPIC_BASE_URL에서도 강제 지연 로드).
4. ENABLE_TOOL_SEARCH=auto:<N> 형태(커스텀 임계값)가 누락됨.
5. Hook 출력 진입 방식 설명 불완전: hookSpecificOutput.additionalContext 외에도 최상위 additionalContext, systemMessage, plain stdout(exit 0)도 진입 가능.

**확인 완료된 주요 사항:**
- 가시성 3단계(hidden/brief/full) 정확
- 1단계 자동 로드 토큰 예시 (4200/680/280/120/450/320/1800) 모두 정확
- Auto memory 200줄/25KB 제한 정확
- /compact 후 스킬 설명 재주입 안 됨 정확 (noSurviveCompact: true 코드 확인)
- 컴팩션 12% = 코드에서 Math.round(sumTokens * 0.12) 하드코딩 확인
- 서브에이전트 별도 컨텍스트, auto memory 미포함 정확
- disable-model-invocation: true → 호출 전 컨텍스트 비용 0 정확
- Hook 출력 10,000자 제한 정확 (공식 hooks 레퍼런스 확인)
- 컨텍스트 절약 예시 수치 (6,100토큰 → 420토큰) 정확

**How to apply:** 이 문서 재검토 시 Hook 가시성(full→hidden), ENABLE_TOOL_SEARCH 옵션 표(true 행과 auto:<N> 행 추가), Hook additionalContext 진입 경로 설명을 우선 확인.
