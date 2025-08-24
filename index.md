---
layout: page
title: Home
permalink: /
class: is-home
---

<div class="hero">
  <h1>Tye Cameron-Robson</h1>
  <p>Systems engineer building reliable robotics & RL tooling: ROS, control, perception, and experiment infrastructure.</p>
  <p class="hero-ctas">
    <a class="btn" href="{{ '/projects/' | relative_url }}">View Projects</a>
    <a class="btn btn-ghost" href="{{ '/about/' | relative_url }}">About</a>
    {% if site.cv_url %}<a class="btn btn-ghost" href="{{ site.cv_url }}">CV</a>{% endif %}
  </p>
</div>

## What I’m focusing on now
- Integrated RL simulation + **live telemetry** for reproducible runs.
- **Arch Linux** dev environment automation (CUDA, Docker, Ansible).
- **Assistive navigation** research planning (safe RL, intent estimation).

## Skills snapshot
ROS • Python • C++ • RL (PPO/IL) • Control • SLAM/VSLAM • Perception (RGB-D/LiDAR) • Docker/CUDA • Linux/Ansible • MATLAB

## Featured projects
{% assign all = site.data.projects %}
{% assign current = all | where: "status", "current" %}
{% assign past    = all | where: "status", "past" %}
{% assign feat_c  = current | where: "featured", true %}
{% assign feat_p  = past    | where: "featured", true %}
{% assign featured = feat_c | concat: feat_p | slice: 0, 6 %}

<div class="featured-grid">
  {% for p in featured %}
    {% assign start = p.dates.start | default: p.start_date %}
    {% assign end   = p.dates.end   | default: p.end_date %}
    <a class="feat-card" href="{{ '/projects/#' | append: p.key | relative_url }}">
      {% if p.thumb %}
        <img class="fc-thumb" src="{{ p.thumb | relative_url }}" alt="{{ p.title }} thumbnail">
      {% endif %}
      <div class="fc-body">
        <h3 class="fc-title">{{ p.toc_title | default: p.title }}</h3>
        {% if p.summary_short %}<p class="fc-blurb">{{ p.summary_short }}</p>{% endif %}
        {% if p.stack %}
          <ul class="fc-tags">
            {% for t in p.stack limit:4 %}<li>{{ t }}</li>{% endfor %}
          </ul>
        {% endif %}
        <div class="fc-meta">
          {% if start or end %}
            <span class="fc-dates">
              {{ start | date: "%Y" }}{% if end %}–{{ end | date: "%Y" }}{% endif %}
            </span>
          {% endif %}
          <span class="fc-cta">Read more →</span>
        </div>
      </div>
    </a>
  {% endfor %}
</div>

<p class="more-link">
  <a href="{{ '/projects/' | relative_url }}">See all projects →</a>
</p>
