---
layout: page
title: Series
icon: fas fa-layer-group
order: 2
---
{% include style.html %}
<div class="post-list">
  {%- assign all_series = site.posts | map: 'series' | uniq | compact -%}
  
  {%- for series_name in all_series -%}
    {%- assign series_posts = site.posts | where: 'series', series_name | sort: 'series_order' -%}
    {%- if series_posts and series_posts.size > 0 -%}
      {%- assign index_page = site.pages | where: "title", series_name | first -%}
      {%- if index_page -%}
        {%- assign series_url = index_page.url | relative_url -%}
      {%- else -%}
        {%- assign series_url = '/series/' | append: series_name | slugify | append: '/' | relative_url -%}
      {%- endif -%}
      <a href="{{ series_url }}" class="post-preview card mb-4 text-decoration-none shadow-sm">
        <div class="card-body">
          <h2 class="h5 mb-2">📘 {{ series_name }}</h2>
          <div class="mb-2 text-muted small">
            <i class="fas fa-list-ul me-1"></i> {{ series_posts.size }} posts
            <span class="ms-2"><i class="fas fa-calendar-alt me-1"></i> {{ series_posts[0].date | date: '%b %d, %Y' }}</span>
            <span class="ms-2"><i class="fas fa-user me-1"></i> {{ series_posts[0].author }}</span>
          </div>
          <p class="mb-0">
            {%- if series_posts[0].description -%}
              {{ series_posts[0].description | truncate: 120 }}
            {%- else -%}
              No description available.
            {%- endif -%}
          </p>
          <div class="mb-2">
            {%- if series_posts[0].tags -%}
              {%- for tag in series_posts[0].tags -%}
                <span class="badge bg-primary me-1">{{ tag }}</span>
              {%- endfor -%}
            {%- endif -%}
          </div>
          <span class="btn btn-outline-primary btn-sm mt-2">Explore Series</span>
        </div>
      </a>
    {%- endif -%}
  {%- endfor -%}
</div>