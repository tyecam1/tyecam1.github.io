---
layout: default
title: ""
class: home
---

<style>
/* -------- Home-only styles (scoped to .home) -------- */
.home .wrap { max-width: 1080px; }
.home .hero {
  margin: 2.5rem 0 2rem;
  display: grid;
  gap: 1.25rem;
}
.home .eyebrow {
  font-size: .9rem;
  letter-spacing: .06em;
  text-transform: uppercase;
  opacity: .8;
}
.home .hero h1 {
  font-size: clamp(1.6rem, 2.6vw, 2.2rem);
  line-height: 1.2;
  margin: .25rem 0 .25rem;
}
.home .lead {
  font-size: 1.03rem;
  max-width: 72ch;
}
.home .quick-points { margin: .5rem 0 0; }
.home .quick-points li { margin: .15rem 0; }

.home .meta {
  display: flex; flex-wrap: wrap; gap: .7rem 1rem;
  font-size: .95rem; opacity: .9;
}
.home .meta span { white-space: nowrap; }

.home section { margin: 2.25rem 0 0; }

.home .pill-list {
  display: flex; flex-wrap: wrap; gap: .5rem .6rem;
  padding: 0; list-style: none;
}
.home .pill {
  padding: .35rem .6rem; border-radius: 999px;
  border: 1px solid var(--border, #e3e3e3);
  font-size: .92rem;
}

.home .grid {
  display: grid;
  gap: 1rem;
  grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
}
.home .grid-card {
  border: 1px solid var(--border, #e3e3e3);
  border-radius: 12px;
  padding: .9rem .95rem;
  background: var(--card, #fff);
}
.home .grid-card h3 { margin: 0 0 .4rem; font-size: 1.02rem; }
.home .grid-card p { margin: 0; font-size: .95rem; opacity: .95; }

.home .featured-head { margin-top: 2.25rem; }
.home .cta-row { margin-top: .75rem; }
.home .btn {
  display: inline-block; padding: .55rem .9rem; border-radius: 8px;
  border: 1px solid var(--border, #e3e3e3); text-decoration: none;
}
</style>

<div class="wrap">

  <section class="hero">
    <div class="eyebrow">Learning to build reliable robotics & RL systems</div>
    <h1>Hi, I’m Tye — a recent master’s graduate who ships small, honest systems and measures them.</h1>
    <p class="lead">
      I focus on control, perception and reinforcement learning; my goal is safe control, clear observability,
      and work others can reproduce. I like humble builds that work in the real world and improve with data.
    </p>
    <ul class="quick-points">
      <li>• Control & perception (ROS, VSLAM/RTAB-Map, IMU fusion)</li>
      <li>• RL training & evaluation (PPO/IL, curriculum, metrics)</li>
      <li>• Reproducibility (Ansible, dotfiles, CI; tidy notebooks & reports)</li>
    </ul>
    <div class="meta">
      <span>🎓 MEng (International), First Class</span>
      <span>📍 Isle of Wight, UK</span>
      <span>🔎 Open to grad/junior roles in robotics / controls / RL</span>
    </div>
  </section>

  <section aria-labelledby="focus-now">
    <h2 id="focus-now">What I’m focusing on now</h2>
    <ul class="quick-points">
      <li>• A reproducible RL pipeline with a lightweight live metrics/video dashboard.</li>
      <li>• A rebuildable CUDA dev box (Ansible + dotfiles) for consistent experiments.</li>
      <li>• Human–robot collaboration planning (safe RL, intent estimation).</li>
    </ul>
  </section>

  <section aria-labelledby="skills">
    <h2 id="skills">Skills snapshot</h2>
    <ul class="pill-list" role="list">
      <li class="pill">Python</li>
      <li class="pill">C++</li>
      <li class="pill">PyTorch</li>
      <li class="pill">ROS (Noetic)</li>
      <li class="pill">Control (state-space, digital)</li>
      <li class="pill">Perception (RGB-D/LiDAR)</li>
      <li class="pill">SLAM / VSLAM</li>
      <li class="pill">CUDA / Docker</li>
      <li class="pill">Linux / Ansible</li>
      <li class="pill">MATLAB / Simulink</li>
      <li class="pill">RL (PPO / IL)</li>
      <li class="pill">Reproducibility & CI</li>
    </ul>
  </section>

  <section aria-labelledby="evidence">
    <h2 id="evidence">Signals for hiring managers</h2>
    <div class="grid">
      <article class="grid-card">
        <h3>Hands-on proof</h3>
        <p>Wearable navigation system with RGB-D perception, haptic actuation, and user trials; plus a full RL quadruped project.</p>
      </article>
      <article class="grid-card">
        <h3>Measurement mindset</h3>
        <p>Defined KPIs, ran experiments, and analysed results (success rate, collisions, odometry loss, reaction time).</p>
      </article>
      <article class="grid-card">
        <h3>Production habits</h3>
        <p>ROS packages, clean nodes, reproducible setups (Ansible/dotfiles), and tidy reports/videos for stakeholders.</p>
      </article>
      <article class="grid-card">
        <h3>Team & humility</h3>
        <p>Happy to start small, learn fast, and help wherever useful—from perception plumbing to experiment cleanup.</p>
      </article>
    </div>
  </section>

  <!-- ===== Featured projects (kept close to your current structure) ===== -->
  <section class="featured-head" aria-labelledby="featured">
    <h2 id="featured">Featured projects</h2>

    <div class="cards">
      {% assign featured = site.data.projects | where: "featured", true | sort: "dates.end" | reverse %}
      {% for p in featured %}
      <article class="project-card">
        <h3><a href="/projects/#{{ p.key }}">{{ p.toc_title | default: p.title }}</a></h3>
        {% if p.summary_short %}
          <p>{{ p.summary_short }}</p>
        {% endif %}
        {% if p.stack %}
        <ul class="pill-list" aria-label="Tech stack">
          {% for s in p.stack limit:5 %}
          <li class="pill">{{ s }}</li>
          {% endfor %}
        </ul>
        {% endif %}
      </article>
      {% endfor %}
    </div>

    <div class="cta-row">
      <a class="btn" href="/projects/">See all projects →</a>
    </div>
  </section>

</div>
