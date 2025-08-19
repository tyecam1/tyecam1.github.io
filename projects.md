---
layout: page
title: Projects
permalink: /projects/
---

# Projects

<div class="projects-grid">
{% for p in site.data.projects %}
  <article class="project">
    <h3>{{ p.title }}{% if p.year %} ({{ p.year }}){% endif %}</h3>

    {% if p.image %}
      <img class="thumb" src="{{ p.image }}" alt="{{ p.title }}">
    {% endif %}

    {% if p.stack %}
      <div class="stack">{{ p.stack | join: " · " }}</div>
    {% endif %}

    <p class="summary">{{ p.summary_short }}</p>
    <p>{{ p.summary_long }}</p>

    <p class="links">
      {% if p.repo_url %}<a href="{{ p.repo_url }}">Repository</a>{% endif %}
    </p>
  </article>
{% endfor %}
</div>
