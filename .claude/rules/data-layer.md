---
paths:
  - "src/services/**"
  - "src/context/**"
  - "src/contexts/**"
  - "src/data/**"
description: 데이터 흐름, 상태 관리, localStorage 컨벤션
---

# 데이터 계층 규칙

## 컨텍스트 구조

React Context는 두 계층으로 나뉘며, 서로 섞지 않습니다.

- `src/context/` — 핵심 런타임 상태:
  - `AuthContext` — 인증, 더미 사용자, localStorage 저장
  - `JobContext` — 지원 내역, 저장한 공고, 기업의 공고 CRUD
  - `ThemeContext` — 다크/라이트 모드 전환
- `src/contexts/` — 캐싱이 적용된 데이터 조회:
  - `JobsDataContext` — 5분 TTL로 캐시되는 공고 목록
  - `CompaniesContext` — 회사 목록

**Provider 중첩 순서** (`App.jsx`에 정의):
`AuthProvider → JobsDataProvider → JobProvider → CompaniesProvider → ThemeProvider`

## 서비스 계층 규칙

- 모든 비동기 서비스 함수는 `src/utils/delay.js`의 `delay()`를 호출해 지연 시간을 흉내 내야 합니다.
- 페이지 컴포넌트에서 직접 데이터를 가져오면 안 됩니다. `src/services/`의 서비스를 사용하세요.
- 목 데이터의 원본은 `src/data/mockData.js`입니다.

## localStorage 키 패턴

| 키                         | 저장하는 내용                     |
| -------------------------- | --------------------------------- |
| `jobPortalUser`            | 현재 로그인한 사용자 객체         |
| `authToken`                | 세션 인증 토큰                    |
| `registeredUsers`          | 가입된 모든 사용자 계정           |
| `globalPostedJobs`         | 기업이 등록한 모든 공고           |
| `jobApplications_{userId}` | 사용자가 제출한 지원서            |
| `savedJobs_{userId}`       | 사용자가 저장(북마크)한 공고      |
| `postedJobs_{userId}`      | 기업 회원이 등록한 공고           |

`{userId}` 접미사에는 항상 로그인한 사용자의 ID가 들어갑니다. 사용자별 키에서는 절대 빼먹지 마세요.