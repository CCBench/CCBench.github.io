---
layout: page
title: News
permalink: /news/
---

# News & Updates

{% for post in site.posts %}
<div class="news-item">
  <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
  <p class="post-meta">{{ post.date | date: "%b %-d, %Y" }}</p>
  {{ post.excerpt }}
  <hr>
</div>
{% endfor %}

{% unless site.posts.size > 0 %}
<p><em>No news items yet. Check back soon for updates!</em></p>
{% endunless %}
