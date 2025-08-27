---
layout: page
title: ""          # hide the default page title
permalink: /
class: is-home
---

<section class="home-hero compact">
  <div class="hh-inner">
    <h1 class="hh-title">Learning to build reliable robotics & RL systems</h1>
    <p class="hh-tag">
      I’m a recent master’s graduate building small, honest systems to improve my judgment —
      aiming for safe control, clear observability, and work others can reproduce.
    </p>
    <ul class="hh-pills">
      <li>Control & perception</li>
      <li>RL training + evaluation</li>
      <li>Reproducible experiments</li>
    </ul>
  </div>
</section>

## What I’m focusing on now
- Reproducible RL pipeline with a live metrics/video dashboard.
- A rebuildable CUDA dev box (Ansible + dotfiles) for consistent experiments.
- Human–robot collaboration planning (safe RL, intent estimation).

<h2>Skills snapshot</h2>
<ul class="skills-list">
  <li>Python</li>
  <li>C++</li>
  <li>PyTorch</li>
  <li>ROS</li>
  <li>Control</li>
  <li>Perception (RGB-D/LiDAR)</li>
  <li>SLAM/VSLAM</li>
  <li>CUDA/Docker</li>
  <li>Linux/Ansible</li>
  <li>MATLAB/Simulink</li>
  <li>RL (PPO/IL)</li>
  <li>Reproducibility & CI</li>
</ul>

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
    <article class="feat-card">
      {% if p.thumb %}
        <img class="fc-thumb" src="{{ p.thumb | relative_url }}" alt="{{ p.title }} thumbnail">
      {% endif %}
      <div class="fc-body">
        <h3 class="fc-title">
          <a class="fc-title-link" href="{{ '/projects/#' | append: p.key | relative_url }}">
            {{ p.toc_title | default: p.title }}
          </a>
        </h3>
        {% if p.summary_short %}
          <p class="fc-blurb">{{ p.summary_short | strip_html }}</p>
        {% endif %}
        {% if p.stack %}
          <ul class="fc-tags">
            {% for t in p.stack limit:4 %}<li>{{ t }}</li>{% endfor %}
          </ul>
        {% endif %}
        <div class="fc-meta">
          {% if start or end %}
            <span class="fc-dates">{{ start | date: "%Y" }}{% if end %}–{{ end | date: "%Y" }}{% endif %}</span>
          {% endif %}
          <a class="btn btn-sm" href="{{ '/projects/#' | append: p.key | relative_url }}">Case study</a>
        </div>
      </div>
    </article>
  {% endfor %}
</div>

<p class="more-link">
  <a href="{{ '/projects/' | relative_url }}">See all projects →</a>
</p>
