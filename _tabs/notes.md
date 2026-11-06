---
title: 노트
icon: fas fa-pen-nib
order: 3
---

중요한 이론과 테크닉을 정리한 글입니다. 주제(두 번째 카테고리)별로 묶여 있습니다.

> 새 노트는 `_templates/note.md`{: .filepath } 를 복사해서 `_posts/`{: .filepath } 에 만듭니다.
> 머리말에 `categories: [Notes, 주제]` 처럼 주제를 적으면 아래에 주제별로 묶입니다.
{: .prompt-tip }

{% assign notes = site.categories['Notes'] %}
{% if notes and notes.size > 0 %}
{% assign groups = notes | group_by_exp: 'post', "post.categories[1] | default: '기타'" | sort: 'name' %}
{% for group in groups %}

## {{ group.name }}

<ul class="simple-post-list">
  {%- for post in group.items %}
  <li>
    <span class="date text-muted">{{ post.date | date: '%Y-%m-%d' }}</span>
    <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
    {%- if post.description %}
    <small class="text-muted d-block">{{ post.description }}</small>
    {%- endif %}
  </li>
  {%- endfor %}
</ul>

{% endfor %}
{% else %}
아직 노트가 없습니다.
{% endif %}
