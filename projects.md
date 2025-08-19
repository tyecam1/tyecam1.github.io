---
layout: page
title: Projects
permalink: /projects/
---

{% comment %}
Order:
1) CURRENT projects by start_date (newest → oldest)
2) PAST projects by end_date (newest → oldest)

Dates in _data/projects.yml should be ISO strings: "YYYY-MM-DD".
{% endcomment %}
{% assign current = site.data.projects | where: "status", "current" | sort: "start_date" | reverse %}
{% assign past    = site.data.projects | where: "status", "past"    | sort: "end_date"   | reverse %}
{% assign projects = current | concat: past %}

<div class="projects-layout">
  <aside class="toc">
    <nav aria-label="Projects table of contents">
      <ul>
        {% for p in projects %}
          <li>
            <a id="toc-{{ p.key | slugify }}" href="#{{ p.key | slugify }}">
              {{ p.toc_title | default: p.title | truncate: 48 }}
            </a>
          </li>
        {% endfor %}
      </ul>
    </nav>
  </aside>

  <main class="projects-main">
    {% for p in projects %}
      <section class="project-section anchor-target" id="{{ p.key | slugify }}">
        <header class="project-header">
          <h2>
            {{ p.title }}
            {% if p.status == "current" %}
              (In Progress{% if p.start_date %}, since {{ p.start_date | date: "%b %Y" }}{% endif %})
            {% elsif p.start_date and p.end_date %}
              ({{ p.start_date | date: "%b %Y" }} – {{ p.end_date | date: "%b %Y" }})
            {% endif %}
          </h2>
          {% if p.stack %}
            <div class="project-meta">{{ p.stack | join: " · " }}</div>
          {% endif %}
        </header>

        {% assign img = p.image | to_s | strip %}
        {% if img != "" %}
          <img class="project-hero" src="{{ img }}" alt="{{ p.title }}">
        {% endif %}

        {% if p.summary_short %}<p class="project-summary">{{ p.summary_short }}</p>{% endif %}
        {% if p.summary_long %}<p class="project-summary-long">{{ p.summary_long }}</p>{% endif %}

        {% if p.repo_url and p.repo_url != "" %}
          <p class="project-links"><a href="{{ p.repo_url }}">Repository</a></p>
        {% endif %}
      </section>

      {% unless forloop.last %}<hr class="project-divider">{% endunless %}
    {% endfor %}
  </main>
</div>

<script>
  // Highlight active ToC item while scrolling
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
