---
layout: page
title: Projects
permalink: /projects/
---

<div class="projects-layout">
  <aside class="toc">
    <nav aria-label="Projects table of contents">
      <ul>
        {% for p in site.data.projects %}
          <li>
            <a id="toc-{{ p.key | slugify }}" href="#{{ p.key | slugify }}">
              {{ p.title }}
            </a>
          </li>
        {% endfor %}
      </ul>
    </nav>
  </aside>

  <main class="projects-main">
    {% for p in site.data.projects %}
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

        {% if p.summary_short %}<p class="project-summary">{{ p.summary_short }}</p>{% endif %}
        {% if p.summary_long %}<p>{{ p.summary_long }}</p>{% endif %}

        {% if p.repo_url and p.repo_url != "" %}
          <p class="project-links"><a href="{{ p.repo_url }}">Repository</a></p>
        {% endif %}
      </section>

      {% unless forloop.last %}<hr class="project-divider">{% endunless %}
    {% endfor %}
  </main>
</div>

<!-- Tiny JS to highlight the active ToC item while scrolling -->
<script>
  (function () {
    const secs = Array.from(document.querySelectorAll('.project-section'));
    const map = new Map(secs.map(s => [s.id, document.getElementById('toc-' + s.id)]));

    const io = new IntersectionObserver((entries) => {
      entries.forEach(e => {
        if (e.isIntersecting) {
          map.forEach(a => a && a.classList.remove('active'));
          const a = map.get(e.target.id);
          if (a) a.classList.add('active');
        }
      });
    }, { rootMargin: '-40% 0px -55% 0px', threshold: 0 });

    secs.forEach(s => io.observe(s));
  })();
</script>
