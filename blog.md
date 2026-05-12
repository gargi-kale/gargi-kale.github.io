---
layout: page
title: Blog
permalink: /blog/
---

{% if site.posts.size == 0 %}
*No posts yet — check back soon.*
{% else %}
<ul class="post-list">
{% for post in site.posts %}
  <li>
    <span class="post-meta">{{ post.date | date: "%b %-d, %Y" }}</span>
    <h3 style="margin: 0.2em 0;"><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
    {% if post.excerpt %}{{ post.excerpt }}{% endif %}
  </li>
{% endfor %}
</ul>
{% endif %}
