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
{% assign list_past = featured_past | concat: past_nonfeatured %}

<div class="projects-page">
  <!-- ================= TOC ================= -->
  <aside class="projects-toc" aria-label="Projects table of contents">
    <div class="toc-inner">
      <h2>Contents</h2>
      <ul>
        {% if inprogress and inprogress.size > 0 %}
          <li><a id="toc-in-progress" href="#in-progress"><span class="toc-title">In-Progress</span></a></li>
        {% endif %}
        {% for p in featured_past %}
          <li><a id="toc-{{ p.key }}" href="#{{ p.key }}"><span class="toc-title">{{ p.toc_title | default: p.title }}</span></a></li>
        {% endfor %}
        {% for p in past_nonfeatured %}
          <li><a id="toc-{{ p.key }}" href="#{{ p.key }}"><span class="toc-title">{{ p.toc_title | default: p.title }}</span></a></li>
        {% endfor %}
      </ul>
    </div>
  </aside>

  <!-- ================= MAIN ================= -->
  <main class="projects-main">

    <!-- ======= In-Progress (single compact panel) ======= -->
    {% if inprogress and inprogress.size > 0 %}
    <section id="in-progress" class="project-section inprogress-section anchor-target">
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

          {% if p.videos and p.videos.size > 0 %}
          <div class="video-embeds">
            {% for v in p.videos %}
              <div class="video">
                <iframe
                  src="https://www.youtube-nocookie.com/embed/{{ v.id }}"
                  title="{{ v.title | default: 'Project video' }}"
                  loading="lazy" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen>
                </iframe>
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

          {% assign repo    = p.links.repo    | default: '' | strip %}
          {% assign docs    = p.links.docs    | default: '' | strip %}
          {% assign demo    = p.links.demo    | default: '' | strip %}
          {% assign video   = p.links.video   | default: '' | strip %}
          {% assign paper   = p.links.paper   | default: '' | strip %}
          {% assign dataset = p.links.dataset | default: '' | strip %}
          {% if repo != '' or docs != '' or demo != '' or video != '' or paper != '' or dataset != '' %}
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

    <!-- ======= Past projects (featured first) ======= -->
    {% for p in list_past %}
    <section class="project-section anchor-target" id="{{ p.key }}">

      {%- assign has_hero_src = p.media and p.media.hero and p.media.hero.src | default: '' | strip -%}
      {%- if has_hero_src != '' -%}
        <figure class="project-hero">
          <img src="{{ p.media.hero.src }}" alt="{{ p.media.hero.alt | default: p.title }}" onerror="this.closest('figure').remove()">
          {%- if p.media.hero.caption and p.media.hero.caption != '' -%}
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

        {% if p.role or p.domain %}
          <div class="project-roleline">
            {% if p.role %}<span class="role">{{ p.role }}</span>{% endif %}
            {% if p.role and p.domain %}<span class="sep">·</span>{% endif %}
            {% if p.domain %}<span class="domain">{{ p.domain }}</span>{% endif %}
          </div>
        {% endif %}

        {% if p.one_liner or p.summary_short %}
          <p class="project-oneliner">{{ p.one_liner | default: p.summary_short }}</p>
        {% endif %}

        {% if p.stack %}
          {% assign max_stack = 12 %}
          <div class="stack-list" aria-label="Tech stack">
            {% for s in p.stack %}
              {% if s and s != '' %}
                {% if forloop.index <= max_stack %}<span class="stack-item">{{ s }}</span>{% endif %}
              {% endif %}
            {% endfor %}
            {% if p.stack.size > max_stack %}
              <span class="stack-item stack-more">+{{ p.stack.size | minus: max_stack }}</span>
            {% endif %}
          </div>
        {% endif %}
      </header>

      {% if p.impact_metrics and p.impact_metrics.size > 0 %}
      <section class="impact-grid" aria-label="Impact metrics" style="--n: {{ p.impact_metrics.size }}">
        {% for m in p.impact_metrics %}
          {% if m and (m.label or m.value) %}
          <div class="impact-card">
            {% if m.label %}<div class="impact-label">{{ m.label }}</div>{% endif %}
            {% if m.value %}<div class="impact-value">{{ m.value }}</div>{% endif %}
            {% if m.note %}<div class="impact-note">{{ m.note }}</div>{% endif %}
          </div>
          {% endif %}
        {% endfor %}
      </section>
      {% endif %}

      {% if p.summary_short %}<p class="project-summary">{{ p.summary_short }}</p>{% endif %}

      {% if p.videos and p.videos.size > 0 %}
      <div class="video-embeds">
        {% for v in p.videos %}
          <div class="video">
            <iframe
              src="https://www.youtube-nocookie.com/embed/{{ v.id }}"
              title="{{ v.title | default: 'Project video' }}"
              loading="lazy" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen>
            </iframe>
          </div>
        {% endfor %}
      </div>
      {% endif %}

      {% if p.highlights and p.highlights.size > 0 %}
      <section class="highlights">
        <h3>Highlights</h3>
        <ul>
          {% for h in p.highlights %}{% if h and h != '' %}<li>{{ h }}</li>{% endif %}{% endfor %}
        </ul>
      </section>
      {% endif %}

      {% assign cs = p.case_study %}
      {% assign show_tags = p.tags and p.tags.size > 0 %}
      {% if cs and (cs.problem or cs.approach or cs.experiments or cs.results or cs.challenges or cs.learnings or cs.next_steps) or show_tags %}
      <section class="case-study">
        <details>
          <summary>Case study</summary>
          <div class="panel">
            {% if show_tags %}
              {% assign tag_max = 6 %}
              <div class="meta-group">
                <div class="meta-label">Focus areas</div>
                <div class="meta-chips">
                  {% for t in p.tags %}
                    {% if t and t != '' and forloop.index <= tag_max %}<span class="chip">{{ t }}</span>{% endif %}
                  {% endfor %}
                  {% if p.tags.size > tag_max %}<span class="chip">+{{ p.tags.size | minus: tag_max }}</span>
                  {% endif %}
                </div>
              </div>
            {% endif %}

            {% if cs.problem %}<h4>Problem</h4><div class="md">{{ cs.problem | markdownify }}</div>{% endif %}
            {% if cs.approach %}<h4>Approach</h4><div class="md">{{ cs.approach | markdownify }}</div>{% endif %}
            {% if cs.experiments %}<h4>Experiments</h4><div class="md">{{ cs.experiments | markdownify }}</div>{% endif %}
            {% if cs.results %}<h4>Results</h4><div class="md">{{ cs.results | markdownify }}</div>{% endif %}

            {% if cs.challenges %}
              {% assign ch_head = cs.challenges | jsonify | slice: 0,1 %}
              <h4>Key challenges</h4>
              {% if ch_head == '[' %}
                <ul class="md">
                  {% for item in cs.challenges %}
                    {% assign s = item | strip %}{% if s != '' %}<li>{{ s }}</li>{% endif %}
                  {% endfor %}
                </ul>
              {% else %}
                {% assign raw = cs.challenges | strip %}
                {% assign parts = raw | split: ' - ' %}
                {% if parts.size > 2 %}
                  <ul class="md">
                    {% for ptxt in parts %}
                      {% assign s = ptxt | strip %}
                      {% unless forloop.first and s == '' %}{% if s != '' %}<li>{{ s }}</li>{% endif %}{% endunless %}
                    {% endfor %}
                  </ul>
                {% else %}
                  <div class="md">{{ cs.challenges | markdownify }}</div>
                {% endif %}
              {% endif %}
            {% endif %}

            {% if cs.learnings %}
              {% assign le_head = cs.learnings | jsonify | slice: 0,1 %}
              <h4>What I learned</h4>
              {% if le_head == '[' %}
                <ul class="md">
                  {% for item in cs.learnings %}
                    {% assign s = item | strip %}{% if s != '' %}<li>{{ s }}</li>{% endif %}
                  {% endfor %}
                </ul>
              {% else %}
                {% assign raw = cs.learnings | strip %}
                {% assign parts = raw | split: ' - ' %}
                {% if parts.size > 2 %}
                  <ul class="md">
                    {% for ptxt in parts %}
                      {% assign s = ptxt | strip %}
                      {% unless forloop.first and s == '' %}{% if s != '' %}<li>{{ s }}</li>{% endif %}{% endunless %}
                    {% endfor %}
                  </ul>
                {% else %}
                  <div class="md">{{ cs.learnings | markdownify }}</div>
                {% endif %}
              {% endif %}
            {% endif %}

            {% if cs.next_steps %}
              {% assign nx_head = cs.next_steps | jsonify | slice: 0,1 %}
              <h4>Next steps</h4>
              {% if nx_head == '[' %}
                <ul class="md">
                  {% for item in cs.next_steps %}
                    {% assign s = item | strip %}{% if s != '' %}<li>{{ s }}</li>{% endif %}
                  {% endfor %}
                </ul>
              {% else %}
                {% assign raw = cs.next_steps | strip %}
                {% assign parts = raw | split: ' - ' %}
                {% if parts.size > 2 %}
                  <ul class="md">
                    {% for ptxt in parts %}
                      {% assign s = ptxt | strip %}
                      {% unless forloop.first and s == '' %}{% if s != '' %}<li>{{ s }}</li>{% endif %}{% endunless %}
                    {% endfor %}
                  </ul>
                {% else %}
                  <div class="md">{{ cs.next_steps | markdownify }}</div>
                {% endif %}
              {% endif %}
            {% endif %}
          </div>
        </details>
      </section>
      {% endif %}

      {% assign repo    = p.links.repo    | default: '' %}
      {% assign docs    = p.links.docs    | default: '' %}
      {% assign demo    = p.links.demo    | default: '' %}
      {% assign video   = p.links.video   | default: '' %}
      {% assign paper   = p.links.paper   | default: '' %}
      {% assign dataset = p.links.dataset | default: '' %}
      {% if repo != '' or docs != '' or demo != '' or video != '' or paper != '' or dataset != '' %}
      <section class="project-links" aria-label="Project links">
        {% if repo    != '' %}<a class="btn-link" href="{{ repo }}"    target="_blank" rel="noopener">Repository</a>{% endif %}
        {% if docs    != '' %}<a class="btn-link" href="{{ docs }}"    target="_blank" rel="noopener">Docs</a>{% endif %}
        {% if demo    != '' %}<a class="btn-link" href="{{ demo }}"    target="_blank" rel="noopener">Demo</a>{% endif %}
        {% if video   != '' %}<a class="btn-link" href="{{ video }}"   target="_blank" rel="noopener">Video</a>{% endif %}
        {% if paper   != '' %}<a class="btn-link" href="{{ paper }}"   target="_blank" rel="noopener">Paper</a>{% endif %}
        {% if dataset != '' %}<a class="btn-link" href="{{ dataset }}" target="_blank" rel="noopener">Dataset</a>{% endif %}
      </section>
      {% endif %}

      {% if p.media and p.media.gallery and p.media.gallery.size > 0 %}
      <!-- Collapsible gallery with 1–2 column thumbnails -->
      <section class="project-gallery" aria-label="Gallery">
        <details>
          <summary>Image gallery ({{ p.media.gallery | size }})</summary>
          <div class="gallery-grid">
            {% for g in p.media.gallery %}
              {% assign gsrc = g.src | default: '' | strip %}
              {% if gsrc != '' %}
              <a class="gallery-thumb" href="#{{ p.key }}-img-{{ forloop.index }}">
                <img src="{{ g.src }}" alt="{{ g.alt | default: p.title }}" loading="lazy">
              </a>
              {% endif %}
            {% endfor %}
          </div>
        </details>
      </section>

      <!-- Lightbox targets (pure CSS via :target) -->
      {% for g in p.media.gallery %}
        {% assign gsrc = g.src | default: '' | strip %}
        {% if gsrc != '' %}
        <figure class="lightbox" id="{{ p.key }}-img-{{ forloop.index }}">
          <a class="lightbox-backdrop" href="#{{ p.key }}" aria-label="Close"></a>
          <img src="{{ g.src }}" alt="{{ g.alt | default: p.title }}">
          {% if g.caption %}<figcaption>{{ g.caption }}</figcaption>{% endif %}
          <a class="lightbox-close" href="#{{ p.key }}" aria-label="Close">×</a>
        </figure>
        {% endif %}
      {% endfor %}
      {% endif %}

      {% if p.ownership or p.responsibilities or p.team or p.meta.Team %}
      <section class="project-footer">
        <div class="ownership">
          <h4>My Contributions</h4>

          {% assign resp_list = nil %}
          {% if p.responsibilities and p.responsibilities.size > 0 %}
            {% assign resp_list = p.responsibilities %}
          {% elsif p.ownership and (p.ownership.Responsibilities or p.ownership.responsibilities) %}
            {% assign resp_raw = p.ownership.Responsibilities | default: p.ownership.responsibilities %}
            {% if resp_raw contains '["' %}
              {%- assign tmp = resp_raw | replace: '["','' | replace: '"]','' | replace: '", "', '||' -%}
              {% assign resp_list = tmp | split: '||' %}
            {% else %}
              {% assign tmp = resp_raw | newline_to_br | split: '<br />' %}
              {% if tmp.size <= 1 %}
                {% assign tmp = resp_raw | replace: ' • ', '||' | replace: '· ', '||' | replace: '., ', '||' | replace: '; ', '||' | replace: ', ', '||' | split: '||' %}
              {% endif %}
              {% assign resp_list = tmp %}
            {% endif %}
          {% endif %}

          {% if resp_list %}
            <ul>
              {% for item in resp_list %}
                {% assign s = item | strip | remove: '[' | remove: ']' | remove: '"' %}
                {% if s != '' %}<li>{{ s }}</li>{% endif %}
              {% endfor %}
            </ul>
          {% endif %}

          {% assign team_raw = p.team | default: p.ownership.Team | default: p.meta.Team | default: '' %}
          {% if team_raw != '' %}
            <div class="team">
              <span class="label">Team:</span>
              {% if team_raw.first and team_raw.first.name %}
                <ul class="inline-list">
                  {% for m in team_raw %}
                    <li>{% if m.link %}<a href="{{ m.link }}" target="_blank" rel="noopener">{{ m.name }}</a>{% else %}{{ m.name }}{% endif %}{% if m.role %} — {{ m.role }}{% endif %}</li>
                  {% endfor %}
                </ul>
              {% elsif team_raw contains '=>' %}
                {% assign cleaned = team_raw | replace: '{','' | replace:'}','' | replace:'"','' | replace: '=>', ':' %}
                {% assign parts = cleaned | split: ',' %}
                {% assign t_name = '' %}{% assign t_role = '' %}{% assign t_link = '' %}
                {% for part in parts %}
                  {% assign kv = part | strip | split: ':' %}
                  {% assign k = kv[0] | downcase | strip %}
                  {% assign v = kv[1] | join: ':' | strip %}
                  {% if k == 'name' %}{% assign t_name = v %}{% endif %}
                  {% if k == 'role' or k == 'roles' %}{% assign t_role = v %}{% endif %}
                  {% if k == 'link' %}{% assign t_link = v %}{% endif %}
                {% endfor %}
                {% if t_link != '' and t_link != 'nil' %}<a href="{{ t_link }}" target="_blank" rel="noopener">{{ t_name }}</a>{% else %}{{ t_name }}{% endif %}
                {% if t_role != '' and t_role != 'nil' %} — {{ t_role }}{% endif %}
              {% else %}
                {{ team_raw }}
              {% endif %}
            </div>
          {% endif %}
        </div>
      </section>
      {% endif %}
    </section>
    {% endfor %}
  </main>
</div>

<script>
document.body.classList.add('is-projects');

(function setupTOCHighlight() {
  const mq = window.matchMedia('(max-width: 820px)');
  let io = null;

  function enable() {
    const sections = Array.from(document.querySelectorAll('.project-section'));
    const map = new Map(sections.map(s => [s.id, document.getElementById('toc-' + s.id)]));
    io = new IntersectionObserver((entries) => {
      entries.forEach(e => {
        if (e.isIntersecting) {
          map.forEach(a => a && a.classList.remove('active'));
          const a = map.get(e.target.id);
          if (a) a.classList.add('active');
        }
      });
    }, { rootMargin: '-45% 0px -50% 0px', threshold: 0 });
    sections.forEach(s => io.observe(s));
  }

  function disable() {
    if (io) { io.disconnect(); io = null; }
    document.querySelectorAll('.projects-toc a.active').forEach(a => a.classList.remove('active'));
  }

  function apply() { if (mq.matches) disable(); else enable(); }
  mq.addEventListener('change', apply);
  apply();
})();

/* Accordion behaviour for in-progress cards */
(function oneOpenAtATime() {
  const detailsList = Array.from(document.querySelectorAll('.ip-details'));
  detailsList.forEach(d => {
    d.addEventListener('toggle', () => {
      if (!d.open) return;
      detailsList.forEach(other => {
        if (other !== d && other.open) other.open = false;
      });
    });
  });
})();
</script>
