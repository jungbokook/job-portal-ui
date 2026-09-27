---
paths:
  - "src/pages/**"
  - "src/components/ProtectedRoute*"
  - "src/App.jsx"
description: 라우팅 구조, 역할별 접근 제한, 접근 제어 컨벤션
---

# 라우팅 & 역할 규칙

## 역할 정의

역할은 세 가지이며, 역할마다 접근할 수 있는 보호 라우트가 다릅니다.

| 역할              | 접근 가능한 라우트                                   |
| ----------------- | ---------------------------------------------------- |
| `ROLE_JOB_SEEKER` | `/profile`, `/applied-jobs`, `/saved-jobs`           |
| `ROLE_EMPLOYER`   | `/post-job`, `/employer/jobs`, `/job-applicants/:id` |
| `ROLE_ADMIN`      | `/admin/*` (`src/pages/admin/`의 모든 관리자 페이지)  |

## 라우트 보호

- 모든 보호 라우트는 `src/components/`의 `ProtectedRoute` 컴포넌트를 사용합니다.
- `ProtectedRoute`는 `AuthContext`에서 현재 사용자의 역할을 읽습니다.
- 로그인하지 않은 사용자는 `/login`으로 리다이렉트됩니다.
- 역할이 맞지 않으면 404가 아니라 알맞은 대체 페이지로 리다이렉트됩니다.

## 새 페이지 추가

1. `src/pages/`에 컴포넌트를 만듭니다. 관리자 페이지는 `src/pages/admin/`에 만듭니다.
2. `src/App.jsx`에 라우트를 등록합니다.
3. 접근을 제한해야 하면 `<ProtectedRoute>`로 감싸고 필요한 역할을 지정합니다.

## 내비게이션

- 내부 이동에는 React Router의 `<Link>`를 사용합니다. 내부 라우트에 일반 `<a>` 태그를 쓰면 안 됩니다.
- `<Navbar>`와 `<Footer>`는 `src/components/`에 있는 공용 레이아웃 컴포넌트입니다.