---
title: News
permalink: /news/
breadcrumb_path: home
---

{% for post in site.posts %}
  <p>{{ post.date | date: "%d-%b-%Y" }} <a href="{{ post.url }}">{{ post.title }}</a></p>
{% endfor %}
