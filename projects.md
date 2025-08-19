---
layout: page
title: Projects
permalink: /projects/
---

<div id="top"></div>

# Projects

<!-- Optional in-page nav generated from your data file -->
<nav class="project-nav">
  <strong>Jump to:</strong>
  {% for p in site.data.projects %}
    <a href="#{{ p.key | slugify }}">{{ p.title }}</a>{% unless forloop.last %} · {% endunless %}
  {% endfor %}
</nav>

{% assign projects = site.data.projects %}
{% for p in projects %}

<section class="project-section anchor-target" id="{{ p.key | slugify }}">
  <header class="project-header">
    <h2>{{ p.title }}{% if p.year %} ({{ p.year }}){% endif %}</h2>
    {% if p.stack %}
      <div class="project-meta">{{ p.stack | join: " · " }}</div>
    {% endif %}
  </header>

  {% assign img = p.image | to_s | strip %}
  {% if img != "" %}
    <img class="project-hero" src="{{ img }}" alt="{{ p.title }}">
  {% endif %}

  <div class="project-body">
    {% if p.summary_short %}<p class="project-summary">{{ p.summary_short }}</p>{% endif %}
    {% if p.summary_long %}<p>{{ p.summary_long }}</p>{% endif %}
  </div>

  <div class="project-links">
    {% if p.repo_url and p.repo_url != "" %}
      <a href="{{ p.repo_url }}">Repository</a>
    {% endif %}
    <a class="back-to-top" href="#top">Back to top</a>
  </div>
</section>

{% unless forloop.last %}<hr class="project-divider">{% endunless %}
{% endfor %}
