---
layout: page
title: ""                # hide the default page title
permalink: /
class: is-home
---

<section class="home-hero">
  <div class="hh-inner">
    <h1 class="hh-title">Learning to build reliable robotics & RL systems</h1>
    <p class="hh-tag">
      I’m a recent master’s graduate taking on real projects to improve my judgment—aiming for
      safe control, clear observability, and work others can reproduce.
    </p>
    <ul class="hh-pills">
      <li>Control & perception</li>
      <li>RL training + evaluation</li>
      <li>Reproducible experiments</li>
    </ul>
  </div>
</section>

## What I’m focusing on now:
- Integrated RL pipeline with live telemetry and config-first runs.
- Arch Linux dev environment automation (CUDA, Docker, Ansible).
- Human Robot Collaboration (/HRI) research planning (safe RL, intent estimation).

## Skills snapshot
ROS • Python • C++ • RL (PPO/IL) • Digital Control • SLAM/VSLAM • Perception (RGB-D/LiDAR) • Docker/CUDA • Linux/Ansible • MATLAB/ Simulink

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
