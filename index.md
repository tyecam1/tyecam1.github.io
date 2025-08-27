---
layout: page
title: Home
permalink: /
class: is-home
---

<div class="home">

  <!-- ===== HERO ===== -->
  <section class="hero">
    <p class="kicker">Robotics · Control · Applied ML</p>
    <h1 class="headline">
      I build dependable, human-centred autonomous systems.
    </h1>
    <p class="subhead">
      First-Class MEng (International), Cardiff University · KAIST exchange.
      I specialise in ROS-based perception & navigation, control design, and
      rapid prototyping from simulation to hardware.
    </p>

    <ul class="hero-highlights">
      <li>ROS (Noetic/2), Python &amp; C++ · RTAB-Map · RealSense</li>
      <li>Control: state-space, digital control, MPC</li>
      <li>RL &amp; simulation: PPO, evaluation, reproducible pipelines</li>
    </ul>
  </section>

  <!-- ===== VALUE CARDS ===== -->
  <section class="value">
    <div class="value-grid">
      <article class="card">
        <h3>Robotics &amp; Control</h3>
        <p>End-to-end autonomy: sensing, SLAM, path planning, and actuation with clear KPIs.</p>
      </article>
      <article class="card">
        <h3>Applied ML</h3>
        <p>RL for behaviour, practical MLOps, fast iteration from baseline to validated results.</p>
      </article>
      <article class="card">
        <h3>Systems Thinking</h3>
        <p>Documentation, safety, and testable interfaces that help teams ship with confidence.</p>
      </article>
    </div>
  </section>

  <!-- ===== FEATURED PROJECTS (brief cards; full detail lives on /projects) ===== -->
  <section class="featured-projects">
    <h2>Featured projects</h2>

    {% assign featured = site.data.projects | where: "featured", true %}
    {%- comment -%}
      Sort by explicit end_date if present; otherwise by title as a stable fallback.
      (Avoids unsupported where_exp / complex expressions on GitHub Pages.)
    {%- endcomment -%}
    {% assign with_end = featured | where: "end_date" %}
    {% assign without_end = featured | where_exp: "x", "x.end_date == nil" %}{% comment %}Liquid on gh-pages doesn’t support where_exp; replace with manual loop below.{% endcomment %}

    {%- assign without_end = "" | split: "" -%}
    {%- for p in featured -%}
      {%- unless p.end_date -%}
        {%- assign without_end = without_end | push: p -%}
      {%- endunless -%}
    {%- endfor -%}

    {% assign ordered = with_end | sort: "end_date" | reverse | concat: (without_end | sort: "title") %}

    <div class="projects-grid">
      {% for p in ordered limit:3 %}
        {% assign start = p.start_date | default: p.dates.start %}
        {% assign end   = p.end_date   | default: p.dates.end   %}
        <article class="project-card" id="proj-{{ p.key }}">
          <h3 class="project-title">{{ p.toc_title | default: p.title }}</h3>
          <p class="project-meta">
            {% if p.status == "current" %}<span class="badge">Current</span>{% endif %}
            {% if start or end %}
              <span class="dates">
                {% if start %}{{ start }}{% endif %}{% if end %}–{{ end }}{% endif %}
              </span>
            {% endif %}
            {% if p.stack %}<span class="stack">{{ p.stack | join: " · " | truncate: 90 }}</span>{% endif %}
          </p>
          {% if p.summary_short %}
            <p class="project-summary">{{ p.summary_short | strip }}</p>
          {% endif %}
        </article>
      {% endfor %}
    </div>

    <div class="projects-cta">
      <a class="button" href="/projects/">See all projects →</a>
    </div>
  </section>

</div>
