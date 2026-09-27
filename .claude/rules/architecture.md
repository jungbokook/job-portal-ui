---
description: 전체 아키텍처 개요 — 기술 스택, 컨텍스트 계층, 주요 라이브러리
---

# 아키텍처

Vite 7, Tailwind CSS 4, React Router 7 기반의 React 19 SPA입니다. TypeScript는 쓰지 않고 전부 일반 JSX로 작성합니다.

## 기술 스택

| 계층   | 기술                                |
| ------ | ----------------------------------- |
| UI     | React 19, Tailwind CSS 4            |
| 라우팅 | React Router 7                      |
| 빌드   | Vite 7                              |
| 아이콘 | Font Awesome, Lucide React          |
| 토스트 | react-toastify                      |
| 데이터 | 목 데이터 + localStorage (API 없음) |

## 상태 관리

React Context가 두 계층으로 나뉘며, 서로 섞지 않습니다.

- **`src/context/`** — 핵심 런타임 상태 (인증, 채용공고, 테마)
- **`src/contexts/`** — 캐싱이 적용된 데이터 조회 컨텍스트 (공고 목록, 회사)

Provider 중첩 순서 (`App.jsx`에 정의):
`AuthProvider → JobsDataProvider → JobProvider → CompaniesProvider → ThemeProvider`

하위 컴포넌트가 이 순서에 의존하므로 중첩 순서를 바꾸지 마세요.

## 어디를 봐야 하나

| 작업               | 위치                                             |
| ------------------ | ------------------------------------------------ |
| 새 페이지 추가     | `src/pages/`에 만들고 `src/App.jsx`에 라우트 등록 |
| 공용 UI 컴포넌트   | `src/components/`                                |
| 인증 로직          | `src/context/AuthContext.jsx`                    |
| 채용공고/지원 로직 | `src/context/JobContext.jsx`                     |
| 목 데이터 수정     | `src/data/mockData.js`                           |
| API 시뮬레이션     | `src/services/`                                  |