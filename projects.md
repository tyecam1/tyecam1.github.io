---
layout: page
title: Projects
permalink: /projects/
class: is-projects
---

{% assign projects = site.data.projects %}
{% assign inprogress = projects | where: "status", "current" %}
{% assign past = projects | where: "status", "past" %}
{% assign featured_past = past | where: "featured", true %}
{% assign past_nonfeatured = past | where: "featured", false %}

<div class="projects-page">
  <!-- ================= TOC ================= -->
  <aside class="projects-toc">
    <div class="toc-inner">
      <h2>Contents</h2>
      <ul>
        {% if inprogress and inprogress.size > 0 %}
          <li><a href="#in-progress"><span class="toc-title">In-Progress</span></a></li>
        {% endif %}
        {% for p in featured_past %}
          <li><a href="#{{ p.key }}"><span class="toc-title">{{ p.toc_title | default: p.title }}</span></a></li>
        {% endfor %}
        {% for p in past_nonfeatured %}
          <li><a href="#{{ p.key }}"><span class="toc-title">{{ p.toc_title | default: p.title }}</span></a></li>
        {% endfor %}
      </ul>
    </div>
  </aside>

  <!-- ================= MAIN ================= -->
  <main class="projects-main">

    <!-- ======= In-Progress (single compact panel) ======= -->
    {% if inprogress and inprogress.size > 0 %}
    <section id="in-progress" class="project-section inprogress-section">
      <header class="project-header">
        <div class="title-row">
          <h2 class="project-title">In-Progress</h2>
        </div>
        <p class="project-oneliner">Active builds and planning that directly support my target roles. Concise snapshots; details inside each card.</p>
      </header>

      <div class="ip-grid">
        {% for p in inprogress %}
        <article class="ip-card" id="{{ p.key }}">
          <div class="ip-head">
            <h3 class="ip-title">{{ p.title }}</h3>
            {% if p.role %}
              <div class="ip-role">{{ p.role }}</div>
            {% endif %}
          </div>

          {% if p.one_liner %}
            <p class="ip-one">{{ p.one_liner }}</p>
          {% endif %}

          {% assign show_tags = p.tags | slice: 0, 4 %}
          {% if show_tags and show_tags.size > 0 %}
            <ul class="ip-tags">
              {% for t in show_tags %}<li class="chip">{{ t }}</li>{% endfor %}
              {% if p.tags and p.tags.size > 4 %}<li class="chip chip-more">+{{ p.tags.size | minus:4 }}</li>{% endif %}
            </ul>
          {% endif %}

          {% if p.impact_metrics and p.impact_metrics.size > 0 %}
          <div class="ip-metrics" style="--m: {{ [p.impact_metrics.size, 3] | sort | first }};">
            {% for m in p.impact_metrics limit:3 %}
            <div class="ip-metric">
              <div class="label">{{ m.label }}</div>
              <div class="value">{{ m.value }}</div>
              {% if m.note %}<div class="note">{{ m.note }}</div>{% endif %}
            </div>
            {% endfor %}
          </div>
          {% endif %}

          {% if p.case_study %}
          <details class="ip-details">
            <summary>More details</summary>
            <div class="panel md">
              {% if p.case_study.problem %}<h4>Problem</h4><p>{{ p.case_study.problem }}</p>{% endif %}
              {% if p.case_study.approach %}<h4>Approach</h4><p>{{ p.case_study.approach }}</p>{% endif %}
              {% if p.case_study.results %}<h4>Current state</h4><p>{{ p.case_study.results }}</p>{% endif %}
              {% if p.case_study.next_steps %}<h4>Next steps</h4><p>{{ p.case_study.next_steps }}</p>{% endif %}
            </div>
          </details>
          {% endif %}

          {% assign any_link = p.links.repo | append:p.links.docs | append:p.links.demo | append:p.links.video | append:p.links.paper | append:p.links.dataset %}
          {% if any_link %}
          <div class="project-links ip-links">
            {% if p.links.repo %}<a class="btn-link" href="{{ p.links.repo }}" target="_blank" rel="noopener">Repository</a>{% endif %}
            {% if p.links.docs %}<a class="btn-link" href="{{ p.links.docs }}" target="_blank" rel="noopener">Docs</a>{% endif %}
            {% if p.links.demo %}<a class="btn-link" href="{{ p.links.demo }}" target="_blank" rel="noopener">Demo</a>{% endif %}
            {% if p.links.video %}<a class="btn-link" href="{{ p.links.video }}" target="_blank" rel="noopener">Video</a>{% endif %}
            {% if p.links.paper %}<a class="btn-link" href="{{ p.links.paper }}" target="_blank" rel="noopener">Paper</a>{% endif %}
            {% if p.links.dataset %}<a class="btn-link" href="{{ p.links.dataset }}" target="_blank" rel="noopener">Dataset</a>{% endif %}
          </div>
          {% endif %}
        </article>
        {% endfor %}
      </div>
    </section>
    {% endif %}

    <!-- ======= Featured past projects ======= -->
    {% for p in featured_past %}
      {% include project_full.html project=p %}
    {% endfor %}

    <!-- ======= Other past projects ======= -->
    {% for p in past_nonfeatured %}
      {% include project_full.html project=p %}
    {% endfor %}

  </main>
</div>
