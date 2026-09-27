---
description: 이 저장소의 브랜치, 커밋 메시지, Pull Request 컨벤션
---

# Git 컨벤션

## 브랜치

```
feature/add-job-filter-sidebar         # 새 기능
fix/employer-route-redirect-loop       # 버그 수정
docs/update-readme                     # 문서만 변경
chore/upgrade-dependencies             # 유지보수, 도구 설정
refactor/simplify-auth-context         # 코드 리팩터링
style/mobile-job-card-spacing          # 화면/스타일 변경
```

- 모든 새 작업은 `main`에서 브랜치를 따서 시작합니다.
- 브랜치는 짧게 유지하고, 준비되면 PR을 엽니다.
- 머지한 뒤에는 브랜치를 삭제합니다.

## 커밋 메시지

**Conventional Commits** 규칙을 따릅니다.

```
feat: add saved jobs count to navbar
fix: correct role guard on employer routes
docs: update README with localStorage keys
chore: upgrade react-router to v7.8
refactor: extract job card into reusable component
style: fix spacing on mobile job list
```

- 현재 시제, 소문자로 쓰고 끝에 마침표를 붙이지 않습니다.
- 제목 줄은 72자 이내로 씁니다.
- 변경 이유가 분명하지 않으면 본문(body)을 추가합니다.

## Pull Request

- PR 제목은 Conventional Commits 형식을 따라야 합니다.
- PR 설명에 요약과 테스트 계획을 포함합니다.
- 베이스 브랜치는 `main`입니다.