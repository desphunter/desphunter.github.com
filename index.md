---
layout: page
title: HomePage
tagline: Supporting tagline
---
{% include JB/setup %}


## First paragraph

This page is initialized with [Jekyll Bootstrap](http://jekyllbootstrap.com)
    
## Posts lists

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>



