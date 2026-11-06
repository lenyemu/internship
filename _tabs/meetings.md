---
title: 미팅
icon: fas fa-calendar-check
order: 2
---

미팅 기록과 발표 자료 모음입니다. 최근 미팅이 맨 위에 옵니다.

> 새 미팅 기록은 `_templates/meeting.md`{: .filepath } 를 복사해서 `_posts/`{: .filepath } 에 만듭니다.
> 발표 자료는 `assets/files/meetings/`{: .filepath } 에 올리고 글에서 링크합니다.
{: .prompt-tip }

{% assign meetings = site.categories['Meetings'] %}
{% if meetings and meetings.size > 0 %}
<ul class="simple-post-list">
  {%- for post in meetings %}
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
아직 미팅 기록이 없습니다.
{% endif %}
