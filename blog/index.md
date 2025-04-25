---
layout: default
title: "All Blogs"
# Ensure pagination is enabled here if you want it
pagination:
  enabled: true
  collection: posts
  per_page: 5 # Optional: Set posts per page
# excerpt_separator: # Optional: Define how excerpts are created
---

<div class="content">
  <h1>{{ page.title }}</h1>
  <p>Welcome to the CodifyMe blog! Here, you'll find a collection of articles, tutorials, and insights on Infrastructure as Code (IaC), DevOps practices, and Cloud Automation.</p>
</div>

<hr>

<div>
  {% assign posts_to_show = site.posts %}
  {% if paginator %}
    {% assign posts_to_show = paginator.posts %}
  {% endif %}

  {% if posts_to_show.size > 0 %}
    {% for post in posts_to_show %}
      <div class="card mb-5">
        <div class="card-content">
          <p class="title is-4 mb-6">
            <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
          </p>
          <p class="subtitle is-6 has-text-grey mb-3">
            {{ post.date | date: "%B %d, %Y" }}
            {% if post.author %} | By {{ post.author }}{% endif %}
          </p>

          {% if post.excerpt %}
            <div class="content">
              {{ post.excerpt | strip_html | truncatewords: 50 }}
            </div>
          {% endif %}

          {% if post.tags.size > 0 %}
          <div class="tags mb-4">
            {% for tag in post.tags %}
              {% include tag.html tag=tag style="is-link is-light is-rounded is-small" %}
            {% endfor %}
          </div>
          {% endif %}

          <a href="{{ post.url | relative_url }}" class="button is-link is-light is-small">Read More</a>

        </div>
      </div>
    {% endfor %}
  {% else %}
      <p>No posts found.</p>
  {% endif %}
</div>

{% comment %} Styled Pagination using Bulma classes {% endcomment %}
{% if paginator.total_pages > 1 %}
<nav class="pagination is-centered" role="navigation" aria-label="pagination" style="margin-top: 3rem;">
  {% if paginator.previous_page %}
    <a href="{{ paginator.previous_page_path | relative_url }}" class="pagination-previous">Previous</a>
  {% else %}
    <a class="pagination-previous" title="This is the first page" disabled>Previous</a>
  {% endif %}

  {% if paginator.next_page %}
    <a href="{{ paginator.next_page_path | relative_url }}" class="pagination-next">Next page</a>
  {% else %}
    <a class="pagination-next" title="This is the last page" disabled>Next page</a>
  {% endif %}

  <ul class="pagination-list">
    {% for page in (1..paginator.total_pages) %}
      {% if page == paginator.page %}
        <li><a class="pagination-link is-current" aria-label="Page {{ page }}" aria-current="page">{{ page }}</a></li>
      {% elsif page == 1 %}
        {% assign first_page_path = paginator.previous_page_path | default: page.url | relative_url | replace: '/page2', '/' %}
         <li><a href="{{ first_page_path }}" class="pagination-link" aria-label="Goto page {{ page }}">{{ page }}</a></li>
      {% else %}
         {% assign page_path = site.paginate_path | relative_url | replace: ':num', page %}
         <li><a href="{{ page_path }}" class="pagination-link" aria-label="Goto page {{ page }}">{{ page }}</a></li>
      {% endif %}
    {% endfor %}
  </ul>
</nav>
{% endif %}