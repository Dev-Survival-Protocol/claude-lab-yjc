---
name: permission-modes.md 팩트체크 결과
description: 2026-04-11 permission-modes.md 공식 docs 대비 오류 검토 기록 (2회차 상세 검증 완료)
type: project
---

2026-04-11 수행한 `claude-code-basic/permission-modes.md` 팩트체크 결과 (2회차 상세 검증).

**Why:** 원본 https://code.claude.com/docs/ko/permission-modes 와 비교 검증.

**오류 (즉시 수정 필요)**:
1. `--allow-dangerously-skip-permissions` 플래그 완전 누락 — 공식 문서에는 세 번째 bypassPermissions 관련 플래그가 존재. 이 플래그는 모드를 활성화하지 않고 순환 목록에만 추가함.
2. plan 모드 완료 후 옵션 표현 불정확 — "피드백 후 재계획" 대신 "계획을 계속하여 추가 라운드 진행"이 정확함. 각 승인 옵션 선택 시 계획 컨텍스트 초기화 제안 동작도 누락.
3. bypassPermissions 섹션에서 `.git` 하나만 예시로 들어 보호 디렉토리 목록 불완전 — `.claude`도 보호 대상이나 누락.
4. 분류기 입력 설명 불완전 — CLAUDE.md 콘텐츠도 분류기 입력으로 들어감을 누락.
5. 비교 표 auto 안전 검사 셀 — "분류기가 검토"만 표기했으나, 정확히는 "분류기가 명령 및 보호된 디렉토리 쓰기 검토".
6. 기본 차단 항목 누락 2개 — "공유 인프라 수정", "세션 시작 전에 존재했던 파일을 되돌릴 수 없게 삭제".

**의심 사항 (확인 권장)**:
- Shift+Tab 순환에서 auto 조건부 표시 미언급 — 기본 순환에 포함 안됨, `--enable-auto-mode` 필요.
- dontAsk 모드에서 `ask` 규칙 붙은 도구도 거부(프롬프트 아님)됨 누락.
- Team/Enterprise의 관리자 사전 활성화 요건 누락.
- 자동 모드 진입 시 무제한 허용 규칙(`Bash(*)` 등) 자동 삭제 및 종료 시 복원 동작 누락.
- 서브에이전트와 자동 모드 상호작용 섹션 전체 누락.
- `claude auto-mode defaults` 명령 미언급.

**정확하게 검증된 항목**:
- 보호 디렉토리 목록 (.git/.vscode/.idea/.husky/.claude), 예외 경로 (.claude/commands/.agents/.skills)
- Shift+Tab 순환 순서, auto 모드 플랜 요건, 모델 요건 (Sonnet/Opus 4.6)
- 분류기 모델 (Sonnet 4.6 고정), 폴백 임계값 (연속 3회 / 총 20회, 구성 불가)
- defaultMode JSON 구조, --enable-auto-mode 플래그, --dangerously-skip-permissions 플래그
- PermissionRequest 훅 이름, 비교 표 plan 제외 (공식도 동일)

**How to apply:** 이 문서 재검토 또는 수정 시 위 항목 기준으로 확인.
