---
title: Hi, I'm Tye
---

I’m a First-Class (International) Engineering Master's graduate from Cardiff University with a KAIST exchange term.  
I build robotics, reinforcement learning, and systems projects with a focus on clean code, clear documentation, and reproducible results.

## Featured Projects
<div class="projects-grid">
{% assign featured = site.data.projects | where: "featured", true %}
{% for p in featured %}
  <article class="project">
    <h3>{{ p.title }}</h3>
    {% if p.image %}<img class="thumb" src="{{ p.image }}" alt="{{ p.title }}">{% endif %}
    <p class="summary">{{ p.summary_short }}</p>
    {% if p.repo_url %}<p class="links"><a href="{{ p.repo_url }}">Repository</a></p>{% endif %}
  </article>
{% endfor %}
</div>
