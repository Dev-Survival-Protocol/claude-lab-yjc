---
name: discover-plugins.md 팩트체크 결과
description: 2026-03-22 수행한 공식 docs 대비 오류 검토 기록 (agent-sdk-dev 누락, /reload-plugins LSP 제한 누락, 버전 요구사항 누락)
type: project
---

2026-03-22에 `/Users/yjc/Workspace/claude-lab-yjc/building-with-claude-code/discover-plugins.md` 팩트체크 수행.
원본 소스: https://code.claude.com/docs/ko/discover-plugins (접근 성공)

**Why:** 요약 문서가 원본 공식 문서와 얼마나 정확하게 일치하는지 검증하기 위해 수행.

**How to apply:** 이 문서를 재검토하거나 업데이트할 때 아래 확인된 오류 사항을 반영해야 함.

## 확인된 오류

1. **agent-sdk-dev 누락**: 개발 워크플로우 카테고리 표에 `agent-sdk-dev` 플러그인이 빠져 있음. 원본에 명시되어 있음.
2. **/reload-plugins 동작 불완전**: LSP 서버 변경사항은 /reload-plugins로 적용되지 않고 재시작이 필요하다는 중요 제한 사항 누락.
3. **버전 요구사항 누락**: 플러그인 기능 사용에 Claude Code 버전 1.0.33 이상이 필요하다는 내용 누락.
4. **외부 통합 플러그인 일부 누락**: atlassian, asana, notion, figma, vercel, firebase, supabase 등이 표에 없음 (단, "등"으로 표현하고 있어 심각도 낮음).

## 확인 완료 항목

- 공식 마켓플레이스 이름 `claude-plugins-official`: 정확
- LSP 플러그인 이름 및 바이너리 전체 테이블(11개 언어): 정확
- 설치 범위 4가지(User/Project/Local/Managed): 정확
- 환경 변수 DISABLE_AUTOUPDATER, FORCE_AUTOUPDATE_PLUGINS=true: 정확
- 마켓플레이스 소스 유형 6가지: 정확
- 플러그인 명령어 구문 전반: 정확
- 캐시 경로 ~/.claude/plugins/cache: 정확
- extraKnownMarketplaces JSON 구조: 정확

## 누락된 개선 사항

- `/plugin market` 단축 명령 (원본에 있으나 요약에 없음)
- 보안 경고 섹션 (신뢰할 수 있는 소스에서만 설치)
