# RealWorld (Conduit) 제품 요구사항 명세서 (PRD)

## 1. 제품 개요

### 1.1 제품명
**Conduit** - 소셜 블로깅 플랫폼

### 1.2 제품 설명
Conduit는 Medium.com 클론으로, 사용자가 기사를 작성, 읽기, 팔로우, 좋아요 기능을 제공하는 완전한 기능을 갖춘 소셜 블로깅 플랫폼입니다.

### 1.3 목표
- 실제 프로덕션 레벨의 풀스택 애플리케이션 구현
- 다양한 프론트엔드/백엔드 기술 스택 간의 상호 운용성 보장
- 개발자들이 실제 애플리케이션 구축에 필요한 지식과 관점 제공

### 1.4 핵심 원칙
- 단순한 "Todo" 데모를 넘어선 복잡한 애플리케이션 개발
- 일관된 Bootstrap 4 테마를 통한 통일된 UI/UX
- 공통 API 사양 준수를 통한 기술 독립성

## 2. 사용자 스토리 및 기능 요구사항

### 2.1 인증 및 사용자 관리

#### 2.1.1 회원가입
- **As a** 방문자
- **I want to** 새 계정을 만들 수 있다
- **So that** 플랫폼의 모든 기능을 사용할 수 있다

**수락 조건:**
- 이메일, 사용자명, 비밀번호 입력 필수
- 중복 이메일/사용자명 검증
- 성공 시 자동 로그인 및 JWT 토큰 발급

#### 2.1.2 로그인
- **As a** 등록된 사용자
- **I want to** 내 계정에 로그인할 수 있다
- **So that** 개인화된 기능을 사용할 수 있다

**수락 조건:**
- 이메일과 비밀번호로 로그인
- JWT 토큰 발급 및 로컬 스토리지 저장
- 기억하기 기능 제공

#### 2.1.3 프로필 관리
- **As a** 로그인한 사용자
- **I want to** 내 프로필을 수정할 수 있다
- **So that** 내 정보를 최신 상태로 유지할 수 있다

**수락 조건:**
- 프로필 이미지, 자기소개, 이메일, 사용자명 수정 가능
- 비밀번호 변경 기능

### 2.2 기사(Article) 관리

#### 2.2.1 기사 작성
- **As a** 로그인한 사용자
- **I want to** 새 기사를 작성할 수 있다
- **So that** 내 생각을 공유할 수 있다

**수락 조건:**
- 제목, 설명, 본문, 태그 입력
- 마크다운 지원
- 작성 즉시 게시

#### 2.2.2 기사 읽기
- **As a** 모든 사용자
- **I want to** 기사를 읽을 수 있다
- **So that** 다른 사람의 콘텐츠를 소비할 수 있다

**수락 조건:**
- 로그인 없이도 기사 읽기 가능
- 작성자 정보 표시
- 작성/수정 날짜 표시

#### 2.2.3 기사 수정/삭제
- **As a** 기사 작성자
- **I want to** 내 기사를 수정하거나 삭제할 수 있다
- **So that** 내 콘텐츠를 관리할 수 있다

**수락 조건:**
- 본인 기사만 수정/삭제 가능
- 수정 시 수정 날짜 업데이트

### 2.3 소셜 기능

#### 2.3.1 기사 좋아요
- **As a** 로그인한 사용자
- **I want to** 기사에 좋아요를 표시할 수 있다
- **So that** 좋은 콘텐츠에 대한 지지를 표현할 수 있다

**수락 조건:**
- 하트 아이콘 토글
- 좋아요 수 실시간 업데이트
- 좋아요한 기사 목록 확인 가능

#### 2.3.2 사용자 팔로우
- **As a** 로그인한 사용자
- **I want to** 다른 사용자를 팔로우할 수 있다
- **So that** 그들의 새 기사를 받아볼 수 있다

**수락 조건:**
- 팔로우/언팔로우 토글
- 팔로우한 사용자의 기사 피드 제공

#### 2.3.3 댓글
- **As a** 로그인한 사용자
- **I want to** 기사에 댓글을 달 수 있다
- **So that** 작성자 및 다른 독자와 소통할 수 있다

**수락 조건:**
- 댓글 작성, 삭제 (본인 댓글만)
- 댓글 작성 시간 표시
- 작성자 정보 표시

### 2.4 콘텐츠 탐색

#### 2.4.1 글로벌 피드
- **As a** 모든 사용자
- **I want to** 최신 기사들을 볼 수 있다
- **So that** 새로운 콘텐츠를 발견할 수 있다

**수락 조건:**
- 모든 공개 기사 표시
- 최신순 정렬
- 페이지네이션 (10개씩)

#### 2.4.2 개인 피드
- **As a** 로그인한 사용자
- **I want to** 팔로우한 사용자의 기사를 볼 수 있다
- **So that** 관심 있는 콘텐츠만 볼 수 있다

**수락 조건:**
- 팔로우한 사용자의 기사만 표시
- 최신순 정렬
- 페이지네이션

#### 2.4.3 태그별 필터링
- **As a** 모든 사용자
- **I want to** 태그로 기사를 필터링할 수 있다
- **So that** 특정 주제의 기사를 찾을 수 있다

**수락 조건:**
- 인기 태그 목록 표시
- 태그 클릭 시 필터링
- 다중 태그 선택 가능

## 3. 기술 스택 (Agentic Coding 최적화)

### 3.1 선정 기준
Armin Ronacher의 "Agentic Coding" 권장사항에 기반하여 AI 어시스턴트와의 협업에 최적화된 기술 스택을 선정했습니다:
- **단순성과 명확성**: AI가 이해하고 수정하기 쉬운 코드
- **명시적 동작**: 마법같은 동작이나 숨겨진 부작용 최소화
- **빠른 피드백 루프**: 빠른 빌드와 테스트 실행
- **낮은 생태계 변동성**: 안정적이고 예측 가능한 도구

### 3.2 백엔드 기술 스택

#### 3.2.1 핵심 기술
- **언어**: Go
  - 명시적 컨텍스트 시스템
  - 간단한 테스트 캐싱
  - 구조적 인터페이스
  - 낮은 생태계 변동성
  - AI 에이전트에 유리한 단순성

#### 3.2.2 프레임워크 및 라이브러리
- **웹 프레임워크**: Echo 또는 Gin (경량, 명시적)
- **데이터베이스**: SQLite + database/sql (직접적인 SQL 사용)
- **인증**: golang-jwt/jwt
- **비밀번호 해싱**: golang.org/x/crypto/bcrypt
- **슬러그 생성**: gosimple/slug
- **유효성 검사**: go-playground/validator

#### 3.2.3 데이터베이스 접근
- **Plain SQL 사용** (ORM 대신)
- **SQLite 드라이버**: github.com/mattn/go-sqlite3
- **마이그레이션**: golang-migrate/migrate (SQLite 지원)
- **쿼리 빌더**: 필요시 squirrel (선택적)
- **개발/테스트 편의성**: 단일 파일 DB, 별도 서버 불필요

### 3.3 프론트엔드 기술 스택

#### 3.3.1 핵심 기술
- **프레임워크**: React 18
- **빌드 도구**: Vite (빠른 HMR, 간단한 설정)
- **언어**: TypeScript (타입 안정성)

#### 3.3.2 스타일링
- **UI 컴포넌트**: shadcn/ui
  - 복사 가능한 컴포넌트 (의존성 최소화)
  - Radix UI 기반 접근성
  - 완전한 커스터마이징 가능
- **CSS 프레임워크**: Tailwind CSS
  - 유틸리티 우선 접근
  - AI가 이해하기 쉬운 명시적 스타일
  - shadcn/ui와 완벽한 통합

#### 3.3.3 상태 관리 및 데이터 페칭
- **라우팅**: TanStack Router
- **서버 상태**: TanStack Query
- **클라이언트 상태**: Zustand (간단하고 명시적)
- **폼 관리**: React Hook Form

#### 3.3.4 추가 라이브러리
- **마크다운 에디터**: @uiw/react-md-editor
- **날짜 처리**: date-fns
- **HTTP 클라이언트**: Axios
- **클래스 유틸리티**: clsx, tailwind-merge
- **아이콘**: lucide-react

### 3.4 개발 도구 및 프로세스

#### 3.4.1 빌드 및 태스크 관리
- **Makefile**: 모든 빌드 및 개발 명령 중앙화
  ```makefile
  # 예시 명령어
  make dev        # 개발 서버 실행
  make test       # 테스트 실행
  make build      # 프로덕션 빌드
  make migrate    # DB 마이그레이션
  make docker-up  # Docker 컨테이너 시작
  make docker-down # Docker 컨테이너 중지
  ```

#### 3.4.2 테스팅
- **백엔드**: Go 내장 testing 패키지
- **프론트엔드**: Vitest + React Testing Library
- **E2E**: Playwright

#### 3.4.3 코드 품질
- **백엔드**: 
  - golangci-lint
  - go fmt
  - go vet
- **프론트엔드**:
  - ESLint
  - Prettier
  - TypeScript strict mode

### 3.5 인프라 및 배포

#### 3.5.1 컨테이너화
- **Docker**: 개발 및 프로덕션 환경 일관성
- **Docker Compose**: 통합 개발 환경
  - 백엔드 컨테이너 (Go + SQLite)
  - 프론트엔드 컨테이너 (Node.js + Vite)
  - 볼륨 마운트로 핫 리로드 지원
- **멀티 스테이지 빌드**: 최적화된 프로덕션 이미지

#### 3.5.2 배포
- **백엔드**: Docker 컨테이너 (Go 바이너리 + SQLite)
- **프론트엔드**: Docker 컨테이너 (Nginx + 정적 파일)
- **데이터베이스**: SQLite 파일 (볼륨 마운트)
- **오케스트레이션**: Docker Compose (개발) / Kubernetes (프로덕션 옵션)

### 3.6 개발 원칙

#### 3.6.1 코드 작성 원칙
- **함수 우선**: 복잡한 클래스보다 단순한 함수 선호
- **명시적 에러 처리**: Go의 에러 반환 패턴 활용
- **로컬 권한 검사**: 권한 체크를 명시적이고 가시적으로
- **병렬화 고려**: 동시성을 염두에 둔 설계
- **최소 의존성**: 필요한 것만 추가

#### 3.6.2 AI 협업 최적화
- **명확한 로깅**: 디버깅과 관찰 용이
- **빠른 피드백**: 빠른 빌드와 테스트
- **간단한 도구**: 복잡한 추상화 피하기
- **문서화된 결정**: 기술 선택 이유 명시

## 4. 기술 요구사항

### 4.1 프론트엔드 요구사항

#### 4.1.1 라우팅
| 경로 | 페이지 | 인증 필요 |
|------|--------|-----------|
| `/` | 홈 (글로벌 피드) | 아니오 |
| `/login` | 로그인 | 아니오 |
| `/register` | 회원가입 | 아니오 |
| `/settings` | 설정 | 예 |
| `/editor` | 새 기사 작성 | 예 |
| `/editor/:slug` | 기사 수정 | 예 |
| `/article/:slug` | 기사 상세 | 아니오 |
| `/profile/:username` | 프로필 | 아니오 |
| `/profile/:username/favorites` | 좋아요한 기사 | 아니오 |

#### 4.1.2 UI 컴포넌트
- **헤더**: 로고, 네비게이션 메뉴, 사용자 정보
- **기사 카드**: 제목, 설명, 작성자, 날짜, 태그, 좋아요 수
- **기사 상세**: 전체 내용, 작성자 정보, 댓글 섹션
- **프로필 페이지**: 사용자 정보, 기사 목록, 팔로우 버튼
- **태그 목록**: 인기 태그 표시
- **페이지네이션**: 이전/다음 버튼

#### 4.1.3 상태 관리
- 사용자 인증 상태
- 현재 사용자 정보
- 기사 목록 및 상세 정보
- 댓글 목록
- 태그 목록
- 로딩 및 에러 상태

### 4.2 백엔드 API 사양

#### 4.2.1 인증
- **헤더 형식**: `Authorization: Token jwt.token.here`
- **JWT 토큰 구조**: 사용자 ID, 이메일, 사용자명, 만료 시간

#### 4.2.2 API 엔드포인트

##### 인증 엔드포인트
```
POST   /api/users/login       - 로그인
POST   /api/users             - 회원가입
GET    /api/user              - 현재 사용자 정보
PUT    /api/user              - 사용자 정보 수정
```

##### 프로필 엔드포인트
```
GET    /api/profiles/:username           - 프로필 조회
POST   /api/profiles/:username/follow    - 팔로우
DELETE /api/profiles/:username/follow    - 언팔로우
```

##### 기사 엔드포인트
```
GET    /api/articles                     - 기사 목록
GET    /api/articles/feed                - 피드 기사
GET    /api/articles/:slug               - 기사 상세
POST   /api/articles                     - 기사 작성
PUT    /api/articles/:slug               - 기사 수정
DELETE /api/articles/:slug               - 기사 삭제
```

##### 댓글 엔드포인트
```
POST   /api/articles/:slug/comments      - 댓글 작성
GET    /api/articles/:slug/comments      - 댓글 목록
DELETE /api/articles/:slug/comments/:id  - 댓글 삭제
```

##### 좋아요 엔드포인트
```
POST   /api/articles/:slug/favorite      - 좋아요
DELETE /api/articles/:slug/favorite      - 좋아요 취소
```

##### 태그 엔드포인트
```
GET    /api/tags                         - 태그 목록
```

#### 4.2.3 응답 형식
- **Content-Type**: `application/json; charset=utf-8`
- **성공 응답**: 해당 데이터 반환
- **에러 응답**: 
```json
{
  "errors": {
    "field": ["error message"]
  }
}
```

### 4.3 데이터 모델

#### 4.3.1 User
```json
{
  "id": "integer",
  "email": "string",
  "username": "string",
  "password": "string (hashed)",
  "bio": "text",
  "image": "string (URL)",
  "createdAt": "timestamp",
  "updatedAt": "timestamp"
}
```

#### 4.3.2 Article
```json
{
  "id": "integer",
  "slug": "string",
  "title": "string",
  "description": "string",
  "body": "text",
  "authorId": "integer",
  "createdAt": "timestamp",
  "updatedAt": "timestamp"
}
```

#### 4.3.3 Comment
```json
{
  "id": "integer",
  "body": "text",
  "articleId": "integer",
  "authorId": "integer",
  "createdAt": "timestamp",
  "updatedAt": "timestamp"
}
```

#### 4.3.4 Tag
```json
{
  "id": "integer",
  "name": "string"
}
```

#### 4.3.5 관계 테이블
- **ArticleTags**: 기사-태그 다대다 관계
- **UserFollows**: 사용자 팔로우 관계
- **ArticleFavorites**: 기사 좋아요 관계

## 5. 비기능 요구사항

### 5.1 성능
- 페이지 로드 시간: 3초 이내
- API 응답 시간: 500ms 이내
- 동시 사용자 지원: 1000명 이상

### 5.2 보안
- 비밀번호 해싱 (bcrypt)
- JWT 토큰 기반 인증
- CORS 설정
- SQL 인젝션 방지
- XSS 공격 방지

### 5.3 사용성
- 반응형 디자인 (모바일, 태블릿, 데스크탑)
- 직관적인 UI/UX
- 에러 메시지 명확성
- 로딩 상태 표시

### 5.4 호환성
- 모던 브라우저 지원 (Chrome, Firefox, Safari, Edge)
- RESTful API 준수
- 프론트엔드/백엔드 독립성

## 6. 개발 단계

### Phase 1: 기본 설정 (1주)
- 프로젝트 구조 설정
- 개발 환경 구성
- 데이터베이스 스키마 설계
- 기본 라우팅 설정

### Phase 2: 인증 시스템 (1주)
- 회원가입/로그인 구현
- JWT 토큰 관리
- 사용자 프로필 관리
- 인증 미들웨어

### Phase 3: 기사 CRUD (2주)
- 기사 작성/읽기/수정/삭제
- 마크다운 에디터 통합
- 슬러그 생성
- 태그 시스템

### Phase 4: 소셜 기능 (1주)
- 팔로우/언팔로우
- 좋아요 기능
- 댓글 시스템
- 피드 구현

### Phase 5: UI/UX 개선 (1주)
- 반응형 디자인
- 로딩/에러 상태
- 페이지네이션
- 검색 및 필터링

### Phase 6: 테스트 및 배포 (1주)
- 단위 테스트
- 통합 테스트
- 성능 최적화
- 배포 준비

## 7. 성공 지표

### 7.1 기능적 완성도
- 모든 핵심 기능 구현 완료
- API 사양 100% 준수
- 크로스 브라우저 호환성

### 7.2 품질 지표
- 코드 커버리지 80% 이상
- 페이지 로드 속도 목표 달성
- 0 치명적 버그

### 7.3 사용자 경험
- 직관적인 네비게이션
- 일관된 UI 패턴
- 명확한 피드백 메시지

## 8. 리스크 및 제약사항

### 8.1 기술적 리스크
- 확장성 문제
- 성능 병목 현상
- 보안 취약점

### 8.2 제약사항
- Tailwind CSS로 Bootstrap 4 디자인 재구현
- RealWorld API 사양 준수
- 모바일 우선 디자인
- Go 백엔드 + React/TypeScript 프론트엔드 필수

## 9. 참고 자료

- [RealWorld 공식 문서](https://realworld-docs.netlify.app/)
- [GitHub 저장소](https://github.com/gothinkster/realworld)
- [API 사양 문서](https://realworld-docs.netlify.app/specifications/backend/endpoints/)
- [프론트엔드 사양](https://realworld-docs.netlify.app/specifications/frontend/)
- [데모 사이트](https://demo.realworld.io/)
- [Agentic Coding 아티클](https://lucumr.pocoo.org/2025/6/12/agentic-coding/)

## 10. 부록

### 10.1 용어 정의
- **Slug**: URL 친화적인 기사 식별자
- **Feed**: 팔로우한 사용자의 기사 목록
- **JWT**: JSON Web Token, 인증 토큰
- **CRUD**: Create, Read, Update, Delete

### 10.2 API 응답 예시

#### 사용자 응답
```json
{
  "user": {
    "email": "jake@jake.jake",
    "token": "jwt.token.here",
    "username": "jake",
    "bio": "I work at statefarm",
    "image": "https://i.stack.imgur.com/xHWG8.jpg"
  }
}
```

#### 기사 응답
```json
{
  "article": {
    "slug": "how-to-train-your-dragon",
    "title": "How to train your dragon",
    "description": "Ever wonder how?",
    "body": "It takes a Jacobian",
    "tagList": ["dragons", "training"],
    "createdAt": "2016-02-18T03:22:56.637Z",
    "updatedAt": "2016-02-18T03:48:35.824Z",
    "favorited": false,
    "favoritesCount": 0,
    "author": {
      "username": "jake",
      "bio": "I work at statefarm",
      "image": "https://i.stack.imgur.com/xHWG8.jpg",
      "following": false
    }
  }
}
```

### 10.3 에러 코드
- 401: 인증 필요
- 403: 권한 없음
- 404: 리소스 없음
- 422: 유효성 검사 실패
- 500: 서버 에러