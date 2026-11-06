# Research Internship

연구 인턴십을 위한 블로그입니다. 읽을 논문, 미팅 기록 · 자료, 이론 · 테크닉 노트를 모아 둡니다.

**사이트 주소: <https://lenyemu.github.io/internship/>**

[Jekyll](https://jekyllrb.com/) + [Chirpy](https://github.com/cotes2020/jekyll-theme-chirpy) 테마로 만들었고,
`main` 브랜치에 커밋하면 GitHub Actions가 1~2분 안에 사이트를 다시 빌드해 배포합니다.

> ⚠️ 이 사이트는 공개 웹사이트입니다. 미발표 연구 내용, 데이터, 개인정보, 논문 PDF는 올리지 마세요.

## 무엇을 어디서 고치나요?

| 하고 싶은 일 | 고칠 곳 |
|---|---|
| 읽을 논문 추가 · 수정 | [`_data/papers.yml`](_data/papers.yml) |
| 미팅 기록 쓰기 | [`_templates/meeting.md`](_templates/meeting.md) 복사 → `_posts/YYYY-MM-DD-제목.md` |
| 이론 · 테크닉 노트 쓰기 | [`_templates/note.md`](_templates/note.md) 복사 → `_posts/YYYY-MM-DD-제목.md` |
| 논문 정리 글 쓰기 | [`_templates/paper.md`](_templates/paper.md) 복사 → `_posts/YYYY-MM-DD-제목.md` |
| 미팅 발표 자료 올리기 | [`assets/files/meetings/`](assets/files/meetings/) 에 업로드 |
| 글에 넣을 이미지 올리기 | [`assets/img/posts/`](assets/img/posts/) 에 업로드 |
| 글쓴이 등록 | [`_data/authors.yml`](_data/authors.yml) |
| 인턴십 안내 (일정 · 장소 등) | [`_tabs/about.md`](_tabs/about.md) |
| 사이트 제목 · 설정 | [`_config.yml`](_config.yml) |

자세한 사용법은 사이트의 두 글을 참고하세요.

- [인턴십 블로그 사용 안내](https://lenyemu.github.io/internship/posts/welcome/): 글 쓰기, 파일 올리기, 오류 해결
- [글쓰기 문법 정리](https://lenyemu.github.io/internship/posts/writing-guide/): 마크다운, 수식, 코드, 이미지 · 파일 첨부

## 폴더 구조

```text
.
├── _config.yml            # 사이트 설정 (제목, 주소, 언어 등)
├── _data/
│   ├── papers.yml         # 읽을 논문 목록 → "읽을 논문" 페이지의 표
│   ├── authors.yml        # 글쓴이 목록
│   ├── contact.yml        # 사이드바 아이콘 링크
│   └── locales/ko-KR.yml  # 테마 한국어 문구 일부 수정
├── _posts/                # 모든 글 (미팅 · 노트 · 논문 정리 · 공지)
├── _tabs/                 # 사이드바 메뉴 페이지
├── _templates/            # 새 글 템플릿 (사이트에는 표시되지 않음)
├── assets/
│   ├── files/meetings/    # 미팅 자료 파일
│   ├── img/posts/         # 글에 넣는 이미지
│   └── css/               # 추가 스타일
└── .github/workflows/     # 자동 빌드 · 배포 설정
```

## 카테고리 규칙

글 머리말의 `categories` 첫 번째 값으로 메뉴가 나뉩니다.

| 카테고리 | 표시되는 곳 |
|---|---|
| `Meetings` | 미팅 |
| `Notes` | 노트 (두 번째 값이 주제 묶음. 예: `[Notes, 선형대수]`) |
| `Papers` | 읽을 논문 → 논문 정리 글 |
| `Notice` | 공지 (홈 화면) |

## 내 컴퓨터에서 미리 보기 (선택)

GitHub 웹에서만 작업해도 됩니다. 글을 많이 쓴다면 로컬에서 미리 볼 수 있습니다.
Ruby 3.x와 Bundler가 있어야 합니다.

```bash
bundle install
bash tools/run.sh      # http://127.0.0.1:4000/internship/ 에서 미리 보기
bash tools/test.sh     # 배포 때와 같은 빌드 + 링크 검사
```

VS Code의 Dev Containers나 GitHub Codespaces를 쓰면 설치 없이 같은 환경을 열 수 있습니다 (`.devcontainer/`).
