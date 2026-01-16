---
layout: page
title: Articles
icon: fas fa-blog
order: 1
---

{% assign blog_posts = site.posts | where_exp: "post", "post.series == nil" %}

{% include post-list.html posts=blog_posts %}
