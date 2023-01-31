---
title: Entries
description: Entries
subtitle: Entries subtitle
featured_image: /images/social.jpg
---

  {% for entry in site.entries %}
  <h3>{{ entry.title }}</h3>
  <h4>{{ entry.subtitle }}</h4>
  <p>{{ entry.excerpt }}... <a href="{{ entry.url }}">Read More</a></p>
  {% endfor %}
