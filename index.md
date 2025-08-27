---
layout: default
title: Home
class: home
---

<style>
/* =========================
   Home page (scoped styles)
   ========================= */
.home {
  --border: #e5e7eb;      /* light border */
  --muted:  #6b7280;      /* muted text */
  --card:   #ffffff;      /* card bg  */
}
@media (prefers-color-scheme: dark) {
  .home { --border:#2f343a; --muted:#a1a1aa; --card:#121417; }
}

/* layout */
.home .wrap { max-width: 1100px; margin: 0 auto; }
.home section { margin-top: 2.0rem; }

/* hero */
.home .eyebrow {
  font-size:.9rem; letter-spacing:.06em; text-transform:uppercase; color:var(--muted);
}
.home .hero {
  margin-top: 2.2rem;
  display:grid; gap:1.25rem;
  grid-template-columns: 1.15fr .85fr;
}
@media (max-width: 860px){ .home .hero { grid-template-columns: 1fr; } }
.home .title { font-size:clamp(1.7rem,2.6vw,2.2rem); line-height:1.2; margin:.25rem 0 .35rem; }
.home .lead  { font-size:1.05rem; max-width:72ch; }

/* cards + pills */
.home .card {
  background:var(--card);
  border:1px solid var(--border);
  border-radius:12px;
  padding:1rem 1.05rem;
}
.home .pill-list { display:flex; flex-wrap:wrap; gap:.5rem .6rem; list-style:none; padding:0; margin:.3rem 0 0; }
.home .pill { border:1px solid var(--border); border-radius:999px; padding:.35rem .6rem; font-size:.92rem; }

/* stat grid */
.home .stats { display:grid; gap: .8rem; grid-template-columns:repeat(2,1fr); }
@media (max-width: 560px){ .home .stats { grid-template-columns: 1fr; } }
.home .stat h4 { margin:0 0 .35rem; font-size:.95rem; color:var(--muted); }
.home .stat .big { font-size:1.15rem; }

/* “signals” grid */
.home .grid { display:grid; gap:1rem; grid-template-columns:repeat(auto-fill,minmax(240px,1fr)); }
.home .grid h3 { margin:.1rem 0 .35rem; font-size:1.02rem; }
.home .grid p  { margin:0; font-size:.95rem; }

/* featured projects preview (keeps your data; just gives home a neat frame) */
.home .featured { margin-top: 2.25rem; }
.home .project-cards { display:grid; gap:1rem; grid-template-columns:repeat(auto-fill,minmax(280px,1fr)); }
.home .project-card h3 { margin:.15rem 0 .35rem; font-size:1.02rem; }
.home .cta { margin-top:.9rem; }
.home .btn { display:inline-block; padding:.55rem .9rem; border-radius:8px; border:1px solid var(--border); text-decoration:none; }

/* lists */
.home .list { margin:.5rem 0 0; padding-left:1.1rem; }
</style>

<div class="wrap">

  <!-- HERO -->
  <section class="hero">
    <div>
      <div class="eyebrow">Reliable robotics & RL — small builds, honest measures</div>
      <h1 class="title">I’m Tye, a recent MEng grad focused on control, perception and reinforcement learning.</h1>
      <p class="lead">
        I build tidy, reproducible systems aimed at safe control, clear observability, and results others can reproduce.
        I prefer humble builds that work in the real world and improve with data.
      </p>
      <ul class="list">
        <li>Control & perception with ROS, VSLAM/RTAB-Map, IMU fusion</li>
        <li>RL training & evaluation (PPO/IL, curriculum, metrics & dashboards)</li>
        <li>Reproducibility (Ansible, dotfiles, CI; clean reports & notebooks)</li>
      </ul>
    </div>

    <aside class="card">
      <h2 style="margin:.1rem 0 .6rem; font-size:1.05rem;">At a glance</h2>
      <div class="stats">
        <div class="stat">
          <h4>Capstone systems</h4>
          <div class="big">Wearable Navigation • RL Quadruped</div>
        </div>
        <div class="stat">
          <h4>Perception stack</h4>
          <div class="big">RGB-D (RTAB-Map) + LiDAR (Hector-SLAM)</div>
        </div>
        <div class="stat">
          <h4>Evaluation mindset</h4>
          <div class="big">Success, collisions, reaction time, odom loss</div>
        </div>
        <div class="stat">
          <h4>Background</h4>
          <div class="big">MEng (International), First Class</div>
        </div>
      </div>

      <ul class="pill-list" aria-label="Core tools">
        <li class="pill">Python</li><li class="pill">C++</li><li class="pill">PyTorch</li>
        <li class="pill">ROS Noetic</li><li class="pill">CUDA/Docker</li><li class="pill">Linux/Ansible</li>
      </ul>
    </aside>
  </section>

  <!-- CURRENT FOCUS -->
  <section aria-labelledby="focus-now">
    <h2 id="focus-now">What I’m focusing on now</h2>
    <div class="card">
      <ul class="list">
        <li>Reproducible RL pipeline with lightweight live metrics/video dashboard.</li>
        <li>Rebuildable CUDA dev box (Ansible + dotfiles) for consistent experiments.</li>
        <li>Human–robot collaboration planning (safe RL, intent estimation).</li>
      </ul>
    </div>
  </section>

  <!-- SKILLS -->
  <section aria-labelledby="skills">
    <h2 id="skills">Skills snapshot</h2>
    <div class="card">
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
    </div>
  </section>

  <!-- HIRING SIGNALS -->
  <section aria-labelledby="signals">
    <h2 id="signals">Signals for hiring managers</h2>
    <div class="grid">
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

  <!-- FEATURED PROJECTS (uses your data; minimal change) -->
  <section class="featured" aria-labelledby="featured">
    <h2 id="featured">Featured projects</h2>
    <div class="project-cards">
      {% assign featured = site.data.projects | where: "featured", true | sort: "dates.end" | reverse %}
      {% for p in featured %}
      <article class="project-card card">
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

    <div class="cta">
      <a class="btn" href="/projects/">See all projects →</a>
      <a class="btn" href="/about/">About me →</a>
    </div>
  </section>

</div>
