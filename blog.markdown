---
title: Sample Blog Folder Page
date: 2020-11-27 01:50:00 Z
---

---
layout: home
permalink: /blog/
---

{% for post in site.posts %}
  <article>
    <h2>
      <a href="{{ post.url | prepend: site.baseurl }}">
        {{ post.title }}
      </a>
    </h2>
    <time datetime="{{ post.date | date: "%Y-%m-%d" }}">{{ post.date | date_to_long_string }}</time>
    {{ post.content }}
  </article>
{% endfor %}