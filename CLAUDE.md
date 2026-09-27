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