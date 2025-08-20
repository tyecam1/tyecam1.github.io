---
layout: page
title: Projects
permalink: /projects/
---

{% assign current = site.data.projects | where: "status", "current" | sort: "dates.start" | reverse %}
{% assign past    = site.data.projects | where: "status", "past"    | sort: "dates.end"   | reverse %}
{% assign projects = current | concat: past %}

<div class="projects-layout">
  <aside class="toc">
    <nav aria-label="Projects table of contents">
      <ul>
        {% for p in projects %}
          <li><a id="toc-{{ p.key }}" href="#{{ p.key }}">{{ p.toc_title | default: p.title }}</a></li>
        {% endfor %}
      </ul>
    </nav>
  </aside>

  <main class="projects-main">
    {% for p in projects %}
      <section class="project-section anchor-target" id="{{ p.key }}">
        <header class="project-header">
          <h2>{{ p.title }}</h2>
          <div class="project-meta">
            <span>{{ p.role }}</span> · <span>{{ p.domain }}</span>
          </div>
          {% if p.stack %}
            <div class="project-stack">{{ p.stack | join: " · " }}</div>
          {% endif %}
        </header>

        {% if p.media.hero.src %}
          <figure class="project-media">
            <img class="project-hero" src="{{ p.media.hero.src }}" alt="{{ p.media.hero.alt }}">
            {% if p.media.hero.caption %}
              <figcaption>{{ p.media.hero.caption }}</figcaption>
            {% endif %}
          </figure>
        {% endif %}

        <div class="project-body">
          <h3>Overview</h3>
          <p>{{ p.one_liner }}</p>

          {% if p.highlights %}
            <ul class="project-highlights">
              {% for h in p.highlights %}
                <li>{{ h }}</li>
              {% endfor %}
            </ul>
          {% endif %}

          {% if p.impact_metrics %}
            <div class="impact-metrics">
              {% for m in p.impact_metrics %}
                <div class="metric">
                  <strong>{{ m.value }}</strong>
                  <span>{{ m.label }}</span>
                  {% if m.note %}<small>{{ m.note }}</small>{% endif %}
                </div>
              {% endfor %}
            </div>
          {% endif %}

          {% if p.case_study %}
            <details><summary>Read full case study</summary>
              {% for sec in "problem,approach,experiments,results,challenges,learnings,next_steps" | split: "," %}
                {% if p.case_study[sec] %}
                  <h3>{{ sec | capitalize }}</h3>
                  <div>{{ p.case_study[sec] | markdownify }}</div>
                {% endif %}
              {% endfor %}
            </details>
          {% endif %}

          {% if p.links %}
            <div class="project-links">
              {% if p.links.repo %}<a href="{{ p.links.repo }}">💻 Repo</a>{% endif %}
              {% if p.links.demo %}<a href="{{ p.links.demo }}">🔗 Demo</a>{% endif %}
              {% if p.links.video %}<a href="{{ p.links.video }}">▶️ Video</a>{% endif %}
              {% if p.links.paper %}<a href="{{ p.links.paper }}">📄 Paper</a>{% endif %}
              {% if p.links.docs %}<a href="{{ p.links.docs }}">📑 Docs</a>{% endif %}
              {% if p.links.dataset %}<a href="{{ p.links.dataset }}">📊 Dataset</a>{% endif %}
            </div>
          {% endif %}
        </div>

        {% if p.media.gallery %}
          <div class="gallery-grid">
            {% for g in p.media.gallery %}
              <figure>
                <img src="{{ g.src }}" alt="{{ g.alt }}">
                {% if g.caption %}<figcaption>{{ g.caption }}</figcaption>{% endif %}
              </figure>
            {% endfor %}
          </div>
        {% endif %}

        {% if p.ownership %}
          <div class="project-ownership">
            <h3>My Contributions</h3>
            <ul>{% for r in p.ownership.responsibilities %}<li>{{ r }}</li>{% endfor %}</ul>
            {% if p.ownership.team %}
              <h4>Team</h4>
              <ul>{% for t in p.ownership.team %}<li>{{ t.name }} — {{ t.role }}</li>{% endfor %}</ul>
            {% endif %}
          </div>
        {% endif %}
      </section>

      {% unless forloop.last %}<hr>{% endunless %}
    {% endfor %}
  </main>
</div>
