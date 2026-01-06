---
title: "Home"
layout: page
permalink: /
hide_hero: true
show_banner: false
---

<!-- Hero Section -->
<section class="hero is-primary is-medium">
  <div class="hero-body">
    <div class="container">
      <div class="columns is-vcentered">
        <div class="column is-8">
          <h1 class="title is-1">Welcome to CodifyMe</h1>
          <p class="subtitle is-4">
            Learn Infrastructure as Code, DevOps, and Cloud Automation through real-world, actionable tutorials. Built by engineer—for engineers.
          </p>
          <a href="javascript:void(0)" class="button is-light is-medium mt-3" onclick="openSubscribeModal()">📩 Subscribe for Updates</a>
        </div>
        <div class="column is-4">
          <figure class="image is-4by3">
            <img src="{{ site.baseurl }}/images/hero-image3.png" alt="CodifyMe Logo">
          </figure>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- What You’ll Learn Section -->
<section class="section">
  <div class="container">
    <h2 class="title is-3">🚀 What You’ll Learn</h2>
    <div class="columns">
      <div class="column is-8">
        <ul>
          <li>✅ Build and manage infrastructure using <strong>Terraform</strong>, <strong>Ansible</strong>.</li>
          <li>✅ Work confidently across <strong>AWS</strong>, <strong>Azure</strong>, and <strong>GCP</strong>.</li>
          <li>✅ Automate end-to-end delivery with <strong>CI/CD pipelines</strong>.</li>
          <li>✅ Solve practical challenges in cloud infrastructure and automation.</li>
        </ul>
      </div>
    </div>
  </div>
</section>

<!-- Latest Posts -->
<section class="section has-background-light">
  <div class="container">
    <h2 class="title is-3">📝 Latest Posts</h2>
    <div class="columns is-multiline">
      {% for post in site.posts limit:3 %}
      <div class="column is-12-mobile is-6-tablet is-4-desktop">
        <div class="card">
          <div class="card-content">
            <h3 class="title is-5"><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h3>
            <p class="is-size-6">{{ post.excerpt | strip_html | truncate: 100 }}</p>
            <a href="{{ site.baseurl }}{{ post.url }}" class="button is-small is-link mt-2">Read More</a>
          </div>
        </div>
      </div>
      {% endfor %}
    </div>
  </div>
</section>

<!-- Featured Series -->
<section class="section">
  <div class="container">
    <h2 class="title is-3">🔥 Featured Series</h2>
    <div class="columns is-multiline">
      {% assign featured_series = site.series | where: "is_series_index", true %}
      {% for series in featured_series %}
      <div class="column is-12-mobile is-6-tablet is-4-desktop">
        <div class="card">
          <div class="card-content">
            <h3 class="title is-5"><a href="{{ site.baseurl }}{{ series.url }}">{{ series.title }}</a></h3>
            <p class="is-size-6">A deep dive into {{ series.title | downcase }} with real-world examples.</p>
            <a href="{{ site.baseurl }}{{ series.url }}" class="button is-small is-primary mt-2">Explore Series</a>
          </div>
        </div>
      </div>
      {% endfor %}
    </div>
  </div>
</section>

<!-- Explore by Category -->
<section class="section has-background-light">
  <div class="container">
    <h2 class="title is-3">🌐 Explore by Category</h2>
    <div class="columns is-multiline">
      <div class="column is-12-mobile is-6-tablet is-4-desktop">
        <div class="card">
          <div class="card-content">
            <h3 class="title is-5"><a href="{{ site.baseurl }}/categories/terraform/">Terraform</a></h3>
            <p class="is-size-6">Modules, tips, and IaC strategies with Terraform.</p>
            <a href="{{ site.baseurl }}/categories/terraform/" class="button is-small is-primary mt-2">Browse Terraform</a>
          </div>
        </div>
      </div>
      <div class="column is-12-mobile is-6-tablet is-4-desktop">
        <div class="card">
          <div class="card-content">
            <h3 class="title is-5"><a href="{{ site.baseurl }}/categories/kubernetes/">Kubernetes</a></h3>
            <p class="is-size-6">From basics to advanced orchestration with K8s.</p>
            <a href="{{ site.baseurl }}/categories/kubernetes/" class="button is-small is-primary mt-2">Browse Kubernetes</a>
          </div>
        </div>
      </div>
      <div class="column is-12-mobile is-6-tablet is-4-desktop">
        <div class="card">
          <div class="card-content">
            <h3 class="title is-5"><a href="{{ site.baseurl }}/categories/cloud-automation/">Cloud Automation</a></h3>
            <p class="is-size-6">Automation strategies across AWS, Azure, and GCP.</p>
            <a href="{{ site.baseurl }}/categories/cloud-automation/" class="button is-small is-primary mt-2">Browse Cloud Automation</a>
          </div>
        </div>
      </div>
      <div class="column is-12-mobile is-6-tablet is-4-desktop">
        <div class="card">
          <div class="card-content">
            <h3 class="title is-5"><a href="{{ site.baseurl }}/categories/ai/">AI & Machine Learning</a></h3>
            <p class="is-size-6">AI concepts for automation engineers and solution architects.</p>
            <a href="{{ site.baseurl }}/categories/ai/" class="button is-small is-primary mt-2">Browse AI</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- Why CodifyMe -->
<section class="section">
  <div class="container">
    <h2 class="title is-3">💡 Why CodifyMe?</h2>
    <p>
      CodifyMe is designed for developers, sysadmins, and cloud architects who want to upskill fast. We focus on simplicity, clarity, and practical application—so you can stop googling and start shipping.
    </p>
  </div>
</section>

<!-- About Me -->
<section class="section">
  <div class="container">
    <h2 class="title is-3">👋 About Me</h2>
    <p>
      I'm a DevOps engineer and cloud architect passionate about simplifying complex infrastructure topics. My mission is to help developers, sysadmins, and cloud architects master Infrastructure as Code (IaC), DevOps practices, and cloud automation.
    </p>
    <p>
      Through CodifyMe, I aim to provide actionable tutorials, real-world examples, and practical insights to bridge the gap between theory and implementation. Whether you're just starting or looking to refine your skills, you're in the right place.
    </p>
    <p>
      <a href="{{ site.baseurl }}/about" class="button is-link is-light mt-3">Learn More About Me</a>
    </p>
  </div>
</section>

<!-- Final CTA -->
<section class="section has-background-light">
  <div class="container has-text-centered">
    <p class="mb-3">📩 Like what you see? Subscribe to get fresh content straight to your inbox.</p>
    <form action="https://your-email-service-provider-url" method="POST" class="subscribe-form" style="max-width: 500px; margin: 0 auto;">
      <div class="field has-addons">
        <div class="control is-expanded">
          <input
            class="input is-medium"
            type="email"
            name="email"
            placeholder="Enter your email address"
            required
          />
        </div>
        <div class="control">
          <button class="button is-primary is-medium" type="submit">
            Subscribe
          </button>
        </div>
      </div>
    </form>
    <p class="is-size-6 mt-3">Happy automating! 🚀</p>
  </div>
</section>

<!-- Subscribe Modal -->
<div id="subscribeModal" class="modal">
  <div class="modal-background" onclick="closeSubscribeModal()"></div>
  <div class="modal-card">
    <header class="modal-card-head">
      <p class="modal-card-title">📩 Subscribe to CodifyMe</p>
      <button class="delete" aria-label="close" onclick="closeSubscribeModal()"></button>
    </header>
    <section class="modal-card-body">
      <form action="https://your-email-service-provider-url" method="POST" class="subscribe-form">
        <div class="field">
          <label class="label">Email Address</label>
          <div class="control">
            <input
              class="input"
              type="email"
              name="email"
              placeholder="Enter your email address"
              required
            />
          </div>
        </div>
        <div class="field">
          <div class="control">
            <button class="button is-primary" type="submit">Subscribe</button>
          </div>
        </div>
      </form>
    </section>
  </div>
</div>
<script>
  // Function to open the Subscribe Modal
  function openSubscribeModal() {
    document.getElementById('subscribeModal').classList.add('is-active');
  }

  // Function to close the Subscribe Modal
  function closeSubscribeModal() {
    document.getElementById('subscribeModal').classList.remove('is-active');
  }
</script>
