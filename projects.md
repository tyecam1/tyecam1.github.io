---
layout: page
title: Projects
permalink: /projects/
---

{% comment %}
This page renders projects from _data/projects.yml.
It expects (per project):
- key (anchor id), title, status ("current"|"past"), dates: { start, end }
- one_liner, summary_short, role, domain
- stack: [ ... ], tags: [ ... ]
- links: { repo, docs, demo, video, paper, dataset }
- media: { hero: { src, alt, caption }, gallery: [ { src, alt, caption } ] }
- highlights: [ ... ]
- impact_metrics: [ { label, value, note } ]
- ownership, meta (optional dicts)
- case_study: { problem, approach, experiments, results, challenges, learnings, next_steps }
{% endcomment %}

{% assign current = site.data.projects | where: "status", "current" | sort: "dates.start" | reverse %}
{% assign past    = site.data.projects | where: "status", "past"    | sort: "dates.end"   | reverse %}
{% assign projects = current | concat: past %}

<div class="projects-page">
  <aside class="projects-toc" aria-label="Projects table of contents">
    <div class="toc-inner">
      <h2>Contents</h2>
      <ul>
        {% for p in projects %}
          <li>
            <a id="toc-{{ p.key }}" href="#{{ p.key }}">
              <span class="toc-title">{{ p.toc_title | default: p.title }}</span>
              {% if p.status == "current" %}<span class="toc-badge">Current</span>{% endif %}
            </a>
          </li>
        {% endfor %}
      </ul>
    </div>
  </aside>

  <main class="projects-main">
    {% for p in projects %}
    <section class="project-section" id="{{ p.key }}">

      {%- assign has_hero = p.media and p.media.hero and p.media.hero.src -%}
      {%- if has_hero -%}
        <figure class="project-hero">
          <img src="{{ p.media.hero.src }}" alt="{{ p.media.hero.alt | default: p.title }}">
          {%- if p.media.hero.caption -%}
            <figcaption>{{ p.media.hero.caption }}</figcaption>
          {%- endif -%}
        </figure>
      {%- endif -%}

      <header class="project-header">
        <div class="title-row">
          <h2 class="project-title">{{ p.title }}</h2>
          <div class="project-dates">
            {%- if p.status == "current" and p.dates and p.dates.start -%}
              In progress — since {{ p.dates.start | date: "%b %Y" }}
            {%- elsif p.dates and p.dates.start and p.dates.end -%}
              {{ p.dates.start | date: "%b %Y" }} – {{ p.dates.end | date: "%b %Y" }}
            {%- endif -%}
          </div>
        </div>

        <p class="project-oneliner">{{ p.one_liner | default: p.summary_short }}</p>

        <div class="project-meta">
          {% if p.role %}<span class="chip" title="Role">{{ p.role }}</span>{% endif %}
          {% if p.domain %}<span class="chip" title="Domain">{{ p.domain }}</span>{% endif %}
          {% if p.tags %}
            {% for t in p.tags %}<span class="chip chip--muted">{{ t }}</span>{% endfor %}
          {% endif %}
        </div>

        {% if p.stack %}
          <div class="stack-list" aria-label="Tech stack">
            {% for s in p.stack %}<span class="stack-item">{{ s }}</span>{% endfor %}
          </div>
        {% endif %}
      </header>

      {% if p.impact_metrics and p.impact_metrics.size > 0 %}
      <section class="impact-grid" aria-label="Impact metrics">
        {% for m in p.impact_metrics %}
          <div class="impact-card">
            <div class="impact-label">{{ m.label }}</div>
            <div class="impact-value">{{ m.value }}</div>
            {% if m.note %}<div class="impact-note">{{ m.note }}</div>{% endif %}
          </div>
        {% endfor %}
      </section>
      {% endif %}

      {% if p.summary_short %}
        <p class="project-summary">{{ p.summary_short }}</p>
      {% endif %}

      {% if p.highlights and p.highlights.size > 0 %}
      <section class="highlights">
        <h3>Highlights</h3>
        <ul>
          {% for h in p.highlights %}<li>{{ h }}</li>{% endfor %}
        </ul>
      </section>
      {% endif %}

      {% assign cs = p.case_study %}
      {% if cs and (cs.problem or cs.approach or cs.experiments or cs.results or cs.challenges or cs.learnings or cs.next_steps) %}
      <section class="case-study">
        <details open>
          <summary>Case study</summary>
          {% if cs.problem %}
            <h4>Problem</h4>
            <p>{{ cs.problem }}</p>
          {% endif %}
          {% if cs.approach %}
            <h4>Approach</h4>
            <p>{{ cs.approach }}</p>
          {% endif %}
          {% if cs.experiments %}
            <h4>Experiments</h4>
            <p>{{ cs.experiments }}</p>
          {% endif %}
          {% if cs.results %}
            <h4>Results</h4>
            <p>{{ cs.results }}</p>
          {% endif %}
          {% if cs.challenges %}
            <h4>Key challenges</h4>
            <p>{{ cs.challenges }}</p>
          {% endif %}
          {% if cs.learnings %}
            <h4>What I learned</h4>
            <p>{{ cs.learnings }}</p>
          {% endif %}
          {% if cs.next_steps %}
            <h4>Next steps</h4>
            <p>{{ cs.next_steps }}</p>
          {% endif %}
        </details>
      </section>
      {% endif %}

      {% if p.links and (p.links.repo or p.links.docs or p.links.demo or p.links.video or p.links.paper or p.links.dataset) %}
      <section class="project-links" aria-label="Project links">
        {% if p.links.repo %}<a class="btn-link" href="{{ p.links.repo }}" target="_blank" rel="noopener">Repository</a>{% endif %}
        {% if p.links.docs %}<a class="btn-link" href="{{ p.links.docs }}" target="_blank" rel="noopener">Docs</a>{% endif %}
        {% if p.links.demo %}<a class="btn-link" href="{{ p.links.demo }}" target="_blank" rel="noopener">Demo</a>{% endif %}
        {% if p.links.video %}<a class="btn-link" href="{{ p.links.video }}" target="_blank" rel="noopener">Video</a>{% endif %}
        {% if p.links.paper %}<a class="btn-link" href="{{ p.links.paper }}" target="_blank" rel="noopener">Paper</a>{% endif %}
        {% if p.links.dataset %}<a class="btn-link" href="{{ p.links.dataset }}" target="_blank" rel="noopener">Dataset</a>{% endif %}
      </section>
      {% endif %}

      {% if p.media and p.media.gallery and p.media.gallery.size > 0 %}
      <section class="project-gallery" aria-label="Gallery">
        {% for g in p.media.gallery %}
          <figure>
            <img src="{{ g.src }}" alt="{{ g.alt | default: p.title }}">
            {% if g.caption %}<figcaption>{{ g.caption }}</figcaption>{% endif %}
          </figure>
        {% endfor %}
      </section>
      {% endif %}

      {% if p.ownership or p.meta %}
      <section class="project-footer">
        {% if p.ownership %}
          <div class="ownership">
            {% for k in p.ownership %}
              <div><span class="label">{{ k[0] | replace: '_',' ' | capitalize }}:</span> <span>{{ k[1] }}</span></div>
            {% endfor %}
          </div>
        {% endif %}
        {% if p.meta %}
          <div class="meta">
            {% for k in p.meta %}
              <div><span class="label">{{ k[0] | replace: '_',' ' | capitalize }}:</span> <span>{{ k[1] }}</span></div>
            {% endfor %}
          </div>
        {% endif %}
      </section>
      {% endif %}

    </section>
    {% endfor %}
  </main>
</div>

<script>
// Sticky TOC active-state on scroll
(function() {
  const sections = Array.from(document.querySelectorAll('.project-section'));
  const map = new Map(sections.map(s => [s.id, document.getElementById('toc-' + s.id)]));
  const io = new IntersectionObserver((entries) => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        map.forEach(a => a && a.classList.remove('active'));
        const a = map.get(e.target.id);
        if (a) a.classList.add('active');
      }
    });
  }, { rootMargin: '-45% 0px -50% 0px', threshold: 0 });
  sections.forEach(s => io.observe(s));
})();
</script>
