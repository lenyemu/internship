---
title: "글쓰기 문법 정리 (마크다운 · 수식 · 코드)"
categories: [Notice]
tags: [guide, markdown]
author: lenyemu
description: "머리말, 마크다운, LaTeX 수식, 코드 블록, 강조 박스, 이미지 · 파일 첨부 쓰는 법"
math: true
---

글은 마크다운(Markdown)으로 씁니다. 자주 쓰는 문법만 모았습니다.
각 항목의 **위 코드 블록이 입력**, 그 아래가 **실제로 보이는 모습**입니다.

## 머리말 (Front Matter)

모든 글은 맨 위에 `---` 로 감싼 머리말이 있어야 합니다.

```yaml
---
title: "글 제목"                # 콜론(:)이나 #이 들어가면 꼭 큰따옴표로 감싸기
categories: [Notes, 선형대수]   # 첫 번째: Meetings / Notes / Papers 중 하나
tags: [regression, numpy]      # 자유롭게, 영어 소문자 권장
author: lenyemu                # _data/authors.yml 에 등록한 아이디
description: "한 줄 요약"       # 목록과 검색 결과에 표시됨
math: true                     # 수식을 쓸 때만 true
pin: true                      # (선택) 홈 화면 맨 위에 고정
---
```

## 기본 문법

```markdown
## 큰 제목
### 작은 제목

**굵게**, *기울임*, `코드`, ~~취소선~~

- 글머리 기호 목록
  - 들여쓰기(스페이스 2칸)로 하위 목록
1. 번호 목록

[링크 글자](https://arxiv.org)

> 인용문
```

**굵게**, *기울임*, `코드`, ~~취소선~~

- 글머리 기호 목록
  - 들여쓰기(스페이스 2칸)로 하위 목록
1. 번호 목록

[링크 글자](https://arxiv.org)

> 인용문

## 표

```markdown
| 방법 | 정확도 | 비고 |
|---|:---:|---:|
| Baseline | 71.2 | 왼쪽 정렬 |
| Ours | **78.5** | 오른쪽 정렬 |
```

| 방법 | 정확도 | 비고 |
|---|:---:|---:|
| Baseline | 71.2 | 왼쪽 정렬 |
| Ours | **78.5** | 오른쪽 정렬 |

## 수식 (LaTeX)

머리말에 `math: true` 가 있어야 수식이 보입니다.

**문장 안 수식**은 `$$ ... $$` 를 문장 중간에 씁니다.

```markdown
손실 함수는 $$ L(\theta) = \frac{1}{n}\sum_{i=1}^{n} \ell(f_\theta(x_i), y_i) $$ 로 정의한다.
```

손실 함수는 $$ L(\theta) = \frac{1}{n}\sum_{i=1}^{n} \ell(f_\theta(x_i), y_i) $$ 로 정의한다.

**별도 줄 수식**은 `$$` 위아래로 **빈 줄**을 꼭 둡니다.

```markdown
(빈 줄)
$$
\nabla_\theta L = \frac{1}{n} \sum_{i=1}^{n} \nabla_\theta \ell(f_\theta(x_i), y_i)
$$
(빈 줄)
```

$$
\nabla_\theta L = \frac{1}{n} \sum_{i=1}^{n} \nabla_\theta \ell(f_\theta(x_i), y_i)
$$

**번호 붙은 수식**과 참조:

```markdown
$$
\begin{equation}
  p(\theta \mid D) = \frac{p(D \mid \theta)\, p(\theta)}{p(D)}
  \label{eq:bayes}
\end{equation}
$$

식 \eqref{eq:bayes} 는 베이즈 정리이다.
```

$$
\begin{equation}
  p(\theta \mid D) = \frac{p(D \mid \theta)\, p(\theta)}{p(D)}
  \label{eq:bayes}
\end{equation}
$$

식 \eqref{eq:bayes} 는 베이즈 정리이다.

> 목록(`-`, `1.`) 맨 앞에서 수식을 시작할 때는 첫 `$` 앞에 `\` 를 붙여 `\$$ x^2 $$` 처럼 씁니다.
{: .prompt-info }

## 코드 블록

언어 이름을 적으면 색이 입혀집니다. 아래 줄에 `{: file="..." }` 을 붙이면 파일 이름이 표시됩니다.

````markdown
```python
def softmax(x):
    e = np.exp(x - x.max())
    return e / e.sum()
```
{: file="utils.py" }
````

```python
def softmax(x):
    e = np.exp(x - x.max())
    return e / e.sum()
```
{: file="utils.py" }

## 강조 박스

인용문(`>`) 바로 아래 줄에 종류를 적습니다. `tip`, `info`, `warning`, `danger` 네 가지가 있습니다.

```markdown
> 미팅 전까지 2절을 읽어 오세요.
{: .prompt-tip }
```

> 미팅 전까지 2절을 읽어 오세요.
{: .prompt-tip }

> 참고할 만한 내용입니다.
{: .prompt-info }

> 자주 하는 실수입니다.
{: .prompt-warning }

> 절대 하면 안 되는 것입니다.
{: .prompt-danger }

## 체크리스트

```markdown
- [x] 논문 1절 읽기
- [ ] 실험 코드 돌려 보기
```

- [x] 논문 1절 읽기
- [ ] 실험 코드 돌려 보기

## 이미지

1. 이미지를 `assets/img/posts/` 폴더에 올립니다 (Add file → Upload files).
2. 글에서 `/assets/img/posts/파일이름` 으로 넣습니다. 바로 아래 줄에 `_설명_` 을 쓰면 캡션이 됩니다.

```markdown
![모델 구조](/assets/img/posts/2026-11-15-model.png){: width="600" }
_그림 1. 모델 구조_
```

> 이미지 주소는 `/assets/...` 로 시작합니다. 사이트 주소의 `/internship` 은 테마가 자동으로 붙여 줍니다.
{: .prompt-info }

## 파일 첨부

PDF, 슬라이드 같은 파일은 `assets/files/` 아래(미팅 자료는 `assets/files/meetings/`)에 올리고, 글에서는 아래처럼 링크합니다.
경로 앞에 `/` 를 붙이지 않습니다.

{% raw %}
```markdown
[킥오프 미팅 자료 (PDF)]({% link assets/files/meetings/2026-11-06-kickoff-agenda.pdf %})
```
{% endraw %}

[킥오프 미팅 자료 (PDF)]({% link assets/files/meetings/2026-11-06-kickoff-agenda.pdf %})

> `{% raw %}{% link ... %}{% endraw %}` 는 파일이 실제로 있는지 검사합니다. 파일 이름에 오타가 있으면 사이트가 갱신되지 않고 Actions 탭에 오류가 표시됩니다.
{: .prompt-tip }

## 다른 글 링크

{% raw %}
```markdown
[최소제곱법 노트]({% link _posts/2026-11-06-least-squares.md %})
```
{% endraw %}

[최소제곱법 노트]({% link _posts/2026-11-06-least-squares.md %})

## 각주

```markdown
Transformer[^1]는 2017년에 제안되었다.

[^1]: Vaswani et al., "Attention Is All You Need", NeurIPS 2017.
```

Transformer[^1]는 2017년에 제안되었다.

[^1]: Vaswani et al., "Attention Is All You Need", NeurIPS 2017.

## 더 알아보기

- Chirpy 테마의 전체 문법 예시: [Writing a New Post](https://chirpy.cotes.page/posts/write-a-new-post/), [Text and Typography](https://chirpy.cotes.page/posts/text-and-typography/)
