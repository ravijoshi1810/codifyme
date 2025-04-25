---
layout: default
title: "All Series"
---

<h1>{{ page.title }}</h1>
<p>Welcome to the CodifyMe series page! Here, you'll find a collection of series that delve into various topics related to Infrastructure as Code (IaC), DevOps practices, and Cloud Automation.</p>

<hr>

{% comment %} Filter the collection to get only main series pages {% endcomment %}
{% assign main_series_pages = site.series | where: "is_series_index", true %}

<div> {% comment %} Container for the series cards {% endcomment %}
  {% if main_series_pages.size > 0 %}
    {% for series_item in main_series_pages %}
      <div class="card mb-5"> {% comment %} Bulma card with bottom margin {% endcomment %}
        <div class="card-content">
          <p class="title is-4 mb-4"> {% comment %} Series Title (increased margin slightly) {% endcomment %}
            <a href="{{ series_item.url | absolute_url }}">{{ series_item.title }}</a>
          </p>
          {% if series_item.date %} {% comment %} Optional: Display date if available for the series {% endcomment %}
            <p class="subtitle is-6 has-text-grey mb-3">
                {{ series_item.date | date: "%B %d, %Y" }}
            </p>
          {% endif %}

          {% if series_item.description %} {% comment %} Display series description {% endcomment %}
            <div class="content">
              {{ series_item.description | strip_html | truncatewords: 50 }}
            </div>
          {% endif %}

          {% if series_item.tags.size > 0 %} {% comment %} Optional: Display tags if series is tagged {% endcomment %}
          <div class="tags mb-4">
            {% for tag in series_item.tags %}
              {% include tag.html tag=tag style="is-link is-light is-rounded is-small" %}
            {% endfor %}
          </div>
          {% endif %}

          <a href="{{ series_item.url | prepend: site.baseurl | relative_url }}" class="button is-link is-light is-small">View Series</a> {% comment %} Link to the series page {% endcomment %}

        </div>{% comment %} End card-content {% endcomment %}
      </div>{% comment %} End card {% endcomment %}
    {% endfor %}
  {% else %}
      <p>No main series pages found. Ensure 'is_series_index: true' is set in series front matter.</p>
  {% endif %}
</div>

{% comment %} --- Pagination can be added back later if needed --- {% endcomment %}