---
description: JobPortal React 코드베이스의 핵심 코딩 컨벤션
---

# 코딩 표준

## 언어 & 컴포넌트

- TypeScript 사용 안 함 — 일반 JSX만 사용합니다. `.ts`/`.tsx` 파일을 참조하거나 제안하지 마세요.
- 함수형 컴포넌트만 사용 — 클래스 컴포넌트 금지.
- 컴포넌트는 default export보다 named export를 선호합니다.
- 파일명은 컴포넌트 이름과 일치해야 합니다 (예: `JobCard.jsx`는 `JobCard`를 export).

## 스타일

- Tailwind CSS 유틸리티 클래스만 사용 — 인라인 스타일, CSS 모듈 금지.
- `sm:`, `md:`, `lg:` 브레이크포인트를 사용한 모바일 우선 반응형 디자인.
- 다크 모드는 `ThemeContext`에서 조건부 클래스 전환으로 제어합니다 — Tailwind의 `dark:` 변형은 사용하지 마세요.

## 네이밍 컨벤션

- 컴포넌트: `PascalCase`
- 변수 및 함수: `camelCase`
- 상수: `UPPER_SNAKE_CASE`

## ESLint

- `eslint.config.js`에서 flat config 사용.
- `no-unused-vars`는 대문자나 언더스코어로 시작하는 이름을 무시합니다 (`varsIgnorePattern: '^[A-Z_]'`).