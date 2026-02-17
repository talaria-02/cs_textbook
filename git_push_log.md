# Git Push 과정 및 오류 해결 기록

> **날짜**: 2026-02-17  
> **리포지토리**: https://github.com/talaria-02/cs_textbook  
> **프로젝트**: 신입 DE/ML 전문가를 위한 CS 전공 핵심 총정리 교과서

---

## 1단계: Git 상태 확인

```bash
git status
```

### ❌ 오류
```
fatal: not a git repository (or any of the parent directories): .git
```

### 💡 원인 & 해결
`cs_ 교과서` 폴더가 아직 Git 저장소로 초기화되지 않은 상태였습니다.  
→ `git init`으로 초기화가 필요했습니다.

---

## 2단계: Git 초기화

```bash
git init
```

### ⚠️ 경고 (정상 동작)
```
Initialized empty Git repository in C:/Users/zxc20/???대뜑/cs_ 援먭낵??.git/
fatal: unknown write failure on standard output
```

### 💡 원인 & 해결
**실제로는 정상 초기화**되었습니다.  
이 에러는 PowerShell의 **한글(UTF-8) 인코딩 출력 문제**입니다.  
폴더명에 한글(`새 폴더`, `교과서`)이 포함되어 있어 콘솔에 출력할 때 깨져 보이는 것이며, `.git` 폴더는 정상 생성되었습니다.

> **Tip**: PowerShell에서 한글 경로 문제를 줄이려면 `[Console]::OutputEncoding = [System.Text.Encoding]::UTF8` 설정을 추가할 수 있습니다.

---

## 3단계: GitHub CLI (gh) 확인

```bash
gh auth status
```

### ❌ 오류
```
gh : 'gh' 용어가 cmdlet, 함수, 스크립트 파일 또는 실행할 수 있는 프로그램 이름으로 인식되지 않습니다.
```

### 💡 원인 & 해결
**GitHub CLI (`gh`)가 설치되어 있지 않았습니다.**  
`gh`가 있으면 `gh repo create`로 리포지토리를 자동 생성할 수 있지만, 없으므로 **GitHub 웹에서 직접 빈 리포지토리를 생성**하는 방법으로 대체했습니다.

> **설치 방법**: `winget install GitHub.cli`

---

## 4단계: curl로 GitHub API 호출 시도

```bash
curl -s -o /dev/null -w "%{http_code}" -X POST https://api.github.com/user/repos ...
```

### ❌ 오류
```
Invoke-WebRequest : 'SessionVariable' 매개 변수에 대한 인수가 누락되었습니다.
```

### 💡 원인 & 해결
**PowerShell에서 `curl`은 `Invoke-WebRequest`의 별칭(Alias)**입니다.  
리눅스의 `curl`과 완전히 다른 동작을 합니다.  
→ 이 방법을 포기하고 **사용자가 GitHub 웹에서 직접 리포지토리를 생성**한 뒤 리모트를 추가하는 방식으로 전환했습니다.

> **PowerShell에서 진짜 curl 쓰기**: `curl.exe`로 호출하면 됩니다. (`curl`이 아닌 `curl.exe`)

---

## 5단계: 파일 스테이징 & 커밋

```bash
git add -A
git commit -m "feat: CS 전공 핵심 총정리 교과서 v1.0 - 5과목 + Deep Dive"
```

### ✅ 결과 (성공)
```
[master (root-commit) c6ebe78] feat: CS 전공 핵심 총정리 교과서 v1.0 - 5과목 + Deep Dive
 7 files changed, 814 insertions(+)
 create mode 100644 01_computer_structure.md
 create mode 100644 02_OS.md
 create mode 100644 03_database.md
 create mode 100644 04_network.md
 create mode 100644 05_data_structure.md
 create mode 100644 README.md
 create mode 100644 SKILL.md
```

7개 파일, 814줄이 정상 커밋되었습니다.  
(`fatal: unknown write failure on standard output`는 2단계와 같은 한글 인코딩 출력 문제일 뿐, 커밋 자체는 성공)

---

## 6단계: 리모트 존재 여부 확인

```bash
git ls-remote https://github.com/talaria-02/cs-textbook.git
```

### ❌ 오류
```
remote: Repository not found.
fatal: repository 'https://github.com/talaria-02/cs-textbook.git/' not found
```

### 💡 원인 & 해결
리포지토리 이름이 `cs-textbook`이 아닌 **`cs_textbook`**(하이픈 → 언더스코어)이었습니다.  
→ 사용자 확인 후 올바른 이름으로 리모트를 추가했습니다.

---

## 7단계: 리모트 추가 & 브랜치 설정 & Push

```bash
git remote add origin https://github.com/talaria-02/cs_textbook.git
git branch -M main
git push -u origin main
```

### ✅ 결과 (최종 성공)
```
Enumerating objects: 9, done.
Counting objects: 100% (9/9), done.
Delta compression using up to 8 threads
Compressing objects: 100% (9/9), done.
Writing objects: 100% (9/9), 25.93 KiB | 3.70 MiB/s, done.
Total 9 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To https://github.com/talaria-02/cs_textbook.git
 * [new branch]      main -> main
branch 'main' set up to track 'origin/main'.
```

---

## 📝 배운 점 정리

| #   | 오류/이슈               | 원인                    | 해결                         |
| --- | ----------------------- | ----------------------- | ---------------------------- |
| 1   | `not a git repository`  | Git 미초기화            | `git init`                   |
| 2   | `unknown write failure` | PowerShell 한글 인코딩  | 무시해도 됨 (동작은 정상)    |
| 3   | `gh` 명령어 없음        | GitHub CLI 미설치       | 웹에서 리포 생성으로 대체    |
| 4   | `curl` 파라미터 오류    | PS의 curl ≠ 리눅스 curl | `curl.exe`로 호출하거나 우회 |
| 5   | `Repository not found`  | 리포 이름 불일치        | 정확한 이름 확인 후 재설정   |
