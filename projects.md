---
layout: page
title: Projects
permalink: /projects/
---

{% comment %}
Order:
1) CURRENT projects by start_date (newest → oldest)
2) PAST projects by end_date (newest → oldest)
Dates in _data/projects.yml must be ISO strings: "YYYY-MM-DD".

YAML supported per project:
- key, title, toc_title, status ("current"|"past"), start_date, end_date
- stack: [ ... ]
- tags: [ ... ]
- image, media_caption
- summary_short
- summary_long (fallback if no case_study)
- case_study: { background, methods, experiments, results, limitations, future_work }
- repo_url, demo_url, video_url, paper_url, docs_url
- gallery: [ "/assets/img/...", ... ]
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

          {% if p.tags %}
            <div class="project-tags">
              {% for t in p.tags %}
                <span class="tag-chip">{{ t }}</span>
              {% endfor %}
            </div>
          {% endif %}
        </header>

        <div class="project-body">
          {% assign img = p.image | to_s | strip %}
          {% if img != "" %}
            <figure class="project-media">
              <img class="project-hero" src="{{ img }}" alt="{{ p.title }}">
              {% if p.media_caption %}
                <figcaption class="project-caption">{{ p.media_caption }}</figcaption>
              {% endif %}
            </figure>
          {% endif %}

          <div class="project-text">
            {% if p.summary_short %}
              <h3 class="project-subhead">Overview</h3>
              <p class="project-summary">{{ p.summary_short }}</p>
            {% endif %}

            {% if p.case_study %}
              {% assign cs = p.case_study %}

              {% if cs.background %}
                <h3 class="project-subhead">Background</h3>
                <div class="project-summary-long">{{ cs.background | markdownify }}</div>
              {% endif %}

              {% if cs.methods %}
                <h3 class="project-subhead">Methods</h3>
                <div class="project-summary-long">{{ cs.methods | markdownify }}</div>
              {% endif %}

              {% if cs.experiments %}
                <h3 class="project-subhead">Experiments</h3>
                <div class="project-summary-long">{{ cs.experiments | markdownify }}</div>
              {% endif %}

              {% if cs.results %}
                <h3 class="project-subhead">Results</h3>
                <div class="project-summary-long">{{ cs.results | markdownify }}</div>
              {% endif %}

              {% if cs.limitations %}
                <h3 class="project-subhead">Limitations</h3>
                <div class="project-summary-long">{{ cs.limitations | markdownify }}</div>
              {% endif %}

              {% if cs.future_work %}
                <h3 class="project-subhead">Future Work</h3>
                <div class="project-summary-long">{{ cs.future_work | markdownify }}</div>
              {% endif %}

            {% elsif p.summary_long %}
              <h3 class="project-subhead">Details</h3>
              <div class="project-summary-long">{{ p.summary_long }}</div>
            {% endif %}

            {% assign links_present = false %}
            {% if p.repo_url %}{% assign links_present = true %}{% endif %}
            {% if p.demo_url %}{% assign links_present = true %}{% endif %}
            {% if p.video_url %}{% assign links_present = true %}{% endif %}
            {% if p.paper_url %}{% assign links_present = true %}{% endif %}
            {% if p.docs_url %}{% assign links_present = true %}{% endif %}

            {% if links_present %}
              <div class="project-cta">
                {% if p.repo_url %}<a class="btn" href="{{ p.repo_url }}">Repository</a>{% endif %}
                {% if p.demo_url %}<a class="btn" href="{{ p.demo_url }}">Demo</a>{% endif %}
                {% if p.video_url %}<a class="btn" href="{{ p.video_url }}">Video</a>{% endif %}
                {% if p.paper_url %}<a class="btn" href="{{ p.paper_url }}">Paper</a>{% endif %}
                {% if p.docs_url %}<a class="btn" href="{{ p.docs_url }}">Docs</a>{% endif %}
              </div>
            {% endif %}
          </div>
        </div>

        {% if p.gallery %}
          <div class="project-gallery">
            {% for g in p.gallery %}
              {% assign gsrc = g | to_s | strip %}
              {% if gsrc != "" %}
                <img src="{{ gsrc }}" alt="{{ p.title }} gallery image {{ forloop.index }}">
              {% endif %}
            {% endfor %}
          </div>
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
