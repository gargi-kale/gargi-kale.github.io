---
layout: page
title: Projects
permalink: /projects/
---

A selection of things I've worked on. Code is on [GitHub](https://github.com/gargi-kale).

<div class="project-grid">
{% for project in site.data.projects %}
  <article class="project-card">
    <h3 class="project-title">
      {% if project.url %}<a href="{{ project.url }}">{{ project.title }}</a>{% else %}{{ project.title }}{% endif %}
    </h3>
    <p>{{ project.description }}</p>
    {% if project.tags %}
    <p class="project-tags">
      {% for tag in project.tags %}<span class="tag">{{ tag }}</span>{% endfor %}
    </p>
    {% endif %}
  </article>
{% endfor %}
</div>
