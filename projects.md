---
layout: page
title: Projects
permalink: /projects/
---

## Current
{% assign current = site.data.projects | where: "status", "current" %}
{% for p in current %}
### {{ p.title }} ({{ p.year }})
{% if p.image %}![{{ p.title }}]({{ p.image }}){% endif %}<br>
<strong>Stack:</strong> {{ p.stack | join: " · " }}<br>  
<strong>Overview:</strong> {{ p.summary_long }}  <br>
{% if p.repo_url %}<strong>Repo:</strong> <a href="{{ p.repo_url }}">{{ p.repo_url }}</a>{% else %}<strong>Repo:</strong> Coming soon{% endif %}

---
{% endfor %}

## Past
{% assign past = site.data.projects | where: "status", "past" %}
{% for p in past %}
### {{ p.title }} ({{ p.year }})
{% if p.image %}![{{ p.title }}]({{ p.image }}){% endif %}<br>
<strong>Stack:</strong> {{ p.stack | join: " · " }}<br>  
<strong>Overview:</strong> {{ p.summary_long }}<br>  
{% if p.repo_url %}<strong>Repo:</strong> <a href="{{ p.repo_url }}">{{ p.repo_url }}</a>{% endif %}

---
{% endfor %}
