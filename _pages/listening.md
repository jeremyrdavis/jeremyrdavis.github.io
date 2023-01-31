---
layout: listening
title: Listening
description: What I've Been Listening To
subtitle: What I've Been Listening To
featured_image: /images/social.jpg
---

{% for week in site.data.streaming %}
  <h3>Week of: {{ week.date }}</h3>
  | Album                | Artist                       |
  |----------------------|------------------------------|
    {% for album in week.albums %}
    | {{album.title}} | {{ album.artist }} |
    {% endfor %}
{% endfor %}