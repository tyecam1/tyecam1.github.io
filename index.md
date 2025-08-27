---
layout: default
title: Home
class: home
---

<div class="home-wrap">

  <!-- HERO -->
  <section class="home-hero">
    <div class="home-hero-left">
      <p class="home-eyebrow">Reliable robotics & RL — small builds, honest measures</p>
      <h1 class="home-title">I’m Tye, a recent MEng graduate focused on control, perception and reinforcement learning.</h1>
      <p class="home-lead">
        I build tidy, reproducible systems aimed at safe control, clear observability, and results others can reproduce.
        I like humble builds that work in the real world and improve with data.
      </p>

      <ul class="home-bullets">
        <li>Control & perception with ROS, VSLAM/RTAB-Map, IMU fusion</li>
        <li>RL training & evaluation (PPO/IL, curriculum, metrics & dashboards)</li>
        <li>Reproducibility (Ansible, dotfiles, CI; clean reports & notebooks)</li>
      </ul>
    </div>

    <aside class="home-hero-card card">
      <h2 class="card-title">At a glance</h2>
      <div class="home-stat-grid">
        <div class="stat">
          <div class="label">Capstone systems</div>
          <div class="value">Wearable Navigation · RL Quadruped</div>
        </div>
        <div class="stat">
          <div class="label">Perception stack</div>
          <div class="value">RGB-D (RTAB-Map) + LiDAR (Hector-SLAM)</div>
        </div>
        <div class="stat">
          <div class="label">Evaluation mindset</div>
          <div class="value">Success, collisions, reaction time, odom loss</div>
        </div>
        <div class="stat">
          <div class="label">Background</div>
          <div class="value">MEng (International), First Class</div>
        </div>
      </div>

      <ul class="pill-list" aria-label="Core tools">
        <li class="pill">Python</li>
        <li class="pill">C++</li>
        <li class="pill">PyTorch</li>
        <li class="pill">ROS Noetic</li>
        <li class="pill">CUDA/Docker</li>
        <li class="pill">Linux/Ansible</li>
      </ul>
    </aside>
  </section>

  <!-- CURRENT FOCUS -->
  <section class="home-section">
    <h2>What I’m focusing on now</h2>
    <div class="card">
      <ul class="home-bullets">
        <li>Reproducible RL pipeline with a lightweight live metrics/video dashboard.</li>
        <li>Rebuildable CUDA dev box (Ansible + dotfiles) for consistent experiments.</li>
        <li>Human–robot collaboration planning (safe RL, intent estimation).</li>
      </ul>
    </div>
  </section>

  <!-- SKILLS -->
  <section class="home-section">
    <h2>Skills snapshot</h2>
    <div class="card">
      <!-- Reuse Projects page “chips” vibe -->
      <div class="stack-list" role="list" aria-label="Tech stack">
        <span class="stack-item">Python</span>
        <span class="stack-item">C++</span>
        <span class="stack-item">PyTorch</span>
        <span class="stack-item">ROS (Noetic)</span>
        <span class="stack-item">Control (state-space, digital)</span>
        <span class="stack-item">Perception (RGB-D/LiDAR)</span>
        <span class="stack-item">SLAM / VSLAM</span>
        <span class="stack-item">CUDA / Docker</span>
        <span class="stack-item">Linux / Ansible</span>
        <span class="stack-item">MATLAB / Simulink</span>
        <span class="stack-item">RL (PPO / IL)</span>
        <span class="stack-item">Reproducibility & CI</span>
      </div>
    </div>
  </section>

  <!-- HIRING SIGNALS -->
  <section class="home-section">
    <h2>Signals for hiring managers</h2>
    <div class="home-grid">
      <article class="card">
        <h3>Hands-on proof</h3>
        <p>Wearable navigation system with RGB-D perception, haptic actuation, and user trials; plus a full RL quadruped project.</p>
      </article>
      <article class="card">
        <h3>Measurement mindset</h3>
        <p>Defined KPIs and analysed results (success rate, collisions, reaction time, odometry loss) to guide iteration.</p>
      </article>
      <article class="card">
        <h3>Production habits</h3>
        <p>ROS packages, clean nodes, reproducible setups (Ansible/dotfiles), and reports/videos suitable for stakeholders.</p>
      </article>
      <article class="card">
        <h3>Team & humility</h3>
        <p>Happy to start small, learn fast, and help wherever useful—from perception plumbing to experiment cleanup.</p>
      </article>
    </div>
  </section>

  <!-- FEATURED PROJECTS (kept as real cards) -->
  <section class="home-section">
    <h2>Featured projects</h2>

    <div class="home-feat-grid">
      {% assign featured = site.data.projects | where: "featured", true | sort: "dates.end" | reverse %}
      {% for p in featured %}
      <article class="home-feat-card card">
        {% if p.media and p.media.hero and p.media.hero.src %}
          <figure class="home-feat-hero">
            <img src="{{ p.media.hero.src }}" alt="{{ p.media.hero.alt | default: p.title }}" loading="lazy" />
          </figure>
        {% endif %}

        <header class="home-feat-head">
          <h3 class="home-feat-title">
            <a href="/projects/#{{ p.key }}">{{ p.toc_title | default: p.title }}</a>
          </h3>
          {% if p.dates and p.dates.end %}
            <div class="home-feat-date">{{ p.dates.end | date: "%b %Y" }}</div>
          {% endif %}
        </header>

        {% if p.summary_short %}
          <p class="home-feat-summary">{{ p.summary_short }}</p>
        {% endif %}

        {% if p.stack %}
          {% assign max_stack = 6 %}
          <div class="stack-list" aria-label="Tech stack">
            {% for s in p.stack %}
              {% if s and s != '' and forloop.index <= max_stack %}
                <span class="stack-item">{{ s }}</span>
              {% endif %}
            {% endfor %}
            {% if p.stack.size > max_stack %}
              <span class="stack-item stack-more">+{{ p.stack.size | minus: max_stack }}</span>
            {% endif %}
          </div>
        {% endif %}
      </article>
      {% endfor %}
    </div>

    <div class="home-cta">
      <a class="btn-link" href="/projects/">See all projects →</a>
      <a class="btn-link" href="/about/">About me →</a>
    </div>
  </section>

</div>
