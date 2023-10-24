---
layout: default 
title: Blog
---

<div class="posts">
 {% for post in site.posts %}
  {% if post.categ == 'blog' and post.lang == 'english' %}
   <div class="post pb-5">
   <h2 class="post-title"><a class="text-dark" href="{{ site.baseurl }}{{ post.url }}">
   {{ post.title }}
   </a></h2>
   <span class="post-date">{{ post.date | date_to_string }}</span>
   {{ post.excerpt }}
   {% if post.excerpt != post.content %}
   <a class="btn btn-light btn-block" href="{{ site.baseurl }}{{ post.url }}">Read more...</a>
   {% endif %}
   </div>
  {% endif %}
 {% endfor %}
</div>
