---
layout: page
title: Marks Blog
tagline: I learnt something today!
---
{% include JB/setup %}

Hello, and welcome on my blog. I'm currently in the process of setting
this up. Real content will appear soon, feel free to subscribe.

## Here are some of my recent posts

<ul>
  {% for post in site.posts limit: 5 %}
    <li><a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
