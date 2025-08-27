---
layout: default
title: ""
---

<div class="home">

<section class="home-intro">
  <p class="kicker">Robotics · Control · Applied ML</p>
  <h1>I build dependable, human-centred autonomous systems.</h1>
  <p class="lede">
    First-Class MEng (International), Cardiff University · KAIST exchange.
    I specialise in ROS-based perception & navigation, control design, and rapid
    prototyping from simulation to hardware.
  </p>

  <!-- Skill chips -->
  <ul class="skill-chips" aria-label="Core tools and methods">
    <li class="chip">ROS (Noetic/2)</li>
    <li class="chip">Python</li>
    <li class="chip">C++</li>
    <li class="chip">RTAB-Map</li>
    <li class="chip">RealSense</li>
    <li class="chip">State-space control</li>
    <li class="chip">Digital control</li>
    <li class="chip">MPC</li>
    <li class="chip">PPO</li>
    <li class="chip">Evaluation</li>
    <li class="chip">Reproducible pipelines</li>
  </ul>
</section>

{% assign projects = site.data.projects | where: "featured", true %}

<section class="featured-projects" aria-labelledby="featured-title">
  <h2 id="featured-title">Featured projects</h2>

  {% for p in projects %}
    {%- comment -%}
    Build gallery from any of these keys:
    - Arrays: gallery, images, media, gallery_images, gallery_urls
    - Single image fallbacks: hero, hero_image, hero_img, cover, cover_image
    {%- endcomment -%}
    {% assign gallery = p.gallery | default: p.images | default: p.media | default: p.gallery_images | default: p.gallery_urls %}
    {% assign hero    = p.hero | default: p.hero_image | default: p.hero_img | default: p.cover | default: p.cover_image %}

    {%- if gallery == nil or gallery == empty -%}
      {%- if hero -%}
        {%- assign gallery = hero | split: ',' -%} {# split guarantees an array; no comma -> single-item array #}
      {%- else -%}
        {%- assign gallery = empty -%}
      {%- endif -%}
    {%- endif -%}

    <article class="project-card" id="{{ p.key }}">
      <header class="project-head">
        <h3 class="project-title">
          {% if p.url %}<a href="{{ p.url | relative_url }}">{{ p.title }}</a>{% else %}{{ p.title }}{% endif %}
        </h3>
        {% if p.dates %}
          <div class="project-meta">
            {% if p.dates.start or p.dates.end %}
              <span class="date">
                {{ p.dates.start | default: p.start_date }}{% if p.dates.end or p.end_date %}—{{ p.dates.end | default: p.end_date }}{% endif %}
              </span>
            {% endif %}
            {% if p.stack %}<span class="stack">{{ p.stack | join: " · " }}</span>{% endif %}
          </div>
        {% endif %}
      </header>

      {% if gallery and gallery.size > 0 %}
      <div class="media-wrap">
        <div class="media-scroller snaps-inline" role="group" aria-label="{{ p.toc_title | default: p.title }} image gallery">
          {% for img in gallery %}
            <figure class="media-item">
              <a class="zoom" href="#{{ p.key }}-img-{{ forloop.index }}" title="Enlarge image {{ forloop.index }}">
                <img loading="lazy" src="{{ img | relative_url }}" alt="{{ p.title }} – image {{ forloop.index }}">
              </a>
            </figure>
          {% endfor %}
        </div>
        <div class="scroll-controls" aria-hidden="true">
          <button class="scroll-btn prev" type="button" onclick="this.closest('.project-card').querySelector('.media-scroller').scrollBy({left:-600,behavior:'smooth'})">‹</button>
          <button class="scroll-btn next" type="button" onclick="this.closest('.project-card').querySelector('.media-scroller').scrollBy({left:600,behavior:'smooth'})">›</button>
        </div>
      </div>

      <!-- CSS-only lightbox set -->
      <div class="lightbox-set">
        {% for img in gallery %}
          {% assign i = forloop.index %}
          {% assign l = forloop.length %}
          {% if i > 1 %}{% assign prev = i | minus: 1 %}{% else %}{% assign prev = l %}{% endif %}
          {% if i < l %}{% assign nxt = i | plus: 1 %}{% else %}{% assign nxt = 1 %}{% endif %}

          <div class="lightbox" id="{{ p.key }}-img-{{ i }}">
            <a class="lb-nav prev" href="#{{ p.key }}-img-{{ prev }}" aria-label="Previous">‹</a>
            <img src="{{ img | relative_url }}" alt="{{ p.title }} – enlarged image {{ i }}">
            <a class="lb-nav next" href="#{{ p.key }}-img-{{ nxt }}" aria-label="Next">›</a>
            <a class="lb-close" href="#close" aria-label="Close">×</a>
          </div>
        {% endfor %}
      </div>
      {% endif %}

      {% if p.summary_short %}
        <p class="project-blurb">{{ p.summary_short }}</p>
      {% endif %}
    </article>
  {% endfor %}
</section>

<div id="close" hidden></div>
</div>
