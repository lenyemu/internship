---
title: 읽을 논문
icon: fas fa-book-open
order: 1
---

인턴십 기간 동안 읽을 논문 목록입니다. **필수** 논문은 해당 주차 미팅 전까지 읽어 와 주세요.

> 목록은 저장소의 `_data/papers.yml`{: .filepath } 파일에서 수정합니다.
> 논문 PDF는 저작권 문제로 직접 올리지 않고 링크로 공유합니다.
{: .prompt-tip }

{% for group in site.data.papers %}

## {{ group.week }}{% if group.topic %} · {{ group.topic }}{% endif %}

<table class="reading-list">
  <thead>
    <tr>
      <th>논문</th>
      <th>구분</th>
      <th>발표</th>
      <th>정리 글</th>
      <th>메모</th>
    </tr>
  </thead>
  <tbody>
  {%- for p in group.papers %}
    <tr>
      <td class="paper">
        {%- if p.url -%}
          <a href="{{ p.url }}" target="_blank" rel="noopener">{{ p.title }}</a>
        {%- else -%}
          {{ p.title }}
        {%- endif -%}
        {%- if p.authors or p.venue -%}
          <br><small class="text-muted">{{ p.authors }}{% if p.authors and p.venue %} · {% endif %}{{ p.venue }}</small>
        {%- endif -%}
      </td>
      <td class="nowrap">
        {%- if p.required -%}
          <span class="paper-badge required">필수</span>
        {%- else -%}
          <span class="paper-badge optional">선택</span>
        {%- endif -%}
      </td>
      <td class="nowrap">{{ p.presenter | default: '-' }}</td>
      <td class="nowrap">
        {%- assign summary = nil -%}
        {%- if p.post -%}
          {%- assign summary = site.posts | where: 'slug', p.post | first -%}
        {%- endif -%}
        {%- if summary -%}
          <a href="{{ summary.url | relative_url }}">보기</a>
        {%- else -%}
          -
        {%- endif -%}
      </td>
      <td>{{ p.memo | default: '' }}</td>
    </tr>
  {%- endfor %}
  </tbody>
</table>

{% endfor %}

## 논문 정리 글

{% assign paper_posts = site.categories['Papers'] %}
{% if paper_posts and paper_posts.size > 0 %}
<ul class="simple-post-list">
  {%- for post in paper_posts %}
  <li>
    <span class="date text-muted">{{ post.date | date: '%Y-%m-%d' }}</span>
    <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
    {%- if post.description %}
    <small class="text-muted d-block">{{ post.description }}</small>
    {%- endif %}
  </li>
  {%- endfor %}
</ul>
{% else %}
아직 정리 글이 없습니다. `_templates/paper.md`{: .filepath } 템플릿으로 첫 글을 써 보세요.
{% endif %}
