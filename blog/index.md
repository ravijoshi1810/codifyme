---
layout: default
title: "Blog"
---

<h1>Welcome to the Blog</h1>

<ul>
  {% for post in site.posts %}
    <li><a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

{% if site.paginate %}
  <div class="pagination">
    <a href="{{ paginator.previous_page_path }}">Previous</a>
    <a href="{{ paginator.next_page_path }}">Next</a>
  </div>
{% endif %}
