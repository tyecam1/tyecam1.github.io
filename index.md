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

  <!-- NEW: grid wrapper so CSS can place two columns consistently -->
  <div class="projects-grid">
  {% for p in projects %}

    {%- comment -%}
    Build gallery_items as an array of maps: [{src, alt, caption}]
    Supports:
    - p.media.hero.src (+ optional .alt/.caption)
    - p.media.gallery[].src (+ optional .alt/.caption)
    - p.gallery / p.images (array of strings)
    - p.hero / p.cover (single string)
    Hero is prepended; duplicates removed.
    {%- endcomment -%}

    {%- assign gallery_items = "" | split: "" -%}
    {%- assign hero_src = nil -%}
    {%- assign hero_alt = nil -%}
    {%- assign hero_caption = nil -%}

    {%- if p.media and p.media.hero and p.media.hero.src -%}
      {%- assign hero_src = p.media.hero.src -%}
      {%- assign hero_alt = p.media.hero.alt | default: p.title -%}
      {%- assign hero_caption = p.media.hero.caption -%}
    {%- elsif p.hero or p.hero_image or p.cover or p.cover_image -%}
      {%- assign hero_src = p.hero | default: p.hero_image | default: p.cover | default: p.cover_image -%}
      {%- assign hero_alt = p.title -%}
    {%- endif -%}

    {%- if p.media and p.media.gallery -%}
      {%- for g in p.media.gallery -%}
        {%- if g.src -%}
          {%- assign item = ("" | split:"") | push:"" | last -%}
          {%- assign item = item | merge: {"src": g.src, "alt": g.alt | default: p.title, "caption": g.caption} -%}
          {%- assign gallery_items = gallery_items | push: item -%}
        {%- endif -%}
      {%- endfor -%}
    {%- endif -%}

    {%- if p.gallery or p.images or p.media_urls or p.gallery_urls -%}
      {%- assign raw = p.gallery | default: p.images | default: p.media_urls | default: p.gallery_urls -%}
      {%- for g in raw -%}
        {%- assign item = ("" | split:"") | push:"" | last -%}
        {%- assign item = item | merge: {"src": g, "alt": p.title} -%}
        {%- assign gallery_items = gallery_items | push: item -%}
      {%- endfor -%}
    {%- endif -%}

    {%- if hero_src -%}
      {%- assign already = false -%}
      {%- for it in gallery_items -%}
        {%- if it.src == hero_src -%}{%- assign already = true -%}{%- endif -%}
      {%- endfor -%}
      {%- unless already -%}
        {%- assign hero_item = ("" | split:"") | push:"" | last -%}
        {%- assign hero_item = hero_item | merge: {"src": hero_src, "alt": hero_alt, "caption": hero_caption} -%}
        {%- assign gallery_items = gallery_items | unshift: hero_item -%}
      {%- endunless -%}
    {%- endif -%}

    {%- if gallery_items == empty and hero_src -%}
      {%- assign hero_item = ("" | split:"") | push:"" | last -%}
      {%- assign hero_item = hero_item | merge: {"src": hero_src, "alt": hero_alt} -%}
      {%- assign gallery_items = gallery_items | push: hero_item -%}
    {%- endif -%}

    <article class="project-card" id="{{ p.key }}">
      <header class="project-head">
        <h3 class="project-title">
          {% if p.url %}<a href="{{ p.url | relative_url }}">{{ p.title }}</a>{% else %}{{ p.title }}{% endif %}
        </h3>
        <div class="project-meta">
          {% if p.dates and (p.dates.start or p.dates.end) %}
            <span class="date">
              {{ p.dates.start | default: p.start_date }}{% if p.dates.end or p.end_date %}—{{ p.dates.end | default: p.end_date }}{% endif %}
            </span>
          {% endif %}
          {% if p.stack %}<span class="stack">{{ p.stack | join: " · " }}</span>{% endif %}
        </div>
      </header>

      {% if gallery_items and gallery_items.size > 0 %}
      <div class="media-wrap">
        <div class="media-scroller snaps-inline" role="group" aria-label="{{ p.toc_title | default: p.title }} image gallery">
          {% for img in gallery_items %}
            <figure class="media-item">
              <a class="zoom" href="#{{ p.key }}-img-{{ forloop.index }}" title="Enlarge image {{ forloop.index }}">
                <img {% if forloop.first %}loading="eager" fetchpriority="high"{% else %}loading="lazy"{% endif %}
                     src="{{ img.src | relative_url }}"
                     alt="{{ img.alt | default: p.title | escape }}">
              </a>
            </figure>
          {% endfor %}
        </div>

        {% if gallery_items.size > 1 %}
        <div class="scroll-controls" aria-hidden="true">
          <button class="scroll-btn prev" type="button" onclick="this.closest('.project-card').querySelector('.media-scroller').scrollBy({left:-600,behavior:'smooth'})">‹</button>
          <button class="scroll-btn next" type="button" onclick="this.closest('.project-card').querySelector('.media-scroller').scrollBy({left:600,behavior:'smooth'})">›</button>
        </div>
        {% endif %}
      </div>

      <!-- Lightbox with click-anywhere-to-close backdrop + captions -->
      <div class="lightbox-set">
        {% for img in gallery_items %}
          {% assign i = forloop.index %}{% assign l = forloop.length %}
          {% if i > 1 %}{% assign prev = i | minus: 1 %}{% else %}{% assign prev = l %}{% endif %}
          {% if i < l %}{% assign nxt = i | plus: 1 %}{% else %}{% assign nxt = 1 %}{% endif %}
          <div class="lightbox" id="{{ p.key }}-img-{{ i }}">
            <a class="lb-backdrop" href="#close" aria-label="Close"></a>
            <a class="lb-nav prev" href="#{{ p.key }}-img-{{ prev }}" aria-label="Previous">‹</a>
            <figure class="lb-media">
              <img src="{{ img.src | relative_url }}" alt="{{ img.alt | default: p.title | escape }}">
              {% if img.caption %}<figcaption class="lb-caption">{{ img.caption }}</figcaption>{% endif %}
            </figure>
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
  </div><!-- /.projects-grid -->
</section>

<div id="close" hidden></div>
</div>
