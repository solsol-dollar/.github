# Contributing Guide

이 문서는 팀 프로젝트의 Git 협업 규칙을 정의합니다.
모든 팀원은 아래의 브랜치 전략, 브랜치 네이밍, 커밋 메시지, Issue, Pull Request 규칙을 기준으로 작업합니다.

---

## 1. Git Flow

우리 팀은 **간소화된 Git Flow**를 사용합니다.

### 브랜치 구조

```text
main
└── develop
    ├── feature/#이슈번호-작업내용
    ├── fix/#이슈번호-작업내용
    ├── refactor/#이슈번호-작업내용
    ├── docs/#이슈번호-작업내용
    ├── test/#이슈번호-작업내용
    └── chore/#이슈번호-작업내용
```

### 브랜치 역할

| 브랜치          | 설명                      |
| ------------ | ----------------------- |
| `main`       | 배포 가능한 최종 브랜치           |
| `develop`    | 개발 통합 브랜치               |
| `feature/*`  | 새로운 기능 개발 브랜치           |
| `fix/*`      | 버그 수정 브랜치               |
| `refactor/*` | 코드 구조 개선 브랜치            |
| `docs/*`     | 문서 작업 브랜치               |
| `test/*`     | 테스트 코드 작업 브랜치           |
| `chore/*`    | 설정, 빌드, 패키지 등 기타 작업 브랜치 |
| `hotfix/*`   | main 배포 후 긴급 수정 브랜치     |

---

## 2. Branch Naming Convention

브랜치는 아래 형식을 따릅니다.

```text
타입/#이슈번호-작업내용
```

### 브랜치 타입

| 타입         | 사용 상황               |
| ---------- | ------------------- |
| `feature`  | 새로운 기능 개발           |
| `fix`      | 버그 수정               |
| `refactor` | 코드 구조 개선            |
| `docs`     | 문서 작성 및 수정          |
| `test`     | 테스트 코드 작성 및 수정      |
| `chore`    | 설정, 빌드, 패키지 등 기타 작업 |
| `hotfix`   | 운영 브랜치 긴급 수정        |

### 브랜치명 작성 규칙

* 브랜치명에는 반드시 Issue 번호를 포함합니다.
* 작업 내용은 소문자 영어와 하이픈(`-`)을 사용합니다.
* 공백은 사용하지 않습니다.
* 브랜치 타입은 작업 성격에 맞게 작성합니다.

### 예시

```text
feature/#12-login-api
feature/#23-user-profile
fix/#31-token-refresh-error
refactor/#42-user-service
docs/#50-update-readme
test/#55-login-service-test
chore/#61-add-github-template
hotfix/#72-production-login-error
```

### 브랜치 생성 기준

기능 개발 및 수정 작업은 반드시 `develop` 브랜치에서 분기합니다.

```bash
git checkout develop
git pull origin develop
git checkout -b feature/#12-login-api
```

작업 완료 후에는 `develop` 브랜치로 Pull Request를 생성합니다.

```text
feature/#12-login-api → develop
```

단, 운영 중 긴급 수정이 필요한 경우에는 `main` 브랜치에서 `hotfix/*` 브랜치를 생성할 수 있습니다.

```text
main → hotfix/#72-production-login-error → main
```

---

## 3. Commit Message Convention

커밋 메시지는 **Conventional Commit** 형식을 따릅니다.

```text
type: subject
```

### Commit Type

| 타입         | 설명                        |
| ---------- | ------------------------- |
| `feat`     | 새로운 기능 추가                 |
| `fix`      | 버그 수정                     |
| `refactor` | 기능 변경 없는 코드 구조 개선         |
| `docs`     | 문서 작성 및 수정                |
| `style`    | 코드 포맷팅, 세미콜론, 공백 등 스타일 수정 |
| `test`     | 테스트 코드 추가 및 수정            |
| `chore`    | 빌드, 설정, 패키지 등 기타 작업       |
| `perf`     | 성능 개선                     |
| `ci`       | CI/CD 설정 변경               |

### 예시

```text
feat: 로그인 API 구현
fix: 토큰 재발급 오류 수정
refactor: UserService 책임 분리
docs: README 실행 방법 추가
test: 회원가입 서비스 테스트 추가
chore: Gradle 의존성 추가
ci: GitHub Actions 워크플로우 추가
```

### 커밋 메시지 작성 규칙

* 커밋 메시지는 한글 또는 영어로 작성할 수 있습니다.
* 제목은 변경 내용을 명확하게 설명합니다.
* 하나의 커밋에는 하나의 목적만 포함합니다.
* 의미 없는 커밋 메시지는 지양합니다.

#### 지양하는 예시

```text
fix: 수정
feat: 작업
chore: 이것저것 수정
```

#### 권장하는 예시

```text
fix: 로그인 실패 시 예외 응답 형식 수정
feat: 사용자 프로필 조회 API 구현
chore: application.yml 환경변수 설정 추가
```

---

## 4. Issue Convention

작업은 가능하면 Issue를 먼저 생성한 뒤 진행합니다.

### Issue 제목 규칙

Issue 제목은 아래 형식을 따릅니다.

```text
[type] 작업 내용
```

### Issue 제목 예시

```text
[feat] 로그인 API 구현
[fix] 토큰 재발급 오류 수정
[chore] GitHub Actions 설정 추가
[docs] README 실행 방법 정리
[refactor] UserService 책임 분리
```

### Issue Template

우리 팀은 아래 Issue Template을 사용합니다.

```text
.github/ISSUE_TEMPLATE/
├── feature_request.md
├── bug_report.md
└── chore.md
```

### Issue Type 기준

| Issue Type | 사용 상황               | 예시                             |
| ---------- | ------------------- | ------------------------------ |
| `feat`     | 새로운 기능 구현           | `[feat] 로그인 API 구현`            |
| `fix`      | 버그 수정               | `[fix] 토큰 재발급 오류 수정`           |
| `chore`    | 설정, 빌드, 패키지 등 기타 작업 | `[chore] Gradle 의존성 추가`        |
| `docs`     | 문서 작성 및 수정          | `[docs] README 실행 방법 추가`       |
| `refactor` | 코드 구조 개선            | `[refactor] UserService 책임 분리` |
| `test`     | 테스트 코드 작성 및 수정      | `[test] 로그인 서비스 테스트 추가`        |

### Issue 기반 작업 흐름

```text
1. Issue 생성
2. Issue 번호 기준으로 브랜치 생성
3. 작업 진행
4. Pull Request 생성
5. 코드 리뷰
6. Squash and Merge
7. 브랜치 삭제
8. Issue Close
```

### Issue와 Branch 연결 예시

Issue 번호가 `#12`이고 제목이 `[feat] 로그인 API 구현`인 경우:

```text
Issue: [feat] 로그인 API 구현
Branch: feature/#12-login-api
```

---

## 5. Pull Request Convention

모든 작업은 Pull Request를 통해 병합합니다.

### PR 생성 방향

```text
feature/* → develop
fix/* → develop
refactor/* → develop
docs/* → develop
test/* → develop
chore/* → develop

develop → main
hotfix/* → main
```

### PR 제목 규칙

PR 제목은 **Conventional Commit** 형식을 따릅니다.

```text
type: 작업 내용
```

### PR 제목 예시

```text
feat: 로그인 API 구현
fix: 토큰 재발급 오류 수정
refactor: UserService 책임 분리
docs: README 실행 방법 추가
test: 로그인 서비스 테스트 추가
chore: GitHub Actions 설정 추가
```

### PR Template

우리 팀은 아래 PR Template을 사용합니다.

```text
.github/PULL_REQUEST_TEMPLATE.md
```

PR 본문에는 아래 내용을 작성합니다.

* 관련 Issue
* 작업 내용
* 핵심 변경 사항
* 리뷰 포인트
* 영향 범위 및 테스트 결과
* 스크린샷
* PR 유형
* PR 체크리스트

### Issue 연결 규칙

PR 본문에는 관련 Issue를 연결합니다.

```markdown
Closes #12
```

Issue를 자동으로 닫지 않아야 하는 경우에는 아래처럼 작성합니다.

```markdown
Related to #12
```

---

## 6. Merge Strategy

우리 팀은 기본적으로 **Squash and Merge**를 사용합니다.

### Squash Merge 사용 이유

* PR 단위로 커밋 히스토리를 깔끔하게 유지할 수 있습니다.
* 기능 단위 변경 이력을 쉽게 파악할 수 있습니다.
* 불필요한 중간 커밋이 `develop`, `main` 브랜치에 남지 않습니다.

### Merge 규칙

* `feature/*`, `fix/*`, `refactor/*`, `docs/*`, `test/*`, `chore/*` 브랜치는 `develop`으로 Squash Merge합니다.
* `develop` 브랜치가 충분히 안정화되면 `main`으로 병합합니다.
* `main` 브랜치에 병합된 내용은 release로 간주합니다.
* PR 병합 후 작업 브랜치는 삭제합니다.

### Squash Merge 커밋 메시지

Squash Merge 시 최종 커밋 메시지는 PR 제목과 동일하게 정리합니다.

```text
feat: 로그인 API 구현
```

---

## 7. Main Branch Policy

`main` 브랜치는 배포 가능한 상태를 유지합니다.

### main 브랜치 규칙

* 직접 push하지 않습니다.
* 반드시 Pull Request를 통해서만 병합합니다.
* `main`에 병합된 내용은 release로 간주합니다.
* 긴급 수정이 필요한 경우 `hotfix/*` 브랜치를 사용합니다.

### develop 브랜치 규칙

* 기능 개발의 기준 브랜치입니다.
* 모든 기능 브랜치는 `develop`에서 분기합니다.
* 기능 작업 완료 후 `develop`으로 Pull Request를 생성합니다.
* `develop`은 항상 실행 가능한 상태를 유지하는 것을 목표로 합니다.

---

## 8. Code Review Rule

### 리뷰 요청 전 확인 사항

PR을 생성하기 전에 아래 내용을 확인합니다.

* [ ] 최신 `develop` 브랜치를 반영했는가?
* [ ] 불필요한 주석, 로그, 테스트 코드는 제거했는가?
* [ ] 코드가 정상적으로 빌드되는가?
* [ ] 관련 테스트를 수행했는가?
* [ ] PR 본문에 작업 내용과 테스트 결과를 작성했는가?
* [ ] 관련 Issue를 연결했는가?

### 리뷰 기준

리뷰어는 아래 기준으로 코드를 확인합니다.

* 기능 요구사항을 충족하는가?
* 코드가 이해하기 쉬운가?
* 불필요한 중복 코드가 없는가?
* 예외 상황이 적절히 처리되었는가?
* 네이밍이 명확한가?
* 테스트가 필요한 부분에 테스트가 작성되었는가?
* 변경 범위가 PR 목적에 비해 과도하지 않은가?

---

## 9. Recommended Workflow

일반적인 기능 개발 흐름은 아래와 같습니다.

```bash
# 1. develop 브랜치로 이동
git checkout develop

# 2. 최신 develop 반영
git pull origin develop

# 3. feature 브랜치 생성
git checkout -b feature/#12-login-api

# 4. 작업 후 변경 파일 확인
git status

# 5. 변경 파일 추가
git add .

# 6. 커밋
git commit -m "feat: 로그인 API 구현"

# 7. 원격 브랜치 push
git push origin feature/#12-login-api
```

이후 GitHub에서 Pull Request를 생성합니다.

```text
feature/#12-login-api → develop
```

PR이 승인되면 Squash and Merge로 병합합니다.

---

## 10. Commit & PR Example

### Issue

```text
[feat] 로그인 API 구현
```

### Branch

```text
feature/#12-login-api
```

### Commit

```text
feat: 로그인 API 구현
test: 로그인 서비스 테스트 추가
docs: 로그인 API 명세 추가
```

### Pull Request

```text
feat: 로그인 API 구현
```

### PR Body

```markdown
Closes #12
```

### Merge Commit

Squash Merge 시 최종 커밋 메시지는 아래와 같이 정리합니다.

```text
feat: 로그인 API 구현
```

---

## 11. Convention Summary

| 항목          | 규칙                   |
| ----------- | -------------------- |
| Git 전략      | 간소화된 Git Flow        |
| 배포 브랜치      | `main`               |
| 개발 브랜치      | `develop`            |
| 기능 브랜치      | `feature/#이슈번호-작업내용` |
| Issue 제목    | `[type] 작업 내용`       |
| PR 제목       | `type: 작업 내용`        |
| 커밋 메시지      | `type: 작업 내용`        |
| PR 병합 방식    | Squash and Merge     |
| Release 브랜치 | 사용하지 않음              |
| main 병합 의미  | release로 간주          |
| 작업 단위       | Issue 기반 작업 권장       |
