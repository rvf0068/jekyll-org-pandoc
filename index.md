---
layout: home
title: Home
---

Welcome to my blog! This is a Jekyll site built from Org-mode files, converted to Markdown using Pandoc.

## Recent Posts

{% for post in site.posts %}
- [{{ post.title }}]({{ post.url | relative_url }}) - {{ post.date | date: "%B %d, %Y" }}
{% endfor %}
