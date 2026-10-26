# 최민준 포트폴리오

2026학년도 초급프로젝트 과제 1, Hugo로 만든 개인 소개 웹사이트입니다.

- 사이트: https://sususk2.github.io/MyWebPage/
- 저장소: https://github.com/sususk2/MyWebPage
- 배포: `main`에 push하면 GitHub Actions가 빌드해서 GitHub Pages에 올립니다 ([Actions 실행 기록](https://github.com/sususk2/MyWebPage/actions))

## 목차

1. [페이지 구성](#페이지-구성)
2. [사용 도구와 버전](#사용-도구와-버전)
3. [설치](#설치)
4. [내 PC에서 사이트 확인하기](#내-pc에서-사이트-확인하기)
5. [수정할 파일 위치](#수정할-파일-위치)
6. [수정 후 재배포와 확인](#수정-후-재배포와-확인)
7. [배포 후 점검 목록](#배포-후-점검-목록)
8. [커밋 메시지 규칙](#커밋-메시지-규칙)
9. [자주 나는 문제](#자주-나는-문제)
10. [폴더 구성](#폴더-구성)
11. [출처와 라이선스](#출처와-라이선스)

## 페이지 구성

| 페이지 | 주소 | 내용 |
|--------|------|------|
| 홈 | `/MyWebPage/` | 이름, 한 줄 소개, 소개·활동 버튼, GitHub 아이콘 |
| 소개 | `/MyWebPage/about/` | 자기소개 `#intro`, 관심 분야 `#interests`, 학습 목표 `#goals`, 역량 `#skills` |
| 활동 목록 | `/MyWebPage/projects/` | 활동 2개 |
| 대표 활동 | `/MyWebPage/projects/activity-1/` | 캡스톤 AI 리포트: `#period` `#purpose` `#role` `#process` `#result` `#lessons` |
| 활동 2 | `/MyWebPage/projects/portfolio-site/` | 이 사이트 제작 과정 |
| 404 | 없는 주소 | 안내 문구와 홈·소개·활동 링크 |

## 사용 도구와 버전

| 도구 | 버전 | 쓰는 곳 |
|------|------|---------|
| Hugo extended | 0.167.0 | 사이트 빌드 (Actions 워크플로 `.github/workflows/hugo-pages.yml`에서 같은 버전 지정) |
| 테마 PaperMod | master, 2026-10-26 Download ZIP | `site/themes/template/` |
| Python | 3.9 이상 | 배포 준비·빌드 스크립트 (`prepare_github_pages.py`, `.github/pages_build.py`) |
| Git | Git for Windows (Git Bash) | 커밋·push |

## 설치

Windows 기준입니다. 처음 한 번만 하면 됩니다.

1. **Git**: https://git-scm.com 에서 Git for Windows 설치 (Git Bash 포함)
2. **Python**: https://www.python.org 에서 3.9 이상 설치
3. **Hugo extended 0.167.0**: [릴리스 페이지](https://github.com/gohugoio/hugo/releases/tag/v0.167.0)에서 `hugo_extended_0.167.0_windows-amd64.zip`을 받아 압축을 풀고, `hugo.exe`가 있는 폴더를 PATH에 추가
4. 설치 확인 (Git Bash):

```bash
git --version
python --version
hugo version     # hugo v0.167.0-...+extended 가 나오면 정상
```

5. 저장소 받기:

```bash
git clone https://github.com/sususk2/MyWebPage.git
cd MyWebPage
```

## 내 PC에서 사이트 확인하기

**미리보기 (수정하면 바로 반영)**

```bash
cd site
hugo server --config pages.json --themesDir themes --theme template
```

브라우저에서 http://localhost:1313/MyWebPage/ 를 엽니다. 끄려면 `Ctrl + C`.

**배포와 같은 방식으로 빌드**

저장소 맨 위 폴더에서 실행합니다. 결과는 `public/`에 생기며 Git에는 올리지 않습니다(`.gitignore`).

```bash
python .github/pages_build.py --build
```

`빌드 완료`가 나오고 `public/index.html`이 생기면 정상입니다.

## 수정할 파일 위치

| 바꾸고 싶은 것 | 파일 |
|----------------|------|
| 사이트 제목, 홈 이름·한 줄 소개, 홈 버튼, 상단 메뉴, GitHub 링크, 언어 | `site/pages.json` |
| 소개 페이지 (자기소개·관심 분야·학습 목표·역량) | `site/content/about.md` |
| 활동 목록 페이지 설명 | `site/content/projects/_index.md` |
| 대표 활동 글 | `site/content/projects/activity-1.md` |
| 키보드 초점 표시·본문 바로가기·동작 줄이기 스타일 | `site/assets/css/extended/focus.css` |
| 홈 GitHub 아이콘 링크 (접근 가능한 이름 추가) | `site/layouts/_partials/social_icons.html` |
| 상단 메뉴·다크모드 버튼 이름·본문 바로가기 링크 | `site/layouts/_partials/header.html` |
| 푸터 문구·맨 위로 버튼 이름 | `site/layouts/_partials/footer.html` |
| 경로 표시(현재 위치) 영역 이름 | `site/layouts/_partials/breadcrumbs.html` |
| 본문 영역 id(본문 바로가기 대상) | `site/layouts/baseof.html` |
| 없는 주소로 왔을 때 보이는 안내 | `site/layouts/404.html` |
| 페이지 제목(404 한국어)·검색 노출(404 noindex) | `site/layouts/_partials/head.html` |
| 404·긴 URL·표 스타일 | `site/assets/css/extended/pages.css` |
| 파비콘 | `site/static/` |

테마 원본 `site/themes/template/`은 직접 고치지 않습니다. 바꿀 부분은 위 파일처럼 `site/` 아래에 같은 경로로 만들어 덮어씁니다.

글에 새 섹션을 넣을 때는 `## 제목 {#영문-앵커}`처럼 앵커를 붙이면 `about/#영문-앵커` 주소로 바로 열 수 있습니다. 글의 `date`를 미래 날짜로 쓰면 Hugo가 그 글을 빌드에서 빼므로 오늘 이전 날짜로 씁니다.

## 수정 후 재배포와 확인

1. 파일 수정 후 `hugo server`로 미리 확인
2. 커밋하고 push

```bash
git add 바꾼-파일
git commit -m "content: 무엇을 바꿨는지"
git push origin main
```

3. [Actions](https://github.com/sususk2/MyWebPage/actions)에서 `Deploy Hugo to GitHub Pages` 실행이 초록 체크(build·deploy 성공)인지 확인 (1~2분)
4. 시크릿 창에서 https://sususk2.github.io/MyWebPage/ 를 열어 바뀐 내용 확인. 예전 화면이 보이면 `Ctrl + F5`

실패(빨간 X)하면 실행을 열어 build 단계 로그의 `ERROR` 줄을 확인합니다. GitHub 저장소의 Settings → Pages → Source는 `GitHub Actions`로 설정되어 있어야 합니다.

## 배포 후 점검 목록

push 후 시크릿 창에서 확인합니다.

- [ ] Actions 실행이 build·deploy 모두 성공
- [ ] 홈·소개·활동·대표 활동 페이지가 열리고 CSS가 적용됨
- [ ] 상단 메뉴(소개·활동·GitHub)와 홈 버튼이 맞는 곳으로 이동, 뒤로 가기로 복귀
- [ ] `about/#goals`처럼 앵커 주소를 직접 입력하고 새로고침해도 같은 위치
- [ ] 없는 주소(`/MyWebPage/없는주소/`)에서 404 안내와 홈 링크가 보임
- [ ] 개발자 도구 기기 모드 1440px·1024px·768px·390px·360px에서 가로 스크롤·겹침 없음
- [ ] Tab만으로 본문 바로가기 → 메뉴 → 본문 링크 → 푸터까지 이동, 파란 초점선이 보임, Enter로 이동
- [ ] 개발자 도구 Console에 빨간 오류가 없고 Network에 실패(4xx) 요청이 없음

## 커밋 메시지 규칙

`종류: 무엇을 왜 바꿨는지` 형식으로 한 커밋에 한 가지 작업만 담습니다.

| 종류 | 쓰는 경우 |
|------|-----------|
| `config` | `site/pages.json` 설정 변경 |
| `content` | 페이지 글 작성·수정 |
| `style` | CSS 변경 |
| `a11y` | 접근성 개선 (키보드, 화면 낭독기 이름 등) |
| `feat` | 새 페이지·기능 추가 |
| `fix` | 잘못된 동작·내용 수정 |
| `docs` | README 등 문서 |
| `chore` | 저장소 관리 파일 (.gitignore 등) |

## 유효 커밋 집계 방법

과제 보고서 4장에 적는 개수를 다음 명령으로 셉니다.

```bash
git fetch origin
git rev-list --count origin/main                 # 전체 커밋 수 (N)
git log --oneline origin/main | tail -1          # 가장 오래된 커밋 = 원본 ZIP 등록(905ed2d) → 제외 (E = 1)
git log --merges --oneline origin/main           # 병합 커밋 (없어야 함)
```

유효 커밋 = N − E. 원본 ZIP 등록처럼 본인 작성 내용이 없는 커밋만 제외합니다.

## 자주 나는 문제

| 증상 | 원인 | 해결 |
|------|------|------|
| `git push`에서 `Password authentication is not supported` | GitHub는 Git 작업에 계정 비밀번호를 받지 않음. 저장된 로그인 정보가 만료됨 | `git config --show-origin --get-all credential.helper`로 저장 방식 확인 → `printf "protocol=https\nhost=github.com\n\n" \| git credential reject`로 저장 정보 삭제 → 다시 push하고 브라우저로 로그인 |
| push했는데 사이트가 그대로 | 브라우저 캐시(최대 약 10분) 또는 Actions 실행 중 | Actions가 초록 체크인지 확인 → 시크릿 창이나 `Ctrl + F5` |
| 새 글이 사이트에 안 나옴 | 글의 `date`가 미래 시각 | `date`를 오늘 이전으로 (시간대는 `Asia/Seoul`) |
| 첫 실행이 실패 | Pages Source를 설정하기 전에 push함 | Settings → Pages → Source를 `GitHub Actions`로 바꾼 뒤 실패한 실행을 Re-run |

## 폴더 구성

```
MyWebPage/
├── site/                     Hugo 사이트 (실제로 수정하는 곳)
│   ├── pages.json            사이트 설정 (baseURL, 메뉴, 프로필 등)
│   ├── content/              페이지 글 (about.md, projects/)
│   ├── assets/css/extended/  추가 CSS
│   ├── layouts/_partials/    테마 부분 덮어쓰기
│   ├── static/               파비콘 등 그대로 복사되는 파일
│   └── themes/template/      PaperMod 테마 원본
├── .github/
│   ├── workflows/hugo-pages.yml  push 시 빌드·배포
│   └── pages_build.py            Actions가 쓰는 빌드 스크립트
├── prepare_github_pages.py   수업 제공 배포 준비 스크립트 (처음 한 번 실행)
├── .github-pages.json        준비 스크립트가 만든 빌드 정보
├── LICENSE                   PaperMod 라이선스 (MIT)
└── assets/ layouts/ i18n/ …  Download ZIP 원본 테마 파일 (빌드에는 site/themes/template 사용)
```

## 출처와 라이선스

| 자료 | 사용 위치 | 구분 | 출처 | 이용 조건 |
|------|-----------|------|------|-----------|
| PaperMod 테마 | `site/themes/template/`, 저장소 루트 원본 파일 | 외부 자료 | https://github.com/adityatelange/hugo-PaperMod | MIT License (`LICENSE` 유지, 사이트 하단 "Powered by Hugo & PaperMod" 표시 유지) |
| Hugo | 빌드 도구 | 외부 도구 | https://gohugo.io | Apache License 2.0 |
| 배포 준비 스크립트·워크플로 | `prepare_github_pages.py`, `.github/` | 수업 제공 | 초급프로젝트 수업 자료 (v3.1) | 수업 자료 |
| 사이트 설정·글 | `site/pages.json`, `site/content/` | AI 초안 + 본인 확인 | Claude로 초안 작성, 본인 정보·사실 확인과 수정 | 본 과제용 |
| 추가 CSS | `site/assets/css/extended/focus.css`, `pages.css` | AI 생성 후 본인 검토 | Claude | 본 과제용 |
| 레이아웃 덮어쓰기 | `site/layouts/` (head·header·footer·breadcrumbs·baseof·social_icons·404) | 외부 자료 수정 | PaperMod 원본 파일을 복사해 바꾼 줄만 주석으로 표시 (Claude 도움) | MIT License (원본 출처 유지) |
| 파비콘 5개 | `site/static/` | AI 생성 | Claude (Python Pillow로 생성) | 본 과제용 |
| 대표 활동 근거 | 활동 페이지 링크 | 본인 팀 프로젝트 | https://github.com/sususk2/capstone | 팀 저장소 |

이미지·사진은 사용하지 않았습니다.

### AI 활용 범위

Claude를 다음 작업에 사용했습니다. 제안은 실제 화면·빌드로 확인한 뒤 반영 여부를 정했고, 커밋과 최종 확인은 본인이 했습니다. AI 도움으로 만든 커밋은 메시지 끝에 `Co-Authored-By: Claude`가 붙어 있습니다.

- push 인증 실패 원인 분석
- `site/pages.json` 설정과 페이지 구성 초안
- 반응형·키보드 접근성 점검과 수정(초점 표시, 아이콘 링크 이름, 본문 바로가기)
- 대표 활동 글 초안 (캡스톤 저장소 기록을 근거로 작성 후 본인 확인)
- README·보고서 초안 정리
