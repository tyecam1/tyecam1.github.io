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

    <!-- ======= In-Progress (single consolidated panel) ======= -->
    {% if inprogress and inprogress.size > 0 %}
    <section id="in-progress" class="project-section inprogress-section">
      <header class="project-header">
        <div class="title-row">
          <h2 class="project-title">In-Progress</h2>
        </div>
        <p class="project-oneliner">
          Active builds and planning that directly support my target roles. Concise snapshots; details inside each card.
        </p>
      </header>

      <div class="ip-grid">
        {% for p in inprogress %}
        <article class="ip-card" id="{{ p.key }}">
          <div class="ip-head">
            <h3 class="ip-title">{{ p.title }}</h3>
            {% if p.role %}<div class="ip-role">{{ p.role }}</div>{% endif %}
          </div>

          {% if p.one_liner %}<p class="ip-one">{{ p.one_liner }}</p>{% endif %}

          {% assign show_tags = p.tags | slice: 0, 4 %}
          {% if show_tags and show_tags.size > 0 %}
            <ul class="ip-tags">
              {% for t in show_tags %}<li class="chip">{{ t }}</li>{% endfor %}
              {% if p.tags and p.tags.size > 4 %}<li class="chip chip-more">+{{ p.tags.size | minus:4 }}</li>{% endif %}
            </ul>
          {% endif %}

          {% if p.impact_metrics and p.impact_metrics.size > 0 %}
            {% assign mcount = p.impact_metrics | size %}
            {% if mcount > 3 %}{% assign mcount = 3 %}{% endif %}
            <div class="ip-metrics" style="--m: {{ mcount }};">
              {% for metric in p.impact_metrics limit:3 %}
              <div class="ip-metric">
                <div class="label">{{ metric.label }}</div>
                <div class="value">{{ metric.value }}</div>
                {% if metric.note %}<div class="note">{{ metric.note }}</div>{% endif %}
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

          {%- comment -%} Links: render only if non-blank {%- endcomment -%}
          {% assign repo    = p.links.repo    | default: '' | strip %}
          {% assign docs    = p.links.docs    | default: '' | strip %}
          {% assign demo    = p.links.demo    | default: '' | strip %}
          {% assign video   = p.links.video   | default: '' | strip %}
          {% assign paper   = p.links.paper   | default: '' | strip %}
          {% assign dataset = p.links.dataset | default: '' | strip %}
          {% assign has_links = false %}
          {% if repo != '' or docs != '' or demo != '' or video != '' or paper != '' or dataset != '' %}
            {% assign has_links = true %}
          {% endif %}

          {% if has_links %}
          <div class="project-links ip-links">
            {% if repo    != '' %}<a class="btn-link" href="{{ repo }}"    target="_blank" rel="noopener">Repository</a>{% endif %}
            {% if docs    != '' %}<a class="btn-link" href="{{ docs }}"    target="_blank" rel="noopener">Docs</a>{% endif %}
            {% if demo    != '' %}<a class="btn-link" href="{{ demo }}"    target="_blank" rel="noopener">Demo</a>{% endif %}
            {% if video   != '' %}<a class="btn-link" href="{{ video }}"   target="_blank" rel="noopener">Video</a>{% endif %}
            {% if paper   != '' %}<a class="btn-link" href="{{ paper }}"   target="_blank" rel="noopener">Paper</a>{% endif %}
            {% if dataset != '' %}<a class="btn-link" href="{{ dataset }}" target="_blank" rel="noopener">Dataset</a>{% endif %}
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
