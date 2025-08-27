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

<section class="featured-projects hf" aria-labelledby="featured-title">
  <h2 id="featured-title">Featured projects</h2>

  <div class="hf-grid">
  {% for p in projects %}

    {%- comment -%}
    Build a pipe-delimited list of image srcs (GitHub Pages–safe).
    Supports:
      - p.media.hero.src and p.media.gallery[].src
      - p.hero / p.cover (string)
      - p.gallery / p.images (array of strings)
    Puts hero first and de-dupes.
    {%- endcomment -%}

    {%- assign gallery_pipe = '|' -%}

    {%- assign hero_src = nil -%}
    {%- if p.media and p.media.hero and p.media.hero.src -%}
      {%- assign hero_src = p.media.hero.src -%}
    {%- elsif p.hero or p.hero_image or p.cover or p.cover_image -%}
      {%- assign hero_src = p.hero | default: p.hero_image | default: p.cover | default: p.cover_image -%}
    {%- endif -%}

    {%- if hero_src -%}
      {%- capture probe %}|{{ hero_src }}|{% endcapture -%}
      {%- unless gallery_pipe contains probe -%}
        {%- assign gallery_pipe = gallery_pipe | append: hero_src | append: '|' -%}
      {%- endunless -%}
    {%- endif -%}

    {%- if p.media and p.media.gallery -%}
      {%- for g in p.media.gallery -%}
        {%- if g.src -%}
          {%- capture s %}|{{ g.src }}|{% endcapture -%}
          {%- unless gallery_pipe contains s -%}
            {%- assign gallery_pipe = gallery_pipe | append: g.src | append: '|' -%}
          {%- endunless -%}
        {%- endif -%}
      {%- endfor -%}
    {%- endif -%}

    {%- if p.gallery or p.images -%}
      {%- assign raw = p.gallery | default: p.images -%}
      {%- for g in raw -%}
        {%- capture s %}|{{ g }}|{% endcapture -%}
        {%- unless gallery_pipe contains s -%}
          {%- assign gallery_pipe = gallery_pipe | append: g | append: '|' -%}
        {%- endunless -%}
      {%- endfor -%}
    {%- endif -%}

    {%- assign gallery = gallery_pipe | split: '|' -%}

    <article class="hf-card" id="{{ p.key }}">
      <header class="hf-head">
        <h3 class="hf-title">
          {% if p.url %}<a href="{{ p.url | relative_url }}">{{ p.title }}</a>{% else %}{{ p.title }}{% endif %}
        </h3>
        <div class="hf-meta">
          {% if p.dates and (p.dates.start or p.dates.end) %}
            <span class="date">
              {{ p.dates.start | default: p.start_date }}{% if p.dates.end or p.end_date %}—{{ p.dates.end | default: p.end_date }}{% endif %}
            </span>
          {% endif %}
          {% if p.stack %}<span class="stack">{{ p.stack | join: " · " }}</span>{% endif %}
        </div>
      </header>

      {% assign gcount = 0 %}
      {% for img in gallery %}{% if img != '' %}{% assign gcount = gcount | plus: 1 %}{% endif %}{% endfor %}

      {% if gcount > 0 %}
      <div class="hf-media-wrap">
        <div class="hf-scroller snaps-inline" role="group" aria-label="{{ p.toc_title | default: p.title }} image gallery">
          {% assign idx = 0 %}
          {% for img in gallery %}
            {% unless img == '' %}
              {% assign idx = idx | plus: 1 %}
              <figure class="hf-item">
                <a class="hf-zoom" href="#{{ p.key }}-img-{{ idx }}" title="Enlarge image {{ idx }}">
                  <img {% if idx == 1 %}loading="eager" fetchpriority="high"{% else %}loading="lazy"{% endif %}
                       src="{{ img | relative_url }}"
                       alt="{{ p.title | escape }} — image {{ idx }}">
                </a>
              </figure>
            {% endunless %}
          {% endfor %}
        </div>

        {% if gcount > 1 %}
        <div class="hf-controls" aria-hidden="true">
          <button class="hf-btn prev" type="button"
            onclick="var s=this.closest('.hf-card').querySelector('.hf-scroller'); s.scrollBy({left:-s.clientWidth,behavior:'smooth'})">‹</button>
          <button class="hf-btn next" type="button"
            onclick="var s=this.closest('.hf-card').querySelector('.hf-scroller'); s.scrollBy({left:s.clientWidth,behavior:'smooth'})">›</button>
        </div>
        {% endif %}
      </div>

      <div class="hf-lightbox-set">
        {% assign idx = 0 %}
        {% for img in gallery %}
          {% unless img == '' %}
            {% assign idx = idx | plus: 1 %}
            {% assign l = gcount %}
            {% if idx > 1 %}{% assign prev = idx | minus: 1 %}{% else %}{% assign prev = l %}{% endif %}
            {% if idx < l %}{% assign nxt = idx | plus: 1 %}{% else %}{% assign nxt = 1 %}{% endif %}
            <div class="hf-lightbox" id="{{ p.key }}-img-{{ idx }}">
              <a class="hf-backdrop" href="#close" aria-label="Close"></a>
              <a class="hf-nav prev" href="#{{ p.key }}-img-{{ prev }}" aria-label="Previous">‹</a>
              <figure class="hf-fig">
                <img src="{{ img | relative_url }}" alt="{{ p.title | escape }} — enlarged image {{ idx }}">
              </figure>
              <a class="hf-nav next" href="#{{ p.key }}-img-{{ nxt }}" aria-label="Next">›</a>
              <a class="hf-close" href="#close" aria-label="Close">×</a>
            </div>
          {% endunless %}
        {% endfor %}
      </div>
      {% endif %}

      {% if p.summary_short %}
        <p class="hf-blurb">{{ p.summary_short }}</p>
      {% endif %}
    </article>

  {% endfor %}
  </div><!-- /.hf-grid -->
</section>

<div id="close" hidden></div>
</div>
