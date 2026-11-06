# Research Internship

연구 인턴십에서 읽을 논문 목록을 보여 주는 사이트입니다.

**사이트 주소: <https://lenyemu.github.io/internship/>**

[Jekyll](https://jekyllrb.com/) + [Chirpy](https://github.com/cotes2020/jekyll-theme-chirpy) 테마로 만들었고,
`main` 브랜치에 커밋하면 GitHub Actions가 1~2분 안에 사이트를 다시 빌드해 배포합니다.

> ⚠️ 이 사이트는 공개 웹사이트입니다. 미발표 연구 내용, 데이터, 개인정보, 논문 PDF는 올리지 마세요.

## 논문 목록 고치는 법

1. [`_data/papers.yml`](_data/papers.yml) 을 열고 연필 아이콘(Edit)을 누릅니다.
2. 파일 맨 위 설명대로 논문을 추가하거나 고칩니다. 들여쓰기는 **스페이스 2칸**이며, 탭 문자는 쓰면 안 됩니다.
3. **Commit changes** 를 누르면 1~2분 뒤 사이트에 반영됩니다.

진행 상황은 [Actions](https://github.com/lenyemu/internship/actions) 탭에서 볼 수 있습니다 (초록 체크 = 반영 완료, 빨간 X = 오류).
빨간 X가 뜨면 그 항목을 눌러 오류 메시지를 확인하세요. 흔한 원인은 YAML 들여쓰기 실수, 또는 제목에 `:` 가 들어갔는데 큰따옴표로 감싸지 않은 경우입니다.

## 그 밖에 고칠 곳

| 하고 싶은 일 | 고칠 곳 |
|---|---|
| 사이트 제목 · 부제 · 설정 | [`_config.yml`](_config.yml) |
| 첫 화면 안내 문구 · 표 모양 | [`_tabs/papers.md`](_tabs/papers.md) |
| 사이드바 아래 아이콘 링크 | [`_data/contact.yml`](_data/contact.yml) |

## 폴더 구조

```text
.
├── _config.yml            # 사이트 설정 (제목, 주소, 언어 등)
├── _data/
│   ├── papers.yml         # 논문 목록 → 첫 화면("논문")의 표
│   ├── contact.yml        # 사이드바 아이콘 링크
│   └── locales/ko-KR.yml  # 테마 한국어 문구 일부 수정
├── _includes/sidebar.html # 테마 사이드바 수정본 ('홈' 메뉴 제거)
├── _tabs/papers.md        # 사이트 첫 화면이자 유일한 메뉴 ("논문")
├── assets/
│   ├── img/avatar.svg     # 사이드바 로고
│   └── css/               # 추가 스타일
└── .github/workflows/     # 자동 빌드 · 배포 설정
```

## 내 컴퓨터에서 미리 보기 (선택)

GitHub 웹에서만 작업해도 됩니다. 로컬에서 미리 보려면 Ruby 3.x와 Bundler가 있어야 합니다.

```bash
bundle install
bash tools/run.sh      # http://127.0.0.1:4000/internship/ 에서 미리 보기
bash tools/test.sh     # 배포 때와 같은 빌드 + 링크 검사
```

VS Code의 Dev Containers나 GitHub Codespaces를 쓰면 설치 없이 같은 환경을 열 수 있습니다 (`.devcontainer/`).
