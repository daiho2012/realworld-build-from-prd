# RealWorld (Conduit) 구현 작업 목록

## 개요
이 문서는 RealWorld (Conduit) 소셜 블로깅 플랫폼을 구현하기 위한 상세 작업 목록입니다.
PRD 문서와 [RealWorld 공식 사양](https://realworld-docs.netlify.app/)을 기반으로 작성되었습니다.

## 기술 스택
- **백엔드**: Go (Echo/Gin), SQLite, JWT
- **프론트엔드**: React 18, TypeScript, Vite, TanStack Router/Query, Zustand, shadcn/ui, Tailwind CSS
- **인프라**: Docker, Docker Compose, Makefile

---

## Phase 1: 프로젝트 초기 설정

### 1.1 프로젝트 구조 설정
- [ ] 루트 디렉토리 구조 생성
  ```
  realworld-build-from-prd/
  ├── backend/         # Go 백엔드
  ├── frontend/        # React 프론트엔드
  ├── docker/          # Docker 설정
  ├── scripts/         # 유틸리티 스크립트
  ├── docs/            # 프로젝트 문서
  └── Makefile         # 빌드 및 개발 명령
  ```
- [ ] .gitignore 파일 설정
- [ ] README.md 작성
- [ ] 라이센스 파일 추가

### 1.2 개발 환경 구성
- [ ] Makefile 작성
  - [ ] `make dev` - 개발 서버 실행
  - [ ] `make test` - 테스트 실행
  - [ ] `make build` - 프로덕션 빌드
  - [ ] `make migrate` - DB 마이그레이션
  - [ ] `make docker-up` - Docker 컨테이너 시작
  - [ ] `make docker-down` - Docker 컨테이너 중지
- [ ] Docker 설정
  - [ ] backend/Dockerfile 작성 (멀티 스테이지 빌드)
  - [ ] frontend/Dockerfile 작성 (멀티 스테이지 빌드)
  - [ ] docker-compose.yml 작성
  - [ ] docker-compose.dev.yml 작성 (개발용)
- [ ] 환경 변수 설정
  - [ ] .env.example 파일 작성
  - [ ] .env.local 설정

---

## Phase 2: 백엔드 구현 (Go)

### 2.1 백엔드 프로젝트 초기화
- [ ] Go 모듈 초기화 (`go mod init`)
- [ ] 주요 의존성 설치
  - [ ] Echo 또는 Gin (웹 프레임워크)
  - [ ] database/sql + go-sqlite3 (데이터베이스)
  - [ ] golang-jwt/jwt (JWT 인증)
  - [ ] golang.org/x/crypto/bcrypt (비밀번호 해싱)
  - [ ] gosimple/slug (슬러그 생성)
  - [ ] go-playground/validator (유효성 검사)
  - [ ] golang-migrate/migrate (마이그레이션)
- [ ] 프로젝트 구조 생성
  ```
  backend/
  ├── cmd/
  │   └── server/
  │       └── main.go
  ├── internal/
  │   ├── api/
  │   │   ├── handlers/
  │   │   ├── middleware/
  │   │   └── routes.go
  │   ├── models/
  │   ├── repository/
  │   ├── service/
  │   └── utils/
  ├── migrations/
  ├── config/
  └── go.mod
  ```

### 2.2 데이터베이스 설계
- [ ] 데이터베이스 스키마 설계
  - [ ] users 테이블
  - [ ] articles 테이블
  - [ ] comments 테이블
  - [ ] tags 테이블
  - [ ] article_tags 테이블 (다대다)
  - [ ] user_follows 테이블
  - [ ] article_favorites 테이블
- [ ] 마이그레이션 파일 작성
  - [ ] 001_create_users_table.up.sql
  - [ ] 002_create_articles_table.up.sql
  - [ ] 003_create_comments_table.up.sql
  - [ ] 004_create_tags_table.up.sql
  - [ ] 005_create_relationships.up.sql
- [ ] 데이터베이스 연결 설정
- [ ] 마이그레이션 실행 스크립트

### 2.3 모델 정의
- [ ] User 모델
- [ ] Article 모델
- [ ] Comment 모델
- [ ] Tag 모델
- [ ] Profile 모델 (User의 공개 정보)

### 2.4 Repository 레이어 구현
- [ ] UserRepository
  - [ ] Create
  - [ ] GetByEmail
  - [ ] GetByUsername
  - [ ] Update
- [ ] ArticleRepository
  - [ ] Create
  - [ ] GetBySlug
  - [ ] Update
  - [ ] Delete
  - [ ] List (필터링, 페이지네이션)
  - [ ] Feed (팔로우한 사용자의 기사)
- [ ] CommentRepository
  - [ ] Create
  - [ ] GetByArticle
  - [ ] Delete
- [ ] TagRepository
  - [ ] GetAll
  - [ ] CreateIfNotExists
- [ ] FollowRepository
  - [ ] Follow
  - [ ] Unfollow
  - [ ] IsFollowing
- [ ] FavoriteRepository
  - [ ] Favorite
  - [ ] Unfavorite
  - [ ] IsFavorited

### 2.5 Service 레이어 구현
- [ ] AuthService
  - [ ] Register
  - [ ] Login
  - [ ] GenerateToken
  - [ ] ValidateToken
- [ ] UserService
  - [ ] GetCurrentUser
  - [ ] UpdateUser
  - [ ] GetProfile
  - [ ] FollowUser
  - [ ] UnfollowUser
- [ ] ArticleService
  - [ ] CreateArticle
  - [ ] GetArticle
  - [ ] UpdateArticle
  - [ ] DeleteArticle
  - [ ] ListArticles
  - [ ] GetFeed
  - [ ] FavoriteArticle
  - [ ] UnfavoriteArticle
- [ ] CommentService
  - [ ] AddComment
  - [ ] GetComments
  - [ ] DeleteComment
- [ ] TagService
  - [ ] GetTags

### 2.6 API 핸들러 구현
- [ ] 인증 엔드포인트
  - [ ] POST /api/users/login
  - [ ] POST /api/users
  - [ ] GET /api/user
  - [ ] PUT /api/user
- [ ] 프로필 엔드포인트
  - [ ] GET /api/profiles/:username
  - [ ] POST /api/profiles/:username/follow
  - [ ] DELETE /api/profiles/:username/follow
- [ ] 기사 엔드포인트
  - [ ] GET /api/articles
  - [ ] GET /api/articles/feed
  - [ ] GET /api/articles/:slug
  - [ ] POST /api/articles
  - [ ] PUT /api/articles/:slug
  - [ ] DELETE /api/articles/:slug
- [ ] 댓글 엔드포인트
  - [ ] POST /api/articles/:slug/comments
  - [ ] GET /api/articles/:slug/comments
  - [ ] DELETE /api/articles/:slug/comments/:id
- [ ] 좋아요 엔드포인트
  - [ ] POST /api/articles/:slug/favorite
  - [ ] DELETE /api/articles/:slug/favorite
- [ ] 태그 엔드포인트
  - [ ] GET /api/tags

### 2.7 미들웨어 구현
- [ ] JWT 인증 미들웨어
- [ ] CORS 미들웨어
- [ ] 로깅 미들웨어
- [ ] 에러 핸들링 미들웨어
- [ ] Rate Limiting 미들웨어 (선택)

### 2.8 유틸리티 함수
- [ ] JWT 토큰 생성/검증
- [ ] 비밀번호 해싱/검증
- [ ] 슬러그 생성
- [ ] 페이지네이션 헬퍼
- [ ] 에러 응답 포맷터

---

## Phase 3: 프론트엔드 구현 (React + TypeScript)

### 3.1 프론트엔드 프로젝트 초기화
- [ ] Vite + React + TypeScript 프로젝트 생성
- [ ] 주요 의존성 설치
  - [ ] @tanstack/react-router (라우팅)
  - [ ] @tanstack/react-query (서버 상태 관리)
  - [ ] zustand (클라이언트 상태 관리)
  - [ ] axios (HTTP 클라이언트)
  - [ ] react-hook-form (폼 관리)
  - [ ] @uiw/react-md-editor (마크다운 에디터)
  - [ ] date-fns (날짜 처리)
  - [ ] clsx, tailwind-merge (클래스 유틸리티)
- [ ] Tailwind CSS 설정
- [ ] shadcn/ui 설정
  - [ ] 컴포넌트 설치 (Button, Card, Form, Input, etc.)
- [ ] 프로젝트 구조 설정
  ```
  frontend/
  ├── src/
  │   ├── components/
  │   │   ├── ui/          # shadcn/ui 컴포넌트
  │   │   ├── layout/      # 레이아웃 컴포넌트
  │   │   └── features/    # 기능별 컴포넌트
  │   ├── pages/           # 페이지 컴포넌트
  │   ├── api/             # API 클라이언트
  │   ├── hooks/           # 커스텀 훅
  │   ├── stores/          # Zustand 스토어
  │   ├── types/           # TypeScript 타입
  │   ├── utils/           # 유틸리티 함수
  │   └── main.tsx
  ├── public/
  └── package.json
  ```

### 3.2 TypeScript 타입 정의
- [ ] User 타입
- [ ] Article 타입
- [ ] Comment 타입
- [ ] Profile 타입
- [ ] API 응답 타입
- [ ] 에러 타입

### 3.3 API 클라이언트 설정
- [ ] Axios 인스턴스 설정
  - [ ] 베이스 URL 설정
  - [ ] 인터셉터 설정 (토큰 자동 추가)
  - [ ] 에러 핸들링
- [ ] API 함수 구현
  - [ ] 인증 API
  - [ ] 사용자 API
  - [ ] 프로필 API
  - [ ] 기사 API
  - [ ] 댓글 API
  - [ ] 태그 API

### 3.4 상태 관리 설정
- [ ] 인증 스토어 (Zustand)
  - [ ] 사용자 정보
  - [ ] 토큰 관리
  - [ ] 로그인/로그아웃 액션
- [ ] TanStack Query 설정
  - [ ] QueryClient 설정
  - [ ] 커스텀 훅 작성

### 3.5 라우팅 설정
- [ ] TanStack Router 설정
- [ ] 라우트 정의
  - [ ] / - 홈 (글로벌 피드)
  - [ ] /login - 로그인
  - [ ] /register - 회원가입
  - [ ] /settings - 설정
  - [ ] /editor - 새 기사 작성
  - [ ] /editor/:slug - 기사 수정
  - [ ] /article/:slug - 기사 상세
  - [ ] /profile/:username - 프로필
  - [ ] /profile/:username/favorites - 좋아요한 기사
- [ ] 보호된 라우트 구현
- [ ] 404 페이지

### 3.6 레이아웃 컴포넌트
- [ ] Header
  - [ ] 로고
  - [ ] 네비게이션 메뉴
  - [ ] 사용자 메뉴 (로그인 상태)
  - [ ] 로그인/회원가입 링크 (비로그인 상태)
- [ ] Footer
- [ ] Layout 래퍼

### 3.7 페이지 구현

#### 3.7.1 인증 페이지
- [ ] 로그인 페이지
  - [ ] 이메일/비밀번호 폼
  - [ ] 유효성 검사
  - [ ] 에러 표시
  - [ ] 회원가입 링크
- [ ] 회원가입 페이지
  - [ ] 사용자명/이메일/비밀번호 폼
  - [ ] 유효성 검사
  - [ ] 에러 표시
  - [ ] 로그인 링크

#### 3.7.2 홈 페이지
- [ ] 피드 탭 (Your Feed / Global Feed)
- [ ] 태그 필터
- [ ] 기사 목록 컴포넌트
  - [ ] 기사 카드
  - [ ] 작성자 정보
  - [ ] 좋아요 버튼
  - [ ] 태그 표시
- [ ] 페이지네이션
- [ ] 인기 태그 사이드바

#### 3.7.3 기사 페이지
- [ ] 기사 상세 보기
  - [ ] 제목, 설명, 본문 (마크다운 렌더링)
  - [ ] 작성자 정보
  - [ ] 팔로우 버튼
  - [ ] 좋아요 버튼
  - [ ] 수정/삭제 버튼 (작성자만)
- [ ] 댓글 섹션
  - [ ] 댓글 목록
  - [ ] 댓글 작성 폼
  - [ ] 댓글 삭제 (작성자만)

#### 3.7.4 에디터 페이지
- [ ] 기사 작성/수정 폼
  - [ ] 제목 입력
  - [ ] 설명 입력
  - [ ] 본문 입력 (마크다운 에디터)
  - [ ] 태그 입력
- [ ] 미리보기 기능
- [ ] 게시/수정 버튼

#### 3.7.5 프로필 페이지
- [ ] 사용자 정보 표시
  - [ ] 프로필 이미지
  - [ ] 사용자명
  - [ ] 자기소개
- [ ] 팔로우/언팔로우 버튼
- [ ] 탭 (My Articles / Favorited Articles)
- [ ] 기사 목록

#### 3.7.6 설정 페이지
- [ ] 프로필 수정 폼
  - [ ] 프로필 이미지 URL
  - [ ] 사용자명
  - [ ] 자기소개
  - [ ] 이메일
  - [ ] 비밀번호 변경
- [ ] 로그아웃 버튼

### 3.8 공통 컴포넌트
- [ ] ArticleList
- [ ] ArticleCard
- [ ] ArticleMeta (작성자, 날짜, 좋아요)
- [ ] TagList
- [ ] Pagination
- [ ] LoadingSpinner
- [ ] ErrorMessage
- [ ] PrivateRoute

### 3.9 커스텀 훅
- [ ] useAuth - 인증 상태 관리
- [ ] useArticles - 기사 목록 조회
- [ ] useArticle - 기사 상세 조회
- [ ] useComments - 댓글 관리
- [ ] useProfile - 프로필 조회
- [ ] useTags - 태그 목록 조회

---

## Phase 4: 통합 및 테스트

### 4.1 백엔드 테스트
- [ ] 단위 테스트
  - [ ] Repository 테스트
  - [ ] Service 테스트
  - [ ] Handler 테스트
  - [ ] 유틸리티 함수 테스트
- [ ] 통합 테스트
  - [ ] API 엔드포인트 테스트
  - [ ] 인증 플로우 테스트
- [ ] 테스트 커버리지 80% 이상 달성

### 4.2 프론트엔드 테스트
- [ ] 컴포넌트 테스트 (React Testing Library)
  - [ ] 페이지 컴포넌트
  - [ ] 공통 컴포넌트
- [ ] 훅 테스트
- [ ] API 클라이언트 테스트

### 4.3 E2E 테스트 (Playwright)
- [ ] 사용자 인증 플로우
  - [ ] 회원가입
  - [ ] 로그인/로그아웃
- [ ] 기사 CRUD 플로우
  - [ ] 기사 작성
  - [ ] 기사 수정
  - [ ] 기사 삭제
- [ ] 소셜 기능 플로우
  - [ ] 팔로우/언팔로우
  - [ ] 좋아요
  - [ ] 댓글 작성/삭제

### 4.4 성능 테스트
- [ ] API 응답 시간 측정
- [ ] 페이지 로드 시간 측정
- [ ] 부하 테스트

---

## Phase 5: 최적화 및 개선

### 5.1 성능 최적화
- [ ] 백엔드 최적화
  - [ ] 데이터베이스 쿼리 최적화
  - [ ] 인덱스 추가
  - [ ] N+1 쿼리 문제 해결
  - [ ] 캐싱 구현 (선택)
- [ ] 프론트엔드 최적화
  - [ ] 코드 스플리팅
  - [ ] 이미지 최적화
  - [ ] 번들 크기 최적화
  - [ ] React.memo 적용
  - [ ] useMemo/useCallback 최적화

### 5.2 보안 강화
- [ ] SQL 인젝션 방지 확인
- [ ] XSS 공격 방지
- [ ] CSRF 보호
- [ ] Rate Limiting 구현
- [ ] 입력 유효성 검사 강화
- [ ] 보안 헤더 설정

### 5.3 사용자 경험 개선
- [ ] 반응형 디자인 개선
- [ ] 로딩 상태 개선
- [ ] 에러 처리 개선
- [ ] 폼 유효성 검사 UX
- [ ] 접근성 개선 (ARIA 레이블 등)

### 5.4 코드 품질
- [ ] 린팅 규칙 설정 및 적용
- [ ] 포맷팅 규칙 적용
- [ ] 코드 리뷰 체크리스트 작성
- [ ] 기술 부채 정리

---

## Phase 6: 배포 준비

### 6.1 문서화
- [ ] API 문서 작성
- [ ] 설치 가이드 작성
- [ ] 개발자 문서 작성
- [ ] 아키텍처 문서 작성

### 6.2 CI/CD 설정
- [ ] GitHub Actions 워크플로우 작성
  - [ ] 테스트 자동화
  - [ ] 빌드 자동화
  - [ ] 린팅 체크
- [ ] 환경별 설정
  - [ ] 개발 환경
  - [ ] 스테이징 환경
  - [ ] 프로덕션 환경

### 6.3 Docker 이미지 최적화
- [ ] 멀티 스테이지 빌드 최적화
- [ ] 이미지 크기 최소화
- [ ] 보안 스캔
- [ ] Docker Compose 프로덕션 설정

### 6.4 모니터링 및 로깅
- [ ] 로깅 시스템 구현
- [ ] 에러 추적 설정
- [ ] 성능 모니터링 (선택)
- [ ] 헬스 체크 엔드포인트

### 6.5 최종 검증
- [ ] 모든 기능 테스트
- [ ] 성능 목표 달성 확인
- [ ] 보안 체크리스트 확인
- [ ] RealWorld 사양 준수 확인

---

## 완료 기준

### 기능적 요구사항
- [ ] 모든 RealWorld API 엔드포인트 구현
- [ ] 모든 프론트엔드 페이지 및 기능 구현
- [ ] JWT 기반 인증 시스템 완성
- [ ] 실시간 업데이트 (좋아요 수, 팔로우 상태 등)

### 비기능적 요구사항
- [ ] 페이지 로드 시간 3초 이내
- [ ] API 응답 시간 500ms 이내
- [ ] 테스트 커버리지 80% 이상
- [ ] 반응형 디자인 (모바일, 태블릿, 데스크탑)
- [ ] 크로스 브라우저 호환성

### 기술적 요구사항
- [ ] Go 백엔드 + SQLite
- [ ] React + TypeScript 프론트엔드
- [ ] Docker 컨테이너화
- [ ] Makefile을 통한 빌드 자동화
- [ ] 깨끗하고 유지보수 가능한 코드

---

## 참고 자료
- [RealWorld 공식 문서](https://realworld-docs.netlify.app/)
- [RealWorld GitHub](https://github.com/gothinkster/realworld)
- [API 사양](https://realworld-docs.netlify.app/specifications/backend/endpoints/)
- [프론트엔드 사양](https://realworld-docs.netlify.app/specifications/frontend/)
- [Agentic Coding](https://lucumr.pocoo.org/2025/6/12/agentic-coding/)