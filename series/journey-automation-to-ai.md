---
layout: page
title: "From Automation to AI – A Practitioner's Journey"
permalink: /series/journey-automation-to-ai/
excerpt: "A hands-on series guiding automation engineers through the essential concepts, tools, and mindset shifts needed to transition from automation to artificial intelligence."
---

{% assign series_posts = site.posts 
  | where: "series", "From Automation to AI – A Practitioner's Journey" 
  | sort: "series_order" %}

{% include post-list.html posts=series_posts %}
