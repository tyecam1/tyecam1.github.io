---
layout: home
title: Hi, I'm Tye
---

I’m a First-Class (International) Engineering Master's graduate from Cardiff University with a KAIST exchange term.  
I build robotics, reinforcement learning, and systems projects with a focus on clean code, clear documentation, and reproducible results.

## Current Work
{% assign current = site.data.projects | where: "status", "current" %}
<ul>
{% for p in current %}
  <li><strong>{{ p.title }}</strong> — {{ p.summary_short }}</li>  
{% endfor %}
</ul>

## Featured Projects
{% assign featured = site.data.projects | where: "featured", true %}
{% for p in featured %}
### {{ p.title }}
{% if p.image %}![{{ p.title }}]({{ p.image }}){% endif %}  
<strong>Stack:</strong> {{ p.stack | join: " · " }}  
<strong>Summary:</strong> {{ p.summary_short }}  
{% if p.repo_url %}<strong>Repo:</strong> <a href="{{ p.repo_url }}">{{ p.repo_url }}</a>{% endif %}

---
{% endfor %}

## About / Contact
- Based in Isle of Wight, UK (Europe/London)  
- Open to freelance and full-time roles in robotics, reinforcement learning, and systems engineering  
- <a href="mailto:tyecameron@hotmail.co.uk">tyecameron@hotmail.co.uk</a> · <a href="https://github.com/tyecam1">GitHub @tyecam1</a> · <a href="https://www.linkedin.com/in/tye-cameron-866aa2203/">LinkedIn</a>
