---
# 사이트 첫 화면이자 사이드바의 유일한 메뉴입니다.
# 표 내용은 _data/papers.yml 에서 수정합니다.
title: 논문
icon: fas fa-book-open
order: 1
permalink: /
---

**필수** 논문은 해당 주차 미팅 전까지 읽어 와 주세요.

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
