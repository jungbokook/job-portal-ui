# CLAUDE.md

이 파일은 Claude Code(claude.ai/code)가 이 저장소의 코드를 다룰 때 참고하는 가이드입니다.

## 명령어

- `npm run dev` — Vite 개발 서버 실행
- `npm run build` — 프로덕션 빌드
- `npm run lint` — ESLint 실행 (flat config, JS/JSX만 대상)
- `npm run preview` — 프로덕션 빌드 미리보기

## 저장소 구조

```
job-portal-ui/
├── public/               # 정적 자산 (파비콘, 회사 로고)
├── src/
│   ├── components/       # 재사용 UI 컴포넌트 (Navbar, Footer, Layout, ProtectedRoute 등)
│   ├── context/          # 핵심 React 컨텍스트: AuthContext, JobContext, ThemeContext
│   ├── contexts/         # 데이터 조회 컨텍스트: JobsDataContext, CompaniesContext
│   ├── data/             # mockData.js — 모든 시드 데이터 (채용공고, 회사, 사용자)
│   ├── pages/            # 라우트 단위 페이지 컴포넌트
│   │   └── admin/        # 관리자 전용 페이지 (Dashboard, CompanyManagement 등)
│   ├── services/         # 비동기 API를 흉내 내는 서비스 함수
│   ├── utils/            # 공용 유틸리티 (delay.js)
│   ├── App.jsx           # 루트 컴포넌트 — 라우터 + Provider 트리
│   ├── main.jsx          # 진입점
│   └── index.css         # 전역 스타일 (Tailwind import)
├── eslint.config.js      # ESLint flat config
├── vite.config.js        # Vite 설정
└── index.html            # HTML 진입점
```

**어디를 봐야 하나:**

- 새 페이지 추가 → `src/pages/`에 만들고 `App.jsx`에 라우트 등록
- 공용 UI → `src/components/`
- 인증 로직 → `src/context/AuthContext.jsx`
- 채용공고/지원 로직 → `src/context/JobContext.jsx`
- 목(mock) 데이터 수정 → `src/data/mockData.js`
- API 시뮬레이션 → `src/services/`

## Git 컨벤션

### 브랜치

```
feature/add-job-filter-sidebar         # 새 기능
fix/employer-route-redirect-loop       # 버그 수정
docs/update-readme                     # 문서만 변경
chore/upgrade-dependencies             # 유지보수, 도구 설정
refactor/simplify-auth-context         # 코드 리팩터링
style/mobile-job-card-spacing          # 화면/스타일 변경
```

- 모든 새 작업은 `main`에서 브랜치를 따서 시작
- 브랜치는 짧게 유지하고, 준비되면 PR 생성
- 머지 후 브랜치 삭제

### 커밋 메시지

**Conventional Commits** 규칙을 따릅니다:

```
feat: add saved jobs count to navbar
fix: correct role guard on employer routes
docs: update README with localStorage keys
chore: upgrade react-router to v7.8
refactor: extract job card into reusable component
style: fix spacing on mobile job list
```

- 현재 시제, 소문자로 쓰고 끝에 마침표를 붙이지 않음
- 제목 줄은 72자 이내
- 변경 이유가 명확하지 않으면 본문(body)을 추가

### Pull Request

- PR 제목은 커밋 메시지 형식과 동일하게
- PR 설명에 요약과 테스트 계획을 포함
- 베이스 브랜치는 `main`

## 코딩 표준

### 일반

- **TypeScript 사용 안 함** — 전부 일반 JSX로 작성하며 `.ts`/`.tsx` 파일을 추가하지 않음
- **함수형 컴포넌트만 사용** — 클래스 컴포넌트 금지
- 컴포넌트는 default export보다 **named export**를 선호
- 컴포넌트는 한 가지 역할에 집중 — 재사용 가능한 부분은 `src/components/`로 분리

### 스타일

- **Tailwind CSS 유틸리티 클래스만** 사용 — 인라인 스타일, CSS 모듈 금지
- 모바일 우선 반응형 디자인 (`sm:`, `md:`, `lg:` 브레이크포인트)
- 다크 모드는 `ThemeContext`로 처리 — `dark:` 변형 대신 조건부 클래스 전환 사용

### 상태 & 데이터

- 공유 상태는 React Context 사용 — 외부 상태 관리 라이브러리 금지
- 페이지 컴포넌트에서 직접 데이터를 가져오지 말고 `src/services/`의 서비스 사용
- 모든 비동기 서비스 호출은 `delay()`로 지연 시간을 흉내 내야 함
- 사용자별 데이터는 정해진 키 패턴(`{entity}_{userId}`)으로 localStorage에 저장

### 네이밍

- 컴포넌트: `PascalCase` (예: `JobCard.jsx`)
- 변수/함수: `camelCase`
- 상수: `UPPER_SNAKE_CASE`
- 파일명: default export 이름과 일치 (예: `JobCard.jsx`는 `JobCard`를 export)

### ESLint

Flat config(`eslint.config.js`) 사용. `no-unused-vars` 규칙은 대문자나 언더스코어로 시작하는 변수를 무시합니다(`varsIgnorePattern: '^[A-Z_]'`). 커밋 전에 `npm run lint`를 실행하세요.

## 아키텍처

Vite 7, Tailwind CSS 4, React Router 7 기반의 React 19 SPA입니다. TypeScript 없이 전부 일반 JSX로 작성되어 있습니다.

### 상태 관리

React Context가 두 계층으로 나뉩니다:

- **`src/context/`** — 핵심 컨텍스트: `AuthContext`(인증 + 더미 사용자 + localStorage 저장), `JobContext`(지원 내역, 저장한 공고, 기업의 공고 CRUD), `ThemeContext`
- **`src/contexts/`** — 데이터 조회 컨텍스트: `JobsDataContext`(5분 TTL로 캐시되는 공고 목록), `CompaniesContext`

Provider 중첩 순서 (App.jsx): AuthProvider → JobsDataProvider → JobProvider → CompaniesProvider → ThemeProvider

### 데이터 계층

현재는 실제 백엔드 없이 **목 데이터**와 localStorage 저장을 사용합니다. `src/services/`의 서비스들은 `src/utils/delay.js`의 `delay()`로 비동기 API 호출을 흉내 냅니다. 데이터의 원본은 `src/data/mockData.js`입니다.

주요 localStorage 키: `jobPortalUser`, `authToken`, `registeredUsers`, `globalPostedJobs`, `jobApplications_{userId}`, `savedJobs_{userId}`, `postedJobs_{userId}`.

### 라우팅 & 역할

`ProtectedRoute` 컴포넌트로 라우트를 보호하며, 역할은 세 가지입니다:

- **ROLE_JOB_SEEKER** (구직자) — profile, applied-jobs, saved-jobs
- **ROLE_EMPLOYER** (기업) — post-job, employer/jobs, job-applicants/:jobId
- **ROLE_ADMIN** (관리자) — admin/\*, 관리자 페이지는 `src/pages/admin/`에 위치

### 주요 라이브러리

- 아이콘: Font Awesome + Lucide React
- 알림: react-toastify

### ESLint

Flat config(`eslint.config.js`) 사용. `no-unused-vars` 규칙은 대문자나 언더스코어로 시작하는 변수를 무시합니다(`varsIgnorePattern: '^[A-Z_]'`).
