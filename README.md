# GitHub CLI Skill

## 개요
GitHub CLI (`gh`) 명령어를 사용하여 GitHub 저장소와 상호작용할 수 있도록 도와주는 Claude Code 스킬입니다.

## 설치
전역 스킬로 설치됨: `~/.claude/skills/github-cli/`

## 주요 기능

### 1. Pull Request 관리
- PR 목록 조회, 상세 정보 확인
- 새 PR 생성 (자동으로 커밋 히스토리 분석하여 설명 생성)
- PR 리뷰 (승인, 변경 요청, 코멘트)
- PR 병합, 닫기, 재오픈
- CI/CD 체크 상태 확인

### 2. Issue 관리
- 이슈 목록 조회, 검색
- 새 이슈 생성
- 이슈 상태 업데이트 (열기, 닫기)
- 라벨, 담당자, 마일스톤 관리
- 이슈에 코멘트 달기

### 3. GitHub Actions
- 워크플로우 실행 상태 확인
- 워크플로우 수동 실행
- 작업 로그 및 아티팩트 조회
- 워크플로우 취소 또는 재실행

### 4. Repository 작업
- 저장소 복제, 포크, 생성
- 저장소 정보 조회
- 저장소 설정 관리

### 5. Release 관리
- 릴리즈 목록 조회
- 새 릴리즈 생성 (릴리즈 노트 포함)
- 릴리즈 자산 업로드 및 다운로드

### 6. Gist 관리
- Gist 생성, 조회, 수정, 삭제
- Gist 로컬 복제

## 사용 방법

### 자동 실행
다음 키워드를 언급하면 Claude가 자동으로 이 스킬을 사용합니다:

**한국어:**
- "풀 리퀘스트", "풀리퀘", "PR"
- "깃허브 이슈", "이슈"
- "깃허브 액션", "워크플로우"
- "릴리즈", "배포"
- "저장소", "레포"
- "코드 리뷰"

**영어:**
- "pull request", "PR", "merge request"
- "github issue", "issue"
- "github actions", "workflow", "CI/CD"
- "release"
- "repository", "repo"
- "code review"
- "gist"

### 사용 예시

#### PR 생성
```
사용자: "인증 기능 추가한 PR 만들어줘"
Claude: [현재 브랜치 확인 → 커밋 분석 → PR 생성 → URL 반환]
```

#### PR 상태 확인
```
사용자: "PR #123 상태 확인해줘"
Claude: [PR 상세 정보, 리뷰 상태, CI 체크 상태 표시]
```

#### Issue 생성
```
사용자: "로그인 버그 이슈 생성해줘"
Claude: [필요시 추가 정보 질문 → 이슈 생성 → URL 반환]
```

#### CI 상태 확인
```
사용자: "CI 통과했는지 확인해줘"
Claude: [현재 PR 또는 최근 워크플로우 실행 상태 표시]
```

#### 릴리즈 생성
```
사용자: "v1.2.0 릴리즈 만들어줘"
Claude: [커밋 히스토리 분석 → 릴리즈 노트 생성 → 릴리즈 생성]
```

## 주요 명령어

### Pull Requests
```bash
gh pr list                    # PR 목록
gh pr view <번호>             # PR 상세 정보
gh pr create                  # 새 PR 생성
gh pr checkout <번호>         # PR 로컬 체크아웃
gh pr review --approve        # PR 승인
gh pr merge                   # PR 병합
gh pr checks                  # CI 상태 확인
```

### Issues
```bash
gh issue list                 # 이슈 목록
gh issue view <번호>          # 이슈 상세 정보
gh issue create               # 새 이슈 생성
gh issue close <번호>         # 이슈 닫기
gh issue comment <번호>       # 이슈에 코멘트
```

### Workflows
```bash
gh workflow list              # 워크플로우 목록
gh run list                   # 워크플로우 실행 목록
gh run view <실행-ID>         # 실행 상세 정보
gh run watch <실행-ID>        # 실행 상태 실시간 모니터링
```

### Repositories
```bash
gh repo view                  # 저장소 정보
gh repo clone <저장소>        # 저장소 복제
gh repo create                # 새 저장소 생성
gh repo fork                  # 저장소 포크
```

### Releases
```bash
gh release list               # 릴리즈 목록
gh release create <태그>      # 새 릴리즈 생성
gh release view <태그>        # 릴리즈 상세 정보
```

## 인증 설정

GitHub CLI를 처음 사용하는 경우:
```bash
gh auth login
```

인증 상태 확인:
```bash
gh auth status
```

## 출력 형식

### 목록 형태
```
#123  feat: 로그인 추가       user1  ✓ 2명 승인
#122  fix: 버튼 스타일        user2  ⏳ 대기 중
#121  docs: README 업데이트   user3  ✗ 변경 요청됨
```

### 상세 정보
```
## PR #123: 인증 기능 추가

**상태**: Open (병합 가능)
**작성자**: @username
**생성**: 2일 전
**Base**: main ← **Head**: feature/auth

### 체크
✓ 테스트 (통과)
✓ 린트 (통과)
✓ 빌드 (통과)

### 리뷰
✓ @reviewer1 승인
✓ @reviewer2 승인
```

## 파일 구조
```
github-cli/
├── SKILL.md    # 메인 스킬 정의
└── README.md   # 이 파일
```

## 특징

### 1. 컨텍스트 인지
- 현재 저장소, 브랜치 자동 감지
- 관련된 작업을 자동으로 그룹화
- 다음 단계 제안

### 2. 스마트한 PR 생성
- 커밋 히스토리를 분석하여 PR 설명 자동 생성
- 변경사항 요약 제공
- 체크리스트 및 테스트 계획 포함

### 3. 통합된 워크플로우
- Git 작업과 GitHub CLI 작업 조합
- 로컬 변경사항 → 커밋 → 푸시 → PR 생성까지 원스톱

### 4. 다국어 지원
- 한국어/영어 모두 지원
- 사용자 언어에 맞춰 응답
- 명령어는 표준 `gh` 문법 사용

## 보안 주의사항
- 토큰이나 인증 정보를 노출하지 않음
- 파괴적인 작업 전 경고 및 확인
- 공개 저장소 생성 전 확인

## 문제 해결

### 인증되지 않음
```bash
gh auth login
```

### 저장소를 찾을 수 없음
- Git 저장소 내에 있는지 확인
- 또는 `-R owner/repo` 플래그 사용

### 권한 거부됨
- 저장소 접근 권한 확인
- 토큰 스코프 확인

### 명령어를 찾을 수 없음
- GitHub CLI 설치 확인: `brew install gh` (macOS)

## 더 알아보기
- GitHub CLI 공식 문서: https://cli.github.com/manual/
- `gh <명령어> --help`로 명령어별 도움말 확인
- `gh manual`로 전체 매뉴얼 확인

## 커스터마이징
`SKILL.md` 파일을 수정하여 동작을 커스터마이즈할 수 있습니다.

## 테스트
스킬을 테스트하려면:
```
"현재 저장소의 PR 목록 보여줘"
"main 브랜치로 PR 만들어줘"
"최근 워크플로우 실행 상태 확인해줘"
```

Claude가 자동으로 이 스킬을 실행하여 GitHub CLI 명령어를 사용합니다.
