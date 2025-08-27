---
layout: default
title: Home
class: home
---

<style>
/* Home-only gallery styling (safe: scoped to .home) */
.home .feat-gallery{
  display:flex; gap:.5rem; overflow-x:auto; padding-bottom:.25rem;
  scroll-snap-type:x mandatory;
}
.home .feat-gallery img{
  height:140px; width:auto; border-radius:8px;
  border:1px solid rgba(0,0,0,.12);
  display:block; scroll-snap-align:center;
}
@media (prefers-color-scheme: dark){
  .home .feat-gallery img{ border-color: rgba(255,255,255,.18); }
}
</style>

<div class="wrap">

  <!-- HERO -->
  <section>
    <p class="eyebrow">Reliable robotics & RL — small builds, honest measures</p>
    <h1>I’m Tye, a recent MEng graduate focused on control, perception and reinforcement learning.</h1>
    <p>
      I build tidy, reproducible systems aimed at safe control, clear observability, and results others can reproduce.
      I like humble builds that work in the real world and improve with data.
    </p>
    <ul>
      <li>Control & perception with ROS, VSLAM/RTAB-Map, IMU fusion</li>
      <li>RL training & evaluation (PPO/IL, curriculum, metrics & dashboards)</li>
      <li>Reproducibility (Ansible, dotfiles, CI; clean reports & notebooks)</li>
    </ul>
  </section>

  <!-- CURRENT FOCUS -->
  <section>
    <h2>What I’m focusing on now</h2>
    <ul>
      <li>Reproducible RL pipeline with a lightweight live metrics/video dashboard.</li>
      <li>Rebuildable CUDA dev box (Ansible + dotfiles) for consistent experiments.</li>
      <li>Human–robot collaboration planning (safe RL, intent estimation).</li>
    </ul>
  </section>

  <!-- SKILLS -->
  <section>
    <h2>Skills snapshot</h2>
    <p>
      Python · C++ · PyTorch · ROS (Noetic) · Control (state-space, digital) ·
      Perception (RGB-D/LiDAR) · SLAM/VSLAM · CUDA/Docker · Linux/Ansible ·
      MATLAB/Simulink · RL (PPO/IL) · Reproducibility & CI
    </p>
  </section>

  <!-- HIRING SIGNALS -->
  <section>
    <h2>Signals for hiring managers</h2>
    <h3>Hands-on proof</h3>
    <p>Wearable navigation system with RGB-D perception, haptic actuation, and user trials; plus a full RL quadruped project.</p>

    <h3>Measurement mindset</h3>
    <p>Defined KPIs and analysed results (success rate, collisions, reaction time, odometry loss) to guide iteration.</p>

    <h3>Production habits</h3>
    <p>ROS packages, clean nodes, reproducible setups (Ansible/dotfiles), and reports/videos suitable for stakeholders.</p>

    <h3>Team & humility</h3>
    <p>Happy to start small, learn fast, and help wherever useful—from perception plumbing to experiment cleanup.</p>
  </section>

  <!-- FEATURED PROJECTS (cards preserved; add small gallery) -->
  <section>
    <h2>Featured projects</h2>

    <div class="cards">
      {% assign featured = site.data.projects | where: "featured", true | sort: "dates.end" | reverse %}
      {% for p in featured %}
      <article class="project-card">
        {% if p.media and (p.media.hero or p.media.gallery) %}
        <div class="feat-gallery" aria-label="Project images">
          {% if p.media.hero and p.media.hero.src %}
            <img src="{{ p.media.hero.src }}" alt="{{ p.media.hero.alt | default: p.title }}" loading="lazy">
          {% endif %}
          {% if p.media.gallery %}
            {% for g in p.media.gallery %}
              {% if g.src %}
                <img src="{{ g.src }}" alt="{{ g.alt | default: p.title }}" loading="lazy">
              {% endif %}
            {% endfor %}
          {% endif %}
        </div>
        {% endif %}

        <h3><a href="/projects/#{{ p.key }}">{{ p.toc_title | default: p.title }}</a></h3>
        {% if p.summary_short %}
          <p>{{ p.summary_short }}</p>
        {% endif %}

        {% if p.stack %}
        <ul class="tags">
          {% for s in p.stack limit:6 %}
            <li class="tag">{{ s }}</li>
          {% endfor %}
          {% if p.stack.size > 6 %}
            <li class="tag">+{{ p.stack.size | minus: 6 }}</li>
          {% endif %}
        </ul>
        {% endif %}
      </article>
      {% endfor %}
    </div>

    <p style="margin-top:.75rem;">
      <a href="/projects/">See all projects →</a> &nbsp;·&nbsp; <a href="/about/">About me →</a>
    </p>
  </section>

</div>
