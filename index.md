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
        <h3>Robotics & Control</h3>
        <p>End-to-end autonomy: sensing, SLAM, path planning, and actuation with clear KPIs.</p>
      </article>
      <article class="card">
        <h3>Applied ML</h3>
        <p>RL for behaviour, practical MLOps, fast iteration from baseline to validated results.</p>
      </article>
      <article class="card">
        <h3>Systems Thinking</h3>
        <p>Documentation, safety, and testable interfaces that make teams ship with confidence.</p>
      </article>
    </div>
  </section>

  <!-- ===== FEATURED PROJECTS (brief cards; fuller detail lives on /projects) ===== -->
  <section class="featured-projects">
    <h2>Featured projects</h2>

    {% assign all = site.data.projects %}
    {% assign featured = all | where: "featured", true %}
    {% comment %}
      Keep this intentionally brief—titles, tiny meta line, short summary if available.
      Sorting: prefer end_date, fall back to dates.end, else keep input order.
    {% endcomment %}

    {% assign f_enddate   = featured | where_exp: "p", "p.end_date" | sort: "end_date" | reverse %}
    {% assign f_dates_end = featured | where_exp: "p", "p.dates and p.dates.end" | sort: "dates.end" | reverse %}
    {% assign f_other     = featured | where_exp: "p", "not p.end_date and not (p.dates and p.dates.end)" %}

    {% assign ordered = f_enddate | concat: f_dates_end | concat: f_other %}

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
