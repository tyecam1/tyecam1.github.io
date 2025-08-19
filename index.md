---
title: Hi, I'm Tye
---

I’m a First-Class (International) Engineering Master's graduate from Cardiff University with a KAIST exchange term.  
  
I build robotics, reinforcement learning, and systems projects with a focus on clean code, clear documentation, and reproducible results.

## Featured Projects

<div class="featured-grid">
{% assign featured = site.data.projects | where: "featured", true %}
{% for p in featured %}
  <article class="featured-card">
    <h3><a href="/projects/#{{ p.key | slugify }}" style="text-decoration:none; color:inherit;">{{ p.title }}</a></h3>

    {% if p.stack %}
      <div class="featured-meta">{{ p.stack | join: " · " }}</div>
    {% endif %}

    {% assign img = p.image | to_s | strip %}
    {% if img != "" %}
      <img class="featured-thumb" src="{{ img }}" alt="{{ p.title }}">
    {% endif %}

    {% if p.summary_short %}
      <p class="featured-summary">{{ p.summary_short }}</p>
    {% endif %}

    <div class="featured-links">
      <a href="/projects/#{{ p.key | slugify }}">Read more</a>
      {% if p.repo_url and p.repo_url != "" %} · <a href="{{ p.repo_url }}">Repository</a>{% endif %}
    </div>
  </article>
{% endfor %}
</div>

