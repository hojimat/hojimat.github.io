---
layout: cleanmode 
title: Blog
---

<div class="container content col-md-6 mx-auto py-5">
    <div class="posts">
    {% for post in site.posts %}
    {% if post.categ == 'note' and post.lang == 'english' %}
    <div class="post-preview">
        <a href="{{ site.baseurl }}{{ post.url }}">
            <h2 class="post-title">{{ post.title }}</h2>
        </a>
        <p class="post-meta">
            Posted on {{ post.date | date_to_string }}
        </p>
    </div>
    <!-- Divider-->
    <hr class="my-4" />
    {% endif %}
    {% endfor %}
    </div>
</div>